vimux-r
=============

This is a vim plugin for added R functionality built on top 
of [vimux](https://github.com/benmills/vimux/); thus, it assumes 
that the vimux plugin is installed as well.  Also, it is adapted 
from [vimux-pyutils](https://github.com/julienr/vimux-pyutils), 
but is for R-script code.

There are two main uses:

+ First, it allows a block of visual-mode selected R-script code to be   
sent from vim to a tmux buffer split running R.  

+ Second, "cells" of code can be sent from vim to the R tmux split.  
Regarding this use case, the idea here is to be able to have code block 
execution similiar to that found in the iPython Notebook, though being 
able to stay in the vim editing environment.


Key mappings
-----------
###### example key mappings that can be enabled by placing into .vimrc:

-----------
##### To open the R tmux split: 

`map <Leader>vr :call VimuxR()<CR>`

After the R tmux split is created, these keybindings are made:

* Jump down into the tmux pane in copy(/vim) mode

`<Leader>vi`

* Close the vim tmux split

`<Leader>vq`

* Interrupt any command running in the tmux pane

`<Leader>ve`

-----------
##### To execute current visually selected block of code in the R tmux split: 

`vmap <silent> <Leader>e :python run_visual_code()<CR>` 

-----------
##### To execute the current "cell" in the R tmux split: 

`noremap <silent> <Leader>c :python run_cell(save_position=False, cell_delim='####')<CR>` 

Note, a cell is similar to an iPython Notebook code cell and is defined as a code block 
spanning from one `cell_delim` to the next `cell_delim` (explained below).

Two arguments can be passed into `run_cell`:

* `save_position`: [default `False`]

    If set True, then the cursor will stay at the current location after the code cell 
    is executed.  If False, then the cursor will jump ahead to the beginning of
    the next code cell block.

* `cell_delim`: [default `'####'`]

    Code cells are delimited by the `cell_delim` argument. This specifies what 
    should seperate the code cell blocks.  Note, there should be a `cell_delim` 
    at the beginning of the first code cell, as well as at the end of the last code cell.
