# Notifications and activity feed

## Why it matters

The more active the team, the harder it is to keep track of
meaningful things happening to the documentation. Someone renamed a
page, someone mentioned you in a comment, someone connected a new
repository. Missing any of this means either duplicating someone
else's work or staying out of the loop.

Nextdocs has two different feeds that solve different problems:

- **Notifications** (bell 🔔 in the top-right corner) — personal
  events addressed to **you**. They require your attention.
- **Activity feed** (widget in the project page's right sidebar) —
  project-wide events, not only about you. Useful for orientation:
  "what's been happening around here lately".

## Notifications (the bell)

### What arrives

- **`@` mentions** — when someone wrote `@Your Name` in page text
  or a comment.
- **Access granted** — a project admin gave you access to a new
  resource.
- **Role change** — you were Editor, became Admin (or vice versa).
- **Access revoked** — your project access was removed.
- **Project invitation** — you were invited to a new project.

### Where to look

- **Bell** in the top-right corner. The badge shows unread count.
  Click opens a dropdown.
- **Toasts** — if an event happens while you're online, a card
  slides up from the bottom with a preview and an "Open" button.
  Click navigates. Auto-hides in 4 seconds (but stays in the bell).

### Tabs

The dropdown has two tabs:

- **Unread** — unread only (default).
- **All** — full history including read, up to the last 50.

### Statuses

- **Unread** — dot indicator on the left. Clicking a notification
  auto-marks it read.
- **Read** — no indicator, slightly dimmed.
- **Mark all read** — one-click badge reset.

### Clicking a notification

What happens:

- **mention in a page** — navigate to the page, scroll to the
  mention spot (cursor lands there).
- **mention in a comment** — navigate to the page, right panel
  opens to Comments, scroll to the specific comment, highlight.
- **access_granted / role_changed** — navigate to the project /
  resource in question.

If you open a notification via a toast, it's also marked read
(after ~2 seconds, once the backend persists the record).

## Activity feed

### Where to look

On the project page, right-side top bar — a pulse icon. Click opens
a dropdown with the last 50 events of **this project**.

### What lands in the feed

Events recorded there (all project members see the feed
identically):

- **page_created / renamed / moved / deleted** — page tree events.
- **repo_attached / detached** — repository link changes.
- **mention** — someone mentioned someone (entry "Alice mentioned
  Bob", click → page with mention).
- **comment_created / resolved / deleted** — new comments,
  resolutions, deletions.
- **page_edited** — aggregated event **once per day**: "Alice
  edited Design overview and 4 more". Collapses all edits by one
  author in one day, so the feed doesn't drown in micro-events.

Each item shows: who, what, when. Clicking an event with a page_id
navigates to the page (a comment event goes straight to the
comment via deep link).

### Pagination

First — last 50. A **Load more** button at the bottom pulls the
next block. Depth limit: 6 months back (further not available).

### Live updates

When the feed is open and something happens in the project —
the event appears at the top of the list without a reload.

## Difference from page history

Similar ideas, different scopes:

- **History** (right tab) — shows only **this page**, including
  content edits. Useful for rollback / diff.
- **Activity feed** — shows the whole **project**, no rollback,
  useful for "what's going on" orientation.

## Recently Visited

Related feature: the **Recently visited** widget on the
`/projects` screen. This is **your personal** recently-visited
pages, in chronological order. Don't confuse with a project
activity feed — this is about your own scroll-back.

- The widget is collapsed by default.
- Click "Recently visited" to expand.
- Shows the last 9 pages, in three columns.
- Click — navigate.

A "visited" entry appears only if you stayed on the page for more
than ~10 seconds (otherwise search-based browsing would pollute
the list).

## Digest and edit notifications

The daily "Alice edited 3 pages" digest is automatic, fires at
midnight in the server's local time. It can be triggered manually:

```
POST /api/internal/activity/digest
Header: X-Service-Secret: <secret>
Body: { "project_id": 42 }   # optional
```

Useful if you need to "catch up" the feed after an import.

## Privacy

- Notifications are private to you.
- Activity feed is visible to every project member. If you don't
  want your actions in the feed — currently not possible (only by
  limiting the actions themselves: don't edit others' work, don't
  comment).

## Typical scenarios

**You wake up in the morning.** Open Nextdocs, bell badge "3
unread". You see "Alice mentioned you at Design overview". Click
— land on the page, see the clarification, reply in the comment.

**Coming back from vacation.** Open the project, click the activity
icon. See "Bob renamed pages, Alice attached a new repository,
4 new comments resolved". Overall picture in 30 seconds instead
of reading the entire history.

**Tracking a spec status.** You wrote a spec, sent it to the team
for review. The activity feed shows who's commenting. If nothing
happens for 24h — nudge explicitly.

## Limitations

- Notifications are kept for **90 days**.
- Activity feed — for **6 months**.
- Push notifications (browser) and email digests are not yet
  wired up.
- "Turn it all off" settings are not available yet — you can only
  mark all as read.
