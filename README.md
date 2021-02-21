

# [studioetrange/calibre-mod](https://github.com/studioetrange/docker-calibre-mod)


calibre-mod **is not a standalone container** but an additional docker layer for linuxserver.io's containers which adds the binaries and dependencies necessary to enable ebook conversion on x86-64 utilising Calibre.

## About this fork

* This is a fork of a calibre-web mod [linuxserver/calibre-web:calibre](https://github.com/linuxserver/docker-calibre-web/tree/calibre)
* Can create an empty calibre database in a specified folder, if you don't have any at startup
* Set some default settings for calibre binary
* For each calibre version match a calibre-mod version
* some ideas taken from [technosoft2000/calibre-web](https://github.com/Technosoft2000/docker-calibre-web) and from [thraxis/lazylibrarian-calibre](https://github.com/Thraxis/docker-lazylibrarian-calibre)

## About linuxserver.io docker-mods

* see https://github.com/linuxserver/docker-mods
* see https://github.com/linuxserver/docker-baseimage-ubuntu/blob/bionic/root/docker-mods



## Supported Architectures

Our images support multiple architectures such as `x86-64`, `arm64` and `armhf`. We utilise the docker manifest for multi-platform awareness. More information is available from docker [here](https://github.com/docker/distribution/blob/master/docs/spec/manifest-v2-2.md#manifest-list) and our announcement [here](https://blog.linuxserver.io/2019/02/21/the-lsio-pipeline-project/). 

Simply pulling `linuxserver/calibre-web` should retrieve the correct image for your arch, but you can also pull specific arch images via tags.

The architectures supported by this image are:

| Architecture | Tag |
| :----: | --- |
| x86-64 | amd64-latest |


## Parameters

Container images are configured using parameters passed at runtime (such as those above). These parameters are separated by a colon and indicate `<external>:<internal>` respectively. For example, `-p 8080:80` would expose port `80` from inside the container to be accessible from the host's IP on port `8080` outside the container.

| Parameter | Function |
| :----: | --- |
| `-e AUTO_CREATE_DB=/books` | Will put an empty calibre database in this folder if not already exist. # optional |
| `-e CALIBRE_CONFIG_DIRECTORY=/config/calibre` | calibre folder  # optional |
| `-e CALIBRE_TEMP_DIR=/config/calibre/tmp` | calibre folder  # optional |
| `-e CALIBRE_CACHE_DIRECTORY=/config/cache/calibre` | calibre folder  # optional |


## Usage



Here are some example snippets to help you get started creating a Calibre-Web container using this mod.


### docker sample usage



```
docker create \
  --name=calibre-web \
  -e PUID=1000 \
  -e PGID=1000 \
  -e TZ=Europe/London \
  -e DOCKER_MODS=studioetrange/calibre-mod:latest \
  -e AUTO_CREATE_DB=/books \
  -e CALIBRE_CONFIG_DIRECTORY=/config/calibre \
  -e CALIBRE_TEMP_DIR=/config/calibre/tmp \
  -e CALIBRE_CACHE_DIRECTORY=/config/cache/calibre \
  -p 8083:8083 \
  -v <path to data>:/config \
  -v <path to calibre library>:/books \
  --restart unless-stopped \
  linuxserver/calibre-web
```


### docker-compose sample usage

Compatible with docker-compose v2 schemas.

```
---
version: "2"
services:
  calibre-web:
    image: linuxserver/calibre-web
    container_name: calibre-web
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Europe/London
      - DOCKER_MODS=studioetrange/calibre-mod:latest
      - AUTO_CREATE_DB=/books
      - CALIBRE_CONFIG_DIRECTORY=/config/calibre
      - CALIBRE_TEMP_DIR=/config/calibre/tmp
      - CALIBRE_CACHE_DIRECTORY=/config/cache/calibre
    volumes:
      - <path to data>:/config
      - <path to calibre library>:/books
    ports:
      - 8083:8083
    restart: unless-stopped
```

## Docker tags

Pre-setted buildable tags for studioetrange/calibre-mod:__TAG__

	 latest, v5.11.0, v5.10.1, v5.10.0, v5.9.0, v5.8.1, v5.8.0, v5.7.2, v5.7.1, v5.7.0, v5.6.0, v5.5.0, v5.4.2, v5.4.1, v5.4.0, v5.3.0, v5.2.0, v5.1.0, v5.0.1, v5.0.0, v4.23.0, v4.22.0, v4.21.0, v4.20.0, v4.19.0, v4.18.0, v4.17.0, v4.16.0, v4.15.0, v4.14.0, v4.13.0, v4.12.0, v4.11.2, v4.11.1, v4.11.0, v4.10.1, v4.10.0, v4.9.1, v4.9.0, v4.8.0, v4.7.0, v4.6.0, v4.5.0, v4.4.0, v4.3.0, v4.2.0, v4.1.0, v4.0.0, v3.48.0, v3.47.1

Current latest tag is version __v5.11.0__



## Building locally

If you want to make local modifications to these images for development purposes or just to customize the logic: 
```
git clone https://github.com/studioetrange/docker-calibre-mod.git
cd docker-calibre-mod
docker build \
  --no-cache \
  --pull \
  -t studioetrange/calibre-mod .
```

But to use it with calibre-web you have to upload it to docker hub first:
```
docker push studioetrange/calibre-mod:latest
```



## Notes on Github / Docker Hub Repository

* This github repository is linked to an automated build in docker hub registry.

	https://registry.hub.docker.com/u/studioetrange/docker-calibre-mod/

* _update.sh_ is only an admin script for this project which update and add new versions. This script do not auto create missing tag in docker hub webui. It is only for this project admin/owner purpose.
