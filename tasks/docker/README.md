# Docker Tasks

Tasks for common Docker workflows using Docker CLI and Docker Compose v2.

## Requirements

- Docker CLI must be installed and available in PATH
- Docker Compose v2 plugin must be available via `docker compose`
- A project Dockerfile and/or Compose file must exist for related tasks

## Available Tasks

- `docker:check-prerequisites` - Verify that Docker CLI and Docker Compose v2 are available
- `docker:build` - Build a Docker image
- `docker:prune` - Aggressively clean unused Docker resources (asks for confirmation)
- `docker:lint` - Lint a Dockerfile using `docker build --check`
- `docker:compose:up` - Start services with `docker compose up -d`
- `docker:compose:down` - Stop services with `docker compose down`
- `docker:compose:lint` - Lint a Compose file using `docker compose config`

## Including in Your Project

To include these tasks in your project, add the following to your `mise.toml`:

```toml
[task_config]
includes = [
    "git::ssh://git@github.com/jterral/mise-tasks.git//tasks/docker?ref=v2.3.7",
]
```

## Usage

When imported via the main repository:

```bash
mise task run docker:build --image my-app --tag dev
mise task run docker:lint --file Dockerfile
mise task run docker:prune
mise task run docker:compose:up --file docker-compose.yml
mise task run docker:compose:down
mise task run docker:compose:lint
```
