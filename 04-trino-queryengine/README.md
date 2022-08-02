## Quick start

```
docker run -d --name trino-trial trinodb/trino
```

```
docker exec -it trino-trial trino
```

```
trino> select count(*) from tpch.sf100.orders;
```

```
docker rm -f trino-trial
```

## Local Instalation

```
# java --version > 17
apt update
apt install openjdk-17-jre -y

# python --version > 2.6
apt install python3 -y && \
update-alternatives --install /usr/bin/python python /usr/bin/python3 1

# wget
apt-get install wget -y

# install trino
wget https://repo.maven.apache.org/maven2/io/trino/trino-server/390/trino-server-390.tar.gz

tar xvzf trino-server-*.tar.gz

mv  trino-server-*/ trino-server

rm trino-server-*.tar.gz

# add config files

cp -r trino-configs/single-installation/etc ./trino-server/

# start

./trino-server/bin/launcher start

./trino-server/bin/launcher status

# cli
## install
wget -O trino https://repo.maven.apache.org/maven2/io/trino/trino-cli/390/trino-cli-390-executable.jar

chmod +x trino 

## if want to put on the path
##mv trino ~/bin && export PATH=~/bin/:$PATH

./trino

trino> select count(*) from tpch.sf100.orders;

./trino-server-*/bin/launcher stop
```

## Build and Run Docker images
docker build . -t otaciliopsf/trino-server

docker run -d -p 8080:8080 -v $(pwd)/trino-configs/single/etc:/trino-server/etc --name trino otaciliopsf/trino-server

docker exec -it trino /trino-server/bin/launcher status

docker exec -it trino trino

trino> select count(*) from tpch.sf100.orders;

docker rm -f trino

## Deploy cluster with Compose

docker-compose up -d

./trino

trino> select count(*) from tpch.sf100.orders;

docker-compose down



### CONFIGS
mkdir etc && \
mkdir etc/catalog

cat << EOF > etc/config.properties
coordinator=true
node-scheduler.include-coordinator=true
http-server.http.port=8080
query.max-memory=5GB
query.max-memory-per-node=1GB
query.max-total-memory-per-node=2GB
discovery-server.enabled=true
discovery.uri=http://localhost:8080
EOF

cat << EOF > etc/node.properties
node.environment=demo
EOF

cat << EOF > etc/jvm.config
-server
-Xmx4G
-XX:-UseBiasedLocking
-XX:+UseG1GC
-XX:G1HeapRegionSize=32M
-XX:+ExplicitGCInvokesConcurrent
-XX:+HeapDumpOnOutOfMemoryError
-XX:+ExitOnOutOfMemoryError
-XX:ReservedCodeCacheSize=512M
-XX:PerMethodRecompilationCutoff=10000
-XX:PerBytecodeRecompilationCutoff=10000
-Djdk.nio.maxCachedBufferSize=2000000
-Djdk.attach.allowAttachSelf=true
EOF

cat << EOF > etc/log.properties
io.trino=WARN
EOF

cat << EOF > etc/catalog/tpch.properties
connector.name=tpch
EOF
    
