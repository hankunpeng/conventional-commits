# Conventional Commits

[简体中文](./README_zh.md) | English

Enforce, validate, lint, and manage [Conventional Commits](https://www.conventionalcommits.org/) across git repositories. This toolkit helps you standardize commit messages, generate semantic changelogs, and install git hooks for automatic enforcement.

## Features

This toolkit provides several features to support Conventional Commits in your workflow:

- **Commit linting** — Validate commit messages against the Conventional Commits specification.
- **Changelog generation** — Automatically produce grouped changelogs from git history.
- **Git hook installation** — Set up a `commit-msg` hook to enforce conventions on every commit.
- **Comprehensive examples** — Reference examples for correct and incorrect commit formats.
- **Specification reference** — Quick-reference summary of the Conventional Commits 1.0.0 spec.

## Commit message format

Conventional Commits follow a structured layout to ensure consistency and readability across the commit history:

```text
<type>[optional scope][optional !]: <description>

[optional body]

[optional footer(s)]
```

### Supported types

The linter supports the following standard and common commit types:

| Type | Description |
|------|-------------|
| `feat` | A new feature |
| `fix` | A bug fix |
| `docs` | Documentation changes |
| `style` | Formatting (no code logic change) |
| `refactor` | Code restructuring (no new feature or bug fix) |
| `perf` | Performance improvements |
| `test` | Adding or correcting tests |
| `build` | Build system or external dependency changes |
| `ci` | CI configuration changes |
| `chore` | General maintenance |
| `revert` | Reverts a previous commit |

## Prerequisites

Before you install and run the scripts, ensure your system meets the following prerequisites:

- **Bash** (v4.0 or newer, installed on the system — scripts can be executed directly from Zsh, Fish, or other shells)
- **Git**
- Standard Unix utilities (`sed`, `awk`, `grep`)

## Installation

This repository is an AI agent skill. You can install it easily using the `skills` CLI:

### Method 1: Project-level installation (recommended)

Install the skill in your current project:

```bash
npx skills add hankunpeng/conventional-commits
```

### Method 2: Global installation (all projects)

Install the skill globally so it is available across all repositories:

```bash
npx skills add hankunpeng/conventional-commits -g
```

### Method 3: Manual installation

If you prefer to install it manually:

1. **Global**: Clone the repository under the global skills directory for your agent platform:
   ```bash
   cd ~/.agents/skills/
   git clone https://github.com/hankunpeng/conventional-commits.git
   ```

2. **Project**: Clone it locally and symlink it to your project:
   ```bash
   # Clone the skill repository
   cd ~/your_path
   git clone https://github.com/hankunpeng/conventional-commits.git

   # Create a symbolic link
   cd ~/your_project_root
   mkdir -p .agents/skills
   ln -s ~/your_path/conventional-commits .agents/skills/conventional-commits
   ```

### Verify installation

After installation, ask the AI agent to lint a commit message to confirm the skill is working:

```
> lint this commit message: "feat(auth): add OAuth2 support"
```

If the skill is loaded correctly, it will use `scripts/commit-lint.sh` to validate the message.

## Quick start

You can use the provided scripts to lint your commit messages, install hooks, or generate changelogs.

### Lint a commit message

To validate a commit message against the specification, run the `commit-lint.sh` script:

```bash
~/your_path/conventional-commits/scripts/commit-lint.sh "feat(auth): add email verification"
# ✔ Commit message style is valid!

~/your_path/conventional-commits/scripts/commit-lint.sh "added new login page"
# ✗ Invalid commit message format.
```

### Install the git hook

Automatically lint every commit message in a repository (defaults to the current directory if no path is provided):

```bash
~/your_path/conventional-commits/scripts/install-git-hook.sh ~/your_repo
# ✔ Installed commit-msg git hook successfully
```

### Generate a changelog

To create a semantic changelog from your git commit history, run the `generate-changelog.sh` script with a revision range:

```bash
./scripts/generate-changelog.sh HEAD~10..HEAD
./scripts/generate-changelog.sh v1.0.0..v1.1.0 v1.1.0
```

**Example output:**

```markdown
# Changelog

## v1.1.0 (2026-06-30)

### Features

- **auth**: add email verification (a1b2c3d)

### Bug Fixes

- fix memory leak in parser (e4f5g6h)
```

## Project structure

The repository contains the following files and directories:

```
conventional-commits/
├── SKILL.md                              # Gemini CLI skill definition
├── README.md                             # This file
├── LICENSE                               # MIT License
├── examples/
│   └── commit-messages.md                # Correct & incorrect commit examples
├── references/
│   └── conventional-commits-spec.md      # Spec summary (Chinese)
└── scripts/
    ├── commit-lint.sh                    # Commit message linter
    ├── generate-changelog.sh             # Changelog generator
    └── install-git-hook.sh               # Git hook installer
```

## Examples

See [examples/commit-messages.md](examples/commit-messages.md) for a full collection of valid and invalid commit message examples.

**Quick valid examples:**

```
feat: add dark mode toggle
fix(parser): handle empty input without crash
refactor(api)!: rename user endpoints
```

## Specification reference

Use these references to learn more about the Conventional Commits specification:

- See [references/conventional-commits-spec.md](references/conventional-commits-spec.md) for a concise summary of the specification written in **Chinese**.
- For the official English specification and guidelines, visit the [Conventional Commits 1.0.0 website](https://www.conventionalcommits.org/).
- See how Conventional Commits tie into [Semantic Versioning](https://semver.org/).

## License

This project is licensed under the [MIT License](LICENSE).
