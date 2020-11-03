FROM ubuntu:20.04 AS base
RUN apt-get update && apt-get install -y \
    gcc \
    g++ \
    libc6-dev \
    build-essential \
    git


FROM base AS bedops
RUN git clone --branch v2.4.39 --depth 1 https://github.com/bedops/bedops.git && \
    cd bedops && \
    make && \
    make install


FROM base AS final
COPY --from=bedops /bedops/bin/* /bin/
