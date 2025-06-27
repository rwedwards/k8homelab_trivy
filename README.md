# K8s Home Lab – Trivy Integration

This repository contains Kubernetes manifests and dashboards for integrating [Trivy Operator](https://github.com/aquasecurity/trivy-operator) into a home lab environment for security auditing and vulnerability visualization.

> ⚠️ **Disclaimer**  
> I am not the original creator of all included resources. This repo contains modified and customized versions of public resources for my own home lab. Credit belongs to the original authors and maintainers.

---

## 📦 Contents

### Dashboards

- `tryvy-dashboard_1.json`: Grafana dashboard visualizing Trivy vulnerability and configuration scan metrics (severity, namespace, cluster).

### Kubernetes Manifests

- `trivy-node-collector.yaml`: Job definition for collecting node-level vulnerabilities.
- `trivy-operator-metrics-svc.yaml`: Service exposing Prometheus metrics from the Trivy operator.
- `trivy-operator-servicemonitor.yaml`: ServiceMonitor for integrating Trivy metrics with Prometheus Operator.
- `trivy-servicemonitor.yaml`: Alternate or legacy ServiceMonitor.
- `trivy-values.yaml`: Helm values used to configure Trivy Operator during installation.

---

## 🔧 Usage

### 1. Install Trivy Operator with Helm

```bash
helm repo add aqua https://aquasecurity.github.io/helm-charts/
helm repo update
helm install trivy-operator aqua/trivy-operator \
  -n trivy-system --create-namespace \
  -f trivy-values.yaml
```

### 2. Apply Monitoring Manifests

```bash
kubectl apply -f trivy-operator-metrics-svc.yaml
kubectl apply -f trivy-operator-servicemonitor.yaml
```

*(Optional)* Apply node collector job:
```bash
kubectl apply -f trivy-node-collector.yaml
```

---

## 📊 Dashboard Import

1. Open Grafana → Dashboards → Import.
2. Upload `tryvy-dashboard_1.json`.
3. Select your Prometheus data source and finish.

---

## 🔒 Security Note

This repository contains no secrets or credentials. If you fork or modify these files for your own use, ensure any credentials (e.g., API keys) are stored securely using Kubernetes Secrets or GitHub Actions secrets.

---

## 🧾 License

MIT License

