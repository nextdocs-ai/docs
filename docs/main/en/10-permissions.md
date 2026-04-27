# Permissions and invitations

## Why it matters

Documentation isn't always public. Architecture decisions, plans,
roadmaps, internal processes — sensitive. Meanwhile, inside a
company access needs to be flexible: juniors read-only, seniors
edit, contractors see one project and not the others.

Nextdocs has a four-level permissions model that covers most
scenarios without bloat.

## Four roles

| Role | What they can do |
|---|---|
| **Owner** | Everything Admin can + delete the project outright. The only role that can't be revoked. A project is automatically owner-ed by its creator. |
| **Admin** | Invite others, change roles, edit any content, attach / detach repositories, delete pages. Can't delete the project itself. |
| **Editor** | Edit pages, create new ones, comment, mention. No admin panels. Can't change permissions. |
| **Reader** | Read-only. Can leave comments and mentions (not counted as "editing"). No "create / delete page" buttons. |

## Inviting a new member

On the project page, gear menu → **Share / Manage access**. A modal
opens:

1. Field "Invite by email or name" — start typing email or
   name / login. If the user has an account in Nextdocs and you
   share at least one project, autocomplete picks them up.
2. If not — enter the full email and click "Invite". They get an
   email with a signup link.
3. Pick a role: Reader / Editor / Admin.
4. Click **Invite**.

The invitee:

- If they already have an account — gets a bell notification "You
  were added to project X".
- If not — gets an email "Create an account and go to project".

## Public projects

Projects with `visibility: public`:

- **Anyone can read**, even not logged in. Pages open via direct
  URL without authorization.
- **Only members can edit** — editing still requires Editor /
  Admin / Owner.
- **Indexed by Google** (see SEO note below).

Public is useful for open-source docs, public specs, marketing
content.

## Permission scopes

Permissions can be granted at three levels:

- **Project-level** — "Alice is Editor of project Foo". She sees
  all pages, can edit all.
- **Page-level** — "Bob is Reader of /design/architecture". Sees
  just this page (and sub-pages within his scope).
- **Repository-level** — "Carol is Reader of repo nextdocs/api".
  She can attach this repo to her own projects and search its
  code, but can't view projects that use the repo.

In everyday use 99% of grants are project-level. Page-level is
useful for confidential pages inside a shared project.

## Managing permissions

On the project page, in the Share modal:

- **Member list** with role labels.
- **Button next to role** — change to another.
- **Remove** — remove access entirely. The person stops seeing
  the project; they may get a "your access was revoked"
  notification (opt-out).

## Invite link

Alternative to email — an invite link in the Share modal:

- **Copy invite link** → short URL with a token is copied.
- Share via Slack / messenger. The recipient logs in (or signs up)
  — automatically receives the pre-set role.
- **Revoke link** — invalidates the token, the link stops working
  (those who already joined stay).

Handy for inviting a batch of people with one action.

## Lock / freeze a project

For projects that become "archive" (product sunsetted, team
disbanded, but docs are valuable), Owner can enable **Lock
project**:

- All Editor / Admin lose edit rights (read remains).
- New invitations are blocked.
- Only the Owner can unlock.

It's a soft mechanism — not deletion, just "freezing".

## What each role sees

**Reader**:
- Page tree, read-only editor, comments.
- History and Outline tabs are visible.
- Create / delete page buttons are hidden.
- Share modal opens but can't edit members.

**Editor**:
- Everything Reader + "+" buttons in the tree, page deletion,
  content editing.
- Share modal opens, can add **Reader** and **Editor** only (not
  Admin).

**Admin**:
- Everything Editor + role changes, repository attach/detach,
  tag creation, moving the project to archive.

**Owner**:
- Everything Admin + project deletion, toggling public ↔ private,
  transferring owner rights to another person.

## SSO / domain invites

For corporate customers: with SSO integration, any company
employee can request access via "Request access" (button on the
403 page). Project admins get a notification and approve with one
click.

## Limitations

- **Permission audit log** (who granted what when) — no dedicated
  page yet. The fact of grant / revoke shows up in Activity feed.
- **User groups** (e.g. "all engineers" in one click) — planned.
  Per-user only for now.
- **Invite expiry** — not supported. Invitations are permanent
  until Owner / Admin revokes.
- Page-level grants are per-page manual. For many pages in a row
  it's more comfortable to create a sub-project.

## Typical scenarios

**New team member.** Admin opens the Share modal, types their
email, picks Editor, clicks Invite. The person gets an invite
email and is in the project within two minutes.

**Leaver.** Admin opens Share → Remove. The person loses access
at the moment of click. No cache clearing — whatever they
loaded in the browser becomes 403 on next request.

**External contractor gets access to one section.** Admin finds
the page, gear → Share → invites the contractor as Reader.
Page-level permission is granted; they don't see the rest of the
project.

**Publishing release notes.** Project → Visibility: public.
Everyone outside can be left without invite — they open by link
without an account. Share in blog / twitter.
