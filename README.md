# pairing-server-container

[![Docker Hub](https://img.shields.io/badge/docker-ready-blue.svg)](https://registry.hub.docker.com/u/ahacop/pairing-server-container/) [![](https://images.microbadger.com/badges/image/ahacop/pairing-server-container.svg)](https://microbadger.com/images/ahacop/pairing-server-container "Get your own image badge on microbadger.com") [![](https://images.microbadger.com/badges/version/ahacop/pairing-server-container.svg)](https://microbadger.com/images/ahacop/pairing-server-container "Get your own version badge on microbadger.com")

Instructions for a container that provides a development environment
running Ubuntu for remote pair programming. It uses ahacop's shell and
vim configuration, but can also accomodate a different configuration to
some extent.

Access is via SSH with the account `dev`, which has sudo.

## Getting Started

Follow these steps to build the image:
```bash
$ git clone https://github.com/ahacop/pairing-server-container
$ cd pairing-server-container
$ docker build . pairing-server-container
```

## Usage

The container exposes SSH and uses [GitHub's public key
API](https://developer.github.com/v3/users/keys/) to add the keys for
authorized users to `~/.ssh/authorized_keys` for the `dev` account. You
must specify all of the allowed GitHub usernames as the
`AUTHORIZED_GH_USERS` environment variable during `docker run`.

To run:
```bash
$ docker run -d \
    -e AUTHORIZED_GH_USERS="ahacop,otherperson" \
    -p 31981:22 \
    ahacop/pairing-server-container:latest
$ ssh dev@localhost -p 31981
```

## Inspiration :bow:
This repo is inspired by and basically a fork of
[dpetersen/dev-container-base](https://github.com/dpetersen/dev-container-base).

I created this mainly because I wanted a similar container but with a
few changes.
