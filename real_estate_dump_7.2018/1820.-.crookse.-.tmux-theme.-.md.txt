# crookse/tmux-theme

These are my configurations for my tmux theme. Take a look at the snapshot below for a visual.

If you're using iTerm2 and want your tmux session names to show up on your iTerm2's tabs, then look at how I've setup `set-titles-string` in `theme.sh`. I hated seeing "Thanks for flying Vim" as well as any other data not relevant to my workflow in my iTerm2's tab titles and decided to do some research (after months of using Vim and tmux) and finally make iTerm2's tab titles reflect the work I'm currently doing in a particular tab. Also, see the iTerm2 Appearance Preferences snapshot below to maximize tab real estate.

## Theme Preview

*Note: Your colors in the preview boxes (bottom half of the screen) may vary. I use `crookse_glacier` from my `vim/vim-crookse` package, so that is where I'm getting my color scheme and syntax highlighting. Also, your prompt variable may vary. See my `.shellrc.sample.load` file in my `dotfiles` repository for my prompt setup.*

![tmux](https://github.com/crookse/tmux-theme/raw/master/tmux_theme_preview_201805241112.png "tmux")

## iTerm2 Appearance Preferences

I love the challenge of saving as much real estate as possible when designing mobile interfaces. When I think about tmux's title string setting and iTerm2's tab titles, I think about how much real estate I can save for each tab. Here are my preferences for iTerm2 that you might like.

![iTerm2 Appearance Preferences](https://github.com/crookse/tmux-theme/raw/master/iterm2_appearance_preferences.png "iTerm2 Appearance Preferences")

Notes:

* I open one tmux session per iTerm2 tab. I like doing this because it allows me to hotkey between tmux sessions faster by looking at iTerm2 tab names instead of pulling up the tmux session list over and over.
* I haven't figured out how to left align tmux's title strings in tabs from a tmux config standpoint. However, I do know that iTerm2's "Show current job name" setting left aligns your tab titles.
* I like my iTerm2 tabs located at the bottom. This allows me to quickly see what tmux sessions I have open and the active window for each session (e.g., `[00] dotfiles -- vim` in Tab #7 tells me that the dotfiles project is open in that tab and the active window is the vim window). I also prefix my tmux session names with numbers for grouping purposes. `[00]` prefix means dotfiles projects, `[20]` prefix means web projects, and `[99]` prefix means system-level management.
* I let iTerm2's tabs stretch to fill the entire bar for maximizing tab real estate.
