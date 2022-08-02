# Data lake using MinIO

[Reference doc](https://docs.min.io/minio/baremetal/)

[Reference doc 2](https://github.com/kubernetes/examples/tree/master/staging/storage/minio)


## Using helm chart

[Bitnami Artifact Hub](https://artifacthub.io/packages/helm/bitnami/minio)

## Using docker-compose

[Bitnami Docker Hub](https://hub.docker.com/r/bitnami/minio/)

```
docker-compose up -d

docker-compose down -v
```



## Standalone Quickstart

```
kubectl create -f manifests/minio-standalone-pvc.yaml
kubectl create -f manifests/minio-standalone-deployment.yaml
kubectl create -f manifests/minio-standalone-service.yaml
```

or

```
kubectl create -f manifests/
```

didn't worked


## Bonus 

### Storage class

verificar as storage class disponiveis

```
kubectl get storageclass
```

```
kubectl describe sc default
```

### PV e PVC

```
kubectl get pv
kubectl get pvc
```