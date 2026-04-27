# Tables

## Why it matters

Tables are one of the most common ways to structure data in
documentation: solution comparisons, responsibility matrices,
release plans, endpoint lists, configs. And, at the same time,
one of the most annoying features in most wiki tools: rigid
column widths, broken pasting from Excel, no comfortable way to
edit.

In Nextdocs a table is a full first-class block. All operations
on it happen through a hover menu, no modals, no settings. Working
with it should feel as fast and natural as in Excel or Google
Sheets.

## Inserting a table

### From the slash menu

`/` → **Table** → inserts a 3×3 table. The first row is a header
by default (bold, fixed font).

### From the clipboard

See the "Pasting from the clipboard" section in
[Editor](02-editor.md):

- **From Excel / Google Sheets** — Cmd+C a range → Cmd+V in
  Nextdocs → a table with the correct size and contents.
- **CSV / TSV** — text with commas / tabs becomes a table
  automatically.
- **HTML table** — copying a web page with a `<table>` gives you
  our table.
- **Markdown pipe-table** — standard markdown syntax
  (`| col | col |`) is parsed.

## Floating menu above the table

Hover over the table — a toolbar appears above its top edge. From
there:

### Adding rows and columns

- **Add row** / **Add column** — adds a row below / column right
  of the current cursor position.
- Alternative — Tab in the last cell of the last row creates a
  new row.
- Shortcuts: Cmd/Ctrl+Shift+↓ / → — adds row / column.

### Deletion

- Select row / column (click the indicator on the left / top) →
  "Delete row/column" in the menu.

### Reorder

- Drag row / column indicators with the mouse — changes order.
  Works with animation, you can see where it'll land.

### Cells

- Merge / split cells via right-click context menu.
- Alignment (left / center / right) for cell text.
- Cell background colour to highlight important bits.

## Content formatting

Full formatting set inside each cell:

- Bold / italic / inline code / link.
- Multi-line text (Shift+Enter inside a cell — new line).
- Checklists in a cell (`/checklist`).
- Bulleted / numbered lists.
- Images — the cell resizes to the image.
- Links to other pages (`@` + page name — autolinks).

## Fullscreen mode

The "expand" icon in the bottom-left of the table — opens it in
its own overlay. In fullscreen:

- The whole table is visible without horizontal scroll.
- Comfortable for 20+ column tables.
- ESC / click "shrink" — back to the editor.

The result is synced automatically: whatever you changed in
fullscreen applies in the main editor (and for colleagues).

## Export to Excel

**Save as Excel** button (in the toolbar). Downloads an `.xlsx`
with the current table's contents. Preserved:

- Cell contents (text, numbers).
- Row headers.
- Column order.

Not preserved: formatting (bold / italic), colours, hyperlinks
(the text itself is pasted). For pixel-perfect compatibility with
Excel — make the table there.

## Copy as HTML

Select the table in Nextdocs → Cmd+C → paste into Gmail / Slack /
Word. It pastes as an HTML table close to the original visually.
Handy for report distribution.

## Sort and filters

Not yet. Nextdocs tables are primarily a tool to present data to
humans, not a mini-spreadsheet. If you need pivot / sort /
formulas — build them in Google Sheets and paste the result into
the docs.

## Co-editing

Tables are a CRDT document like the rest of the editor:

- Two people can edit different cells at the same time without
  conflicts.
- The colleague's cursor is visible in the cell they're typing
  in.
- If both edit the same cell — merges happen just like in a
  regular paragraph: characters interleave, nothing is lost.

## Deep linking

Right-click a cell → **Copy cell link**. Gives you a
`https://nextdocs.ai/projects/.../page#cell-ab12` URL that you can
share in Slack — the opener lands directly on the cell and it's
highlighted.

## Search

Full-text search (Cmd/Ctrl+K, **Table** filter) searches cell
contents. A match highlights the specific cell on page open.

## Typical scenarios

**Product comparison** (like the table in
[13-comparison.md](13-comparison.md)). Properties in rows,
products in columns. Fill with ✅ / ❌ / ⚠️. One table replaces
five paragraphs of text.

**Responsibility matrix (RACI).** Roles in columns, activities in
rows. Cells — R / A / C / I. Shared via a cell link when
discussing a specific task.

**Release plan.** Version / Date / Features / Owner / Status.
Each row — a release. Updated by the team in real time.

**Env variables / API endpoints.** Name / Description / Example
value. Standard way to document configs.

**Data import from a spreadsheet.** Select a range in Google
Sheets → Cmd+C → Cmd+V in Nextdocs — table populated. Good for
one-off dashboard snapshots.

## Limitations

- **Max ~50 columns × 500 rows** per table. Above that the editor
  slows down (especially in fullscreen).
- **No formulas or computations.** Use Google Sheets / Excel.
- **No autofill** (like drag-fill in Excel).
- **No pivot tables** (group-by, aggregation).
- **Splitting a table across pages on PDF export** — in progress;
  very large tables export with horizontal scroll.
