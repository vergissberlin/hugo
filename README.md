# hugo

> Slim alpine image with hugo inside and nothing more!

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
