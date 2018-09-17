# PowerDNS Recursor Docker Image

[![](https://images.microbadger.com/badges/version/xyzxyz442/docker-pdns-recursor.svg)](https://microbadger.com/images/xyzxyz442/docker-pdns-recursor "Get your own version badge on microbadger.com") [![](https://images.microbadger.com/badges/image/xyzxyz442/docker-pdns-recursor.svg)](https://microbadger.com/images/xyzxyz442/docker-pdns-recursor "Get your own image badge on microbadger.com")

[![](https://images.microbadger.com/badges/version/xyzxyz442/docker-pdns-recursor:alpine.svg)](https://microbadger.com/images/xyzxyz442/docker-pdns-recursor:alpine "Get your own version badge on microbadger.com") [![](https://images.microbadger.com/badges/image/xyzxyz442/docker-pdns-recursor:alpine.svg)](https://microbadger.com/images/xyzxyz442/docker-pdns-recursor:alpine "Get your own image badge on microbadger.com")

This repository is a splitting `pdns-recursor` subfolder from https://github.com/pschiffe/docker-pdns

Image are available on Docker Hub:

https://hub.docker.com/r/xyzxyz442/docker-pdns-recursor/

Docker image with [PowerDNS 4.1.x recursor](https://www.powerdns.com/).

PowerDNS recursor is configurable via env vars. Every variable starting with `PDNS_` will be inserted into `/etc/pdns/recursor.conf` conf file in the following way: prefix `PDNS_` will be stripped and every `_` will be replaced with `-`. For example, from above mysql config, `PDNS_gmysql_host=mysql` will became `gmysql-host=mysql` in `/etc/pdns/recursor.conf` file. This way, you can configure PowerDNS recursor any way you need within a `docker run` command.

You can find [here](https://doc.powerdns.com/recursor/settings.html) all available settings.

### Examples

Recursor server with API enabled:
```
docker run -d -p 53:53 -p 53:53/udp --name pdns-recursor \
  -e PDNS_api=yes \
  -e PDNS_api_key=secret \
  -e PDNS_webserver=yes \
  -e PDNS_webserver_address=0.0.0.0 \
  -e PDNS_webserver_password=secret2 \
  pschiffe/pdns-recursor
```
