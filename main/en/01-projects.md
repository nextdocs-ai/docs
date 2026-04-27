# Projects and repositories

## Why it matters

A **project** is your main container. It holds documentation pages, a
team with permissions, version history, and (optionally) links to code
repositories.

A single project usually maps to one of three things:

- **One microservice / library** — API docs, internal-logic notes,
  READMEs for developers.
- **One product / feature** — mixed documentation for product, design,
  and engineering teams.
- **One team or department** — internal knowledge base, processes,
  onboarding, retros.

A **repository** is a link to a GitHub repo. One project can link to
multiple repositories at once (monorepos, tightly related services),
and vice versa — one repo can appear in several projects (e.g. a
utility library used by three teams).

## How to create a project

1. Open `/projects` — the same place where you see cards for all your
   projects.
2. Click **Create New Project**.
3. Pick a type in the modal:
   - **Blank project** — an empty project with a single empty page.
     Best for documentation written from scratch.
   - **From GitHub** — pick a repository from your installed list
     (see the Integrations section). Nextdocs clones it, auto-generates
     the first version of documentation from the code, and places it
     into the page tree. Use this when you want a "starter" knowledge
     base for existing code without manual entry.
   - **From ZIP archive** — upload a `.zip` with sources. Same flow as
     GitHub but without the integration.
   - **From Confluence export** — import Confluence documentation as a
     `.zip` archive exported in HTML.
4. For all options, set a **name**, **description**, and **visibility**:
   `private` (invited-only) or `public` (accessible via link, no login
   required).

After creation you land on the project page — page tree on the left,
editor in the middle, tabs with comments, table of contents, and
history on the right.

## Managing a project

From the project menu (gear icon on the card or in the page header):

- **Rename** — change the name. Every link to the project picks up the
  new name automatically.
- **Visibility** — toggle public/private. Switching to `public` makes
  pages indexable by search engines (Google etc.) and accessible
  without login.
- **Delete** — remove the project. **This is irreversible**: all
  pages, comments, and history are removed. Private repositories
  connected to the project remain — only the link is removed.

## Pages inside a project

The page tree is a hierarchy, like folders and files. Any page can be:

- **created** via the "+" button in the tree — the page appears at
  the root or as a child (pick the spot with your cursor);
- **renamed** by double-clicking the name — everyone who has the
  project open sees the change within the same second;
- **dragged** with the mouse to another location in the tree —
  standard drag & drop, synced live;
- **deleted** via right-click context menu — a deleted page can be
  restored from the project history.

Each page has a URL like `/projects/{id}/{pageId}` that's handy to
share in Slack or email — the recipient lands directly on the page
(assuming they have access).

## Connecting repositories

The `/repositories` screen lists every repository you have access to.

- **Add from GitHub** — clones a new repository (requires the GitHub
  App to be installed; see Integrations).
- **Attach to project** — links an already-loaded repository with an
  existing project. A "Generate from repo" button appears on the
  project page that kicks off AI-driven documentation generation from
  the sources.
- **Detach** — removes the link. The repository stays in Nextdocs, the
  project stays too; only the generation path disappears.
- **Share** — give colleagues access to the repository (so they can
  attach it to their own projects).

## Typical scenarios

**New team joining, need a wiki from scratch.** Blank project → create
pages by hand → structure in the tree by department / topic.

**You have code, need API documentation.** From GitHub → pick the repo →
Nextdocs generates the first version → edit the key pages → connect
the AI chat to search across code.

**You have a Confluence base and you're migrating.** Export the
Confluence space as an HTML archive → From Confluence export → get a
mirror of the old structure in Nextdocs.

**Microservice project, 5 repos for one product.** Create one project
→ on the Repositories screen add all 5 repos → on the project page
attach each of them → AI chat searches across all attached repos at
once.

## Limitations

- 1 MB max per page (Yjs document). If you're planning to store a book
  — split it into chapter-pages.
- Bulk operations (mass delete, moving several pages at once) are not
  yet supported — only one at a time.
- Public-visibility projects aren't backed up separately from the
  project — a snapshot is taken automatically, but if the project is
  deleted, the public copy disappears too.
