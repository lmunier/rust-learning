# pinned to Debian Bookworm — stable base
FROM rust:1.94-slim

# Core dev tools
RUN apt-get update && apt-get install -y --no-install-recommends \
        git \
        sudo \
        ca-certificates \
        curl \
        wget \
        build-essential \
        pkg-config \
        libssl-dev \
        openssh-client \
        bash-completion \
        locales \
        procps \
        lsb-release \
        less \
        nano \
        vim \
    && rm -rf /var/lib/apt/lists/* \
    # Generate locale
    && sed -i '/en_US.UTF-8/s/^# //g' /etc/locale.gen \
    && locale-gen

ENV LANG=en_US.UTF-8

# Create non-root user
RUN groupadd --gid 1000 vscode \
    && useradd --uid 1000 --gid 1000 -m -s /bin/bash vscode \
    && echo "vscode ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers.d/vscode \
    && chmod 0440 /etc/sudoers.d/vscode

# Rust tooling (as root so all users get it)
RUN rustup component add clippy rustfmt rust-analyzer \
    && cargo install rustlings \
    && rm -rf /usr/local/cargo/registry/cache /tmp/*

# Let vscode user access cargo/rustup
RUN chmod -R a+r /usr/local/cargo /usr/local/rustup

USER vscode
WORKDIR /home/vscode

