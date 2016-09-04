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

## SQL Database Fundamentals

* PaaS (Platform as a Service)
* Server not a machine in Azure, it's a TDS proxy endpoint
* SSL TDS encryption [Tabular Data Stream](https://en.wikipedia.org/wiki/Tabular_Data_Stream)
* Load Balanced
* SQL Azure Fabric - Automated Failover, Replication and Load Balancing
* As long as can talk TDS, stuff can access Azure
* Even security & patches is managed by Microsoft

### How it works

* Architecture - Client Layer, Services Layer, Platform Layer, Infrastructure Layer
* Failover in seconds, SLA to guarantee up time 

### Server Provisioning 

* **Server Defined** 
* Service logically groups dbs
* Connect via xxx.database.windows.net
* Contains master at start
* No windows AD logins only SQL (which you setup below)
* **Interactive** 
* Azure portal
* Create DB server
* Admin credentials
* Firewall rules 
* **Automate** 
* Powershell

### Firewall 

* No IP allowed by default
* Rules can be at db and or server level
* All over SSL so very robust encryption 
* Still able to do own security on databases etc 

### Creating a SQL Database

* Create logical server
* Create database and add to server
* Size of DB doesnt include transaction log
* DB size restricted for HA
* You can chunk up databases to handle this
* Only billed for size of database is, max size is just a cap
* Choose collation and assign to available server 
* Can also choose location of database
* Add local IP address to firewall rule of server 
* 

### Management Tooling

* Azure Management Portal
* SQL Database Management Portal - database design
* SSMS 
* REST API & Powershell - deployment, automate management, lifecycle management, continuous build/integration
* 3rd Party - TDS compatible, visual studio, RedGate, ERWin

### Security

* Server level security as on premises
* Database level security as on premises

### Application Connectivity

* TDS supported
* SSL is required
* Use firewalls rules to connect outside Microsoft data center
* In the portal you can get all the connection strings for the database in different types (ODBC, ADO etc)

### Monitoring

* Query plans, extended events, DMVs, Event Table
* No profiler - use DMVs
* No SQL profiler 
* sys_partitions
* dm_exec_sessions

### Backup 
* No point in time. Video might be out of date? CREATE DATABASE... AS COPY OF
* Export copy as BACPAC to Azure Blob Storage 

## Migration and Maintenance

### Missing Stuff 

* **Easier to Fix**
* IS - can use IaaS
* RS
* AS
* SQL Agent 

* **Harder to Fix**
* Cross DB Trans (so IaaS)
* SMO (SQL Management Objects_
* Som system objects
* Full Text Indexing
* Transparent Data Encryption
* Master Data Services
* Data Auditing and CDC
* SQL Agent 

### Non-Supported DDL

* XML Schema on XML COlumns
* CLR
* Tables without clustered indesx or PK
* Filestream
* Google what is missing 

### Non-Supported DML

* BULK INSERT
* OPENROWSET, OPENQUERY, OPENXML
* EXECUTE AS LOGIN
* Several DBCC commands
* Google what is missing

### Other Gremlins

* Limits on user names (E.g. sa)
* USE is not used supported
* Must specify db name in connection string
* ALTER INDEX REORGANIZE (have to REBUILD, can't do REORGANIZE)
* Best to use latest versionf of stuff (e.g. .Net) to move to Azure

### Migration Wizard

* Open source [Migration Wizard](https://sqlazuremw.codeplex.com/) on codeplex
* Tool will analyse database 
* Gets schema up to date and resolves errors
* Script database that is created 
* SSMS has deploy database to SQL Azure option based on this 
* dacpac (schema only) and bacpac (data and schema) are compatibe to upload to Azure

### Index Maintenance

* Only maintenance job left is use SQL DB PaaS
* No tasks for DBAs apart from this!
* REBUILD only 
* Performance tuning still required to be done by you 
* can still look at sys.dm_db_index_physical_stats 
* Do usual stuff and look for over certain % etc (Ola Hallengren!)
* Windows Azure Scheduler - does this exist? Can use instead of Agent

### Scripted Backup 

* Says no point in time support - think there is now
* CREATE... COPY OF -> EXPORT TO BLOB. Basically copying to other Azure instances. 
* For import export each Azure data centre has its own endpoint definition 

## Windows Azure SQL Database Premium SKU

* This is a shared service - multi tenant mode
* You're sharing resources 
* Noisy neighbour - they do IO on your stuff can affect you
* Throttling - tactic to ensure doesnt completely wreck your shared resources
* Your database can have times its fast and slow depending on others
* Premium Azure SQL Database  - dedicated resources, CPU, IO, Memory, pay more but avoid noisy neighbour
* Have some of biggest internnt pipes in world so latency shouldnt be an issue

### Scale UP vs Scale Out 

* **Scale Out** 
* Multiple databases and route to right data via distribution key
* Spreading load across lots of databases means higher throughput 
* Sharding like in PaaS easier as not managing loads of VMs as you would in IaaS 

### Performance Principles 

* Chunky not chatty - batch work, get all data at once
* Caching - minimize unneccesary reads, how fresh does web app data have to be (consider short duration caching)
* Be sensitive to IO

### Instrumenting your app

* Snapshotting DMVs
* Collecting XEvents 

### Other places get info

* SQL DB Portal - Query performance from DMV, connection activity
* Exeution plans
* Special wait stats - SE_REPL_SLOW_SECONDARY_THROTTLE (e.g. noisy neighbour issues)
* Call support - need session info to be able to call them 

### DMVs to use

* sys.dm_exec_requests - currentlly running queries
* sys.dm_exec_query_stats - aggregate query performance
* sys.dm_exec_query_plan - execution plan
* sys.dm_db_wait_stats - db levbel wait stats
* "missing index" dmos - indexes for perfomance

## Developing for SQL Database

* SDK - [Software Development Kit](https://en.wikipedia.org/wiki/Software_development_kit)

### Azure Mobile Services Against Sql Server

* **In Azure GUI...**
* New Mobile Service 
* Enter unique DNS name 
* Can use an existing Azure SQL Database
* Pick region 
* Enter login name and password 
* Fast and zero code way of creating an [API](https://en.wikipedia.org/wiki/Application_programming_interface)
* REST is open protocol so can have internal and external consumption
* You can pick a platform e.g. Windows, iOS, Android, HTML/JavaScript, Xamarin
* Can download sample app
* You can get endpoint from what they provide 
* Sample app added to the table! 
* Very easy to get started 

* **PHP**
* Create a website very easily 
* New website from gallery 
* Give URL name and region 
* All infrastrcuture is managed 
* Can open up web matrix to edit code 
* Get FQDNS Host for the database you want to connect to 
* have to add user, dbname, password etc 
* Run website straight away from what setup which retrieves data 

* **.Net**
* Visual studio console app simple stuff
* Basic Ado.Net to work with SQL Azure databases
* Uses SQLCommand, DataReader, DataAdapter etc and connection string to Azure
* Returns into console your command from SQL Azure 
* Transient faults - these can be small issues that sometimes in relation to Azure, so doesnt just break
* TransientFaultHandling - can install this for Azure SQL Databases 
* Define a retry strategy e.g. try 5 times every 1 second then increment a  time each retry
* Create retry policy based on what is a transient fault and fatal error
* Change SQLConnection object to ReliableSQLConnection, this understands transient faults 
* Cascading errors can be very bad in the cloud 
* AlwaysOn - TransientFaultHandling should be used anyway, not just for Azure 

