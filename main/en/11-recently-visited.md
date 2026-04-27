# Recently visited pages

## Why it matters

When documentation is big, you probably come back to the same
pages day after day. Yesterday you opened "Release process", the
day before "Auth flow", today you need "Auth flow" again. Looking
them up each time through the project tree or global search is
wasted seconds.

The **Recently visited** widget keeps your last-touched pages so
you can jump back with one click.

## Where the widget lives

Open `/projects` (the main screen with all your project cards).
Above the cards — a compact "Recently visited" header with a
clock-arrow icon. By default it's **collapsed** (to not waste
screen real estate for people who don't need it).

Click the header — expands the list:

- **3 columns** on wide screens (9 pages at once).
- **2 columns** on medium, **1** on narrow.

Row format: **page name — project — time**.

Click a row — navigate to the page. Time is short: "now", "3m"
(3 minutes ago), "1h", "4d", "2w". Exact time on hover (title
attribute).

## How it works

Every time you open a page and **stay there for more than 10
seconds** — Nextdocs records it in your "recently visited".

Why 10 seconds and not instant:

- If every open counted, the list would fill up with pass-through
  from global search, follow-mode, accidental clicks in the
  activity feed. Useless.
- 10 seconds is the informal threshold for "actually read /
  looked at, not an accidental flip".

The entry is refreshed at most once every 30 seconds for the
same page — so long reading doesn't create dozens of events.

## Collapse / expand

The "collapsed / expanded" state is stored **in your browser** (in
localStorage). If you expanded it, next time it opens expanded. If
collapsed — collapsed.

Each device has its own state (not synced via account) — by
design: on a big monitor you may prefer it expanded, on a laptop
collapsed.

## What's in the list

- **Only pages you currently have access to**. If you lost access
  (admin revoked), the page is removed from Recently visited on
  next load.
- **Only pages that still exist**. Deleted pages disappear.
- At most **9 entries** (grid size).
- Newest first.

## Difference from Activity Feed

- **Recently Visited** — **yours personally** (nobody else sees
  where you've been).
- **Activity Feed** — **shared in the project** (action history
  of the whole team).

## Privacy

- Does anyone else see your recently-visited? No, only you.
- Stored in the Nextdocs database or in the browser? In the
  database. Log in from another device — same list.
- Can you clear it? No UI button for now. If needed — contact
  support.

## Typical scenarios

**Monday morning.** Open Nextdocs. Recently visited suggests
"Release process (yesterday)", "Q4 roadmap (3 days ago)",
"Current sprint (today)". Jump straight to relevant context
instead of "now where was that…".

**Context switch between projects.** Working on two projects at
once, pages open from both. Recently visited mixes them into one
"last 9 pages across everything" list.

## Limitations

- Doesn't sync between browser tabs in real time — updates on
  reload / refetch.
- Doesn't support "pin a page". If you need a permanent
  favourites list — use browser bookmarks or a dedicated "My
  frequent links" page.
- No undo after "Clear all" (because Clear all doesn't exist
  yet).
