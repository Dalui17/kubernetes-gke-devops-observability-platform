# 🚀 Kubernetes HPA Setup & Autoscaling Workflow

## Step 1 — Deploy NGINX Application

```bash
kubectl apply -f nginx-deployment.yaml
```

Verify deployment:

```bash
kubectl get pods
kubectl describe deployment nginx-deployment
```

---

## Step 2 — Expose Application

```bash
kubectl expose deployment nginx-deployment \
--type=LoadBalancer \
--port=80 \
--name=nginx-service
```

Verify service:

```bash
kubectl get svc
```

---

## Step 3 — Install Metrics Server

```bash
kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml
```

Verify Metrics Server:

```bash
kubectl get apiservices | grep metrics
```

---

## Step 4 — Create Horizontal Pod Autoscaler

```bash
kubectl autoscale deployment nginx-deployment \
--cpu-percent=2 \
--min=2 \
--max=5
```

Verify HPA:

```bash
kubectl get hpa
```

---

## Step 5 — Generate Traffic Load

```bash
kubectl run -it --rm --image=busybox load-generator -- /bin/sh
```

Inside container:

```bash
while true; do wget -q -O- http://nginx-service; done
```

---

## Step 6 — Monitor Autoscaling

```bash
kubectl get pods -w
kubectl get hpa -w
```

---

# ✅ Result

* Automatic scale up during high CPU usage
* Dynamic scale down during low traffic
* Improved workload availability
* Better infrastructure utilization

```
```

