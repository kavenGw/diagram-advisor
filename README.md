# diagram-advisor

[中文](README_CN.md)

An agent skill that decides **which diagram to draw** before drawing it. It analyzes the question you want a diagram to answer, recommends 2–4 candidate diagram types with trade-offs, waits for your choice, then hands off to [drawio-skill](https://github.com/Agents365-ai/drawio-skill) to produce an editable `.drawio` file.

## Requirements

- **[drawio-skill](https://github.com/Agents365-ai/drawio-skill)** — does the actual drawing. Install it first by following its README.
- **[draw.io desktop](https://www.drawio.com/)** — needed by drawio-skill for exports and some layout features.

Without drawio-skill, diagram-advisor still analyzes and recommends, then stops and asks where drawio-skill is installed.

## Install

```bash
npx skills add kavenGw/diagram-advisor -g
```

Manual install (Claude Code):

```bash
git clone https://github.com/kavenGw/diagram-advisor.git ~/src/diagram-advisor
mkdir -p ~/.claude/skills
ln -s ~/src/diagram-advisor/skills/diagram-advisor ~/.claude/skills/diagram-advisor
```

On Windows (`ln -s` in Git Bash copies instead of linking), use a junction from `cmd`:

```bat
mklink /J "%USERPROFILE%\.claude\skills\diagram-advisor" "%USERPROFILE%\src\diagram-advisor\skills\diagram-advisor"
```

For Codex, link the same folder into `~/.agents/skills/diagram-advisor`. `SKILL.md` must end up at `<skills root>/diagram-advisor/SKILL.md`.

## Usage

> Use diagram-advisor to help me explain how our login flow handles token refresh.

1. **Analyze** — the core question, audience, scope, key objects and relations; facts vs. assumptions.
2. **Recommend** — a short table of candidate diagram types, with one marked as recommended.
3. **Draw** — after you pick, it reads drawio-skill's `SKILL.md` and follows its drawing and validation workflow.

It replies in the language you use.

## Note on drawio-skill invocation

drawio-skill declares `disable-model-invocation: true`, so the model cannot call it through the Skill tool. diagram-advisor therefore locates and reads drawio-skill's `SKILL.md` directly at hand-off. This is intentional.

## License

MIT
