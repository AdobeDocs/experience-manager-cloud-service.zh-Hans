---
title: 处理大型内容存储库
description: 本节介绍如何处理大型内容存储库
exl-id: 21bada73-07f3-4743-aae6-2e37565ebe08
source-git-commit: abe5f8a4b19473c3dddfb79674fb5f5ab7e52fbf
workflow-type: tm+mt
source-wordcount: '1800'
ht-degree: 8%

---

# 处理大型内容存储库 {#handling-large-content-repositories}

## 概述 {#overview}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_precopy"
>title="处理大型内容存储库"
>abstract="为了显著加快将内容移至 AEM as a Cloud Service 的内容转移活动的提取和引入阶段，内容转移工具（CTT）可使用 AzCopy 作为可选的复制前步骤。配置此前置步骤后，在提取阶段，AzCopy 将 blob 从 Amazon S3 或 Azure Blob 存储复制到迁移集 blob 存储。在引入阶段，AzCopy 将 blob 从迁移集 blob 存储复制到目标 AEM as a Cloud Service blob 存储。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=zh-Hans#setting-up-pre-copy-step" text="AzCopy 作为复制前步骤的快速入门"

使用内容传输工具(CTT)复制多个Blob可能需要几天时间。
要加快内容传输活动的提取和摄取阶段以将内容移至AEMas a Cloud Service，CTT可以使用 [AzCopy](https://learn.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) 作为可选的预复制步骤。 当源AEM实例配置为使用Amazon S3、Azure Blob Storage数据存储或文件数据存储时，可以使用此预复制步骤。 预复制步骤对首次完全提取和摄取最有效。 但是，不建议对后续增补使用预复制（如果增补大小小于200 GB），因为这可能会增加整个过程所需的时间。 配置此预步骤后，在提取阶段，AzCopy会将Blob从Amazon S3、Azure Blob存储或文件数据存储中复制到迁移集Blob存储中。 在引入阶段，AzCopy 将 blob 从迁移集 blob 存储复制到目标 AEM as a Cloud Service blob 存储。

## 开始前的重要注意事项 {#important-considerations}

请阅读以下章节，以了解在开始之前需要考虑的重要事项：

* 从CTT版本2.0.16开始，预复制设置会在安装捆绑包时自动完成。 此外，如果迁移集大小大于200 GB，则提取过程将自动使用预复制功能。 azcopy.config文件在crx-quickstart/cloud-migration/目录中创建。 如果您使用CTT版本2.0.16或更高版本，则无需手动进行预复制设置。

* 源AEM版本必须为6.3 - 6.5。

* 源AEM数据存储配置为使用Amazon S3或Azure Blob存储。 有关更多详细信息，请参阅 [在AEM 6中配置节点存储和数据存储](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/data-store-config.html).

* 每个迁移集都会复制整个数据存储，因此只应使用单个迁移集。

* 您需要访问权限才能安装 [AzCopy](https://learn.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) 在运行源AEM实例的实例（或VM）上。

* 在过去七天内，在源上运行了数据存储垃圾收集。 有关更多详细信息，请参阅 [数据存储垃圾收集](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/data-store-config.html#data-store-garbage-collection).

### 如果源AEM实例配置为使用Amazon S3或Azure Blob存储数据存储，则其他注意事项 {#additional-considerations-amazons3-azure}

* 从Amazon S3和Azure Blob Storage传输数据会产生成本。 传输成本与现有存储容器中的数据总量相关(无论是否在AEM中引用)。 请参阅 [Amazon S3](https://aws.amazon.com/s3/pricing/) 和 [Azure Blob存储](https://azure.microsoft.com/en-us/pricing/details/bandwidth/) 以了解更多详细信息。

* 您既需要现有源Amazon S3存储段的访问密钥和密钥对，也需要现有源Azure Blob存储容器的SAS URI（只读访问正常）。

### 如果将源AEM实例配置为使用文件数据存储，则应考虑其他事项 {#additional-considerations-aem-instance-filedatastore}

* 本地系统的可用空间必须严格大于源数据存储大小的1/256。 例如，如果数据存储的大小为3 TB，则大于11.72 GB的可用空间必须存在于 `crx-quickstart/cloud-migration` 要使AzCopy正常工作的源上的文件夹。 源系统至少应有1 GB的可用空间。 可用空间可以通过使用获得 `df -h` Linux®实例中的command和Windows实例中的dir command。

* 每次在启用AzCopy的情况下运行提取时，整个文件数据存储都会扁平化并复制到云迁移容器中。 如果迁移集小于数据存储的大小，则AzCopy提取不是最佳方法。

* 使用AzCopy复制现有数据存储后，请为增量或增补提取禁用它。

## 设置使用AzCopy作为预复制步骤 {#setting-up-pre-copy-step}

>[!NOTE]
>从CTT版本2.0.16开始，预复制设置会在安装捆绑包时自动完成。 此外，如果迁移集大小大于200 GB，则提取过程将自动使用预复制功能。 azcopy.config文件在crx-quickstart/cloud-migration/目录中创建。 如果要手动更新文件的配置，请查看以下部分。

请阅读此部分，以便了解如何设置将AzCopy用作内容传输工具的预复制步骤，将内容迁移到AEMas a Cloud Service：

### 0.确定数据存储中所有内容的总大小 {#determine-total-size}

确定数据存储的总大小很重要，原因有二：

* 如果将源AEM配置为使用文件数据存储，则本地系统的可用空间必须严格大于源数据存储大小的1/256。

#### Azure Blob存储数据存储 {#azure-blob-storage}

在Azure Portal中的现有容器属性页面中，使用 **计算大小** 按钮来确定容器中所有内容的大小。 例如：

![图像](/help/journey-migration/content-transfer-tool/assets/Azure-blob-storage-data-store.png)

#### Amazon S3数据存储 {#amazon-data}

您可以使用容器的“量度”选项卡来确定容器中所有内容的大小。 例如：


![图像](/help/journey-migration/content-transfer-tool/assets/amazon-s3-data-store.png)

#### 文件数据存储 {#file-data-store-determine-size}

* 对于Mac、UNIX®系统，在datastore目录上运行du命令以获取其大小：
  `du -sh [path to datastore on the instance]`. 例如，如果您的数据存储在 `/mnt/author/crx-quickstart/repository/datastore`，则以下命令会获取其大小： `du -sh /mnt/author/crx-quickstart/repository/datastore`.

* 对于Windows，使用数据存储目录上的dir命令获取其大小：
  `dir /a/s [location of datastore]`。

### 1.安装AzCopy {#install-azcopy}

[AzCopy](https://learn.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) 是由Microsoft提供的命令行工具®必须在源实例上可用才能启用此功能。

简而言之，您要从下载Linux® x86-64二进制文件 [AzCopy文档页面](https://learn.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) 并将其解压到某个位置，如/usr/bin。

>[!IMPORTANT]
>请记下放置二进制文件的位置，因为需要在后续步骤中获取该二进制文件的完整路径。

### 2.安装支持AzCopy的内容传输工具(CTT)版本 {#install-ctt-azcopy-support}

>[!IMPORTANT]
>应使用最新发布的CTT版本。

最新CTT版本中包含对Amazon S3、Azure Blob Storage和文件数据存储的AzCopy支持。
您可以从以下网站下载最新版本的CTT： [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html) 门户。
需要注意的是，仅支持版本2.0.0及更高版本，建议使用最新版本。

### 3.配置azcopy.config文件 {#configure-azcopy-config-file}

在源AEM实例上，位于 `crx-quickstart/cloud-migration`，创建一个名为的文件 `azcopy.config`.

>[!NOTE]
>此配置文件的内容因您的源AEM实例使用的是Azure还是Amazon S3数据存储或文件数据存储而有所不同。

#### Azure Blob存储数据存储 {#azure-blob-storage-data}

您的azcopy.config文件应包含以下属性（请确保为实例使用正确的azCopyPath和azureSas）。

>[!NOTE]
>
> 如果不希望向现有blob存储容器授予写入权限，则可以生成一个只具有读取和列表权限的新SAS URI。

```
azCopyPath=/usr/bin/azcopy
azureSas=https://example-resource.blob.core.windows.net/example-container?sig=--REDACTED--
```

#### Amazon S3数据存储 {#amazon-sdata-store}

azcopy.config文件应包含以下属性（请确保为实例使用正确的值）。

>[!NOTE]
>
> 如果您的实例使用IAM角色来启用AEM以访问S3，则必须创建一个策略和用户，并为S3存储段启用ListBucket和GetObject操作。 设置后，使用此用户的访问密钥和密钥。

```
azCopyPath=/usr/bin/azcopy
s3Bucket=aem-63
s3Region=us-west-2
s3AccessKey=--REDACTED--
s3SecretKey=--REDACTED--
```

#### 文件数据存储 {#file-data-store-azcopy-config}

您的 `azcopy.config` 文件必须包含azCopyPath属性和指向文件数据存储位置的可选repository.home属性。 为您的实例使用正确的值。
文件数据存储

```
azCopyPath=/usr/bin/azcopy
repository.home=/mnt/crx/author/crx-quickstart/repository/datastore
```

azCopyPath属性必须包含源AEM实例上安装azCopy命令行工具的位置的完整路径。 如果缺少azCopyPath属性，则不执行blob预复制步骤。

如果 `repository.home` azcopy.config中缺少属性，因此缺少默认的数据存储位置 `/mnt/crx/author/crx-quickstart/repository/datastore` 用于执行预复制。

### 4.使用AzCopy提取 {#extracting-azcopy}

有了上述配置文件，AzCopy预复制阶段将作为每次后续提取的一部分运行。 要阻止其运行，可以重命名或移除此文件。

>[!NOTE]
>如果未正确配置AzCopy，您将在日志中看到以下消息：
>`INFO c.a.g.s.m.c.a.AzCopyCloudBlobPreCopy - Blob pre-copy is not supported`。

1. 从CTT UI开始提取。 请参阅 [内容传输工具快速入门](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/getting-started-content-transfer-tool.md) 和 [提取过程](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md) 以了解更多详细信息。

1. 确认在提取日志中打印了以下行：

```
c.a.g.s.m.commons.ContentExtractor - *************** Beginning AzCopy Pre-Copy phase ***************
```

恭喜！此日志条目表示您的配置被视为有效，并且AzCopy正在将所有blob从源容器复制到迁移容器。

AzCopy中的日志条目显示在提取日志中，并以c.a.g.s.m.c.azcopy.AzCopyBlobPreCopy为前缀 —  [AzCopy预复制]

>[!CAUTION]
>
> 在提取的前几分钟，请密切观察提取日志是否有任何问题迹象。 例如，如果找不到源Azure容器，将记录以下内容：

```
[AzCopy pre-copy] failed to perform copy command due to error: cannot start job due to error: cannot list files due to reason > github.com/Azure/azure-storage-blob-go/azblob.newStorageError, github.com/Azure/azure-storage-blob-go@v0.10.1-0.20210407023846-16cf969ec1c3/azblob/zc_storage_error.go:42
[AzCopy pre-copy] ===== RESPONSE ERROR (ServiceCode=ContainerNotFound) =====
[AzCopy pre-copy] Description=The specified container does not exist.
[AzCopy pre-copy] RequestId:5fb674b9-201e-001b-2a5b-527400000000
[AzCopy pre-copy] Time:2021-05-26T18:18:07.5931967Z, Details: 
[AzCopy pre-copy] Code: ContainerNotFound
```

如果AzCopy存在问题，提取将立即失败，并且提取日志包含有关失败的详细信息。

AzCopy在后续运行时会自动跳过在错误之前复制的任何Blob，并且无需再次复制。

>[!TIP]
>现在，提取成功后，可以将摄取计划为立即自动开始。 请参阅 [将内容提取到目标](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md) 以了解更多信息。

#### 用于文件数据存储 {#file-data-store-extract}

当为源文件dataStore运行AzCopy时，您应在日志中看到以下消息，指示正在处理文件夹：
`c.a.g.s.m.c.a.AzCopyFileSourceBlobPreCopy - [AzCopy pre-copy] Processing folder (1/24) crx-quickstart/repository/datastore/5d`

### 5.使用AzCopy引入 {#ingesting-azcopy}

请参阅 [将内容提取到目标](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md) 有关从Cloud Acceleration Manager (CAM)将内容摄取到目标的一般信息，包括在“新建摄取”对话框中关于如何使用AzCopy（预复制）或不使用的说明。

要在摄取期间使用AzCopy，Adobe要求您使用的是至少版本2021.6.5561的AEMas a Cloud Service版本。

请查看Cloud Acceleration Manager中的“引入作业”列表和引入日志，以便您能够查看进度。 与成功的AzCopy任务相关的日志条目显示如下（允许存在某些差异）。 有时检查日志可能会提前通知您问题，并帮助您找到解决任何问题的快速方法。

```
*************** Beginning AzCopy pre-copy phase ***************
INFO: Scanning...
INFO: Failed to create one or more destination container(s). Your transfers may still succeed if the container already exists.
INFO: Any empty folders will not be processed, because source and/or destination does not have full folder support
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

## 后续内容 {#whats-next}

您现在已了解如何处理大型内容存储库，从而加快内容传输活动的提取和摄取阶段以将内容移至AEMas a Cloud Service。 您现在可以学习使用内容传输工具的提取流程。 请参阅 [在内容传输工具中从源提取内容](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md) 这样您就可以了解如何从内容传输工具中提取迁移集。
