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



















