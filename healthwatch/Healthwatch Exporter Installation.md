# Healthwatch Exporter Installation 
## High Level Points
Unless you are an advanced user, VMware recommends configuring and deploying your tile manually the first time, so you can see which properties in the automation script correlate to the configuration settings present in the tile UI before you modify and re-deploy the tile with the om CLI.

Below is an example of an automation script that configures and deploys the Healthwatch tile:

```
product-name: p-healthwatch2
product-properties:
  .properties.scrape_configs:
    value:
      - ca: |
          -----BEGIN CERTIFICATE-----
          SECRET
          -----END CERTIFICATE-----
        scrape_job: |
          job_name: foundation1
          metrics_path: /metrics
          scheme: https
          static_configs:
            - targets:
              - "1.2.3.4:9090"
              - "5.6.7.8:9090"
        server_name: pasexporter
        tls_certificates:
          cert_pem: |
            -----BEGIN CERTIFICATE-----
            SECRET
            -----END CERTIFICATE-----
          private_key_pem: |
            -----BEGIN RSA PRIVATE KEY-----
            SECRET
            -----END RSA PRIVATE KEY-----
      - ca: |
          -----BEGIN CERTIFICATE-----
          SECRET
          -----END CERTIFICATE-----
        scrape_job: |
          job_name: foundation2
          metrics_path: /metrics
          scheme: https
          static_configs:
            - targets:
              - "9.10.11.12:9090"
        server_name: pasexporter
        tls_certificates:
          cert_pem: |
            -----BEGIN CERTIFICATE-----
            SECRET
            -----END CERTIFICATE-----
          private_key_pem: |
            -----BEGIN RSA PRIVATE KEY-----
            SECRET
            -----END RSA PRIVATE KEY-----
  .properties.grafana_authentication:
    selected_option: basic
    value: basic
  .tsdb.canary_exporter_port:
    value: 9115
  .tsdb.scrape_interval:
    value: 15s
  .grafana.enable_login_form:
    value: true
network-properties:
  network:
    name: subnet1
  other_availability_zones:
  - name: us-central1-f
  - name: us-central1-c
  - name: us-central1-b
  singleton_availability_zone:
    name: us-central1-f
resource-config:
  pxc:
    instances: automatic
    persistent_disk:
      size_mb: automatic
    instance_type:
      id: automatic
    internet_connected: true
    max_in_flight: 5
  pxc-proxy:
    instances: automatic
    persistent_disk:
      size_mb: automatic
    instance_type:
      id: automatic
    internet_connected: true
    max_in_flight: 5
  tsdb:
    instances: automatic
    persistent_disk:
      size_mb: automatic
    instance_type:
      id: automatic
    internet_connected: true
    max_in_flight: 1
  grafana:
    instances: automatic
    persistent_disk:
      size_mb: automatic
    instance_type:
      id: automatic
    internet_connected: true
    max_in_flight: 5
errand-config:
  smoke-test:
    post-deploy-state: true
  update-admin-password:
    post-deploy-state: true
```

- Already installed within the LAB currently 
- We could utilise OM CLI to pull down the tile configuration to allow us to create the  automation ? 




#Work/products/healthwatch
