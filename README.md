# Toolchain Docker image

Based on the [nfriedly toolchain Docker image](https://github.com/nfriedly/miyoo-toolchain/) by nfriedly.

Vsync pached SDL 1.2.15 is pre-compiled and installed to /opt/miyoo

## Installation

With Docker installed and running, `make shell` builds the toolchain and drops into a shell inside the container. The container's `~/workspace` is bound to `./workspace` by default. The toolchain is located at `/opt/` inside the container.

After building the first time, unless a dependency of the image has changed, `make shell` will skip building and drop into the shell. Running `make shell` from another window while already in a running shell will attach to the already running image.

## Workflow

You can work on your existing project by running:

```bash
make "WORKSPACE_DIR=$(realpath path/to/your/project)" shell
```

The shell will run as your own user, sudo is unavailable within the container, run the `make shell` command as root to have root access to the container.

## Legacy workflow

- On your host machine, clone repositories into `./workspace` and make changes as usual.
- In the container shell, find the repository in `~/workspace` and build as usual.
- This used to run as root, but it will run as whatever user is running the `make shell` command.

See [setup-env.sh](./build/setup-env.sh) for some useful vars for compiling that are exported automatically.
