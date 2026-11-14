# Agent setups

An agent setup says **where** an agent works on a task. It is picked when a task is taken or handed to a runner.

| Field | What it decides |
|---|---|
| **Where** | The computer that takes the task, or a connected runner |
| **Network access** | Full, limited to a list of domains (package managers optional), or none |
| **Setup script** | Commands run in the task folder before the agent starts — `pnpm install`, `docker compose up -d postgres` |
| **Values from** | The environment whose variables the agent and the script get |
| **Repositories** | Only these may be planned and changed; empty means any |

A setup keeps **no values of its own**. It names one environment of the same owner — a workspace setup one of the workspace's environments, your own setup one of **My environments** — so `preprod` for an agent is exactly `preprod` for a reader of the documentation. To change a value, edit the environment; every setup that names it picks the change up for its next task.

## From taking a task to the agent starting

```mermaid
sequenceDiagram
  actor P as Person
  participant N as Nextdocs
  participant M as Computer or runner
  participant S as Setup script
  participant A as Agent

  P->>N: takes a task, picks the setup "preprod e2e"
  N->>N: pins the setup's version and its environment's version
  N->>M: the task
  M->>N: the setup and the values of that version
  N-->>M: Values, and Secrets only to the setup's runner
  M->>M: adds values kept on this machine
  M->>M: makes worktrees for the repositories
  M->>S: runs the setup script with the variables
  S-->>M: done, or the task stops with the script's output
  M->>A: starts the agent with the variables in its environment
  Note over A: the agent can read every variable it was given
```

The versions are pinned when the task is taken: editing the setup or its environment later does not change a task already under way.

## Which values reach the agent

```mermaid
flowchart LR
  ENV["Environment the setup names"]
  ENV -- "Value" --> BOTH
  ENV -- "Secret" --> RUNNER_ONLY{"Runs on a runner?"}
  RUNNER_ONLY -- "yes" --> BOTH
  RUNNER_ONLY -- "no, on a desktop" --> LOST["not given — the variable is missing"]
  ENV -- "On this computer: name only" --> LOCAL{"Where it runs"}
  LOCAL -- "desktop" --> KEPT["Settings → Secrets →<br/>Values kept on this computer"] --> BOTH
  LOCAL -- "runner" --> FILE["the runner's env-secrets file"] --> BOTH
  BOTH(["Agent process and setup script"])
```

The setup form warns when this happens: a **Secret** in the chosen environment does not reach a setup that runs on the computer taking the task. Keep such a variable **On this computer**, or run the setup on a runner.

Some names are kept by the runner itself and cannot come from an environment a setup uses: `PATH`, `HOME`, proxy settings and anything starting with `ANTHROPIC_`, `OPENAI_`, `GIT_`, `GITHUB_`, `NEXTDOCS_` and the like. A setup refuses such an environment until the variable is renamed.

## The network and what it is not

On a computer or a runner, limited or no network is an agreement with the agent — it is told the rule — not isolation: a program that ignores the rule is not stopped. Isolation comes with cloud containers.

## Setups made before

A setup saved before setups took values from environments may show **Its own variables** under **Values from**. It keeps working as it was; pick an environment to move it over.
