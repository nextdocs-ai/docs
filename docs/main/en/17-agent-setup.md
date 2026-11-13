# Setting up the agents

Nextdocs does not host the agents: each one is a command line tool that runs on your own computer, under your own account with its provider, and the app starts it in a folder you pick. So every agent is installed and signed into once, by you. This page is what that takes, per agent and per system.

In the desktop app the same page lives at **Set up the agents** — from the Claude Code page, from the agents board, or Settings → Agents → Claude Code. There it also shows what is already installed on the computer you are at, and can run the install commands for you.

## Which to pick

Any of them, and more than one: the agent is chosen per conversation. Claude Code is the only one with a plan to approve before it edits anything, per-command permission rules and a cost per turn — the others report less and are steered more coarsely. If you have a subscription to one of these already, start there; if you have none, Qwen’s free tier needs no card.

## Claude Code

Anthropic’s agent, and the one everything else here is measured against: the only one with a plan to approve, per-command permission rules and a cost per turn.

<Tabs>
<TabItem label="macOS" value="macos">

<Steps>
<Step title="Install it">

```bash
curl -fsSL https://claude.ai/install.sh | bash
```

Other ways:

* Homebrew — `brew install --cask claude-code`
* npm — `npm install -g @anthropic-ai/claude-code`

</Step>
<Step title="Sign in">

Opens a browser; a Claude subscription or an API account both work.

```bash
claude login
```

</Step>
<Step title="Or an API key instead">

In the desktop app: Settings → Secrets → Model keys, as **Anthropic** (`ANTHROPIC_API_KEY`). A key is pay-as-you-go where a sign-in is a subscription, and it is the only way in for a provider that sells no subscription. With both, the key wins and the runs are billed to it.

</Step>
<Step title="Check it">

Run `claude --version`. In the desktop app, **Check again** on the setup page turns the agent’s mark green once it can start it.

</Step>
</Steps>

</TabItem>
<TabItem label="Linux" value="linux">

<Steps>
<Step title="Install it">

```bash
curl -fsSL https://claude.ai/install.sh | bash
```

Other ways:

* npm — `npm install -g @anthropic-ai/claude-code`

</Step>
<Step title="Sign in">

Opens a browser; a Claude subscription or an API account both work.

```bash
claude login
```

</Step>
<Step title="Or an API key instead">

In the desktop app: Settings → Secrets → Model keys, as **Anthropic** (`ANTHROPIC_API_KEY`). A key is pay-as-you-go where a sign-in is a subscription, and it is the only way in for a provider that sells no subscription. With both, the key wins and the runs are billed to it.

</Step>
<Step title="Check it">

Run `claude --version`. In the desktop app, **Check again** on the setup page turns the agent’s mark green once it can start it.

</Step>
</Steps>

</TabItem>
<TabItem label="Windows" value="windows">

<Steps>
<Step title="Install it">

```bash
irm https://claude.ai/install.ps1 | iex
```

Other ways:

* winget — `winget install Anthropic.ClaudeCode`
* npm — `npm install -g @anthropic-ai/claude-code`

</Step>
<Step title="Sign in">

Opens a browser; a Claude subscription or an API account both work.

```bash
claude login
```

</Step>
<Step title="Or an API key instead">

In the desktop app: Settings → Secrets → Model keys, as **Anthropic** (`ANTHROPIC_API_KEY`). A key is pay-as-you-go where a sign-in is a subscription, and it is the only way in for a provider that sells no subscription. With both, the key wins and the runs are billed to it.

</Step>
<Step title="Check it">

Run `claude --version`. In the desktop app, **Check again** on the setup page turns the agent’s mark green once it can start it.

</Step>
</Steps>

</TabItem>
</Tabs>

:::note

**Worth knowing.** macOS keeps this sign-in in the keychain, so the app cannot see it from outside: a card that says it could not check the sign-in is not saying you are signed out.

:::

[Its own documentation](https://code.claude.com/docs/en/setup)

## Codex

OpenAI’s agent, on a ChatGPT plan or an API key. It has no plan mode and no per-command rules — its sandbox is the whole of its permissions.

<Tabs>
<TabItem label="macOS" value="macos">

<Steps>
<Step title="Install it">

```bash
curl -fsSL https://chatgpt.com/codex/install.sh | sh
```

Other ways:

* Homebrew — `brew install --cask codex`
* npm — `npm install -g @openai/codex`

</Step>
<Step title="Sign in">

Opens a browser for a ChatGPT account.

```bash
codex login
```

</Step>
<Step title="Or an API key instead">

In the desktop app: Settings → Secrets → Model keys, as **OpenAI** (`OPENAI_API_KEY`). A key is pay-as-you-go where a sign-in is a subscription, and it is the only way in for a provider that sells no subscription. With both, the key wins and the runs are billed to it.

</Step>
<Step title="Check it">

Run `codex --version`. In the desktop app, **Check again** on the setup page turns the agent’s mark green once it can start it.

</Step>
</Steps>

</TabItem>
<TabItem label="Linux" value="linux">

<Steps>
<Step title="Install it">

```bash
curl -fsSL https://chatgpt.com/codex/install.sh | sh
```

Other ways:

* npm — `npm install -g @openai/codex`

</Step>
<Step title="Sign in">

Opens a browser for a ChatGPT account.

```bash
codex login
```

</Step>
<Step title="Or an API key instead">

In the desktop app: Settings → Secrets → Model keys, as **OpenAI** (`OPENAI_API_KEY`). A key is pay-as-you-go where a sign-in is a subscription, and it is the only way in for a provider that sells no subscription. With both, the key wins and the runs are billed to it.

</Step>
<Step title="Check it">

Run `codex --version`. In the desktop app, **Check again** on the setup page turns the agent’s mark green once it can start it.

</Step>
</Steps>

</TabItem>
<TabItem label="Windows" value="windows">

<Steps>
<Step title="Install it">

```bash
powershell -ExecutionPolicy ByPass -c "irm https://chatgpt.com/codex/install.ps1 | iex"
```

Other ways:

* npm — `npm install -g @openai/codex`

</Step>
<Step title="Sign in">

Opens a browser for a ChatGPT account.

```bash
codex login
```

</Step>
<Step title="Or an API key instead">

In the desktop app: Settings → Secrets → Model keys, as **OpenAI** (`OPENAI_API_KEY`). A key is pay-as-you-go where a sign-in is a subscription, and it is the only way in for a provider that sells no subscription. With both, the key wins and the runs are billed to it.

</Step>
<Step title="Check it">

Run `codex --version`. In the desktop app, **Check again** on the setup page turns the agent’s mark green once it can start it.

</Step>
</Steps>

</TabItem>
</Tabs>

[Its own documentation](https://developers.openai.com/codex/cli)

## Gemini CLI

Google’s agent on a Google AI Studio key.

<Tabs>
<TabItem label="macOS" value="macos">

<Steps>
<Step title="Install it">

```bash
npm install -g @google/gemini-cli
```

Other ways:

* Homebrew — `brew install gemini-cli`

</Step>
<Step title="Or an API key instead">

In the desktop app: Settings → Secrets → Model keys, as **Google AI Studio** (`GEMINI_API_KEY`). A key is pay-as-you-go where a sign-in is a subscription, and it is the only way in for a provider that sells no subscription. With both, the key wins and the runs are billed to it.

</Step>
<Step title="Check it">

Run `gemini --version`. In the desktop app, **Check again** on the setup page turns the agent’s mark green once it can start it.

</Step>
</Steps>

</TabItem>
<TabItem label="Linux" value="linux">

<Steps>
<Step title="Install it">

```bash
npm install -g @google/gemini-cli
```

Needs Node.js: `curl -fsSL https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.1/install.sh | bash && nvm install 22`

</Step>
<Step title="Or an API key instead">

In the desktop app: Settings → Secrets → Model keys, as **Google AI Studio** (`GEMINI_API_KEY`). A key is pay-as-you-go where a sign-in is a subscription, and it is the only way in for a provider that sells no subscription. With both, the key wins and the runs are billed to it.

</Step>
<Step title="Check it">

Run `gemini --version`. In the desktop app, **Check again** on the setup page turns the agent’s mark green once it can start it.

</Step>
</Steps>

</TabItem>
<TabItem label="Windows" value="windows">

<Steps>
<Step title="Install it">

```bash
npm install -g @google/gemini-cli
```

Needs Node.js: `winget install OpenJS.NodeJS.LTS`

</Step>
<Step title="Or an API key instead">

In the desktop app: Settings → Secrets → Model keys, as **Google AI Studio** (`GEMINI_API_KEY`). A key is pay-as-you-go where a sign-in is a subscription, and it is the only way in for a provider that sells no subscription. With both, the key wins and the runs are billed to it.

</Step>
<Step title="Check it">

Run `gemini --version`. In the desktop app, **Check again** on the setup page turns the agent’s mark green once it can start it.

</Step>
</Steps>

</TabItem>
</Tabs>

:::note

**Worth knowing.** A key, not a sign-in: Gemini Code Assist stopped serving this CLI to individual Google accounts and points them at Antigravity instead. If you are here for a subscription rather than a key, Antigravity is the one to pick.

:::

[Its own documentation](https://github.com/google-gemini/gemini-cli)

## Antigravity

Google’s own CLI, under the Google sign-in you already have — what is left of Gemini by subscription. The same sign-in also serves Claude and GPT-OSS models.

<Tabs>
<TabItem label="macOS" value="macos">

<Steps>
<Step title="Install it">

Download the app: https://antigravity.google

</Step>
<Step title="Sign in">

Sign in inside the Antigravity app; the CLI then finds the session under ~/.gemini/antigravity-cli.

```bash
agy
```

</Step>
<Step title="Check it">

Run `agy --version`. In the desktop app, **Check again** on the setup page turns the agent’s mark green once it can start it.

</Step>
</Steps>

</TabItem>
<TabItem label="Linux" value="linux">

<Steps>
<Step title="Install it">

Download the app: https://antigravity.google

</Step>
<Step title="Sign in">

Sign in inside the Antigravity app; the CLI then finds the session under ~/.gemini/antigravity-cli.

```bash
agy
```

</Step>
<Step title="Check it">

Run `agy --version`. In the desktop app, **Check again** on the setup page turns the agent’s mark green once it can start it.

</Step>
</Steps>

</TabItem>
<TabItem label="Windows" value="windows">

<Steps>
<Step title="Install it">

Download the app: https://antigravity.google

</Step>
<Step title="Sign in">

Sign in inside the Antigravity app; the CLI then finds the session under ~/.gemini/antigravity-cli.

```bash
agy
```

</Step>
<Step title="Check it">

Run `agy --version`. In the desktop app, **Check again** on the setup page turns the agent’s mark green once it can start it.

</Step>
</Steps>

</TabItem>
</Tabs>

:::note

**Worth knowing.** The only one here with no package manager: agy arrives with the Antigravity app, so there is nothing to install from a terminal.

:::

[Its own documentation](https://antigravity.google)

## Qwen

The Qwen Code CLI on a Qwen account of your own — the free tier needs no key and no card.

<Tabs>
<TabItem label="macOS" value="macos">

<Steps>
<Step title="Install it">

```bash
npm install -g @qwen-code/qwen-code@latest
```

Other ways:

* Homebrew — `brew install qwen-code`

</Step>
<Step title="Sign in">

Then /auth inside it, and pick the Qwen account. The sign-in lands in ~/.qwen/oauth_creds.json, which is the file this page checks for.

```bash
qwen
```

</Step>
<Step title="Check it">

Run `qwen --version`. In the desktop app, **Check again** on the setup page turns the agent’s mark green once it can start it.

</Step>
</Steps>

</TabItem>
<TabItem label="Linux" value="linux">

<Steps>
<Step title="Install it">

```bash
npm install -g @qwen-code/qwen-code@latest
```

Needs Node.js 22 or newer: `curl -fsSL https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.1/install.sh | bash && nvm install 22`

</Step>
<Step title="Sign in">

Then /auth inside it, and pick the Qwen account. The sign-in lands in ~/.qwen/oauth_creds.json, which is the file this page checks for.

```bash
qwen
```

</Step>
<Step title="Check it">

Run `qwen --version`. In the desktop app, **Check again** on the setup page turns the agent’s mark green once it can start it.

</Step>
</Steps>

</TabItem>
<TabItem label="Windows" value="windows">

<Steps>
<Step title="Install it">

```bash
npm install -g @qwen-code/qwen-code@latest
```

Needs Node.js 22 or newer: `winget install OpenJS.NodeJS.LTS`

</Step>
<Step title="Sign in">

Then /auth inside it, and pick the Qwen account. The sign-in lands in ~/.qwen/oauth_creds.json, which is the file this page checks for.

```bash
qwen
```

</Step>
<Step title="Check it">

Run `qwen --version`. In the desktop app, **Check again** on the setup page turns the agent’s mark green once it can start it.

</Step>
</Steps>

</TabItem>
</Tabs>

:::note

**Worth knowing.** Needs Node.js 22 or newer — the one place here where 20 is not enough.

:::

[Its own documentation](https://github.com/QwenLM/qwen-code)

## Grok

xAI’s own agent, on an xAI sign-in or an API key. It prints what Claude Code prints and takes Claude Code’s permission rules, so along with Claude Code it is one of the two here with a plan to approve, per-command rules and a cost per turn.

<Tabs>
<TabItem label="macOS" value="macos">

<Steps>
<Step title="Install it">

```bash
curl -fsSL https://x.ai/cli/install.sh | bash
```

Other ways:

* npm — `npm install -g @xai-official/grok`

</Step>
<Step title="Sign in">

Opens a browser for your xAI account; the session lands in ~/.grok/auth.json.

```bash
grok login
```

</Step>
<Step title="Or an API key instead">

In the desktop app: Settings → Secrets → Model keys, as **xAI** (`XAI_API_KEY`). A key is pay-as-you-go where a sign-in is a subscription, and it is the only way in for a provider that sells no subscription. With both, the key wins and the runs are billed to it.

</Step>
<Step title="Check it">

Run `grok --version`. In the desktop app, **Check again** on the setup page turns the agent’s mark green once it can start it.

</Step>
</Steps>

</TabItem>
<TabItem label="Linux" value="linux">

<Steps>
<Step title="Install it">

```bash
curl -fsSL https://x.ai/cli/install.sh | bash
```

Other ways:

* npm — `npm install -g @xai-official/grok`

</Step>
<Step title="Sign in">

Opens a browser for your xAI account; the session lands in ~/.grok/auth.json.

```bash
grok login
```

</Step>
<Step title="Or an API key instead">

In the desktop app: Settings → Secrets → Model keys, as **xAI** (`XAI_API_KEY`). A key is pay-as-you-go where a sign-in is a subscription, and it is the only way in for a provider that sells no subscription. With both, the key wins and the runs are billed to it.

</Step>
<Step title="Check it">

Run `grok --version`. In the desktop app, **Check again** on the setup page turns the agent’s mark green once it can start it.

</Step>
</Steps>

</TabItem>
<TabItem label="Windows" value="windows">

<Steps>
<Step title="Install it">

```bash
irm https://x.ai/cli/install.ps1 | iex
```

Other ways:

* npm — `npm install -g @xai-official/grok`

</Step>
<Step title="Sign in">

Opens a browser for your xAI account; the session lands in ~/.grok/auth.json.

```bash
grok login
```

</Step>
<Step title="Or an API key instead">

In the desktop app: Settings → Secrets → Model keys, as **xAI** (`XAI_API_KEY`). A key is pay-as-you-go where a sign-in is a subscription, and it is the only way in for a provider that sells no subscription. With both, the key wins and the runs are billed to it.

</Step>
<Step title="Check it">

Run `grok --version`. In the desktop app, **Check again** on the setup page turns the agent’s mark green once it can start it.

</Step>
</Steps>

</TabItem>
</Tabs>

:::note

**Worth knowing.** Its own installer puts it in ~/.grok/bin before it is on any PATH, which is where Nextdocs looks for it too — so it is found even when your shell cannot run it yet. There is also a community “grok-cli” on npm that is not this: the official package is @xai-official/grok.

:::

[Its own documentation](https://x.ai/build)

## A model of your own

Anything that serves an OpenAI-compatible API — Ollama, vLLM or LM Studio on this machine, or a provider like DeepSeek or OpenRouter. One server is set at a time, and it is the same one the Qwen card can fall back to.

<Tabs>
<TabItem label="macOS" value="macos">

<Steps>
<Step title="Install it">

```bash
brew install ollama
```

</Step>
<Step title="Point the model server at it">

In the desktop app: Settings → Agents → Model server — address `http://localhost:11434/v1`, model `qwen3-coder:30b`, key from nothing — a local server wants no key. One server is set at a time, so the agents on this page that use one take turns.

</Step>
<Step title="Check it">

Run `codex --version`. In the desktop app, **Check again** on the setup page turns the agent’s mark green once it can start it.

</Step>
</Steps>

</TabItem>
<TabItem label="Linux" value="linux">

<Steps>
<Step title="Install it">

```bash
curl -fsSL https://ollama.com/install.sh | sh
```

</Step>
<Step title="Point the model server at it">

In the desktop app: Settings → Agents → Model server — address `http://localhost:11434/v1`, model `qwen3-coder:30b`, key from nothing — a local server wants no key. One server is set at a time, so the agents on this page that use one take turns.

</Step>
<Step title="Check it">

Run `codex --version`. In the desktop app, **Check again** on the setup page turns the agent’s mark green once it can start it.

</Step>
</Steps>

</TabItem>
<TabItem label="Windows" value="windows">

<Steps>
<Step title="Install it">

```bash
winget install Ollama.Ollama
```

</Step>
<Step title="Point the model server at it">

In the desktop app: Settings → Agents → Model server — address `http://localhost:11434/v1`, model `qwen3-coder:30b`, key from nothing — a local server wants no key. One server is set at a time, so the agents on this page that use one take turns.

</Step>
<Step title="Check it">

Run `codex --version`. In the desktop app, **Check again** on the setup page turns the agent’s mark green once it can start it.

</Step>
</Steps>

</TabItem>
</Tabs>

:::note

**Worth knowing.** Two backends drive the same server and the choice matters: “Local model” uses the Codex CLI, which speaks only the Responses API and hands over tools the way OpenAI’s own models expect them — good for gpt-oss, and measurably useless for everything else, which calls no tool at all. “Qwen Code” uses chat completions and suits the rest.

:::

[Its own documentation](https://docs.ollama.com)

## If the app cannot find something you installed

An app opened from the Dock or the Start menu does not inherit the PATH your terminal has — it gets the one the system gives to applications, which usually has none of these tools. Nextdocs reads your login shell’s PATH to get around that, so anything your terminal can run it can run too. A tool installed somewhere your shell does not know about is the case that stays invisible: add it to your PATH and check again.
