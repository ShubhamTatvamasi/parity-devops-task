# parity-devops-task

### Download helm charts

```bash
helm fetch --untar stable/nginx-ingress
helm fetch --untar stable/prometheus
helm fetch --untar stable/grafana
```
> this part is already done and code is added on this repo
---

### Ingress

Install: Ingress controller
```bash
helm install ingress ./nginx-ingress --values ./nginx-ingress/myvalues.yaml
```

Add TLS certificate as secret for Ingress
```bash
kubectl create secret tls shubhamtatvamasi-tls \
  --key ./shubhamtatvamasi.com.key \
  --cert ./fullchain.cer
```

Check the changes done as compared to original values
```bash
diff ./nginx-ingress/values.yaml ./nginx-ingress/myvalues.yaml
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

Install: Prometheus
```bash
helm install prometheus ./prometheus --values ./prometheus/myvalues.yaml
```

Check the changes done as compared to original values
```bash
diff ./prometheus/values.yaml ./prometheus/myvalues.yaml
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

Install Dashboards:

Dashboard | ID
--- | --- 
Kubernetes Pods | 6336
Kubernetes Deployment | 8588
Node Exporter Full | 1860
Node Exporter for Prometheus | 11074

Install: Grafana
```bash
helm install grafana ./grafana --values ./grafana/myvalues.yaml
```

Check the changes done as compared to original values
```bash
diff ./grafana/values.yaml ./grafana/myvalues.yaml
```
---

### polkadot

Deploy polkadot node
```bash
kubectl apply -f polkadot.yaml
```
---

### Deleting Everything

```bash
helm uninstall ingress
helm uninstall prometheus
helm uninstall grafana
kubectl delete secret shubhamtatvamasi-tls
kubectl delete -f pv.yaml
kubectl delete -f polkadot.yaml
```
