# Setting Up Thanos with S3 Using Kubernetes 

Thanos is a highly available Prometheus setup that provides global query, long-term storage, and deduplication. Using S3 as the object store allows your metrics to persist safely in the cloud. This guide walks you through setting up Thanos with Docker.  


    helm repo update

    kubectl apply -f thanos-secret.yaml
    helm upgrade --install prometheus prometheus-community/prometheus -f values.yaml

    helm upgrade --install grafana grafana/grafana 

Install Thanos Componenets  

    kubectl apply -f thanos-query.yaml
    kubectl apply -f thanos-store.yaml
    kubectl apply -f thanos-compactor.yaml


Check the metrics via below magic query  

    count({__name__=~".+"}) by (job)

Import the dashboard: 1860
Add the below Thanos query datasource  

    url: http://thanos-query:9090
    Type: Prometheus



