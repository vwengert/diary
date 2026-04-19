FROM mcr.microsoft.com/devcontainers/rust:1-1-bookworm
#
#ARG DEBIAN_FRONTEND=noninteractive
#

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        graphviz \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

RUN su vscode -c "rustup toolchain install 1.91.0 --profile minimal --component rustfmt --component clippy" \
    && su vscode -c "rustup default 1.91.0" \
    && su vscode -c "cargo install cargo-deny cargo-nextest bacon --locked"