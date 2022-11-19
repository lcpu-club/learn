# AutoTeX Developmet Wiki

## What is AutoTeX

A tool to compile TeX files. It can be used in PCs, servers, and clusters.

It facilitates the modulized and automatic TeX compilation by using configuration files, in which process it functions as a configuration manager and a command generator.

It automatically detects the TeX environment or sets up its own side-effectless environment. Instant secure containers are used for compilation. 

Mass automatic compilation and automatic artifact delivery are supported.

## Components of AutoTeX

### Configuration Parser

Parses YAML or TOML configuration files to the internal representation, usually composition types provided by Golang.

Configuration can be in the user's local storage or a remote policy server.

### Environment Configurator

Detects the software environment on host machine. If unsatisfied, it will set up its own environment without side effects.

### Command Generator

Takes internal representation provided by 'Configuration Parser,' generates needed command list and file resource list.

### Command Executor

Uses instant secure containers to control user input and run commands generated by 'Command Generator.

### Artifact Deliverer

Delivers compilation artifacts in specified protocol to a specified destination. Both protocol and destination will be provided by configuration.

Supported protocols:

- Redis
- amazon s3
- [objdeliv](https://github.com/lcpu-club/objdeliv)

### Facade

Provides a command line interface, APIs, and code editor extension

## Supported Backend TeX Engine

- LaTeX
- XeLaTeX
- pdfTeX
- LuaLaTeX

## Configures supported by AutoTeX

TODO