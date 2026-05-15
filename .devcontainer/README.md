# Dev Container

## Minimal setup

This project uses a VS Code dev container configuration in `.devcontainer/devcontainer.json`.

- **Base image:** `mcr.microsoft.com/devcontainers/rust:1-1-bookworm`
- **Workspace path:** `/workspaces/diary`
- **Default user:** `vscode`
- **UID/GID sync:** disabled (`updateRemoteUserUID: false`) to avoid host repo ownership changes
- **Podman mapping:** `--userns=keep-id:uid=1000,gid=1000` keeps workspace writable without chowning host files
- **X11 forwarding:** `/tmp/.X11-unix` is mounted for GUI application support

## Environment variables

Set automatically inside the container:

| Variable      | Value                                                        |
|---------------|--------------------------------------------------------------|
| `CARGO_HOME`  | `/usr/local/cargo`                                           |
| `RUSTUP_HOME` | `/usr/local/rustup`                                          |
| `PATH`        | `/usr/local/cargo/bin:/usr/local/sbin:/usr/local/bin:...`   |
| `DISPLAY`     | forwarded from host (`${localEnv:DISPLAY}`)                  |

## Post-create setup (`postCreateCommand`)

After the container starts, the following steps run automatically:

1. **System packages** (via `apt-get`):
   `pkg-config`, `cmake`, `clang`, font/X11/Wayland/GL/input libraries for GUI support
2. **Rust toolchain:** `rustup toolchain install 1.90.0 --profile minimal` with `rustfmt` and `clippy`; set as default
3. **Cargo tools** (via `cargo-binstall`):
   - `bacon` – background build watcher
   - `cargo-audit` – security advisory checks
   - `cargo-nextest` – improved test runner
   - `ripgrep` – fast grep tool

> **Note:** Rust 1.90.0 is set as the default toolchain via `rustup default` in `postCreateCommand`.
> There is no `rust-toolchain.toml` in this repository.

## VS Code extensions

Auto-installed in container (`devcontainer.json`):

- `zerotaskx.rust-extension-pack`
- `davidanson.vscode-markdownlint`
- `ms-vscode.test-adapter-converter`
- `hbenl.vscode-test-explorer`
- `esbenp.prettier-vscode`

## JetBrains plugins

Auto-installed when opening in a JetBrains IDE (backend: IntelliJ):

- `org.rust.cargo`
- `org.rust.rustfmt`
- `org.rust.cargo-audit`
- `PlantUML integration`
- `org.jetbrains.plugins.github`

## Open in container

Use **Dev Containers: Rebuild and Reopen in Container** (VS Code) or the equivalent JetBrains action.

## Verify tools inside container

```bash
cargo --version
rustfmt --version
clippy-driver --version
cargo audit --version
cargo nextest --version
bacon --version
rg --version
```
