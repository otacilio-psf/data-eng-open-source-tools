## Building your own Spark image

```
# download

wget https://archive.apache.org/dist/spark/spark-3.3.0/spark-3.3.0-bin-hadoop3.tgz

tar xvzf spark-*.tgz

rm spark-*.tgz

cd spark-*

# build

./bin/docker-image-tool.sh -r otaciliopsf -t v3.3.0-hadoop3.3 -p kubernetes/dockerfiles/spark/bindings/python/Dockerfile build

docker push otaciliopsf/spark:v3.3.0-hadoop3.3

docker push otaciliopsf/spark-py:v3.3.0-hadoop3.3

```
