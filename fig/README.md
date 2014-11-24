# Link container by fig

Try to link docker container by [fig](http://www.fig.sh/) within *Single* host.

## Run

```bash
$ fig run --rm cli
redis 172.17.0.42:6379> ping
PONG
```

## Link without fig

```bash
$ docker run -d --name redis crosbymichael/redis
$ docker run -it --rm --link redis:redis relateiq/redis-cli
```

## Install fig

You can install fig by one command

```bash
$ curl -L https://github.com/docker/fig/releases/download/1.0.1/fig-`uname -s`-`uname -m` > /usr/local/bin/fig; chmod +x /usr/local/bin/fig
```
