### Build and deploy the network aware scheduler

After setting up a Kubernetes cluster, execute the following steps inside the *angelo1996/scheduler-plugins* project to build the network-aware scheduler:

- Build scheduler docker image (inside scheduler-plugins folder)
```
make local-image LOCAL_REGISTRY=ghcr.io/amarchese96 LOCAL_IMAGE=kube-scheduler:nascheduling-x RELEASE_VERSION=vx
```

- Push to remote registry
```
docker push ghcr.io/amarchese96/kube-scheduler:nascheduling-x
```

Execute the following steps inside this project to deploy the network-aware scheduler:

- Deploy scheduler with Helm
```
helm install nascheduler scheduler/chart --values scheduler/nascheduler.yml
```

- Clean up
```
helm uninstall nascheduler
```