# Integrations: GitHub, Confluence, ZIP, PDF

## Why it matters

Documentation is rarely written "from scratch". There's usually
already code in a repository, an existing README, specs in
Confluence, a PDF with technical requirements sitting somewhere,
and a markdown folder in email. To avoid forcing people to rewrite
everything by hand, Nextdocs can import from these sources and
then pull in updates automatically.

Four import options:

- **GitHub** — a lasting two-way link: Nextdocs clones the repo,
  the AI agent generates docs from code, and when the code changes
  (merge to main) the docs update.
- **ZIP** — a one-off import of any repository as an archive.
  Good for private codebases not on GitHub.
- **Confluence** — a one-off import from Confluence HTML export.
- **PDF** — a one-off import of PDF files (specs, technical
  requirements, manuals) at the page level.

## GitHub

### Install the GitHub App

1. On `/repositories` click **Install GitHub App**.
2. GitHub redirects you, you pick an organisation and repositories
   Nextdocs should access. Read-only is fine.
3. Back in Nextdocs — the repos show up in the list.

The App needs:

- Read-only on repository contents (clone, pull).
- Read-only on events (we need webhooks to detect pushes).

**The App doesn't write to the repo** — no commits, no PRs on
behalf of Nextdocs. One-way flow: code → docs.

### Creating a project from a repo

On `/projects` → **Create New Project** → **From GitHub**:

1. Pick a repository from the installed list.
2. (Optional) Pick a branch to generate from — default is
   `main` / `master`.
3. Give the project a name.
4. **Create** — the project appears immediately with "Generating"
   status.
5. In the background:
   - The repo is cloned into Nextdocs storage.
   - The AI agent goes through files, generates markdown docs.
   - Pages appear in the tree. You see them show up in real time.
6. Once done, project status flips to "Ready"; you can read and
   edit.

### Sync on push to main

When something is merged into a tracked repository (push to
default branch):

- GitHub sends a webhook to Nextdocs.
- Nextdocs updates the clone.
- The agent looks at which files changed and **updates the
  corresponding doc pages**. Your manual edits made via Nextdocs
  are preserved when they don't collide with the changed parts.
  Otherwise a separate `agent_update` entry is created that you
  can review / roll back.

### Linking several repos to one project

On `/repositories` you can **Attach to project** — link an
already-cloned repo to an existing project. The AI chat / search
in that project then sees all attached repos' code at once.

Scenario: team monorepo with 5 microservices → 1 Nextdocs project
+ 5 attached repos → a single place to search across all code.

### Detach / delete

- **Detach repository from project** — the link is removed, the
  repo stays in Nextdocs. Pages generated from it are **not
  deleted** — they become regular "manual" pages. The agent no
  longer updates them automatically.
- **Delete repository** — the clone is removed from storage. If
  the repo was attached to projects, it's detached first.

## ZIP

### When to use

- Private GitLab / Bitbucket / self-hosted git server.
- No way to install the GitHub App.
- One-off import, no update loop planned.

### How to import

On `/projects` → **Create New Project** → **From ZIP**:

1. Upload a `.zip` archive with the whole repository (exclude
   `.git/`, `node_modules/`, build artefacts — sources only).
2. Provide name and description.
3. Nextdocs unpacks, runs the agent, generates docs.
4. Result — a regular project with no link to an external repo.
   Updates are via new zip uploads: a separate "Re-upload archive"
   button in the project menu.

Max archive size — 100 MB.

## Confluence

### When to use

- You have documentation in Confluence and you're moving to
  Nextdocs.
- You want to "freeze" the old wiki as an archive inside
  Nextdocs.

### How to import

1. In Confluence: Space settings → **Export space** → **HTML**
   format.
2. Download the resulting archive (can be several MB).
3. In Nextdocs: `/projects` → **Create New Project** → **From
   Confluence export**.
4. Set a project name, upload the archive.
5. Nextdocs:
   - Parses HTML pages, converts to internal markdown.
   - Restores the page hierarchy (same as the source space).
   - Images and files referenced by links are pulled from the zip
     and uploaded to storage.
   - Confluence macros without a counterpart — become text
     placeholders like `[Confluence macro: jira-issue]`, visible in
     the body so you can hand-fix them later.

### What's lost

- **Confluence-specific macros**: Jira, Calendars, Analytics —
  become placeholders.
- **Attachments**: files attached to a page as `attachment` are
  uploaded to storage; an embedded Confluence gallery becomes a
  list of links.
- **Comments** — not transferred, because they reference
  Confluence users who don't exist in Nextdocs.
- **Watchers / permissions** — need to be re-created (see
  [Permissions](./10-permissions.md)).

### What's preserved

- Full page hierarchy.
- All text, headings, lists, tables.
- Embedded images.
- Inter-page links (within the imported space they're converted
  to Nextdocs links).

## PDF

### When to use

- You got a TS in PDF from a client or contractor.
- A regulation / procedure / manual arrived as a PDF.
- Old documentation requested in "official" format that now
  needs to live in a wiki.
- Articles and whitepapers you're writing conclusions about.

### How to import

Two options:

**1. Import into a page** (recommended for documents you plan to
edit / discuss / comment on).

1. Open or create an empty page in a project.
2. Slash menu → **Import PDF**.
3. Pick a file (up to 50 MB).
4. Nextdocs parses the PDF:
   - Extracts text preserving order.
   - Detects headings by font size (large → H1, medium → H2 etc.).
   - Detects lists (bulleted / numbered).
   - Tables — if the PDF has "real" tables (not images), become
     Nextdocs tables.
   - Images are extracted and uploaded to storage.
5. After a few seconds the page fills with parsed content. Edit
   like any other.

**2. Import as project** (for a big 100+ page document you want
split by sections).

1. `/projects` → **Create New Project** → **From PDF**.
2. Upload the file.
3. Nextdocs splits the PDF into chapters / sections (by top-level
   headings) and creates project structure:
   - Root page — table of contents.
   - Child pages — document chapters.
   - Each chapter is a regular editable page.

### What transfers well

- **Text PDFs** (produced by Word / LaTeX / Pandoc) — excellent.
  Text, headings, lists, basic tables, images.
- **Multi-column PDFs** (academic papers) — the parser understands
  column order.
- **PDFs with bookmarks** — used to build the hierarchy when
  importing "as project".

### What transfers worse

- **Scans / OCR PDFs** (where text is an image). Nextdocs does
  OCR, but quality depends on the original: a clean 300 dpi scan
  recognises well, a crumpled photo doesn't.
- **Complex layouts** (infographics, ad brochures) — text is
  extracted but visual integrity is lost.
- **Formulas** (LaTeX-style math) — inserted as text
  approximations. For originals, use screenshots.
- **Comments and annotations** in the PDF — ignored (body text
  only).

### Search and AI chat after import

Once imported, the page is a normal page — search and AI chat find
its content. So after a PDF import you can:

- Ask "what does this document say about X?"
- Find an exact quote via Cmd/Ctrl+K.
- Comment passages, mention colleagues.

Things not possible in a vanilla PDF viewer — work out of the box
in Nextdocs.

### Limitations

- **50 MB** max per file.
- **500 pages** max (more — import in parts).
- **Forms and checkboxes** inside the PDF aren't detected (text
  only).
- **Password-protected PDFs** — remove protection first, outside
  Nextdocs.
- Full layout preservation is impossible (PDFs are laid out for
  print, our editor is reflow-text).

## Project statuses

A project has a visual **status chip** on its card:

- **Generating / Importing** — in progress. You can edit, but with
  care — the agent may overwrite pages.
- **Ready** — import / generation finished.
- **Error** — something failed. Project details show what:
  "Clone failed" / "Archive too large" / "File X doesn't parse as
  HTML". Usually fix the input and retry.
- **Updating** — a push-triggered update. Fast, 10-30 seconds.

## Limitations

- GitHub App: organisation + user level only. Enterprise Server
  on-premise — via a separate contract.
- Supported code languages for doc generation: Go, Python,
  TypeScript / JavaScript, Java, Rust, C#, C/C++. Others are
  parsed as "text" — doc quality is lower.
- Confluence export — HTML format only. PDF / XML aren't
  supported.
- Webhooks only work for the **default branch**. If your docs
  live on `dev`, either switch default or update manually.

## Typical scenarios

**"We already have 200 repos, want a wiki from each."** Install
the GitHub App org-wide, create projects in batches (one per repo)
or group several repos under an umbrella project.

**"Archive of an old Confluence base with 500 pages."** Import
via ZIP — one-off. You get a living archive. Mark outdated items
with a tag / move into an "Archive" section.

**"We want docs that auto-update with code."** GitHub App +
from-repo project + auto-sync enabled (default). Tech lead reviews
`agent_update` events in history, rolls back anything completely
off.
