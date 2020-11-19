1. Create a Log Analytics workspace and record the Workspace ID an Key
2. Create an App Registration called O365ClientSecret and create a Key for it.  Record the App ID and Key
3. Create a Key Vault and add a secret called "O365ClientSecret" with the App Registration Key as the Value.
4. Deploy the CSVtoJSON Function App.  Record the function resource group, function app and function names.
5. Deploy SendO365AuditLogstoLOGA.json Template
6. Deploy SendO365UsageReportstoLOGA.json Template