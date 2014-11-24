# Dynamic Docker links with an ambassador powered by etcd

[Dynamic Docker links with an ambassador powered by etcd](https://coreos.com/blog/docker-dynamic-ambassador-powered-by-etcd/)

## Setup CoreOS cluster

This example try to create cluster on DigitalOcean with `vagrant`. First, you need to set environmental variables,

```bash
$ export TOKEN=""
$ export SSH_KEY_NAME=""
```

Add your etcd discovery service in `user-data.yml` and ecide how many instances you use,

```bash
$ export NUM_INSTANCES=3
```

And up it,

```bash
$ vagrant up --provider=digital_ocean
```

## Run

Send `.service` files to one instance,

```bash
$ scp *.service core@{YOUR_IP}:.
```

And run it,

```bash
$ ssh -A core@{YOUR_IP}
```

```bash
$ fleetctl start *.service
```

Then login to machine where `redis-dyn-amb` container is working and connect to `redis` container,

```bash
$ fleetctl ssh redis-dyn-amb
```

```bash
$ docker run -it --link redis-dyn-amb.service:redis relateiq/redis-cli
redis 172.17.0.19:6379> ping
PONG
```
