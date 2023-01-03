FROM jlesage/baseimage-gui:debian-11

MAINTAINER Small_Ku, <kuko@duck.com>

RUN useradd -m -d /home/container container
ENV USER=container HOME=/home/container

RUN apt update && apt upgrade -y

RUN apt install -y wget unzip tar strace mono-complete xterm gettext-base jq netcat procps

RUN wget -qO dotnet.tar.gz https://download.visualstudio.microsoft.com/download/pr/d4b71fac-a2fd-4516-ac58-100fb09d796a/e79d6c2a8040b59bf49c0d167ae70a7b/dotnet-sdk-5.0.408-linux-arm64.tar.gz \
    && tar -zxf dotnet.tar.gz -C /usr/share/dotnet \
    && rm dotnet.tar.gz \
    && ln -s /usr/share/dotnet/dotnet /usr/bin/dotnet 

WORKDIR /home/container
COPY ./entrypoint.sh /entrypoint.sh
CMD ["/bin/bash", "/entrypoint.sh"]
