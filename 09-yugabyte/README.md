# Docker

mkdir ~/yb_data

docker run -d --name yugabyte \
         -p7000:7000 -p9000:9000 -p5433:5433 -p9042:9042 \
         -v /mnt/c/Users/otaci/Desktop/repos/data-eng-open-source-tools/09-yugabyte/yb_data:/home/yugabyte/yb_data \
         yugabytedb/yugabyte:latest \
         bin/yugabyted start --base_dir=/home/yugabyte/yb_data --daemon=false



# Docker compose

mkdir ~/yb_data

docker-compose up -d

docker-compose down

## Clean

sudo rm -r ~/yb_data

### how to get wsl ip

```
ip addr | grep eth0
```