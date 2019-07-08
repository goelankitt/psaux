---
title: "Vim Setup"
date: 2019-07-08T20:47:33+05:30
draft: true
---

# Setting up vim for golang on Ubuntu 18.04

I spent a month finding the perfect vim setup for golang. I struggled with pathogen and janus vim to realize that they were not what I was looking for. So here is the cleanest and easiest way to setup vim for golang.

### Step 1: Install vim and curl.

    sudo apt install vim curl

### Step 2: Generate .vimrc

Use [vim-bootstrap](http://vim-bootstrap.com/) to generate a .vimrc. Open the website, select go and click on the Generate button. This downloads a file called generate.vim.

Copy this file to your home directory and rename it to .vimrc

Open vim, it will prompt you to press enter. Then it will install a bunch of plugins(this could take some time). When it’s done, restart vim.

And that’s it you are done.

If you want to make any changes to the generated .vimrc then a clean way of doing so is making all those changes is ~/.vimrc.local file and those setting will automatically be loaded in vim. I am happy with all default settings except for cursor style in insert mode.

### (Optional) Change cursor style for insert mode

Save the following snippet of code in ~/.vimrc.local
```
" Fix the cursor in vim
if has("autocmd")
  au VimEnter,InsertLeave * silent execute '!echo -ne "\e[1 q"' | redraw!
  au InsertEnter,InsertChange *
    \ if v:insertmode == 'i' |
    \   silent execute '!echo -ne "\e[5 q"' | redraw! |
    \ elseif v:insertmode == 'r' |
    \   silent execute '!echo -ne "\e[3 q"' | redraw! |
    \ endif
  au VimLeave * silent execute '!echo -ne "\e[ q"' | redraw!
endif
```

### (Optional) Fix for the disappearing cursor on lines with errors

My cursor kept disappearing when it was on any line that had an error. It jumped to the status line in the bottom. This was really frustrating and the fix for this was updating vim because it’s a bug in some vim version.

    sudo apt-get update
    sudo add-apt-repository ppa:jonathonf/vim
    sudo apt-get install vim
