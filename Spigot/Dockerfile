FROM alpine:latest
# Install JDK
RUN apk update && \
    apk add openjdk8-jre && \
    apk add openssl && \
    apk add ca-certificates && \
    apk add git
# Build Minecraft Server
RUN mkdir /tmp/build && \
    mkdir -p /opt/mc && \
    cd /tmp/build && \
    wget https://hub.spigotmc.org/jenkins/job/BuildTools/lastSuccessfulBuild/artifact/target/BuildTools.jar && \
    java -jar BuildTools.jar --rev latest && \
    cp /tmp/build/spigot-*.jar /opt/spigot.jar && \
    rm -rf /tmp/build
COPY setup.sh /opt/
COPY eula.txt /opt/mc/eula.txt
# Running Server and stuff
RUN cd /opt/mc && \
    chmod +x ../setup.sh && \
    ../setup.sh | java -Xmx1024M -Xms1024M -jar ../spigot.jar nogui && \
    rm -rf world/* && \
    rm -rf world_nether/* && \
    rm -rf world_the_end/*
# Install fix users and permissions
RUN adduser -D minecraft && \
    chown minecraft:root -R /opt/mc && \
    chmod 770 -R /opt/mc
# Deze nog wegcommenten, want als je dat wel er in laat, dan gaat alles kapot vanwege de volumes.
#VOLUME /opt/mc
EXPOSE 25565
WORKDIR /opt/mc
USER minecraft
CMD java -Xmx1024M -Xms1024M -jar ../spigot.jar nogui
