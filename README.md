# tmux-ops-skill

Tmux operations skill for reliably targeting panes, sending commands, and capturing logs.

[![license](https://img.shields.io/github/license/w00ing/tmux-ops-skill)](https://github.com/w00ing/tmux-ops-skill/blob/main/LICENSE)

## Features

- Identify the right tmux pane safely before sending keys
- Send commands to exact panes with minimal ambiguity
- Capture recent pane output for debugging and status checks
- Follow a consistent, low-risk tmux workflow

## Install

Codex (skill-installer UI):
- Run `$skill-installer`
- Ask: install GitHub repo `w00ing/tmux-ops-skill` path `tmux-ops`

Claude Code (plugin):
- `/plugin marketplace add w00ing/tmux-ops-skill`
- `/plugin install tmux-ops-skill@tmux-ops`

Manual (Codex):
```bash
mkdir -p ~/.codex/skills
git clone https://github.com/w00ing/tmux-ops-skill.git /tmp/tmux-ops-skill
rsync -a /tmp/tmux-ops-skill/skills/tmux-ops/ ~/.codex/skills/tmux-ops/
```

Manual (Claude Code):
```bash
mkdir -p ~/.claude/skills
git clone https://github.com/w00ing/tmux-ops-skill.git /tmp/tmux-ops-skill
rsync -a /tmp/tmux-ops-skill/skills/tmux-ops/ ~/.claude/skills/tmux-ops/
```

## Use

- Skill name: `tmux-ops`
- Skill file: `skills/tmux-ops/SKILL.md`

Examples:
```bash
tmux list-panes -F '#{session_name}:#{window_index}.#{pane_index} #{pane_id} #{pane_current_command} #{pane_title}'
tmux send-keys -t %3 "echo hello" C-m
tmux capture-pane -t %3 -p -S -200
```

## Safety

- Always list panes and verify pane ID before sending destructive keys.
- Prefer `C-c` to stop processes before closing panes.
- Avoid `kill-session` unless explicitly requested.
