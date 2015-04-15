---
layout: post
title: tmux丢失或显示vim的配色
date: 2012-11-02
comments: true
categories:
- tmux
- vim
---

使用tmux，同时使用vim，发现配色总是和别人截图有差别
在.tmux.conf内设置了
```
set -g default-terminal "screen-256color"
```
还是木有作用，最后在SO上找到了解决的办法
在.bashrc内(我是在.zshrc内)添加
```
alias tmux='tmux -2'
```
就OK了

参见

[http://vim.wikia.com/wiki/256_colors_setup_for_console_Vim](http://vim.wikia.com/wiki/256_colors_setup_for_console_Vim)
[http://stackoverflow.com/questions/10158508/lose-vim-colorscheme-in-tmux-mode](http://stackoverflow.com/questions/10158508/lose-vim-colorscheme-in-tmux-mode)
