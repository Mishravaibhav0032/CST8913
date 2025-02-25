<h1>Cloud-Native Refactoring of a Monolithic Application on Azure</h1>

Overview :-
<br></br>
Refurbish a monolithic web application that was developed years back on Windows Server 2019 as the VM within Azure to a newer cloud-native application. Minimize the cost with enhanced scalability and dependability with ease of management through use of Azure Services such as Azure App Service, Azure Functions, Azure SQL Database, and Azure Storage.


The original architecture :- <br></br>

One Windows Server 2019 virtual machine (VM) in Azure hosts the application, which is a monolithic web application.  
<br></br>
(1) The frontend : is an IIS-hosted web application that makes up the architecture.<br></br>
(2) The backend : is a single program that manages database interactions and business logic.<br></br>
(3) Database : The same virtual machine hosts SQL Server.<br></br>
(4) Static Content : Locally stored within the virtual machine.<br></br>
(5) Background Tasks : Managed by the virtual machine's scheduled tasks or Windows services.<br></br>


Challenges :-<br></br>

- Scalability : It is difficult to scale each component due to the monolithic design.<br></br>
- Resilience : There is a single point of failure because the VM is hosting the application and database.<br></br>
- Maintainability : The attached components are difficult to debug and update.<br></br>
- Cost : Operating a VM 24/7 very expensive, particularly for non-mission-critical workloads.<br></br>


Refactored Architecture :- <br></br>
The following Azure services are used to rework the application into a cloud-native architecture :- <br></br>
 (1) Frontend : Azure App Service is used for hosting.<br></br>
 (2) Database : Azure SQL Database was used.<br></br>
 (3) Azure Functions were used to replace the background tasks.<br></br>
 (4) Logs and static content are kept in Azure Blob Storage.<br></br>
 (5) Azure AD was used to implement authorization and authentication.<br></br>


Diagram of Refactored Architecture :- <br></br>

+-------------------+       +-------------------+       +-------------------+
|   User Browser    |       |   Azure AD        |       |   Azure Monitor   |
|   (Frontend)      |       |   (Authentication)|       |   (Monitoring)    |
+--------+----------+       +--------+----------+       +--------+----------+
         |                           |                           |
         |                           |                           |
         v                           v                           v
+-------------------+       +-------------------+       +-------------------+
|   Azure App       |       |   Azure Functions |       |   Azure SQL       |
|   Service         |       |   (Background     |       |   Database        |
|   (Frontend/API)  |       |   Tasks)          |       |   (Database)      |
+--------+----------+       +--------+----------+       +--------+----------+
         |                           |                           |
         |                           |                           |
         v                           v                           v
+-------------------+       +-------------------+       +-------------------+
|   Azure Blob      |       |   Azure Blob      |       |   Application     |
|   Storage         |       |   Storage         |       |   Insights        |
|   (Static Content)|       |   (Logs)          |       |   (Telemetry)     |
+-------------------+       +-------------------+       +-------------------+

Refactoring Technique :- <br></br>

 1. Dismantle the Application Monolith<br></br>
  -Frontend : The user interface layer was divided and put into Azure App Service.<br></br>
  -Backend : The business logic was broken down into microservices, each of which was hosted on Azure Functions or Azure App Service.<br></br>
  -Database : To improve scalability and managed services, the database was moved to Azure SQL Database.<br></br>

 2. Decide on Azure Services<br></br>
 The frontend and backend APIs are hosted by Azure App Service.<br></br>
 - Azure SQL Database: Takes the place of SQL Server hosted in virtual machines.<br></br>
 - Azure Functions: Manages event-driven processing and background jobs.<br></br>
 - Azure Blob Storage: Holds logs and static data, such as papers and photos.<br></br>
 - Azure AD is in charge of permission and authentication.<br></br>

 3. Authentication and Authorization : Role-based access control (RBAC) and secure authentication are made possible by the integration of Azure AD.<br></br>


Steps for Implementation :-<br></br>

First, an Azure App Service plan was created and the frontend was deployed to Azure App Service.<br></br>

 - Azure App Service was used to deploy the front-end application.<br></br>
 - Set up SSL certificates and custom domains.<br></br>

2. Convert the database to Azure SQL.<br></br>
 - The database was exported from the virtual machine-hosted SQL Server.<br></br>
 - Azure SQL Database was used to import the database.<br></br>
 - The application's connection strings have been updated to point to the new database.<br></br>

3. Convert Tasks in the Background to Azure Functions.<br></br>
 - Background tasks in the monolithic application were identified.<br></br>
 - Azure Functions was used to rewrite the jobs.<br></br>
 - Configured triggers for the functions, such as timers and queues.<br></br>

4. Use Azure Blob Storage to store static content and logs.<br></br>
 - An Azure Storage account was created.<br></br>
 - In Azure Blob Storage, static content was uploaded.<br></br>
 - Set up the program to use Blob Storage for log storage.<br></br>

5. Put Auto-Scaling into Practice. <br></br> 
 - Azure App Service auto-scaling was set up according to CPU and memory use.<br></br>
 - Configure Azure Functions scaling rules.<br></br>


6. Set up Monitoring and Logging.<br></br>
 - Azure Monitor and Application Insights have been enabled for the application.<br></br>
 - Configure alerts for important indicators, such as unsuccessful requests and excessive CPU utilization.<br></br>


Testing and Optimization :-<br></br>

Testing Performance :<br></br>

 - Azure Load Testing was used to do load testing.<br></br>
 - The application's ability to scale automatically under high demand was confirmed.<br></br>

Reliability Testing :<br></br>

 - To guarantee resilience, failures were simulated, such as database outages.<br></br>
 - Azure Functions retry logic was confirmed to function as intended.<br></br>

Optimization of Costs :<br></br>

 - Examined Azure Cost Management to find areas where money may be saved.<br></br>
 - Moved to Azure SQL Database reserved instances.<br></br>

Lessons Acquired :<br></br>

 - Decoupling Components : Scalability and maintainability were enhanced by dismantling the monolithic application.<br></br>
 - Managed Services : Operational overhead was decreased by utilizing Azure Functions and Azure SQL Database.<br></br>

Savings on costs : <br></br>

 - Costs were greatly decreased by switching to a pay-as-you-go basis using Azure services.<br></br>

Readings :<br></br>

 - Database Migration : It was difficult to guarantee data consistency throughout the migration.<br></br>
 - Reworking Legacy Code : The monolithic program needed extensive reworking because several of its components were closely connected.<br></br>
 - Learning Curve : It required some time to become acquainted with Azure services and their setups.<br></br>

An added benefit is Infrastructure as Code (IaC) :-<br></br>

 - Terraform was used to implement IaC and automate the refactored application's deployment.<br></br>
 - Terraform scripts can be found in this repository's infrastructure subdirectory.<br></br>

References :- <br></br>
<br></br>(1) SyntaxC. (n.d.). Azure App Service documentation - Azure App Service. Microsoft Learn. https://learn.microsoft.com/en-us/azure/app-service/
<br></br>(2) Ggailey. (n.d.). Azure Functions documentation. Microsoft Learn. https://learn.microsoft.com/en-us/azure/azure-functions/
<br></br>(3) MashaMSFT. (n.d.). Azure SQL Database documentation - Azure SQL. Microsoft Learn. https://learn.microsoft.com/en-us/azure/azure-sql/database/?view=azuresql
<br></br>(4) Bwren. (n.d.). Azure Monitor documentation - Azure Monitor. Microsoft Learn. https://learn.microsoft.com/en-us/azure/azure-monitor/
