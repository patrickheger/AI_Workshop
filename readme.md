# AI Exploration Workshop | Practical Part

> AI Exploration Workshop  
> Practical Part  
> 2025  
> 
> Patrick Heger & Jan Rother  

## Table of Contents

<!-- TOC -->
- [AI Exploration Workshop | Practical Part](#ai-exploration-workshop--practical-part)
  - [Table of Contents](#table-of-contents)
  - [Introduction](#introduction)
  - [Setting up a local Python Installation](#setting-up-a-local-python-installation)
  - [Setting up a Development Container](#setting-up-a-development-container)
    - [DevContainer](#devcontainer)
    - [Getting Started locally](#getting-started-locally)
      - [Prerequisites](#prerequisites)
      - [Getting the Docker Image](#getting-the-docker-image)
      - [Starting the Development Container](#starting-the-development-container)
    - [Getting Started in the Cloud](#getting-started-in-the-cloud)
      - [Prerequisites](#prerequisites-1)
      - [Starting a Code Space](#starting-a-code-space)
    - [Adjust to every Need](#adjust-to-every-need)
    - [Compatibility](#compatibility)
  - [Starting the Coding Session](#starting-the-coding-session)
    - [Configuring a Python Virtual Environment](#configuring-a-python-virtual-environment)
    - [Creating the Kernel for Jupyter Notebooks](#creating-the-kernel-for-jupyter-notebooks)
    - [Starting Jupyter Notebooks](#starting-jupyter-notebooks)
<!-- TOC -->

-----

## Introduction

The **AI Workshop** is meant to serve as a brief introduction into the technical world of Artificial Intelligence.

## Setting up a local Python Installation

The local installation of this project is currently not intended.

## Setting up a Development Container

### DevContainer

A *DevContainer* allows developers to define a development environment in a container. This leads to a consistent development environment across different machines and therefore simplifies the setup process while also reducing dependencies on the host system. Some of the most relevant Integrated Development Environments (IDEs) already support the use of *DevContainers*:

- **Visual Studio Code**: [Developing inside a Container](https://code.visualstudio.com/docs/devcontainers/containers)
- **JetBrains IntelliJ**: [DevContainers](https://www.jetbrains.com/help/idea/connect-to-devcontainer.html)

Any configuration regarding the development container is stored in the `./.devcontainer/` directory. It must not be removed.

### Getting Started locally

#### Prerequisites

To use the *DevContainer* feature, the following software has to be installed on the host system:

- To clone the repository, a **GIT client** is required.
- For containerizing the development environment, **Docker Desktop** has to be installed via [docker.com](https://www.docker.com/products/docker-desktop/) or by using `winget install -e --id Docker.DockerDesktop`.
- An **Editor or IDE** as described in the [DevContainer](#devcontainer) section for accessing the development container is required:
  - **Visual Studio Code** can be downloaded at [code.visualstudio.com](https://code.visualstudio.com/download) or directly installed via `winget install -e --id Microsoft.VisualStudioCode`.
  - **JetBrains IntelliJ** is recommended to be installed using the [JetBrains Toolbox](https://www.jetbrains.com/toolbox-app/download/).

As of now, it is recommended to use either *Visual Studio Code* or *GitHub Codespaces* to access the development container. Other IDEs are currently adopting this technology, but still have to catch up. 

#### Getting the Docker Image

A Docker Image is already configured and can be used to start a development environment right away or to include it as base image in a custom Dockerfile. The image is build from the `Dockerfile` located in the `.devcontainer` directory.

To use the Docker Image directly, run

```shell
docker build -t python -f .\Dockerfile .
```

and

```shell
docker run -it python
```

#### Starting the Development Container

1. Before starting the development container, ensure that the *Docker Engine* is running on the host system.
2. Clone your fork of the repository to your local machine using `git clone <your-fork-url>`.
3. Open the repository as new project in your preferred IDE or editor.
4. If the editor supports *DevContainers*, a notification should appear to reopen the project in a container.
5. The editor will build the container and open the project in the development container.

### Getting Started in the Cloud

#### Prerequisites

To use the *DevContainer* remotely, no software has to be installed on the host system. Other requirements have to be met:

- A **GitHub account** at [github.com](https://github.com/) has to be created.
- A **GitHub repository** containing the toolchain, especially the `.devcontainer` directory, has to be created.

#### Starting a Code Space

1. Open the repository in the browser and click on the `Code` button.
2. Select `Codespaces` from the dropdown menu.
3. Click on `Create Codespace on Main` to create a new code space.
4. The code space will be created and opened in the browser.
5. After the *DevContainer* is built, the development environment is available right in the browser.

> **Note**:  
> *Visual Studio Code* provides an option to connect to a *DevContainer* in the cloud.  
> Therefore, the *GitHub Codespaces* extension has to be installed in the editor.

### Adjust to every Need

The *DevContainer* can be adjusted to every need. The `Dockerfile` defines the base image and the tools installed in the container. The `devcontainer.json` file defines the settings for the development container, thus shaping the development environment.

It is recommended to leave the `Dockerfile` as-is. It uses the `python` image from [hub.docker.com](https://hub.docker.com/_/python) as base image and configures it for the *Python* environment using *Poetry*. Specifiers can easily be modified using `ARG` variables.

If changes to the development environment are necessary, the `devcontainer.json` file can be adjusted. It uses the image created by the `Dockerfile` and defines the settings for the development container. Besides its behavior, precise settings for the editor `vscode` or the IDEs `jetbrains` can be defined. The `extensions` array can be used to install additional extensions in the development container.

The *DevContainer* provides a pre-configured ZSH shell. It can be further customized by adjusting the `.zshrc` file. The `starship.toml` file can be used to configure the prompt of the shell.

### Compatibility

If after initial creation of a project, a higher compatibility should be achieved, the base images and packages used should be pinned to a specific version.

## Starting the Coding Session

### Configuring a Python Virtual Environment

To configure the Python Virtual Environment (VENV), the package manager *Poetry* is used.

Ensure the correct installation of *Poetry* by running

```shell
poetry --version
```

If the command returns a version number, *Poetry* is installed correctly. If not, the installation can be done by running

```shell
python -m pip install poetry
```

In *Poetry*, dependencies are managed in the `pyproject.toml` file. To install the dependencies, run

```shell
poetry install --no-root
```

To get the path to the virtual environment, run

```shell
poetry env info --path
```

The result of this command can be used to activate the virtual environment by running

```shell
source <path-to-venv>/bin/activate
```

The virtual environment is now activated and can be used.

### Creating the Kernel for Jupyter Notebooks

To create a kernel for Jupyter Notebooks, the following command has to be run:

```shell
ipython kernel install --name "python-venv" --user
```

This command creates a kernel named `python-venv` that can be used in Jupyter Notebooks. The kernel is based on the virtual environment created by *Poetry*.

### Starting Jupyter Notebooks

Now, the Jupyter Notebooks can be used.

**Have fun!**
