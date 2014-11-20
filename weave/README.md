# Link via an weave network

[Weave - the Docker network](https://github.com/zettio/weave)


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

To start weave router on each host, 

```bash
$ vagrant ssh h1
$ sudo weave launch
```

```bash
$ vagrant ssh h2 
$ sudo weave launch 192.20.20.11 
```

At first, run redis container in `h1`,

```bash
$ vagrant ssh h1
$ sudo weave run 10.0.1.1/24 -d crosbymichael/redis
```

Then, run redis-cli container from `h2`,

```bash
$ vagrant ssh h2
$ C=$(sudo weave run 10.0.1.2/24 -i -t relateiq/redis-cli -h 10.0.1.1)
$ docker attach $C
redis 10.0.1.1:6379> ping
PONG
```
