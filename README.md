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

```install.packages(c("ggplot2","knitr","ggthemes","scales","ggmap","plotly","rstudioapi","ggfortify","leaflet","leaflet.extras","rgdal","forecast","prophet","treemapify","dbscan","survival","googleVis","rmarkdown","flexdashboard","highcharter","arules","devtools","tidyverse","maptools","treemap","networkD3","visNetwork","DiagrammeR","DT"))```

This will take a while (...hours) as there is a lot to compile.

To check

## Install LaTeX

A full install of LaTeX is very large so we will start with the smallest possible install and then add in the fonts and packages needed.

Let's start with [TinyTex](https://yihui.name/tinytex/):

```wget -qO- "https://yihui.name/gh/tinytex/tools/install-unx.sh" | sh```

And then add the extra packages we need using ```tlmgr```:

To do

## Additional goodies

To do

zathura
gimp
open office?
