# Profile and preferences

## Why it matters

When a team has 20 people and everyone `@`-mentions each other
and comments pages — your name needs to display the way you want
it. Not as `alex.teroshkin@banank.eu`, but as "Alexey Tereshkin"
or at least "alex".

The Profile section is your personal data that colleagues see when
you do things in the documentation.

## Where to find it

Top-right corner → click on the avatar → **Profile** in the
dropdown. Opens the `/settings/profile` page.

## What you can configure

### Nickname

Your main displayed name shown everywhere: in comments, mentions,
the online user list, edit authorship, notifications.

If the nickname isn't set, the system falls back via:
**first name + last name → first name → nickname → email**.

### First name and Last name

Optional fields. Useful if:

- You want colleagues to see your real name in documentation
  ("Alexey Tereshkin" in the Activity feed looks nicer than
  `alex.teroshkin@gmail.com`).
- You work in an organisation where given+surname is standard
  (finance, regulated docs, etc.).

If both are set — first line shows `First Last`, and the nickname
(if set too) is rendered as `@nickname · email` below.

### Email (read-only)

Shown for reference. Can't be changed through this screen —
contact support (email change requires re-verification and
affects authorship history).

### Avatar

Avatar is pulled automatically from the source you signed in
with:

- **GitHub login** — your GitHub avatar.
- **Email / OTP** — an initial on a coloured background.

Uploading a custom avatar isn't supported yet (planned).

## How to save

Change fields → **Save changes** becomes active if there are
unsaved changes → click. A green "Saved" strip appears after a
second, new data propagates to all colleagues immediately (their
nicknames update within minutes — when their JWT refreshes).

## Where it's displayed

| Place | What's shown |
|---|---|
| Comment / mention | `First Last` if present, else nickname, else email |
| Activity feed | Same resolveDisplayName |
| Online avatars in the top-right | Avatar + tooltip with name |
| Notifications "X mentioned you" | "Alice Smith mentioned you" |
| Edit author in History | Same name as in comments |

The same fallback chain is applied everywhere so the display is
consistent. If you see your email somewhere — you likely haven't
set first/last name or nickname; fill them in in the profile.

## Example

Say Alexey has:
- email: `alex.teroshkin@gmail.com`
- nickname: `teroshkin`
- first_name: `Alexey`
- last_name: `Tereshkin`

Comments show: **Alexey Tereshkin**, below — `@teroshkin ·
alex.teroshkin@gmail.com`.

Remove last_name → **Alexey**, below — `@teroshkin · alex@...`.

Remove both first_name and last_name → just **teroshkin**, no
subscript.

## Theme

In the same avatar menu — a **Dark Mode** toggle. Switches theme
instantly. Stored in local browser storage (separate setting per
device).

## Logging out

Avatar menu → **Log Out**. Signs you out from every tab, no
confirmation required. After logout, redirect to `/login`.

## Privacy

- Email is visible to other project members only if you typed it
  into a comment / page yourself. In system surfaces (Activity
  feed, mention) it's hidden.
- First / last name are visible to colleagues in projects you
  share.
- Third-party users with no common projects can't see your info
  (except public projects, where mentions use the display name).

## Limitations

- Custom avatar upload — not yet.
- Change email — via support.
- Nickname must be non-empty; up to 256 chars.
- First / last name — up to 128 chars each; UTF-8, any
  language.
- Account deletion — via support (GDPR-compliance, we erase or
  anonymise all data on request).

## Typical scenarios

**First login.** Set a nickname + first/last name right away.
Colleagues then see a normal name in comments instead of email.

**Moved from another company.** Old email, need to update the
profile. Open Profile, change nickname / name to current.

**International team.** First / last in Latin characters so
every colleague can read your name.
