# Nextdocs — user guide

Nextdocs is a collaborative documentation platform. You create a project\
(or connect a GitHub repository), write pages in a live editor, invite\
your team — and end up with a full-featured knowledge base with version\
history, search, and an AI agent that can both answer questions and edit\
pages on request.

This folder is the **end-user guide**. Each file describes one feature:\
why it exists, where to find it, and how to use it.

## Philosophy: everything included, no plugins

The classic competitor approach is "bare wiki engine + plugin\
marketplace". Need diagrams? Buy Gliffy or Lucidchart. AI search? Add\
Rovo / Notion AI for an extra fee. PDF import? Hunt for a third-party\
add-on. Real-time collaboration? That's on the Premium plan. Assemble\
the puzzle yourself.

Nextdocs is built on the opposite principle: **everything you need is**\
**in the box, integrated, and seamless**.

* **Editor + collaboration + live cursors + follow mode** — not\
  separate products, one system.

* **Mermaid + TLDraw + Excalidraw diagrams** — built in, searchable\
  by their text, with real-time collab.

* **AI agent + full-text search + semantic search across docs and**\
  **code simultaneously** — a single interface, nothing to plug in. The\
  agent doesn't just search and explain; it can create and edit pages\
  on your command (with mandatory confirmation). Repository code is\
  read-only.

* **Import from Confluence / Notion / Google Docs / PDF / Excel /**\
  **markdown / ZIP / GitHub** — each parser extension lives in the core,\
  not as a separate plugin.

* **Versions, comments, mentions, notifications, permissions, GitHub**\
  **integration** — core features, not options.

This is an important trade-off on both sides:

* **Upside:** you don't spend 2–3 weeks on "glue": plugin registration,\
  SSO configuration, piping separate pricing for AI and diagrams.\
  Everything works out of the box.

* **Downside:** if you have a very specific need ("we want an\
  integration with our in-house HR portal"), you can't bolt it on via\
  a plugin marketplace — you need to request the feature through\
  support or the roadmap. We move fast, but it's not "install a plugin\
  today".

For most engineering teams this is the right call: less time on\
assembly, less SaaS burn, fewer places where something might break.

## Where to start

1. [Creating a project](01-projects.md) — how to spin up an empty\
   project or import docs from GitHub.

2. [Editor and slash commands](02-editor.md) — how to write, insert\
   headings, lists, code, and media.

3. [Inviting your team](10-permissions.md) — how to grant colleagues\
   read and write access.

## Table of contents

### Content

* [Projects and repositories](01-projects.md)

* [Editor and slash commands](02-editor.md) — including pasting from\
  Google Docs, Notion, Word, Excel, CSV, HTML, markdown

* [Tables](14-tables.md)

* [Diagrams — Mermaid, TLDraw, Excalidraw](03-diagrams.md)

* [Version history and rollback](04-history.md)

### Teamwork

* [Collaborative editing and presence](05-collaboration.md)

* [Comments and @-mentions](06-comments-mentions.md)

* [Notifications and activity feed](07-notifications.md)

* [Permissions and invitations](10-permissions.md)

### Search and navigation

* [Search across documentation](08-search.md)

* [AI agent (search + page create/edit)](08a-ai-agent.md)

* [Recently visited pages](11-recently-visited.md)

### Integrations

* [GitHub, Confluence, PDF, ZIP — import and sync](09-integrations.md)

### User settings

* [Profile and preferences](12-profile.md)

### Comparison with other tools

* [Nextdocs vs Confluence / Notion / GitBook / Outline / ReadMe](13-comparison.md)

## Glossary

* **Project** — container for related documents (e.g. one microservice,\
  one product, one team).

* **Page** — a single markdown document inside a project. Has its own\
  nesting tree, history, and comments.

* **Repository** — a link to a GitHub repo. One project can be linked\
  to several repos at once.

* **Yjs / live editing** — the mechanism that lets multiple people type\
  into the same page simultaneously without conflicts.

* **RAG** — semantic AI search. Unlike regular search, it matches on\
  meaning, not just on word matches.

## Help and support

If something doesn't work — reach out via the support chat (button in\
the lower right corner) or email [support@nextdocs.ai](mailto:support@nextdocs.ai).
