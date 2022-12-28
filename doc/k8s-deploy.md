- Create kind cluster
```
kind create cluster --config kind-cluster.yml
```

- Install mentat component
```
kubectl apply -f mentat.yml
```

- Install Istio
```
istioctl install --set profile=demo -y
```

- Label default namespace
```
kubectl label namespace default istio-injection=enabled
```

- Install prometheus server
```
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm install prometheus prometheus-community/prometheus -n istio-system --values prometheus.yml
```

- Install grafana dashboard
```
helm repo add grafana https://grafana.github.io/helm-charts
helm install grafana grafana/grafana -n istio-system --values grafana.yml
```

- Install jaeger
```
kubectl apply -f jaeger.yml
```

- Install kiali
```
kubectl apply -f kiali.yml
```

- Install sophos-telemetry:
```
kubectl apply -f telemetry.yml
```

- Install sophos-cluster-monitor:
```
kubectl apply -f cluster-monitor.yml
```

- Install sophos-app-controller:
```
kubectl apply -f app-controller.yml
```

- Clean up
```
kubectl delete -f app-controller.yml
kubectl delete -f cluster-monitor.yml
kubectl delete -f telemetry.yml
kubectl delete -f kiali.yml
kubectl delete -f jaeger.yml
helm uninstall grafana -n istio-system
helm uninstall prometheus -n istio-system
istioctl manifest generate --set profile=demo | kubectl delete --ignore-not-found=true -f -
kubectl delete namespace istio-system
kubectl label namespace default istio-injection-
```