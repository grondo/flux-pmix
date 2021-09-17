FROM fluxrm/flux-core:focal

ARG USER=fluxuser
ARG UID=1000

# ompi can't coexist with mpich
RUN sudo apt remove -yy mpich libmpich-dev libmpich12

RUN sudo apt-get update \
 && sudo apt-get -qq install -y --no-install-recommends \
    libevent-dev \
    flex \
    openssh-client \
 && sudo rm -rf /var/lib/apt/lists/*

RUN cd /tmp \
 && git clone -b v5.0.x --recursive --depth=1 https://github.com/open-mpi/ompi \
 && cd ompi \
 && ./autogen.pl \
 && ./configure --prefix=/usr \
      --disable-man-pages --enable-debug --enable-mem-debug \
 && make -j 6 \
 && sudo make install \
 && cd .. \
 && rm -rf ompi

RUN \
 if test "$USER" != "fluxuser"; then  \
      sudo groupadd -g $UID $USER \
   && sudo useradd -g $USER -u $UID -d /home/$USER -m $USER \
   && sudo sh -c "printf \"$USER ALL= NOPASSWD: ALL\\n\" >> /etc/sudoers" \
   && sudo adduser $USER sudo ; \
 fi

USER $USER
WORKDIR /home/$USER

