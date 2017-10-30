[bristleurl]: https://bristle.io
[githuburl]: https://github.com/bristleio/plexpy
[app]: plexpy
[appurl]: https://github.com/JonnyWong16/plexpy/
[hub]: https://hub.docker.com/r/bristleio/plexpy/
[lsiorepo]: https://github.com/linuxserver/docker-plexpy-armhf

# [bristle.io][bristleurl]

The [bristle.io][bristleurl] team has created a fork of [LinuxServer.io][lsiorepo]'s container release of [Plexpy][appurl]

# bristleio/plexpy
[![Version](https://img.shields.io/github/tag/bristleio/docker-plexpy-armhf.svg)][githuburl][![Docker Pulls](https://img.shields.io/docker/pulls/bristleio/plexpy.svg)][hub][![Docker Stars](https://img.shields.io/docker/stars/bristleio/plexpy.svg)][hub][![Build Automated](https://img.shields.io/docker/automated/bristleio/plexpy.svg)][hub][![Build Status](https://img.shields.io/docker/automated/bristleio/plexpy.svg)][hub]

[Plexpy][appurl] Is a Python-based Plex Usage tracker, that is currently in active development.


## Usage

```
docker create \
  --name=plexpy \
  -v <path to data>:/config \
  -v <path to plexlogs>:/logs:ro \
  -e PGID=<gid> -e PUID=<uid>  \
  -e TZ=<timezone> \
  -p 8181:8181 \
  bristleio/plexpy
```

## Parameters

`The parameters are split into two halves, separated by a colon, the left hand side representing the host and the right the container side.
For example with a port -p external:internal - what this shows is the port mapping from internal to external of the container.
So -p 8080:80 would expose port 80 from inside the container to be accessible from the host's IP on port 8080
http://192.168.x.x:8080 would show you what's running INSIDE the container on port 80.`


* `-p 8181` - Port for webui
* `-v /config` Containes plexpy config and database
* `-v /logs` Map this to PLex Media servers log directory - bonus points for mapping RO
* `-e PGID` for GroupID - see below for explanation
* `-e PUID` for UserID - see below for explanation
* `-e TZ` for setting timezone information, eg Europe/London

It is based on alpine linux with s6 overlay, for shell access whilst the container is running do `docker exec -it plexpy /bin/bash`.

### User / Group Identifiers

Sometimes when using data volumes (`-v` flags) permissions issues can arise between the host OS and the container. We avoid this issue by allowing you to specify the user `PUID` and group `PGID`. Ensure the data volume directory on the host is owned by the same user you specify and it will "just work" ™.

In this instance `PUID=1001` and `PGID=1001`. To find yours use `id user` as below:

```
  $ id <dockeruser>
    uid=1001(dockeruser) gid=1001(dockergroup) groups=1001(dockergroup)
```

## Setting up the application
`IMPORTANT... THIS IS THE ARMHF VERSION`

Access the webui at `<your-ip>:8181`, for more information check out [Plexpy][appurl].

## Info

* To monitor the logs of the container in realtime `docker logs -f plexpy`.

* container version number

`docker inspect -f '{{ index .Config.Labels "build_version" }}' plexpy`

* image version number

`docker inspect -f '{{ index .Config.Labels "build_version" }}' bristleio/plexpy`


## Versions

Versions are tagged and released whenever there is an update of the [Application Branch][appurl] that we watch. Please reach out to us if you see isssues.
