# Hello, hello, hello: MCP server

An MCP server that lets Claude search and quote the book "Hello, hello, hello" by Nigel Blackmore, and build slide decks from it. Every result links back to the live site: https://tablackmore.github.io/hello-hello/

Page numbers follow the original printed edition.

## Install

Claude Code:

```
claude mcp add hello-hello -- npx -y github:tablackmore/hello-hello
```

Claude Desktop (`claude_desktop_config.json`):

```json
{"mcpServers":{"hello-hello":{"command":"npx","args":["-y","github:tablackmore/hello-hello"]}}}
```

Requires Node 18 or later. No other dependencies; the book data is bundled.

## Tools

- `search_book {query, limit=8}`: full-text search, tolerant of typos and diacritics, page-level hits with snippets.
- `lookup_index {term}`: look up a term in the printed index and get page links.
- `get_passage {chapter, page?, heading?, context=0}`: read a page, or the page under a heading, with optional neighbouring pages.
- `get_chapter {chapter, include_text=false, offset=0}`: chapter overview, or its text in slices of up to 20,000 characters with `next_offset`.
- `list_figures {chapter?, topic?}`: figures and captions; only figures with `published: true` have an `imageUrl`.
- `list_contents {}`: all chapters with page ranges and links.

Prompt: `slide_deck {topic, slides="10"}` builds a cited deck with speaker notes and a Sources slide.
Resource: `book://chapter/{id}` gives a chapter as plain text.

Chapter ids can be typed loosely: `"18a"`, `"Chapter 17"`, `17`.

© Nigel Blackmore. All rights reserved.
