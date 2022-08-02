https://superset.apache.org/docs/installation/installing-superset-using-docker-compose/


git clone https://github.com/apache/superset.git

cp ./superset/docker-compose-non-dev.yml ./docker-compose-non-dev.yml
cp -r ./superset/docker ./docker

rm -rf superset

docker-compose -f docker-compose-non-dev.yml pull
docker-compose -f docker-compose-non-dev.yml up -d

docker-compose -f docker-compose-non-dev.yml down -v

### how to get wsl ip

```
ip addr | grep eth0
```