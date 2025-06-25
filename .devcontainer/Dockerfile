############################################################
####### Docker Container for Python Jupyter Notebook #######
######################## DEVELOPMENT #######################
############################################################

########## AUTHOR:  Jan Rother
########## DATE:    2025-06
########## VERSION: 1.0

# |---------------------- Environment ---------------------|
ARG BASE_REPOSITORY=python
ARG BASE_IMAGE=python
ARG BASE_VERSION=3

############################################################
# |---------------------- Base Image ----------------------|
FROM ${BASE_IMAGE}:${BASE_VERSION} AS base

ARG AUTHOR="Jan Rother"
ARG DATE="2025-06"
ARG VERSION="1.0"

# |----------------------- Meta Data ----------------------|
LABEL org.opencontainers.image.author=$AUTHOR \
      org.opencontainers.image.date=$DATE \
      org.opencontainers.image.version=$VERSION \
      org.opencontainers.image.title="Python Jupyter Notebook" \
      org.opencontainers.image.description="Docker Image for  Python Jupyter Notebook development environment based on Python."

# |----------------------- Packages -----------------------|
RUN apt update && apt install -y \
    curl \
    git \
    unzip \
    zip \
    && apt clean

# |----------------- Python Dependencies ------------------|
RUN pip install \
    poetry \
    ipykernel

# |----------------------- Dotfiles -----------------------|
RUN bash -c  \
    "$(curl -#fL https://raw.githubusercontent.com/Toolchain-as-Code/tac-dotfiles/refs/heads/main/install.sh)"

# |--------------------- Customization --------------------|
# Welcome Note
COPY ./.devcontainer/resources/welcome.txt /root/welcome.txt

# Terminal: ZSH
RUN apt update && \
    apt install -y zsh fzf && \
    chsh -s /usr/bin/zsh && \
    apt clean

# Terminal: Configuration
COPY ./.devcontainer/resources/.zshrc /root/.zshrc
COPY ./.devcontainer/resources/starship.toml /root/.config/starship.toml

# Terminal: Starship Prompt
RUN curl -sS https://starship.rs/install.sh | sh -s -- -y -v latest
# Terminal: Zinit
RUN curl -sS https://raw.githubusercontent.com/zdharma-continuum/zinit/HEAD/scripts/install.sh | sh && \
    sed -i '/### End of Zinit'\''s installer chunk/d' /root/.zshrc
# Terminal: Zinit Plugins
RUN zsh -il

# |----------------------- Finalize -----------------------|

USER root

COPY . /workspace/ai-workshop

WORKDIR /workspace
ENTRYPOINT [ "/bin/zsh" ]

############################################################