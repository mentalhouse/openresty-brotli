
Dockerfiles for building libnginx-mod-brotli for Debian / Ubuntu

If you want to build packages by yourself, this is for you :

DCH Dockerfile usage (always use stretch as it is replaced before build) :

```bash
docker build -t deb-dch -f Dockerfile-deb-dch .
docker run -it -v $PWD:/local -e HOME=/local deb-dch bash -c 'cd /local && \
dch -M -v 1.0.9+openresty-1.19.3.1-1~stretch1 --distribution "stretch" "Updated upstream."'
```

Build Dockerfile usage :

```bash
docker build -t build-openresty-brotli -f Dockerfile-deb \
--build-arg DISTRIB=debian --build-arg RELEASE=stretch \
--build-arg NGINX_VERSION=1.18.0 .
```

Or for Ubuntu :
```bash
docker build -t build-openresty-brotli -f Dockerfile-deb \
--build-arg DISTRIB=ubuntu --build-arg RELEASE=bionic \
--build-arg NGINX_VERSION=1.18.0 .
```

Then :
```bash
docker run build-openresty-brotli
docker cp $(docker ps -l -q):/src ~/Downloads/
```

And once you don't need it anymore :
```bash
docker rm $(docker ps -l -q)
```

Latest Brotli version : https://github.com/google/brotli/releases

Latest ngx_brotli version : https://github.com/google/ngx_brotli

Get latest nginx version : https://nginx.org/en/download.html
Or :
```bash
curl -s https://openresty.org/package/debian/pool/openresty/o/openresty/ |grep '"openresty_' | sed -n "s/^.*\">nginx_\(.*\)\~.*$/\1/p" |sort -Vr |head -1| cut -d'-' -f1
```
