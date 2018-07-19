FROM debian:stretch

RUN dpkg --add-architecture armhf \
    && echo "deb [arch=armhf] http://httpredir.debian.org/debian/ stretch main contrib non-free" > /etc/apt/sources.list.d/armhf.list \
    && apt-get update && apt-get install -y \
        openjdk-8-jdk automake autoconf \
        curl zip unzip libtool swig libpng-dev zlib1g-dev pkg-config git g++ wget xz-utils \
        python3-numpy python3-dev python3-pip python3-mock \
        libpython3-all-dev:armhf \
    && update-alternatives --install /usr/bin/python python /usr/bin/python3 1 \
    && rm -rf /var/lib/apt/lists/*

COPY . /build
WORKDIR /build/
RUN chmod 755 *.sh

ENTRYPOINT ["/build/build_tensorflow.sh"]
