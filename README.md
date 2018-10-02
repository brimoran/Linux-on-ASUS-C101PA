# Linux-on-ASUS-C101PA
Setting up Linux on Chromebook

## Aims

The Asus C101PA ua a highly portable 10.1 inch Chromebook that is ideal to take on trips.

Unfortunately hard drive space is at a premium, so we will have to be careful about what we install.

My minimal needs for Linux are working installs of R and LaTeX to enable me to finish off documents on the go... but we'll see what else we can get away with.

## What comes with the standard debian install?

After creating the Limnux container I have 7.1 GB available.

Run ```apt list --installed``` to see what we already have installed.  Most notably we already have Python 3.


## Install stuff that R packages need

```sudo apt-get install curl libcurl4-openssl-dev libxml2-dev libssl-dev libgdal-dev libproj-dev xorg libx11-dev libglu1-mesa-dev r-cran-rgl```

```sudo apt-get update```

```sudo apt-get install r-base```

## Install useful R packages

To do.

## Install LaTeX

A full install of LaTeX is very large so we will start with a small install and just add in the fonts and packages that I need.

## Additional goodies

