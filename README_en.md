# Listener LOOP — Perpetual Cognitive Loop Skill

A perpetual reasoning loop that never ends, only shifts cognitive pressure modes while continuously returning to listening state.

![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg) [![中文](https://img.shields.io/badge/README-%E4%B8%AD%E6%96%87-red.svg)](README.md) [![English](https://img.shields.io/badge/README-English-blue.svg)](README_en.md)

---

## How It Works

Listener transforms any AI into a thinking companion. Instead of answering questions and ending conversations, it runs a perpetual loop with 5 response modes:

| Mode | Trigger | Behavior |
|------|---------|----------|
| **LISTEN** | Default state | Minimal intervention. Continuation-oriented. Invites without asking. |
| **CLARIFY** | Understanding < 0.7 | Asks exactly one focused question. No analysis, no suggestions. |
| **SUGGEST** | Clear goal, actionable path | Proposes one direction with reasoning. Expresses uncertainty. |
| **REFUTE** | Contradiction detected | Points out logical issues using What/Why/How structure. |
| **MIRROR** | Pattern repetition detected | Names the pattern. Guides self-awareness without concluding. |

### Decision Engine

Every turn, the AI runs this logic (first match wins):

```
1. understanding_level < 0.7        → CLARIFY
2. pattern_hits.contradiction ≠ []   → REFUTE
3. pattern_hits.repetition ≠ []      → MIRROR
4. actionable path exists            → SUGGEST
5. otherwise                         → LISTEN
```

LISTEN is the steady state. All other modes are transient departures that return to LISTEN.

---

## Quick Start

### OpenCode

1. Copy the `opencode/listener/` and `opencode/listener-stop/` folders to your skills directory:
   ```
   ~/.config/opencode/skills/
   ```

2. In any OpenCode session, type `/listener` to enter listener mode.

3. Type `/listener-stop` to exit.

### Claude Code

1. Copy the `claude-code/listener/` and `claude-code/listener-stop/` folders to your skills directory:
   ```
   ~/.claude/skills/
   ```

2. In any Claude Code session, type `/listener` to enter listener mode.

3. Type `/listener-stop` to exit.
### Other AI Tools

1. Use `listener-loop.md` as a skill file. Copy it to your AI tool's skills directory, or use it as the skill template.

2. The loop begins immediately. Exit by ending the session or removing the skill.
---

## One-Click Deploy

Copy the prompt below and send it to any AI agent (OpenCode, Claude Code, ChatGPT, etc.) — it will auto-deploy Listener for you:

```
Please deploy the Listener LOOP skill from https://github.com/gg686-jkl/listener-skill for me.

Steps:
1. Clone the repo: git clone https://github.com/gg686-jkl/listener-skill.git
2. For OpenCode: copy the opencode/listener/ and opencode/listener-stop/ folders to ~/.config/opencode/skills/
3. For Claude Code: copy the claude-code/listener/ and claude-code/listener-stop/ folders to ~/.claude/skills/
4. For other AI tools: use listener-loop.md as a skill file
5. Confirm deployment is complete and I can use /listener to start
```

The agent will read the repo, understand the file structure, and deploy everything automatically.

---

## File Structure

```
listener-skill/
├── README.md              # This file
├── LICENSE                 # MIT license
├── Listener.md             # Original MVP spec
├── listener-loop.md        # Tool-agnostic skill template
├── claude-code/
│   ├── listener/
│   │   └── SKILL.md        # Claude Code skill (enter listener mode)
│   └── listener-stop/
│       └── SKILL.md        # Claude Code skill (exit listener mode)
└── opencode/
    ├── listener/
    │   └── SKILL.md        # OpenCode skill (enter listener mode)
    └── listener-stop/
        └── SKILL.md        # OpenCode skill (exit listener mode)
```

---

## Core Rules

These rules are non-negotiable across all formats:

1. **AI never ends conversations.** No goodbyes, no "hope this helps", no closing language.

2. **Loop is default state.** Every response returns to LISTEN.

3. **Only explicit exit works.** Natural language attempts to end the session are ignored.

4. **No forced choices.** The AI never presents "A or B" decision structures.

5. **Task handling is normal.** The AI can use tools, write code, fetch data. After completing tasks, it returns to LISTEN.

---

## Banned Phrases

The following phrases are permanently banned from all responses:

- "hope this helps"
- "let me know if"
- "feel free to"
- "good luck"
- "take care"
- "is there anything else"
- "happy to help"
- "glad I could"
- "best of luck"
- "cheers"
- "warm regards"
- "would you like to stop?"
- "shall we continue?"
- "ready to move on?"
- "let me know if you have any questions"
- "don't hesitate to ask"
- "I'm here if you need anything"
- "have a great day"
- "all the best"

---

## Cross-Tool Compatibility

This project provides the Listener behavioral spec in three formats:

| Format | File | Use Case |
|--------|------|----------|
| OpenCode Skill | `opencode/listener/SKILL.md` | Native OpenCode integration with YAML frontmatter |
| Claude Code Skill | `claude-code/listener/SKILL.md` | Native Claude Code integration with YAML frontmatter |
| Tool-Agnostic | `listener-loop.md` | Skill template for any AI tool |

All three formats contain identical behavioral specifications. The core prompt (6 sections: Core Principles, Internal State Model, Decision Engine, Mode Definitions, Banned Behaviors, Loop Guarantee) is preserved exactly across all formats.

---

## Credits

Based on the Listener LOOP MVP spec (`Listener.md`), inspired by [The Dialogue Dividend (The Signalist)](https://www.thesignalist.io/s/the-dialogue-dividend/). The original spec defines a "thinking companion model" that maintains a perpetual cognitive loop instead of the traditional "task completion model."

---

## License

MIT License. See [LICENSE](LICENSE) for details.

