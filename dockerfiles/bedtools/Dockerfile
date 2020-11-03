# Build base image
# Essentially install necessary packages in the alpine official image
FROM alpine:3.11.3 AS base
RUN apk update && apk add \
    bash \
	wget \
    make \
    gcc \
    g++ \
    zlib \
	zlib-dev \
    python


# Build bedtools (2.22.1)
# Clone and build bedtools from GitHub repository
FROM base AS bedtools
RUN wget https://github.com/arq5x/bedtools2/archive/v2.22.1.tar.gz && \
    tar -zxvf v2.22.1.tar.gz && \
    cd bedtools2-2.22.1 && \
    make


# Build final image
# Essentially copy compiled binaries to a new image
FROM base AS final
COPY --from=bedtools /bedtools2-2.22.1/bin /bin
