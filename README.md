[![CircleCI](https://circleci.com/gh/bitnami/bitnami-docker-grafana/tree/master.svg?style=shield)](https://circleci.com/gh/bitnami/bitnami-docker-grafana/tree/master)

# What is Grafana?

Grafana is an open source, feature rich metrics dashboard and graph editor for Graphite, Elasticsearch, OpenTSDB, Prometheus and InfluxDB.

[https://grafana.com](https://grafana.com)

# TL;DR;

```bash
$ docker run --name grafana bitnami/grafana:latest
```

# Why use Bitnami Images?

* Bitnami closely tracks upstream source changes and promptly publishes new versions of this image using our automated systems.
* With Bitnami images the latest bug fixes and features are available as soon as possible.
* Bitnami containers, virtual machines and cloud images use the same components and configuration approach - making it easy to switch between formats based on your project needs.
* Bitnami images are built on CircleCI and automatically pushed to the Docker Hub.
* All our images are based on [minideb](https://github.com/bitnami/minideb) a minimalist Debian based container image which gives you a small base container image and the familiarity of a leading linux distribution.

# Why use a non-root container?

Non-root container images add an extra layer of security and are generally recommended for production environments. However, because they run as a non-root user, privileged tasks are typically off-limits. Learn more about non-root containers [in our docs](https://docs.bitnami.com/containers/how-to/work-with-non-root-containers/).

# Supported tags and respective `Dockerfile` links

> NOTE: Debian 8 images have been deprecated in favor of Debian 9 images. Bitnami will not longer publish new Docker images based on Debian 8.

Learn more about the Bitnami tagging policy and the difference between rolling tags and immutable tags [in our documentation page](https://docs.bitnami.com/containers/how-to/understand-rolling-tags-containers/).


* [`5-debian-9`, `5.2.4-debian-9-r6`, `5`, `5.2.4`, `5.2.4-r6`, `latest` (5/debian-9/Dockerfile)](https://github.com/bitnami/bitnami-docker-grafana/blob/5.2.4-debian-9-r6/5/debian-9/Dockerfile)
* [`5-ol-7`, `5.2.3-ol-7-r6` (5/ol-7/Dockerfile)](https://github.com/bitnami/bitnami-docker-grafana/blob/5.2.3-ol-7-r6/5/ol-7/Dockerfile)

Subscribe to project updates by watching the [bitnami/grafana GitHub repo](https://github.com/bitnami/bitnami-docker-grafana).

# Get this image

The recommended way to get the Bitnami Grafana Docker Image is to pull the prebuilt image from the [Docker Hub Registry](https://hub.docker.com/r/bitnami/grafana).

```bash
$ docker pull bitnami/grafana:latest
```

To use a specific version, you can pull a versioned tag. You can view the [list of available versions](https://hub.docker.com/r/bitnami/grafana/tags/) in the Docker Hub Registry.

```bash
$ docker pull bitnami/grafana:[TAG]
```

If you wish, you can also build the image yourself.

```bash
$ docker build -t bitnami/grafana:latest https://github.com/bitnami/bitnami-docker-grafana.git
```

# Connecting to other containers

Using [Docker container networking](https://docs.docker.com/engine/userguide/networking/), a different server running inside a container can easily be accessed by your application containers and vice-versa.

Containers attached to the same network can communicate with each other using the container name as the hostname.

## Using the Command Line

### Step 1: Create a network

```bash
$ docker network create grafana-network --driver bridge
```

### Step 2: Launch the grafana container within your network

Use the `--network <NETWORK>` argument to the `docker run` command to attach the container to the `grafana-network` network.

```bash
$ docker run --name grafana-node1 --network grafana-network bitnami/grafana:latest
```

### Step 3: Run another containers

We can launch another containers using the same flag (`--network NETWORK`) in the `docker run` command. If you also set a name to your container, you will be able to use it as hostname in your network.

# Configuration

## Dev config

Create a `custom.ini` in the conf (`/opt/bitnami/grafana/conf`) directory to override default configuration options. You only need to add the options you want to override. Config files are applied in the order of:

```
grafana.ini
custom.ini
```

In your `custom.ini` uncomment (remove the leading ;) sign. And set `app_mode = development`.

## Production config

Override the `/opt/bitnami/grafana/conf/grafana.ini` file mounting a volume.

```
docker run --name grafana-node -v /path/to/grafana.ini:/opt/bitnami/grafana/conf/grafana.ini bitnami/grafana:latest
```

After that, your configuration will be taken into account in the server's behaviour.

Using Docker Compose:

```yaml
version: '2'

services:
  grafana:
    image: bitnami/grafana:latest
    volumes:
      - /path/to/grafana.ini:/opt/bitnami/grafana/conf/grafana.ini
```

# Logging

The Bitnami grafana Docker image sends the container logs to the `stdout`. To view the logs:

```bash
$ docker logs grafana
```

You can configure the containers [logging driver](https://docs.docker.com/engine/admin/logging/overview/) using the `--log-driver` option if you wish to consume the container logs differently. In the default configuration docker uses the `json-file` driver.

# Maintenance

## Upgrade this image

Bitnami provides up-to-date versions of grafana, including security patches, soon after they are made upstream. We recommend that you follow these steps to upgrade your container.

### Step 1: Get the updated image

```bash
$ docker pull bitnami/grafana:latest
```

### Step 2: Stop and backup the currently running container

Stop the currently running container using the command

```bash
$ docker stop grafana
```

Next, take a snapshot of the persistent volume `/path/to/grafana-persistence` using:

```bash
$ rsync -a /path/to/grafana-persistence /path/to/grafana-persistence.bkp.$(date +%Y%m%d-%H.%M.%S)
```

You can use this snapshot to restore the database state should the upgrade fail.

### Step 3: Remove the currently running container

```bash
$ docker rm -v grafana
```

### Step 4: Run the new image

Re-create your container from the new image, [restoring your backup](#restoring-a-backup) if necessary.

```bash
$ docker run --name grafana bitnami/grafana:latest
```

# Contributing

We'd love for you to contribute to this container. You can request new features by creating an [issue](https://github.com/bitnami/bitnami-docker-grafana/issues), or submit a [pull request](https://github.com/bitnami/bitnami-docker-grafana/pulls) with your contribution.

# Issues

If you encountered a problem running this container, you can file an [issue](https://github.com/bitnami/bitnami-docker-grafana/issues). For us to provide better support, be sure to include the following information in your issue:

- Host OS and version
- Docker version (`docker version`)
- Output of `docker info`
- Version of this container
- The command you used to run the container, and any relevant output you saw (masking any sensitive information)

# License
Copyright 2018 Bitnami

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
