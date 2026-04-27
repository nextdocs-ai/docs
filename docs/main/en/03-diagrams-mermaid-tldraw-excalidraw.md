# Diagrams: Mermaid, TLDraw, Excalidraw

## Why it matters

Documentation without diagrams is boring and hard to follow. System\
architecture, data flow, a user journey — a single picture explains\
it faster than ten paragraphs of text.

Nextdocs gives you three different ways to draw. All of them live\
directly in the page — no external tools, external files, or\
screenshots needed.

## Which tool for which case
| Tool | Input | Good for | Not good for |
| -- | -- | -- | -- |
| **Mermaid** | Text DSL | Flow charts, sequence diagrams, ER, Gantts, state machines — **when structure matters more than aesthetics** | Free-form drawing, arbitrary shapes |
| **TLDraw** | Mouse / trackpad | Architecture schemes, wireframes, UI mockups — **geometrically precise diagrams** | Text-DSL diagrams (flowchart etc.) |
| **Excalidraw** | Mouse / trackpad | Sketches, whiteboard notes, doodles — **hand-drawn feel** | Precise technical schemes (looks "handwritten") |

Rule of thumb: if you want a diagram editable in a PR review — pick\
Mermaid (it shows up in git diff). If you want to quickly throw an\
"idea on a napkin" — Excalidraw. If you need a precise scheme with\
alignment and snapping — TLDraw.

## Mermaid

### How to insert

1. Pick **Code** in the slash menu.

2. In the top-right corner of the block — a language dropdown. Pick\
   `mermaid`.

3. Enter the diagram code:

```
flowchart LR
    A[Start] --> B{Is user authed?}
    B -->|Yes| C[Load page]
    B -->|No| D[Redirect to login]

```

A picture renders right below the block. Edit the code — the picture\
re-renders in real time.

### What Mermaid can do

* **flowchart** — arrow diagrams (LR/TB directions).

* **sequenceDiagram** — participant interaction over time.

* **classDiagram** — UML classes.

* **erDiagram** — ER database models.

* **stateDiagram-v2** — finite state machines.

* **gantt** — schedules and planning.

* **pie** — pie charts.

* **journey** — user journeys.

Full grammar — <https://mermaid.js.org>.

### Tips

* Always specify direction in flowchart (`LR`, `TB`, `RL`, `BT`) —\
  without it, different Mermaid versions render differently.

* Comments start with `%%` — handy for notes to colleagues who'll\
  edit the diagram later.

* Syntax errors are displayed right in the block: the offending line\
  and token are highlighted in red, with a hint about what was\
  expected.

### Collaboration

While editing a Mermaid block, colleagues see your cursor (in the\
code, not on the SVG). The picture re-renders for everyone\
automatically.

## TLDraw

### How to insert

1. Slash menu — **Diagram**.

2. A built-in canvas about 400 pixels tall appears.

3. Draw: pick a tool on the left (rectangle, ellipse, arrow, text),\
   click-drag across the canvas.

4. For full-featured work — click the "expand" icon in the top-right.\
   The canvas opens in full-window mode.

### What TLDraw can do

* Geometric shapes with precise positioning.

* Snapping to other shapes.

* Arrows tied to shapes — when shapes move, arrows stay connected.

* Images — paste an architecture screenshot and annotate it.

* Several pages/layers inside one diagram (bottom panel has a picker).

* Export to PNG/SVG.

### Collaboration

Real-time: colleagues' cursors are visible, all changes apply\
synchronously. Two people can drag different shapes at the same time\
— no conflicts.

## Excalidraw

### How to insert

1. Slash menu — **Excalidraw**.

2. Same flow — built-in canvas, fullscreen via the icon.

### Difference from TLDraw

* **Hand-drawn style** — lines are "wobbly" with variation. Visually\
  resembles a fast whiteboard sketch.

* **Sticker images** — icons, emoji, pre-made elements.

* **SVG/PNG export** preserves the hand-drawn style.

Excalidraw is better for communicating ideas "in conversation":\
"Look, this is frontend, this is backend, the arrow is a request".\
For strict documentation that needs to last years — TLDraw or\
Mermaid are preferable.

### Collaboration

Also real-time, including live cursors.

## Search across diagrams

The internal Nextdocs search indexes text inside diagrams:

* **Mermaid** — source (node names, arrow labels).

* **TLDraw** — text inside shapes (label, name, rich text).

* **Excalidraw** — text in text elements, shape labels, frame names.

So if you labelled a rectangle "Auth Service", global search\
(Cmd/Ctrl+K) finds this diagram with the query "Auth".

Google search on public docs doesn't index diagrams **as images** —\
only surrounding text and captions.

## Fullscreen mode

The "expand" icon (top-right of any diagram) blows the editor up to\
the full viewport. ESC or another click to exit.

Fullscreen is comfortable for big diagrams; in-page is fast for a\
quick look + minor tweak.

## Limitations

* **Mermaid**: 2 MB per block. Very large graphs can slow down\
  editing.

* **TLDraw / Excalidraw**: the snapshot is stored in page attributes;\
  recommended size of a single diagram — up to \~1 MB (that's a lot of\
  shapes, rarely needed in practice).

* **Export diagrams to PDF** — happens through the general page\
  export (PDF is built from the whole content, diagrams rasterised).

* **Importing Excalidraw from** `.excalidraw` **files** directly isn't\
  there yet — workaround is "select all in your native app → paste\
  into our canvas".
