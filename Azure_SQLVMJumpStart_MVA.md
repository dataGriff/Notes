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
* Just look for performance whitepaper

## SQL Server on Azure VM Performance

### Key Performance Considerations

* Analyse performance impact, is it a problem with SQL App? Or how I configured IaaS?
* KPIs - throughput, response time (latency)
* Dimension - workload (OLTP, DW, Backup), IO size and pattern

### Windows Azure VM Sizes

* Varies a lot but still limited
* CPU cores, Memory, OS disk space, temp disk space, max no of data disks (1TB each), Max IOPS (inputs outputs)

### Windows Azure IO Subsystem

* Disks implemented as a shared multi-tennant service
* Built in triple redundancy, optional geo-redudnancy
* Performance less predictable than on-prem

### VM Disk Types and Configurtions

* OS disk (persistent) - 127GB optimised for OS e.g. bootup
* Data disk (persist) - VHD attach to VM to store app data, up to 1TB in szie and 16 disks for big VMs
* Temporary local disk (non-persisted) - Volume D - transient data, cleaned up in VM fail or recycle, physical disks across other VMs on same physical machine, not receommended for user or system db files. Dont store data here. 

### VM Disk Caching and Configurations

* Caches VM data inside physical host
* 2 tier cache - RAM cache, local hard disk
* **Disk type caching**
* OS disk - supported, default read write
* Data disk - supported (up to 4), supported (up to 4)
* Temp Disk - Implemented using local attached storage 

### Disk caching Best Practices for SQL Server

* **OS Disk**
* Read wrote defai;t redices ready latency for IO intensive workloads with smaller DBs (<=10GB)
* Working set can fit in disk cache or memory, reducing blob storage IO
* **Data disks**
* Cache setting depends on the IO pattern and workload intensity
* Use default of none for higher rate of random IOs (e.g. OLTP) & higher throuput - byp[asses physical hosts disks, maximising IO rate
* Consider enabling read cache for latency sensitive read heavy workloads - lower latency then for reading

### Single Disk Configuration

* Recommended for <1TB stirage
* Accetpable performance (<500 IOPS)
* Minimal complexity, simpler recovery

### Multiple Disk Configuration

* **Recommended for**
* > 1TB DB files 
* Higher IOPS / bandwidth requirements
* **2 Config Choices**
* Option 1: Use filegroups with multiple db files, place each db file on seperate data disk - **showed best performance in testing**, does not help scaling transaction log
* Option 2: Create OS volumne on top of multiple data disks - striped

### Tool for performance

* [SQLIO](https://www.microsoft.com/en-gb/download/details.aspx?id=20163)

### VM Network Best Practices

* Network latency can be higher compared to on prem
*   Virtualization msecurity, load balancing, proximity
*   Reducing network round trips can have more impact compare to on-prem
* Consolidate chartty application layers on the same machine
* Host VMs in the same Virtual Network / Cloud Service

### Should tempdb go on D drive? 

* **No**
* Why? 
* Preditable performance - D drive shares with other VMs on host so performance to variable
* Configuration overhead - will have to recreate TEMPDB in D if VM goes down, SQL Service account requires admin priveleges. If stored in separate folder this needs to be created at startup

### Reduce IO with Data Compression

* IO intensive workloads: fewer pages so reduced IO. Even more important in Azure 

### Reduce IO with Instant File Initialisation

* Not default in Azure VM Images
* Reduces IO for - creatinfg DB, restore db, adding files to DB, extending file size, autogrow
* Add SQL Service account to **perform volume maintenance tasks** security policy
* Restart SQL Server
* Note: doesnt help trnasaction log

### What else to consider for data disk performance? 

* Disk warm-up
* [NTFS](https://en.wikipedia.org/wiki/NTFS) allocation unit size
* Single vs. multiple storage accounts with a single VM
*   **DO NOT SPREAD DATA FILES OF A SINGLE DATABSE INTO MULTIPLE STORAGE ACCOUNTS**
*     Data in different blobs not written at the same time
*     BLOBs that make up the stripe set could be out of sync
*   Instead:
*     Spread the data files across multipke disjs to achieve higher IOPS/bandwithd
*   Note: a storage account has limit fo 20K tps 

### Performance Monitoring

* Goal: Determine IO capacity if VM configurations, Establish baseline
* Tools [SQLIO](https://www.microsoft.com/en-gb/download/details.aspx?id=20163) - Disk subssystem benchmark tool, performance metrics, DMvs. 

* **Key Tools**
* VM dashboard
* Storage Analytics
* SQL perf counters

### High level troubleshooting steps

* Define KPIs to monitor resourece utilisation
* Monitor KPIs to track utilisation over time
* Exmaine trends and patterns as workload increases
* Mionitor DMVs to understand resource contention waits
* Monitor spinlock and backoff events
* Gogle troubleshooting common VM issues and find KPIs to monitor

### Summary

* Read whitepaprt
* PLan and test for IO perf variability
* Identify optimal VM size
* Optimse for reduce IO and network round trips
* Use Filegroups and multiple daty disks for large DBs
* Identify your KPIs to montior
* Revisit optimisation decisions as workload changes

* [Link to best practices documentation](https://azure.microsoft.com/en-gb/documentation/articles/virtual-machines-windows-sql-performance/)
* See white paper you download on performance guidance for SQL server in Azure VMs




























