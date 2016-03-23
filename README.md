#Nim language support for Vim

This provides [Nim](http://nim-lang.org) language support for Vim:

* Syntax highlighting
* Auto-indent
* Build/jump to errors within Vim
* Project navigation and Jump to Definition (ctags or compiler-assisted
  idetools).

#Installation

##Pathogen

1. [Install pathogen.vim](https://github.com/tpope/vim-pathogen#installation)
2. Install nim.vim as a pathogen bundle

    cd ~/.vim/bundle
    git clone git://github.com/kori/nim-vim

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
  
#Other recomended Vim plugins


#If something goes wrong

Since you are using vim, on source code which might have syntax problems,
invoking an external tool which may have its own share of bugs, sometimes stuff
just doesn't work as expected. In these situations if you want to debug the
issue you can type ``:e log://nim`` and a buffer will open with the log of
the plugin's invocations and nim's idetool answers.

This can give you a hint of where the problem is and allow you to easily
reproduce on the commandline the idetool parameters the vim plugin is
generating so you can prepare a test case for either this plugin or the nim
compiler.
