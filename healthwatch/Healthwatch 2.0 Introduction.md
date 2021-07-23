# Healthwatch 2.0 Introduction 

## High Level Points 
- Three tiles make up the Healthwatch 2.0 Architecture - Healthwatch, Healthwatch Exporter  for TAS and Healthwatch Exporter for TKGI .

- A Complete Healthwatch install consist of the Healthwatch tile and at least one Healthwatch exporter tile. 

- A Healthwatch exporter tile must be installed in order to allow monitoring of the foundation however the logs can be sent to a Healthwatch tile on either the same foundation or different depending on requirements. ( Think centralised logging solution ) 

## Healthwatch Tile Architecture
### Healthwatch Tile component makeup 
	- Prometheus
	- Grafana
	- MySQL
	- NGINX Proxy ( In front of prometheus for load balancing) 


Prometheus  scrapes the log endpoints generated on the Exporter VMS to enable you to use alert manager to configure alerts based on the log output. 

NOTE: 
`The MySQL instance that the Healthwatch tile deploys only stores your Grafana settings, and does not store any time-series data.`


The diagram below illustrates how metrics travel from the Healthwatch Exporter tiles through Prometheus and Grafana. 

It also shows how metrics travel through Prometheus to Alert Manager.

![](Healthwatch%202.0%20Introduction/82E5C817-35FA-4320-BCC2-AD586E31FEA2.png)


#Work/products/healthwatch
