# Dotnet Tasks

Tasks for building and linting .NET projects via the `dotnet` CLI.

## Requirements

- .NET SDK must be installed and `dotnet` available in PATH

## Available Tasks

- `dotnet:check-prerequisites` - Verify that the .NET CLI is installed and available
- `dotnet:build` - Build a .NET solution
- `dotnet:lint` - Lint a .NET solution using `dotnet format`

## Including in Your Project

To include these tasks in your project, add the following to your `mise.toml`:

```toml
[task_config]
includes = [
    "git::ssh://git@github.com/jterral/mise-tasks.git//tasks/dotnet?ref=v2.3.7",
]
```

## Usage

When imported via the main repository:

```bash
mise task run dotnet:build --solution MyApp.sln --configuration Release
mise task run dotnet:lint --solution MyApp.sln
```
