# Azure Data Factory

Azure Data Factory is the cloud-based ETL and data integration service that allows you to create data-driven workflows for orchestrating data movement and transforming data at scale. Using Azure Data Factory, you can create and schedule data-driven workflows (called pipelines) that can ingest data from disparate data stores. You can build complex ETL processes that transform data visually with data flows or by using compute services such as Azure HDInsight Hadoop, Azure Databricks, and Azure SQL Database.



## Security Monitoring/Auditing

https://docs.microsoft.com/en-us/azure/data-factory/data-movement-security-considerations

If you're interested in Azure compliance and how Azure secures its own infrastructure, visit the [Microsoft Trust Center](https://microsoft.com/en-us/trustcenter/default.aspx). For the latest list of all Azure Compliance offerings check - https://aka.ms/AzureCompliance.

It is important to monitor Activity Logs on the subscription and ship these to a log analytics workspace. This should help us to keep track of what changes have been made to the data factories permissions and by who.




## Performance Monitoring

Performance Monitoring on Azure Data Factory can be done using the Built-in Monitoring [docs](https://docs.microsoft.com/en-us/azure/data-factory/monitor-visually) or with Azure Monitor [docs](https://docs.microsoft.com/en-us/azure/data-factory/monitor-using-azure-monitor). For Pipeline Runs and Activities on the pipeline, using Built-in Monitoring will suffice, however when looking for more detailed metrics around resource usage, it is recommended that Azure Monitor is used.

## Keeping Azure Data Factory metrics and pipeline-run data

Data Factory stores pipeline-run data for only 45 days. Use Azure Monitor if you want to keep that data for a longer time. With Monitor, you can route diagnostic logs for analysis to multiple different targets.

- **Storage Account**: Save your diagnostic logs to a storage account for auditing or manual inspection. You can use the diagnostic settings to specify the retention time in days.
- **Event Hub**: Stream the logs to Azure Event Hubs. The logs become input to a partner service/custom analytics solution like Power BI.
- **Log Analytics**: Analyze the logs with Log Analytics. The Data Factory integration with Azure Monitor is useful in the following scenarios:
  - You want to write complex queries on a rich set of metrics that are published by Data Factory to Monitor. You can create custom alerts on these queries via Monitor.
  - You want to monitor across data factories. You can route data from multiple data factories to a single Monitor workspace.

**Monitoring PowerShell & Script-Based Commands**

For monitoring programmatically or using SDKs it is a good idea to setup scripts to ingest and read ADF Logs, although the 45-day retention period still applies.

https://docs.microsoft.com/en-us/azure/data-factory/monitor-programmatically



**Monitor Pipeline Runs**

The pipeline run grid contains the following columns:

| **Column name** | **Description**                                              |
| :-------------- | :----------------------------------------------------------- |
| Pipeline Name   | Name of the pipeline                                         |
| Run Start       | Start date and time for the pipeline run (MM/DD/YYYY, HH:MM:SS AM/PM) |
| Run End         | End date and time for the pipeline run (MM/DD/YYYY, HH:MM:SS AM/PM) |
| Duration        | Run duration (HH:MM:SS)                                      |
| Triggered By    | The name of the trigger that started the pipeline            |
| Status          | **Failed**, **Succeeded**, **In Progress**, **Canceled**, or **Queued** |
| Annotations     | Filterable tags associated with a pipeline                   |
| Parameters      | Parameters for the pipeline run (name/value pairs)           |
| Error           | If the pipeline failed, the run error                        |
| Run ID          | ID of the pipeline run                                       |

**Monitor Activity Runs**

| **Column name**     | **Description**                                              |
| :------------------ | :----------------------------------------------------------- |
| Activity Name       | Name of the activity inside the pipeline                     |
| Activity Type       | Type of the activity, such as **Copy**, **ExecuteDataFlow**, or **AzureMLExecutePipeline** |
| Actions             | Icons that allow you to see JSON input information, JSON output information, or detailed activity-specific monitoring experiences |
| Run Start           | Start date and time for the activity run (MM/DD/YYYY, HH:MM:SS AM/PM) |
| Duration            | Run duration (HH:MM:SS)                                      |
| Status              | **Failed**, **Succeeded**, **In Progress**, or **Canceled**  |
| Integration Runtime | Which Integration Runtime the activity was run on            |
| User Properties     | User-defined properties of the activity                      |
| Error               | If the activity failed, the run error                        |
| Run ID              | ID of the activity run                                       |

**Monitor Consumption**

You can see the resources consumed by a pipeline run by clicking the consumption icon next to the run.

![Screenshot that shows where you can see the resources consumed by a pipeline.](https://docs.microsoft.com/en-us/azure/data-factory/media/monitor-visually/monitor-consumption-1.png)

Clicking the icon opens a consumption report of resources used by that pipeline run.

![Monitor consumption](https://docs.microsoft.com/en-us/azure/data-factory/media/monitor-visually/monitor-consumption-2.png)

## Create Alerts

You can create alerts on various metrics, including those for ADF entity count/size, activity/pipeline/trigger runs, Integration Runtime (IR) CPU utilization/memory/node count/queue, as well as for SSIS package executions and SSIS IR start/stop operations.

