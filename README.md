[linuxserverurl]: https://linuxserver.io
[forumurl]: https://forum.linuxserver.io
[ircurl]: https://www.linuxserver.io/irc/
[podcasturl]: https://www.linuxserver.io/podcast/
[appurl]: https://github.com/Radarr/Radarr
[hub]: https://hub.docker.com/r/lsioarmhf/radarr/

[![linuxserver.io](https://raw.githubusercontent.com/linuxserver/docker-templates/master/linuxserver.io/img/linuxserver_medium.png)][linuxserverurl]

The [LinuxServer.io][linuxserverurl] team brings you another container release featuring easy user mapping and community support. Find us for support at:
* [forum.linuxserver.io][forumurl]
* [IRC][ircurl] on freenode at `#linuxserver.io`
* [Podcast][podcasturl] covers everything to do with getting the most from your Linux Server plus a focus on all things Docker and containerisation!

# lsioarmhf/radarr
[![](https://images.microbadger.com/badges/version/lsioarmhf/radarr.svg)](https://microbadger.com/images/lsioarmhf/radarr "Get your own version badge on microbadger.com")[![](https://images.microbadger.com/badges/image/lsioarmhf/radarr.svg)](https://microbadger.com/images/lsioarmhf/radarr "Get your own image badge on microbadger.com")[![Docker Pulls](https://img.shields.io/docker/pulls/lsioarmhf/radarr.svg)][hub][![Docker Stars](https://img.shields.io/docker/stars/lsioarmhf/radarr.svg)][hub][![Build Status](https://ci.linuxserver.io/buildStatus/icon?job=Docker-Builders/armhf/armhf-radarr)](https://ci.linuxserver.io/job/Docker-Builders/job/armhf/job/armhf-radarr/)

[Radarr][appurl] - A fork of Sonarr to work with movies à la Couchpotato.

[![radarr](https://raw.githubusercontent.com/linuxserver/docker-templates/master/linuxserver.io/img/radarr.png)][appurl]

## Usage

```
docker create \
  --name=radarr \
	-v <path to data>:/config \
	-v <path to data>:/downloads \
	-v <path to data>:/movies \
	-e PGID=<gid> -e PUID=<uid>  \
	-e TZ=<timezone> \
	-p 7878:7878 \
  lsioarmhf/radarr
```

You can choose between ,using tags, various branch versions of radarr, no tag is required to remain on the main branch.

Add one of the tags,  if required,  to the linuxserver/radarr line of the run/create command in the following format, linuxserver/radarr:nightly

The nightly branch and master branch can from time to time be the same version.

HOWEVER , USE THE NIGHTLY BRANCH AT YOUR OWN PERIL !!!!!!!!!

## Parameters

`The parameters are split into two halves, separated by a colon, the left hand side representing the host and the right the container side. 
For example with a port -p external:internal - what this shows is the port mapping from internal to external of the container.
So -p 8080:80 would expose port 80 from inside the container to be accessible from the host's IP on port 8080
http://192.168.x.x:8080 would show you what's running INSIDE the container on port 80.`


* `-p 7878` - the port(s)
* `-v /config` - Radarr Application Data
* `-v /downloads` - Downloads Folder
* `-v /movies` - Movie Share
* `-e PGID` for for GroupID - see below for explanation
* `-e PUID` for for UserID - see below for explanation
* `-e TZ` for timezone information, eg Europe/London

It is based on alpine linux with s6 overlay, for shell access whilst the container is running do `docker exec -it radarr /bin/bash`.

### User / Group Identifiers

Sometimes when using data volumes (`-v` flags) permissions issues can arise between the host OS and the container. We avoid this issue by allowing you to specify the user `PUID` and group `PGID`. Ensure the data volume directory on the host is owned by the same user you specify and it will "just work" ™.

In this instance `PUID=1001` and `PGID=1001`. To find yours use `id user` as below:

```
  $ id <dockeruser>
    uid=1001(dockeruser) gid=1001(dockergroup) groups=1001(dockergroup)
```

## Setting up the application
`IMPORTANT... THIS IS THE ARMHF VERSION`

Access the webui at `<your-ip>:7878`, for more information check out [Radarr][appurl].

## Info

* Shell access whilst the container is running: `docker exec -it radarr /bin/bash`
* To monitor the logs of the container in realtime: `docker logs -f radarr`

* container version number 

`docker inspect -f '{{ index .Config.Labels "build_version" }}' radarr`

* image version number

`docker inspect -f '{{ index .Config.Labels "build_version" }}' lsioarmhf/radarr`

## Versions

+ **24.02.18:** Add nightly branch.
+ **06.02.18:** Radarr repo changed owner.
+ **12.01.18:** Fix continuation lines.
+ **19.04.17:** Switch to using inhouse mono baseimage, adds python also.
+ **10.01.17:** Initial Release.
