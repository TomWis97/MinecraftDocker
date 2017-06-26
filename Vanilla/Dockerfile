FROM alpine:latest
# Install JDK
RUN apk update && \
    apk add openjdk8-jre && \
    apk add openssl && \
    apk add ca-certificates
# Install Minecraft Server
RUN mkdir -p /opt/mc/world && \
    cd /opt/mc && \
    wget https://s3.amazonaws.com/Minecraft.Download/versions/1.12/minecraft_server.1.12.jar
COPY server.properties /opt/mc/server.properties
COPY eula.txt /opt/mc/eula.txt
# Install fix users and permissions
RUN adduser -D minecraft && \
    chown minecraft:root -R /opt/mc
VOLUME /opt/mc/world
EXPOSE 25565
WORKDIR /opt/mc
USER minecraft
CMD java -Xmx1024M -Xms1024M -jar minecraft_server.1.12.jar nogui
