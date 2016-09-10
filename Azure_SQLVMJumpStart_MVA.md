## SQL Azure on VM Role Jump Start MVA

[Link](https://mva.microsoft.com/en-US/training-courses/sql-azure-on-vm-role-jump-start-8293?l=2OlYzCYy_1004984382)

### SQL Server Cloud Continuum

Goes from high copntrol and high maintenance
To Low control and low maintenance
Goes from dedicated high cost 
To shared lower cost

1. Physical
1. Virtual
1. IaaS
1. PaaS
1. SaaS 

### Windows Azure VMs

* **VMs hosted on Windows Azure Infrastructure ("IaaS")**
* Can take your own image
* Fast provision
* Remote desktop and powershell

* **Pay per use**
* VM by minute: Size and Licensing
**If stop machine still pay for the storage!**
* Network: Outgoing only costs, not incoming
* Only pay for storage used so can over provision

* **Elasticity**
* Can go from small VM to very large VM 

* **You manage the VM**
* Security, patching, monitoring etc 

### Storage 

* Every VM dish is a BLOB in Azure Storage
* 3 Sync local copies
* No data loss
* High availability (transparent to VM)
* 3 more async remote copies (geo-replication, other data centres!)
* For disaster recovery and managed by microsoft
* These remote copies are optional

### Availbility

* SLA: No data loss
* If becomes unavailable, restart in another host
* SLA: 1of 2 VMs in availability set
* Different racks are available 
* 99.95% (less that 22 minutes downtime per month)
* Includes planned updates, like patches etc 

* **High availability**
* Availability set: this is option when create 
* Load balanced set with load balancer
* All requests load balanced between two machines
* If one machine becomes unavailable can go to the other one

### Connectivity

* Over internet via public endpoints
* Over a site-to-site tunnel
* Extend on premise network to Azure
* Can join Azure VMs to on premise domain
* Secure tunnel 
* VPB Device (hardware) / Windows Server RRAS (software) solutions

* **External Connectivity**
* CISCO, CITRIX, JUNIPER, WatchGuard

* **DNS namne is how people connect over the internet**

* **As soon as SQL is available it is in azure as an image in the gallery!**
* There are images specific for data warehousing, the VM is optimised for data warehousing
* Can small DW be looked at as image, then just copied as an on-prem design?

### Endpoints

* Remote Desktop, Powershell, SSMS

### Virtual Networks

* Can refer to on premise and azure VMs in this 
* Can look at all the VMs in the virtual network 

### Support SQL Server and OS

* Many SQL Server versions supported
* Many windows versions supported
* Almost 100% Compatibility with on premise
* You manage SQL server (Security, backups, HA, DR, etc)

### Scenarios of Use

* Dev and test new stuff in Azure VMs 
* Lift and shift - can just move databses to VM in Azure
* Move without changes, or when needed (high utilize), or how needed (elasticity)
* Hybrid - some on prem, some in cloud. 
* Hybrid e.g. AD on prem, SQL server in Azure, app on premise, SQL server in Azure
* Hybrid e.g. Replicas in cloud, disaster recovery

### Deployment

* **Use image gallery**
* Database Engine, IS, RS, AS
* Image refreshed monthly - hotfixes on windows and SQL 
* **Can bring own image**
* Upload VHD to Azure and use from there
* **Use deployment wizard**
* Can move database from on premises to VM in azure

### Always On

* Primary, secondary, witness
* You can configure high availablity set between VMs in Azure
* Always On High availability can be seen in SSMS down bottom by management folders etc

### Best Practices 

* **Deployment Best Practices**
* Configure a SQL HA technology (AlwaysOn / Database Mirroring)
* Put replicas in same - affinity group (Cluster), availability set (Different racks and upgrade domains) and VNet( Maintain VM IPs)
* Use secondary replicas to offload read/backups
* You can load balance reads across the secondary replicas! 
* Can use secondary for auto failover for OLTP, listener always points at primary
* Can then have multiple secondary with azure load balancer readable for reporting applications

* **Connectivity Best practices**
* Remove unused endpoints on VMs
* Use endpoint ACL'ing to control connections
* Dont disable firewall
* If clients are in Azure, host them in same VNET (Virtual Network) as SQL Server
* If windows auth is needed: configure domain controller, configure VPN tunnel from On premise and use on premise domain controller
* If not use SQL authentication

* **Security Best Practices**
* Windows update on by default for image gallery
* Turn on Microsoft Updates for critical SQL server updates
* Avoid "Administrator" account (disallowed from Portal)
* Use strong passwords
* Local VM administrator is SQL sysadmin, change this if company policy
* Enable database connection encryption

* **Performance Best Practices**
* If database fits in 1TB put in single data drive, not on OS drive (C) and not on temp drive (D)
* If more than 1TB, stipe data files across multiple data drives
* If hitting IOPS limit (500 p/disk), stripe Data files across multiple data drives
* Leave default cache settings (disabled) for data disks
* Use DB compression
* Use windows instant file initialisation (to reduce backup times)
* Expect higher IO disk latencies than on premises






















