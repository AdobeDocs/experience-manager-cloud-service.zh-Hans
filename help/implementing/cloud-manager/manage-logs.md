---
title: 管理日志-Cloud Service
description: 管理日志-Cloud Service
translation-type: tm+mt
source-git-commit: 703248cdcab9797b20d3f7e46f7ac03c15ec6980
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 17%

---


# 访问和管理日志 {#manage-logs}

用户可以使用列表卡访问选定环境的可用日志文件的环境。  用户可以访问选定环境的可用日志文件列表。

这些文件可通过UI下载，可从“概述” **页面** :

![](assets/download-logs1.png)

或者，环境 **页面** :

![](assets/download-logs.png)

>[!NOTE]
>无论打开位置如何，都会显示相同的对话框，允许下载单个日志文件。

![](assets/download-logs2.png)


## 通过API进行日志 {#logs-thorugh-api}

除了通过UI下载日志外，日志还可通过API和命令行界面使用。

例如，要下载特定环境的日志文件，该命令将是

```java
$ aio cloudmanager:download-logs --programId 5 1884 author aemerror
```

以下命令允许跟踪日志：

```java
$ aio cloudmanager:tail-log --programId 5 1884 author aemerror
```

为了获得环境ID（本例中为1884）以及可用的服务或日志名称选项，您可以使用：

```java
$ aio cloudmanager:list-environments
Environment Id Name                     Type  Description                          
1884           FoundationInternal_dev   dev   Foundation Internal Dev environment  
1884           FoundationInternal_stage stage Foundation Internal STAGE environment
1884           FoundationInternal_prod  prod  Foundation Internal Prod environment
 
 
$ aio cloudmanager:list-available-log-options 1884
Environment Id Service    Name         
1884           author     aemerror     
1884           author     aemrequest   
1884           author     aemaccess    
1884           publish    aemerror     
1884           publish    aemrequest   
1884           publish    aemaccess    
1884           dispatcher httpderror   
1884           dispatcher aemdispatcher
1884           dispatcher httpdaccess
```

>[!NOTE]
>虽然 **日志下载** (Log Downloads **)可通过UI和API使用，但** Log Tailing（日志跟踪）是仅限API/CLI的。

### 其他资源 {#resources}

请参阅以下其他资源，进一步了解Cloud Manager API和AdobeI/O CLI:

* [Cloud Manager API文档](https://www.adobe.io/apis/experiencecloud/cloud-manager/docs.html)
* [AdobeI/O CLI](https://github.com/adobe/aio-cli-plugin-cloudmanager)