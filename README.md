# [warhorse/cobaltstrike-ag](https://github.com/war-horse/docker-cobaltstrike-ag)
[![GitHub Release](https://img.shields.io/github/release/war-horse/docker-cobaltstrike.svg?style=flat-square&color=E68523)](https://github.com/war-horse/docker-cobaltstrike-ag/releases)
[![MicroBadger Layers](https://img.shields.io/microbadger/layers/warhorse/cobaltstrike-ag.svg?style=flat-square&color=E68523)](https://microbadger.com/images/warhorse/cobaltstrike-ag "Get your own version badge on microbadger.com")
[![MicroBadger Size](https://img.shields.io/microbadger/image-size/warhorse/cobaltstrike-ag.svg?style=flat-square&color=E68523)](https://microbadger.com/images/warhorse/cobaltstrike-ag "Get your own version badge on microbadger.com")
[![Docker Pulls](https://img.shields.io/docker/pulls/warhorse/cobaltstrike-ag.svg?style=flat-square&color=E68523)](https://hub.docker.com/r/warhorse/cobaltstrike)
[![Docker Stars](https://img.shields.io/docker/stars/warhorse/cobaltstrike-ag.svg?style=flat-square&color=E68523)](https://hub.docker.com/r/warhorse/cobaltstrike-ag)

[Cobaltstrike](https://www.cobaltstrike.com/) - Software for Adversary Simulations and Red Team Operations.


![Cobaltstrike](https://www.cobaltstrike.com/images/logo.png)

## WARNING

This image is for server side AGGRESSOR scripts. You will need a running Cobaltstrike server to use this image.

You need a valid Cobaltstrike key to use this image. The Cobaltstrike software is downloaded when this image is started. If you need a license please go to [Cobaltstrike](https://www.cobaltstrike.com/)

## Usage

Here are some example snippets to help you get started creating a container.

### docker

```
docker create \
  --name=coblatstrike-ag \
  -e TZ=Europe/London \
  -e COBALTSTRIKE_KEY=cs_key \
  -e COBALTSTRIKE_PASS=cs_password \
  -e COBALTSTRIKE_HOSTNAME=cobaltstrike.mydomain.com \
  -e AG_SCRIPT_NAME=script.cna \
  -v <path to data>:/opt/cobaltstrike \
  --restart unless-stopped \
  warhorse/cobaltstrike-ag
```

### docker-compose

Compatible with docker-compose v2 schemas. Server and AG server example.

```
---
version: "2"
services:
  cobaltstrike:
    image: warhorse/cobaltstrike
    container_name: cobaltstrike
    environment:
      - TZ=Europe/London
      - COBALTSTRIKE_KEY=cs_key
      - COBALTSTRIKE_PASS=cs_password
      - COBALTSTRIKE_EXP=2020-12-20
      - COBALTSTRIKE_PROFILE=malleable.profile
    volumes:
      - <path to data>:/opt/cobaltstrike
    ports:
      - 50050:50050
      - 443:443
      - 80:80
    restart: unless-stopped
  cobaltstrike-ag:
    image: warhorse/cobaltstrike-ag
    container_name: cobaltstrike-ag
    environment:
      - TZ=Europe/London
      - COBALTSTRIKE_KEY=cs_key
      - COBALTSTRIKE_PASS=cs_password
      - COBALTSTRIKE_HOSTNAME=cobaltstrike.mydomain.com
      - AG_SCRIPT_NAME=script.cna
    volumes:
      - <path to data>:/opt/cobaltstrike
    restart: unless-stopped
```

## Parameters

Container images are configured using parameters passed at runtime (such as those above). These parameters are separated by a colon and indicate `<external>:<internal>` respectively. For example, `-p 8080:80` would expose port `80` from inside the container to be accessible from the host's IP on port `8080` outside the container.

| Parameter | Function |
| :----: | --- |
| `-e TZ=Europe/London` | Specify a timezone to use EG Europe/London|
| `-e COBALTSTRIKE_KEY=cs_key` | Specify a valid Cobaltstrike key|
| `-e COBALTSTRIKE_PASS=cs_password` | Specify a Cobaltstrike password|
| `-e COBALTSTRIKE_HOSTNAME=cobaltstrike.mydomain.com` | Specify a cobaltstrike hostname|
| `-e AG_SCRIPT_NAME=script.cna` | Specify a cobaltstrike AGGRESSOR script name|
| `-v /opt/cobaltstrike` | Cobaltstrike data folder |

&nbsp;
## Application Setup

This setup is completely server side and as such there is no interface.

## Support Info

* Shell access whilst the container is running: `docker exec -it cobaltstrike-ag /bin/bash`
* To monitor the logs of the container in realtime: `docker logs -f cobaltstrike-ag`

## Building locally

If you want to make local modifications to these images for development purposes or just to customize the logic:
```
git clone https://github.com/warhorse/docker-cobaltstrike-ag.git
cd docker-cobaltstrike-ag
docker build \
  --no-cache \
  --pull \
  -t warhorse/cobaltstrike-ag:latest .
```
## Versions

* **10.31.19:** - First Push