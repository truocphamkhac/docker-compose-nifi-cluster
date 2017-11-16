# docker-compose-nifi-cluster

A Docker Compose files to compose a NiFi cluster on Docker.

The master branch uses the latest NiFi version (1.0.0)

- [1.0](https://github.com/truocphamkhac/docker-compose-nifi-cluster/tree/master): NiFi version 1.0.0

For newer version, use following branches:

- [1.4.0](https://github.com/truocphamkhac/docker-compose-nifi-cluster/tree/1.4.0): NiFi Cluster version 1.4.0

For older version, use following branches:

- [0.x](https://github.com/ijokarumawak/docker-compose-nifi-cluster/tree/0.x): NCM and 2 nodes cluster.

## PREREQUISITE

You need docker, docker-machine and docker-compose. For example, in my environment I have these versions.

```Shell
$ docker -v
Docker version 17.09.0-ce, build afdb6d4

$ docker-machine -v
docker-machine version 0.12.2, build 9371605

$ docker-compose -v
docker-compose version 1.16.1, build 6d1ac21
```

## HOW TO USE

```Shell
# Clone this repository
$ git@github.com:ijokarumawak/docker-compose-nifi-cluster.git
$ cd docker-compose-nifi-cluster

# To start nifi cluster
$ docker-compose up -d

# Wait few minutes for NiFi to unpack nars and the nodes recognized eachother.
# Then access to the seed node's url through docker-machine vm
$ docker-machine ip
192.168.99.100

http://192.168.99.100:8080/nifi/

# You may need to add routing by a command something like this:
$ sudo route add -net 172.17.0.0 `docker-machine ip`

# View logs or container status
$ docker-compose logs -f
$ docker exec nifi-cluster-seed tail -f logs/nifi-app.log
$ docker-compose ps

# Scale number of nodes (seed + n)
$ docker-compose scale nifi-nodes=2

# Dispose the cluster
$ docker-compose down

# To rebuild nifi-node docker image
$ docker-compose build
```

## BASE DOCKER IMAGE

I used [apache/nifi](https://hub.docker.com/r/apache/nifi/) 1.4.0 as a base image.

## NIFI CLUSTER SAMPLE

![connected-node](https://raw.githubusercontent.com/ijokarumawak/docker-compose-nifi-cluster/master/images/connected-nodes.png)
