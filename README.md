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

This will add all the necessary plugin and spelling correction (change "it" with your preferred language)
