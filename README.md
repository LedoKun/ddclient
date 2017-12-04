# ddclient
ddclient running on Alpine Linux, based on linuxserver/docker-ddclient, with cURL for services like deSEC.

## Usage
```
docker create \
  --name=ddclient \
  -v <path to data>:/config \
  -e PGID=<gid> -e PUID=<uid>  \
  -e TZ=<Timezone> \
  ledokun/ddclient
```
