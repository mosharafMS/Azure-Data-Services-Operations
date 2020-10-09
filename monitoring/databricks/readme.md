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

From a security monitoring and auditing perspective, Azure Databricks provides comprehensive end-to-end diagnostic logs of activities performed by Azure Databricks users, allowing an enterprise to monitor detailed Azure Databricks usage patterns:

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

#### How to set up

Log in to Azure Portal as Owner or Contributor role. Under the Databricks workspace in monitoring, click on Diagnostic settings and Turn on diagnostics / Add diagnostic setting. Once the user confirm, the logs should flow through.

![image](https://docs.microsoft.com/en-us/azure/databricks/_static/images/audit-logs/azure-diagnostic-settings.png)

For example, once logging is configured:
* The user accessing Azure Databricks and the user's progression through the workspace and timelines can be monitored. Here is what the logging looks like, exported from storage account:

![adbaad](/monitoring/assets/images/adbaad.PNG)
![adbnotebook](/monitoring/assets/images/adbnotebook.PNG)

* Access to secrets in secret scopes can be monitored as well

![adbsecret](/monitoring/assets/images/adbsecret.PNG)

* Jobs can be monitored as well through diagnostic logging. Some users may like to use the Databricks APIs to build pipeline job alerting. More information can be found here: https://docs.microsoft.com/en-us/azure/databricks/dev-tools/api/latest/jobs#--runs-list.

## Performance Monitoring

For performance monitoring, a good starting point is the Ganglia metrics: https://docs.microsoft.com/en-us/azure/databricks/clusters/clusters-manage#monitor-performance. 

#### Ganglia

The user can also export historical metrics from the UI as well. This is a good way to monitor notebook runs to determine if tasks require more memory or CPU. User can find metrics under the Cluster page in Azure Databricks:

![image](https://docs.microsoft.com/en-us/azure/databricks/_static/images/clusters/metrics-tab.png)
![adbmetrics](/monitoring/assets/images/adbmetrics.PNG)

#### Cluster logging

For Spark driver, worker and event logging, this is a good reference: https://docs.microsoft.com/en-us/azure/databricks/clusters/configure#cluster-log-delivery. The user can specify a custom location for the logs to be saved in. At the cluster configuration page, under Advanced Options, the Logging area can be specified:

![image](https://docs.microsoft.com/en-us/azure/databricks/_static/images/clusters/log-delivery-azure.png)

#### Application logging

For application logging, this is a more advanced topic and covered here: https://docs.microsoft.com/en-us/azure/architecture/databricks-monitoring/application-logs. This uses the Azure Databricks Monitoring Library and sends application logs and metrics to a Log Analytics workspace.









## Capacity Monitoring

For capacity planning and monitoring, there are a few topics to keep in mind below.

#### Tagging

To monitor cost and accurately attribute Azure Databricks usage to the organization’s business units and teams (for chargebacks, for example), the user can tag workspaces (resource groups), clusters, and pools. These tags propagate to detailed cost analysis reports that can be accessed in the Azure portal.

To configure cluster tags, on the cluster configuration page, click on Advanced Options and Tags:

![image](https://docs.microsoft.com/en-us/azure/databricks/_static/images/clusters/tags.png)

#### Core quotas

It is important to track of core limits for the underlying VMs of Azure Databricks clusters as exceeding quotes will prevent cluster creation, e.g. see here: https://docs.microsoft.com/en-us/azure/databricks/kb/clusters/azure-core-limit

One way to monitor is here: https://docs.microsoft.com/en-us/azure/virtual-machines/windows/quotas#check-usage

#### IP limits

In addition, if Azure Databricks is deployed through vnet injection, it is worthwhile to monitor the number of avaiable IP addresses. This information can be found under the subnet settings page:

![adbmetrics](/monitoring/assets/images/adbmetrics.PNG)

