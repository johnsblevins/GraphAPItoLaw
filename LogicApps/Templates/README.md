1. Create a Log Analytics Workspace and record the Workspace ID and Key.
2. Create an App Registration with the following API Access to O365 Management and Graph APIs.
   1. Microsoft Graph
      1. Reports.Read.All
      2. Application
      3. Read all usage reports
      4. Yes Granted for Self
    1. Office 365 Management APIs
       1. ActivityFeed.Read
       2. Application
       3. Read activity data for your organization Yes
       4. Granted for Self
3. Create a Key Vault and add a secret called "O365ClientSecret" with the App Registration Key as the Value.
4. Deploy the CSVtoJSON Function App.  Record the function resource group, function app and function names.
5. Deploy SendO365AuditLogstoLOGA.json Template
6. Deploy SendO365UsageReportstoLOGA.json Template