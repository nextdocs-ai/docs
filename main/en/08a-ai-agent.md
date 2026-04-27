# AI agent

## Why it matters

Full-text search (see [Search](./08-search.md)) answers "where does
word X appear in the docs". That's fast and useful, but often you
need more:

- Synthesis across several pages into one coherent answer.
- Explanation of connections that aren't written down directly.
- A human-language answer, not a list of fragments.
- **Do something** to the documentation: create a page, fill in a
  section, rename a batch of headings, restructure text.

The Nextdocs AI agent is a **conversational assistant** that reads
your documentation and code, answers, and **takes action**: creates
and edits pages when you ask.

The agent **does not edit code** in repositories — it only reads
them. Documentation is its scope for changes.

## How to open

- **Cmd/Ctrl+K** — opens a unified panel with search. Next to the
  input — an "Ask agent" toggle.
- **A long phrasing** in the search input (natural-language
  question or command) — the panel auto-switches to agent mode.
- Separate page **`/chat`** — the full agent interface: you can
  pick several projects in scope, save threads, see the action
  log.

## What the agent can do

### 1. Search and answers

Acts as smart search across your projects:

- Reads your docs + attached repositories.
- Answers in coherent text with links to sources.
- If there's no answer — honestly says "don't know" instead of
  hallucinating.

Examples:

- "How is our release process set up?"
- "What does `handleUserRegistration` do?"
- "Why do we use Redis for queues instead of RabbitMQ?"
- "What roles do orders have in billing, describe the full flow"

### 2. Creating pages

Ask the agent to write a new page — it creates one.

Examples:

- "Create a page 'Deployment guide' under DevOps and write a
  step-by-step guide based on our existing processes."
- "Add an FAQ page about authorization — collect questions from
  comments and our ADRs."
- "Make a template for new microservices: Overview, API,
  Dependencies, Owner, On-call sections."

What happens:

1. The agent drafts the page structure.
2. Writes a draft based on existing documentation and code.
3. Shows you a **preview**: "I'm about to create page X with this
   content. Confirm?"
4. You hit **Apply** — the page is created. Or **Reject** —
   nothing happens.

The created page lands in history as an `agent_create` action,
authored as "Agent (via @your-name)". You can always roll back.

### 3. Editing pages

Ask the agent to modify an existing page.

Examples:

- "On the `Auth flow` page replace all JWT mentions with OAuth 2.0
  and update the diagram."
- "In the `API endpoints` section add the undocumented endpoint
  `/api/v2/users` — look at the code and describe it."
- "Rewrite the introduction of the `Billing` page — it's outdated
  and doesn't mention the new trial-period logic."
- "Merge these three pages into one."

Same flow: preview → confirmation → apply. The agent **always**
shows a diff (before vs after) before making changes. You see
line-by-line edits with highlights.

Changes land in page history as `agent_update` records. Rollback
works the normal way (see [History](./04-history.md)).

### 4. Structural operations

The agent can:

- **Move a page** elsewhere in the tree: "Move `Security` under
  `Engineering`".
- **Rename**: "Rename `API v1` to `Legacy API`".
- **Delete**: "Delete empty pages under Drafts".
- **Create a series of pages**: "Create 5 retro template pages,
  one per team: Platform, Billing, Frontend, Data, Security."

All structural changes require explicit confirmation.

### 5. Find and extract

- "Find all mentions of deprecated endpoints in the docs."
- "Collect every TODO comment scattered across the Architecture
  page."
- "Show me pages not updated in more than 6 months."

These tasks usually run **without confirmation** — they're
read-only.

## What the agent does NOT do

Hard boundaries to keep your system safe:

- **Doesn't change code in repositories.** Read-only. If you need
  a code PR, open it in GitHub by hand — the agent doesn't push
  to Git.
- **Doesn't send messages** (email, Slack, webhooks).
- **Doesn't change permissions** on pages or projects.
- **Doesn't delete projects or repositories** — only pages.
- **Doesn't work on things you can't access.** If you don't have
  Editor rights on a project, the agent can only read.
- **Doesn't act without confirmation.** Any change — preview →
  you hit Apply.

## Action confirmations

When the agent is about to do something — it shows:

```
┌────────────────────────────────────────────────────┐
│ 📝 Update page «Auth flow»                         │
│                                                    │
│ Diff preview:                                      │
│ - Our JWT tokens rotate every 15 minutes...        │
│ + Our OAuth 2.0 access tokens rotate every 15      │
│ + minutes. Refresh tokens are issued on login...   │
│                                                    │
│ [✓ Apply] [✗ Reject] [✎ Edit before applying]     │
└────────────────────────────────────────────────────┘
```

Options:

- **Apply** — apply as-is.
- **Reject** — cancel, nothing changes.
- **Edit before applying** — open the diff in the editor, tweak
  by hand, then save.

### Batch operations

If the agent is running multiple operations at once ("create 5
pages" or "update every mention of X in 8 places"), it shows a
**list of changes** and lets you:

- Confirm all at once (**Apply all**).
- Pick one by one (checkboxes).
- Reject all.

## Source citations

Like a regular chat, the agent **always** references where it got
the facts:

```
According to "Release process" [1], releases ship on Tuesdays.
At release time the changelog is updated automatically [2].

Sources:
[1] Release process — /projects/42/17
[2] Changelog automation — /projects/42/23
```

Click `[1]` / `[2]` — navigate to the page, highlight the quoted
fragment.

If there's no answer in the docs — it says so directly: "I didn't
find an answer to X in your documentation. I suggest [creating a
page about X] — shall I draft it from the repository code?"

## Under the hood

1. **Retrieval.** Your query is vectorized, and the most relevant
   fragments from project pages + repositories are picked.
2. **Reasoning.** The LLM receives context + the question + a list
   of available tools (create_page, update_page, move_page,
   search_pages, read_file, etc.).
3. **Planning.** The agent decides: answer with text or execute an
   action. If action — it formulates a tool call.
4. **Preview.** The result comes back to you as "I'm about to do
   X and Y, confirm?"
5. **Execution.** After your Apply the actions run in real time.
   Colleagues see changes instantly.

This is the **ReAct agent** architecture (Reasoning + Acting)
with a required confirmation step.

## Agent scope

Context is determined by where you opened it:

- **On a project page** — the agent works within this project and
  its attached repositories.
- **On `/chat`** — global mode. You pick projects in the dropdown
  manually. Handy for cross-project tasks ("project A got a new
  feature — document it in project B using our template").

You can't change scope mid-conversation — open a new session.

## Memory

The agent remembers the current conversation:

- Previous turns in this thread.
- Which files / pages it already searched.
- Your previously confirmed actions in this session.

This makes things like:

```
You: Show me every auth page.
Agent: [list of 4 pages]
You: Update the second one, it's outdated.
Agent: [knows which page you mean]
```

The thread lives within one tab. Close / reload — new session.

## Permissions and limits

The agent acts **on your behalf**:

- Reader role → agent can search and answer, but can't change
  anything (if you ask — it'll say "you don't have rights").
- Editor role → creates and edits pages.
- Admin role → can also change the tree structure and names.

The agent **cannot** exceed your permissions. You won't get admin
rights by asking "agent, grant me admin access".

## Action audit

Everything the agent does is logged:

- In **page history** — as `agent_create` / `agent_update` /
  `agent_delete` events, with your confirmation text.
- In **project activity feed** — as "Agent (via Alice) created
  page …".
- Easily reversible with standard rollback.

If the agent broke a page, it's not a "lost edit", it's exactly
the same history entry as a human edit.

## Example dialogs

### Long task

```
You: We have a new microservice billing-reconciliation. The code
is in the repo but no docs. Create a starter page with Overview,
API, Dependencies, Owner sections.

Agent: Read the service code at /repos/billing/billing-reconciliation.
Observations: Go service, 12 endpoints under /api/v1, depends on
PostgreSQL and Kafka. Owner is not in metadata.

I'm proposing to create "Billing Reconciliation" under "Services"
with this structure:

[page draft]

Whom should I ask for the owner? I can leave a "TBD — ask
@billing-team" placeholder.

[✓ Apply] [✗ Reject] [✎ Edit before applying]
```

### Multi-step action

```
You: We ran a team retro. Create a page from the template with
Plus / Minus / Action items. Also add a link to it from the
team home page.

Agent: Plan:
1. Create "Retro — April 2026" under /projects/platform/retros
2. Add a link to it at the bottom of
   /projects/platform/team-home

Apply all / Apply individually?

[Apply 1+2] [Apply 1] [Apply 2] [Reject]
```

### Honest "don't know"

```
You: What's our SLA with the hosting provider?

Agent: I didn't find SLA info in the projects available to me.
Either it's not documented, or it's in a private folder I don't
have access to.

I can draft a "Hosting SLA" page if you share the key terms —
or I can look for mentions in infrastructure code?
```

## Privacy

- The agent operates only on resources you have access to.
- Query + context go to the LLM. For enterprise customers — the
  LLM is self-hosted, data doesn't leave the perimeter.
- Chat history is private to you.
- Agent actions are audited and visible in the activity feed.

## Limitations

- **Doesn't write or change code** in repositories. Read-only.
- **Doesn't make big architectural decisions** for you. "Make
  our docs better" is too broad — narrow down.
- **Doesn't spend an hour on one task.** Long batch ops ("update
  100 pages") should be split into subtasks.
- **Context freshness** — 1–3 minutes (indexing delay after your
  edits).
- **Large projects** (~10k pages) — retrieval picks the top N; it
  might miss the right fragment. Sharpen your query.

## Difference from generic chat in other products

| Feature | Notion AI / Confluence Rovo | Nextdocs Agent |
|---|---|---|
| Answer questions about docs | ✅ | ✅ |
| Create a new page on demand | ⚠️ within writing context | ✅ |
| Edit existing pages | ⚠️ auto-suggestions | ✅ with diff + confirmation |
| Read repository code | ❌ | ✅ |
| Batch ops with confirmation | ❌ | ✅ |
| Audit log of actions | ⚠️ | ✅ full |
| "Don't know" instead of hallucinations | ⚠️ | ✅ explicitly |
| Source citations | ⚠️ | ✅ always |

## Typical scenarios

**Employee onboarding.** A new engineer asks "how does our code
review work?". Gets a coherent answer with links. Next: "where's
the FAQ on that?". Agent: "No FAQ — I can create one from the
comments in past PRs?" → creates it.

**Documenting a new service.** "Create a page for
billing-reconciliation from the code." The agent reads the repo,
generates a draft, you tweak, Apply.

**Bulk update.** "We're moving from JWT to OAuth 2.0. Find and
replace every JWT mention in the docs with OAuth 2.0, preserving
meaning." The agent finds 12 spots, shows the diff for each, you
confirm. 10 minutes vs an hour.

**Search in decision history.** "Why did we pick BigQuery over
Redshift?" — finds the ADR, explains.

**Structural cleanup.** "Find pages not updated in more than a
year and suggest archiving or deleting them." You get a list
with recommendations, decide each.
