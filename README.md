# yq

[![Build Status](https://travis-ci.org/mikefarah/yq.svg?branch=master)](https://travis-ci.org/mikefarah/yq)  ![Docker Pulls](https://img.shields.io/docker/pulls/mikefarah/yq.svg) ![Github Releases (by Release)](https://img.shields.io/github/downloads/mikefarah/yq/total.svg) ![Go Report](https://goreportcard.com/badge/github.com/mikefarah/yq)


a lightweight and portable command-line YAML processor

The aim of the project is to be the [jq](https://github.com/stedolan/jq) or sed of yaml files.

## Install
### On MacOS:
```
brew install yq
```
### On Debian and other Linux distros:
```
docker build -t yd-deb -f Dockerfile.debian .
docker run yd-deb > yd-${VERSION}.deb
sudo deb --install yd-${VERSION}.deb
```

### or, [Download latest binary](https://github.com/mikefarah/yq/releases/latest) or alternatively:
```
GO111MODULE=on go get github.com/mikefarah/yq@2.4.1
```

## Run with Docker

Oneshot use:

```bash
docker run --rm -v ${PWD}:/workdir mikefarah/yq yq [flags] <command> FILE...
```

Run commands interactively:

```bash
docker run --rm -it -v ${PWD}:/workdir mikefarah/yq sh
```

It can be useful to have a bash function to avoid typing the whole docker command:

```bash
yq() {
  docker run --rm -i -v ${PWD}:/workdir mikefarah/yq yq $@
}
```

## Features
- Written in portable go, so you can download a lovely dependency free binary
- Deep read a yaml file with a given path
- Update a yaml file given a path
- Update a yaml file given a script file
- Update creates any missing entries in the path on the fly
- Create a yaml file given a deep path and value
- Create a yaml file given a script file
- Prefix a path to a yaml file
- Convert from json to yaml
- Convert from yaml to json
- Pipe data in by using '-'
- Merge multiple yaml files where each additional file sets values for missing or null value keys.
- Merge multiple yaml files and override previous values.
- Merge multiple yaml files and append array values.
- Supports multiple documents in a single yaml file

## [Usage](http://mikefarah.github.io/yq/)

Check out the [documentation](http://mikefarah.github.io/yq/) for more detailed and advanced usage.

```
yq is a lightweight and portable command-line YAML processor. It aims to be the jq or sed of yaml files.

Usage:
  yq [flags]
  yq [command]

Available Commands:
  delete      yq d [--inplace/-i] [--doc/-d index] sample.yaml a.b.c
  help        Help about any command
  merge       yq m [--inplace/-i] [--doc/-d index] [--overwrite/-x] [--append/-a] sample.yaml sample2.yaml
  new         yq n [--script/-s script_file] a.b.c newValue
  prefix      yq p [--inplace/-i] [--doc/-d index] sample.yaml a.b.c
  read        yq r [--doc/-d index] sample.yaml a.b.c
  write       yq w [--inplace/-i] [--script/-s script_file] [--doc/-d index] sample.yaml a.b.c newValue

Flags:
  -h, --help      help for yq
  -t, --trim      trim yaml output (default true)
  -v, --verbose   verbose mode
  -V, --version   Print version information and quit

Use "yq [command] --help" for more information about a command.
```

## Contribute
1. `scripts/devtools.sh`
2. `make [local] vendor`
3. add unit tests
4. apply changes to go.mod
5. `make [local] build`
6. If required, update the user documentation
    - Update README.md and/or documentation under the mkdocs folder
    - `make [local] build-docs`
    - browse to docs/index.html and check your changes
7. profit
