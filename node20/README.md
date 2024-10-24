---
display_name: Docker Containers
description: Provision Docker containers as Coder workspaces
icon: ../../../site/static/icon/docker.png
maintainer_github: coder
verified: true
tags: [docker, container]
---

# Basic Node 20 Dev Template for Coder

## Description

- Node 20
- Postgres Client library
- Development essentials
    - Build essentials
    - SSL libs
    - Git
    - Wget2
    - curl
    - dig
    - ping
    - Python3 and pip

## Usage

`coder login`

`coder templates push -d . -y`


Login to your Coder instance and create a new workspace from this template, or update an existing one


## Prerequisites

### Infrastructure

The VM you run Coder on must have a running Docker socket and the `coder` user must be added to the Docker group:

```sh
# Add coder user to Docker group
sudo adduser coder docker

# Restart Coder server
sudo systemctl restart coder

# Test Docker
sudo -u coder docker ps
```

## Architecture

This template provisions the following resources:

- Docker image (built by Docker socket and kept locally)
- Docker container pod (ephemeral)
- Docker volume (persistent on `/home/coder`)

This means, when the workspace restarts, any tools or files outside of the home directory are not persisted. To pre-bake tools into the workspace (e.g. `python3`), modify the container image. Alternatively, individual developers can [personalize](https://coder.com/docs/dotfiles) their workspaces with dotfiles.

> **Note**
> This template is designed to be a starting point! Edit the Terraform to extend the template to support your use case.

### Editing the image

Edit the `Dockerfile` and run `coder templates push` to update workspaces.
