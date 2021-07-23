# Healthwatch Exporter for TAS for VMs Architecture


## High Level Points

- The Healthwatch Exporter for TAS for VMs  tile deploys metric exporter VMs to generate each type of metric related to the health of your TAS for VMs deployment.

- Healthwatch Exporter > Loggregator Firehose - Out to prometheus endpoint setup  on the associated exporter VMs.  

- The prometheus instance that exists scrapes the exposition endpoint on the metric exporter vis and imports those metrics into your monitoring system. 


## Monitoring TAS for VMs on a Single Ops Manager Foundation
If you only want to monitor a single Ops Manager foundation that has TAS for VMs installed. : 

- Install the Healthwatch tile 
- Install Healthwatch Exporter for TAS for VMs on the same foundation. 

 The Healthwatch tile automatically detects Healthwatch Exporter for TAS for VMs on the same foundation and adds a scrape job for Healthwatch Exporter for TAS for VMs to the Prometheus instance.



## Monitoring TAS for VMs on a Different Ops Manager Foundation

You can monitor several Ops Manager foundations that have TAS for VMs installed from a Healthwatch tile that you install on a separate Ops Manager foundation or the TKGI 

- Install the Healthwatch tile (Ops Manager foundation or the TKGI Control Plane) 

- Install Healthwatch Exporter for TAS for VMs 

- Open the ports for the metric exporter VMs that Healthwatch Exporter for TAS for VMs deploys on each Ops Manager foundation you want to monitor. 
( All exporter VMS must be setup with Static IPS to allow for rules to be created ) 


![](Healthwatch%20Exporter%20for%20TAS%20for%20VMs%20Architecture/Screenshot%202021-07-23%20at%2011.12.02.png)



Once you have installed Healthwatch Exporter for TAS for VMs and opened the required ports on each Ops Manager foundation you want to monitor.

You then need to dd a scrape job for each Healthwatch Exporter for TAS for VMs tile in the **Prometheus Configuration** pane of the Healthwatch tile  that you installed on your monitoring Ops Manager foundation or the TKGI Control Plane. **


`It doesnt mention additional FW rules but I would assume rules need to be setup to allow Foundation X to scrape Foundation Y's Metrics`


```
1	Retrieve the Ops Manager root certificate authority (CA) for the foundation you want to monitor. For more information, see Retrieve the Ops Manager Root CA in Managing Certificates with the Ops Manager API in the Ops Manager documentation.

2	Nagivate to the Ops Manager Installation Dashboard for the foundation you want to monitor.

3	Click the Healthwatch Exporter for Tanzu Application Service tile.

4	Select the Credentials tab.

5	In the row for Healthwatch Exporter Client Mtls, click Link to Credential.

6  Record the credentials for Healthwatch Exporter Client Mtls.

7	 Navigate to the Healthwatch tile installed on your monitoring Ops Manager foundation or the TKGI Control Plane.

8	 Select Prometheus Configuration.

9  Under Additional Scrape Config Jobs, click Add.

10 For TSDB Scrape job, provide the configuration YAML for the scrape job for Healthwatch Exporter for TAS for VMs, similar to the following example:
- job_name: FOUNDATION-NAME
  metrics_path: /metrics
  scheme: https
  static_configs:
    - targets:
      - "<gauge exporter ip>:9090"
      - "<counter exporter ip>:9090"
      - "<timer exporter ip>:9090"

Where FOUNDATION-NAME is the name of the foundation you want to monitor.

18 	For TLS Config Certificate Authority, enter the Ops Manager root CA that you retrieved in a previous step.

19 	For TLS Config Certificate and Private Key, enter the certificate and private key from Healthwatch Exporter Client Mtls that you recorded from the Credentials tab in the Healthwatch Exporter for TAS for VMs tile in a previous step.
	
20 	For TLS Config Server Name, enter the name of the server that facilitates TLS communication between the Prometheus instance in the Healthwatch tile and the metric exporter VMs that Healthwatch Exporter for TAS for VMs deploys.

```

Section within OpsManager for creating Job scrape 
![](Healthwatch%20Exporter%20for%20TAS%20for%20VMs%20Architecture/Screenshot%202021-07-23%20at%2011.21.58.png)




#Work/products/healthwatch
