# Storage accounts

An Azure storage account contains all of your Azure Storage data objects: blobs, files, queues, tables, and disks. The storage account provides a unique namespace for your Azure Storage data that is accessible from anywhere in the world over HTTP or HTTPS. Data in your Azure storage account is durable and highly available, secure, and massively scalable. for more info refer to the [docs](https://docs.microsoft.com/en-us/azure/storage/common/storage-account-overview) 

When it comes to saving files we have two types of storage accounts

- Storage accounts with hierarchical namespace (aka Data Lake Gen2):
  - Folders are real objects that are independent from the files inside them 
  - Supports a superset of POSIX permissions along with ACL
- Storage accounts without hierarchical namespace (aka blob storage)
  - Flat hierarchy, folders are just added to the name of the file, by deleting the last file in a folder, the folder disappear. 
  - Supports ACL on the container level only. No folder or file level



## Security Monitoring/Auditing

| What to Monitor        | How to Monitor            | Comments                                                     |
| ---------------------- | ------------------------- | ------------------------------------------------------------ |
| Configuration changes  | Activity logs             | Make sure to send activity logs (per subscription) to log analytics workspace then query the logs from there. For known security configuration changes like *secure transfer required* , alerts should be created for it |
| Data Access logging    | Storage Analytics logging | ![image-20200924000811590](/monitoring/assets/images/image-20200924000811590.png) <br /> For more details refer to the [docs](https://docs.microsoft.com/en-us/azure/storage/common/storage-analytics-logging?tabs=dotnet) |
| Unusual egress traffic | Azure monitor - Metrics   | ![image-20200924104121774](/monitoring/assets/images/image-20200924104121774.png)<br />The Egress metrics shows the size of the egress traffic. If you have higher than usual, that can be a sign of breach and data exfiltration attempt. You can use the [dynamic threshold feature](https://docs.microsoft.com/en-us/azure/azure-monitor/platform/alerts-dynamic-thresholds) of Azure monitor |





## Performance Monitoring

