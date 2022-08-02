# Enviroment will be based on kubernetes k3s

Once is a simpler K8S flavor will be enough for our use case


## Create cluster with k3d

[K3D web site](https://k3d.io/)

### Install k3d

```
curl -s https://raw.githubusercontent.com/k3d-io/k3d/main/install.sh | bash
```

### Create cluster
```
k3d cluster create --config cluster-k3d.yaml

kubectl config use-context k3d-de-opensource
```

### Cleaning up

```
k3d cluster delete --config cluster-k3d.yaml
```

## Install k3s directly on docker

[K3S git repo](https://github.com/k3s-io/k3s)

```
K3S_TOKEN=${RANDOM}${RANDOM}${RANDOM}

docker-compose up -d

mv kubeconfig.yaml /home/otacilio/.kube/config
```

[Reference](https://medium.com/codex/setup-local-integration-environment-with-k3s-and-docker-compose-13fd815765cc)

### Cleaning up

```
docker-compose down -v
```

## Bonus

### Apply sample application

```
kubectl apply -f kube-news/k8s/deployment.yaml
```

to open the application on the browser use localhost:30000, if its a wsl it need to use the wsl ip

*kube-news is a application provide by KubeDev (Fabricio Veronez) on DevOps iniciative course

### how to get wsl ip

```
ip addr | grep eth0
```