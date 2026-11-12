# 🧰 Mise Tasks

Shared tasks for [mise-en-place](https://mise.jdx.dev/) so I can keep a single source of truth for common setup and automation steps.

## ✨ What is this repo for?

- Provide reusable, versioned tasks for `mise-en-place`.
- Keep environment setup and project automation consistent across machines.
- Make it easy to discover and run tasks with clear names and docs.

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

Each task folder is independently importable. The nested folder structure (e.g., `gitversion/gitversion/`) allows tasks to be automatically namespaced by the parent folder name (e.g., `gitversion:current`).

## 🚀 Usage

### For Projects Importing Specific Task Collections

Import only the task collections you need in your `mise.toml`:

```toml
[task_config]
includes = [
    "git::ssh://git@github.com/jterral/mise-tasks.git//tasks/docker?ref=v2.0.0",
    "git::ssh://git@github.com/jterral/mise-tasks.git//tasks/gitversion?ref=v2.0.0",
    "git::ssh://git@github.com/jterral/mise-tasks.git//tasks/precommit?ref=v2.0.0",
]
```

Tasks are automatically namespaced by folder:

```bash
mise task run gitversion:current
mise task run docker:clean
mise task run docker:compose:lint
mise task run precommit:configure
```

### Available Tasks

- `gitversion`: see [tasks/gitversion/README.md](tasks/gitversion/README.md)
- `precommit`: see [tasks/precommit/README.md](tasks/precommit/README.md)
- `docker`: see [tasks/docker/README.md](tasks/docker/README.md)

For details, see the official mise docs: <https://mise.jdx.dev/tasks/>

## 🤝 Contributing

- Add or update tasks in `tasks/` under the appropriate task collection folder.
- Keep tasks small, focused, and well-named.
- Document any required inputs or environment variables in the task itself.
- Update the corresponding task collection's `README.md` when adding new tasks.

## 🔑 License

See [LICENSE](LICENSE).
