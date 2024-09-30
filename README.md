# TeX_Notes_Setup
A brief tutorial to setup Neovim Vimtex and other useful plugins to take notes faster.

# Warning
All these steps are performed in Fedora Workstation 39.
I have mainly taken inspiration from [this](https://castel.dev/post/lecture-notes-1/) blog that i read a while back.

# Tutorial Start
First thing first we will need to install neovim.
fedora:

      sudo dnf update && sudo dnf install neovim

arch:

      sudo pacman -Sy install neovim

Also install neovim python module

    pip3 install --user neovim

Create the directory to store all the nvim plugins

      mkdir ~/.config/nvim

Install Vim-plug plugin manager

      curl -fLo ~/.local/share/nvim/site/autoload/plug.vim --create-dirs https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim

Edit your config file

      vim ~/.config/nvim/init.vim

Add the following lines

      setlocal spell
      set spelllang=en,it
      inoremap <C-l> <c-g>u<Esc>[s1z=`]a<c-g>u

      call plug#begin()
      Plug 'SirVer/ultisnips'
      let g:UltiSnipsExpandTrigger = '<tab>'
      let g:UltiSnipsJumpForwardTrigger = '<tab>'
      let g:UltiSnipsJumpBackwardTrigger = '<s-tab>'
      
      Plug 'lervag/vimtex'
      call plug#end()
      
      let g:vimtex_view_method='zathura'
      let g:vimtex_quickfix_mode=0

This will add all the necessary plugin and spelling correction (change "it" with your preferred language).

Open neovim

      nvim

It will now prompt you to install different languages pack for the spelling checker.
Inside nvim:

      :PlugInstall
      :UpdateRemotePlugins
      :q!
      :q!

Now we need to install zathura, a file visualizer, zathura-pdf-popplerm, the plugin for PDFs, and latexmk.

      sudo dnf install zathura zathura-pdf-poppler latexmk

Now we need to create a directory to store all our .snippets file for the UltiSnips plugin.

      mkdir .config/nvim/UltiSnips

Now we are all setup!

# What to do now?
Now we are free to add all of our favourite snippets to our tex.snippets file, to do so we just have to use the following commadn inside nvim

      :UltiSnipsEdit

This will open the tex.snippets file inside of our nvim terminal.

I will now add all of the snippets inside the tex.snippets file that I use, feel free to add your favourites to your .snippets file. Many are from [this](https://castel.dev/post/lecture-notes-1/) blog.

# add snippets

# setup.tex file

If you have noticed the "newfile" snippets 
