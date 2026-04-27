# Editor and slash commands

## Why it matters

The Nextdocs editor is where you actually write documentation. It's
built on TipTap / ProseMirror and works like Notion or Confluence:
type plain text, add structured blocks (headings, lists, code, tables,
diagrams) as you go.

The key difference is that everything is live. Your colleague watches
you type in the same page; your cursor is visible to them, theirs to
you. No "Save" buttons — everything is synced automatically.

## How to open it

Open any page in a project (click its name in the tree on the left) —
you're immediately in the editor. The page title is edited in-place
(first line — `# Title`), the body follows.

## How to format

### Basic keyboard shortcuts

Standard markdown shortcuts work:

| Input | Result |
|---|---|
| `# ` at the start of a line | H1 heading |
| `## `, `### ` | H2 / H3 headings |
| `**bold**` or `Cmd/Ctrl+B` | **bold** |
| `*italic*` or `Cmd/Ctrl+I` | *italic* |
| `` `mono` `` | `monospace` |
| `> quote` | Block quote |
| `- item` or `1. item` | Bulleted / numbered list |
| `[ ] task` | Checklist |
| `---` on a blank line | Horizontal rule |

Ctrl/Cmd+Z — undo, Ctrl/Cmd+Shift+Z — redo. History is local to the
current session: recent steps can be rolled back, but once you close
the page, Ctrl+Z is no longer enough — use the **History tab** in the
right panel (see [History](./04-history.md)).

### Slash commands (`/` menu)

Type `/` on an empty line — a menu of every available block pops up.
You can type the name (e.g. `/table` or `/code`) to filter. Arrow keys
↑/↓ to select, Enter to insert.

Available blocks:

- **Text** — regular paragraph (exits any formatting).
- **Heading 1/2/3** — headings at different levels.
- **Bulleted / Numbered / To-do list** — lists.
- **Quote** — block quote.
- **Code** — code block with syntax highlighting (language picker in
  the block's upper-right corner).
- **Table** — a table. Defaults to 3×3; columns/rows added via the
  hover menu. Tables can be exported to `.xlsx` via the "Save" button.
- **Image** — image upload. The file goes into our S3-compatible
  storage, only a link stays in the text (not base64), so the page
  doesn't bloat.
- **Diagram** — TLDraw editor: geometric schemes, arrows, stickers.
  See [Diagrams](./03-diagrams.md).
- **Excalidraw** — Excalidraw sketch in hand-drawn style. Same doc.
- **YouTube** — video embed via URL.
- **Demo · …** — interactive demo widgets (grow over time — a way to
  show live examples right in the documentation).

### `@` mentions

Type `@` anywhere — a popover opens with people in the project. Pick
a colleague — an `@Name` chip appears in the text, and the person is
notified. Details — [Comments & mentions](./06-comments-mentions.md).

### Links

Select text, press `Cmd/Ctrl+K`, paste a URL. Or just paste a URL next
to selected text — it auto-converts to a hyperlink. Hover shows a mini
popover with preview and Edit / Remove buttons.

If you paste a link to another Nextdocs page (format
`/projects/42/17`) — the reader lands directly on it.

## Pasting from the clipboard

The editor tries to interpret what you paste intelligently. It guesses
the format and normalises it to its own schema — no settings, no
plugins. Details below.

### Google Docs / Word / Pages

Copy paragraphs from Google Docs, paste into Nextdocs. Preserved:

- H1/H2/H3 headings (recognised from Google Docs "Heading 1/2/3").
- Bulleted and numbered lists (with correct nesting).
- Bold / italic / underline.
- Links (URL + anchor text).
- Quotes — blockquote.
- Inline code, code blocks.
- Images — pasted into the document (each image is automatically
  uploaded to our storage, **nothing stays as base64**).

Lost:

- Google-specific fonts (we use a unified Inter + Fira Code).
- Text colours, highlights, multi-colour underlines — normalised to
  standard (rainbow-styled docs are rare in documentation).
- Google Docs tables — come across as Nextdocs tables; see
  [Tables](./14-tables.md).

### Notion

Copy a page (or any block) from Notion → paste. Supported:

- **Toggle** (collapsible block) — becomes our `Details`.
- **Callout** (coloured block with icon) — becomes blockquote or
  `AlertBlock`.
- **Heading 1/2/3** — headings.
- **Bulleted / numbered / to-do list** — lists and checklists.
- **Table** — table.
- **Code** — code block, language preserved.
- **Quote** — block quote.
- **Image / file** — images. File attachments as links.
- **Notion inline mentions** — converted to plain text with the name
  (our `@` mentions are re-established manually only — see
  [Comments & Mentions](./06-comments-mentions.md)).

Lost: Notion-specific databases (database views), Figma / Miro
embeds (link stays, rendering doesn't), pages-as-relations (turn
into links).

### HTML

Any HTML from a browser — articles, Confluence, internal portal
pages, web archives. Same grammar as Google Docs: headings, lists,
tables, links, images, `<code>`, `<pre>`.

If the HTML contains complex attributes (inline CSS, `style="..."`),
they're normalised to our theme. Scripts and iframes are removed
for security.

### Markdown

Paste a `.md` file, a block from ChatGPT, or any pre-formatted
markdown — it becomes proper blocks:

- `# Heading` → headings.
- `- Item` / `1. Item` → lists.
- `[text](url)` → link.
- `![alt](url)` → image (external URL stays external, base64 blob
  uploads to storage).
- ` ```lang ... ``` ` → code block with language.
- `> quote` → blockquote.
- Pipe-format tables → full tables.
- `| Mermaid / TLDraw` blocks — if it's a markdown fence in our
  syntax (`:::editorCanvas ... :::`) — the diagram is restored.

If the clipboard has raw markdown without explicit signals, we still
try to detect markdown syntax and convert it. If nothing matches —
pasted as plain text.

### Tables from Excel / Google Sheets / Numbers

Copy a range of cells in Excel, paste into Nextdocs. You get our
table with proper columns/rows. Preserved:

- Cell contents (text, numbers, percentages).
- Bold headers, if they were in the source.
- Hyperlinks in cells.

Lost:

- Formulas (the result is pasted, not `=SUM(A1:A10)`).
- Conditional formatting (cell colours).
- Merged cells — become regular (value duplicated).

More on tables — [Tables](./14-tables.md).

### CSV / TSV

A table special case. If the clipboard contains comma- or
tab-separated text in a standard rows-columns shape — the parser
auto-detects CSV/TSV and creates a table. Handy for pasting from
`curl | jq -r`, database exports, logs.

### Screenshots and images

- **Cmd+V of a screenshot** (Cmd+Shift+4 on macOS) — the image is
  pasted immediately. The file uploads to storage asynchronously —
  you see an "Uploading…" toast, and the placeholder is replaced by
  the image once done.
- **Drag-and-drop a file** into the window — same flow.

Supported: PNG, JPEG, GIF, WebP, SVG. Up to 20 MB per file.

### PDF

PDF can't be pasted through the clipboard (it's binary), but there's
a PDF import at the page level:

- **On an empty page** — slash menu → "Import PDF" → pick a file.
  The PDF is parsed, text + basic structure (headings, paragraphs,
  lists) laid out as a new page.
- **As a file attachment** — drag a PDF into the editor window,
  choose "Attach as file". A link-attachment is inserted (click
  opens the PDF in a new tab).

More — [Integrations → PDF](./09-integrations.md#pdf).

### ZIP / archives

Drop a ZIP into the window — a menu appears: "Upload attachment /
Try to import as repository". The second option only works at the
project level (creates pages from the archive contents) —
[Integrations](./09-integrations.md).

## Smart normalisation

A central idea of the editor: you paste from anywhere, and
**everything becomes part of Nextdocs's unified typography**. No "the
font is off", "the heading size is wrong". Paste freely — styling is
homogenised automatically.

The same works in reverse: **when you copy from Nextdocs** into Word
/ Slack / Notion / email — the recipient sees a properly formatted
chunk, not an HTML mess.

## Drag & drop

- **Drag a file** into the editor — works for images and archives.
- **Drag a block** — every block has a "handle" on its left
  (appears on hover). Drag it up or down to re-order.
- **Drag a page** in the left tree — changes hierarchy.

## Find and replace

`Cmd/Ctrl+F` opens a search bar in the current page. Works like any
editor: matches are highlighted, Enter jumps between them.
`Cmd/Ctrl+Shift+F` switches to find-and-replace (if you have write
access).

`Cmd/Ctrl+K` — opens **global search + AI agent** (details:
[Search](./08-search.md) and [AI Agent](./08a-ai-agent.md)).

## Table of contents (ToC)

The right panel in the editor has several tabs:

- **Outline** — auto-generated table of contents from headings. Click
  an item to scroll to that heading. We recommend structuring the
  document with headings, not bold text, so the ToC is useful.
- **Comments** — page comments (separate section).
- **History** — page versions (separate section).

## Limitations

- One document — ~1 MB max. For more — split into subpages.
- Nested lists — 4 levels max (technically more is possible, but the
  visuals break).
- Arbitrary iframe embeds aren't possible yet; safe embeds (YouTube,
  Mermaid, TLDraw, Excalidraw) — via slash commands.
- Editing **one** block with two people at once works, but isn't
  always comfortable (the other person's cursor can "push" yours).
  Teams usually write different sections.
