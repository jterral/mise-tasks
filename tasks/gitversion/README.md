# GitVersion Tasks

Tasks for managing version information using [GitVersion](https://gitversion.net/).

## Requirements

- GitVersion must be installed and available in PATH
- The repository must be a git repository with proper git history

## Available Tasks

- `gitversion:check-prerequisites` - Verify that GitVersion is properly installed and configured
- `gitversion:current` - Get the current semantic version from the repository
- `gitversion:calver` - Get the current version in CalVer format (`YY.WW.N`)

## Including in Your Project

To include these tasks in your project, add the following to your `mise.toml`:

```toml
[task_config]
includes = [
    "git::ssh://git@github.com/jterral/mise-tasks.git//tasks/gitversion?ref=v2.3.7",
]
```

## Usage

When imported via the main repository:

```bash
mise task run gitversion:check-prerequisites
mise task run gitversion:current
mise task run gitversion:calver
```
