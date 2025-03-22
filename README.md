# prometheus-install
---

### Download Prometheus binary
```
https://prometheus.io/download/
```

-   Install

```
sudo wget https://github.com/prometheus/prometheus/releases/download/v2.53.4/prometheus-2.53.4.linux-amd64.tar.gz
```

```
sudo groupadd --system prometheus
```
```
sudo useradd -s /sbin/nologin --system -g prometheus prometheus
```
```
sudo mkdir /var/lib/prometheus
```
```
sudo mkdir -p /etc/prometheus/rules
```
```
sudo mkdir -p /etc/prometheus/rules.s
```
```
sudo mkdir -p /etc/prometheus/files_sd
```
```
sudo tar xvf prometheus-2.53.4.linux-amd64.tar.gz
```
```
cd prometheus-2.53.4.linux-amd64/
```
```
sudo mv prometheus promtool /usr/local/bin/
```
```
sudo mv prometheus.yml /etc/prometheus/prometheus.yml
```
```
 sudo tee /etc/systemd/system/prometheus.service<<EOF
 ```
-   in above command press enter than,
from this link
```
https://raw.githubusercontent.com/aussiearef/Prometheus/refs/heads/main/prometheus.service
```
copy content and paste
```
sudo chown -R prometheus:prometheus /etc/prometheus
```
```
sudo chown -R prometheus:prometheus /etc/prometheus/*
```
```
sudo chmod -R 755 /etc/prometheus
```
```
sudo chmod -R 755 /etc/prometheus/*
```
```
sudo chown -R prometheus:prometheus /var/lib/prometheus/
```
```
sudo  systemctl daemon-reload
```
```
sudo systemctl start prometheus
```
```
sudo systemctl enable prometheus
```
```
http://<ip>>:9090/
```

### Download Node Exporter
```
sudo wget https://github.com/prometheus/node_exporter/releases/download/v1.9.0/node_exporter-1.9.0.linux-amd64.tar.gz
```
```
sudo tar xvf node_exporter-1.9.0.linux-amd64.tar.gz
```
```
cd node_exporter-1.9.0.linux-amd64/
```

### Configure Node exporter with prometheus
-   go to 
```
cd /etc/prometheus/
```
```
sudo vim prometheus.yml
```
-   make config changes
```
scrape_configs:
  # The job name is added as a label `job=<job_name>` to any timeseries scraped from this config.
  - job_name: "prometheus"

    # metrics_path defaults to '/metrics'
    # scheme defaults to 'http'.

    static_configs:
      - targets: ["localhost:9090"]

  - job_name: "target-vm"

    # metrics_path defaults to '/metrics'
    # scheme defaults to 'http'.

    static_configs:
      - targets: ["104.215.252.204:9100"]
```
```
sudo systemctl stop prometheus
```
```
sudo systemctl start prometheus
```
-   now open prometheus, got to status and from there target.


### Run this command in node exporter vm
-   make sure to run this commands in node dir.
```
sudo groupadd --system prometheus
```
```
sudo useradd -s /sbin/nologin --system -g prometheus prometheus
```
```
sudo mkdir /var/lib/node/
```
```
sudo mv node_exporter /var/lib/node/
```
```
sudo vim /etc/systemd/system/node.service
```
-   add this
```
[Unit]
Description=Prometheus Node Exporter
Documentation=https://prometheus.io/docs/introduction/overview/
Wants=network-online.target
After=network-online.target

[Service]
Type=simple
User=prometheus
Group=prometheus
ExecReload=/bin/kill -HUP $MAINPID
ExecStart=/var/lib/node/node_exporter

SyslogIdentifier=prometheus_node_exporter
Restart=always

[Install]
WantedBy=multi-user.target
```
```
sudo chown -R prometheus:prometheus /var/lib/node/*
```
```
sudo chown -R prometheus:prometheus /var/lib/node
```
```
sudo chown -R 755 /var/lib/node
```
```
sudo chown -R 755 /var/lib/node/*
```
```
sudo systemctl daemon-reload
```
```
sudo systemctl start node
```
```
sudo systemctl enable node
```

## Grafana installation

```
sudo apt-get install -y adduser libfontconfig1 musl
```
navigate here
```
https://grafana.com/grafana/download
```
```
wget https://dl.grafana.com/enterprise/release/grafana-enterprise_11.5.2_amd64.deb
```
```
sudo dpkg -i grafana-enterprise_11.5.2_amd64.deb
```
```
sudo dpkg -i grafana-enterprise_11.5.2_amd64.deb
```
```
sudo /bin/systemctl daemon-reload
```
```
sudo /bin/systemctl enable grafana-server
```
```
sudo /bin/systemctl start grafana-server
```
# Install Loki
```
sudo apt-get install loki
```

# Install Promtail
```
wget https://github.com/grafana/loki/releases/download/v3.4.2/promtail-linux-amd64.zip
```
github link for binary
```
https://github.com/grafana/loki/releases
```
```
unzip promtail-linux-amd64.zip
```
```
sudo mv promtail-linux-amd64 /usr/local/bin/promtail
```
```
sudo chmod +x /usr/local/bin/promtail
```
```
cd /etc/
```
```
sudo mkdir promtail
```
```
cd promtail/
```
