# AGENTS.md

Minimal operator guide for this meta repo. Keep actions safe, fast, and scoped.

## What This Repo Is
- This directory is a `mani` control repo for multiple sibling git repos.
- Project inventory and automation entrypoints live in `mani.yaml`.
- Main groups: `lz/*`, `sgfdevs/*`, and `opensgf/*`.

## Core Mani Commands
- Validate config: `mani check`
- List projects: `mani list projects`
- Run a task: `mani run <task> [--target <target>]`
- Run ad-hoc command: `mani exec --target <target> '<cmd>'`
- Sync clone status: `mani sync --status`

## Targets You Should Use
- Org: `lz`, `sgfdevs`, `opensgf`
- Stack: `tf`, `ansible`, `k8s`
- Combined: `lz-tf`, `lz-ansible`, `lz-k8s`, `sgfdevs-tf`, `sgfdevs-ansible`, `sgfdevs-k8s`, `opensgf-tf`

## Built-in Mani Tasks
- `git-status` -> `git status -sb`
- `git-branch` -> current branch
- `git-fetch` -> fetch/prune remotes
- `git-pull-main` -> ff-only pull when branch is `main`
- `if-changed` -> run the supplied `run='<command>'` only in dirty repos
- `tf-fmt-check` -> `make tf-lint` (tf-tagged repos)
- `ansible-install` -> `make ansible-install` (ansible-tagged repos)
- `ansible-lint` -> `make ansible-lint` (ansible-tagged repos)

## Makefile Conventions (Inside Child Repos)
- Start with: `make help`
- Terraform/OpenTofu lifecycle usually:
  - `make tf-init`
  - `make tf-plan`
  - `make tf-apply` (only when explicitly requested)
- Common checks:
  - `make tf-format` (check)
  - `make tf-lint-fix` (rewrite)
- Ansible lifecycle usually:
  - `make ansible-install`
  - `make ansible-lint`
  - `make ansible PLAYBOOK=<name>.yml`

## Practical Safety Rules
- Prefer read-only/status commands first.
- Do not run apply/destructive commands unless user explicitly asks.
- Scope commands via `mani` targets instead of running across all repos by default.
- Each child repo is independent: branching, commits, and CI are per-repo.

## Useful Patterns
- Check all LZ terraform repos: `mani run git-status --target lz-tf`
- Fetch all ansible repos: `mani run git-fetch --target ansible`
- Run one make target everywhere in k8s repos:
  - `mani exec --target k8s 'make help'`

## Notes
- Some repos pin `uv` versions in `src/ansible/pyproject.toml`.
- If tooling errors mention version constraints, check those files first.
