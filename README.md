# PowerDNS Recursor Docker Image

[![](https://images.microbadger.com/badges/version/xyzxyz442/docker-pdns-recursor.svg)](https://microbadger.com/images/xyzxyz442/pdns-recursor "Get your own version badge on microbadger.com") [![](https://images.microbadger.com/badges/image/xyzxyz442/docker-pdns-recursor.svg)](https://microbadger.com/images/xyzxyz442/pdns-recursor "Get your own image badge on microbadger.com")

[![](https://images.microbadger.com/badges/version/xyzxyz442/docker-pdns-recursor:alpine.svg)](https://microbadger.com/images/xyzxyz442/pdns-recursor:alpine "Get your own version badge on microbadger.com") [![](https://images.microbadger.com/badges/image/xyzxyz442/docker-pdns-recursor:alpine.svg)](https://microbadger.com/images/xyzxyz442/pdns-recursor:alpine "Get your own image badge on microbadger.com")

This repository is a splitting `pdns-recursor` subfolder from https://github.com/pschiffe/docker-pdns

Image are available on Docker Hub:

https://hub.docker.com/r/xyzxyz442/pdns-recursor/

Docker image with [PowerDNS 4.1.x recursor](https://www.powerdns.com/).

PowerDNS recursor is configurable via env vars. Every variable starting with `PDNS_` will be inserted into `/etc/pdns/recursor.conf` conf file in the following way: prefix `PDNS_` will be stripped and every `_` will be replaced with `-`. For example, from above mysql config, `PDNS_gmysql_host=mysql` will became `gmysql-host=mysql` in `/etc/pdns/recursor.conf` file. This way, you can configure PowerDNS recursor any way you need within a `docker run` command.

You can find [here](https://doc.powerdns.com/recursor/settings.html) all available settings.

### Examples

Recursor server is use as a front for forwarding private zones to a internal authoritative server or resolve not-exists with external dns server like Google DNS.
```
docker run -d -p 53:53 -p 53:53/udp --name pdns-recursor \
  -e PDNS_forward_zones=.=172.27.0.11;172.27.0.12;8.8.8.8;8.8.4.4
  -e PDNS_forward_zones_recurse=.=172.27.0.11;172.27.0.12;8.8.8.8;8.8.4.4
  xyzxyz442/pdns-recursor
```
