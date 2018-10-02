# Linux-on-ASUS-C101PA
Setting up Linux on a dinky Chromebook.

## Aims

The Asus C101PA is a highly portable 10.1 inch Chromebook that is ideal to take on trips.

I love the form factor of this machine but unfortunately the hard drive is only 16 GB so space is at a premium.  We will therefore have to be very careful about what we install.

My minimal needs are to have working installs of R and LaTeX to enable me to finish off charts and documents on the go... but we'll see what else we can get away with.

## What comes with the standard Linux container?

After creating the Linux container I have 7.1 GB of free space available according to the Files app.

To see what we are dealing with here:

```lsb_release -da```

It's Debian stretch 9.5.

```apt list --installed```

will show us what we already have installed.  Most notably (for me) we already have Vim and Python 3.  I'll be using Vim to edit code and all my text editing - with Python installed arguably I don't really need R but my knowledge of R is much better... so...

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

To be honest tidyverse is the main loss here.

```q()``` to exit R

## Install LaTeX

A full install of LaTeX is very large (c. 5 GB!) so we will start with the smallest possible install and then add in the fonts and packages needed.

Thankfully we can start with [TinyTex](https://yihui.name/tinytex/) and then add to its install:

First we need ```wget``` so:

```sudo apt-get install wget``` and then:

```
wget -qO- "https://yihui.name/gh/tinytex/tools/install-unx.sh" \
  | sh -s - --admin --no-path
```

Add the install location to the path to enable us to use ```pdflatex``` from anywhere in the terminal:

```sudo ~/.TinyTeX/bin/*/tlmgr path add```

Now we have 4.7 GB left to play with.  The size of the Linux container is 3.5 GB.

Now to add the extra packages I need using ```tlmgr install```:

```tlmgr install subfiles isodate substr enumitem datatool xfor fp pdfpages csquotes microtype hyphenat xcolor fancyhdr lastpage fira mweights fontaxes wrapfig capt-of mdframed needspace tcolorbox pgf environ trimspaces titlesec titlecaps ifnextok floatrow placeins adjustbox collectbox lcg relsize lineno```

These are very specific packages I need for the LaTeX templates I have created.  Your mileage **will** vary.

Now we have 4.7 GB left to play with.  The size of the Linux container is 3.6 GB... not sure why the overall space has stayed the same... TinyTex clearly does an excellent job of staying tiny!

## Additional goodies

### Pandoc

A command line tool to convert between document types.  The version available in Debian stretch is unfortunately very old.  As the C101 is an ARM chromebook we would need to compile the newer version which requires a (1GB +) Haskell install.  We might actually have space to do this... but in the meantime we'll make do with the older version:

```sudo apt-get install pandoc```

And ```pandoc --version``` confirms that the version is 1.17.2.

### Zathura

It's a bit of a pain having to flip back and forth to a browser to view compiled pdfs.  I prefer to use Zathura from the terminal or from Vim, especially because it uses Vim key bindings.

```sudo apt-get install zathura```

### Gimp

I need to edit graphics so:

```sudo apt-get install gimp```

### Libre Office

A 602 MB install really just so I have a reliable Excel alternative that I probably don't need...

```sudo apt-get install libreoffice```

### SQLite

To do

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

**Assuming you are comfortable with Vim**, edit the file using Vim:

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

## Concluding thoughts

We now have a little machine with:

- Vim for document writing and scripting
- R for analysis and producing top notch charts
- LaTeX to create beautiful documents
- Pandoc to convert between document types
- Zathura as a light weight pdf viewer
- Gimp as a powerful graphics editor
- Libre Office providing a full office suite

Add this to what the C101PA offers through ChromeOs and Android and we are very close to having the perfect little machine for my needs... There are just two things missing:

### RStudio

I'd like to figure out if I can get an RStudio server running on the machine.  It would be great to be able to use RStudio through the Chromebook browser.

### KeyNote

I love KeyNote on MacOS.  It's what made me start to use Macs and it's kept me using them.  No other presentation software comes close in my opinion.

For a while I was interested enough by [reveal.js](https://revealjs.com/#/) to create my own templates and delivered a few presentations through it.  Unfortunately though it is too clunky to use and to share with others.

KeyNote itself is still just a little too awkward to use in a browser.

If Linux were to ever get a good KeyNote alternative I'd happily jump to a Linux enabled Chromebook.

Until that happens though, I'd much rather travel with a £250 Chromebook than with a £1,000 Mac and this set up gets me 95% of the tools that I need.