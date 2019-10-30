FROM ubuntu
MAINTAINER pandazwb

RUN set -ex \
    && apt-get update \
    && apt-get install -y -qq --no-install-recommends ca-certificates git wget apt-utils \
    && apt-get install -y build-essential libtool autotools-dev automake pkg-config libssl-dev libevent-dev bsdmainutils \
    && apt-get install -y libboost-all-dev \
	&& apt-get install -y software-properties-common \
	&& add-apt-repository -y ppa:bitcoin/bitcoin \
	&& apt-get update \
	&& apt-get install -y libdb4.8-dev libdb4.8++-dev \
	&& apt-get install -y libzmq3-dev \
 	&& rm -rf /var/lib/apt/lists/*

# install tachacoin from github
RUN cd /tmp && git clone --recursive https://github.com/tachacoin/tachacoin.git \
	&& cd tachacoin \
	&& ./autogen.sh \
	&& ./configure --without-gui \
	&& make \
	&& make check \
	&& make install  \
	&& rm -rf /tmp/*

# create data directory
ENV TACHACOIN_DATA /data
RUN mkdir $TACHACOIN_DATA \
	&& ln -sfn $TACHACOIN_DATA /root/.tachacoin \
VOLUME /data

EXPOSE 44450 45551 44460 45561
CMD ["tachacoind"]
