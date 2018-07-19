FROM debian:stretch

RUN apt-get update && apt-get install -y \
        automake autoconf \
        curl zip unzip libtool swig zlib1g-dev pkg-config git g++ wget xz-utils \
        python3-numpy python3-dev python3-pip python3-mock \
    && update-alternatives --install /usr/bin/python python /usr/bin/python3 1 \
    && curl --show-error -L https://bazel.build/bazel-release.pub.gpg | apt-key add - \
    && echo "deb [arch=amd64] http://storage.googleapis.com/bazel-apt stable jdk1.8" > /etc/apt/sources.list.d/bazel.list \
    && apt-get update && apt-get install -y \
        bazel \
    && echo "deb [arch=amd64] http://httpredir.debian.org/debian/ jessie main contrib non-free" > /etc/apt/sources.list.d/jessie.list \
    && apt-get update && apt-get install -y \
        libpng12-dev \
    && rm -f /etc/apt/sources.list.d/jessie.list \
    && dpkg --add-architecture armhf \
    && echo "deb [arch=armhf] http://httpredir.debian.org/debian/ stretch main contrib non-free" > /etc/apt/sources.list.d/armhf.list \
    && apt-get update && apt-get install -y \
        libpython3-all-dev:armhf \
    && rm -rf /var/lib/apt/lists/*

COPY . /build
WORKDIR /build/
RUN chmod 755 *.sh

ENTRYPOINT ["/build/build_tensorflow.sh"]
