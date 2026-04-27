# Collaborative editing and presence

## Why it matters

Documentation is never written alone. Someone throws together a
draft, someone fills in sections, someone transcribes a meeting,
someone fixes typos. In the classic flow this leads to hell: "Vasya,
you were editing the file at the same time as me — now re-read both
versions and merge by hand".

Nextdocs is designed so that multiple people work on the same page
at the same time, and **nothing breaks**. Like Google Docs — but for
technical documentation.

## What it looks like

You open a page. In the top-right corner you see avatars of everyone
currently viewing or editing it. Each avatar has:

- **A coloured ring** — unique per user. The same colour highlights
  their cursor in the text.
- **A small indicator** under the avatar — where they are right now
  (this same page, another page in this project, or just online
  in the system).

In the text you see live cursors — a vertical bar in their colour
with their name, moving as they type. Their text selections are
highlighted too.

In diagram blocks (TLDraw, Excalidraw) — same cursors, but in the
scene space of the canvas.

## Simultaneous editing

You and a colleague edit the same paragraph at once — what happens?

- **Editing different spots** — no conflicts, edits interleave:
  each of you sees both your own and the other's edits.
- **Editing one block** — the system uses CRDT (Yjs), conflicts
  resolve automatically. In practice: cursors may "push" each
  other, but characters can't be lost.
- **Connection drops** — keep typing. Nextdocs buffers changes
  locally in the browser; when the network returns they're sent
  automatically. If a colleague also wrote meanwhile, the changes
  merge.

## Connect / disconnect

- The page automatically establishes the connection on open (via
  WebSocket to NATS + Hocuspocus). You don't do anything.
- The page disconnects when you close it. Your avatar drops from
  others' "online" list within ~20 seconds.
- If you quietly left for coffee for an hour without closing the tab
  — colleagues still see you as "online" but the cursor freezes.
  That's normal.

## Follow mode

Double-click a colleague's avatar in the top corner to enable
**Follow** — you auto-navigate to the page they're on, and follow
their scroll / page switches.

Why:

- **Walkthrough** — someone on the team gives a tour of the doc
  structure. Others enable follow and see the same thing.
- **Pair editing** — one edits, the other watches and comments.
- **Onboarding a new team member** — they follow the tech lead
  for a couple of hours, watching how work is done.

Leave follow: ESC, click anywhere in the editor, double-click the
same avatar again, or click another one.

A single click on an avatar is **jump** — a one-off navigation to
the colleague's page + cursor position without subscribing.

## Different pages in the same project

Avatars on your page may show people who are on **other** pages of
the same project right now. You can tell by the indicator: the
avatar is dimmed, not pulsing. Useful to see who's active in the
project overall.

Clicking such an avatar navigates to their page.

## Comments and mentions

A separate mechanic, tightly related to collaboration. See
[Comments & Mentions](06-comments-mentions.md).

## Presence and privacy

The fact that you're reading a page is visible to every project
member (those with access). That can be considered a feature, not a
bug: it's useful to know your manager actually read your spec and
didn't come back with questions — so the spec was OK.

If you need "silent" reading (no presence) — switch on **Invisible
mode** in profile settings (coming soon — currently always on).

The list of pages you've been to is saved for **you** in the
"Recently Visited" widget on the home page. Colleagues don't see
this list.

## Offline and sync

- On connection loss you see a "Connection lost, retrying…" strip
  at the top of the page.
- While offline you can keep typing. Everything is saved locally in
  the browser's IndexedDB.
- When the connection is restored — changes are sent, confirmed,
  and anything new from colleagues is pulled.
- If you close the tab before the connection returns — **nothing is
  lost**. On next page open the unsent edits are still local and
  will sync then.

## Typical scenarios

**Team retro.** The host opens the page, others enable follow.
Everyone writes their points into Plus / Minus / Actions sections.
The host drives, all cursors are visible. Moving to the next item
— scroll, others follow.

**Four-handed feature spec.** Product opens the page, writes the
user story. Engineer joins, adds technical design. Neither waits
for the other to "close the file".

**Docs code-review.** Two people open a PR branch in Nextdocs
(which the AI agent generated from code). One goes top-to-bottom
making inline comments, the other replies. The activity feed on
the side shows the edit history.

## Limitations

- A single document comfortably handles **5–10 concurrent editors**.
  More works but may have micro-lag.
- Mobile browser — read and short edits work, but the main UX is
  tuned for desktop.
- Follow mode across viewports of different widths — scroll
  position is approximate (different layouts).
