# Quickstart

This is a tachacoin-qt image, launch GUI wallet

## Get docker image

To get the latest image, you might take either way:

### Pull a image from Public Docker hub

```
$ docker pull tachacoin/tachacoin-qt
```

### Or, build tachacoin image with provided Dockerfile

```
$docker build --rm -t tachacoin/tachacoin-qt .
```

For historical versions, please visit [docker hub](https://hub.docker.com/r/tachacoin/tachacoin-qt/)

## Prepare data path & tachacoin.conf

In order to use user-defined config file, as well as save block chain data, -v option for docker is recommended.

First chose a path to save tachacoin block chain data:

```
sudo rm -rf /data/tachacoin-data
sudo mkdir -p /data/tachacoin-data
sudo chmod a+w /data/tachacoin-data
```

Create your config file, refer to the example [tachacoin.conf]!(https://github.com/tachacoin/tachacoin/blob/1a926b980f03e97322c7dd787835bec1730f35d2/contrib/debian/examples/tachacoin.conf). Then please create the file ${PWD}/tachacoin.conf with content:

```
rpcuser=tachacoin
rpcpassword=tachacointest
```

User can set their own config file on demands.

## Launch tachacoin-qt

For Linux:

```
$ docker run -it --rm \
             -v /tmp/.X11-unix:/tmp/.X11-unix \
             -v ${PWD}/tachacoin.conf:/root/.tachacoin/tachacoin.conf \
             -v /data/tachacoin-data/:/root/.tachacoin/ \
             -e DISPLAY  tachacoin/tachacoin-qt
```

For Mac:

Please refer to
[https://cntnr.io/running-guis-with-docker-on-mac-os-x-a14df6a76efc](https://cntnr.io/running-guis-with-docker-on-mac-os-x-a14df6a76efc) about how to run gui with docker on mac.

```
## install & launch socat
$ brew install socat
$ socat TCP-LISTEN:6000,reuseaddr,fork UNIX-CLIENT:\"$DISPLAY\"

## install & open Xquartz
$ brew install xquartz
$ open -a Xquartz

## then set Xquartz preferences "Security-'Allow connections from network clients'"

## launch tachacoin-qt 
$ docker run -e DISPLAY=<your_ip>:0 -v ${PWD}/tachacoin.conf:/root/.tachacoin/tachacoin.conf -v /data/tachacoin-data/:/root/.tachacoin/ tachacoin/tachacoin-qt

```


`${PWD}/tachacoin.conf` will be used, and blockchain data saved under /data/tachacoin-data/


## exit tachacoin-qt

Exit the gui wallet in normal way.


