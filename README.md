<p align="center">
  <img src="docs/logo.svg" width="84" height="84" alt="" />
</p>

<h1 align="center">AI Chat Exporter</h1>

<p align="center">
  <b>Your AI chats, as clean Markdown.</b><br>
  Keep the conversations worth keeping — from <b>Claude</b>, <b>ChatGPT</b> and <b>Mistral Vibe</b>.
</p>

<p align="center">
  <a href="https://markusritschel.github.io/ai-chat-exporter/"><img src="https://img.shields.io/badge/Install-AI%20Chat%20Export%20bookmark-0f766e?style=for-the-badge" alt="Install the AI Chat Export bookmark" /></a>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Claude-stable-0f766e" alt="Claude: stable" />
  <img src="https://img.shields.io/badge/ChatGPT-beta-b45309" alt="ChatGPT: beta" />
  <img src="https://img.shields.io/badge/Mistral%20Vibe-beta-b45309" alt="Mistral Vibe: beta" />
  <a href="LICENSE"><img src="https://img.shields.io/badge/license-MIT-55625f" alt="MIT licence" /></a>
</p>

<p align="center"><sub>free · MIT-licensed · works locally</sub></p>

---

One click saves the chat on your screen as a `.md` file — every table, formula and code block
as the assistant wrote it, with frontmatter your notes app understands.

## Set up once, use on every chat

No extension and no account — the whole tool lives in one bookmark.

1. **Add it to your bar.** On the [install page](https://markusritschel.github.io/ai-chat-exporter/), pull the _AI Chat Export_ button up into your bookmarks bar.
2. **Open a conversation** on [claude.ai](https://claude.ai), [chatgpt.com](https://chatgpt.com) or [chat.mistral.ai](https://chat.mistral.ai).
3. **Click to save.** A small notice confirms the export, and the Markdown file lands in your downloads.

**Bookmarks bar hidden, or dragging not working?** The install page has a _Copy the code_
button: create a bookmark by hand and paste the code in as its address. It behaves exactly like
the dragged one.

**Keeping it current.** Each time you use it, the bookmark checks whether a newer version
exists and says so with a short notice. Drag the button from the install page again to refresh
your bookmark.

<details>
<summary><b>Prefer the developer console?</b></summary>

1. Open the conversation, then the browser's developer console — <kbd>F12</kbd> in most browsers; in Safari, turn on the Develop menu and press <kbd>⌥</kbd><kbd>⌘</kbd><kbd>C</kbd>.
2. Paste the complete contents of [`ai-chat-exporter.js`](ai-chat-exporter.js) and press <kbd>Enter</kbd>.

Chrome, Edge and Firefox refuse the first paste into a console as a safety measure. Type
`allow pasting`, press <kbd>Enter</kbd> and paste again; the browser remembers it.
</details>

## Everything, exactly as written

It reads each app's own data — never the rendered page — so nothing is lost in translation.

- **Source-level fidelity.** Tables, formulas and code blocks come from the assistant's own markdown — nothing is scraped from the screen or converted from HTML.
- **The version you see.** Regenerated or edited a message? The export follows the branch that's on your screen. To save another version, switch to it first; no reload needed.
- **Made for notes and retrieval.** Frontmatter (`title`, `source`, `model`, `exported`) turns into Obsidian properties, and one `#` heading per turn gives retrieval pipelines tidy chunks — the assistant's own `##` headings nest underneath.
- **Artifacts & attachments.** Claude's artifacts (in their final version), created files and charts arrive as fenced code; uploads are noted above the message they belong to.
- **Long chats, complete.** The whole thread comes from the API — no scrolling, and no messages missing because they weren't rendered.
- **Stays on your machine.** The file is assembled inside your browser tab. There is no server behind this tool to send anything to.

### What a saved chat looks like

The file is named after the conversation — here `merge_two_sorted_lists.md`:

````markdown
---
title: "Merge two sorted lists"
source: "https://chatgpt.com/c/…"
model: "gpt-5"
exported: 2026-09-26
---

# Human — Sep 24, 2026, 9:14 AM

How do I merge two sorted lists in Python?

# ChatGPT — Sep 24, 2026, 9:14 AM

Use `heapq.merge` — lazy and stable:

```python
from heapq import merge
merged = list(merge(a, b))
```
````

On Claude, special elements sit where they appeared, each under a short label:

````markdown
> **Attachment: notes.md · text/markdown · 2.0 KB**
>
> (the attachment's text, quoted)

**Artifact: Merge helper · python**

```python
def merge_sorted(a, b): ...
```
````

A reply you stopped early ends with an `Interrupted` note, so a short answer isn't mistaken for
a broken export. Turn headings read `# Claude`, `# ChatGPT` or `# Vibe`, and the file body
contains no emoji.

## Supported apps

One bookmark detects the site it's on and reads that app's own API.

| App                                | Status | Saved                                                                                            | Left out                                                                    |
| ---------------------------------- | ------ | ------------------------------------------------------------------------------------------------ | --------------------------------------------------------------------------- |
| **Claude** · claude.ai             | stable | Answers; artifacts (final version), created files and charts as fenced code; attachments (below) | Thinking, web search and other tool calls, map/recipe-style display widgets |
| **ChatGPT** · chatgpt.com          | beta   | Answers; uploads listed by name. Team/Enterprise workspaces supported                            | Reasoning, tool runs (code, browsing), canvas documents, search citations   |
| **Mistral Vibe** · chat.mistral.ai | beta   | Answers, following the version on screen                                                         | Canvas documents, uploads                                                   |

**Attachments on Claude, precisely:** the extracted text of text files (.md, .docx, .txt, .html…)
is quoted in full. Images and PDFs appear as links to claude.ai, which open only while you're
signed in to the same account; other files (audio, for instance) are named. The files
themselves are not packed into the export.

**Beta** means exports work on live conversations, but ChatGPT and Vibe don't document the
data this relies on, and it can change without warning. If a result looks wrong, the browser
console explains what happened — please [open an issue](../../issues).

## Your data stays with you

For your conversation, the bookmark talks only to the chat app you're signed in to. It asks for
the conversation the same way the app itself does, turns it into Markdown inside your tab and
hands the file to your browser. **No copy goes anywhere else.**

Each run also compares your bookmark with the newest version on GitHub. That check downloads a
public file and sends nothing about you or your chats. The install page itself contacts GitHub
only — for the script and the star count — and loads no fonts, trackers or other outside
resources.

## Status messages

While it works, a small box in the top-right corner reports progress. It stays until you've
had a chance to read it — it only counts down while the tab has focus, so a save dialog won't
hide it — and hovering keeps it open; a click closes it.

| Message                                                   | What it means                                                                                                                        |
| --------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| `Fetching conversation…`                                  | Reading the chat from the app's API                                                                                                  |
| `✅ Exported N messages: file.md`                         | Saved                                                                                                                                |
| `✅ Exported N messages (1 interrupted response): …`      | Saved and complete — a reply was stopped before it finished, and the file says so at that spot                                       |
| `⚠️ Exported N messages (1 message flagged truncated): …` | Saved; Claude's data marked one message `truncated`. It's noted inline — worth a glance at the original                              |
| `⚠️ Exported N messages (1 warning — see console): …`     | Saved, but something couldn't be rebuilt cleanly, e.g. an artifact edit or a branch that couldn't be traced. The console has details |
| `Error: …`                                                | Nothing saved; the box names the cause, such as `Open a specific ChatGPT conversation first…` or an expired session                  |

If nothing works at all: check that you're signed in and have a specific conversation open, then
reload the tab and try again. Scrolling first is never necessary.

## Limitations

- Works in the web apps of Claude, ChatGPT and Mistral Vibe while you're signed in, in current Chrome, Edge, Firefox and Safari.
- The apps' data formats are undocumented; when one changes, this tool needs an update.
- **Left out on purpose:** the models' thinking and reasoning (drafts and discarded ideas would muddy search results and the document outline) and web-search results (their links expire).
- **Not supported yet:** canvas documents in ChatGPT and Vibe, Vibe uploads, and bundling the attached files themselves — a ZIP with the originals may come later.

## How it works

The bookmark carries the complete script. On click it checks which site it's on, asks that
app's API for the open conversation — Claude's `chat_conversations`, ChatGPT's
`backend-api/conversation`, Vibe's `message.all` — and follows the conversation tree along the
branch you're viewing. It keeps the answer text in order (plus Claude's artifacts, files and
charts in place), skips hidden, system and tool messages, adds the frontmatter and turn
headings, and downloads the result. Reading the data rather than the page is what makes long
chats complete and keeps the tool independent of each app's changing layout.

## For developers

The script is a single closure. A loader per app — `loadClaude` (`fetchConversationData` →
`getOrderedMessages`), `loadChatGPT`, `loadMistral` — returns the same list of messages, and
`buildMarkdown` turns that into the file. [`AGENTS.md`](AGENTS.md) documents each app's data
contract, including which fields were verified against live responses. A new Claude tool type
is a one-line addition to `renderToolUse`.

Issues and pull requests are welcome — especially updates when an app changes its data, and
canvas export.

## License

MIT — see [LICENSE](LICENSE).

AI Chat Exporter grew out of [Claude Chat Exporter](https://github.com/agarwalvishal/claude-chat-exporter)
by Vishal Agarwal. Its idea of reading the chat app's own data instead of the page — and much of
the Claude export — is his work. Thank you.

Not affiliated with Anthropic, OpenAI or Mistral AI. Use it in line with each provider's terms
of service.
