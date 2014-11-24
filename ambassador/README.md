# Link via an Ambassador Container

[Link via an Ambassador Container](http://docs.docker.com/articles/ambassador_pattern_linking/)

```bash
(consumer) --> (redis-ambassador) ---network---> (redis-ambassador) --> (redis)
```

## Setup environment

Up 2 Ubuntu VM hosts

```bash
$ vagrant up
```

## Host roles

We have two hosts named `h1` (`192.20.20.11`) and `h2` (`192.20.20.55`), each has role,

- `h1` is host for running redis
- `h2` is host for connectin redis in `h1`


## Run

At first, run redis container in `h1`,

```bash
$ vagrant ssh h1
$ docker run -d --name redis crosbymichael/redis
$ docker run -d --link redis:redis --name redis_ambassador -p 6379:6379 svendowideit/ambassador
```

Then, run redis-cli container from `h2`,

```bash
$ vagrant ssh h2
$ docker run -d --name redis_ambassador --expose 6379 -e REDIS_PORT_6379_TCP=tcp://192.168.1.52:6379 svendowideit/ambassador
$ sudo docker run -i -t --rm --link redis_ambassador:redis relateiq/redis-cli
redis 172.17.0.160:6379> ping
PONG
```
