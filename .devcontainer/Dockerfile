# pinned to Debian Bookworm — stable base
FROM mcr.microsoft.com/devcontainers/rust:1.83-bookworm

# Rustlings needs these
RUN rustup component add clippy rustfmt

# Install rustlings (v6+)
RUN cargo install rustlings

# Keep container lean
RUN rm -rf /usr/local/cargo/registry/cache \
    && rm -rf /tmp/*

USER vscode
WORKDIR /home/vscode
