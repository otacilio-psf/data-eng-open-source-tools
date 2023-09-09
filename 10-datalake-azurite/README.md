# Run Azurite V3 docker image

Is for test and dev only

[Github repo](https://github.com/Azure/Azurite#dockerhub)

## Only blob

```bash
docker run -d -p 10000:10000 -v $(pwd)/10-azurite/workspace:/workspace mcr.microsoft.com/azure-storage/azurite azurite-blob -l /workspace -d /workspace/debug.log --blobHost 0.0.0.0
```