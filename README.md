# CodeQL extension for the [GitHub CLI](https://cli.github.com/)

This CLI extension exposes the [CodeQL CLI](https://codeql.github.com/docs/codeql-cli/) as a subcommand of the GitHub CLI, with some additional niceties such as version management.

## Installation

Once you have installed the GitHub CLI (version 2.0 or higher), run `gh extensions install github/gh-codeql`.

## Usage

```bash
$ gh codeql
GitHub command-line wrapper for the CodeQL CLI.

Usage:
    gh codeql set-channel [release|nightly]     # default: release
    gh codeql set-version [version]             # default: latest
    gh codeql list-versions                     # list all available versions for current channel
    gh codeql list-installed                    # list installed versions for current channel
    gh codeql cleanup <version>                 # delete a specific downloaded version
    gh codeql cleanup-all                       # delete all installed versions for all channels
    gh codeql download [version]                # download a specific version (default: latest)
    gh codeql debug [on|off]                    # enable/disable debug output for gh extension
    gh codeql <anything else>                   # pass arguments to CodeQL CLI

Current channel: release.
Current version: not specified.
```

You should be able to prefix any `codeql` command you run with `gh` to automatically download the selected version (by default: the latest release version at the time you first run it) and delegate to it.

### Channels

There are two channels: "release" and "nightly". You are on the release channel by default, and switching channels unpins the selected version (meaning that, unless you run `gh codeql set-version`, the latest version of the current channel will be selected the next time you run a command).

You can list the versions available on the current channel with `gh codeql list-versions`.

You can list the installed versions from the current channel with `gh codeql list-installed`, and reclaim disk space with `gh codeql cleanup <version>`. There is no automatic cleanup.

### Versions

The `gh codeql` command always works relative to a pinned version on the current channel. You can manually specify the pinned version using `gh codeql set-version`.

You can download additional versions without pinning them (perhaps to prepare for local comparisons) using `gh codeql download`.

To upgrade, run `gh codeql set-version latest`, which will pin you to the current latest version.