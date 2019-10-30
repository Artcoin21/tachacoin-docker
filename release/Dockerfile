FROM ubuntu
MAINTAINER pandazwb

RUN set -ex \
    && apt-get update \
    && apt-get install -y -qq --no-install-recommends ca-certificates curl wget apt-utils jq

# install tachacoin binaries
RUN set -ex \
    && echo `curl -s https://api.github.com/repos/tachacoin/tachacoin/releases/latest | jq -r ".assets[] | select(.name | test(\"x86_64-linux-gnu.tar.gz\")) | .browser_download_url"` > /tmp/tachacoin_url \
    && TACHACOIN_URL=`cat /tmp/tachacoin_url` \
    && TACHACOIN_DIST=$(basename $TACHACOIN_URL) \
    && wget -O $TACHACOIN_DIST $TACHACOIN_URL \
	&& tar -xzvf $TACHACOIN_DIST -C /usr/local --strip-components=1 \
	&& rm /tmp/tachacoin*

# create data directory
ENV TACHACOIN_DATA /data
RUN mkdir $TACHACOIN_DATA \
	&& ln -sfn $TACHACOIN_DATA /root/.tachacoin \
VOLUME /data

EXPOSE 44450 45551 44460 45561
CMD ["tachacoind"]
