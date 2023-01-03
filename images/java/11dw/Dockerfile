FROM        --platform=$TARGETOS/$TARGETARCH dragonwell-registry.cn-hangzhou.cr.aliyuncs.com/dragonwell/dragonwell:11-alpine

LABEL       author="Small_Ku" maintainer="kuko@duck.com"

LABEL       org.opencontainers.image.source="AliBaba Dragonwell 11"
LABEL       org.opencontainers.image.licenses=MIT

RUN         apk add --update --no-cache curl ca-certificates openssl git tar sqlite fontconfig tzdata iproute2 freetype \
            && adduser -D -h /home/container container

COPY        ./../entrypoint.sh /entrypoint.sh
RUN         chmod +x /entrypoint.sh \ 
            && chown container /entrypoint.sh

USER        container
ENV         USER=container HOME=/home/container
WORKDIR     /home/container

CMD         [ "/bin/ash", "/entrypoint.sh" ]
