# parity-devops-task

### Ingress

Download Ingress chart
```bash
helm fetch --untar stable/nginx-ingress
```
> this part is already done and code in added on the repo

Install: Ingress controller
```bash
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

Download Prometheus chart
```bash
helm fetch --untar stable/prometheus
```
> this part is already done and code in added on the repo

Install: Prometheus
```bash
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

Two Dashboard Installed as of now

Dashboard | ID
--- | --- 
Kubernetes | 8588
Node Exporter for Prometheus | 11074

Download Grafana chart
```bash
helm fetch --untar stable/grafana
```
> this part is already done and code in added on the repo

Install: Grafana
```bash
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

Deploy polkadot node
```bash
kubectl apply -f polkadot.yaml
```

Delete polkadot node
```bash
kubectl delete -f polkadot.yaml
```
