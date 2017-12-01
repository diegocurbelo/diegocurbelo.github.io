---
layout: post
title:  Vim syntax highlighting for log files
date:   2016-09-14 14:00:00 -0300
categories: vim java logs
---

Edit the file `~/.vimrc` to enable colored syntax and (optionally) disable line wrap:

```vim
syntax on
set nowrap
```

Create the file `~/.vim/filetype.vim`

```vim
if exists("did_load_filetypes")
  finish
endif

augroup filetypedetect
  au! BufRead,BufNewFile *.log,*.log.* setf log
augroup END
```

Create the file `~/.vim/syntax/log.vim`

```vim
if exists("b:current_syntax")
  finish
endif

syn match fatal ".* FATAL .*"
syn match fatal "^FATAL: .*"
syn match error ".* ERROR .*"
syn match error "^ERROR: .*"
syn match warn  ".* WARN .*"
syn match warn  "^WARN: .*"
syn match debug ".* DEBUG .*"
syn match debug "^DEBUG: .*"

syn match error "^java.*Exception.*"
syn match error "^java.*Error.*"
syn match error "^.*Exception"
syn match error "^\tat .*"

hi fatal ctermfg=Red    ctermbg=Black
hi error ctermfg=Red    ctermbg=Black
hi warn  ctermfg=Yellow ctermbg=Black
hi debug ctermfg=Gray   ctermbg=Black

let b:current_syntax = "log"
```
