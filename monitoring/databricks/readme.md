## Azure Databricks


Azure Databricks is a Spark-based analytics platform optimized for the Azure cloud services platform. Designed by the founders of Spark, Azure Databricks has native integration with Azure Data and AI services and enables data engineers and data scientists through an interactive notebook experience, supporting Python, R, SQL, and Scala. See this [link](https://docs.microsoft.com/en-us/azure/databricks/) for more information.

Some of the key benefits for Azure Databricks include:
* Fully managed Spark cluster on the Azure cloud
* Optimized Databricks runtime with many Spark and other libraries included for Python and R
* Collaborative workspace
* Enterprise-grade Azure security
* Native Azure service integration

In this section, areas of secuirty monitoring, auditing, performance monitoring, and capacity planning are discussed.

## Security Monitoring/Auditing

From a security monitoring and auditing perspective, Azure Databricks provides comprehensive end-to-end diagnostic logs of activities performed by Azure Databricks users, allowing your enterprise to monitor detailed Azure Databricks usage patterns:

*	DBFS
*	Clusters
*	Pools
*	Accounts
*	Jobs
*	Notebook
*	SSH
*	Workspace
*	Secrets
*	SQL Permissions

Reference here: https://docs.microsoft.com/en-us/azure/databricks/administration-guide/account-settings/azure-diagnostic-logs

Please note that Diagnostic Logs require the Azure Databricks Premium Plan. 

Log in to Azure Portal as Owner or Contributor role. Under the Databricks workspace in monitoring, click on Diagnostic settings and Turn on diagnostics / Add diagnostic setting. Once you confirm, the logs should flow through.

![image](https://docs.microsoft.com/en-us/azure/databricks/_static/images/audit-logs/azure-diagnostic-settings.png)

For example, once logging is configured:
* The user accessing Azure Databricks and the user's progression through the workspace and timelines can be monitored
* Access to secrets in secret scopes can be monitored as well

![adbaad](/monitoring/assets/images/adbaad.PNG)


## Performance Monitoring











## Capacity Monitoring

