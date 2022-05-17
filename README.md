# pre-commit-action

[![Test](https://github.com/ScribeMD/pre-commit-action/workflows/Test/badge.svg)](https://github.com/ScribeMD/pre-commit-action/actions/workflows/test.yaml)
[![pre-commit](https://img.shields.io/badge/pre--commit-enabled-brightgreen?logo=pre-commit&logoColor=white)](https://github.com/pre-commit/pre-commit)
[![Conventional Commits](https://img.shields.io/badge/Conventional%20Commits-1.0.0-yellow.svg?style=flat-square)](https://conventionalcommits.org)
[![code style: prettier](https://img.shields.io/badge/code_style-prettier-ff69b4.svg?style=flat-square)](https://github.com/prettier/prettier)

GitHub Action Optimized for Running
[ScribeMD/pre-commit-hooks](https://github.com/ScribeMD/pre-commit-hooks/)

<!--TOC-->

- [pre-commit-action](#pre-commit-action)
  - [Usage](#usage)
  - [Supported Runners](#supported-runners)
  - [Changelog](#changelog)

<!--TOC-->

Install [asdf](https://asdf-vm.com/); use asdf to install
[Node.js](https://nodejs.org), [Python](https://www.python.org), and
[Poetry](https://python-poetry.org/); use Poetry to install
[pre-commit](https://pre-commit.com); and finally run pre-commit hooks. Assume
the presence of
[`.tool-versions`](https://asdf-vm.com/manage/configuration.html#tool-versions)
specifying versions for Node.js, Python, and Poetry as well as
[`poetry.lock`](https://python-poetry.org/docs/basic-usage/#installing-with-poetrylock).
Cache Node.js packages specified in [`.mega-linter.yaml`](https://megalinter.github.io),
`.pre-commit-config.yaml`, and/or `.pre-commit-hooks.yaml`.
Since [pre-commit supports Docker](https://pre-commit.com/#docker_image), cache
[Docker](https://www.docker.com/) images. Skip the
[`no-commit-to-branch` hook](https://github.com/pre-commit/pre-commit-hooks#no-commit-to-branch)
since it causes all runs on a given branch to fail and is most often used to
protect the default branch. Finally, uninstall pre-commit hooks to avoid
breaking subsequent Git commands. This relies on specifying
[`default_install_hook_types`](https://pre-commit.com/#top_level-default_install_hook_types)
in `.pre-commit-config.yaml`.

## Usage

- Add the following step before your first use of Docker since
  [rootless-docker](https://github.com/ScribeMD/rootless-docker) is used to avoid
  permission issues:

```yaml
- name: Install and run pre-commit hooks.
  uses: ScribeMD/pre-commit-action@0.5.0
```

## Supported Runners

Please refer to
[`README.md` of ScribeMD/rootless-docker](https://github.com/ScribeMD/rootless-docker#supported-runners).

## Changelog

Please refer to [`CHANGELOG.md`](CHANGELOG.md).
