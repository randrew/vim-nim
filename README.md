#Nim language support for Vim

This provides [Nim](http://nim-lang.org) language support for Vim:

* Syntax highlighting
* Auto-indent
* Build/jump to errors within Vim
* Project navigation and Jump to Definition (ctags or compiler-assisted
  idetools).

#Installation

## vim-plug
  
1. [Install vim-plug](https://github.com/junegunn/vim-plug#installation)
2. Add `Plug 'kori/vim-nim'

##Final Step
Next you *need to add this* to your `~/.vimrc`:

    fun! JumpToDef()
      if exists("*GotoDefinition_" . &filetype)
        call GotoDefinition_{&filetype}()
      else
        exe "norm! \<C-]>"
      endif
    endf
    
    " Jump to tag
    nn <M-g> :call JumpToDef()<cr>
    ino <M-g> <esc>:call JumpToDef()<cr>i

The `JumpToDef` function hooks the `nim.vim` plugin to invoke the nim
compiler with the appropriate idetools command. Pressing meta+g will then jump
to the definition of the word your cursor is on. This uses the nim compiler
instead of ctags, so it works on any nim file which is compilable without
requiring you to maintain a database file.
