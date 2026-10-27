# ⌨️ Tmux Cheat Sheet

Welcome to your ultimate quick-reference guide for Tmux commands and shortcuts!

---

## ⚡ Quick Cheats
* **Create a new horizontal pane:** `ctrl + b + "` 🪟
* **Create a new vertical pane:** `ctrl + b + %` 🪟
* **Switch between panes:** `ctrl + b + <arrow keys>` ↔️
* **Shut a pane:** `ctrl + d` ❌

---

## 📂 Session Management
* `tmux ls` (or `tmux list-sessions`) — List all active sessions 📋
* `tmux new -s session-name` — Create a new named session ✨
* `Ctrl-b d` — Detach from the current session 🔌
* `tmux attach -t [session name]` — Attach to an existing session 🔗
* `tmux kill-session -t session-name` — Terminate a session 🗑️

---

## 🪟 Window Management
* `Ctrl-b c` — Create a new window ➕
* `Ctrl-b d` — Detach current client 🔌
* `Ctrl-b n` — Move to the next window ➡️
* `Ctrl-b p` — Move to the previous window ⬅️
* `Ctrl-b l` — Move to the previously selected window ↩️
* `Ctrl-b w` — List all windows / window numbers 📑
* `Ctrl-b 0-9` — Move to the specified window number 🔢
* `Ctrl-b &` — Kill the current window ❌
* `Ctrl-b ,` — Rename the current window ✏️
* `Ctrl-b ?` — List all keybindings ❓

---

## 📐 Tiling & Pane Commands
* `Ctrl-b %` — Split the window vertically 🪟
* `Ctrl-b "` — Split window horizontally 🪟
* `Ctrl-b o` — Switch to the next pane 🔄
* `Ctrl-b q` — Show pane numbers (press the number to jump) 🔢
* `Ctrl-b {` — Move the current pane left ◀️
* `Ctrl-b }` — Move the current pane right ▶️
* `Ctrl-b : "break-pane"` — Extract a pane into its own separate window 🚀

---

## ⚙️ Configuration (`~/.tmux.conf`)
Add these lines to your configuration file for intuitive split shortcuts:

```tmux
bind | split-window -h
bind - split-window -v