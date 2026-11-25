<div align="center">

# docker-playground

**An experiment with Docker: an nginx web server image built on Ubuntu (2016).**

[![Tool: Docker](https://img.shields.io/badge/tool-Docker-2496ED)](ubuntu-nginx/Dockerfile)
[![Base image: ubuntu](https://img.shields.io/badge/base%20image-ubuntu-E95420)](ubuntu-nginx/Dockerfile)
[![Server: nginx](https://img.shields.io/badge/server-nginx-009639)](ubuntu-nginx/nginx.conf)
[![Year: 2016](https://img.shields.io/badge/year-2016-informational)](#history)
[![License: MIT](https://img.shields.io/badge/license-MIT-green)](LICENSE)

</div>

## Table of contents

- [About](#about)
- [What the image does](#what-the-image-does)
- [Status](#status)
- [Repository layout](#repository-layout)
- [History](#history)
- [License](#license)

## About

This repository holds a small Docker image definition written while trying out Docker: an Ubuntu container that
installs nginx, replaces its main configuration file and starts it. A one-line HTML page sits next to it.

## What the image does

[`ubuntu-nginx/Dockerfile`](ubuntu-nginx/Dockerfile), step by step:

| Instruction | Effect |
|---|---|
| `FROM ubuntu` | starts from the official Ubuntu image, with no version tag |
| `RUN apt-get install -y nginx` | installs nginx from the Ubuntu packages |
| `COPY nginx.conf /etc/nginx/nginx.conf` | replaces nginx's main configuration with the one in this folder |
| `EXPOSE 80 443` | declares the HTTP and HTTPS ports |
| `CMD ["nginx"]` | starts nginx when the container starts |

[`ubuntu-nginx/nginx.conf`](ubuntu-nginx/nginx.conf) is a general-purpose configuration with commented
optional sections: 4 worker processes, `sendfile`, gzip compression, access and error logs under
`/var/log/nginx/`, and virtual hosts loaded from
[`conf.d/` and `sites-enabled/`](ubuntu-nginx/nginx.conf#L71). The mail proxy and the naxsi and passenger sections
are commented out.

[`volume/index.html`](volume/index.html) is a "Hello world!" page, kept in a folder named `volume/`: it is not
copied into the image, the way to serve it being to share the folder with the container as a Docker volume.

## Status

This is an experiment kept as it was from 2016; it has not been rebuilt for this README, and the repository holds
no build or run script. The base image has no version tag, so a new build starts from the current `ubuntu` image.

## Repository layout

```
.
├── ubuntu-nginx/
│   ├── Dockerfile     image definition
│   └── nginx.conf     nginx main configuration copied into the image
├── volume/
│   └── index.html     "Hello world!" page
├── README.md
└── LICENSE
```

## History

Four commits on 29 March 2016: the first Dockerfile, a switch of the start command to `/bin/bash` and back to
`nginx`, the "Hello world!" page, then the custom `nginx.conf`.

## License

Released under the [MIT License](LICENSE). © 2016 Erwan Rouzel.
