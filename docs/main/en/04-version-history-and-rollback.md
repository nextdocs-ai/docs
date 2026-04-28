# Version history and rollback

## Why it matters

A documentation page lives for a long time — and gets touched often.\
A month from now someone rewrites a paragraph, three months later\
someone deletes half of it, six months in someone renames it. When\
a team has 10 people it's important to answer:

* "Who wrote this and when?"

* "What was here before Pete redid everything?"

* "Can we roll back to yesterday's version?"

Nextdocs history gives you all of this automatically. No manual\
"snapshots" required — every meaningful change is saved.

## Where to find it

The right panel in the editor has three tabs. One of them is\
**History**.

The list shows:

* **Event type** — page created, renamed, moved in the tree, edited,\
  restored, AI-generated, updated by the AI agent.

* **Who did it** — user name, or "Agent" for changes from the\
  AI generator.

* **When** — relative time ("5 minutes ago", "2 days ago") plus an\
  exact date on hover.

* **Edit session duration** (for content edits) — e.g. "edited for\
  12 minutes": if someone edited for half an hour with pauses, it's\
  one entry, not thirty.

## What counts as "one entry"

Nextdocs doesn't save a snapshot after every keystroke — that would\
bloat history to thousands of useless entries. Instead:

* **A pause of 5+ minutes** closes the current edit session. If you\
  typed for 20 minutes without breaks, it's **one** history entry\
  showing the full result.

* **Author change** also ends the session. If a colleague saved an\
  edit 30 seconds after you — **two** entries.

* **Renaming a page** — always a separate entry, even inside an\
  edit session.

* **Tree move** — separate entry.

* **Page delete** — the only way to "lose" a page. Its entry stays\
  in the project history; recovery is a separate mechanism (see\
  "Restoring deleted pages" below).

## How to view an old version

1. Open the **History** tab.

2. Click the entry you're interested in.

3. The page text in the main window switches to that version. It's\
   a **preview** — you're reading, not editing.

4. A banner appears on top: "Preview of version from 22.04.2026\
   14:32" with buttons:

   * **Rollback to this version** — make this version the current\
     one. Rollback doesn't delete history — a new entry "Petr\
     restored version from …" is added.

   * **Cancel** — back to the current version, no changes.

## Rollback and its side effects

When you roll back:

* Current page content **is not lost** — it moves into history as the\
  previous version.

* A new entry appears: "Pete rolled the page back to 22.04.2026".\
  Metadata records which version was restored.

* Colleagues with the page open at that moment instantly see the\
  updated content. They may get a toast that the page was rolled\
  back.

So rollback is safe: you can't "lose" edits; you can always roll\
forward again.

## Restoring a deleted page

When someone deletes a page outright, it goes into project history\
with `deleted` status. To bring it back:

1. Open the project menu (gear next to the project name in the page\
   header).

2. **Project history** → list of all events in the project.

3. Find the `page_deleted` entry for the page.

4. **Restore** button — the page returns to the tree in the same\
   spot, with its content as of immediately before deletion.

Restoration is possible for **90 days** after deletion. After that,\
deleted pages are physically removed.

## Diff between versions

Clicking a history entry opens a preview. To compare two versions\
line by line:

1. Click the first version (it'll be highlighted green).

2. Shift-click the second (highlighted red).

3. The main window shows a diff: added — green, removed — red,\
   renamed blocks — blue.

## Agent activity

If the project is linked to a repository and the AI doc generator\
ran — its entries are highlighted as a separate type (`agent_generate`,\
`agent_update`) with a robot icon. These entries behave exactly like\
human ones: rollback, diff, preview all work on them.

That's handy when the agent generated something wrong — you can\
quickly roll back to the last "human" version.

## Limitations

* **Full history is kept for 1 year**, after which old entries are\
  collapsed into "start-of-month" snapshots.

* Concurrent Yjs editing generates many micro-updates inside a\
  session — they are **not** stored separately. History is\
  high-level entries, not a CRDT log.

* History does **not** include changes to comments or permissions\
  (those live in Activity feeds).

* Diff is plain-text-based — complex diagrams may look odd (JSON\
  diff). For visual comparison of diagrams it's easier for now to\
  open two versions in two tabs.

## Typical scenarios

**"A colleague broke the page."** Open History, find the last "good"\
entry, preview, confirm, rollback. One minute of work.

**"I want to understand why we landed on this wording."** Open old\
versions one after another — you see how the section evolved.\
Sometimes the metadata has a PR link (if the change came from the\
AI agent on a code update).

**"The agent generated garbage on top of our edits."** Open history\
— the last human entry before the agent. Rollback. Then in project\
settings you can explicitly tell the agent not to regenerate this\
section.
