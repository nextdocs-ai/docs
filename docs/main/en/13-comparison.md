# Comparison with other documentation tools

## Why it matters

The documentation-tool market is big, and teams usually compare
several platforms before picking one: Confluence, Notion, GitBook,
Outline, ReadMe, Google Docs. This page lays out where Nextdocs is
stronger or weaker than each.

Two key differentiators for Nextdocs:

1. **Integration with code** — we glue text documentation to the
   repository itself, expose AI search over both, and auto-update
   documentation on push. The other products are either "pretty
   wiki" or "separate GitBook for API" — combining them is
   manual work.

2. **Batteries included — no plugins.** Everything you need for
   documentation (diagrams, AI search, import from many formats,
   collaboration, live cursors, history, comments, permissions)
   is built in. Competitors are most often "bare wiki + plugin
   marketplace" where each feature is its own subscription and
   setup.

### How many plugins to catch up with Nextdocs

To reach a comparable feature set on Confluence, teams typically
buy:

- **Gliffy** or **Draw.io** ($2-$5/user/mo) — diagrams.
- **Scroll Markdown Exporter** ($500+/year) — markdown export.
- **Rovo** (enterprise, $20+/user/mo) — AI search.
- **Comala Workflows** — if you need approval flows.
- **Scroll PDF Exporter** — PDF export.
- **Balsamiq Wireframes** — freehand diagrams.
- **Code Block Plugin** — decent syntax highlighting.
- **Table Filter and Charts** — advanced tables.

Total: $50+/user/month on top of the Confluence base. In Nextdocs
all of it is part of the platform with no extra subscriptions.

On Notion:

- **Notion AI** ($10/user/mo) — AI search.
- **External Miro / Whimsical embeds** — diagrams (their
  subscriptions on top).
- **Scripts / Zapier** — if you need automation beyond Notion
  API.

Competitors mostly **don't** have:

- AI chat across **code + documentation at the same time** (just
  documentation).
- Text index **over diagram contents** (Mermaid code, TLDraw
  labels, Excalidraw notes).
- Built-in PDF import with OCR.
- Simultaneous work with several GitHub repositories in one
  project.

## Summary table

Legend: ✅ yes; ⚠️ partial / with limits; ❌ no; 💰 paid on all
tiers; ⭐ premium-only / higher tiers.

| Feature | **Nextdocs** | Confluence | Notion | GitBook | Outline | ReadMe |
|---|:---:|:---:|:---:|:---:|:---:|:---:|
| **Editor** ||||||
| WYSIWYG + markdown input | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| Real-time co-editing | ✅ | ⚠️ partial | ✅ | ⚠️ | ✅ | ❌ |
| Live cursors | ✅ | ❌ | ✅ | ❌ | ✅ | ❌ |
| Follow-mode (follow a colleague) | ✅ | ❌ | ❌ | ❌ | ❌ | ❌ |
| Page hierarchy (tree) | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| Inline comments | ✅ | ✅ | ✅ | ✅ | ✅ | ⚠️ suggestions only |
| Threaded comments + resolve | ✅ | ✅ | ✅ | ⚠️ | ⚠️ | ❌ |
| `@` mentions | ✅ | ✅ | ✅ | ⚠️ | ✅ | ❌ |
| Version history | ✅ | ✅ | ⭐ | ✅ | ✅ | ⚠️ |
| Rollback to a version | ✅ | ✅ | ⭐ | ✅ | ✅ | ❌ |
| Diff between versions | ✅ | ⭐ | ❌ | ✅ | ⚠️ | ❌ |
| **Diagrams** ||||||
| Mermaid (code-based diagrams) | ✅ | ⚠️ plugin | ⚠️ embed | ✅ | ✅ | ⚠️ |
| Drawing canvas (freehand) | ✅ TLDraw | ⚠️ Gliffy 💰 | ⚠️ embed | ❌ | ❌ | ❌ |
| Excalidraw-like sketches | ✅ | ❌ | ⚠️ embed | ❌ | ❌ | ❌ |
| Text inside diagrams is indexed | ✅ | ❌ | ❌ | ❌ | ❌ | ❌ |
| **Search** ||||||
| Full-text | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| Semantic / smart search | ✅ | ⭐ AI Rovo | ⭐ Notion AI | ⭐ | ❌ | ⚠️ |
| Content-type filters | ✅ | ⚠️ | ✅ | ⚠️ | ⚠️ | ⚠️ |
| Unified search: repo code + docs | ✅ | ❌ | ❌ | ❌ | ❌ | ⚠️ OpenAPI only |
| **AI agent** ||||||
| AI Q&A on docs | ✅ | ⭐ Rovo | ⭐ Notion AI | ⭐ | ❌ | ⭐ |
| AI over repo code + docs | ✅ | ❌ | ❌ | ⚠️ | ❌ | ❌ |
| AI creates new pages on demand | ✅ | ❌ | ⚠️ writing only | ❌ | ❌ | ❌ |
| AI edits existing (diff + confirm) | ✅ | ❌ | ⚠️ suggestions | ❌ | ❌ | ❌ |
| AI runs batch operations | ✅ | ❌ | ❌ | ❌ | ❌ | ❌ |
| Audit log of AI actions in activity | ✅ | — | ⚠️ | — | — | — |
| Source citations in answers | ✅ | ⚠️ | ⚠️ | ⚠️ | — | ⚠️ |
| "Don't know" instead of hallucinating | ✅ | ⚠️ | ⚠️ | ⚠️ | — | ⚠️ |
| **Git integration** ||||||
| Attach GitHub repo as source | ✅ | ❌ | ❌ | ✅ | ❌ | ✅ |
| Auto-sync on push to main | ✅ | ❌ | ❌ | ✅ | ❌ | ✅ |
| AI doc generation from code | ✅ | ❌ | ❌ | ❌ | ❌ | ❌ |
| Several repos per project | ✅ | ❌ | ❌ | ⚠️ | ❌ | ❌ |
| **Import / export** ||||||
| Import from Confluence | ✅ | — | ✅ | ⚠️ | ✅ | ⚠️ |
| Import from Notion | ✅ on paste | ⚠️ | — | ⚠️ | ⚠️ | ❌ |
| Import from Google Docs / Word | ✅ on paste | ⚠️ | ⚠️ | ⚠️ | ⚠️ | ⚠️ |
| Import PDF (text + tables) | ✅ | ⭐ plugin | ❌ | ❌ | ❌ | ❌ |
| Import Excel/CSV as tables | ✅ | ⚠️ | ✅ | ⚠️ | ⚠️ | ❌ |
| Import markdown ZIP | ✅ | ❌ | ❌ | ✅ via git | ⚠️ | ⚠️ |
| HTML/Markdown smart paste | ✅ | ⚠️ | ⚠️ | ✅ | ✅ | ⚠️ |
| Export PDF | ⚠️ planned | ✅ | ✅ | ✅ | ✅ | ✅ |
| Export as markdown | ✅ | ⭐ plugin | ⚠️ | ✅ | ✅ | ❌ |
| **Tables** ||||||
| Inline tables with formatting | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| Paste from Excel/Sheets | ✅ | ⚠️ | ✅ | ⚠️ | ⚠️ | ⚠️ |
| Export to .xlsx | ✅ | ⭐ | ⚠️ csv | ❌ | ❌ | ❌ |
| Deep link to a specific cell | ✅ | ❌ | ❌ | ❌ | ❌ | ❌ |
| Fullscreen mode for big tables | ✅ | ❌ | ⚠️ | ❌ | ❌ | ❌ |
| **Permissions and publishing** ||||||
| Role-based (Owner/Admin/Editor/Reader) | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| Page-level permissions | ✅ | ✅ | ✅ | ⚠️ | ⚠️ | ✅ |
| Public publish without login | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| Custom domain | ⚠️ planned | ⭐ | ⭐ | ✅ | ✅ | ✅ |
| SSO | ⭐ enterprise | ⭐ | ⭐ | ⭐ | ✅ | ⭐ |
| **Notifications** ||||||
| In-app notifications | ✅ | ✅ | ✅ | ⚠️ | ✅ | ⚠️ |
| Email digest | ⚠️ planned | ✅ | ✅ | ✅ | ✅ | ⚠️ |
| Live activity feed per project | ✅ | ✅ | ⚠️ | ❌ | ⚠️ | ❌ |
| **Misc** ||||||
| Open Source / self-hosted | ⚠️ enterprise | ⭐ DC | ❌ | ❌ | ✅ | ❌ |
| API for automation | ⚠️ partial | ✅ | ✅ | ✅ | ✅ | ✅ |
| Mobile app | ❌ | ✅ | ✅ | ⚠️ web | ⚠️ web | ❌ |
| Slack integration | ⚠️ via webhooks | ✅ | ✅ | ✅ | ✅ | ✅ |

## When to pick Nextdocs

**You're a technology team with a lot of code.** Confluence /
Notion are good wikis but they can't see your repository.
Nextdocs can answer "what does this function do" alongside "how
does code review work" — in one place.

**Documentation must not go stale automatically.** On merge to
main the docs update without manual work. At competitors this is
either impossible or limited to OpenAPI specs (ReadMe).

**You use Mermaid / TLDraw / Excalidraw.** In Nextdocs all three
are built in, text in diagrams is indexed, collaboration works in
real time. In Confluence — paid plugins (Gliffy); in Notion —
embeds with no indexing; in others — either Mermaid only, or
nothing at all.

**Quality AI search over your documentation matters.** Nextdocs
uses a RAG pipeline with source citations and answers "don't
know" instead of hallucinating. At competitors AI is an extra
paid option.

**You need live collaborative sessions** (retros, groomings,
design reviews). Follow-mode + live cursors let you work like in
Figma. Confluence / ReadMe have limited live collab; Notion /
Outline — no follow-mode.

## When a competitor is a better fit

**Confluence** — if the company has already bought the Atlassian
stack (Jira, Bitbucket, Bamboo) and needs tight integration.
Confluence wins on a mature ecosystem: after 20 years it has
thousands of plugins, templates, guides.

**Notion** — if you need **more than documentation**: tasks,
databases, CRM, notes, calendar. Notion is a universal
workspace. Nextdocs is focused on docs and specs.

**GitBook** — if the job is **OpenAPI + SDK reference only**.
GitBook is the leader in "API docs": interactive API explorer,
SDK generation, language highlights. For public API
documentation, it's stronger.

**Outline** — if **self-hosted is a must**. Outline is open
source, free to host yourself. Nextdocs self-hosted is
enterprise-only.

**ReadMe** — if **the audience is external developers**. ReadMe
focuses on dev-portal: API versioning, usage metrics, customer
accounts, interactive API consoles.

**Google Docs** — for **one-off unstructured documents** (memos,
reports, briefs). No page tree, no code integrations — but the
fastest way to write and share a single document.

## Detailed comparisons

### Real-time collaboration

- **Nextdocs**: Yjs-based, live cursors, follow-mode,
  conflict-free merge, works offline.
- **Notion**: proprietary stack, cursors yes, no follow, limited
  offline.
- **Outline**: Yjs-based, cursors yes, no follow.
- **Confluence**: collaborative editor only since 2020, lagging,
  no live cursors.
- **GitBook**: only partially real-time (auto-debounced saves).
- **ReadMe**: one editor at a time.

### Diagrams

- **Nextdocs**: Mermaid + TLDraw + Excalidraw, full real-time,
  text indexed.
- **Confluence**: basic draw.io, PlantUML via markdown, Gliffy
  paid plugin.
- **Notion**: embed only (Miro, Whimsical, Figma) — the diagram
  isn't in the document, it's in an external service.
- **GitBook**: Mermaid in code blocks, no freehand.
- **Outline**: Mermaid, no freehand.
- **ReadMe**: screenshots / embed only.

### AI search

- **Nextdocs**: RAG over pages + repository code, with
  citations, honest "don't know".
- **Notion AI**: great writing assistant, but doc Q&A is weaker
  and no repo integration.
- **Confluence (Rovo)**: new AI product, expensive, enterprise
  only.
- **GitBook AI**: focuses on API docs, decent at reference Q&A.
- **Outline**: AI via optional OpenAI-key connection —
  minimal features.
- **ReadMe AskAI**: Q&A over OpenAPI specs, not prose docs.

### Version history

- **Nextdocs**: session-based (not tiny saves but logical edits),
  text + visual diff, rollback, agent edits aggregated
  separately.
- **Confluence**: versioned, diff yes, rollback yes, but fills up
  with micro-edits.
- **Notion**: page history on paid plans only.
- **GitBook**: git-like history, good diffs.
- **Outline**: versions with diff.
- **ReadMe**: publication-level versions, no page-level diff.

## Approximate pricing

- **Confluence**: from $6.05/user/month (Standard), enterprise
  by contract. Free up to 10 users.
- **Notion**: from $10/user/month (Business), Plus $8, Free for
  personal.
- **GitBook**: from $12.5/user/month (Pro), free for public
  projects.
- **Outline**: $10/user/month cloud, self-hosted free.
- **ReadMe**: from $399/month for 5 seats.
- **Nextdocs**: ask us, enterprise includes self-host.

## Migrating from competitors

**From Confluence** — export HTML, import into Nextdocs.
Hierarchy, formatting, links transfer. Custom Jira macros and
some plugin-specific blocks are lost. See
[Integrations](09-integrations.md).

**From Notion** — export markdown zip, import via "From ZIP"
treated as a regular markdown repo. Text works well, embeds
(Figma, Miro) become external links.

**From GitBook / Outline** — both export to markdown, import is
analogous.

**From Google Docs** — "File → Download → Markdown", split into
pages, import the zip.

## Philosophy: out of the box vs plugin marketplace

Most competitors are **core + marketplace**. Confluence without
Gliffy has no diagrams. Notion without Notion AI is blind in
smart search. GitBook without Git-sync is a plain wiki.

This is convenient if your needs are standard: install plugins
per the guide, pay subscriptions, work. But when the team needs
15 features — that's 15 subscriptions, 15 configs, 15 places
something might break.

Nextdocs is designed to cover the typical engineering team's
needs **out of the box**:

- 5 import types (GitHub, ZIP, Confluence, PDF, markdown paste)
  — no extra subscriptions.
- 3 diagram types (Mermaid, TLDraw, Excalidraw) — full
  integration with search and collaboration.
- 2 search types (full-text + AI) — one price, one interface.
- Collaboration, versions, comments, mentions, notifications —
  for every user immediately, no feature flags, no gating.

Single-vendor upside: predictable pricing, minimal onboarding,
one-point support.
Downside: if you have a very specific need like "bolt this BI
dashboard into the editor", it can't be done via plugin
marketplace. Either via our roadmap or via our API.

For most engineering-profile teams "no plugins" is the right
call.

## Conclusion

Tool choice isn't "best", it's "fits the task". Nextdocs is a
strong pick for teams that:

- Have substantial code and active development.
- Want AI search across both wiki and repositories.
- Need diagrams + their indexing + impairment-free import from
  other platforms.
- Value live collaboration at the level of Figma / Google Docs.
- Are tired of the "zoo of plugins" in Confluence / Notion.

If your documentation is 95% prose text + tables, with no code
and no diagrams, and the team is already settled on Confluence /
Notion — switching may not be worth it. For you Nextdocs is a
10-30% improvement, not a step change.
