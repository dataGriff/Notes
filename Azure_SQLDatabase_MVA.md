## Windows Azure SQL Database (14 Feb 2014)
[Link](https://mva.microsoft.com/en-us/training-courses/windows-azure-sql-database-8280?l=eOml92Wy_3004984382)

### Introduction to Relation Data in the Windows Azure Platform
* Elasiticy - scale up and scale down, pay for what you use
* Reduces upfront cost and maintenance cost

#### NonRelational

* Blob Storage - unstructured
* Tables - NoSQL
* HDInsight - Big Data (Apache Hadoop)

#### Relational 

* SQL Server in a VM (good for existing stuff, IaaS, Full Control, like a VM)
* SQL Database (good for new stuff, PaaS, Managed by Azure)

### IaaS
* IaaS - Infrastructure as a Service 
* Only charged for when running 
* Decreases time to market 
* High availibility out of box
* Usage - Hybrid where disaster recovery is secondary VM in Azure
* Low TCO for Existing Apps - familiar, no app changes, can create template VM library
* Full SQL Server Capability - High Availbility, Full BI Function, Advanced Security
* Felxibility ands Control - VM you control, integrates with active directory 
* Managed Infrastructure - 99.95% SLA for VM 
* Can upload local VMs direct to Azure by converting 
* Azure VMs are in Hyper V 
* Can develop in SSDT and test in Azure then go to on-prem if want
* Can go from "on desktop" app e.g. Access or express. To full managed environment in Azure!
* Can be done programmaticaly via powershell or rest.api
* Lots can be done automatically - create VM, destory VM
* Can choose a VM image that azure offers, even Oracle and Linux! 
* Can choose with SQL server on etc 
* Can attach empty disk to the VM - log files, tempdb, partition tables etc
* You can take your enterprise on-prem license to cloud 

### PaaS
* PaaS - Platform as a Service
* As above IaaS with regards to benefits
* Also reduced I.T & reduced Admin overhead 
* Combine with website and mobile apps
* Extend on premises apps 
* All have to think about is database 
* Visual studio build once and deploy anywhere 
* Fully managed 
* High availibilty, powershell, SSMS 
* HA - muliti tenant environment, one primary and two online replicas 
* [Sharding?] (https://azure.microsoft.com/en-gb/documentation/articles/sql-database-elastic-scale-introduction/)
* Elasticity! e.g. ticket sales, boost service for big sales and then scale down again when goes quiet





### SQL Database Fundamentals

### Migration and Maintenance

### Windows Azure SQL Database Premium SKU

### Developing for SQL Database
