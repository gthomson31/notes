# Configuring Grafana

## Load Balancing and DNS 
[Configuring DNS for Your Grafana Instance |    Pivotal Docs](https://docs.pivotal.io/healthwatch/2-1/configuring/dns-configuration.html)

Configuring a DNS entry for your Grafana instance enables users to access the Grafana UI more easily from outside your BOSH network, including from the links to the Grafana UI that Alertmanager provides in alert messages

To avoid creating an unnecessary dependency on VMware Tanzu Application Service for VMs (TAS for VMs), Healthwatch does not use a Gorouter in TAS for VMs to route the Grafana instance to a subdomain for your foundation. 

To facilitate user access to the Grafana UI, you must configure a DNS entry for either the public IP address of a single Grafana VM or the load balancer in front of the Grafana instance.


```
To add a LB for use with Grafana 

1 Select **Resource Config**.
2 (Optional) To scale a job, select an option from the dropdown for the resource you want to modify:
	* **Instances:** Configures the number of instances each job has.
	* **VM Type:** Configures the type of VM used in each instance.
	* **Persistent Disk Type:** Configures the amount of persistent disk space to allocate to the job.
3 (Optional) To add a load balancer to a job:
	* Click the icon next to the job name.
	* For **Load Balancers**, enter the name of your load balancer.
	* Ensure that the **Internet Connected** checkbox is disabled. Enabling this checkbox gives VMs a public IP address that enables outbound Internet access.
4 Click **Save**.

```




## Overview of Firewall Policies for the Grafana Instance
In the Healthwatch tile, allowing external access to individual VMs is disabled by default. Creating a firewall policy for your Grafana instance enables users to access the Grafana UI more easily from outside your BOSH network, including from the links to the Grafana UI that Alertmanager provides in alert messages.

You create firewall policies in the console for your Ops Manager deployment’s IaaS. 

To create a firewall policy for your Grafana instance, see the section for your IaaS:
[Creating a Firewall Policy for Your Grafana Instance |    Pivotal Docs](https://docs.pivotal.io/healthwatch/2-1/configuring/iaas-configuration.html#vsphere)

```
Create a Firewall Policy in vSphere NSX-V
To create a firewall policy in vSphere NSX-V:
	1	Log in to vSphere.
	2	Click Networking & Security.
	3	Select NSX Edges.
	4	Double-click the Edge for your TAS for VMs deployment.
	5	Select Manage.
	6	Select Firewall.
	7	To create the first rule:
	a	Click the Add icon.
	b	For Name, enter a name for the first rule.
	c	For Source, select Any.
	d	For Destination, enter the public IP address for your Grafana instance or the load balancer for your Grafana instance.
	e	For Service, select Any.
	8	To create the second rule:
	a	Click the Add icon.
	b	For Name, enter a name for the first rule.
	c	For Source, select Any.
	d	For Destination, enter the public IP address for your Grafana instance or the load balancer for your Grafana instance.
	e	For Service, select Any.
	9	Click Publish Changes.

```



## Configure LDAP Authentication
[Configuring Grafana Authentication |    Pivotal Docs](https://docs.pivotal.io/healthwatch/2-1/configuring/grafana-authentication.html)

```
Configure LDAP Authentication
When you configure LDAP authentication for the Grafana UI, users can log in to the Grafana UI with their LDAP credentials. You can also create mappings between LDAP group memberships and Grafana org user roles. For more information about configuring LDAP authentication, see LDAP Authentication in the Grafana documentation.

To configure LDAP authentication for the Grafana UI:
	1	Navigate to the Ops Manager Installation Dashboard.
	2	Click the Healthwatch tile.
	3	Select Grafana Configuration.
	4	Under Select an authentication mechanism for Grafana, select LDAP.
	5	For Host, enter the network address of your LDAP server host. This network address appears as the host property in the [auth.ldap] section of the Grafana configuration file.

	6	(Optional) For Port, enter the port for your LDAP server host. The default port is 389 when the Use SSL checkbox is disabled, or 636 when the Use SSL checkbox is enabled. This port appears as the port property in the [auth.ldap] section of the Grafana configuration file.

	7	(Optional) To allow new users to log in to the Grafana UI with their existing LDAP credentials, enable the Allow sign up checkbox. This checkbox is enabled by default. Disabling this checkbox prevents users without a pre-existing Grafana account from logging in to the Grafana UI with their existing LDAP credentials. This checkbox appears as the allow_sign_up property in the [auth.ldap] section of the Grafana configuration file.

	8	(Optional) To enable the LDAP server to communicate with the Grafana instance over TLS when authenticating user credentials, enable the Use SSL checkbox. This checkbox is disabled by default. This checkbox appears as the use_ssl property in the [auth.ldap] section of the Grafana configuration file.

	9	(Optional) To enable the LDAP server to run the STARTTLS command when communicating with the Grafana instance over TLS, enable the Start TLS checkbox. This checkbox is disabled by default. This checkbox appears as the start_tls property in the [auth.ldap] section of the Grafana configuration file.

	10	(Optional) To enable the Grafana instance to skip SSL validation when communicating with the LDAP server over TLS, enable the Skip SSL Verification checkbox. This checkbox is disabled by default. This checkbox appears as the ssl_skip_verify property in the [auth.ldap] section of the Grafana configuration file.

	11	(Optional) For Bind DN, enter the distinguished name (DN) for binding to the LDAP server. For example, "cn=admin,dc=grafana,dc=org". This DN appears as the bind_dn property in the [auth.ldap] section of the Grafana configuration file.

	12	(Optional) For Bind password, enter the password for binding to the LDAP server. For example, grafana. This password appears as the bind_password property in the [auth.ldap] section of the Grafana configuration file.

	13	(Optional) For User search filter, enter a regex string that defines LDAP user search criteria. For example, "(cn=%s)". This string appears as the search_filter property in the [auth.ldap] section of the Grafana configuration file.

	14	(Optional) For Search base DNS, enter an array of base DNs in the LDAP directory tree from which any LDAP user search begins. The typical LDAP search base matches your domain name. For example, "dc=grafana,dc=org". This array appears as the search_base_dns property in the [auth.ldap] section of the Grafana configuration file.

	15	(Optional) For Group search filter, enter a regex string that defines LDAP group search criteria. For example, "(&(objectClass=posixGroup)(memberUid=%s))". This string appears as the group_search_filter property in the [auth.ldap] section of the Grafana configuration file.

	16	(Optional) For Group search base DNS, enter an array of base DNs in the LDAP directory tree from which any LDAP group search begins. For example, "ou=groups,dc=grafana,dc=org". This array appears as the group_search_base_dns property in the [auth.ldap] section of the Grafana configuration file.

	17	(Optional) For Group search filter user attribute, enter a value that defines which user attribute is substituted for %s in the regex string you entered for Group search filter. You can use the value of any property under [server.attributes] in the [auth.ldap] section of the Grafana configuration file. The default value is the value of the username property. This value appears as the group_search_filter_user_attribute property in the [auth.ldap] section of the Grafana configuration file.

	18	(Optional) For Server attributes, enter in TOML format tables of the LDAP attributes that your LDAP server uses. Each table must use the table name [servers.attributes]. These tables appear under [servers.attributes] in the [auth.ldap] section of the Grafana configuration file.

	19	(Optional) For Server group mappings, enter in TOML format an array of tables of LDAP groups mapped to a Grafana org and role. Each table must use the table name [[servers.group_mappings]]. This array of tables appears under a [[servers.group_mappings]] heading in the [auth.ldap] section of the Grafana configuration file. For more information, see Group Mappings in LDAP Authentication in the Grafana documentation.

	20	(Optional) To configure TLS communication between the Grafana instance and your LDAP server:
	a	For TLS Credentials, provide at least one certificate and private key to enable TLS communication between the Grafana instance and your LDAP server. These certificates and private keys appear as the client_cert and client_key properties in the [auth.ldap] section of the Grafana configuration file.
	b	For TLS CA, provide a CA that signs the certificates you provide in the TLS Credentials field above. This CA appears as the root_ca_cert property in the [auth.ldap] section of the Grafana configuration file.
	21	Click Save.
```

#Work/products/healthwatch
