---
layout: post
title: "OSX 上默认 VIM 不支持 + 寄存器"
date: 2012-11-26 21:48
comments: true
categories: 
- vim
- OSX
- Mac
---
OSX 上默认 VIM 不支持 + 寄存器，所以从系统剪贴板相互复制东西就麻烦了
所以,我重新装了一下vim

```bash
brew install vim
```
然后
```bash
which vim
```
发现还是 /usr/bin

则，在 .zshrc内 把 /usr/local/bin 加入 PATH 就 ok 了
其实后来想想，把原来的 move 到 old 上去，将 /usr/bin/vim ln 到/usr/local/vim 就 OK 了
或者 
```bash
brew install macvim --HEAD --override-system-vim
```
来安装 macvim 并覆盖系统原来的vim
