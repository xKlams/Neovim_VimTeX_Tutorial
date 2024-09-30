# TeX_Notes_Setup
A brief tutorial to set up Neovim, Vimtex, and other useful plugins for faster note-taking.

# Warning
All these steps were performed in Fedora Workstation 39.
I have mainly taken inspiration from [this](https://castel.dev/post/lecture-notes-1/) blog that i read a while back.

# Tutorial Start
First we'll install Neovim
fedora:

      sudo dnf update && sudo dnf install neovim

arch:

      sudo pacman -Sy install neovim

Also install Neovim Python module:

    pip3 install --user neovim

Next, create a directory to store your Neovim plugins:

      mkdir ~/.config/nvim

Install Vim-plug plugin manager:

      curl -fLo ~/.local/share/nvim/site/autoload/plug.vim --create-dirs https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim

Edit your config file:

      vim ~/.config/nvim/init.vim

Add the following lines:

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

This will add all the necessary plugins and enable spell-checking (change "it" to your preferred language).

Open Neovim

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
Now you can add your favorite snippets to the tex.snippets file. Simply use this command in Neovim:

      :UltiSnipsEdit

This will open the tex.snippets file inside of our nvim terminal.

I will now add all of the snippets inside the tex.snippets file that I use, feel free to add your favourites to your .snippets file. Many are from [this](https://castel.dev/post/lecture-notes-1/) blog.

```
snippet newfile "New file"
\documentclass[12px]{article}

\title{$1}
\date{`date +%F`}
\author{xKlams}

\input{./setup.tex}

\begin{document}
	\maketitle
	\newpage
	\section{$2}
	$0
\end{document}
endsnippet

snippet today "Date"
`date +%F`
endsnippet

snippet \l "lambda"
\lambda
endsnippet

snippet beg "begin"
\begin{$1}
	$0
\end{$1}
endsnippet

snippet dm "Math" wA
\[
$1
.\] $0
endsnippet

snippet '([A-Za-z])(\d)' "auto subscript" wrA
`!p snip.rv = match.group(1)`_`!p snip.rv = match.group(2)`
endsnippet

snippet '([A-Za-z])_(\d\d)' "auto subscript2" wrA
`!p snip.rv = match.group(1)`_{`!p snip.rv = match.group(2)`}
endsnippet

snippet vec "vector" wA
\overrightarrow{$1}
endsnippet

snippet matrix "matrix"
\begin{pNiceArray}{$1}
	$2
\end{pNiceArray} $0
endsnippet

snippet cap "cap"
\cap
endsnippet

snippet Sigma "Sigma"
\Sigma
endsnippet

snippet mk "Math" wA
$${1}$`!p
if t[2] and t[2][0] not in [',', '.', '?', '-', ' ']:
    snip.rv = ' '
else:
    snip.rv = ''
`$2
endsnippet

snippet => "Rightarrow"
\Rightarrow $1
endsnippet

snippet <=> "If and only" wA
\Leftrightarrow
endsnippet

snippet sum "Somma" wA
\sum^n_{i=1}
endsnippet

snippet -> "freccia" wA
\rightarrow
endsnippet

snippet phi "phi" 
\varphi
endsnippet

snippet bold "bold_text" 
\textbf{$1}$0
endsnippet

snippet epsilon "varepsilon" 
\varepsilon
endsnippet

snippet K "goodK"
\mathbb{K}
endsnippet

snippet scalar "prodotto scalare" 
\langle $1, $2 \rangle $0
endsnippet

snippet canonic "base canonica"
\{e_1,\ldots,e_n\}
endsnippet

```

# Create a new .tex file

The "newfile" snippet initializes a new .tex file by creating the document class and setting up the main features. It includes the following line:

	input{./setup.tex}

The content of this file is just a bunch of includes of different packages and many custom environments. Feel free to change it as you like.

# Install LaTeX package (fedora)

To install a package just use:

	sudo dnf install 'tex(example.cls)' 
	sudo dnf install 'tex(example.sty)'

To install all the packages in the setup.tex file you can run:

	sudo dnf install 'tex(amsmath.sty)' 'tex(amsthm.sty)' 'tex(mdframed.sty)' 'tex(amssymb.sty)' 'tex(nicematrix.sty)' 'tex(amsfonts.sty)' 'tex(tcolorbox.sty)' 'tex(xcolor.sty)' 'tex(cancel.sty)' 'tex(graphicx.sty)' 'tex(rotating.sty)' 'tex(color.sty)' 'tex(soul.sty)' 'tex(imakeidx.sty)' 'tex(wrapfig.sty)' 'tex(blindtext.sty)' 'tex(tikz.sty)' 'tex(hyperref.sty)' 'tex(mathrsfs.sty)' 'tex(unicode-math.sty)' 'tex(euscript.sty)'

 Also install the core LaTeX system:
 
 	sudo dnf install texlive-scheme-basic

# Have fun!
