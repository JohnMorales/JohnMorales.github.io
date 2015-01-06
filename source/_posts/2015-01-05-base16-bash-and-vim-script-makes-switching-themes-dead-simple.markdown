---
layout: post
title: "base16 bash and vim script makes switching themes dead simple"
date: 2015-01-05 19:42:58 -0500
comments: true
categories: bash vim base16
---

I've been using base16 as my terminal colorscheme for a while now. I've been pleased with the results. 
It's a great looking set of themes that seems to work well in the shell and in vim. 
One of the issues that I've had is switching colorschemes mid-session. 

## Dark themes + shitty projectors == :(

Typically I use a dark theme, but when I have do an ad-hoc presentation or someone comes over to pair program, it's easier on the eyes to use a light theme.

## Attempt 1 iTerm Profiles + Environment variables

Intially I created dedicated iterm profiles so that I can import the correct colorscheme which would set the 16 ansi colors to the exact color. 
The solution roughly consisted of the following:
1. Manually Create a new iterm profile titled with the name of the base16 theme I wanted to use. e.g. `base16-default.dark`
1. Manually update my bashrc to include logic to source the right iterm-shell init script
  - The bashrc would also tell tmux to source the right color schemes.
1. Manually update my vimrc to set the right colorscheme and background accordingly
While this worked for the most part, it required creating a new iterm and was pretty kludgy overall.

## Environment variables + Tmux == :( 
The biggest problem was that switching profiles wouldn't change the ITERM_PROFILE environment variable in tmux. Since tmux is a client/server app

## Attempt 2 (Current solution) auto-generated bash functions

I created a `profiler_helper.sh` that will automatically create `base16_{theme}_{dark|light}` functions that will quickly switch to that theme.
in addition the functions will create `~/.vimrc_base16` and `~/.base16_theme` files. These files allow the following:
  - the vimrc_base16 file will configure vim to use the latest use base16 profile. 
