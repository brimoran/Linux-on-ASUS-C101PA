# Linux-on-ASUS-C101PA
Setting up Linux on a dinky Chromebook.

## Aims

The Asus C101PA ia a highly portable 10.1 inch Chromebook that is ideal to take on trips.

I love the form factor of this machine but unfortunately the hard drive is only 16 GB so space is at a premium.  We will therefore have to be very careful about what we install.

My minimal needs are to have working installs of R and LaTeX to enable me to finish off documents on the go... but we'll see what else we can get away with.

## What comes with the standard Linux container?

After creating the Linux container I have 7.1 GB available according to the Files app.

To see what we are dealing with here:

```lsb_release -da```

It's Debian stretch 9.5.

```apt list --installed```

will show us what we already have installed.  Most notably (for me) we already have Vim and Python 3.  I'll be using Vim to edit code and all my text editing.

## Install stuff that R packages need

```sudo apt-get install curl libcurl4-openssl-dev libxml2-dev libssl-dev libgdal-dev libproj-dev xorg libx11-dev libglu1-mesa-dev r-cran-rgl```

I now have 5.5 GB available, with Linux comprising 2.9 GB.

```sudo apt-get update```

```sudo apt-get install r-base```

## Install useful R packages

Enter R as a superuser in interactive mode:

```sudo -i R```

Let's install the packages we need in one command:

```install.packages(c("ggplot2","knitr","ggthemes","scales","ggmap","plotly","ggfortify","leaflet","leaflet.extras","rgdal","forecast","treemapify","dbscan","survival","googleVis","rmarkdown","flexdashboard","highcharter","devtools","maptools","treemap","networkD3","visNetwork","DiagrammeR","DT"))```

This will take a while (...an hour or so) as there is a lot to compile.

Not bad, just three packages from my normal setup don't work:

- prophet
- arules
- tidyverse

```q()``` to exit R

## Install LaTeX

A full install of LaTeX is very large so we will start with the smallest possible install and then add in the fonts and packages needed.

Let's start with [TinyTex](https://yihui.name/tinytex/):

First we need ```wget``` so:

```sudo apt-get install wget``` and then:

```
wget -qO- "https://yihui.name/gh/tinytex/tools/install-unx.sh" \
  | sh -s - --admin --no-path
```


Add the install location to the path to enable us to use ```pdflatex``` from anywhere in the terminal:

```sudo ~/.TinyTeX/bin/*/tlmgr path add```

Now we have 4.7 GB left to play with.  The size of the Linux container is 3.5 GB.

Now to add extra packages I need using ```tlmgr install```:

```tlmgr install subfiles isodate substr enumitem datatool xfor fp pdfpages csquotes microtype hyphenat xcolor fancyhdr lastpage fira mweights fontaxes wrapfig capt-of mdframed needspace tcolorbox pgf environ trimspaces titlesec titlecaps ifnextok floatrow placeins adjustbox collectbox lcg relsize lineno```

Now we have 4.7 GB left to play with.  The size of the Linux container is 3.6 GB... um that's weird but never mind!

## Additional goodies

### Pandoc

A command line tool to convert between document types.  The version in Debian stretch is unfortunately very old.  As the C101 is an ARM chromebook we would need to compile the newer version which I think requires a (1GB +) Haskell install.  So in the meantime:

```sudo apt-get install pandoc```

And ```pandoc --version``` confirms that the version is 1.17.2.

### Zathura

It's a bit of a pain having to flip back and forth to a browser to view compiled pdfs.  I prefer to use Zathura from the terminal or Vim, especially because it uses Vim key bindings.

```sudo apt-get install zathura```

### Gimp

I need to edit graphics so:

```sudo apt-get install gimp```

### Libre Office

602 MB really just for Calc...

```sudo apt-get install libreoffice```

## Fine tuning

### Customising Vim

I like the hybrid material colour scheme so let's set that up and a few other things.

Let's install VimPlug:

```
curl -fLo ~/.vim/autoload/plug.vim --create-dirs \
    https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
```

Then create .vimrc file:

```cd```
```vim .vimrc```

Add the following into the file:

```
set number
syntax on

call plug#begin()

       Plug 'flazz/vim-colorschemes'
       
 call plug#end()

set background=dark
colorscheme hybrid_material

:setlocal spell spelllang=en_gb
```
And then from within Vim type:

```:source %``` and then
```:PlugInstall```

Let Vim do its stuff.
