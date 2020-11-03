FROM debian:stretch-20200803 AS base

# Build base image
# Essentially install necessary packages in the alpine official image
RUN apt-get update && apt-get -y install \
        g++ \
        make \
        git \
        zlib1g-dev \
    && rm -rf /var/lib/apt/lists/*

# Build bwa (v0.7.17)
# Clone and build bwa from Heng Li's (lh3) GitHub repository
FROM base AS bwa
RUN git clone --branch v0.7.17 --depth 1 https://github.com/lh3/bwa.git && \
    cd bwa && \
    make

# Build final image
# Essentially copy compiled bwa binary to a new image
FROM base AS final
COPY --from=bwa /bwa/bwa /bin
