# Widget API reference

> Generated from the frontend code (`src/components/widgets`) for widget API **v1.1.0**. Do not edit by hand — run `pnpm generate:types` in nextdocs-front.

## How a widget works

A widget is a small TSX program. It reads data through **named sources** with `api.get(name, params)`, declares its options with `settings({...})`, and returns a tree of our components with `render(...)`. It runs in a Web Worker inside a sandboxed iframe with no network, no storage and no DOM of ours; the home screen draws what it returns with the app’s own components. A press on a row is an *intent* (where to go), opened by the app on your click.

## Data sources

### Core API

Tasks, notifications, projects, repositories, people, feed.

| Source | Params | Returns | |
|---|---|---|---|
| `tasks.list` | `{ status?: 'open' \| 'done' \| 'all'; mine?: boolean; /* Tasks assigned to this person. */ assignee?: UserRef; /* Tasks linked to this project. */ project?: ProjectRef; type?: 'any' \| 'task' \| 'bug' \| 'story' \| 'epic'; sort?: 'updated' \| 'created' \| 'priority'; /* 1..50, default 10 */ limit?: number }` | `WidgetTask[]` | Tasks of the organization by a filter. |
| `tasks.recent` | `{ /* 1..50, default 10 */ limit?: number }` | `WidgetTask[]` | The newest tasks. |
| `tasks.mine` | `{ /* 1..50, default 20 */ limit?: number }` | `WidgetTask[]` | Open tasks assigned to the person viewing. |
| `tasks.byStatus` | `{ mine?: boolean }` | `{ status: string; category: 'todo' \| 'in_progress' \| 'done'; count: number }[]` | How many tasks are in each status. |
| `tasks.trend` | `{ /* 1..30, default 14 */ days?: number }` | `{ labels: string[]; created: number[]; closed: number[] }` | Tasks created and closed per day, oldest day first. |
| `tasks.summary` | `{ /* 1..30, default 7 */ days?: number }` | `{ open: number; closed: number; closedPerDay: number[] }` | Open tasks now, and tasks closed per day over a period. |
| `notifications.recent` | `{ /* 1..30, default 10 */ limit?: number; unread?: boolean }` | `WidgetNotification[]` | The person's latest notifications. Open one with { open: 'notification', id }. |
| `notifications.unread` | `Record<string, never>` | `number` | How many notifications are unread. |
| `pages.recent` | `{ /* 1..20, default 8 */ limit?: number }` | `WidgetPage[]` | Pages the person visited last. Open one with { open: 'page', projectId, pageId }. |
| `projects.list` | `{ /* 1..100, default 20 */ limit?: number }` | `{ id: number; name: string }[]` | Projects (knowledge bases) the person can open. Open one with { open: 'project', id }. |
| `repositories.list` | `{ /* 1..100, default 20 */ limit?: number }` | `{ id: number; name: string; provider: string }[]` | Connected repositories. Open one with { open: 'repository', id }. |
| `members.list` | `{ /* 1..200, default 50 */ limit?: number }` | `{ name: string; handle: string }[]` | People of the organization: name and handle only — no e-mails, no ids. |
| `feed.recent` | `{ /* 1..30, default 10 */ limit?: number }` | `WidgetFeedItem[]` | The organization's news feed, newest first. |

### Comments service

Comment threads on tasks.

| Source | Params | Returns | |
|---|---|---|---|
| `comments.task` | `{ /* Task key, e.g. "ND-12" */ key: string }` | `WidgetComment[]` | Comments on one task, oldest first. Bodies are cut to 280 characters. |

### Chat service

Rooms and unread counts — never message text.

| Source | Params | Returns | |
|---|---|---|---|
| `chat.unread` | `Record<string, never>` | `{ rooms: number; messages: number }` | How many rooms and messages are unread. |
| `chat.rooms` | `{ /* 1..50, default 10 */ limit?: number }` | `{ id: string; name: string; lastMessageAt: string }[]` | Rooms of the organization the person is in. Open one with { open: 'room', id }. |

### RAG

Search over documentation and code.

| Source | Params | Returns | |
|---|---|---|---|
| `docs.search` | `{ /* 2..200 characters */ query: string; /* 1..20, default 5 */ limit?: number }` | `WidgetDocHit[]` | Search the documentation. Open a hit with { open: 'page', projectId, pageId }. |
| `code.search` | `{ /* 2..200 characters */ query: string; /* 1..20, default 5 */ limit?: number }` | `WidgetCodeHit[]` | Search the code of the organization's repositories. |

### Code graph

Documentation coverage of repositories.

| Source | Params | Returns | |
|---|---|---|---|
| `coverage.repository` | `{ repositoryId: number }` | `{ units: number; mentioned: number; documented: number; computedAt: string } \| null` | How much of a repository is documented. |

### Agents

Agent work and runners.

| Source | Params | Returns | |
|---|---|---|---|
| `agents.work` | `Record<string, never>` | `{ taskId: number; state: string; waiting: boolean; where: 'computer' \| 'runner'; label: string; updatedAt: string }[]` | Tasks agents are working on now. Open one with { open: 'task', key } using the key from tasks.* sources. |
| `agents.runners` | `Record<string, never>` | `{ label: string; online: boolean }[]` | Agent runners the person can see, and whether they are online. |

## Components

| Component | Props | |
|---|---|---|
| `<List>` | `{ children?: Child }` | A vertical stack. Also what <>…</> becomes. |
| `<Row>` | `{ onPress?: Intent; children?: Child }` | A horizontal line. With onPress it is a button that asks the host to open something. |
| `<Text>` | `{ muted?: boolean; mono?: boolean; children?: TextChild }` | Text. Never HTML. |
| `<Heading>` | `{ children?: TextChild }` | A small section title. |
| `<Chip>` | `{ tone?: Tone; children?: TextChild }` | A short label with a tone. |
| `<Stat>` | `{ label: string; value: string; tone?: Tone }` | A labelled number. |
| `<Grid>` | `{ columns?: 1 \| 2 \| 3 \| 4; children?: Child }` | Tiles in 1–4 columns. |
| `<Bar>` | `{ values: number[] }` | A minimal bar sparkline. |
| `<Chart>` | `{ kind?: 'bar' \| 'line'; labels?: string[]; series: ChartSeries[]; stacked?: boolean }` | Bar or line chart, up to 6 series. |
| `<Donut>` | `{ segments: { label: string; value: number; tone?: Tone }[] }` | Parts of a whole. |
| `<AgentChat>` (ours) | `Record<string, never>` | Ours: the widget places it and cannot configure it. |

## Opening things

`<Row onPress={…}>` takes an intent, never a URL: `{ open: 'task', key }`, `{ open: 'page', projectId, pageId }`, `{ open: 'project', id }`, `{ open: 'repository', id }`, `{ open: 'room', id }`, `{ open: 'notification', id }`, `{ open: 'section', name }` with name one of `tasks`, `feed`, `repositories`, `members`, `messages`.

## Limits

| | |
|---|---|
| Compiled code | 64 KB |
| First render within | 10 s |
| Data requests per run | 64, 8 at once |
| Tree | depth 8, 500 nodes |

## Interactive reference

Every source as an operation: what you pass, what you get. These are not HTTP endpoints — the app calls our API for the widget.

```openapi
{
  "openapi": "3.0.3",
  "info": {
    "title": "Nextdocs widget data sources",
    "version": "1.1.0",
    "description": "What a widget can read with api.get(name, params). Generated from src/components/widgets/models.ts."
  },
  "paths": {
    "/sources/tasks.list": {
      "post": {
        "operationId": "tasksList",
        "tags": [
          "core"
        ],
        "summary": "Tasks of the organization by a filter.",
        "description": "In widget code: `api.get('tasks.list', params)`. Not an HTTP endpoint — the host calls our API for the widget.",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "status": {
                    "type": "string",
                    "enum": [
                      "open",
                      "done",
                      "all"
                    ]
                  },
                  "mine": {
                    "type": "boolean"
                  },
                  "assignee": {
                    "type": "object",
                    "properties": {
                      "toString": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Returns a string representation of a string."
                      },
                      "charAt": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Returns the character at the specified index."
                      },
                      "charCodeAt": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Returns the Unicode value of the character at the specified location."
                      },
                      "concat": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Returns a string that contains the concatenation of two or more strings."
                      },
                      "indexOf": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Returns the position of the first occurrence of a substring."
                      },
                      "lastIndexOf": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Returns the last occurrence of a substring in the string."
                      },
                      "localeCompare": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Determines whether two strings are equivalent in the current locale.\nDetermines whether two strings are equivalent in the current or specified locale."
                      },
                      "match": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Matches a string with a regular expression, and returns an array containing the results of that search.\nMatches a string or an object that supports being matched against, and returns an array\ncontaining the results of that search, or null if no matches are found."
                      },
                      "replace": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Replaces text in a string, using a regular expression or search string.\nPasses a string and {@linkcode replaceValue} to the `[Symbol.replace]` method on {@linkcode searchValue}. This method is expected to implement its own replacement algorithm.\nReplaces text in a string, using an object that supports replacement within a string."
                      },
                      "search": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Finds the first substring match in a regular expression search."
                      },
                      "slice": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Returns a section of a string."
                      },
                      "split": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Split a string into substrings using the specified separator and return them as an array."
                      },
                      "substring": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Returns the substring at the specified location within a String object."
                      },
                      "toLowerCase": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Converts all the alphabetic characters in a string to lowercase."
                      },
                      "toLocaleLowerCase": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Converts all alphabetic characters to lowercase, taking into account the host environment's current locale."
                      },
                      "toUpperCase": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Converts all the alphabetic characters in a string to uppercase."
                      },
                      "toLocaleUpperCase": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Returns a string where all alphabetic characters have been converted to uppercase, taking into account the host environment's current locale."
                      },
                      "trim": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Removes the leading and trailing white space and line terminator characters from a string."
                      },
                      "length": {
                        "type": "number",
                        "description": "Returns the length of a String object."
                      },
                      "substr": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Gets a substring beginning at the specified location and having the specified length."
                      },
                      "valueOf": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Returns the primitive value of the specified object."
                      },
                      "codePointAt": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Returns a nonnegative integer Number less than 1114112 (0x110000) that is the code point\nvalue of the UTF-16 encoded code point starting at the string element at position pos in\nthe String resulting from converting this object to a String.\nIf there is no element at that position, the result is undefined.\nIf a valid UTF-16 surrogate pair does not begin at pos, the result is the code unit at pos."
                      },
                      "includes": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Returns true if searchString appears as a substring of the result of converting this\nobject to a String, at one or more positions that are\ngreater than or equal to position; otherwise, returns false."
                      },
                      "endsWith": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Returns true if the sequence of elements of searchString converted to a String is the\nsame as the corresponding elements of this object (converted to a String) starting at\nendPosition – length(this). Otherwise returns false."
                      },
                      "normalize": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Returns the String value result of normalizing the string into the normalization form\nnamed by form as specified in Unicode Standard Annex #15, Unicode Normalization Forms."
                      },
                      "repeat": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Returns a String value that is made from count copies appended together. If count is 0,\nthe empty string is returned."
                      },
                      "startsWith": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Returns true if the sequence of elements of searchString converted to a String is the\nsame as the corresponding elements of this object (converted to a String) starting at\nposition. Otherwise returns false."
                      },
                      "anchor": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Returns an `<a>` HTML anchor element and sets the name attribute to the text value"
                      },
                      "big": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Returns a `<big>` HTML element"
                      },
                      "blink": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Returns a `<blink>` HTML element"
                      },
                      "bold": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Returns a `<b>` HTML element"
                      },
                      "fixed": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Returns a `<tt>` HTML element"
                      },
                      "fontcolor": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Returns a `<font>` HTML element and sets the color attribute value"
                      },
                      "fontsize": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Returns a `<font>` HTML element and sets the size attribute value"
                      },
                      "italics": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Returns an `<i>` HTML element"
                      },
                      "link": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Returns an `<a>` HTML element and sets the href attribute value"
                      },
                      "small": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Returns a `<small>` HTML element"
                      },
                      "strike": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Returns a `<strike>` HTML element"
                      },
                      "sub": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Returns a `<sub>` HTML element"
                      },
                      "sup": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Returns a `<sup>` HTML element"
                      },
                      "padStart": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Pads the current string with a given string (possibly repeated) so that the resulting string reaches a given length.\nThe padding is applied from the start (left) of the current string."
                      },
                      "padEnd": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Pads the current string with a given string (possibly repeated) so that the resulting string reaches a given length.\nThe padding is applied from the end (right) of the current string."
                      },
                      "trimEnd": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Removes the trailing white space and line terminator characters from a string."
                      },
                      "trimStart": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Removes the leading white space and line terminator characters from a string."
                      },
                      "trimLeft": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Removes the leading white space and line terminator characters from a string."
                      },
                      "trimRight": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Removes the trailing white space and line terminator characters from a string."
                      },
                      "matchAll": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Matches a string with a regular expression, and returns an iterable of matches\ncontaining the results of that search."
                      },
                      "__@iterator@360": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Iterator"
                      },
                      "__entity": {
                        "type": "string",
                        "enum": [
                          "user"
                        ]
                      }
                    },
                    "required": [
                      "toString",
                      "charAt",
                      "charCodeAt",
                      "concat",
                      "indexOf",
                      "lastIndexOf",
                      "localeCompare",
                      "match",
                      "replace",
                      "search",
                      "slice",
                      "split",
                      "substring",
                      "toLowerCase",
                      "toLocaleLowerCase",
                      "toUpperCase",
                      "toLocaleUpperCase",
                      "trim",
                      "length",
                      "substr",
                      "valueOf",
                      "codePointAt",
                      "includes",
                      "endsWith",
                      "normalize",
                      "repeat",
                      "startsWith",
                      "anchor",
                      "big",
                      "blink",
                      "bold",
                      "fixed",
                      "fontcolor",
                      "fontsize",
                      "italics",
                      "link",
                      "small",
                      "strike",
                      "sub",
                      "sup",
                      "padStart",
                      "padEnd",
                      "trimEnd",
                      "trimStart",
                      "trimLeft",
                      "trimRight",
                      "matchAll",
                      "__@iterator@360",
                      "__entity"
                    ],
                    "additionalProperties": false
                  },
                  "project": {
                    "type": "object",
                    "properties": {
                      "toString": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Returns a string representation of a string."
                      },
                      "charAt": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Returns the character at the specified index."
                      },
                      "charCodeAt": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Returns the Unicode value of the character at the specified location."
                      },
                      "concat": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Returns a string that contains the concatenation of two or more strings."
                      },
                      "indexOf": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Returns the position of the first occurrence of a substring."
                      },
                      "lastIndexOf": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Returns the last occurrence of a substring in the string."
                      },
                      "localeCompare": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Determines whether two strings are equivalent in the current locale.\nDetermines whether two strings are equivalent in the current or specified locale."
                      },
                      "match": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Matches a string with a regular expression, and returns an array containing the results of that search.\nMatches a string or an object that supports being matched against, and returns an array\ncontaining the results of that search, or null if no matches are found."
                      },
                      "replace": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Replaces text in a string, using a regular expression or search string.\nPasses a string and {@linkcode replaceValue} to the `[Symbol.replace]` method on {@linkcode searchValue}. This method is expected to implement its own replacement algorithm.\nReplaces text in a string, using an object that supports replacement within a string."
                      },
                      "search": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Finds the first substring match in a regular expression search."
                      },
                      "slice": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Returns a section of a string."
                      },
                      "split": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Split a string into substrings using the specified separator and return them as an array."
                      },
                      "substring": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Returns the substring at the specified location within a String object."
                      },
                      "toLowerCase": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Converts all the alphabetic characters in a string to lowercase."
                      },
                      "toLocaleLowerCase": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Converts all alphabetic characters to lowercase, taking into account the host environment's current locale."
                      },
                      "toUpperCase": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Converts all the alphabetic characters in a string to uppercase."
                      },
                      "toLocaleUpperCase": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Returns a string where all alphabetic characters have been converted to uppercase, taking into account the host environment's current locale."
                      },
                      "trim": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Removes the leading and trailing white space and line terminator characters from a string."
                      },
                      "length": {
                        "type": "number",
                        "description": "Returns the length of a String object."
                      },
                      "substr": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Gets a substring beginning at the specified location and having the specified length."
                      },
                      "valueOf": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Returns the primitive value of the specified object."
                      },
                      "codePointAt": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Returns a nonnegative integer Number less than 1114112 (0x110000) that is the code point\nvalue of the UTF-16 encoded code point starting at the string element at position pos in\nthe String resulting from converting this object to a String.\nIf there is no element at that position, the result is undefined.\nIf a valid UTF-16 surrogate pair does not begin at pos, the result is the code unit at pos."
                      },
                      "includes": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Returns true if searchString appears as a substring of the result of converting this\nobject to a String, at one or more positions that are\ngreater than or equal to position; otherwise, returns false."
                      },
                      "endsWith": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Returns true if the sequence of elements of searchString converted to a String is the\nsame as the corresponding elements of this object (converted to a String) starting at\nendPosition – length(this). Otherwise returns false."
                      },
                      "normalize": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Returns the String value result of normalizing the string into the normalization form\nnamed by form as specified in Unicode Standard Annex #15, Unicode Normalization Forms."
                      },
                      "repeat": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Returns a String value that is made from count copies appended together. If count is 0,\nthe empty string is returned."
                      },
                      "startsWith": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Returns true if the sequence of elements of searchString converted to a String is the\nsame as the corresponding elements of this object (converted to a String) starting at\nposition. Otherwise returns false."
                      },
                      "anchor": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Returns an `<a>` HTML anchor element and sets the name attribute to the text value"
                      },
                      "big": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Returns a `<big>` HTML element"
                      },
                      "blink": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Returns a `<blink>` HTML element"
                      },
                      "bold": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Returns a `<b>` HTML element"
                      },
                      "fixed": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Returns a `<tt>` HTML element"
                      },
                      "fontcolor": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Returns a `<font>` HTML element and sets the color attribute value"
                      },
                      "fontsize": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Returns a `<font>` HTML element and sets the size attribute value"
                      },
                      "italics": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Returns an `<i>` HTML element"
                      },
                      "link": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Returns an `<a>` HTML element and sets the href attribute value"
                      },
                      "small": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Returns a `<small>` HTML element"
                      },
                      "strike": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Returns a `<strike>` HTML element"
                      },
                      "sub": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Returns a `<sub>` HTML element"
                      },
                      "sup": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Returns a `<sup>` HTML element"
                      },
                      "padStart": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Pads the current string with a given string (possibly repeated) so that the resulting string reaches a given length.\nThe padding is applied from the start (left) of the current string."
                      },
                      "padEnd": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Pads the current string with a given string (possibly repeated) so that the resulting string reaches a given length.\nThe padding is applied from the end (right) of the current string."
                      },
                      "trimEnd": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Removes the trailing white space and line terminator characters from a string."
                      },
                      "trimStart": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Removes the leading white space and line terminator characters from a string."
                      },
                      "trimLeft": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Removes the leading white space and line terminator characters from a string."
                      },
                      "trimRight": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Removes the trailing white space and line terminator characters from a string."
                      },
                      "matchAll": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Matches a string with a regular expression, and returns an iterable of matches\ncontaining the results of that search."
                      },
                      "__@iterator@360": {
                        "type": "object",
                        "properties": {},
                        "additionalProperties": false,
                        "description": "Iterator"
                      },
                      "__entity": {
                        "type": "string",
                        "enum": [
                          "project"
                        ]
                      }
                    },
                    "required": [
                      "toString",
                      "charAt",
                      "charCodeAt",
                      "concat",
                      "indexOf",
                      "lastIndexOf",
                      "localeCompare",
                      "match",
                      "replace",
                      "search",
                      "slice",
                      "split",
                      "substring",
                      "toLowerCase",
                      "toLocaleLowerCase",
                      "toUpperCase",
                      "toLocaleUpperCase",
                      "trim",
                      "length",
                      "substr",
                      "valueOf",
                      "codePointAt",
                      "includes",
                      "endsWith",
                      "normalize",
                      "repeat",
                      "startsWith",
                      "anchor",
                      "big",
                      "blink",
                      "bold",
                      "fixed",
                      "fontcolor",
                      "fontsize",
                      "italics",
                      "link",
                      "small",
                      "strike",
                      "sub",
                      "sup",
                      "padStart",
                      "padEnd",
                      "trimEnd",
                      "trimStart",
                      "trimLeft",
                      "trimRight",
                      "matchAll",
                      "__@iterator@360",
                      "__entity"
                    ],
                    "additionalProperties": false
                  },
                  "type": {
                    "type": "string",
                    "enum": [
                      "task",
                      "bug",
                      "story",
                      "epic",
                      "any"
                    ]
                  },
                  "sort": {
                    "type": "string",
                    "enum": [
                      "updated",
                      "created",
                      "priority"
                    ]
                  },
                  "limit": {
                    "type": "number"
                  }
                },
                "additionalProperties": false
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "What the widget receives",
            "content": {
              "application/json": {
                "schema": {
                  "type": "array",
                  "items": {
                    "$ref": "#/components/schemas/WidgetTask"
                  }
                }
              }
            }
          }
        }
      }
    },
    "/sources/tasks.recent": {
      "post": {
        "operationId": "tasksRecent",
        "tags": [
          "core"
        ],
        "summary": "The newest tasks.",
        "description": "In widget code: `api.get('tasks.recent', params)`. Not an HTTP endpoint — the host calls our API for the widget.",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "limit": {
                    "type": "number"
                  }
                },
                "additionalProperties": false
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "What the widget receives",
            "content": {
              "application/json": {
                "schema": {
                  "type": "array",
                  "items": {
                    "$ref": "#/components/schemas/WidgetTask"
                  }
                }
              }
            }
          }
        }
      }
    },
    "/sources/tasks.mine": {
      "post": {
        "operationId": "tasksMine",
        "tags": [
          "core"
        ],
        "summary": "Open tasks assigned to the person viewing.",
        "description": "In widget code: `api.get('tasks.mine', params)`. Not an HTTP endpoint — the host calls our API for the widget.",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "limit": {
                    "type": "number"
                  }
                },
                "additionalProperties": false
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "What the widget receives",
            "content": {
              "application/json": {
                "schema": {
                  "type": "array",
                  "items": {
                    "$ref": "#/components/schemas/WidgetTask"
                  }
                }
              }
            }
          }
        }
      }
    },
    "/sources/tasks.byStatus": {
      "post": {
        "operationId": "tasksByStatus",
        "tags": [
          "core"
        ],
        "summary": "How many tasks are in each status.",
        "description": "In widget code: `api.get('tasks.byStatus', params)`. Not an HTTP endpoint — the host calls our API for the widget.",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "mine": {
                    "type": "boolean"
                  }
                },
                "additionalProperties": false
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "What the widget receives",
            "content": {
              "application/json": {
                "schema": {
                  "type": "array",
                  "items": {
                    "type": "object",
                    "properties": {
                      "status": {
                        "type": "string"
                      },
                      "category": {
                        "type": "string",
                        "enum": [
                          "done",
                          "todo",
                          "in_progress"
                        ]
                      },
                      "count": {
                        "type": "number"
                      }
                    },
                    "required": [
                      "status",
                      "category",
                      "count"
                    ],
                    "additionalProperties": false
                  }
                }
              }
            }
          }
        }
      }
    },
    "/sources/tasks.trend": {
      "post": {
        "operationId": "tasksTrend",
        "tags": [
          "core"
        ],
        "summary": "Tasks created and closed per day, oldest day first.",
        "description": "In widget code: `api.get('tasks.trend', params)`. Not an HTTP endpoint — the host calls our API for the widget.",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "days": {
                    "type": "number"
                  }
                },
                "additionalProperties": false
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "What the widget receives",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "labels": {
                      "type": "array",
                      "items": {
                        "type": "string"
                      }
                    },
                    "created": {
                      "type": "array",
                      "items": {
                        "type": "number"
                      }
                    },
                    "closed": {
                      "type": "array",
                      "items": {
                        "type": "number"
                      }
                    }
                  },
                  "required": [
                    "labels",
                    "created",
                    "closed"
                  ],
                  "additionalProperties": false
                }
              }
            }
          }
        }
      }
    },
    "/sources/tasks.summary": {
      "post": {
        "operationId": "tasksSummary",
        "tags": [
          "core"
        ],
        "summary": "Open tasks now, and tasks closed per day over a period.",
        "description": "In widget code: `api.get('tasks.summary', params)`. Not an HTTP endpoint — the host calls our API for the widget.",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "days": {
                    "type": "number"
                  }
                },
                "additionalProperties": false
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "What the widget receives",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "open": {
                      "type": "number"
                    },
                    "closed": {
                      "type": "number"
                    },
                    "closedPerDay": {
                      "type": "array",
                      "items": {
                        "type": "number"
                      }
                    }
                  },
                  "required": [
                    "open",
                    "closed",
                    "closedPerDay"
                  ],
                  "additionalProperties": false
                }
              }
            }
          }
        }
      }
    },
    "/sources/notifications.recent": {
      "post": {
        "operationId": "notificationsRecent",
        "tags": [
          "core"
        ],
        "summary": "The person's latest notifications. Open one with { open: 'notification', id }.",
        "description": "In widget code: `api.get('notifications.recent', params)`. Not an HTTP endpoint — the host calls our API for the widget.",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "limit": {
                    "type": "number"
                  },
                  "unread": {
                    "type": "boolean"
                  }
                },
                "additionalProperties": false
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "What the widget receives",
            "content": {
              "application/json": {
                "schema": {
                  "type": "array",
                  "items": {
                    "$ref": "#/components/schemas/WidgetNotification"
                  }
                }
              }
            }
          }
        }
      }
    },
    "/sources/notifications.unread": {
      "post": {
        "operationId": "notificationsUnread",
        "tags": [
          "core"
        ],
        "summary": "How many notifications are unread.",
        "description": "In widget code: `api.get('notifications.unread', params)`. Not an HTTP endpoint — the host calls our API for the widget.",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {},
                "additionalProperties": false
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "What the widget receives",
            "content": {
              "application/json": {
                "schema": {
                  "type": "number"
                }
              }
            }
          }
        }
      }
    },
    "/sources/pages.recent": {
      "post": {
        "operationId": "pagesRecent",
        "tags": [
          "core"
        ],
        "summary": "Pages the person visited last. Open one with { open: 'page', projectId, pageId }.",
        "description": "In widget code: `api.get('pages.recent', params)`. Not an HTTP endpoint — the host calls our API for the widget.",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "limit": {
                    "type": "number"
                  }
                },
                "additionalProperties": false
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "What the widget receives",
            "content": {
              "application/json": {
                "schema": {
                  "type": "array",
                  "items": {
                    "$ref": "#/components/schemas/WidgetPage"
                  }
                }
              }
            }
          }
        }
      }
    },
    "/sources/projects.list": {
      "post": {
        "operationId": "projectsList",
        "tags": [
          "core"
        ],
        "summary": "Projects (knowledge bases) the person can open. Open one with { open: 'project', id }.",
        "description": "In widget code: `api.get('projects.list', params)`. Not an HTTP endpoint — the host calls our API for the widget.",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "limit": {
                    "type": "number"
                  }
                },
                "additionalProperties": false
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "What the widget receives",
            "content": {
              "application/json": {
                "schema": {
                  "type": "array",
                  "items": {
                    "type": "object",
                    "properties": {
                      "id": {
                        "type": "number"
                      },
                      "name": {
                        "type": "string"
                      }
                    },
                    "required": [
                      "id",
                      "name"
                    ],
                    "additionalProperties": false
                  }
                }
              }
            }
          }
        }
      }
    },
    "/sources/repositories.list": {
      "post": {
        "operationId": "repositoriesList",
        "tags": [
          "core"
        ],
        "summary": "Connected repositories. Open one with { open: 'repository', id }.",
        "description": "In widget code: `api.get('repositories.list', params)`. Not an HTTP endpoint — the host calls our API for the widget.",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "limit": {
                    "type": "number"
                  }
                },
                "additionalProperties": false
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "What the widget receives",
            "content": {
              "application/json": {
                "schema": {
                  "type": "array",
                  "items": {
                    "type": "object",
                    "properties": {
                      "id": {
                        "type": "number"
                      },
                      "name": {
                        "type": "string"
                      },
                      "provider": {
                        "type": "string"
                      }
                    },
                    "required": [
                      "id",
                      "name",
                      "provider"
                    ],
                    "additionalProperties": false
                  }
                }
              }
            }
          }
        }
      }
    },
    "/sources/members.list": {
      "post": {
        "operationId": "membersList",
        "tags": [
          "core"
        ],
        "summary": "People of the organization: name and handle only — no e-mails, no ids.",
        "description": "In widget code: `api.get('members.list', params)`. Not an HTTP endpoint — the host calls our API for the widget.",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "limit": {
                    "type": "number"
                  }
                },
                "additionalProperties": false
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "What the widget receives",
            "content": {
              "application/json": {
                "schema": {
                  "type": "array",
                  "items": {
                    "type": "object",
                    "properties": {
                      "name": {
                        "type": "string"
                      },
                      "handle": {
                        "type": "string"
                      }
                    },
                    "required": [
                      "name",
                      "handle"
                    ],
                    "additionalProperties": false
                  }
                }
              }
            }
          }
        }
      }
    },
    "/sources/feed.recent": {
      "post": {
        "operationId": "feedRecent",
        "tags": [
          "core"
        ],
        "summary": "The organization's news feed, newest first.",
        "description": "In widget code: `api.get('feed.recent', params)`. Not an HTTP endpoint — the host calls our API for the widget.",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "limit": {
                    "type": "number"
                  }
                },
                "additionalProperties": false
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "What the widget receives",
            "content": {
              "application/json": {
                "schema": {
                  "type": "array",
                  "items": {
                    "$ref": "#/components/schemas/WidgetFeedItem"
                  }
                }
              }
            }
          }
        }
      }
    },
    "/sources/comments.task": {
      "post": {
        "operationId": "commentsTask",
        "tags": [
          "comments"
        ],
        "summary": "Comments on one task, oldest first. Bodies are cut to 280 characters.",
        "description": "In widget code: `api.get('comments.task', params)`. Not an HTTP endpoint — the host calls our API for the widget.",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "key": {
                    "type": "string"
                  }
                },
                "required": [
                  "key"
                ],
                "additionalProperties": false
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "What the widget receives",
            "content": {
              "application/json": {
                "schema": {
                  "type": "array",
                  "items": {
                    "$ref": "#/components/schemas/WidgetComment"
                  }
                }
              }
            }
          }
        }
      }
    },
    "/sources/chat.unread": {
      "post": {
        "operationId": "chatUnread",
        "tags": [
          "chat"
        ],
        "summary": "How many rooms and messages are unread.",
        "description": "In widget code: `api.get('chat.unread', params)`. Not an HTTP endpoint — the host calls our API for the widget.",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {},
                "additionalProperties": false
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "What the widget receives",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "rooms": {
                      "type": "number"
                    },
                    "messages": {
                      "type": "number"
                    }
                  },
                  "required": [
                    "rooms",
                    "messages"
                  ],
                  "additionalProperties": false
                }
              }
            }
          }
        }
      }
    },
    "/sources/chat.rooms": {
      "post": {
        "operationId": "chatRooms",
        "tags": [
          "chat"
        ],
        "summary": "Rooms of the organization the person is in. Open one with { open: 'room', id }.",
        "description": "In widget code: `api.get('chat.rooms', params)`. Not an HTTP endpoint — the host calls our API for the widget.",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "limit": {
                    "type": "number"
                  }
                },
                "additionalProperties": false
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "What the widget receives",
            "content": {
              "application/json": {
                "schema": {
                  "type": "array",
                  "items": {
                    "type": "object",
                    "properties": {
                      "id": {
                        "type": "string"
                      },
                      "name": {
                        "type": "string"
                      },
                      "lastMessageAt": {
                        "type": "string"
                      }
                    },
                    "required": [
                      "id",
                      "name",
                      "lastMessageAt"
                    ],
                    "additionalProperties": false
                  }
                }
              }
            }
          }
        }
      }
    },
    "/sources/docs.search": {
      "post": {
        "operationId": "docsSearch",
        "tags": [
          "rag"
        ],
        "summary": "Search the documentation. Open a hit with { open: 'page', projectId, pageId }.",
        "description": "In widget code: `api.get('docs.search', params)`. Not an HTTP endpoint — the host calls our API for the widget.",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "query": {
                    "type": "string"
                  },
                  "limit": {
                    "type": "number"
                  }
                },
                "required": [
                  "query"
                ],
                "additionalProperties": false
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "What the widget receives",
            "content": {
              "application/json": {
                "schema": {
                  "type": "array",
                  "items": {
                    "$ref": "#/components/schemas/WidgetDocHit"
                  }
                }
              }
            }
          }
        }
      }
    },
    "/sources/code.search": {
      "post": {
        "operationId": "codeSearch",
        "tags": [
          "rag"
        ],
        "summary": "Search the code of the organization's repositories.",
        "description": "In widget code: `api.get('code.search', params)`. Not an HTTP endpoint — the host calls our API for the widget.",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "query": {
                    "type": "string"
                  },
                  "limit": {
                    "type": "number"
                  }
                },
                "required": [
                  "query"
                ],
                "additionalProperties": false
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "What the widget receives",
            "content": {
              "application/json": {
                "schema": {
                  "type": "array",
                  "items": {
                    "$ref": "#/components/schemas/WidgetCodeHit"
                  }
                }
              }
            }
          }
        }
      }
    },
    "/sources/coverage.repository": {
      "post": {
        "operationId": "coverageRepository",
        "tags": [
          "graph"
        ],
        "summary": "How much of a repository is documented.",
        "description": "In widget code: `api.get('coverage.repository', params)`. Not an HTTP endpoint — the host calls our API for the widget.",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "repositoryId": {
                    "type": "number"
                  }
                },
                "required": [
                  "repositoryId"
                ],
                "additionalProperties": false
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "What the widget receives",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "units": {
                      "type": "number"
                    },
                    "mentioned": {
                      "type": "number"
                    },
                    "documented": {
                      "type": "number"
                    },
                    "computedAt": {
                      "type": "string"
                    }
                  },
                  "required": [
                    "units",
                    "mentioned",
                    "documented",
                    "computedAt"
                  ],
                  "additionalProperties": false,
                  "nullable": true
                }
              }
            }
          }
        }
      }
    },
    "/sources/agents.work": {
      "post": {
        "operationId": "agentsWork",
        "tags": [
          "agents"
        ],
        "summary": "Tasks agents are working on now. Open one with { open: 'task', key } using the key from tasks.* sources.",
        "description": "In widget code: `api.get('agents.work', params)`. Not an HTTP endpoint — the host calls our API for the widget.",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {},
                "additionalProperties": false
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "What the widget receives",
            "content": {
              "application/json": {
                "schema": {
                  "type": "array",
                  "items": {
                    "type": "object",
                    "properties": {
                      "taskId": {
                        "type": "number"
                      },
                      "state": {
                        "type": "string"
                      },
                      "waiting": {
                        "type": "boolean"
                      },
                      "where": {
                        "type": "string",
                        "enum": [
                          "computer",
                          "runner"
                        ]
                      },
                      "label": {
                        "type": "string"
                      },
                      "updatedAt": {
                        "type": "string"
                      }
                    },
                    "required": [
                      "taskId",
                      "state",
                      "waiting",
                      "where",
                      "label",
                      "updatedAt"
                    ],
                    "additionalProperties": false
                  }
                }
              }
            }
          }
        }
      }
    },
    "/sources/agents.runners": {
      "post": {
        "operationId": "agentsRunners",
        "tags": [
          "agents"
        ],
        "summary": "Agent runners the person can see, and whether they are online.",
        "description": "In widget code: `api.get('agents.runners', params)`. Not an HTTP endpoint — the host calls our API for the widget.",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {},
                "additionalProperties": false
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "What the widget receives",
            "content": {
              "application/json": {
                "schema": {
                  "type": "array",
                  "items": {
                    "type": "object",
                    "properties": {
                      "label": {
                        "type": "string"
                      },
                      "online": {
                        "type": "boolean"
                      }
                    },
                    "required": [
                      "label",
                      "online"
                    ],
                    "additionalProperties": false
                  }
                }
              }
            }
          }
        }
      }
    }
  },
  "components": {
    "schemas": {
      "WidgetTask": {
        "type": "object",
        "properties": {
          "key": {
            "type": "string"
          },
          "title": {
            "type": "string"
          },
          "type": {
            "type": "string",
            "enum": [
              "task",
              "bug",
              "story",
              "epic"
            ]
          },
          "priority": {
            "type": "number"
          },
          "status": {
            "type": "string",
            "description": "Status name as the organization spells it."
          },
          "done": {
            "type": "boolean"
          },
          "createdAt": {
            "type": "string"
          },
          "updatedAt": {
            "type": "string"
          }
        },
        "required": [
          "key",
          "title",
          "type",
          "priority",
          "status",
          "done",
          "createdAt",
          "updatedAt"
        ],
        "additionalProperties": false
      },
      "WidgetNotification": {
        "type": "object",
        "properties": {
          "id": {
            "type": "string"
          },
          "title": {
            "type": "string"
          },
          "body": {
            "type": "string"
          },
          "actor": {
            "type": "string",
            "description": "Who did it, if anyone."
          },
          "type": {
            "type": "string"
          },
          "read": {
            "type": "boolean"
          },
          "createdAt": {
            "type": "string"
          }
        },
        "required": [
          "id",
          "title",
          "body",
          "actor",
          "type",
          "read",
          "createdAt"
        ],
        "additionalProperties": false
      },
      "WidgetFeedItem": {
        "type": "object",
        "properties": {
          "id": {
            "type": "string"
          },
          "kind": {
            "type": "string"
          },
          "summary": {
            "type": "string"
          },
          "actor": {
            "type": "string"
          },
          "count": {
            "type": "number",
            "description": "How many events this item folds together."
          },
          "occurredAt": {
            "type": "string"
          }
        },
        "required": [
          "id",
          "kind",
          "summary",
          "actor",
          "count",
          "occurredAt"
        ],
        "additionalProperties": false
      },
      "WidgetComment": {
        "type": "object",
        "properties": {
          "id": {
            "type": "string"
          },
          "author": {
            "type": "string"
          },
          "body": {
            "type": "string"
          },
          "quoted": {
            "type": "string",
            "description": "The text the comment is anchored to, if any."
          },
          "resolved": {
            "type": "boolean"
          },
          "createdAt": {
            "type": "string"
          }
        },
        "required": [
          "id",
          "author",
          "body",
          "quoted",
          "resolved",
          "createdAt"
        ],
        "additionalProperties": false
      },
      "WidgetDocHit": {
        "type": "object",
        "properties": {
          "projectId": {
            "type": "number"
          },
          "pageId": {
            "type": "number"
          },
          "title": {
            "type": "string",
            "description": "Headings path, e.g. \"Install › Docker\"."
          },
          "snippet": {
            "type": "string"
          }
        },
        "required": [
          "projectId",
          "pageId",
          "title",
          "snippet"
        ],
        "additionalProperties": false
      },
      "WidgetCodeHit": {
        "type": "object",
        "properties": {
          "repositoryId": {
            "type": "number"
          },
          "language": {
            "type": "string"
          },
          "kind": {
            "type": "string"
          },
          "description": {
            "type": "string"
          },
          "snippet": {
            "type": "string"
          }
        },
        "required": [
          "repositoryId",
          "language",
          "kind",
          "description",
          "snippet"
        ],
        "additionalProperties": false
      },
      "WidgetPage": {
        "type": "object",
        "properties": {
          "pageId": {
            "type": "number"
          },
          "page": {
            "type": "string"
          },
          "projectId": {
            "type": "number"
          },
          "project": {
            "type": "string"
          },
          "visitedAt": {
            "type": "string"
          }
        },
        "required": [
          "pageId",
          "page",
          "projectId",
          "project",
          "visitedAt"
        ],
        "additionalProperties": false
      }
    }
  }
}
```

## Versions

- **v1.1.0** (2026-11-11) — Extended source tasks.list: ({ status?: 'open' | 'done' | 'all'; mine?: boolean; assignee?: UserRef; project?: ProjectRef; type?: 'any' | 'task' | 'bug' | 'story' | 'epic'; sort?: 'updated' | 'created' | 'priority'; limit?: number }) => WidgetTask[]; Widened declaration SettingSpec; Widened declaration SettingValue; Added declaration user; Added declaration project; Added declaration repo; Added declaration org; Added model UserRef; Added model ProjectRef; Added model RepoRef; Added model OrgRef
- **v1.0.2** (2026-11-11) — Documentation
- **v1.0.1** (2026-11-11) — Documentation
- **v1.0.0** (2026-11-11) — First release of the widget API

## Type declarations

Also published with the app at `/widget-api/latest.d.ts`.

```typescript
// Widget API — generated from src/components/widgets/contract.ts. Do not edit.

type Tone = 'default' | 'primary' | 'success' | 'warning' | 'danger';

/** Where a press may lead. Never a URL. */
type Intent =
  | { open: 'task'; key: string }
  | { open: 'project'; id: number }
  | { open: 'page'; projectId: number; pageId: number }
  | { open: 'section'; name: 'tasks' | 'feed' | 'repositories' | 'members' | 'messages' }
  | { open: 'notification'; id: string }
  | { open: 'repository'; id: number }
  | { open: 'room'; id: string };

/** What components return. Opaque: build it with JSX, hand it to render(). */
interface UiNode { readonly __uiNode: true }

type TextChild = string | number | boolean | null | undefined | TextChild[];
type Child = UiNode | TextChild | Child[];

interface ChartSeries { name: string; values: number[]; tone?: Tone }

declare namespace JSX {
  type Element = UiNode;
  interface ElementChildrenAttribute { children: {} }
  /** No DOM: <div> and friends do not exist inside the box. */
  interface IntrinsicElements {}
}

/** Draw the widget. Call it again to redraw (calls are coalesced). Limits:
 *  depth 8, 500 nodes, 100 children per node. */
declare function render(node: UiNode): void;

type SettingSpec =
  | { type: 'select'; label?: string; options: readonly (string | { value: string; label?: string })[]; default?: string }
  | { type: 'number'; label?: string; min?: number; max?: number; step?: number; default?: number }
  | { type: 'boolean'; label?: string; default?: boolean }
  | { type: 'text'; label?: string; maxLength?: number; default?: string }
  /** Picked by name in the settings form; the value is a reference ('' if none). */
  | { type: 'user'; label?: string; default?: string }
  | { type: 'project'; label?: string; default?: string }
  | { type: 'repository'; label?: string; default?: string }
  | { type: 'organization'; label?: string; default?: string };

type OptionValue<O> = O extends string ? O : O extends { value: infer V } ? V : never;

type SettingValue<S> =
  S extends { type: 'select'; options: readonly (infer O)[] } ? OptionValue<O> :
  S extends { type: 'number' } ? number :
  S extends { type: 'boolean' } ? boolean :
  S extends { type: 'user' } ? UserRef | '' :
  S extends { type: 'project' } ? ProjectRef | '' :
  S extends { type: 'repository' } ? RepoRef | '' :
  S extends { type: 'organization' } ? OrgRef | '' :
  string;

/** Declare what the person can set; get back what they chose (or the
 *  defaults). The host draws the form and restarts the widget on change. */
declare function settings<const S extends Record<string, SettingSpec>>(decl: S): { readonly [K in keyof S]: SettingValue<S[K]> };

/** Entity references. Type the name after @ in the editor and pick: the
 *  editor writes the id and shows the name. */
declare function user(id: string): UserRef;
declare function project(id: string | number): ProjectRef;
declare function repo(id: string | number): RepoRef;
declare function org(id: string): OrgRef;

/** The JSX factory the box provides. You never call it: <Row/> compiles to it. */
declare function h(type: unknown, props: unknown, ...children: unknown[]): UiNode;

/** Fragment: <>…</> is a List. */
declare const Fragment: (props: { children?: Child }) => UiNode;

/** A reference to one of our entities. In code it is written user("…"),
 *  project("…"), repo("…"), org("…"); the editor finds the id by name and
 *  shows the name over it. Opaque to the widget: it can only hand it back. */
type UserRef = string & { readonly __entity: 'user' };

type ProjectRef = string & { readonly __entity: 'project' };

type RepoRef = string & { readonly __entity: 'repository' };

type OrgRef = string & { readonly __entity: 'organization' };

/** A task, as a widget sees it: what a list row needs, nothing about people. */
type WidgetTask = {
  key: string;
  title: string;
  type: 'task' | 'bug' | 'story' | 'epic';
  priority: number;
  /** Status name as the organization spells it. */
  status: string;
  done: boolean;
  createdAt: string;
  updatedAt: string;
};

type WidgetNotification = {
  id: string;
  title: string;
  body: string;
  /** Who did it, if anyone. */
  actor: string;
  type: string;
  read: boolean;
  createdAt: string;
};

type WidgetFeedItem = {
  id: string;
  kind: string;
  summary: string;
  actor: string;
  /** How many events this item folds together. */
  count: number;
  occurredAt: string;
};

type WidgetComment = {
  id: string;
  author: string;
  body: string;
  /** The text the comment is anchored to, if any. */
  quoted: string;
  resolved: boolean;
  createdAt: string;
};

type WidgetDocHit = {
  projectId: number;
  pageId: number;
  /** Headings path, e.g. "Install › Docker". */
  title: string;
  snippet: string;
};

type WidgetCodeHit = {
  repositoryId: number;
  language: string;
  kind: string;
  description: string;
  snippet: string;
};

type WidgetPage = {
  pageId: number;
  page: string;
  projectId: number;
  project: string;
  visitedAt: string;
};

/** Every data source a widget can read: api.get(name, params) → result. */
type WidgetSources = {
  /** Tasks of the organization by a filter. */
  'tasks.list': {
    params: { status?: 'open' | 'done' | 'all'; mine?: boolean; /** Tasks assigned to this person. */ assignee?: UserRef; /** Tasks linked to this project. */ project?: ProjectRef; type?: 'any' | 'task' | 'bug' | 'story' | 'epic'; sort?: 'updated' | 'created' | 'priority'; /** 1..50, default 10 */ limit?: number };
    result: WidgetTask[];
  };
  /** The newest tasks. */
  'tasks.recent': {
    params: { /** 1..50, default 10 */ limit?: number };
    result: WidgetTask[];
  };
  /** Open tasks assigned to the person viewing. */
  'tasks.mine': {
    params: { /** 1..50, default 20 */ limit?: number };
    result: WidgetTask[];
  };
  /** How many tasks are in each status. */
  'tasks.byStatus': {
    params: { mine?: boolean };
    result: { status: string; category: 'todo' | 'in_progress' | 'done'; count: number }[];
  };
  /** Tasks created and closed per day, oldest day first. */
  'tasks.trend': {
    params: { /** 1..30, default 14 */ days?: number };
    result: { labels: string[]; created: number[]; closed: number[] };
  };
  /** Open tasks now, and tasks closed per day over a period. */
  'tasks.summary': {
    params: { /** 1..30, default 7 */ days?: number };
    result: { open: number; closed: number; closedPerDay: number[] };
  };
  /** The person's latest notifications. Open one with { open: 'notification', id }. */
  'notifications.recent': {
    params: { /** 1..30, default 10 */ limit?: number; unread?: boolean };
    result: WidgetNotification[];
  };
  /** How many notifications are unread. */
  'notifications.unread': {
    params: Record<string, never>;
    result: number;
  };
  /** Pages the person visited last. Open one with { open: 'page', projectId, pageId }. */
  'pages.recent': {
    params: { /** 1..20, default 8 */ limit?: number };
    result: WidgetPage[];
  };
  /** Projects (knowledge bases) the person can open. Open one with { open: 'project', id }. */
  'projects.list': {
    params: { /** 1..100, default 20 */ limit?: number };
    result: { id: number; name: string }[];
  };
  /** Connected repositories. Open one with { open: 'repository', id }. */
  'repositories.list': {
    params: { /** 1..100, default 20 */ limit?: number };
    result: { id: number; name: string; provider: string }[];
  };
  /** People of the organization: name and handle only — no e-mails, no ids. */
  'members.list': {
    params: { /** 1..200, default 50 */ limit?: number };
    result: { name: string; handle: string }[];
  };
  /** The organization's news feed, newest first. */
  'feed.recent': {
    params: { /** 1..30, default 10 */ limit?: number };
    result: WidgetFeedItem[];
  };
  /** Comments on one task, oldest first. Bodies are cut to 280 characters. */
  'comments.task': {
    params: { /** Task key, e.g. "ND-12" */ key: string };
    result: WidgetComment[];
  };
  /** How many rooms and messages are unread. */
  'chat.unread': {
    params: Record<string, never>;
    result: { rooms: number; messages: number };
  };
  /** Rooms of the organization the person is in. Open one with { open: 'room', id }. */
  'chat.rooms': {
    params: { /** 1..50, default 10 */ limit?: number };
    result: { id: string; name: string; lastMessageAt: string }[];
  };
  /** Search the documentation. Open a hit with { open: 'page', projectId, pageId }. */
  'docs.search': {
    params: { /** 2..200 characters */ query: string; /** 1..20, default 5 */ limit?: number };
    result: WidgetDocHit[];
  };
  /** Search the code of the organization's repositories. */
  'code.search': {
    params: { /** 2..200 characters */ query: string; /** 1..20, default 5 */ limit?: number };
    result: WidgetCodeHit[];
  };
  /** How much of a repository is documented. */
  'coverage.repository': {
    params: { repositoryId: number };
    result: { units: number; mentioned: number; documented: number; computedAt: string } | null;
  };
  /** Tasks agents are working on now. Open one with { open: 'task', key } using the key from tasks.* sources. */
  'agents.work': {
    params: Record<string, never>;
    result: { taskId: number; state: string; waiting: boolean; where: 'computer' | 'runner'; label: string; updatedAt: string }[];
  };
  /** Agent runners the person can see, and whether they are online. */
  'agents.runners': {
    params: Record<string, never>;
    result: { label: string; online: boolean }[];
  };
};

/** Read data. Only named sources; params are checked by the host. */
declare const api: {
  get<K extends keyof WidgetSources>(source: K, params?: WidgetSources[K]['params']): Promise<WidgetSources[K]['result']>;
};

/** A vertical stack. Also what <>…</> becomes. */
declare const List: (props: { children?: Child }) => UiNode;

/** A horizontal line. With onPress it is a button that asks the host to open something. */
declare const Row: (props: { onPress?: Intent; children?: Child }) => UiNode;

/** Text. Never HTML. */
declare const Text: (props: { muted?: boolean; mono?: boolean; children?: TextChild }) => UiNode;

/** A small section title. */
declare const Heading: (props: { children?: TextChild }) => UiNode;

/** A short label with a tone. */
declare const Chip: (props: { tone?: Tone; children?: TextChild }) => UiNode;

/** A labelled number. */
declare const Stat: (props: { label: string; value: string; tone?: Tone }) => UiNode;

/** Tiles in 1–4 columns. */
declare const Grid: (props: { columns?: 1 | 2 | 3 | 4; children?: Child }) => UiNode;

/** A minimal bar sparkline. */
declare const Bar: (props: { values: number[] }) => UiNode;

/** Bar or line chart, up to 6 series. */
declare const Chart: (props: { kind?: 'bar' | 'line'; labels?: string[]; series: ChartSeries[]; stacked?: boolean }) => UiNode;

/** Parts of a whole. */
declare const Donut: (props: { segments: { label: string; value: number; tone?: Tone }[] }) => UiNode;

/** Ours: the widget places it and cannot configure it. */
declare const AgentChat: (props: Record<string, never>) => UiNode;
```
