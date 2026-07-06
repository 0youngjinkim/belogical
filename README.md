# belogical — a skill that makes AI answer logically

> AI answers, conclusion first and in the order a reader can follow. Barbara Minto's Pyramid Principle, ported to a Claude Code skill.

AI answers are too long, too dense, and too complex for people. They follow the mechanical order the information arrived in, with no regard for how human comprehension works or what it costs. belogical builds on Barbara Minto's Pyramid Principle to make AI always set the conclusion first and answer in the order a reader can follow.

It's a Claude Code skill you invoke with `/belogical`. Use it to write standalone documents (reports, proposals, READMEs), to draw a conclusion out of unsorted material, to check and repair the logic of text you already have, or simply to make an answer land logically.

## Requirements

[Claude Code](https://code.claude.com/docs), any version that supports skills and plugins.

## Installation

Two ways. The plugin install is recommended.

### Option 1 — plugin marketplace (recommended)

Two commands in Claude Code and you're done.

```
/plugin marketplace add 0youngjinkim/belogical-en
/plugin install belogical@belogical-en
```

Once installed, invoke it with `/belogical`. To update later, run `/plugin marketplace update belogical-en`.

### Option 2 — manual copy

Copy the `skills/belogical/` directory into one of the locations below. Principles, router, and modules live in one folder, so this single copy is all it takes.

- `~/.claude/skills/` — global; `/belogical` works in every project.
- `<project>/.claude/skills/` — that project only.

## Usage

Invoke `/belogical` directly. Call it bare and the router classifies the request into one of four routes; name a route as the argument to go straight there.

- `/belogical` — classify the request and route to answer, document, organize, or repair
- `/belogical document` — standalone document writing (SCQA introduction + pyramid building + page layout)
- `/belogical organize` — draw a conclusion from unsorted material and ideas (bottom-up + logic tree)
- `/belogical repair` — diagnose and repair existing text (extract → diagnose → rearrange)

## Two ways to apply it

There are two ways to apply the principles, and they can be combined.

- **On invocation (default)**: calling `/belogical` loads the principles and routing together. The skill is explicit-invocation only (`disable-model-invocation` in the frontmatter), so it fires only when you type it and never injects itself into ordinary requests like "write me a report".
- **Ambient (optional)**: to apply the principles to every conversation without invoking the skill, copy only the 'Governing principles' section between the `BELOGICAL:PRINCIPLES` markers in `skills/belogical/SKILL.md` into your global (`~/.claude/CLAUDE.md`) or project CLAUDE.md. The source of truth stays in one place; when it changes, update only your pasted copy.

## What's inside

One set of principles and six methodologies.

| File | Role |
|---|---|
| `skills/belogical/SKILL.md` | Governing principles + router — applies the principles, classifies the request, and points to the right methodology module |
| `skills/belogical/references/` | Six methodology modules — loaded only on their route |

The principles and the router live in the single SKILL.md. Invoking the skill loads that file whole, so the principles apply first and only the module the request needs is added on top.

```
belogical-en/
├── README.md
├── LICENSE
├── .claude-plugin/
│   ├── marketplace.json   # plugin marketplace catalog
│   └── plugin.json        # plugin manifest
└── skills/
    └── belogical/
        ├── SKILL.md                # Governing principles (marked section, paste-ready for ambient use) + router: classify → load module → common gate
        └── references/
            ├── build-pyramid.md    # Setting the apex — five top-down questions / three bottom-up steps
            ├── scqa-intro.md       # Introduction design — SCQA, order variants, skeletons by document type
            ├── grouping-order.md   # Grouping and checking — three rules, deduction vs induction, MECE, summaries
            ├── page-delivery.md    # Page and screen delivery — the 30-second rule, headings, presentations
            ├── thinking-tools.md   # Thinking tools — problem definition, structuring relationships (logic trees)
            └── repair-text.md      # Repairing existing text — extraction, diagnosis, rearrangement
```

## Source

Barbara Minto, *The Minto Pyramid Principle*. The methodology's vocabulary and concepts follow the original, but no original text is reproduced — everything is distilled into core principles. The numeric thresholds the original gives (4–5 items per group, 30 seconds) are treated as recommended defaults, not absolute rules.

## License

MIT — use, modify, and redistribute freely. The methodology itself is copyright its original author (Barbara Minto); this repository's license covers only the skill files it contains.
