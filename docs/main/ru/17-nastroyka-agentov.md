# Настройка агентов

Nextdocs не держит агентов у себя: каждый из них — консольная программа, которая работает на вашем компьютере под вашей же учётной записью у провайдера, а приложение запускает её в выбранной вами папке. Поэтому каждого агента нужно один раз поставить и один раз в него войти. На этой странице — что именно для этого нужно, по агентам и по системам.

В десктопном приложении эта же страница открывается как **Set up the agents** — со страницы Claude Code, с доски агентов или из Settings → Agents → Claude Code. Там она ещё и показывает, что уже стоит на этом компьютере, и умеет выполнить команды установки за вас.

## Кого выбрать

Любого, и не одного: агент выбирается для каждого разговора отдельно. Только у Claude Code есть план, который вы утверждаете до первой правки, правила разрешений для отдельных команд и стоимость хода — остальные рассказывают о себе меньше и управляются грубее. Если у вас уже есть подписка на кого-то из них, начните с него; если подписки нет ни одной — у Qwen есть бесплатный уровень, для которого не нужна карта.

## Claude Code

Агент Anthropic и мерило для всех остальных здесь: единственный, у кого есть план на утверждение, правила разрешений для отдельных команд и стоимость хода.

<Tabs>
<TabItem label="macOS" value="macos">

<Steps>
<Step title="Установка">

```bash
curl -fsSL https://claude.ai/install.sh | bash
```

Другие способы:

* Homebrew — `brew install --cask claude-code`
* npm — `npm install -g @anthropic-ai/claude-code`

</Step>
<Step title="Вход">

Откроется браузер; подойдёт и подписка Claude, и аккаунт с API.

```bash
claude login
```

</Step>
<Step title="Или ключ API вместо входа">

В десктопном приложении: Settings → Secrets → Model keys, как **Anthropic** (`ANTHROPIC_API_KEY`). Ключ — это оплата по факту там, где вход — подписка, и для провайдера, который подписок не продаёт, это единственный путь. Если есть и то и другое, побеждает ключ, и расход идёт по нему.

</Step>
<Step title="Проверка">

Выполните `claude --version`. В десктопном приложении кнопка **Check again** на странице настройки сделает отметку агента зелёной, как только он сможет запуститься.

</Step>
</Steps>

</TabItem>
<TabItem label="Linux" value="linux">

<Steps>
<Step title="Установка">

```bash
curl -fsSL https://claude.ai/install.sh | bash
```

Другие способы:

* npm — `npm install -g @anthropic-ai/claude-code`

</Step>
<Step title="Вход">

Откроется браузер; подойдёт и подписка Claude, и аккаунт с API.

```bash
claude login
```

</Step>
<Step title="Или ключ API вместо входа">

В десктопном приложении: Settings → Secrets → Model keys, как **Anthropic** (`ANTHROPIC_API_KEY`). Ключ — это оплата по факту там, где вход — подписка, и для провайдера, который подписок не продаёт, это единственный путь. Если есть и то и другое, побеждает ключ, и расход идёт по нему.

</Step>
<Step title="Проверка">

Выполните `claude --version`. В десктопном приложении кнопка **Check again** на странице настройки сделает отметку агента зелёной, как только он сможет запуститься.

</Step>
</Steps>

</TabItem>
<TabItem label="Windows" value="windows">

<Steps>
<Step title="Установка">

```bash
irm https://claude.ai/install.ps1 | iex
```

Другие способы:

* winget — `winget install Anthropic.ClaudeCode`
* npm — `npm install -g @anthropic-ai/claude-code`

</Step>
<Step title="Вход">

Откроется браузер; подойдёт и подписка Claude, и аккаунт с API.

```bash
claude login
```

</Step>
<Step title="Или ключ API вместо входа">

В десктопном приложении: Settings → Secrets → Model keys, как **Anthropic** (`ANTHROPIC_API_KEY`). Ключ — это оплата по факту там, где вход — подписка, и для провайдера, который подписок не продаёт, это единственный путь. Если есть и то и другое, побеждает ключ, и расход идёт по нему.

</Step>
<Step title="Проверка">

Выполните `claude --version`. В десктопном приложении кнопка **Check again** на странице настройки сделает отметку агента зелёной, как только он сможет запуститься.

</Step>
</Steps>

</TabItem>
</Tabs>

:::note

**Что стоит знать.** macOS хранит этот вход в связке ключей, и снаружи приложение его не видит: отметка «не удалось проверить вход» не означает, что вы не вошли.

:::

[Его собственная документация](https://code.claude.com/docs/en/setup)

## Codex

Агент OpenAI — по тарифу ChatGPT или по ключу API. Плана на утверждение нет, правил для отдельных команд тоже: его песочница и есть все его разрешения.

<Tabs>
<TabItem label="macOS" value="macos">

<Steps>
<Step title="Установка">

```bash
curl -fsSL https://chatgpt.com/codex/install.sh | sh
```

Другие способы:

* Homebrew — `brew install --cask codex`
* npm — `npm install -g @openai/codex`

</Step>
<Step title="Вход">

Откроется браузер для аккаунта ChatGPT.

```bash
codex login
```

</Step>
<Step title="Или ключ API вместо входа">

В десктопном приложении: Settings → Secrets → Model keys, как **OpenAI** (`OPENAI_API_KEY`). Ключ — это оплата по факту там, где вход — подписка, и для провайдера, который подписок не продаёт, это единственный путь. Если есть и то и другое, побеждает ключ, и расход идёт по нему.

</Step>
<Step title="Проверка">

Выполните `codex --version`. В десктопном приложении кнопка **Check again** на странице настройки сделает отметку агента зелёной, как только он сможет запуститься.

</Step>
</Steps>

</TabItem>
<TabItem label="Linux" value="linux">

<Steps>
<Step title="Установка">

```bash
curl -fsSL https://chatgpt.com/codex/install.sh | sh
```

Другие способы:

* npm — `npm install -g @openai/codex`

</Step>
<Step title="Вход">

Откроется браузер для аккаунта ChatGPT.

```bash
codex login
```

</Step>
<Step title="Или ключ API вместо входа">

В десктопном приложении: Settings → Secrets → Model keys, как **OpenAI** (`OPENAI_API_KEY`). Ключ — это оплата по факту там, где вход — подписка, и для провайдера, который подписок не продаёт, это единственный путь. Если есть и то и другое, побеждает ключ, и расход идёт по нему.

</Step>
<Step title="Проверка">

Выполните `codex --version`. В десктопном приложении кнопка **Check again** на странице настройки сделает отметку агента зелёной, как только он сможет запуститься.

</Step>
</Steps>

</TabItem>
<TabItem label="Windows" value="windows">

<Steps>
<Step title="Установка">

```bash
powershell -ExecutionPolicy ByPass -c "irm https://chatgpt.com/codex/install.ps1 | iex"
```

Другие способы:

* npm — `npm install -g @openai/codex`

</Step>
<Step title="Вход">

Откроется браузер для аккаунта ChatGPT.

```bash
codex login
```

</Step>
<Step title="Или ключ API вместо входа">

В десктопном приложении: Settings → Secrets → Model keys, как **OpenAI** (`OPENAI_API_KEY`). Ключ — это оплата по факту там, где вход — подписка, и для провайдера, который подписок не продаёт, это единственный путь. Если есть и то и другое, побеждает ключ, и расход идёт по нему.

</Step>
<Step title="Проверка">

Выполните `codex --version`. В десктопном приложении кнопка **Check again** на странице настройки сделает отметку агента зелёной, как только он сможет запуститься.

</Step>
</Steps>

</TabItem>
</Tabs>

[Его собственная документация](https://developers.openai.com/codex/cli)

## Gemini CLI

Агент Google по ключу Google AI Studio.

<Tabs>
<TabItem label="macOS" value="macos">

<Steps>
<Step title="Установка">

```bash
npm install -g @google/gemini-cli
```

Другие способы:

* Homebrew — `brew install gemini-cli`

</Step>
<Step title="Или ключ API вместо входа">

В десктопном приложении: Settings → Secrets → Model keys, как **Google AI Studio** (`GEMINI_API_KEY`). Ключ — это оплата по факту там, где вход — подписка, и для провайдера, который подписок не продаёт, это единственный путь. Если есть и то и другое, побеждает ключ, и расход идёт по нему.

</Step>
<Step title="Проверка">

Выполните `gemini --version`. В десктопном приложении кнопка **Check again** на странице настройки сделает отметку агента зелёной, как только он сможет запуститься.

</Step>
</Steps>

</TabItem>
<TabItem label="Linux" value="linux">

<Steps>
<Step title="Установка">

```bash
npm install -g @google/gemini-cli
```

Нужен Node.js: `curl -fsSL https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.1/install.sh | bash && nvm install 22`

</Step>
<Step title="Или ключ API вместо входа">

В десктопном приложении: Settings → Secrets → Model keys, как **Google AI Studio** (`GEMINI_API_KEY`). Ключ — это оплата по факту там, где вход — подписка, и для провайдера, который подписок не продаёт, это единственный путь. Если есть и то и другое, побеждает ключ, и расход идёт по нему.

</Step>
<Step title="Проверка">

Выполните `gemini --version`. В десктопном приложении кнопка **Check again** на странице настройки сделает отметку агента зелёной, как только он сможет запуститься.

</Step>
</Steps>

</TabItem>
<TabItem label="Windows" value="windows">

<Steps>
<Step title="Установка">

```bash
npm install -g @google/gemini-cli
```

Нужен Node.js: `winget install OpenJS.NodeJS.LTS`

</Step>
<Step title="Или ключ API вместо входа">

В десктопном приложении: Settings → Secrets → Model keys, как **Google AI Studio** (`GEMINI_API_KEY`). Ключ — это оплата по факту там, где вход — подписка, и для провайдера, который подписок не продаёт, это единственный путь. Если есть и то и другое, побеждает ключ, и расход идёт по нему.

</Step>
<Step title="Проверка">

Выполните `gemini --version`. В десктопном приложении кнопка **Check again** на странице настройки сделает отметку агента зелёной, как только он сможет запуститься.

</Step>
</Steps>

</TabItem>
</Tabs>

:::note

**Что стоит знать.** Именно ключ, а не вход: Gemini Code Assist перестал обслуживать этот CLI для личных аккаунтов Google и отправляет их в Antigravity. Если вам нужна подписка, а не ключ — выбирайте Antigravity.

:::

[Его собственная документация](https://github.com/google-gemini/gemini-cli)

## Antigravity

Собственный CLI Google под тем же аккаунтом Google, что у вас уже есть, — то, что осталось от Gemini по подписке. Тот же вход даёт и модели Claude, и GPT-OSS.

<Tabs>
<TabItem label="macOS" value="macos">

<Steps>
<Step title="Установка">

Скачайте приложение: https://antigravity.google

</Step>
<Step title="Вход">

Вход делается внутри приложения Antigravity; CLI затем находит сессию в ~/.gemini/antigravity-cli.

```bash
agy
```

</Step>
<Step title="Проверка">

Выполните `agy --version`. В десктопном приложении кнопка **Check again** на странице настройки сделает отметку агента зелёной, как только он сможет запуститься.

</Step>
</Steps>

</TabItem>
<TabItem label="Linux" value="linux">

<Steps>
<Step title="Установка">

Скачайте приложение: https://antigravity.google

</Step>
<Step title="Вход">

Вход делается внутри приложения Antigravity; CLI затем находит сессию в ~/.gemini/antigravity-cli.

```bash
agy
```

</Step>
<Step title="Проверка">

Выполните `agy --version`. В десктопном приложении кнопка **Check again** на странице настройки сделает отметку агента зелёной, как только он сможет запуститься.

</Step>
</Steps>

</TabItem>
<TabItem label="Windows" value="windows">

<Steps>
<Step title="Установка">

Скачайте приложение: https://antigravity.google

</Step>
<Step title="Вход">

Вход делается внутри приложения Antigravity; CLI затем находит сессию в ~/.gemini/antigravity-cli.

```bash
agy
```

</Step>
<Step title="Проверка">

Выполните `agy --version`. В десктопном приложении кнопка **Check again** на странице настройки сделает отметку агента зелёной, как только он сможет запуститься.

</Step>
</Steps>

</TabItem>
</Tabs>

:::note

**Что стоит знать.** Единственный здесь без пакетного менеджера: `agy` приезжает вместе с приложением Antigravity, ставить из терминала нечего.

:::

[Его собственная документация](https://antigravity.google)

## Qwen

CLI Qwen Code под вашим аккаунтом Qwen — на бесплатном уровне не нужны ни ключ, ни карта.

<Tabs>
<TabItem label="macOS" value="macos">

<Steps>
<Step title="Установка">

```bash
npm install -g @qwen-code/qwen-code@latest
```

Другие способы:

* Homebrew — `brew install qwen-code`

</Step>
<Step title="Вход">

Затем `/auth` внутри и выберите аккаунт Qwen. Вход попадёт в ~/.qwen/oauth_creds.json — именно этот файл проверяет приложение.

```bash
qwen
```

</Step>
<Step title="Проверка">

Выполните `qwen --version`. В десктопном приложении кнопка **Check again** на странице настройки сделает отметку агента зелёной, как только он сможет запуститься.

</Step>
</Steps>

</TabItem>
<TabItem label="Linux" value="linux">

<Steps>
<Step title="Установка">

```bash
npm install -g @qwen-code/qwen-code@latest
```

Нужен Node.js 22 или новее: `curl -fsSL https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.1/install.sh | bash && nvm install 22`

</Step>
<Step title="Вход">

Затем `/auth` внутри и выберите аккаунт Qwen. Вход попадёт в ~/.qwen/oauth_creds.json — именно этот файл проверяет приложение.

```bash
qwen
```

</Step>
<Step title="Проверка">

Выполните `qwen --version`. В десктопном приложении кнопка **Check again** на странице настройки сделает отметку агента зелёной, как только он сможет запуститься.

</Step>
</Steps>

</TabItem>
<TabItem label="Windows" value="windows">

<Steps>
<Step title="Установка">

```bash
npm install -g @qwen-code/qwen-code@latest
```

Нужен Node.js 22 или новее: `winget install OpenJS.NodeJS.LTS`

</Step>
<Step title="Вход">

Затем `/auth` внутри и выберите аккаунт Qwen. Вход попадёт в ~/.qwen/oauth_creds.json — именно этот файл проверяет приложение.

```bash
qwen
```

</Step>
<Step title="Проверка">

Выполните `qwen --version`. В десктопном приложении кнопка **Check again** на странице настройки сделает отметку агента зелёной, как только он сможет запуститься.

</Step>
</Steps>

</TabItem>
</Tabs>

:::note

**Что стоит знать.** Нужен Node.js 22 или новее — единственное место здесь, где версии 20 не хватит.

:::

[Его собственная документация](https://github.com/QwenLM/qwen-code)

## Grok

Собственный агент xAI — по входу в аккаунт xAI или по ключу API. Он печатает то же, что печатает Claude Code, и принимает его правила разрешений, так что вместе с Claude Code это один из двух здесь, у кого есть план на утверждение, правила для отдельных команд и стоимость хода.

<Tabs>
<TabItem label="macOS" value="macos">

<Steps>
<Step title="Установка">

```bash
curl -fsSL https://x.ai/cli/install.sh | bash
```

Другие способы:

* npm — `npm install -g @xai-official/grok`

</Step>
<Step title="Вход">

Opens a browser for your xAI account; the session lands in ~/.grok/auth.json.

```bash
grok login
```

</Step>
<Step title="Или ключ API вместо входа">

В десктопном приложении: Settings → Secrets → Model keys, как **xAI** (`XAI_API_KEY`). Ключ — это оплата по факту там, где вход — подписка, и для провайдера, который подписок не продаёт, это единственный путь. Если есть и то и другое, побеждает ключ, и расход идёт по нему.

</Step>
<Step title="Проверка">

Выполните `grok --version`. В десктопном приложении кнопка **Check again** на странице настройки сделает отметку агента зелёной, как только он сможет запуститься.

</Step>
</Steps>

</TabItem>
<TabItem label="Linux" value="linux">

<Steps>
<Step title="Установка">

```bash
curl -fsSL https://x.ai/cli/install.sh | bash
```

Другие способы:

* npm — `npm install -g @xai-official/grok`

</Step>
<Step title="Вход">

Opens a browser for your xAI account; the session lands in ~/.grok/auth.json.

```bash
grok login
```

</Step>
<Step title="Или ключ API вместо входа">

В десктопном приложении: Settings → Secrets → Model keys, как **xAI** (`XAI_API_KEY`). Ключ — это оплата по факту там, где вход — подписка, и для провайдера, который подписок не продаёт, это единственный путь. Если есть и то и другое, побеждает ключ, и расход идёт по нему.

</Step>
<Step title="Проверка">

Выполните `grok --version`. В десктопном приложении кнопка **Check again** на странице настройки сделает отметку агента зелёной, как только он сможет запуститься.

</Step>
</Steps>

</TabItem>
<TabItem label="Windows" value="windows">

<Steps>
<Step title="Установка">

```bash
irm https://x.ai/cli/install.ps1 | iex
```

Другие способы:

* npm — `npm install -g @xai-official/grok`

</Step>
<Step title="Вход">

Opens a browser for your xAI account; the session lands in ~/.grok/auth.json.

```bash
grok login
```

</Step>
<Step title="Или ключ API вместо входа">

В десктопном приложении: Settings → Secrets → Model keys, как **xAI** (`XAI_API_KEY`). Ключ — это оплата по факту там, где вход — подписка, и для провайдера, который подписок не продаёт, это единственный путь. Если есть и то и другое, побеждает ключ, и расход идёт по нему.

</Step>
<Step title="Проверка">

Выполните `grok --version`. В десктопном приложении кнопка **Check again** на странице настройки сделает отметку агента зелёной, как только он сможет запуститься.

</Step>
</Steps>

</TabItem>
</Tabs>

:::note

**Что стоит знать.** Свой установщик кладёт его в ~/.grok/bin ещё до того, как он появится в PATH, — туда же смотрит и Nextdocs, поэтому он находится даже тогда, когда ваш шелл запустить его ещё не может. На npm есть и сторонний «grok-cli» — это не он: официальный пакет называется @xai-official/grok.

:::

[Его собственная документация](https://x.ai/build)

## A model of your own

Всё, что отдаёт OpenAI-совместимый API, — Ollama, vLLM или LM Studio на этой машине, или провайдер вроде DeepSeek и OpenRouter. Сервер задаётся один, и это тот же сервер, на который при случае опирается карточка Qwen.

<Tabs>
<TabItem label="macOS" value="macos">

<Steps>
<Step title="Установка">

```bash
brew install ollama
```

</Step>
<Step title="Указать на него сервер моделей">

В десктопном приложении: Settings → Agents → Model server — адрес `http://localhost:11434/v1`, модель `qwen3-coder:30b`, ключ отсюда: nothing — a local server wants no key. Сервер задаётся один, поэтому агенты с этой страницы, которым он нужен, пользуются им по очереди.

</Step>
<Step title="Проверка">

Выполните `codex --version`. В десктопном приложении кнопка **Check again** на странице настройки сделает отметку агента зелёной, как только он сможет запуститься.

</Step>
</Steps>

</TabItem>
<TabItem label="Linux" value="linux">

<Steps>
<Step title="Установка">

```bash
curl -fsSL https://ollama.com/install.sh | sh
```

</Step>
<Step title="Указать на него сервер моделей">

В десктопном приложении: Settings → Agents → Model server — адрес `http://localhost:11434/v1`, модель `qwen3-coder:30b`, ключ отсюда: nothing — a local server wants no key. Сервер задаётся один, поэтому агенты с этой страницы, которым он нужен, пользуются им по очереди.

</Step>
<Step title="Проверка">

Выполните `codex --version`. В десктопном приложении кнопка **Check again** на странице настройки сделает отметку агента зелёной, как только он сможет запуститься.

</Step>
</Steps>

</TabItem>
<TabItem label="Windows" value="windows">

<Steps>
<Step title="Установка">

```bash
winget install Ollama.Ollama
```

</Step>
<Step title="Указать на него сервер моделей">

В десктопном приложении: Settings → Agents → Model server — адрес `http://localhost:11434/v1`, модель `qwen3-coder:30b`, ключ отсюда: nothing — a local server wants no key. Сервер задаётся один, поэтому агенты с этой страницы, которым он нужен, пользуются им по очереди.

</Step>
<Step title="Проверка">

Выполните `codex --version`. В десктопном приложении кнопка **Check again** на странице настройки сделает отметку агента зелёной, как только он сможет запуститься.

</Step>
</Steps>

</TabItem>
</Tabs>

:::note

**Что стоит знать.** Один и тот же сервер обслуживают два бэкенда, и выбор важен: «Local model» идёт через CLI Codex, который говорит только на Responses API и отдаёт инструменты так, как их ждут собственные модели OpenAI, — хорошо для gpt-oss и, по замерам, бесполезно для остальных, которые не вызывают ни одного инструмента. «Qwen Code» говорит на chat completions и подходит всем прочим.

:::

[Его собственная документация](https://docs.ollama.com)

## Если приложение не видит то, что вы поставили

Приложение, запущенное из Dock или из меню «Пуск», не наследует PATH вашего терминала — ему достаётся системный, в котором этих программ обычно нет. Nextdocs обходит это тем, что читает PATH вашего login-шелла, так что всё, что запускается в терминале, запустится и здесь. Невидимым остаётся только то, что установлено в папку, о которой ваш шелл не знает: добавьте её в PATH и проверьте снова.
