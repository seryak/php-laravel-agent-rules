# LLM Agent Rules

I created this repository as a template for configuring LLM agents according to my technology stack and the individual characteristics of my projects.

The main file is **AGENTS.md**.

In it, I describe how an agent should behave and what my preferences are when editing Laravel and PHP code. I also document how to apply tests, work with the frontend, and handle other aspects of development. I use this together with RooCode https://roocode.com/, but it can also be useful for other agents.

This repository helps AI agents behave the way I expect by providing **explicit and enforceable contracts** for AI agents:
- how to write code
- how to run commands
- when a real browser must be used
- how to validate changes
- how to handle deviations from the rules

## Core Concept

Each project or technology stack is described using:

- **AGENTS.md** — the entry point and behavioral contract for the AI
- **Rule files** — narrowly scoped, domain-specific constraints (PHP, Laravel, Tailwind, testing, browser, etc.)

Expected agent behavior:
1. Read `AGENTS.md`
2. Open the required rule files
3. Follow them strictly
4. Explicitly report any deviations

---

## Rules Structure

```text
.
├── AGENTS.md
├── .humans/ (documents in my native language, later translated into English for LLMs)
│   ├── laravel-core-rules.md
│   ├── php-rules.md
│   ├── phpunit-core-rules.md
│   ├── tailwindcss-rules.md
│   └── browser-skill-rules.md
└── .agents/
    ├── laravel-core-rules.md
    ├── php-rules.md
    ├── phpunit-core-rules.md
    ├── tailwindcss-rules.md
    └── browser-skill-rules.md
```

## What Goes Into AGENTS.md

`AGENTS.md` is the **router and single source of truth**.

Typical responsibilities of this file:
- defining rule priority
- specifying which rule files must be opened and when
- describing environment constraints (Docker, paths, URLs)
- integrating tools (browser, tests, formatters)
- enforcing explicit deviation reporting

---

## Rule Files Philosophy

To avoid overloading the AI agent’s context, rule files should:
- be written in English
- be small
- be LLM-friendly
- use the words `ALWAYS`, `MUST`, `MUST NOT`
- include clear examples (`Bad / Good`)
- have zero ambiguity
- each cover **exactly one area of responsibility**

---

## Important Notes

- In my projects, I use the spec-driven framework OpenSpec https://openspec.dev/, therefore `AGENTS.md` contains the block `<!-- OPENSPEC:START --> … <!-- OPENSPEC:END -->`. Remove it if you do not use OpenSpec.
- The `<laravel-boost-guidelines>` block is only required if you use Laravel Boost MCP https://laravel.com/ai/boost. Remove this block if you are not using this MCP.
- Feel free to add or change rules and preferences as you see fit. The rules I provide are not the only correct way to work.
- Except for the `.agents` directory and the `AGENTS.md` file, all other files are OPTIONAL.
