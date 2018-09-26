#USAGE: Build the docker image with "docker build -t name_you_want ." and run it as follows "docker run -it -w /work/ -v PATH/TO/REPO:/work name_you_want".
FROM debian:stretch

# This is the same as pulling buildpack-deps:stretch-curl
RUN apt-get update && apt-get install -y --no-install-recommends \
		ca-certificates \
		curl \
		netbase \
		wget \
	&& rm -rf /var/lib/apt/lists/*

RUN set -ex; \
	if ! command -v gpg > /dev/null; then \
		apt-get update; \
		apt-get install -y --no-install-recommends \
			gnupg \
			dirmngr \
		; \
		rm -rf /var/lib/apt/lists/*; \
	fi

# install yarn
RUN curl -L https://yarnpkg.com/latest.tar.gz | tar xvz && mv yarn-* /yarn && ln -s /yarn/bin/yarn /usr/bin/yarn
RUN apt-get -qq update && apt-get -qq dist-upgrade

# Install RPM and AR for building .rpm and .deb
RUN apt-get update && apt-get install -y --no-install-recommends rpm &&\
    apt-get install -y --no-install-recommends binutils && apt-get install -y --no-install-recommends sudo

# Install nodejs. If you require nodejs 10 just use .../setip_10.x
RUN curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash -
RUN apt-get install -y nodejs
