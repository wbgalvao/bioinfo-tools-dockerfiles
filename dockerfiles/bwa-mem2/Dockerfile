FROM alpine:3.11.3 AS base

# Build base image
# Essentially install necessary packages in the alpine official image
RUN apk update && apk add \
    bash \
    zlib \
    zlib-dev \
    gcc \
    g++ \
    make \
    git \
    libbz2 \
    xz \
    xz-dev \
    libcurl \
    autoconf \
    libbz2 \
    bzip2-dev \
    ncurses \
    ncurses-dev


# Build bwa-mem2 (v2.0)
# Clone and build bwa-mem2 from its GitHub repository
FROM base AS bwa-mem2
RUN git clone --recursive --branch v2.0 --depth 1 https://github.com/bwa-mem2/bwa-mem2.git && \
    cd bwa-mem2 && \
    make

# Build final image
# Essentially copy compiled bwa-mem2 binary to a new image
FROM base AS final
COPY --from=bwa-mem2 /bwa-mem2/bwa-mem2 /bin
