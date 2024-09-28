[![NPM version][npm-image]][npm-url]
[![Build Status][build-image]][build-url]
[![Dependency Status][deps-image]][deps-url]

# connect-gzip-static

Middleware for [connect]: serves compressed files if they exist, falls through to connect-static
if they don't, or if browser does not send 'Accept-Encoding' header.

You should use `connect-gzip-static` if your build process already creates compressed (using gzip or
[brotli]) files. If you want to compress your data on the fly use [compression]
middleware. And if you want to compress your files dynamically you may want to look up [connect
gzip].

## Installation

```bash
npm install @figliolia/static-compression
# or
yarn add @figliolia/static-compression
```

## Options

gzip-static is meant to be a drop in replacement for [connect static] middleware. Use the same
options as you would with [connect static].


## Usage

```javascript
import staticCompression from 'connect-gzip-static';
const oneDay = 86400000;

connect()
  .use(staticCompression(__dirname + '/public'))

connect()
  .use(staticCompression(__dirname + '/public', { maxAge: oneDay }))
```

## How it works

We start by locating all compressed files (ie. _files with .gz and .br extensions_) in `root`
directory. All HTTP GET and HTTP HEAD requests with Accept-Encoding header set to gzip are checked
against the list of compressed files and, if possible, fulfilled by returning the compressed
versions. If compressed version is not found or if the request does not have an appropriate Accept-
Encoding header, the request is processed in the same way as standard static middleware would
handle it.

## Debugging

This project uses [debug] module. To enable the debug log, just set the debug enviromental variable:

    DEBUG="connect:static-compression"
