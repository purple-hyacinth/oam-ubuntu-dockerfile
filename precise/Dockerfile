FROM scratch
ADD ubuntu-core-12.04-core-armel.tar.gz /

LABEL summary="Emulated environment for arm development" \
      version="0.1"

ARG DEBIAN_FRONTEND=noninteractive

# update and install dependencies
RUN apt-get update \
	&& apt-get install -y \
	sudo \
	net-tools \
	ping \
	ssh-server \
	autoconf \
	automake \
	build-essential \
	make \
	git \
	curl \
	vim \
	cmake \
	gcc \
	g++ \
	libtool \
	&& rm -rf /var/lib/apt/lists/*

# make systemd-detect-virt return "docker"
# See: https://github.com/systemd/systemd/blob/aa0c34279ee40bce2f9681b496922dedbadfca19/src/basic/virt.c#L434
RUN mkdir -p /run/systemd && echo 'docker' > /run/systemd/container

ARG USER=dev-user
ARG UID=1000
ARG GID=1000
#default password for user
ARG PW=docker

RUN useradd -rm -d /home/${USER} -s /bin/bash -g root -G sudo --uid=${UID} ${USER} && echo "${USER}:${PW}" | chpasswd
USER dev-user
WORKDIR /home/dev-user

CMD ["/bin/bash"]
