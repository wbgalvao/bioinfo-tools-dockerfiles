# Create base image with necessary dependencies
FROM ubuntu:16.04 as base

RUN apt-get update && apt-get -y install \
    -qq \
    bzip2 \
    gcc \
    g++ \
    make \
    python \
    zlib1g-dev \
    wget \
    && rm -rf /var/lib/apt/lists/*


# Build manta (v1.6.0) from source
FROM base as builder

WORKDIR /usr/src/
RUN wget https://github.com/Illumina/manta/releases/download/v1.6.0/manta-1.6.0.release_src.tar.bz2 \
    && tar -xjf manta-1.6.0.release_src.tar.bz2 \
    && mkdir build \
    && cd build \
    && ../manta-1.6.0.release_src/configure --jobs=4 --prefix=/etc/manta-1.6.0/ \
    && make -j4 install


# Copy installed manta directory to new image
FROM base as final
COPY --from=builder /etc/manta-1.6.0/ /usr/manta-1.6.0/
WORKDIR /usr/manta-1.6.0/
