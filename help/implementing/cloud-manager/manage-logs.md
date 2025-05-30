---
title: 访问和管理日志
description: 了解如何访问和管理日志，可促进您在 AEM as a Cloud Service 中的开发过程。
exl-id: f17274ce-acf5-4e7d-b875-75d4938806cd
solution: Experience Manager
feature: Log Files, Developing
role: Admin, Architect, Developer
source-git-commit: bc92ed7acefbbd906b0986ea0b6b96fa6d8422de
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 69%

---


# 访问和管理日志 {#manage-logs}

了解如何访问和管理日志，可促进您在 AEM as a Cloud Service 中的开发过程。

您可以使用&#x200B;**概述**&#x200B;页面或环境详细信息页面中的&#x200B;**环境**&#x200B;信息卡访问所选环境的可用日志文件列表。

日志将保留七天。

## 正在下载日志 {#download-logs}

要下载日志，请执行以下操作：

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织。

1. 在&#x200B;**[我的程序](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;控制台上，选择该程序。

1. 从&#x200B;**概述**&#x200B;页面导航到&#x200B;**环境**&#x200B;信息卡。

1. 从省略号菜单中选择&#x200B;**下载日志**。

   ![下载日志菜单项](assets/download-logs1.png)

1. 在&#x200B;**下载日志**&#x200B;对话框中，从下拉菜单中选择适当的&#x200B;**服务**

   ![下载日志对话框](assets/download-preview.png)

   如果您的环境启用了[其他Publish地区](/help/operations/additional-publish-regions.md)，您将能够选择每个地区并单独下载其日志，如下所示：

   ![下载其他发布区域的日志](assets/download-publish-region-logs.png)

1. 选择服务后，单击要检索的日志旁边的下载图标。

您还可以从&#x200B;**环境**&#x200B;页面访问日志。

![“环境”屏幕中的日志](assets/download-logs.png)

## 通过 API 下载的日志 {#logs-through-api}

除了通过 UI 下载日志外，还可以通过 API 和命令行界面下载日志。

要下载特定环境的日志文件，命令如下所示。

```shell
$ aio cloudmanager:download-logs --programId 5 1884 author aemerror
```

您还可以通过命令行界面跟踪日志。

```shell
$ aio cloudmanager:tail-log --programId 5 1884 author aemerror
```

若要获得环境 Id（本例中为 1884）和可用的服务或日志名称选项，可以使用以下命令。

```shell
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

### 其他资源 {#resources}

>[!TIP]
>
>查看[此视频资源](https://app.frame.io/reviews/28cdf463-b7fc-443b-a54a-93cb7da6567e/dbf158f1-568b-4efc-8fbc-3b241561cbab)，了解有关调试AEM as a Cloud Service的更多信息。

请参阅以下附加资源，了解有关 Cloud Manager API 和 Adobe I/O CLI 的更多信息：

* [Cloud Manager API 文档](https://developer.adobe.com/experience-cloud/cloud-manager/)
* [Adobe I/O CLI](https://github.com/adobe/aio-cli-plugin-cloudmanager)

请参阅以下附加资源，了解有关AEM as a Cloud Service中日志文件的更多信息：

* [Cloud 5 AEM日志文件](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/expert-resources/cloud-5/cloud5-aem-log-files.html?lang=zh-Hans)
* [使用日志调试AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/logs.html?lang=zh-Hans)
