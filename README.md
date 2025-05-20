# grafana-prometheus
How to configure grafana in local machine

# Monitoring Setup with Prometheus and Grafana

## 1. Install Prometheus and node_exporter

- Download and extract Prometheus: use this below command to extract prometheus
````
 wget https://github.com/prometheus/prometheus/releases/download/v2.52.0/prometheus-2.52.0.linux-amd64.tar.gz
 tar -xvzf prometheus-2.52.0.linux-amd64.tar.g
````
# Download node_exporter
````
wget https://github.com/prometheus/node_exporter/releases/latest/download/node_exporter-*.linux-amd64.tar.gz
````
# Extract it
````
tar -xvzf node_exporter-*.linux-amd64.tar.gz
cd node_exporter-*.linux-amd64
````
# Start node_exporter
````
./node_exporter
```` 
Node Exporter will now run on port 9100.
Download and extract node_exporter similarly.

## 2. Configure prometheus.yml

```yaml
scrape_configs:
- job_name: 'prometheus'
  static_configs:
    - targets: ['localhost:9090']

- job_name: 'node_exporter'
  static_configs:
    - targets: ['localhost:9100']
```
## 3. Start Prometheus
````
   ./prometheus --config.file=prometheus.yml &    ---->use this command to execute prometheus and
````
## For Node Exporter (CPU metrics)
````
wget https://github.com/prometheus/node_exporter/releases/download/v1.8.1/node_exporter-1.8.1.linux-amd64.tar.gz
tar -xvzf node_exporter-1.8.1.linux-amd64.tar.gz
cd node_exporter-1.8.1.linux-amd64
./node_exporter
````
## Start Grafana (if not already running)
  If Grafana is installed, start it:
````
sudo systemctl start grafana-server
sudo systemctl enable grafana-server
````
## Access Grafana:
🖥️ Open your browser → Visit: http://<web1-ip>:3000
Default login: admin
Username: admin
Password: admin (you'll be asked to change it)

##  Add Prometheus in Grafana
 -> Open Grafana → ⚙️ Configuration → Data Sources
 -> Click Add Data Source
 -> Delect Prometheus
 -> Set URL to: http://localhost:9090
 -> Click Save & Test

## 6: Create CPU Usage Panel in Grafana
  -> Go to + Create → Dashboard → Add new panel
  -> Use this query:
```
100 - (avg by(instance) (rate(node_cpu_seconds_total{mode="idle"}[5m])) * 100)
```
  -> Choose Time Series or Gauge
  -> Title: CPU Usage
  -> Click Apply
Click Save & Test – it should say “Data source is working”





