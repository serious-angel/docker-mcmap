FROM ubuntu AS base

# Build
# ----------------------------------------------------------------

FROM base AS build

# General Update and Upgrade
# --------------------------------

RUN \
    apt-get autoremove -y && \
    apt-get autoclean && \
    apt-get clean all && \
    apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y --no-install-recommends \
        ca-certificates \
        curl \
        wget \
        p7zip-full \
        nano \
        gosu && \
    apt-get clean && \
    rm -rf '/var/lib/apt/lists/'* '/tmp/'* '/var/tmp/'* '/usr/share/doc/'*;

# Dependencies
# ----------------------------------------------------------------

FROM build AS deps

RUN \
    apt-get autoremove -y && \
    apt-get autoclean && \
    apt-get clean all && \
    apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y --no-install-recommends \
        git \
        make \
        g++ \
        libpng-dev \
        cmake \
        libspdlog-dev && \
    apt-get autoremove --purge -y && \
    apt-get clean && \
    rm -rf '/var/lib/apt/lists/'* '/tmp/'* '/var/tmp/'* '/usr/share/doc/'*;

# Compilations
# ----------------------------------------------------------------

FROM deps AS compilations

RUN \
    mkdir -p '/tmp/mcmap' && \
    cd -P '/tmp/mcmap' && \
    git clone --depth 1 -- 'https://github.com/spoutn1k/mcmap' './' && \
    mkdir -p './build' && cd './build' && \
    cmake .. && \
    make -j && \
    { '/tmp/mcmap/build/bin/mcmap' -h || [ $? = 1 ]; } && \
    cp -vr -- '/tmp/mcmap/build/bin/'* '/usr/local/bin/' && \
    rm -rf -- '/tmp/mcmap/';

# Entrypoint
# ----------------------------------------------------------------

FROM compilations AS entry

ENTRYPOINT [ "/usr/local/bin/mcmap" ]

CMD [ "-help" ]

# Compilations
# ----------------------------------------------------------------

LABEL org.opencontainers.image.title="MCMap Docker Image"
LABEL org.opencontainers.image.description="Docker image containing prebuilt binaries of MCMap."
LABEL org.opencontainers.image.authors="Artworks <https://github.com/serious-angel>; spoutn1k <https://github.com/spoutn1k>"
LABEL org.opencontainers.image.source="https://github.com/serious-angel/docker-mcmap"
LABEL org.opencontainers.image.url="https://github.com/spoutn1k/mcmap"
LABEL org.opencontainers.image.vendor="Artworks"
LABEL org.opencontainers.image.licenses="MIT"