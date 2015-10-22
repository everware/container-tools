# A toolbox for building everware containers

Tools for constructing containers that work with
`everware`.

This repository contains [example containers](#containers),
documentation and [tools](#tools) for designing a `docker`
container for your repository.


# Tools

## run_local.sh

To help with testing your setup and running your repository
on your local machine there is the `run_local.sh` script.


# Containers

Basic docker containers for use with `everware`. These
serve as documentation/specification for what a container
has to do to be `everware`-ready.

They are as basic as possible, so probably not so useful
for actually running your repository.


## base

This is the most barebones container that will work with
everware. If you want to create your own use this one as
a starting point. The important thing is to configure your
container to `RUN` the `singleuser.sh` script in the same
way that this one does.

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


## science-python

This is a container based on `everware/base` that includes
a few more science-y libraries. Use it as an example of how
to extend `everware/base` for your repository.

Build the image with:
```
cd science-python
docker build -t everware/science-python .
```
