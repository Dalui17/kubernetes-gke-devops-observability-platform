# 🚀 Kubernetes Monitoring Stack Setup

## Step 1 — Create Namespace

```bash
kubectl create ns monitor
```

---

## Step 2 — Add Helm Repository

```bash
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts

helm repo update
```

---

## Step 3 — Install Prometheus & Grafana Stack

```bash
helm install kube-prometheus-stack \
prometheus-community/kube-prometheus-stack \
--namespace monitor
```

---

## Step 4 — Verify Installation

```bash
kubectl get pods -n monitor
kubectl get svc -n monitor
kubectl get deploy -n monitor
```

---

## Step 5 — Expose Grafana Dashboard

```bash
kubectl expose deployment kube-prometheus-stack-grafana \
--port=3000 \
--target-port=3000 \
--name=grafana \
--type=LoadBalancer \
-n monitor
```

---

## Step 6 — Retrieve Grafana Admin Password

```bash
kubectl --namespace monitor get secrets kube-prometheus-stack-grafana \
-o jsonpath="{.data.admin-password}" | base64 -d ; echo
```

---

## Step 7 — Access Grafana

```bash
http://<EXTERNAL-IP>:3000
```

Default Credentials:

```text
Username: admin
Password: Retrieved from Kubernetes Secret
```

---

## Step 8 — Explore Dashboards

### Kubernetes Monitoring Dashboards

* Compute Resources / Cluster
* Compute Resources / Namespace
* Node Resource Monitoring
* Pod Monitoring
* Workload Metrics

---

# ✅ Result

* Real-time Kubernetes monitoring
* Prometheus metrics collection
* Grafana dashboard visualization
* Namespace-level observability
* Cluster resource visibility

```
```

