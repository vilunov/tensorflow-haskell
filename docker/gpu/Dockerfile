# Prepare the image with:
#   docker build -t tensorflow/haskell:1.14.0-gpu docker/gpu
FROM tensorflow/tensorflow:1.14.0-gpu
LABEL maintainer="TensorFlow authors <tensorflow-haskell@googlegroups.com>"

RUN apt-get update

RUN apt-get install -y \
        # stack needs git
        git \
        # Required by snappy-frames dependency.
        libsnappy-dev \
        # Avoids /usr/bin/ld: cannot find -ltinfo
        libncurses5-dev \
        # Makes stack viable in the container
        libgmp-dev \
        zlib1g-dev \
        # For fetching dependencies
        curl \
        unzip \
        # Required for locales configuration.
        locales

# Support output of Unicode characters.
RUN dpkg-reconfigure locales && \
    locale-gen en_US.UTF-8 && \
    update-locale LANG=en_US.UTF-8

# Installs protoc and the libraries.
RUN \
    curl -O -L https://github.com/google/protobuf/releases/download/v3.2.0/protoc-3.2.0-linux-x86_64.zip && \
    unzip -d /usr/local protoc-3.2.0-linux-x86_64.zip bin/protoc && \
    chmod 755 /usr/local/bin/protoc && \
    curl -O https://storage.googleapis.com/tensorflow/libtensorflow/libtensorflow-gpu-linux-x86_64-1.14.0.tar.gz && \
    tar zxf libtensorflow-gpu-linux-x86_64-1.14.0.tar.gz -C /usr/local && \
    ldconfig

ENV LANG en_US.UTF-8
