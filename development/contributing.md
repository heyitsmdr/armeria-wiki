---
title: Contributing
description: 
published: true
date: 2020-12-15T19:05:16.538Z
tags: 
editor: markdown
dateCreated: 2020-12-15T18:58:01.152Z
---

# Contributing

Since Armeria is open-source, anyone can run Armeria locally and contribute to the game. All contributions are welcome and extremely appreciated. The only thing not included is access to the production data. However, there is an abundance of example data included within the repo.

## Getting Started

To begin contributing to Armeria, create a fork of the `armeria` repo. You can work on your changes on a feature branch based off of your forked repo.

## Local Development

To get started, you will need the following installed:

- Golang (>= 1.13)
- Node.js (>= 10.0.0)
- Yarn (>= 1.6.0)

To build and run the game:

```bash
$ go run cmd/armeria/main.go
```

To build and run the web client:

```bash
$ yarn install
$ yarn serve
```

You can load the client here: [http://localhost:8080/](http://localhost:8080/).

You should now be able to login using the command: `/login admin admin`.

### Client Development

While running `yarn serve`, you can make changes to the client files and the changes will be hot reloaded immediately within the browser. Some of these changes may terminate your connection to the game server and require you to re-login.

### Data Files

When creating in-game content locally, you will notice changes to the `data/*.json` files. Unless you plan to push these upstream, it may make sense to instruct Git to ignore changes to those files so they no longer show up in `git status` and won't be accidentally pushed with your changes.

You can enable this by running:

```bash
$ git update-index --skip-worktree data/*.json
```

When you want to actually push data changes, you can then run:

```bash
$ git update-index --no-skip-worktree data/*.json
```

If you're on a system with `make` support, you can simply run `make skip-data` and `make no-skip-data` respectively to accomplish the same tasks noted above.

Note that even with `--skip-worktree` enabled, newer versions of these files will be pulled if/when they are changed upstream. Plan accordingly and ensure you're using the latest versions prior to pulling down changes (to avoid conflicts).

## Upgrading Dependencies

This section outlines upgrading dependencies for both the client and the server.

### Client

To upgrade Vue.js, make sure you're using the latest version of the Vue CLI. If you don't have it installed, install it with:

```bash
$ yarn global add @vue/cli
$ yarn global add @vue/cli-upgrade
```

If you already have the Vue CLI installed, upgrade it to the latest version with:

```bash
$ yarn global upgrade @vue/cli
$ yarn global upgrade @vue/cli-upgrade
```

Next, use the Vue CLI UI to handle upgrades gracefully. To do this:

```bash
$ vue ui
```

The Vue CLI UI should pop up in your default browser. If the project is not already imported into the UI, go ahead and import it now. For additional help with navigating the Vue CLI UI, take a look at the [Vue CLI Overview](https://cli.vuejs.org/guide/).

Use the **Plugins** and **Dependencies** tabs to upgrade all of the plugins and dependencies that have updates available. Be especially careful when updating the `vue` and `vuex` dependencies to make sure everything is working within the client. It's a good idea to read through the Vue/Vuex release notes when doing this as well.

Note that when performing these upgrades, the `package.json` and `yarn.lock` files will be updated accordingly and, assuming everything is working, these should be committed to the repo.

#### Ace

The [Ace Editor](https://ace.c9.io/) is used for the in-game script editor. Upgrading it is outside the scope of the above client dependencies.

To upgrade Ace, grab the latest build from the [ace-builds](https://github.com/ajaxorg/ace-builds/releases) repo and place the necessary files in `public/vendor/ace-<version>`.

To determine the "necessary" files, look in the directory for the previous version of Ace and you'll discover which Ace plugins / themes we are using that should be copied over from the updated release.

Lastly, update the `<script>` declarations in `public/scripteditor.html` to use the newer `public/vendor/ace-<version>` directory.

Be sure to check the script editor before pushing the change! Make sure syntax highlighting, code completion, and any other Ace-specific features are operational.

### Server

To upgrade *all* of Armeria's dependencies, use:

```
$ go get -u ./...
$ go mod tidy
```

You should also run `go mod tidy` any time you introduce or remove any new or existing dependencies. This will keep the `go.mod` file as clean as possible.

To upgrade a specific dependency, use:

```bash
$ go get -u example.com/pkg
$ go mod tidy
```

Note that the `-u` flag will upgrade both the dependency and all of its dependencies to the latest version.

Lastly, to view all of the available dependency updates, use:

```bash
$ go list -u -m all
```

## Publishing Features

When you have finished working on a feature, be sure there are no broken unit tests. You can check this via:

```bash
$ go test ./...
```

If you are adding new code, be sure you are also modifying or adding unit tests to ensure test coverage. Furthermore, anything that should be documented externally should be submitted to the [Armeria Wiki](https://wiki.armeria.io).

Once ready, create a Pull Request (PR) from your forked repo's feature branch to this repo's `master` branch. Our Heroku pipeline will attempt to build the client and server and will supply you with a Heroku-hosted link of the working client.

## CI/CD

Once you create a Pull Request, a Heroku build will kick off and ensure both the client and server can be built. If there are any errors, you will be notified directly on the Pull Request. Assuming everything succeeds, you will be supplied with a Heroku-hosted link to be able to login and play the game using your branch's code.

## Releasing

A production release will be coordinated on Discord. We will try limiting these to no more than one per day to avoid as many interruptions as possible to the game's players. A production release requires the game server to be restarted.

## Discord

If you plan to develop for Armeria, it's strongly encouraged that you join our community Discord at: https://discord.gg/hMzjH6n (room: #armeria-dev).