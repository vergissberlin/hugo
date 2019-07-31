![Hugo version](https://img.shields.io/badge/hugo%20version-0.56.0-informational?style=flat-square)
![Docker Cloud Build Status](https://img.shields.io/docker/cloud/build/vergissberlin/hugo?style=flat-square)
![Docker Automated build](https://img.shields.io/docker/automated/vergissberlin/hugo?style=flat-square)
![Docker Pulls](https://img.shields.io/docker/pulls/vergissberlin/hugo?style=flat-square)


# hugo

> Slim alpine image with [hugo](https://gohugo.io) and [git](https://git-scm.com) inside and nothing more!

## Usage

### The binary only

```bash
docker run -it -v $PWD:/build vergissberlin/hugo hugo
```

### On a muti stage build

```
FROM vergissberlin/hugo as build

COPY ./ /build
RUN /usr/bin/hugo

FROM nginx:alpine
LABEL maintainer André Lademann <vergissberlin@googlemail.com>

COPY ./config/nginx/default.conf /etc/nginx/conf.d/default.conf

COPY --from=build /build/public /var/www/html

WORKDIR /var/www/html
```
