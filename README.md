[appurl]: https://sourceforge.net/p/ddclient/wiki/Home/

# ledokun/ddclient

ddclient running on Alpine Linux, based on [linuxserver/docker-ddclient](https://github.com/linuxserver/docker-ddclient), with cURL for services like deSEC.

[DDClient][appurl] is a Perl client used to update dynamic DNS entries for accounts on Dynamic DNS Network Service Provider. It was originally written by Paul Burry and is now mostly by wimpunk. It has the capability to update more than just dyndns and it can fetch your WAN-ipaddress in a few different ways.

[![ddclient]()][appurl]

## Usage

```
docker create \
  --name=ddclient \
  -v <path to data>:/config \
  -e PGID=<gid> -e PUID=<uid>  \
  -e TZ=<Timezone> \
  ledokun/ddclient
```

## Parameters

`The parameters are split into two halves, separated by a colon, the left hand side representing the host and the right the container side.
For example with a port -p external:internal - what this shows is the port mapping from internal to external of the container.
So -p 8080:80 would expose port 80 from inside the container to be accessible from the host's IP on port 8080
http://192.168.x.x:8080 would show you what's running INSIDE the container on port 80.`



* `-v /config` - Where ddclient should store its config files
* `-e PGID` for GroupID - see below for explanation
* `-e PUID` for UserID - see below for explanation
* `-e TZ` - for timezone information *eg Europe/London, etc*

It is based on alpine linux with s6 overlay, for shell access whilst the container is running do `docker exec -it ddclient /bin/bash`.

### User / Group Identifiers

Sometimes when using data volumes (`-v` flags) permissions issues can arise between the host OS and the container. We avoid this issue by allowing you to specify the user `PUID` and group `PGID`. Ensure the data volume directory on the host is owned by the same user you specify and it will "just work" ™.

In this instance `PUID=1001` and `PGID=1001`. To find yours use `id user` as below:

```
  $ id <dockeruser>
    uid=1001(dockeruser) gid=1001(dockergroup) groups=1001(dockergroup)
```

## Setting up the application

Edit the ddclient.conf file found in your /config volume. This config file has many providers to choose from and you basically just have to uncomment your provider and add username/password where requested. If you modify ddclient.conf, ddclient will automaticcaly restart and read the config.

## Info

* Shell access whilst the container is running: `docker exec -it ddclient /bin/bash`
* To monitor the logs of the container in realtime: `docker logs -f ddclient`

* container version number

`docker inspect -f '{{ index .Config.Labels "build_version" }}' ddclient`

* image version number

`docker inspect -f '{{ index .Config.Labels "build_version" }}' ledokun/ddclient`
