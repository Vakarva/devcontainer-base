# VS Code Dev Container Base Template <!-- omit in toc -->

**A simple [VS Code Dev Container](https://code.visualstudio.com/docs/devcontainers/containers) with Node.js, Python, and Zsh.**

This template creates a containerized development environment that includes both Node.js and Python runtimes, along with a configured Zsh shell. It's designed as a starting point for projects that need these languages in a consistent, reproducible environment.

## Table of Contents <!-- omit in toc -->

- [1. What's Inside?](#1-whats-inside)
- [2. Prerequisites](#2-prerequisites)
- [3. Setup](#3-setup)
  - [3.1. For new projects](#31-for-new-projects)
  - [3.2. Existing project](#32-existing-project)
  - [3.3. Font Installation](#33-font-installation)
  - [3.4. Running the Dev Container](#34-running-the-dev-container)
  - [3.5. Shutting Down the Dev Container](#35-shutting-down-the-dev-container)
- [4. You're In! Now What?](#4-youre-in-now-what)
  - [4.1. Node.js](#41-nodejs)
  - [4.2. Python](#42-python)
  - [4.3. Terminal](#43-terminal)
- [5. Customization](#5-customization)
  - [5.1. Container Configuration](#51-container-configuration)
  - [5.2. Shell Configuration](#52-shell-configuration)
- [6. Troubleshooting](#6-troubleshooting)

## 1. What's Inside?

- [Debian](https://www.debian.org)-Slim operating system
- [Git](https://git-scm.com)
- [GitHub CLI](https://cli.github.com)
- [OpenSSH](https://www.openssh.com) client (for SSH agent forwarding to use host's Git credentials)
- [curl](https://curl.se) & [Wget](https://www.gnu.org/software/wget/)
- [ca-certificates](https://packages.debian.org/sid/ca-certificates) (for secure HTTPS connections and package downloads)
- [Node.js](https://nodejs.org/) managed by [nvm](https://github.com/nvm-sh/nvm)
- [Python](https://www.python.org) managed by [uv](https://docs.astral.sh/uv/)
- [Zsh](https://www.zsh.org) with:
  - [oh my zsh](https://ohmyz.sh) with [zsh-autosuggestions](https://github.com/zsh-users/zsh-autosuggestions) and [zsh-syntax-highlighting](https://github.com/zsh-users/zsh-syntax-highlighting) plugins
  - [Powerlevel10k](https://github.com/romkatv/powerlevel10k) theme
- VS Code extensions

## 2. Prerequisites

- [Podman](https://podman.io) / [Docker](https://www.docker.com)
- [VS Code](https://code.visualstudio.com/) with [Dev Containers](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers) extension
- [MesloLGS NF](https://github.com/romkatv/powerlevel10k#fonts) font family (included in this repository for convenience; see below for installation instructions)

## 3. Setup

### 3.1. For new projects

1. Click 'Use this template' on this GitHub repository
2. Follow instructions to create your new repository

### 3.2. Existing project

1. Download the zipped repository to your local machine
2. Extract to your project root

### 3.3. Font Installation

1. Install the MesloLGS NF fonts from `.devcontainer/fonts/`, if you do not have them on your local machine:

    - **macOS**: Double-click each `.ttf` file and click "Install"
    - **Windows**: Right-click each `.ttf` file and select "Install"
    - **Linux**: Copy to `/usr/share/fonts/truetype/` and run `fc-cache -fv`

2. (Optional, but recommended): Delete the `.devcontainer/fonts/` directory

#### Q: Why are these fonts needed? <!-- omit in toc -->

We've configured the Dev Container's integrated terminal to use MesloLGS NF as the font family (which is [Powerlevel10k's recommended font](https://github.com/romkatv/powerlevel10k?tab=readme-ov-file#fonts)). VS Code can only use fonts on your local machine—so, we've got to install MesloLGS NF locally.

You can alter the font family in `.devcontainer/devcontainer.json`. If you do, you should run the `p10k configure` command in a Zsh instance (in your Dev Container) to re-set up Powerlevel10k's theme. Then rewrite the `.devcontainer/shell-config/p10k.zsh` with the new Powerlevel10k configuration (found at `/root/.p10k.zsh` in the container), so that your changes persist across container rebuilds.

### 3.4. Running the Dev Container

1. Fire up your project in VS Code (make sure the `.devcontainer` folder is at the root)
2. Open the Command Palette
3. Select `Dev Containers: Reopen in Container`

VS Code will build the container image and start the Dev Container.

*Note: Containerization platforms cache build images to save on build time. So if your Containerfile has not changed, your container will reuse the cached image. For this reason, if you have not modified your Containerfile (in particular, any instructions prior to the apt installations): at some point in the future you will notice that your Dev Container is running older versions of apt packages (which were current when the image was first built). If you'd like to use the newest ones, run `Dev Containers: Rebuild Container Without Cache` in the command palette to rebuild your Dev Container image from scratch.*

### 3.5. Shutting Down the Dev Container

You can simply close the VS Code window. This will automatically stop the container process (you can check check active containers via `podman ps` or `docker ps`).

Or you can reload your project on your local machine:

1. Open the Command Palette
2. Select `Dev Containers: Reopen Folder Locally`

## 4. You're In! Now What?

### 4.1. Node.js

By default, the latest LTS version of Node.js is installed by nvm. You can configure this by changing the NVM_VERSION arg in `.devcontainer/devcontainer.json`. You can read more about using nvm in the [nvm documentation](https://github.com/nvm-sh/nvm#readme). The `node` alias is available in the terminal.

### 4.2. Python

By default, the latest stable version of Python is installed by uv. You can configure this by modifying the `PYTHON_VERSIONS` in the `args` object in `.devcontainer/devcontainer.json`. Note that you can install multiple Python versions by separating each version by a space: (ex: `"PYTHON_VERSIONS": "3.9 3.10 3.13"`).

While nvm adds `node` directly to your PATH, uv uses a different approach in which Python runs through the `uv` command. Read more about using uv in the [uv documentation](https://docs.astral.sh/uv/).

### 4.3. Terminal

Zsh loads automatically with all enhancements active.

## 5. Customization

### 5.1. Container Configuration

Edit the following files to customize the Dev Container to your specific needs:

- `.devcontainer/Containerfile` - Add/remove packages or modify the container image

- `.devcontainer/devcontainer.json` - Configure VS Code extensions and settings

### 5.2. Shell Configuration

- `.devcontainer/shell-config/.zshrc` - Customize Zsh behavior

- `.devcontainer/shell-config/p10k.zsh` - Configure Powerlevel10k theme

## 6. Troubleshooting

**The Dev Container is super slow**: Check [VS Code's performance optimization guide](https://code.visualstudio.com/remote/advancedcontainers/improve-performance) -- This is particularly felt on Windows machines.

**Use with Podman**: Set `"dev.containers.dockerPath": "podman"` in your local machine's VS Code user settings ([official docs](https://code.visualstudio.com/remote/advancedcontainers/docker-options#_podman))

**Container won't start**: Verify that your containerization platform (Podman/Docker) is running

**VS Code integrated terminal font looks wrong**: Ensure MesloLGS NF font family is installed on your local machine
