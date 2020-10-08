FROM debian:buster-slim

ENV DEBIAN_FRONTEND=noninteractive
RUN ln -fs /usr/share/zoneinfo/America/New_York /etc/localtime
RUN cp /etc/apt/sources.list /etc/apt/sources.list~; \
    sed "/^deb /{p;s/deb /deb-src /g}" /etc/apt/sources.list -i; \
    apt-get update 
RUN apt-get install -y git

WORKDIR /src
RUN git clone https://github.com/raspberrypi/tools.git --depth 1
RUN git clone https://gitlab.haskell.org/ghc/ghc.git --depth 1 --branch ghc-8.6.5-release
WORKDIR /src/ghc
RUN git submodule update --init

RUN dpkg --add-architecture armhf
RUN apt-get update
RUN apt-get install -y haskell-platform
RUN apt-get install -y libtinfo-dev libncurses5 libncurses5-dev 
RUN apt-get install -y binutils-arm-linux-gnueabihf cpp-8-arm-linux-gnueabihf gcc-8-arm-linux-gnueabihf
RUN apt-get install -y linux-libc-dev-armhf-cross libc6-armhf-cross
RUN apt-get install -y libtinfo-dev libncurses5 libncurses5-dev
RUN apt-get install -y build-essential crossbuild-essential-armhf crossbuild-essential-arm64
RUN apt-get upgrade -y
RUN mkdir -p /usr/share/man/man1
RUN apt-get build-dep -y ghc

RUN apt-get install -y llvm-7 llvm-7-tools ncurses-dev libedit-dev
ENV PATH="/src/tools/arm-bcm2708/gcc-linaro-arm-linux-gnueabihf-raspbian-x64/bin:/root/.cabal/bin:${PATH}"

RUN cabal update
RUN cabal install happy alex
RUN sed "/quick-cross$/s/#//" mk/build.mk.sample > mk/build.mk; \
    echo "\
Stage1Only    = Yes \
GhcLibHcOpts  = -O -fllvm \
GhcRtsHcOpts += -fllvm\
INTEGER_LIBRARY = integer-simple \
" >>mk/build.mk 

RUN ./boot
RUN ./configure \
        --target=arm-linux-gnueabihf \
        --prefix=/ghc/rpi/ \
        --enable-unregisterised \
        CC=arm-linux-gnueabihf-gcc \
        CPPFLAGS="-std=c99"
RUN make; make install

