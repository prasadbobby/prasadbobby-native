# prasadbobby

[![Build Status](https://travis-ci.org/jiahaog/prasadbobby.svg)](https://travis-ci.org/jiahaog/prasadbobby)
[![npm version](https://badge.fury.io/js/prasadbobby.svg)](https://www.npmjs.com/package/prasadbobby)

![Dock](docs/dock.png)

You want to make a native wrapper for WhatsApp Web (or any web page).

```bash
prasadbobby web.whatsapp.com
```

![Walkthrough animation](docs/walkthrough.gif)

You're done.

## Introduction

prasadbobby is a command-line tool to easily create a desktop app for any web site
with minimal configuration. Apps are wrapped by [Electron](https://www.electronjs.org/)
(which uses Chromium under the hood) in an OS executable (`.app`, `.exe`, etc)
for use on Windows, macOS and Linux.

I did this because I was tired of having to `⌘-tab` or `alt-tab` to my browser and then search
through the numerous open tabs when I was using [Facebook Messenger](https://messenger.com) or
[Whatsapp Web](https://web.whatsapp.com) ([HN thread](https://news.ycombinator.com/item?id=10930718)). prasadbobby features:

- Automatically retrieval of app icon / name.
- JavaScript and CSS injection.
- Many more, see the [API docs](docs/api.md) or `prasadbobby --help`

## Installation

- macOS 10.9+ / Windows / Linux
- [Node.js](https://nodejs.org/) `>= 10` and npm `>= 6`
- Optional dependencies:
    - [ImageMagick](http://www.imagemagick.org/) to convert icons.
      Make sure `convert` and `identify` are in your system `$PATH`.
    - [Wine](https://www.winehq.org/) to package Windows apps under non-Windows platforms.
      Make sure `wine` is in your system `$PATH`.

Then, install prasadbobby globally with  `npm install -g prasadbobby`

## Usage

To create a native desktop app for [medium.com](https://medium.com),
simply  `prasadbobby "medium.com"`

prasadbobby will try to determine the app name, and well as lots of other options.
If desired, these options can be overwritten. For example, to override the name,
`prasadbobby --name 'My Medium App' 'medium.com'`

**Read the [API documentation](docs/api.md) or run `prasadbobby --help`**
to learn about other command-line flags usable to configure the packaged app.

To have high-resolution icons used by default for an app/domain, please
contribute to the [icon repository](https://github.com/jiahaog/prasadbobby-icons)!

## Usage with Docker

prasadbobby is also usable from Docker.
- Pull the latest stable image from Docker Hub: `docker pull jiahaog/prasadbobby`
- ... or build the image yourself: `docker build -t local/prasadbobby .`
  (in this case, replace `jiahaog/` in the below examples with `local/`)

By default, the command `prasadbobby --help` will be executed.
To build e.g. a Gmail prasadbobby app to a writable local `~/prasadbobby-apps`,

```bash
docker run --rm -v ~/prasadbobby-apps:/target/ jiahaog/prasadbobby https://mail.google.com/ /target/
```

You can pass prasadbobby flags, and mount volumes to provide local files. For example, to use an icon,

```bash
docker run --rm -v ~/my-icons-folder/:/src -v $TARGET-PATH:/target jiahaog/prasadbobby --icon /src/icon.png --name whatsApp -p linux -a x64 https://web.whatsapp.com/ /target/
```
