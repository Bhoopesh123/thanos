# Setting Up Thanos with S3 Using Kubernetes 

Thanos is a highly available Prometheus setup that provides global query, long-term storage, and deduplication. Using S3 as the object store allows your metrics to persist safely in the cloud. This guide walks you through setting up Thanos with Docker.

helm repo update
helm upgrade --install prometheus prometheus-community/kube-prometheus-stack -f values.yaml

helm repo add bitnami https://charts.bitnami.com/bitnami
helm repo update
helm upgrade --install thanos bitnami/thanos -f thanos-values.yaml

##################

kubectl create namespace monitoring
kubectl apply -f https://raw.githubusercontent.com/prometheus-operator/prometheus-operator/main/bundle.yaml

helm install node-exporter prometheus-community/prometheus-node-exporter

helm upgrade [RELEASE_NAME] oci://ghcr.io/prometheus-community/charts/prometheus --install

helm upgrade --install prometheus prometheus-community/prometheus -f values.yaml
helm upgrade --install grafana grafana/grafana 

count({__name__=~".+"}) by (job)

