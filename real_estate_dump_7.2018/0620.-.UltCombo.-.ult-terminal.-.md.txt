# ult-terminal

UltCombo's Atom terminal. Forked from terminal-status.

# Features

Here is a quick overview of the features:

- Command history
- Clickable file paths and URLs
- Multiple terminals
- Preserve screen real estate

See the details below.

# Command history

Press up/down to navigate the command history.

Type the beginning of a command and press up to search the command history. For instance, type `pm2 deploy` and press up to get the most recent command beginning with `pm2 deploy` (e.g. `pm2 deploy ecosystem.json stage`), press up again to get older results that match the initial search (e.g. `pm2 deploy ecosystem.json production`).

Start a command with a space in case you don't want to store it in the command history.

# Clickable file paths and URLs

URLs and email addresses are clickable and open in the default browser or application.

Absolute file paths that point to inside of the working directory are also clickable and open in Atom.

# Multiple terminals

You can open multiple terminals and switch between them through the status bar or key bindings.

# Preserve screen real estate

Most developers have wide monitors and tend to limit line lengths in order to keep code optimally readable. Therefore, ult-terminal opens in a panel in the right side of your workspace taking advantage of the unused space instead of consuming your screen's precious vertical real estate.

You can set the width of the terminal panel to a fixed pixel size in the package settings, or you may also edit your stylesheet to perform more advanced customizations.

# Default keymap

- `shift-enter`: Show/hide current terminal
- `cmd-shift-e` / `alt-shift-t`: Open new terminal
- `cmd-shift-j` / `alt-shift-j`: Open next terminal
- `cmd-shift-k` / `alt-shift-k`: Open prev terminal
- `cmd-shift-x` / `alt-shift-x`: Destroy current terminal

All key bindings are available for remapping.

# Known limitations

- Can't write to stdin using the terminal emulator.

# Protip

Check out the package settings for customizations and tips! :smiley:
