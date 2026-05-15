# 🚀 Helm Installation & Monitoring Stack Deployment

## Add Prometheus Community Helm Repository

```bash
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts

helm repo update
```

---

## Install kube-prometheus-stack

```bash
helm install kube-prometheus-stack \
prometheus-community/kube-prometheus-stack \
--namespace monitor
```

---

## Verify Deployment

```bash
kubectl get pods -n monitor

kubectl get svc -n monitor

kubectl get deploy -n monitor
```

---

## Expose Grafana Dashboard

```bash
kubectl expose deployment kube-prometheus-stack-grafana \
--port=3000 \
--target-port=3000 \
--name=grafana \
--type=LoadBalancer \
-n monitor
```

---

## Retrieve Grafana Admin Password

```bash
kubectl --namespace monitor get secrets kube-prometheus-stack-grafana \
-o jsonpath="{.data.admin-password}" | base64 -d ; echo
```

---

## Access Grafana

```text
http://<EXTERNAL-IP>:3000
```

Default Username:

```text
admin
```

---

# ✅ Components Installed

* Prometheus
* Grafana
* Alertmanager
* Node Exporter
* kube-state-metrics

---

# ✅ Result

* Kubernetes cluster observability
* Real-time monitoring dashboards
* Namespace-level visibility
* CPU and memory utilization tracking
* Enterprise-grade monitoring setup

```
```
