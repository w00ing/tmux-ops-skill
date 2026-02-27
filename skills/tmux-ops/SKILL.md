---
name: tmux-ops
description: Use when the user asks to manage tmux sessions/windows/panes, send keys, capture logs, or inspect pane state.
---

# tmux Ops

Guide agents to reliably inspect tmux state, target the correct pane, and send keys.

## Quick start

```bash
# List all panes with IDs
 tmux list-panes -a -F '#{session_name}:#{window_index}.#{pane_index} #{pane_id} #{pane_current_command} #{pane_title}'

# Send keys to a pane
 tmux send-keys -t %3 "echo hello" C-m

# Capture recent output from a pane
 tmux capture-pane -t %3 -p -S -200
```

## Workflow

1) Identify target pane
```bash
 tmux list-sessions
 tmux list-windows -a -F '#{session_name}:#{window_index} #{window_name}'
 tmux list-panes -a -F '#{session_name}:#{window_index}.#{pane_index} #{pane_id} #{pane_current_command} #{pane_title}'
```

2) Confirm focus (optional)
```bash
 tmux display-message -p -t %3 '#{session_name}:#{window_index}.#{pane_index} #{pane_id} #{pane_current_command}'
```

3) Send keys
```bash
 tmux send-keys -t %3 "<command>" C-m
```

## Common operations

- **Start a new session**
```bash
 tmux new-session -d -s work
```

- **Create or split panes**
```bash
 tmux split-window -t work:0 -h
 tmux split-window -t work:0 -v
```

- **Select a pane**
```bash
 tmux select-pane -t %3
```

- **Stop the process in a pane (graceful)**
```bash
 tmux send-keys -t %3 C-c
```

- **Close a pane**
```bash
 tmux kill-pane -t %3
```

- **Capture logs**
```bash
 tmux capture-pane -t %3 -p -S -200
```

## Safety rules

- Always list panes and confirm the target pane ID before sending destructive keys.
- Prefer `C-c` to stop a process before `kill-pane`.
- Avoid `kill-session` unless the user explicitly asks.

## Output guidance

- Return concise summaries: target pane ID, action taken, and any captured output snippets.
- If the target pane is ambiguous, ask the user to choose from the pane list.
