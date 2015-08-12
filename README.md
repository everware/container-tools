# Basic containers for everware

A basic docker containers for use with everware. Base your
analysis' container on these to get started.


# base

This is the most barebones container that will work with
everware. If you want to create your own use this one as
a starting point. The important thing is to configure your
container to run the `singleuser.sh` script as this one
does.

The single user jupyter notebook is based on python 3 and
needs things like `tornado` installed.

We use anaconda as python distribution, it is just easier
that way.

In addition to the basics this container also includes a
python2 kernel.

Build the image with:
```
cd base
docker build -t everware/base .
```


# science-python

This is a container based on `everware/base` that includes
a few more science libraries. Use it as an example for how
to extend `everware/base` for your analysis.

Build the image with:
```
cd science-python
docker build -t everware/science-python .
```
