<h1>Cloud-Native Refactoring of a Monolithic Application on Azure</h1>

Overview :-

Refurbish a monolithic web application that was developed years back on Windows Server 2019 as the VM within Azure to a newer cloud-native application. Minimize the cost with enhanced scalability and dependability with ease of management through use of Azure Services such as Azure App Service, Azure Functions, Azure SQL Database, and Azure Storage.



The original architecture :-
One Windows Server 2019 virtual machine (VM) in Azure hosts the application, which is a monolithic web application.  

(1) The frontend : is an IIS-hosted web application that makes up the architecture.
(2) The backend : is a single program that manages database interactions and business logic.
(3) Database : The same virtual machine hosts SQL Server.
(4) Static Content : Locally stored within the virtual machine.
(5) Background Tasks : Managed by the virtual machine's scheduled tasks or Windows services.


Challenges :-
- Scalability : It is difficult to scale each component due to the monolithic design.
- Resilience : There is a single point of failure because the VM is hosting the application and database.
- Maintainability : The attached components are difficult to debug and update.
- Cost : Operating a VM 24/7 very expensive, particularly for non-mission-critical workloads.



Refactored Architecture :-
The following Azure services are used to rework the application into a cloud-native architecture:
 (1) Frontend : Azure App Service is used for hosting.
 (2) Database : Azure SQL Database was used.
 (3) Azure Functions were used to replace the background tasks.
 (4) Logs and static content are kept in Azure Blob Storage.
 (5) Azure AD was used to implement authorization and authentication.


Diagram of Refactored Architecture :-


Refactoring Technique

 1. Dismantle the Application Monolith
  -Frontend : The user interface layer was divided and put into Azure App Service.
  -Backend : The business logic was broken down into microservices, each of which was hosted on Azure Functions or Azure App Service.
  -Database : To improve scalability and managed services, the database was moved to Azure SQL Database.

 2. Decide on Azure Services
 The frontend and backend APIs are hosted by Azure App Service.
 - Azure SQL Database: Takes the place of SQL Server hosted in virtual machines.
 - Azure Functions: Manages event-driven processing and background jobs.
 - Azure Blob Storage: Holds logs and static data, such as papers and photos.
 - Azure AD is in charge of permission and authentication.

 3. Authentication and Authorization : Role-based access control (RBAC) and secure authentication are made possible by the integration of Azure AD.


Steps for Implementation :-

First, an Azure App Service plan was created and the frontend was deployed to Azure App Service.

 - Azure App Service was used to deploy the front-end application.
 - Set up SSL certificates and custom domains.

2. Convert the database to Azure SQL.
 - The database was exported from the virtual machine-hosted SQL Server.
 - Azure SQL Database was used to import the database.
 - The application's connection strings have been updated to point to the new database.

3. Convert Tasks in the Background to Azure Functions
 - Background tasks in the monolithic application were identified.
 - Azure Functions was used to rewrite the jobs.
 - Configured triggers for the functions, such as timers and queues.

4. Use Azure Blob Storage to store static content and logs.
 - An Azure Storage account was created.
 - In Azure Blob Storage, static content was uploaded.
 - Set up the program to use Blob Storage for log storage.

5. Put Auto-Scaling into Practice: 
 - Azure App Service auto-scaling was set up according to CPU and memory use.
 - Configure Azure Functions scaling rules.


6. Set up Monitoring and Logging
 - Azure Monitor and Application Insights have been enabled for the application.
 - Configure alerts for important indicators, such as unsuccessful requests and excessive CPU utilization.


Testing and Optimization :-

Testing Performance :

 - Azure Load Testing was used to do load testing.
 - The application's ability to scale automatically under high demand was confirmed.

Reliability Testing :

 - To guarantee resilience, failures were simulated, such as database outages.
 - Azure Functions retry logic was confirmed to function as intended.

Optimization of Costs :

 - Examined Azure Cost Management to find areas where money may be saved.
 - Moved to Azure SQL Database reserved instances.

Lessons Acquired :

 - Decoupling Components : Scalability and maintainability were enhanced by dismantling the monolithic application.
 - Managed Services : Operational overhead was decreased by utilizing Azure Functions and Azure SQL Database.

Savings on costs : 

 - Costs were greatly decreased by switching to a pay-as-you-go basis using Azure services.

Readings :

 - Database Migration : It was difficult to guarantee data consistency throughout the migration.
 - Reworking Legacy Code : The monolithic program needed extensive reworking because several of its components were closely connected.
 - Learning Curve : It required some time to become acquainted with Azure services and their setups.

An added benefit is Infrastructure as Code (IaC) :-

 - Terraform was used to implement IaC and automate the refactored application's deployment.
 - Terraform scripts can be found in this repository's infrastructure subdirectory.
