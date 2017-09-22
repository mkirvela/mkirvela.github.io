---
layout: default
title:  "My tmux & vim setup"
date:   2017-09-21 09:00:00 +0300
categories: tmux vim
---

I've been using `vim` for years. The other day I wanted to try out `tmux`, too. It turned out to be a hassle but now I got my setup (almost) just the way I wanted. I had all kinds of trouble with copy&paste, mouse mode, true colors, etc..


{% highlight bash %}
# Add truecolor support
set -g default-terminal "xterm-256color"
set-option -ga terminal-overrides ",xterm-256color:Tc"
set-window-option -g mode-keys vi
set-option -g pane-border-status top
set-option -g pane-border-format " #P: #{pane_current_command} "
# Smart pane switching with awareness of Vim splits.
# See: https://github.com/christoomey/vim-tmux-navigator
is_vim="ps -o state= -o comm= -t '#{pane_tty}' \
    | grep -iqE '^[^TXZ ]+ +(\\S+\\/)?g?(view|n?vim?x?)(diff)?$'"
    bind-key -n C-h if-shell "$is_vim" "send-keys C-h"  "select-pane -L"
    bind-key -n C-j if-shell "$is_vim" "send-keys C-j"  "select-pane -D"
    bind-key -n C-k if-shell "$is_vim" "send-keys C-k"  "select-pane -U"
    bind-key -n C-l if-shell "$is_vim" "send-keys C-l"  "select-pane -R"
    bind-key -n C-\ if-shell "$is_vim" "send-keys C-\\" "select-pane -l"
    bind-key -T copy-mode-vi C-h select-pane -L
    bind-key -T copy-mode-vi C-j select-pane -D
    bind-key -T copy-mode-vi C-k select-pane -U
    bind-key -T copy-mode-vi C-l select-pane -R
    bind-key -T copy-mode-vi C-\ select-pane -l
    bind-key -T copy-mode-vi 'v' send-keys -X begin-selection
    bind-key -T copy-mode-vi 'y' send-keys -X copy-selection
# List of plugins
bind-key -T copy-mode-vi 'v' send -X begin-selection
bind-key -T copy-mode-vi 'y' send -X copy-selection
set -g @plugin 'tmux-plugins/tpm'
set -g @plugin 'tmux-plugins/tmux-sensible'
set -g @plugin 'seebi/tmux-colors-solarized'
set -g @plugin 'robhurring/tmux-spotify'
set -g mouse on
bind-key -T copy-mode-vi MouseDragEnd1Pane send -X copy-pipe-and-cancel "pbcopy"
bind-key -T copy-mode MouseDragEnd1Pane send -X copy-pipe-and-cancel "pbcopy"
set -g status-right "♫ #{spotify_status} #{spotify_artist}: #{spotify_track} | %a %h-%d %H:%M "
# bind-key -T copy-mode-vi MouseDragEnd1Pane send -X copy-pipe-and-cancel "pbcopy"
# bind-key -T copy-mode MouseDragEnd1Pane send -X copy-pipe-and-cancel "pbcopy"
# setw -g mode-keys vi
# Other examples:
# set -g @plugin 'github_username/plugin_name'
# set -g @plugin 'git@github.com/user/plugin'
# set -g @plugin 'git@bitbucket.com/user/plugin'
set-window-option -g window-status-current-bg red
set-option -g pane-active-border-fg blue
# set-window-option -g window-status-current-bg yellow
# Initialize TMUX plugin manager (keep this line at the very bottom of tmux.conf)
run '~/.tmux/plugins/tpm/tpm'
end
{% endhighlight %}
