FROM        --platform=$TARGETOS/$TARGETARCH dragonwell-registry.cn-hangzhou.cr.aliyuncs.com/dragonwell/dragonwell:17-alpine

LABEL       author="Small_Ku" maintainer="kuko@duck.com"

RUN         apt update -y \
						&& apt install -y curl ca-certificates openssl git tar sqlite3 fontconfig tzdata iproute2 libfreetype6 \
						&& useradd -d /home/container -m container

USER        container
ENV         USER=container HOME=/home/container
WORKDIR     /home/container

COPY        ./../entrypoint.sh /entrypoint.sh
CMD         [ "/bin/bash", "/entrypoint.sh" ]
