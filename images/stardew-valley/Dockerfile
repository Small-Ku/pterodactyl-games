# Pull base image.
FROM jlesage/baseimage-gui:debian-11

MAINTAINER Small_Ku, <kuko@duck.com>

# Set the name of the application.
ENV APP_NAME="StardewValley"

## add container user
RUN useradd -m -d /home/container container
ENV USER=container HOME=/home/container

RUN apt update && apt upgrade -y

RUN apt install -y wget unzip tar strace mono-complete xterm gettext-base jq netcat procps dotnet-sdk-5.0
RUN APP_ICON_URL=https://stardewcommunitywiki.com/mediawiki/images/4/48/Fiddlehead_Fern.png && \
    install_app_icon.sh "$APP_ICON_URL"

# Game + ModLoader 1.5.6 3.14.7
RUN mkdir -p /home/container/Stardew && \
    mkdir -p /home/container/nexus && \
    wget https://eris.cc/Stardew_latest.tar.gz -qO /home/container/latest.tar.gz && \
    tar xf /home/container/latest.tar.gz -C /home/container/Stardew && \
    rm /home/container/latest.tar.gz 

RUN wget -qO dotnet.tar.gz https://download.visualstudio.microsoft.com/download/pr/d4b71fac-a2fd-4516-ac58-100fb09d796a/e79d6c2a8040b59bf49c0d167ae70a7b/dotnet-sdk-5.0.408-linux-arm64.tar.gz \
#RUN wget -qO dotnet.tar.gz https://download.visualstudio.microsoft.com/download/pr/95352809-7f41-40f3-974d-8d530321a8e4/0024d7bf0c872f176ceba7a63a34915b/dotnet-runtime-6.0.0-linux-musl-x64.tar.gz \
    && tar -zxf dotnet.tar.gz -C /usr/share/dotnet \
    && rm dotnet.tar.gz \
    && ln -s /usr/share/dotnet/dotnet /usr/bin/dotnet 

RUN wget https://github.com/Pathoschild/SMAPI/releases/download/3.14.7/SMAPI-3.14.7-installer.zip -qO /home/container/nexus.zip && \
    unzip /home/container/nexus.zip -d /home/container/nexus/ && \
    /bin/bash -c "SMAPI_NO_TERMINAL=true SMAPI_USE_CURRENT_SHELL=true echo -e \"2\n\n\" | /data/nexus/SMAPI\ 3.14.7\ installer/internal/linux/SMAPI.Installer --install --game-path \"/data/Stardew/Stardew Valley\"" || :


# Add Mods & Scripts
COPY ["mods/", "/home/container/Stardew/Stardew Valley/Mods/"]
COPY scripts/ /home/container/scripts

RUN chmod +x /home/container/Stardew/Stardew\ Valley/StardewValley && \
    chmod -R 777 /home/container/Stardew/ && \
    chown -R 1000:1000 /home/container/Stardew && \
    chmod +x /home/container/scripts/*.sh

WORKDIR /home/container
COPY ./entrypoint.sh /entrypoint.sh
CMD ["/bin/bash", "/entrypoint.sh"]
