# Azure SQL Database & Azure SQL Managed Instance

Azure SQL is a family of managed, secure, and intelligent products that use the SQL Server database engine in the Azure cloud. For this operation docs, we will discuss the monitoring for 

- **Azure SQL Database**: Support modern cloud applications on an intelligent, managed database service, that includes serverless compute.
- **Azure SQL Managed Instance**: Modernize your existing SQL Server applications at scale with an intelligent fully managed instance as a service, with almost 100% feature parity with the SQL Server database engine. Best for most migrations to the cloud.



## Security Monitoring/Auditing

| What to Monitor                                              | How to Monitor                                               | Comments                                                     |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Configuration changes                                        | Azure Monitor - Activity logs                                | Make sure to send activity logs (per subscription) to log analytics workspace then query the logs from there. For known security configuration changes like *secure transfer required* , alerts should be created for it |
| logins (Success & Failure)                                   | Azure SQL Database Audit<br />Azure SQL Managed Instance Auditing | **Azure SQL Database:** <br/> The default auditing policy includes all actions and the following set of action groups, which will audit all the queries and stored procedures executed against the database, as well as successful and failed logins:<br />BATCH_COMPLETED_GROUP SUCCESSFUL_DATABASE_AUTHENTICATION_GROUP FAILED_DATABASE_AUTHENTICATION_GROUP<br /> The audit logs can be saved to storage account, event hub or log analytics workspace. <br />*Which destination to choose?* <u>`GC specific`</u>: For internal review inside the department, a centralized log analytic workspace should be chosen. For GC-wide security inspection, Event Hub should be chosen so the central security agencies can ingest the data centrally. So both log analytics & event hub should be chosen for optimal operation. <br />**Azure SQL Managed Instance**<br /> Azure SQL Managed Instance doesn't have default audit. You need to create an audit specification. A Sample server  specification is [listed here](https://gist.github.com/mosharafMS/b2f75c2c0735f917031b127e321ab0b5)  that covers all the essential auditing<br /> Then create the audit object using TSQL <br />`CREATE SERVER AUDIT [<your_audit_name>] TO EXTERNAL_MONITOR;` Then setup the Diagnostic logs to Storage account, Event hub or Log analytics. The same recommendations for <u>`GC specific`</u> still apply. For detailed step by step, refer to [the docs](https://docs.microsoft.com/en-us/azure/azure-sql/managed-instance/auditing-configure#set-up-auditing-for-your-server-to-event-hubs-or-azure-monitor-logs)<br /> |
| Data Manipulation Language (DML) : Insert, Update, Select, Delete | Azure SQL Database Audit<br />Azure SQL Managed Instance Auditing | **Azure SQL Database:** Covered with the default auditing described above <br />**Azure SQL Managed Instance**<br /> Create individual Database audit specification as per need. Excessive auditing for DML will cause performance impact so no auditing beyond the default server audit mentioned above unless there's a business need for it.  For more details about database audit specification, refer to [the docs](https://docs.microsoft.com/en-us/sql/t-sql/statements/create-database-audit-specification-transact-sql?view=sql-server-ver15) |
| Database schema changes                                      | Azure SQL Database Audit<br />Azure SQL Managed Instance Auditing | **Azure SQL Database:** For any extra audit actions group or audit actions, you can setup them using PowerShell, REST APIs or ARM templates<br />**Azure SQL Managed Instance**<br /> Create individual audit specifications as per need. For more details about database audit specification, refer to [the docs](https://docs.microsoft.com/en-us/sql/t-sql/statements/create-database-audit-specification-transact-sql?view=sql-server-ver15) |
| One-stop central security monitoring                         | Azure Security Center                                        | Azure Security Center assess the overall security of many Azure resources including SQL Servers and show recommendations ![Azure Security Center](/monitoring/assets/images/security-center-sql-server.png) |
| Audit Access to sensitive data                               | Azure SQL Data Discovery & Classification                    | Once classify fields in the database(s) the audit will track any access to them with special mark<br />![Azure SQL Data Classification Auditing](/monitoring/assets/images/11_data_classification_audit_log.png). For more details refer to [the docs](https://docs.microsoft.com/en-us/azure/azure-sql/database/data-discovery-and-classification-overview) |







## Performance Monitoring

| What to Monitor                                              | How to Monitor                                               | Comments                                                     |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| CPU percentage / DTU percentage / memory percentage and IO percentage | Azure Monitor Metrics for alerts and Azure SQL analytics for dashboard | Basic Metrics are different from a resource to another. For example, in Azure SQL database DTU percentage, DTU used, DTU limit, CPU percentage, physical data read percentage, log write percentage, Successful/Failed/Blocked by firewall connections, sessions percentage, workers percentage, storage, storage percentage, XTP storage percentage, and deadlocks <br /> Adding alerts for excessive CPU usage (>95 ) for 5 minutes or more helps identify any bad code or unexpected high workload<br />![Azure monitor metrics](/monitoring/assets/images/sqldb-metrics-cpu.png) |
| SQL-specific performance counters                            | DMV                                                          | `sys.dm_db_resource_stats` and `sys.dm_os_performance_counters`  can be used to identify more detailed resource pressure issues (cpu, memory & IO) |
| Blocking & Deadlocks                                         | Azure monitor for SQL Database and Extended events for SQL Managed Instance | Azure Diagnostics for SQL Database exposes the blocking data as described in this [schema](https://docs.microsoft.com/en-us/azure/azure-sql/database/metrics-diagnostic-telemetry-logging-streaming-export-configure?tabs=azure-portal#blockings-dataset) . <br /> For Azure Managed Instance, You can use [Extended Events](https://docs.microsoft.com/en-us/azure/azure-sql/database/xevent-db-diff-from-svr?view=sql-server-ver15) |
| Query performance & performance regression                   |                                                              | SQL [Query Store](https://docs.microsoft.com/en-us/sql/relational-databases/performance/monitoring-performance-by-using-the-query-store?view=sql-server-ver15) is always enabled on both SQL Database & SQL Managed Instance |







## Capacity Monitoring



| What to Monitor          | How to Monitor | Comments |
| ------------------------ | -------------- | -------- |
| Billing unit consumption |                |          |
| Tempdb data & log size   |                |          |
| Database data & log size |                |          |

