---
title: 处理大型内容存储库
description: 本节介绍如何处理大型内容存储库
source-git-commit: a6d225943c5d23ebd960fda0b0912a81f1f80014
workflow-type: tm+mt
source-wordcount: '1739'
ht-degree: 1%

---

# 处理大型内容存储库 {#handling-large-content-repositories}

## 概述 {#overview}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_precopy"
>title="处理大型内容存储库"
>abstract="为了显着加快内容传输活动的提取和摄取阶段以将内容移动到AEMas a Cloud Service,CTT可以将AzCopy作为可选的预复制步骤。 配置此预先步骤后，在提取阶段，AzCopy会将Blob从Amazon S3或Azure Blob Storage复制到迁移集Blob存储。 在摄取阶段，AzCopy将Blob从迁移集Blob存储复制到目标AEMas a Cloud ServiceBlob存储。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en#setting-up-pre-copy-step" text="开始使用AzCopy作为预复制步骤"

使用内容传输工具(CTT)复制大量Blob可能需要多天。
为了显着加快内容传输活动的提取和摄取阶段以将内容移动到AEMas a Cloud Service,CTT可以利用 [AzCopy](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) 作为可选的预复制步骤。 在将源AEM实例配置为使用Amazon S3、Azure Blob Storage数据存储或文件数据存储时，可以使用此预复制步骤。 配置此预先步骤后，在提取阶段，AzCopy将Blob从Amazon S3、Azure Blob Storage或文件数据存储复制到迁移集Blob存储。 在摄取阶段，AzCopy将Blob从迁移集Blob存储复制到目标AEMas a Cloud ServiceBlob存储。

>[!NOTE]
> 此功能已在CTT 1.5.4版本中引入。

## 开始之前的重要注意事项 {#important-considerations}

在开始之前，请阅读以下章节，了解重要注意事项：

* 源AEM版本需要为6.3 - 6.5。

* 源AEM数据存储配置为使用Amazon S3或Azure Blob Storage。 有关更多详细信息，请参阅 [在AEM 6中配置节点存储和数据存储](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/data-store-config.html?lang=en).

* 每个迁移集都将复制整个数据存储，因此只应使用一个迁移集。

* 您需要访问才能安装 [AzCopy](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) 在运行源AEM实例的实例（或VM）上。

* 数据存储垃圾收集已在源上的前7天内运行。 有关更多详细信息，请参阅 [数据存储垃圾收集](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/data-store-config.html?lang=en#data-store-garbage-collection).


### 如果将源AEM实例配置为使用Amazon S3或Azure Blob Storage数据存储，则需考虑的其他事项 {#additional-considerations-amazons3-azure}

* 由于从Amazon S3和Azure Blob Storage中传输数据存在相关成本，因此传输成本将与存储容器中的数据总量(无论是否在AEM中引用)相关。 请参阅 [Amazon S3](https://aws.amazon.com/s3/pricing/) 和 [Azure Blob存储](https://azure.microsoft.com/en-us/pricing/details/bandwidth/) 以了解更多详细信息。

* 您需要源Amazon S3存储段的访问密钥和密钥对，或源Azure Blob Storage容器的SAS URI（只读访问可以正常）。

### 如果源AEM实例配置为使用文件数据存储，则其他注意事项 {#additional-considerations-aem-instance-filedatastore}

* 本地系统的可用空间必须严格大于源数据存储的1/256大小。 例如，如果数据存储的大小为3 TB，则中必须存在大于11.72 GB的可用空间 `crx-quickstart/cloud-migration` 文件夹，以便AzCopy正常工作。 源系统至少应具有1 GB的可用空间。 可利用 `df -h` 命令，以及Windows实例中的dir命令。

* 每次在启用AzCopy的情况下运行提取时，整个文件数据存储都会被扁平化，并复制到云迁移容器中。 如果您的迁移集大大小于数据存储的大小，则AzCopy提取不是最佳方法。

* 使用AzCopy通过数据存储进行复制后，请将其禁用以进行增量或增补提取。

## 设置为使用AzCopy作为预复制步骤 {#setting-up-pre-copy-step}

请阅读本节内容，了解如何设置如何使用AzCopy作为内容传输工具的预复制步骤，以将内容迁移到AEMas a Cloud Service:

### 0.确定数据存储中所有内容的总大小 {#determine-total-size}

确定数据存储的总大小很重要，原因有二：

* 如果源AEM配置为使用文件数据存储，则本地系统的可用空间必须严格大于源数据存储的1/256大小。

* 了解数据存储的总大小将有助于评估提取和摄取时间。 使用 [内容传输工具计算器](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-implementation-phase.html?lang=en#content-transfer) in [Cloud Acceleration Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/introduction-cam/overview-cam.html?lang=en) 以获取提取和摄取时间的估计值。

#### Azure Blob存储数据存储 {#azure-blob-storage}

从Azure门户的容器属性页面中，使用 **计算大小** 按钮以确定容器中所有内容的大小。 例如：

![图像](/help/journey-migration/content-transfer-tool/assets/Azure-blob-storage-data-store.png)

#### Amazon S3数据存储 {#amazon-data}

您可以使用容器的“量度”选项卡确定容器中所有内容的大小。 例如：


![图像](/help/journey-migration/content-transfer-tool/assets/amazon-s3-data-store.png)

#### 文件数据存储 {#file-data-store-determine-size}

* 对于mac、UNIX系统，在数据存储目录上运行du命令以获取其大小：
   `du -sh [path to datastore on the instance]`. 例如，如果您的数据存储位于 `/mnt/author/crx-quickstart/repository/datastore`，以下命令将获得其大小： `du -sh /mnt/author/crx-quickstart/repository/datastore`.

* 对于Windows，使用数据存储目录上的dir命令获取其大小：
   `dir /a/s [location of datastore]`。

### 1.安装AzCopy {#install-azcopy}

[AzCopy](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) 是Microsoft提供的命令行工具，需要在源实例上可用才能启用此功能。

简而言之，您很可能希望从 [AzCopy文档页面](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) 并将其解除标记到/usr/bin等位置。

>[!IMPORTANT]
>请注意二进制文件的放置位置，因为您将需要在后续步骤中获得该二进制文件的完整路径。

### 2.安装支持AzCopy的内容传输工具(CTT)版本 {#install-ctt-azcopy-support}

CTT 1.5.4版本中包含对Amazon S3和Azure Blob Storage的AzCopy支持。
CTT 1.7.2版本中包含对文件数据存储的支持。您可以从 [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html) 门户。


### 3.配置azcopy.config文件 {#configure-azcopy-config-file}

在源AEM实例上， `crx-quickstart/cloud-migration`，请创建名为 `azcopy.config`.

>[!NOTE]
>此配置文件的内容将因源AEM实例是使用Azure还是Amazon S3数据存储还是文件数据存储而异。

#### Azure Blob存储数据存储 {#azure-blob-storage-data}

您的azcopy.config文件应包含以下属性（确保为实例使用正确的azCopyPath和azureSas）。

>[!NOTE]
>
> 如果您不想授予对Blob存储容器的写入权限，则可以生成一个新的SAS URI，该URI仅具有读取和列表权限。

```
azCopyPath=/usr/bin/azcopy
azureSas=https://example-resource.blob.core.windows.net/example-container?sig=--REDACTED--
```

#### Amazon S3数据存储 {#amazon-sdata-store}

您的azcopy.config文件应包含以下属性（确保为实例使用正确的值）。

>[!NOTE]
>
> 如果您的实例使用IAM角色来启用AEM以访问S3，则您将需要创建策略和用户，并为S3存储段启用ListBucket和GetObject操作。 设置后，使用此用户的访问密钥和密钥。

```
azCopyPath=/usr/bin/azcopy
s3Bucket=aem-63
s3Region=us-west-2
s3AccessKey=--REDACTED--
s3SecretKey=--REDACTED--
```

#### 文件数据存储 {#file-data-store-azcopy-config}

您的 `azcopy.config` 文件必须包含azcopyPath属性，以及指向文件数据存储位置的可选repository.home属性。 为实例使用正确的值。
文件数据存储

```
azCopyPath=/usr/bin/azcopy
repository.home=/mnt/crx/author/crx-quickstart/repository/datastore
```

azcopyPath属性必须包含源AEM实例上安装azCopy命令行工具的位置的完整路径。 如果azCopyPath属性缺失，则不会执行Blob预复制步骤。

如果 `repository.home` azcopy.config中缺少属性，则缺省数据存储位置 `/mnt/crx/author/crx-quickstart/repository/datastore` 将用于执行预复制。

### 4.用AzCopy提取 {#extracting-azcopy}

在上述配置文件就位后，AzCopy预复制阶段将作为后续提取的一部分运行。 要阻止其运行，您可以重命名此文件或将其删除。

>[!NOTE]
>如果AzCopy配置不正确，您会在日志中看到以下消息：
>`INFO c.a.g.s.m.c.a.AzCopyCloudBlobPreCopy - Blob pre-copy is not supported`。

1. 从CTT UI开始提取。 请参阅 [内容传输工具快速入门](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=en) 和 [提取流程](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/extracting-content.html?lang=en) 以了解更多详细信息。

1. 确认提取日志中打印了以下行：

```
c.a.g.s.m.commons.ContentExtractor - *************** Beginning AzCopy Pre-Copy phase ***************
```

恭喜！ 此日志条目表示您的配置被视为有效，AzCopy当前正在将所有Blob从源容器复制到迁移容器。

来自AzCopy的日志条目将显示在提取日志中，并将添加c.a.g.s.m.c.azcopy.AzCopyBlobPreCopy - [AzCopy预拷贝]

>[!CAUTION]
>
> 提取的前几分钟，请仔细观看提取日志，以查找问题的任何迹象。 例如，如果找不到源Azure容器，将记录以下内容：

```
[AzCopy pre-copy] failed to perform copy command due to error: cannot start job due to error: cannot list files due to reason -> github.com/Azure/azure-storage-blob-go/azblob.newStorageError, github.com/Azure/azure-storage-blob-go@v0.10.1-0.20210407023846-16cf969ec1c3/azblob/zc_storage_error.go:42
[AzCopy pre-copy] ===== RESPONSE ERROR (ServiceCode=ContainerNotFound) =====
[AzCopy pre-copy] Description=The specified container does not exist.
[AzCopy pre-copy] RequestId:5fb674b9-201e-001b-2a5b-527400000000
[AzCopy pre-copy] Time:2021-05-26T18:18:07.5931967Z, Details: 
[AzCopy pre-copy] Code: ContainerNotFound
```

如果AzCopy出现问题，提取将立即失败，提取日志将包含有关失败的详细信息。

AzCopy会在后续运行中自动跳过在错误之前复制的任何Blob，而无需再次复制。

#### 对于文件数据存储 {#file-data-store-extract}

当为源文件dataStore运行AzCopy时，您应会在日志中看到如下消息，指示文件夹正在处理：
`c.a.g.s.m.c.a.AzCopyFileSourceBlobPreCopy - [AzCopy pre-copy] Processing folder (1/24) crx-quickstart/repository/datastore/5d`

### 5.使用AzCopy摄取 {#ingesting-azcopy}

随着内容传输工具1.5.4的发布，我们为创作摄取添加了AzCopy支持。

>[!NOTE]
>建议先单独运行创作摄取。 这将在稍后运行发布摄取时加快其速度。

要在摄取期间利用AzCopy，我们要求您使用至少为2021.6.5561版的AEMas a Cloud Service版本。

从CTT UI开始创作摄取。 请参阅 [摄取流程](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/ingesting-content.html?lang=en) 以了解更多详细信息。
AzCopy中的日志条目将显示在摄取日志中。 它们将如下所示：

```
*************** Beginning AzCopy pre-copy phase ***************
INFO: Scanning...
INFO: Failed to create one or more destination container(s). Your transfers may still succeed if the container already exists.
INFO: Any empty folders will not be processed, because source and/or destination doesn't have full folder support
INFO: azcopy: A newer version 10.11.0 is available to download
 
 
Job 419d98da-fc05-2a45-70cc-797fee632031 has started
Log file is located at: /root/.azcopy/419d98da-fc05-2a45-70cc-797fee632031.log
 
 
0.0 %, 0 Done, 0 Failed, 886 Pending, 0 Skipped, 886 Total,
 
 
Job 419d98da-fc05-2a45-70cc-797fee632031 summary
Elapsed Time (Minutes): 0.0334
Number of File Transfers: 886
Number of Folder Property Transfers: 0
Total Number of Transfers: 886
Number of Transfers Completed: 17
Number of Transfers Failed: 0
Number of Transfers Skipped: 869
TotalBytesTransferred: 248350
Final Job Status: CompletedWithSkipped
 
*************** Completed AzCopy pre-copy phase ***************
```

## 禁用AzCopy {#disable-azcopy}

要禁用AzCopy，请重命名或删除 `azcopy.config` 文件。

例如，可以通过以下方式禁用azcopy提取： `mv /mnt/crx/author/crx-quickstart/cloud-migration/azcopy.config /mnt/crx/author/crx-quickstart/cloud-migration/noazcopy.config`.

## 下一步 {#whats-next}

学习了处理大型内容存储库以显着加快内容传输活动的提取和摄取阶段以将内容移动到AEMas a Cloud Service后，您便可以学习内容传输工具中的提取流程。 请参阅 [在内容传输工具中从源提取内容](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md) 了解如何从内容传输工具中提取迁移集。