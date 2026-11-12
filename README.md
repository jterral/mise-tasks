# 🧰 Mise Tasks

Shared tasks for [mise-en-place](https://mise.jdx.dev/) so I can keep a single source of truth for common setup and automation steps.

## ✨ What is this repo for?

- Provide reusable, versioned tasks for `mise-en-place`.
- Keep environment setup and project automation consistent across machines.
- Make it easy to discover and run tasks with clear names and docs.

## 📦 Task collections

Each collection is independently importable and documented in its own README.

| Collection | Description | Docs |
| --- | --- | --- |
| `docker` | Build, lint and clean with Docker, plus Docker Compose v2 workflows | [README](tasks/docker/README.md) |
| `dotnet` | Build and lint .NET solutions | [README](tasks/dotnet/README.md) |
| `gitversion` | Compute SemVer or CalVer versions with GitVersion | [README](tasks/gitversion/README.md) |
| `precommit` | Install, run, update and remove pre-commit hooks | [README](tasks/precommit/README.md) |

## 📋 Available tasks

Every collection also ships a hidden `check-prerequisites` task, run automatically as a dependency of the other tasks.

### 🐳 docker

| Task | Description |
| --- | --- |
| `docker:build` | Build a Docker image (`--image`, `--tag`, `--file`, `--context`) |
| `docker:lint` | Lint a Dockerfile with `docker build --check` |
| `docker:prune` | Aggressively clean unused images, containers, networks and volumes (asks for confirmation) |
| `docker:compose:up` | Start services with `docker compose up -d` |
| `docker:compose:down` | Stop services with `docker compose down` |
| `docker:compose:lint` | Validate a Compose file with `docker compose config` |

### 🟣 dotnet

| Task | Description |
| --- | --- |
| `dotnet:build` | Build a .NET solution (`--solution`, `--configuration`) |
| `dotnet:lint` | Lint a .NET solution with `dotnet format` |

### 🔖 gitversion

| Task | Description |
| --- | --- |
| `gitversion:current` | Get the current version using GitVersion |
| `gitversion:calver` | Get the current version in CalVer format (`YY.WW.N`) |

### 🪝 precommit

| Task | Description |
| --- | --- |
| `precommit:install` | Install pre-commit hooks |
| `precommit:run-all` | Run all pre-commit hooks |
| `precommit:run-hook` | Run a single hook (`<hook>`) |
| `precommit:update` | Update hooks to their latest versions |
| `precommit:uninstall` | Uninstall all pre-commit hooks |

## 🚀 Usage

Import only the collections you need in your `mise.toml`:

```toml
[task_config]
includes = [
    "git::ssh://git@github.com/jterral/mise-tasks.git//tasks/docker?ref=v2.3.7",
    "git::ssh://git@github.com/jterral/mise-tasks.git//tasks/dotnet?ref=v2.3.7",
    "git::ssh://git@github.com/jterral/mise-tasks.git//tasks/gitversion?ref=v2.3.7",
    "git::ssh://git@github.com/jterral/mise-tasks.git//tasks/precommit?ref=v2.3.7",
]
```

> Pin `ref` to a [release tag](https://github.com/jterral/mise-tasks/tags) so your tasks only change when you decide to upgrade.

Tasks are automatically namespaced by collection:

```bash
mise tasks ls                                   # list available tasks
mise task run gitversion:current
mise task run docker:build --image my-app --tag dev
mise task run docker:compose:lint
mise task run dotnet:build --solution MyApp.sln --configuration Release
mise task run precommit:run-hook <hook>
```

For details, see the official mise docs: <https://mise.jdx.dev/tasks/>

## 🗂️ Structure

```txt
tasks/
├── docker/
│   ├── README.md
│   └── docker/
│       ├── check-prerequisites.sh
│       ├── *.sh
│       └── compose/
│           ├── check-prerequisites.sh
│           └── *.sh
├── dotnet/
│   ├── README.md
│   └── dotnet/
│       ├── check-prerequisites.sh
│       └── *.sh
├── gitversion/
│   ├── README.md
│   └── gitversion/
│       ├── check-prerequisites.sh
│       └── *.sh
├── precommit/
│   ├── README.md
│   └── precommit/
│       ├── check-prerequisites.sh
│       └── *.sh
└── ...
```

The nested folder (e.g., `gitversion/gitversion/`) namespaces tasks by the parent folder name (e.g., `gitversion:current`). Task metadata (description, dependencies, flags) lives in `#MISE` and `#USAGE` comments at the top of each script.

## 🤝 Contributing

- Add or update tasks in `tasks/<name>/<name>/`, one script per action.
- Every collection must include a `check-prerequisites.sh`.
- Keep tasks small, focused, and well-named; declare dependencies with `#MISE depends`.
- Document any required inputs or environment variables in the task itself.
- Update the collection's `README.md` **and** the tables above when adding or changing tasks.
- Follow the Conventional Commits format (a scope is mandatory), e.g. `feat(docker): add push task`.

## 🔑 License

See [LICENSE](LICENSE).
