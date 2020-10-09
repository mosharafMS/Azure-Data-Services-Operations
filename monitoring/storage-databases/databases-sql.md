Configuration changes  Azure Monitor - Activity logs  Make sure to send activity logs (per subscription) to log analytics workspace then query the logs from there. For known security configuration changes like *secure transfer required* , alerts should be created for itAzure SQL

Azure SQL is a family of managed, secure, and intelligent products that use the SQL Server database engine in the Azure cloud. For this operation docs, we will discuss the monitorintg for 

- **Azure SQL Database**: Support modern cloud applications on an intelligent, managed database service, that includes serverless compute.
- **Azure SQL Managed Instance**: Modernize your existing SQL Server applications at scale with an intelligent fully managed instance as a service, with almost 100% feature parity with the SQL Server database engine. Best for most migrations to the cloud.



## Security Monitoring/Auditing

| What to Monitor            | How to Monitor                                               | Comments                                                     |
| -------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Configuration changes      | Azure Monitor - Activity logs                                | Make sure to send activity logs (per subscription) to log analytics workspace then query the logs from there. For known security configuration changes like *secure transfer required* , alerts should be created for it |
| logins (Success & Failure) | Azure SQL Database Audit<br />Azure SQL Managed Instance Auditing | **Azure SQL Database:** <br/> The default auditing policy includes all actions and the following set of action groups, which will audit all the queries and stored procedures executed against the database, as well as successful and failed logins:<br />BATCH_COMPLETED_GROUP SUCCESSFUL_DATABASE_AUTHENTICATION_GROUP FAILED_DATABASE_AUTHENTICATION_GROUP<br /> The audit logs can be saved to storage account, event hub or log analytics workspace. <br />*Which destination to choose?* <u>`GC specific`</u>: For internal review inside the department, a centralized log analytic workspace should be chosen. For GC-wide security inspection, Event Hub should be chosen so the central security agencies can ingest the data centrally. So both log analytics & event hub should be chosen for optimal operation. <br />**Azure SQL Managed Instance**<br /> Azure SQL Managed Instance doesn't have default audit. You need to create an audit specification. A Sample server  specification is listed here https://gist.github.com/mosharafMS/b2f75c2c0735f917031b127e321ab0b5 |
|                            |                                                              |                                                              |
|                            |                                                              |                                                              |
|                            |                                                              |                                                              |
|                            |                                                              |                                                              |







## Performance Monitoring









## Capacity Monitoring





