**English** | [한국어](README-ko.md)

# belogical — a skill that makes AI answer logically

> Answer first. Reasons after.

AI produces more and more text, but the amount a person can read and understand in a day is fixed. Using that time efficiently means raising the quality of every piece of text AI produces.

belogical is an agent skill for Claude Code and Codex that makes AI answer the way a trained management consultant would: conclusion at the top, support beneath it, unfolding in the order the reader's questions arise. It distills Barbara Minto's *Pyramid Principle* — the bible of the management consulting industry — into rules an LLM can follow.

Invoke `/belogical|$belogical` to write documents, draw conclusions from unsorted material, check the logic of existing text, or compress a finished source into a summary read in its place. It works in casual conversation, too.

I hope this skill helps many people get more out of their reading time. For questions, reach me at 0youngjin.kim@gmail.com.

## Requirements

[Claude Code](https://code.claude.com/docs) (any version that supports skills and plugins) or [Codex CLI](https://developers.openai.com/codex/cli) (any version that supports Agent Skills).

## Installation

Two ways on each tool — the installer route is recommended.

### Claude Code, option 1 — plugin marketplace (recommended)

Two commands in Claude Code and you're done.

```
/plugin marketplace add 0youngjinkim/belogical
/plugin install belogical@belogical
```

Once installed, invoke it with `/belogical`. To update later, run `/plugin marketplace update belogical`.

### Claude Code, option 2 — manual copy

Copy the `skills/belogical/` directory into one of the locations below. Principles, router, and modules live in one folder, so this single copy is all it takes.

- `~/.claude/skills/` — global; `/belogical` works in every project.
- `<project>/.claude/skills/` — that project only.

### Codex, option 1 — skill installer (recommended)

Run `$skill-installer` in Codex and ask it to install from this repo:

```
$skill-installer install from repo 0youngjinkim/belogical, path skills/belogical
```

Restart Codex, then invoke it with `$belogical`.

### Codex, option 2 — manual copy

Copy the `skills/belogical/` directory into one of the locations below, then invoke it with `$belogical`.

- `~/.codex/skills/` — global; `$belogical` works in every project.
- `<project>/.codex/skills/` — that project only.

The bundled `agents/openai.yaml` keeps the skill explicit-invocation only on Codex — it never injects itself into ordinary requests.

## Usage

Invoke `/belogical` directly (on Codex, replace `/belogical` with `$belogical` throughout — routes pass the same way). Call it bare and the router classifies the request into one of five routes; name a route as the argument to go straight there.

- `/belogical` — classify the request and route to answer, document, organize, repair, or summarize
- `/belogical document` — standalone document writing (SCQA introduction + pyramid building + page layout)
- `/belogical organize` — draw a conclusion from unsorted material and ideas (bottom-up + logic tree)
- `/belogical repair` — diagnose and repair existing text (extract → diagnose → rearrange)
- `/belogical summarize` — compress a finished source into a summary read in its place (selection against your question; map-reduce for oversized or multi-document sources)

## Two ways to apply it

There are two ways to apply the principles, and they can be combined.

- **On invocation (default)**: calling `/belogical` loads the principles and routing together. The skill is explicit-invocation only (`disable-model-invocation` in the frontmatter; `agents/openai.yaml` on Codex), so it fires only when you type it and never injects itself into ordinary requests like "write me a report".
- **Ambient (optional)**: to apply the principles to every conversation without invoking the skill, copy only the 'Governing principles' section between the `BELOGICAL:PRINCIPLES` markers in `skills/belogical/SKILL.md` into your global (`~/.claude/CLAUDE.md`) or project CLAUDE.md — on Codex, into `~/.codex/AGENTS.md` or the project AGENTS.md. The source of truth stays in one place; when it changes, update only your pasted copy.

## What's inside

One set of principles and seven methodologies.

| File | Role |
|---|---|
| `skills/belogical/SKILL.md` | Governing principles + router — applies the principles, classifies the request, and points to the right methodology module |
| `skills/belogical/references/` | Seven methodology modules — loaded only on their route |

The principles and the router live in the single SKILL.md. Invoking the skill loads that file whole, so the principles apply first and only the module the request needs is added on top.

```
belogical/
├── README.md
├── README-ko.md
├── LICENSE
├── .claude-plugin/
│   ├── marketplace.json   # plugin marketplace catalog
│   └── plugin.json        # plugin manifest
└── skills/
    └── belogical/
        ├── SKILL.md                # Governing principles (marked section, paste-ready for ambient use) + router: classify → load module → common gate
        ├── agents/
        │   └── openai.yaml         # Codex metadata — keeps the skill explicit-invocation only
        └── references/
            ├── build-pyramid.md    # Setting the apex — five top-down questions / three bottom-up steps
            ├── scqa-intro.md       # Introduction design — SCQA, order variants, skeletons by document type
            ├── grouping-order.md   # Grouping and checking — three rules, deduction vs induction, MECE, summaries
            ├── page-delivery.md    # Page and screen delivery — the 30-second rule, headings, presentations
            ├── thinking-tools.md   # Thinking tools — problem definition, structuring relationships (logic trees)
            ├── repair-text.md      # Repairing existing text — extraction, diagnosis, rearrangement
            └── exec-summary.md     # Summarizing a finished source — re-aimed apex, extraction contract, drill-down
```

## Source

Barbara Minto, *The Minto Pyramid Principle*. The methodology's vocabulary and concepts follow the original, but no original text is reproduced — everything is distilled into core principles. The numeric thresholds the original gives (4–5 items per group, 30 seconds) are treated as recommended defaults, not absolute rules.

## License

MIT — use, modify, and redistribute freely. The methodology is not itself copyrightable; *The Minto Pyramid Principle* book and its text are copyright Barbara Minto. This repository's MIT license covers only the skill files.
