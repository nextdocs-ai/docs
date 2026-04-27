# Search across documentation

## Why it matters

Documentation with more than 20 pages stops being "readable" in a
linear sense. People don't read it cover to cover — they search for
answers: "where's our auth stuff?", "which page describes the
release process?", "do we have anything on rate limiting?"

Fast and precise search is critical documentation infrastructure.
If search is slow or misses the obvious, the team gives up on the
wiki and falls back to "ask in Slack". The Nextdocs goal is that
search always works.

## How to open it

- **Cmd/Ctrl+K** from anywhere in the app — the fastest way.
- The **Search and Chat** button in the editor's right sidebar.
- Any link with `#search=…` in the URL — opens the panel with a
  preset query (good for sharing searches).

The panel opens as a modal over the app: input box on top, results
below. Focus is on the input by default, start typing immediately.

## How to phrase a query

### Plain words

Type any words — search finds pages where they appear. Order and
case don't matter.

```
auth flow
```

Finds pages where both words appear (not necessarily adjacent).

### Exact phrase

Quotes — matches the exact phrase.

```
"JWT rotation"
```

Returns only pages where those words appear in that exact order.

### Mixed query

You can combine: a required phrase plus any extra words.

```
"JWT rotation" security
```

Results with the exact phrase "JWT rotation" are ranked higher;
then those that additionally contain security.

## Content-type filters

Above the results list — a row of filter buttons:

- **Text** — plain paragraphs, headings, lists.
- **Code** — code blocks. If you're looking for a function /
  variable name — filter to code only.
- **Table** — table cell content.
- **Image** — pages with images (by alt text / captions).
- **Canvas** — TLDraw, Excalidraw, Mermaid diagrams (text inside
  labels, node names, shape names).
- **Tasks** — checklist items.

Clicking a filter narrows results to that type. Handy when a
project has docs + code + lots of tables.

## How ranking works

Nextdocs uses a hybrid of BM25 (classical full-text rank) and
semantic search (meaning-based proximity). What influences
ranking:

- **Heading match** on a page pushes it up.
- **Match in the first lines** (intro paragraph) also boosts it.
- **Word proximity** in text — tighter is better than scattered.
- **Exact phrases in quotes** — are hard requirements.
- **Semantic closeness** — works even when words don't match:
  query `refresh token` finds a page about `access token
  rotation`, even if it doesn't say "refresh".

## What results look like

Results are grouped by page:

- **Page title** and path (project / parent page).
- A collapsible block with found fragments: 1–3 fragments per
  page, with context and highlights.
- Code blocks keep syntax highlighting.
- Canvas fragments highlight the matching text inside diagrams.
- "Go to" arrow icon — opens the page and scrolls right to the
  match.

## Search scope

Search always works within **projects you have access to**:

- On a project page — defaults to this project only. A toggle
  "All projects" at the top of the panel expands to all your
  projects.
- On `/projects` — defaults to all at once.
- Private projects you weren't invited to aren't reachable via
  search: those results are filtered out at the index layer.

If a project is public — its pages are found by the internal
search for everyone (including logged-out users) and by Google /
Yandex (see the SEO section in [Projects](01-projects.md)).

## Hotkeys in the panel

| Key | Action |
|---|---|
| `↑` / `↓` | Toggle between results |
| `Enter` | Open the selected result |
| `Cmd/Ctrl+Enter` | Open in a new tab |
| `Esc` | Close search |
| `Tab` | Cycle contentType filter |

## What lands in the index

- Page text (headings, paragraphs, lists, quotes).
- Code blocks with language. Highlight is kept in rendering.
- Text in tables.
- Labels inside diagrams (Mermaid source, TLDraw / Excalidraw
  labels).
- Image alt text and captions.
- Page titles and metadata.

Not indexed:

- Raw comments (separate comment search is TBD).
- Repository sources — indexed separately and accessed via the
  **AI agent**, not full-text search (see
  [AI Agent](08a-ai-agent.md)).

## Indexing lag

When you change something, the index updates asynchronously:

- Typical: **1–3 minutes** after save.
- Under load: up to **5 minutes**.
- If nothing shows up in 10 minutes — something broke, ping
  support.

## Sharing searches

Want to share a query? Copy the URL from the address bar with the
panel open:

```
https://nextdocs.ai/#search=refresh%20token&project=42
```

The person you send it to (if they have access to those projects)
sees exactly the same results.

## Typical scenarios

**"Where are our environment variables described?"**
`env variables` → results, with "Environment variables
configuration" in the title. Open.

**"Which database do we use for billing?"**
`billing database` → semantic search surfaces "Billing
architecture" which mentions PostgreSQL, even if "PostgreSQL"
isn't in the query.

**Specific function in code**
`handleUserRegistration` + **Code** filter → every place in code
where the function is defined / called.

**Exact quote you remember**
`"we decided to use redis pub/sub"` → exact phrase. If it's
nowhere else in the docs — one page comes back.

## Difference from the AI agent

Full-text search answers **where**: "find me pages with words X".
Fast, predictable, deterministic, no LLM in the loop.

The AI agent answers **what**: "explain how this is built", plus
it can **do things**: create a page, update a section, move the
tree. See [AI Agent](08a-ai-agent.md).

Both open with `Cmd/Ctrl+K` and switch with one click in the
panel. In practice the two are used together: fast search first,
if that's not enough — switch to agent mode with a follow-up. If
you need to change something — straight to agent.

## Limitations

- 500 results max per query (usually more than enough).
- Search across non-Russian/English languages works but morphology
  quality is lower (not all languages have stemmers).
- Doesn't work offline (search is a backend request).
- Search across archived (deleted 90+ days ago) pages is not
  possible.
