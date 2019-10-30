# Quickstart

## Get docker image

You might take either way:

### Pull a image from Public Docker hub

```
$ docker pull tachacoin/tachacoin
```

### Or, build tachacoin image with provided Dockerfile

```
$docker build --rm -t tachacoin/tachacoin .
```

For historical versions, please visit [docker hub](https://hub.docker.com/r/tachacoin/tachacoin/)

## Prepare data path and tachacoin.conf

In order to use user-defined config file, as well as save block chain data, -v option for docker is recommended.

First chose a path to save tachacoin block chain data:

```
sudo rm -rf /data/tachacoin-data
sudo mkdir -p /data/tachacoin-data
sudo chmod a+w /data/tachacoin-data
```

Create your config file, refer to the example [tachacoin.conf]!(https://github.com/tachacoin/tachacoin/blob/1a926b980f03e97322c7dd787835bec1730f35d2/contrib/debian/examples/tachacoin.conf). Note rpcuser and rpcpassword to required for later `tachacoin-cli` usage for docker, so it is better to set those two options. Then please create the file ${PWD}/tachacoin.conf with content:

```
rpcuser=tachacoin
rpcpassword=tachacointest
```
## Launch tachacoind

To launch tachacoin node:

```
## to launch tachacoind
$ docker run -d --rm --name tachacoin_node \
             -v ${PWD}/tachacoin.conf:/root/.tachacoin/tachacoin.conf \
             -v /data/tachacoin-data/:/root/.tachacoin/ \
             tachacoin/tachacoin tachacoind

## check docker processed
$ docker ps

## to stop tachacoind
$ docker run -i --network container:tachacoin_node \
             -v ${PWD}/tachacoin.conf:/root/.tachacoin/tachacoin.conf \
             -v /data/tachacoin-data/:/root/.tachacoin/ \
             tachacoin/tachacoin tachacoin-cli stop
```

`${PWD}/tachacoin.conf` will be used, and blockchain data saved under /data/tachacoin-data/

## Interact with `tachacoind` using `tachacoin-cli`

Use following docker command to interact with your tachacoin node with `tachacoin-cli`:

```
$ docker run -i --network container:tachacoin_node \
             -v ${PWD}/tachacoin.conf:/root/.tachacoin/tachacoin.conf \
             -v /data/tachacoin-data/:/root/.tachacoin/ \
             tachacoin/tachacoin tachacoin-cli getinfo
```

For more tachacoin-cli commands, use:

```
$ docker run -i --network container:tachacoin_node \
             -v ${PWD}/tachacoin.conf:/root/.tachacoin/tachacoin.conf \
             -v /data/tachacoin-data/:/root/.tachacoin/ \
             tachacoin/tachacoin tachacoin-cli help
```

