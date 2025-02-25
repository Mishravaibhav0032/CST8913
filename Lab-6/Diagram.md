
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

