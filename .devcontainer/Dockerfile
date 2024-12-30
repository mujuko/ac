FROM ubuntu:24.04

RUN apt update \
    && apt install -y git curl unzip \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

USER ubuntu
WORKDIR /workspaces

# isntall mise
RUN curl https://mise.run | sh \
    && echo 'eval "$(~/.local/bin/mise activate bash)"' >> ~/.bashrc
ENV PATH="/home/ubuntu/.local/bin:/home/ubuntu/.local/share/mise/shims:$PATH"

# install tools with mise
COPY --chown=ubuntu:ubuntu ./mise.toml .
RUN mise trust mise.toml && mise install && mise run install
ENV PATH="/home/ubuntu/.local/kotlinc/bin:$PATH"

ENV DEVCONTAINER=true
