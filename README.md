# parity-devops-task

### Ingress

Download and Install: Ingress controller
```bash
helm fetch --untar stable/nginx-ingress
helm install ingress ./nginx-ingress --values ./nginx-ingress/myvalues.yaml
```

Check the changes done as compared to original values
```bash
diff ./nginx-ingress/values.yaml ./nginx-ingress/myvalues.yaml
```

Add TLS certificate as secret for Ingress
```bash
kubectl create secret tls shubhamtatvamasi-tls \
  --key ./shubhamtatvamasi.com.key \
  --cert ./fullchain.cer
```
> letsencrypt certificate used for this

Delete Ingress controller
```bash
helm uninstall ingress
```

Delete TLS Certificate
```bash
kubectl delete secret shubhamtatvamasi-tls
```
---

### Prometheus

GUI | URL
--- | --- 
Alert Manager | https://alertmanager.shubhamtatvamasi.com:32443
Push Gateway | https://pushgateway.shubhamtatvamasi.com:32443
Prometheus | https://prometheus.shubhamtatvamasi.com:32443

Create Persistent Volume for prometheus
```bash
kubectl apply -f pv.yaml
```
> this also includes PersistentVolume for grafana

Download and Install: Prometheus
```bash
helm fetch --untar stable/prometheus
helm install prometheus ./prometheus --values ./prometheus/myvalues.yaml
```

Check the changes done as compared to original values
```bash
diff ./prometheus/values.yaml ./prometheus/myvalues.yaml
```

Delete Prometheus 
```bash
helm uninstall prometheus
```
---

### Grafana

GUI | URL
--- | --- 
Grafana | https://grafana.shubhamtatvamasi.com:32443

Login credentials for grafana
```
ID: admin
Pass: strongpassword
```

Add prometheus datasource
```
http://prometheus-server
```

Dashboard | ID
--- | --- 
Kubernetes | 8588
Node Exporter for Prometheus | 11074
Polkadot metrics | 11171

Download and Install: Grafana
```bash
helm fetch --untar stable/grafana
helm install grafana ./grafana --values ./grafana/myvalues.yaml
```

Check the changes done as compared to original values
```bash
diff ./grafana/values.yaml ./grafana/myvalues.yaml
```

Delete Grafana 
```bash
helm uninstall grafana
```
---

### polkadot


docker run --rm -it chevdor/polkadot:latest polkadot --version

parity/polkadot

https://polkascan.io/pre/westend

docker run -d -p 30333:30333 -p 9933:9933 -v $PWD/data:/data chevdor/polkadot polkadot --chain westend


docker run --rm parity/polkadot --help

docker run --rm parity/polkadot --version

docker run --rm parity/polkadot --light --alice

/polkadot/.local/share/polkadot

curl -s https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3 | bash

helm repo add stable https://kubernetes-charts.storage.googleapis.com/

helm repo update

helm install prometheus stable/prometheus

helm install stable/prometheus

helm fetch --untar stable/prometheus

helm install prometheus stable/prometheus --values myvalues.yaml .

parity.shubhamtatvamasi.com:30080


