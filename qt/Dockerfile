FROM ubuntu
MAINTAINER pandazwb

RUN set -ex \
    && apt-get update \
    && apt-get install -y -qq --no-install-recommends ca-certificates curl wget apt-utils jq \
    && apt-get install -y libqt5gui5 libqt5core5a libqt5dbus5 qttools5-dev qttools5-dev-tools protobuf-compiler qrencode

# install tachacoin binaries
RUN set -ex \
    && echo `curl -s https://api.github.com/repos/tachacoin/tachacoin/releases/latest | jq -r ".assets[] | select(.name | test(\"x86_64-linux-gnu.tar.gz\")) | .browser_download_url"` > /tmp/tachacoin_url \
    && TACHACOIN_URL=`cat /tmp/tachacoin_url` \
    && TACHACOIN_DIST=$(basename $TACHACOIN_URL) \
    && wget -O $TACHACOIN_DIST $TACHACOIN_URL \
	&& tar -xzvf $TACHACOIN_DIST -C /usr/local --strip-components=1 \
	&& rm /tmp/tachacoin* \
	&& rm -rf /var/lib/apt/lists/*

# create data directory
ENV TACHACOIN_DATA /data
RUN mkdir $TACHACOIN_DATA \
	&& ln -sfn $TACHACOIN_DATA /root/.tachacoin \
VOLUME /data

EXPOSE 44450 45561 44460 45561
CMD ["tachacoin-qt"]
