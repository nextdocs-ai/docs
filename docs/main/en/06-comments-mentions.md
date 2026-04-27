# Comments and mentions

## Why it matters

When documentation is written collectively, discussions are
inevitable. Someone dislikes a phrasing, someone doesn't understand
a term, someone asks for clarification. If the discussion happens in
Slack/email, the context is lost: a month later nobody remembers why
the doc says what it says, or what the alternatives were.

Comments in Nextdocs are attached to a specific spot in the text.
They stay anchored even if the surrounding text is fully rewritten.
The whole discussion sits next to the spec it's about.

`@` mentions are how you summon someone into a discussion: they get
a notification with a direct link to that comment.

## How to leave a comment

1. Select the fragment you want to ask about / suggest on.
2. A floating toolbar appears above the selection. Click the
   speech-bubble icon → **Comment**.
3. The right panel opens (the **Comments** tab), with the quoted
   fragment pre-filled.
4. Type the text. Enter sends, Shift+Enter makes a new line,
   Escape cancels.

On the page, the quoted fragment is highlighted. Click the
highlight → scrolls to the corresponding comment in the right panel,
and vice versa.

## What goes into a comment

- **Plain text**, bold / italic via Cmd/Ctrl+B / Cmd/Ctrl+I.
- **Mention** — type `@`, pick a person from the list.
- **Links** — just paste a URL; they're auto-detected. Links to
  other Nextdocs pages work as usual.
- **Line break** with Shift+Enter.

Long stretches of code / tables are better not pushed into a
comment — comments are designed for short discussions, 1–5
sentences.

## Threads

Reply to a comment — click the "Reply…" tab under it. A mini-editor
opens. The reply becomes part of the thread, shown indented.

A thread can have any number of replies. Chronology is preserved.

## Resolve

When a discussion is done and the question is answered — anyone in
the thread can hit **Resolve**. The comment is visually dimmed
(semi-transparent), but not deleted. You can always reopen to see
history, or click **Unresolve** if the discussion is live again.

The goal is to keep active discussion visible and archived ones
below.

## Deletion

A comment can be deleted by:

- The author;
- A project administrator.

Deletion is irreversible, the thread history is gone. Usually
better to Resolve rather than delete.

## `@` mentions

### Where they work

- **In page text** — right in a paragraph. Type `@iv` — the list
  suggests project members with matching names; pick one. The
  text gets an "@Ivan" chip.
- **In a new comment** — same mechanism. Mentions in comments are
  especially useful: "@Peter, can you confirm this endpoint is
  deprecated?"
- **In a reply** — the same.

### Who's in the list

- In page text and comments — **only members of this project**
  (not all system users). Prevents accidentally mentioning someone
  without access.
- When inviting new members to a project (separate modal) — search
  across **all users you share at least one project with**. Lets
  you quickly pull in a familiar colleague without the full email.

### What happens after a mention

1. On comment send / page save — the mentioned users get a
   notification.
2. The bell 🔔 in the top-right corner shows an "unread" badge.
3. If the mentioned user is online — a toast pops up with a preview
   and an "Open" button.
4. Click on the notification / toast — navigates to the specific
   page, the comment panel opens automatically and scrolls to the
   mention.

### Deduplication

Mentioning one person 5 times in a single comment → one
notification. Mentioning them again in another comment within 10
minutes → also one (in the activity feed) to avoid spam.

`@` notifications in personal notifications (the bell) are
rate-limited: one per hour from one author to one recipient per
resource.

## Navigation and deep links

- Click any comment in the right panel — scroll in the text to the
  quoted spot, highlight flashes.
- The page URL can contain `#comment-{id}` — opening that link
  auto-opens the comment panel at the right spot. This is the
  link format used in notifications and the activity feed.
- "Copy link" button next to every comment — copies a deep link to
  the clipboard.

## Typical scenarios

**Spec review.** PM wrote a user story. Tech lead / team open the
page, walk through the sections, highlight unclear spots, leave
inline comments. PM replies, adds detail. Each thread is closed
with Resolve after the answer. The document retains a clean spec,
the discussion stays in comment history.

**Contradiction flag.** You noticed section A contradicts section
B. Highlight, leave "@Maria, here and in the 'Security' section —
they contradict, which is right?". Maria sees the notification,
fixes it, resolves.

**Question for the author.** You're reading someone else's project
docs. Something's unclear. Select, `@author, what was meant here?`.
You don't leave the reading context and get the answer right
there.

## Limitations

- ~2000 character soft limit per comment (for long discussions it's
  more natural to create a page).
- Attachments (images, files) in comments aren't supported yet —
  links only.
- Emoji reactions on comments (~like, thumbsup) — planned.
- Offline comments aren't supported: a comment won't send until the
  connection is restored.
