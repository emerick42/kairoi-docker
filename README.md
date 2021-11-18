# Kairoi-Docker

The Docker image packager for Kairoi.

## What is Kairoi?

> Kairoi is a Dynamic, Accurate and Scalable Time-based Job Scheduler written in Rust.

You can read more about **Kairoi** on the [Kairoi Official Repository](https://github.com/emerick42/kairoi).

## TL;DR

```console
$ docker run emerick42/kairoi:latest
```

### Docker Compose

```yaml
version: '2'

services:
    kairoi:
        image: emerick42/kairoi:latest
        ports:
            - '5678:5678'
        volumes:
            - 'persisted_data:/var/lib/kairoi'
```

## Usage

The recommended way to get the Kairoi Docker image is to pull the prebuilt image from the [Docker Hub Registry](https://hub.docker.com/r/emerick42/kairoi).

```console
$ docker pull emerick42/kairoi:latest
```

You should always use a specific version with a versioned tag. You can view the [list of available versions](https://hub.docker.com/r/emerick42/kairoi/tags/) in the Docker Hub Registry. For example, to get the `0.1.0-alpha`, you can:

```console
$ docker pull emerick42/kairoi:0.1.0-alpha
```

### Configuration

Kairoi uses a `configuration.toml` file for configuration. This file is read at startup by the software. You can use your own configuration file by mounting a volume containing a `configuration.toml` file.

```console
$ touch /path/to/data/configuration.toml
$ docker run -v /path/to/data:/var/lib/kairoi emerick42/kairoi:latest
```

### Data Persistence

In the default configuration, if you remove the container, all your data and configurations will be lost. To avoid this loss of data, you should mount a volume that will persist even after the container is removed.

The image exposes a volume at `/var/lib/kairoi`, containing both the `configuration.toml` file and all persisted data (`logfile`, `logfile.compressed`, etc). If the mounted directory is empty, it will be initialized on the first run.

```console
$ docker run -v /path/to/data:/var/lib/kairoi emerick42/kairoi:latest
```
