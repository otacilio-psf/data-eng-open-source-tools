FROM debian:bullseye-slim

RUN apt update && \
    apt install openjdk-17-jre python3 -y && \
    update-alternatives --install /usr/bin/python python /usr/bin/python3 1 && \
    apt-get install wget -y

RUN wget https://repo.maven.apache.org/maven2/io/trino/trino-server/390/trino-server-390.tar.gz && \
    tar xvzf trino-server-*.tar.gz && \
    mv  trino-server-*/ trino-server && \
    rm trino-server-*.tar.gz

RUN mkdir /trino-server/etc
#COPY trino-configs/single-installation/etc /trino-server/etc

WORKDIR /trino-server

RUN wget -O trino \
    https://repo.maven.apache.org/maven2/io/trino/trino-cli/390/trino-cli-390-executable.jar && \
    chmod +x trino && \
    mv trino /bin

EXPOSE 8080

ENTRYPOINT [ "bin/launcher" , "run" ]