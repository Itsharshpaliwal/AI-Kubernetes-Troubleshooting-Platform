# Monitoring

Monitoring is provided by kube-prometheus-stack.

Components:
- Prometheus: collects Kubernetes and node metrics
- Grafana: visualizes metrics in dashboards
- Alertmanager: handles alerts
- kube-state-metrics: exposes Kubernetes object/state metrics
- node-exporter: exposes node CPU, memory and system metrics

Installed using Helm:

helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update

helm upgrade --install kube-prometheus-stack \
  prometheus-community/kube-prometheus-stack \
  --namespace monitoring \
  --set grafana.service.type=NodePort \
  --set grafana.service.nodePort=30300 \
  --set prometheus.service.type=NodePort \
  --set prometheus.service.nodePort=30090 \
  --set prometheus.prometheusSpec.retention=7d
