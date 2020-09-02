# Overview
This solution utilizes a Logic App workflow to query Office and Azure AD report data from the Graph API and ingest it into a Log Analytics Workspace for retention and reporting.  Report data from the Graph API comes back as CSV format and must be converted to JSON before ingestion into the LAW. A CSVtoJSON Function App is used to perform this conversion.

# How to Deploy Solution
## Install and Configure Visual Studio Code (VSCode) and Prereqs
It is recommended that the CSVtoJSON Function App be deployed to Azure using Visual Studio Code (VSCode) if unfamiliar with the Function App Deployment process.  You will need to install VSCode from https://code.visualstudio.com/Download.  Once installed the following VSCode extensions are needed:
* Azure Functions
* Azure Account
* C#

In addition the .NET Core 3.1 SDK is required to compile the Function App code. This can be be downloaded from https://dotnet.microsoft.com/download/dotnet-core/3.1.

## Compile and Deploy Function App
1. Clone this repo to your local machine using VSCode
2. Compile and Execute on Local .NET Function Instance (for local testing)
3. Deploy to Azure Function App using VSCode
4. Deploy Logic App ARM Template

# Graph API Sample Calls and References
* Exchange > Email Activity 
  * Get details about email activity users have performed
    * Sample Call: https://graph.microsoft.com/v1.0/reports/getEmailActivityUserDetail(period='D7')
    * https://docs.microsoft.com/en-us/graph/api/reportroot-getemailactivityuserdetail?view=graph-rest-1.0
  * Enables you to understand the trends of email activity (like how many were sent, read, and received) in your organization.
    * Sample Call: https://graph.microsoft.com/v1.0/reports/getEmailActivityCounts(period='D7')
    * https://docs.microsoft.com/en-us/graph/api/reportroot-getemailactivitycounts?view=graph-rest-1.0
  * Enables you to understand trends on the number of unique users who are performing email activities like send, read, and receive.
    * Sample Call: https://graph.microsoft.com/v1.0/reports/getEmailActivityUserCounts(period='D7')
    * https://docs.microsoft.com/en-us/graph/api/reportroot-getemailactivityusercounts?view=graph-rest-1.0
* Microsoft Teams > User Activity
  * Get details about Microsoft Teams user activity by user
    * Sample Call: https://graph.microsoft.com/v1.0/reports/getTeamsUserActivityUserDetail(period='D7')
    * Reference: https://docs.microsoft.com/en-us/graph/api/reportroot-getteamsuseractivityuserdetail?view=graph-rest-1.0
  * Get the number of Microsoft Teams activities by activity type. The activity types are team chat messages, private chat messages, calls, and meetings
    * Sample Call: https://graph.microsoft.com/v1.0/reports/getTeamsUserActivityCounts(period='D7')
    * https://docs.microsoft.com/en-us/graph/api/reportroot-getteamsuseractivitycounts?view=graph-rest-1.0
  * Get the number of Microsoft Teams users by activity type. The activity types are number of teams chat messages, private chat messages, calls, or meetings - 
    * Sample Call: https://graph.microsoft.com/v1.0/reports/getTeamsUserActivityUserCounts(period='D7') - 
    * https://docs.microsoft.com/en-us/graph/api/reportroot-getteamsuseractivityusercounts?view=graph-rest-1.0
* Office 365 > Active Users
  * Get details about Microsoft 365 active users
    * Sample Call: https://graph.microsoft.com/v1.0/reports/getOffice365ActiveUserDetail(period='D7')
  * Get the count of daily active users in the reporting period by product - 
    * Sample Call: https://graph.microsoft.com/v1.0/reports/getOffice365ActiveUserCounts(period='D7')
  * Get the count of users by activity type and service - 
    * Sample Call: https://graph.microsoft.com/v1.0/reports/getOffice365ServicesUserCounts(period='D7')
* One Drive > Activity
  * Get details about OneDrive activity by user - 
    * Sample Call: https://graph.microsoft.com/v1.0/reports/getOneDriveActivityUserDetail(period='D7')
  * Get the trend in the number of active OneDrive users - 
    * Sample Call: https://graph.microsoft.com/v1.0/reports/getOneDriveActivityUserCounts(period='D7')
  * Get the number of unique, licensed users that performed file interactions against any OneDrive account - 
    * Sample Call: https://graph.microsoft.com/v1.0/reports/getOneDriveActivityFileCounts(period='D7')
* Sharepoint > Activity
  * Get details about SharePoint activity by user
    * Sample Call: https://graph.microsoft.com/v1.0/reports/getSharePointActivityUserDetail(period='D7')
  * Get the number of unique, licensed users who interacted with files stored on SharePoint sites
    * Sample Call: https://graph.microsoft.com/v1.0/reports/getSharePointActivityFileCounts(period='D7')
  * Get the trend in the number of active users. A user is considered active if he or she has executed a file activity (save, sync, modify, or share) or visited a page within the specified time period
    * Sample Call: https://graph.microsoft.com/v1.0/reports/getSharePointActivityUserCounts(period='D7')
  * Get the number of unique pages visited by users
    * Sample Call: https://graph.microsoft.com/v1.0/reports/getSharePointActivityPages(period='D7')
* Azure Active Directory Logs > Sign-ins by Date
  * Get the list of audit logs generated by Azure Active Directory. This includes audit logs generated by various services within Azure AD, including user, app, device and group Management, privileged identity management (PIM), access reviews, terms of use, identity protection, password management (self-service and admin password resets), and self- service group management, and so on.
    * Sample Call: https://graph.microsoft.com/v1.0/auditLogs/directoryAudits
  * Retrieve the Azure AD user sign-ins for your tenant. Sign-ins that are interactive in nature (where a username/password is passed as part of auth token) and successful federated sign-ins are currently included in the sign-in logs
    * Sample Call: https://graph.microsoft.com/v1.0/auditLogs/signIns