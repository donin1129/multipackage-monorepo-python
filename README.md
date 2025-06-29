# Multipackage monorepo python project with uv workspace

This repository demonstrates a Python monorepo structure using [`uv`](https://github.com/astral-sh/uv) workspaces to manage multiple interdependent packages.


# Project Overview

This monorepo contains three packages:

- `common`: Representing sshared functionality

- `cli`: Skeleton project that depends on common

- `api`: Skeleton project that depends on common

The uv tool is used to manage dependencies, environments, and execution across packages.

***

# Getting Started

## Prerequisite

- [Install `uv`](https://github.com/astral-sh/uv?tab=readme-ov-file#installation)

## Project Structure

```
project-root
├── pyproject.toml
└── packages/
    ├── api/
    │   ├── pyproject.toml
    │   └── src/
    │       └── api/
    │           ├── __init__.py
    │           └── main.py
    ├── cli/
    │   ├── pyproject.toml
    │   └── src/
    │       └── cli/
    │           ├── __init__.py
    │           └── main.py
    └── common/
        ├── pyproject.toml
        └── src/
            └── common/
                ├── __init__.py
                └── datetime_lib.py
```

The CLI and API packages both import and use shared functionality from the `common` package.

***

# Usage

Sync dependencies across the workspace:
```shell
uv sync
```

Run modules from specific packages:
```shell
uv run --package common python -m common.datetime_lib
```

```shell
uv run --package api python -m api.main
```

```shell
uv run --package cli python -m cli.main
```

To initialize a new package in the workspace, use:

```shell
uv init packages/core --package
```

This will create a new `core` package scaffold under `packages`.

***

# Notes

This project follows a **multipackage monorepo** structure, which typically includes:

- Two or more packages located in a single repository
- Logical separation of functionality across packages (e.g. `common`, `cli`, `api`)
- Shared tooling and dependency management (in this case, via `uv`)
- Packages that may have interdependencies (e.g. `cli` and `api` both depend on `common`)
- Multiple entrypoints. Packages are peers and there is no "root" package (e.g. `cli` and `api` can both be entrypoints)
- Centralized development and testing across all packages

Each package:
- Resides in its own subdirectory (e.g. `packages/common`)
- Has its own `pyproject.toml`
- Participates in the shared `uv` workspace defined in the top-level `uv` configuration

This setup enables better modularity, easier reuse of code, and simpler dependency/version management across internal packages.

> If you use PyCharm as IDE, some configurations are also provided. 