# 🚀 Helm Installation & Kubernetes Monitoring Stack

This monitoring stack was deployed using the official Prometheus Community Helm charts and Prometheus Operator ecosystem.

---


# 📌 Official Helm & Monitoring Resources

## Prometheus Community Helm Charts GitHub Repository

https://github.com/prometheus-community/helm-charts/tree/main/charts/kube-prometheus-stack

---

## Prometheus Community Helm Repository

https://prometheus-community.github.io/helm-charts

---

## Prometheus Operator kube-prometheus Project

https://github.com/prometheus-operator/kube-prometheus

---

# Step 1 — Create Monitoring Namespace

```bash id="5jlwm"
kubectl create ns monitor
```

---

# Step 2 — Add Helm Repository

```bash id="5jlwm"
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts

helm repo update
```

---

# Step 3 — Install Prometheus & Grafana Stack

```bash id="5jlwm"
helm install kube-prometheus-stack \
prometheus-community/kube-prometheus-stack \
--namespace monitor
```

---

# Step 4 — Verify Installation

```bash id="5jlwm"
kubectl get pods -n monitor

kubectl get svc -n monitor

kubectl get deploy -n monitor
```

---

# Step 5 — Expose Grafana Dashboard

```bash id="5jlwm"
kubectl expose deployment kube-prometheus-stack-grafana \
--port=3000 \
--target-port=3000 \
--name=grafana \
--type=LoadBalancer \
-n monitor
```

---

# Step 6 — Retrieve Grafana Admin Password

```bash id="5jlwm"
kubectl --namespace monitor get secrets kube-prometheus-stack-grafana \
-o jsonpath="{.data.admin-password}" | base64 -d ; echo
```

---

# Step 7 — Access Grafana Dashboard

```text id="5jlwm"
http://<EXTERNAL-IP>:3000
```

Default Username:

```text id="5jlwm"
admin
```

---

# Step 8 — Explore Kubernetes Dashboards

Example dashboards:

* Kubernetes / Compute Resources / Cluster
* Kubernetes / Compute Resources / Namespace (Pods)
* Node Resource Monitoring
* Workload Monitoring
* Pod Metrics & CPU Usage

---

# ✅ Components Installed

* Prometheus
* Grafana
* Alertmanager
* Node Exporter
* kube-state-metrics

---

# ✅ Final Result

* Real-time Kubernetes monitoring
* Grafana dashboard visualization
* Prometheus metrics collection
* Namespace-level observability
* Cluster resource visibility
* Enterprise-style monitoring platform
