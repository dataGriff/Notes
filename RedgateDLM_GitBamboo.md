
Steve Jones Presents

# Database Lifecycle Management using Git and Bamboo

* Out of pace with application
* Little or no traceability
* Unable to rollback
* Databases become bottlenects
* Release frequency less and more risky

## Benefits of DLM & Continuous Delivery

* Repeatbility and greater predictablity over releases
* Eliminate repitition of manual tasks
* Smaller units of change so faster
* Greater reliability as automated tests

## The Bottom Line

* IT performance correlates with version control and continuous delivery
* Agile more deployment

## Development & Operations

* Source Control > Continuous Integration > release management (testing, qa, staging) > Production > Monitoring & Backup
* Redgate plugs into - visual studio, ssms, git, jenkins, team city, bamboo, octopus 

## Demo 

### SQL Source Control 

* Redgate SQL Source control repo  - no changes found in beginning
* Amend something (SQL Prompt is great blah blah) e.g. Alter procedure 
* when something amended shows blue + - needs to be checked into source control then
* You can commit in commit tab of SQL source control - shows what is different at the bottom 
* Link static data - this is reference data bit where want to put data into source control e.g country or something 
* SQL Source control will also then have data that has changed requiting commits into source control
* can push to remote repo as well - master branch 
* git is the trend... 
* you can right-click the database and look for a commit history 
* you can pull down from remote repo as well
* you can "lock this object" to stop changes by anyone, lock tab will show who's locked it, you can unlock too
* No source control for BI or at server level stuff?? No SQL agent jobs either? 
* Can choose what objects want in source control 

### Build with bamboo

* Redgate DLM automatiom build
* Builds a nuget package 
* Can use SQL LocalDB or SQL Server
* Run a test step - uses Redgate DLM Automation tool
* SQLCOP tests can be used - enforce standards, performance checks, in SQLCOP schema. e.g. check if procedures start with sp which is a bad practice
* tSQLt tests can be used and in tSQLt schema, unit tests - create fakes tables - ensures data added matches what is expected in return
* can run tests locally with SQL test redgate plugin 
* Database build and test
* can see logs of all the tests etc you did in bamboo 

### Deploy with Bamboo
* Integration environment gets auto updated after succesful build
* Deploy release verstion to test environment...
* Deployment steps setup are... Powershell commmand list nuget packages for changes - see in HTML report. Deploy. 
* Integration > Testing > Acceptance > Production environments
* Acceptance - refresh from production, comparison between production and acceptance. 
* Acceptance then goes to production
* Drift detection built in - makes sure dbs match before executes update. deploy will fail if there is drift. 
* RSS feed for deployment
* All in transaction so can rollback 
* Integrates with DLM dashboard (free tool)
* Can see states of objects before and after deployment
* Tabs coloured
* If make change to production DLM dashbaord will show database drift and where changes came from
* Can setup notifications - so if drift can be notified 
* You can filter what objects, schemas you want to deploy

## Examples of CI (Continuous Integration) tools

* TeamCity
* TFS Team Build
* Jenkins 

## Example of release management

* Octopus
* Visual Studio Release Management
* Jenkins
* Bamboo 



