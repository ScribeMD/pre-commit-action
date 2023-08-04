# pre-commit-action

[![GitHub Action: Try Me](https://img.shields.io/badge/GitHub_Action-Try_Me-AC80A0?logo=githubactions&logoColor=2088FF&labelColor=343B42)](https://github.com/marketplace/actions/pre-commit-optimized-for-scribemd-pre-commit-hooks)
[![Test Workflow Status](https://github.com/ScribeMD/pre-commit-action/workflows/Test/badge.svg)](https://github.com/ScribeMD/pre-commit-action/actions/workflows/test.yaml)
[![Copy/Paste: 0%](https://img.shields.io/badge/Copy%2FPaste-0%25-B200B2?logo=data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIyNCIgaGVpZ2h0PSIyNCIgdmlld0JveD0iMCAwIDI0IDI0Ij48cGF0aCBmaWxsLXJ1bGU9ImV2ZW5vZGQiIGQ9Ik03LjAyNCAzLjc1YzAtLjk2Ni43ODQtMS43NSAxLjc1LTEuNzVIMjAuMjVjLjk2NiAwIDEuNzUuNzg0IDEuNzUgMS43NXYxMS40OThhMS43NSAxLjc1IDAgMDEtMS43NSAxLjc1SDguNzc0YTEuNzUgMS43NSAwIDAxLTEuNzUtMS43NVYzLjc1em0xLjc1LS4yNWEuMjUuMjUgMCAwMC0uMjUuMjV2MTEuNDk4YzAgLjEzOS4xMTIuMjUuMjUuMjVIMjAuMjVhLjI1LjI1IDAgMDAuMjUtLjI1VjMuNzVhLjI1LjI1IDAgMDAtLjI1LS4yNUg4Ljc3NHoiLz48cGF0aCBkPSJNMS45OTUgMTAuNzQ5YTEuNzUgMS43NSAwIDAxMS43NS0xLjc1MUg1LjI1YS43NS43NSAwIDExMCAxLjVIMy43NDVhLjI1LjI1IDAgMDAtLjI1LjI1TDMuNSAyMC4yNWMwIC4xMzguMTExLjI1LjI1LjI1aDkuNWEuMjUuMjUgMCAwMC4yNS0uMjV2LTEuNTFhLjc1Ljc1IDAgMTExLjUgMHYxLjUxQTEuNzUgMS43NSAwIDAxMTMuMjUgMjJoLTkuNUExLjc1IDEuNzUgMCAwMTIgMjAuMjVsLS4wMDUtOS41MDF6Ii8+PC9zdmc+&labelColor=343B42)](https://github.com/kucherenko/jscpd)

[![Automated Updates: Renovate](https://img.shields.io/badge/Renovate-Automated_Updates-FF9F1C?logo=renovatebot&logoColor=1A1F6C&labelColor=666)](https://docs.renovatebot.com/)
[![Package Management: Poetry](https://img.shields.io/badge/Poetry-Package_Management-06BA63?logo=poetry&logoColor=60A5FA&labelColor=666)](https://python-poetry.org/)
[![Git Hooks: pre-commit](https://img.shields.io/badge/pre--commit-Git_Hooks-04E762?logo=precommit&logoColor=FAB040&labelColor=666)](https://pre-commit.com/)
[![Commit Style: Conventional Commits](https://img.shields.io/badge/Conventional_Commits-Commit_Style-090C9B?logo=conventionalcommits&logoColor=FE5196&labelColor=666)](https://conventionalcommits.org)
[![Releases: Semantic Versioning](https://img.shields.io/badge/SemVer-Releases-08A045?logo=semver&logoColor=3F4551&labelColor=666)](https://semver.org/)
[![Code Style: Prettier](https://img.shields.io/badge/Prettier-Code_Style-000?logo=prettier&logoColor=F7B93E&labelColor=666)](https://prettier.io/)
[![Code Style: EditorConfig](https://img.shields.io/badge/EditorConfig-Code_Style-FF69EB?logo=editorconfig&logoColor=FEFEFE&labelColor=666)](https://editorconfig.org/)
[![Editor: Visual Studio Code](https://img.shields.io/badge/VSCode-Editor-EE8434?logo=visualstudiocode&logoColor=007ACC&labelColor=666)](https://code.visualstudio.com/)

GitHub Action Optimized for Running
[ScribeMD/pre-commit-hooks](https://github.com/ScribeMD/pre-commit-hooks/)

<!--TOC-->

- [pre-commit-action](#pre-commit-action)
  - [Usage](#usage)
  - [Inputs](#inputs)
    - [Optional](#optional)
  - [Supported Runners](#supported-runners)
  - [Permissions](#permissions)
  - [Changelog](#changelog)

<!--TOC-->

Install [asdf](https://asdf-vm.com/), [Node.js](https://nodejs.org),
[Python](https://www.python.org), and [Poetry](https://python-poetry.org/); use
Poetry to install [pre-commit](https://pre-commit.com); run pre-commit hooks;
and optionally use
[commitizen-action](https://github.com/commitizen-tools/commitizen-action/) to
bump the project version. Assume the presence of
[`.tool-versions`](https://asdf-vm.com/manage/configuration.html#tool-versions)
specifying versions for Node.js, Python, and Poetry as well as
[`poetry.lock`](https://python-poetry.org/docs/basic-usage/#installing-with-poetrylock).
Cache Poetry dependencies. Cache Node.js packages specified in
[`.mega-linter.yaml`](https://megalinter.io/), `.pre-commit-config.yaml`, and/or
`.pre-commit-hooks.yaml`. Since
[pre-commit supports Docker](https://pre-commit.com/#docker_image), cache
[Docker](https://www.docker.com/) images. Cache pre-commit hook environments.
Set `origin/HEAD` to the default branch to support the
[`commitizen-branch` hook](https://commitizen-tools.github.io/commitizen/#integrating-with-pre-commit).
Skip the `commitizen-branch` hook and
[`no-commit-to-branch` hook](https://github.com/pre-commit/pre-commit-hooks#no-commit-to-branch)
on `main` to avoid false positives. Finally, uninstall pre-commit hooks to avoid
breaking subsequent Git commands. This relies on specifying
[`default_install_hook_types`](https://pre-commit.com/#top_level-default_install_hook_types)
in `.pre-commit-config.yaml`.

## Usage

- Commitizen relies on tags in order to perform an incremental release, and the
  [`commitizen-branch` hook](https://commitizen-tools.github.io/commitizen/#integrating-with-pre-commit)
  relies on `origin/HEAD` being set to the default branch, so you must pass
  [`fetch-depth: 0`](https://github.com/marketplace/actions/checkout#Fetch-all-history-for-all-tags-and-branches)
  to [`checkout`](https://github.com/marketplace/actions/checkout).
- Add the following step before your first use of Docker since
  [rootless-docker](https://github.com/ScribeMD/rootless-docker) is used to avoid
  permission issues:

  ```yaml
  - name: Install and run pre-commit hooks.
    uses: ScribeMD/pre-commit-action@0.9.87
  ```

## Inputs

### Optional

#### bump

default: `true`

If `"true"`, run
[commitizen-action](https://github.com/commitizen-tools/commitizen-action/) on
push to `main` to commit a version bump and tag a release if there are any
release-worthy changes. Uses your
[`GITHUB_TOKEN`](https://docs.github.com/en/actions/security-guides/automatic-token-authentication),
which must have write access to your repository.

## Supported Runners

Please refer to
[`README.md` of ScribeMD/rootless-docker](https://github.com/ScribeMD/rootless-docker#supported-runners).

## Permissions

The `contents:write`
[permission](https://docs.github.com/en/actions/security-guides/automatic-token-authentication#permissions-for-the-github_token)
is required to bump the project version via Commitizen unless `bump` is `false`.

## Changelog

Please refer to [`CHANGELOG.md`](CHANGELOG.md).
