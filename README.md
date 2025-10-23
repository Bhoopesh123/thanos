# Setting Up Thanos with S3 Using Docker 

Thanos is a highly available Prometheus setup that provides global query, long-term storage, and deduplication. Using S3 as the object store allows your metrics to persist safely in the cloud. This guide walks you through setting up Thanos with Docker.

# Prerequisites 
Docker & Docker Compose installed
AWS S3 bucket (or MinIO) ready
Basic familiarity with Prometheus

# 1: Prepare Directories 
mkdir -p prometheus_data thanos_data
sudo chown -R 65534:65534 prometheus_data thanos_data

# 2: Configure S3 Object Storage 
Create objstore.yml for Thanos:

# 3: Create Docker Compose File 
Set up Prometheus, Thanos Sidecar, Store, Query, and optionally Grafana:
Create docker-compose.yml file.

# 4: Launch the Stack
    docker compose up -d

Check logs to ensure the sidecar uploads TSDB blocks to S3:
    docker logs thanos-sidecar | grep upload

# 5: Connect Grafana
    Add a new data source in Grafana of type Prometheus
    Use the Thanos Query HTTP endpoint URL
    Example: http://<public-ip>:10905
    Save & Test → you should see metrics from Prometheus

# 6: Verify Thanos Uploads 

In S3, you should now see Thanos TSDB blocks being created and updated. This confirms long-term storage is working.