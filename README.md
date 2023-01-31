# Repository Sync action

[![](https://img.shields.io/badge/made%20by-Swarm-blue.svg?style=flat-square)](https://swarm.ethereum.org/)
[![standard-readme compliant](https://img.shields.io/badge/standard--readme-OK-brightgreen.svg?style=flat-square)](https://github.com/RichardLitt/standard-readme)

> Action that takes master repo and sync its files (for example configuration files) into the repo where it is run.

**Warning: This project is in beta state. There might (and most probably will) be changes in the future to its API and working. Also, no guarantees can be made about its stability, efficiency, and security at this stage.**

## Table of Contents

- [Usage](#usage)
- [Action inputs](#action-inputs)
- [Action outputs](#action-outputs)
- [Contribute](#contribute)
- [License](#license)

## Usage

Have a repository (that we call master repo) with files that you want to have synced. If this repo is private then you
have to specify `token` that has access both to the master repository and synced repository.

In your synced repository define a Workflow like this:

```yaml
name: Sync configuration files

on:
  schedule:
    - cron:  "0 0 * * *"
  push:
    branches:
      - 'master'

jobs:
  check:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v2

      - name: Check and update the Bee version
        uses: ethersphere/repo-sync-action@v1
        with:
          repo: ethersphere/configs-js
```

This workflow will be triggered both on push to master and regularly run on midnight every day.

## Action inputs

| Name | Description | Default |
| --- | --- | --- |
| `repo` | Repo in format `<owner>/<repo>` |  |
| `branch` | What branch should be used in the repo | default branch |
| `path` | Path to the repo where to sync the files to | |
| `exclude` | Bash Glob of files that should be excluded from the syncing (`.git` folder is is automatically excluded) | `README.md` |
| `title` | Title of the syncing PR | `chore: syncing files` |
| `body` | Body of the syncing PR | |
| `author` | Author of the syncing PR | `github-actions[bot] <github-actions[bot]@users.noreply.github.com>` |
| `pr-branch` | Branch of the syncing PR | `chore/syncing-files` |
| `token` | Token to be used for git-checkout of the master repo and creation of the syncing PR. | `GITHUB_TOKEN` |

## Action outputs

| Name | Description |
| --- | --- |
| `result` | Result of the syncing. Possible values: `created`, `updated` or `unchanged`s |

## Contribute

There are some ways you can make this module better:

- Consult our [open issues](https://github.com/ethersphere/update-supported-bee-action/issues) and take on one of them
- Help our tests reach 100% coverage!
- Join us in our [Discord chat](https://discord.gg/wdghaQsGq5) in the #develop-on-swarm channel if you have questions or want to give feedback

## Maintainers

See what "Maintainer" means [here](https://github.com/ethersphere/repo-maintainer).

## License

[BSD-3-Clause](./LICENSE)

