---
layout: post
title: "base16 shell tmux vim color switching dead simple"
date: 2015-01-09 08:10:20 -0500
comments: true
categories: 
---

I've been using base16 as my terminal color scheme for a while now, I used to
use solarized. I've been pleased with the results.  Over all the base 16 suite
is a great looking set of themes that works well in the shell and in vim.
[Chris](https://github.com/chriskempson) has done a great job on it.

One of the issues that I've had is my setup was theme specific, meaning after I
chose a theme, I was committed and switching colorschemes mid-coding session was
painful. There were ad-hoc times where the visibility of a light theme was
crucial to taking pride of my environment. Basically: 

## Dark themes + shitty projectors == :(

Typically I use a dark theme, but when I have do an ad-hoc presentation or
someone comes over to pair program, it's easier on the eyes to use a light
theme.

## Attempt 1: iTerm Profiles + Environment variables

Intially I created dedicated iTerm profiles so that I can
[__import__](https://github.com/chriskempson/base16-iterm2) the correct
colorscheme which would set the 16 ansi colors to the exact color. I had my
`.bashrc` and `.vimrc` check the __ITERM_PROFILE__ setting provided by iTerm to set the
proper themes in tmux and vim. The
solution roughly consisted of the following:

1. Manually Create a new iTerm profile titled with the name of the base16 theme
   I wanted to use. e.g. `base16-default.dark`
1. Manually update my bashrc to include logic to source the right iterm-shell
   init script. The bashrc would also tell tmux to source the right color
   schemes.
1. Manually update my vimrc to set the right colorscheme and background
   accordingly

While this worked for the most part, it required creating a new iTerm and was
pretty kludgy overall.


The __biggest problem__ was that switching profiles wouldn't change the
ITERM_PROFILE environment variable in tmux. Since tmux is a client/server app
it would hold on to the ITERM_PROFILE that was initially used when the tmux
server was created. Therefore creating new tmux shells would have the original
theme not the latest.

## Attempt 2: (Current solution) auto-generated bash functions

I created a `profiler_helper.sh` that will automatically create
`base16_{theme}_{dark|light}` functions that will quickly switch to that theme.
in addition the functions will create `~/.vimrc_background` and `~/.base16_theme`
files. These files allow the following:

  - the `.vimrc_background` file will configure vim to use the latest use base16 profile. 
  - the `.base16_theme` is a soft link to the latest activated theme so that it
    can be sourced newly created shell

### In action

{% img https://s3.amazonaws.com/johnmorales_blog/base16_profile_helpers.gif %}

### Super quick setup:

Until I convince [Chris](https://github.com/chriskempson) to include this in his project, clone my fork

```
$ git clone https://github.com/JohnMorales/base16-shell
```

Add the following to your bashrc _(change the location to match where you've cloned the base-16 shell)_:

```
if [ -n "$PS1" ]; then # if statement guards adding these helpers for non-interative shells
  eval "$(~/Development/base-16/shell/profile_helper.sh)"
fi
```

Add the following to your vimrc:

```
if filereadable(expand("~/.vimrc_background"))
  let base16colorspace=256
  source ~/.vimrc_background
endif
```

### Usage

In new shells, use the bash functions to change the color scheme:

```
$ base16_default_dark
```

Quick and painless color switching, Enjoy.

