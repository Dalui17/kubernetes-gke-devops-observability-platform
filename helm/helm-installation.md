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


## Official Metrics Server Deployment

Metrics Server was installed using the official Kubernetes SIGs release manifest:

[Metrics Server Components YAML](https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml?utm_source=chatgpt.com)

Deployment Command:

```bash
kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml
```

# 🔗 Official Helm & Monitoring Resources

This project uses the official Prometheus Community Helm charts and Prometheus Operator stack.

### Official Repositories

* [Prometheus Community Helm Charts GitHub Repository](https://github.com/prometheus-community/helm-charts/tree/main/charts/kube-prometheus-stack?utm_source=chatgpt.com)

* [Prometheus Community Helm Repository](https://prometheus-community.github.io/helm-charts?utm_source=chatgpt.com)

* [Prometheus Operator kube-prometheus Project](https://github.com/prometheus-operator/kube-prometheus?utm_source=chatgpt.com)

```
```
