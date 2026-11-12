# GitHub App: access and organisations

## Why it matters

Connecting a repository looks like one click, but it answers two\
questions that are easy to confuse:

* **Can Nextdocs read this repository?** — decided on GitHub,\
  when someone installs the App.

* **May this organisation have a copy of it?** — decided in\
  Nextdocs, per organisation.

Treating the first as an answer to the second is the mistake\
worth naming: an installation is permission given to an\
application, not permission given to everyone who uses that\
application.

## What installing the App means

The GitHub App is installed **on a GitHub account** — your\
personal account or a GitHub organisation — and covers the\
repositories chosen during installation. Read-only on contents\
and events; no commits, no pull requests.

Two consequences people run into:

* **One account, one installation.** Running the install flow\
  again for the same GitHub account doesn't create a second\
  installation — it reconfigures the existing one. There is no\
  "per-team" installation of the same account.

* **The installation is not a Nextdocs permission.** It says the\
  App may read those repositories. Which Nextdocs organisations\
  may act on that is a separate decision, and each organisation\
  makes it for itself by running the install flow from its own\
  workspace.

So if two teams use different Nextdocs organisations against the\
same GitHub organisation, each connects the App from its own\
workspace. They end up pointing at the same installation on\
GitHub's side, each having proved it controls that account.

## One organisation, one copy

A GitHub repository can be connected in several Nextdocs\
organisations at once. Each connection is a **separate copy**,\
and the separation is complete:

| What | Shared? |
|---|---|
| The clone on disk | No — one per organisation |
| The code index and graph | No |
| README stored in Nextdocs | No |
| Repository name in Nextdocs | No — rename affects your copy |
| Who has access | No |
| Deleting it | No — your copy only |

Connecting the same repository twice **inside one organisation**\
does nothing new: you get the repository you already have, not a\
second copy of it.

What the copies do share is the source. A push to the default\
branch updates every connected copy — each one pulls, re-indexes\
and refreshes its own pages, on its own schedule and under its\
own access rules.

### Why not one shared copy

A shared clone would mean one organisation's deletion removes\
another organisation's data, one organisation's rename shows up\
in another's service map, and — the part that matters most —\
private code sitting in storage that serves requests for people\
who were never given it. Copies cost disk; sharing costs\
isolation.

## When access goes away

Removing the App from a GitHub account, or dropping a repository\
from the App's selected list, ends Nextdocs' read access to it.

* Pages already generated stay. They are yours: documentation,\
  not a mirror of the code.

* Updates stop. No pulls, no re-indexing, no regeneration on\
  push.

* The repository page says so rather than failing quietly.

Re-installing restores the link and the next push picks up where\
it left off.

## Frequently asked

**"I connected a repository and got one with an older id — why?"**\
Because it already existed in this organisation. Connecting is\
idempotent within an organisation.

**"We're two separate companies using one shared GitHub org."**\
Each company connects from its own Nextdocs organisation. Each\
gets its own copy, its own access list and its own documentation;\
neither can see the other's edits.

**"Does connecting a repository give my whole team the code?"**\
It gives your organisation a copy under your organisation's\
access rules — the same rules that govern projects and pages\
(see *Permissions and invitations*).

**"The repository is private and the App isn't installed."**\
Then it can't be connected. Public repositories work without an\
installation; private ones don't, and no amount of knowing the\
URL changes that.
