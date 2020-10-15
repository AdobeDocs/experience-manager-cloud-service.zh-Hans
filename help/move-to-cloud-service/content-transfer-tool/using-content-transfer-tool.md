---
title: 使用内容传输工具
description: 使用内容传输工具
translation-type: tm+mt
source-git-commit: e96ffc15849baa306fae8839476fa453ace69ef5
workflow-type: tm+mt
source-wordcount: '1710'
ht-degree: 78%

---


# 使用内容传输工具 {#using-content-transfer-tool}

## 使用内容传输工具的重要注意事项 {#pre-reqs}

请阅读以下章节，以了解运行内容传输工具时的重要注意事项：

* 内容传输工具的最低系统要求为 AEM 6.3 + 和 JAVA 8。如果您使用的是较低版本的 AEM，则需要将内容存储库升级到 AEM 6.5，才能使用内容传输工具。

* 需要在AEM环境上配置Java，以便 `java` 命令可由开始AEM的用户执行。

* 内容传输工具可用于以下类型的数据存储：文件数据存储、S3数据存储、共享的S3数据存储和Azure Blob存储数据存储。

* 如果您使用沙 *箱环境*，请确保环境为最新并升级到最新版本。 如果您使用的是“生产环境”**，则会自动更新。

* 要使用内容传输工具，您必须是源实例上的管理员用户，并且属于要将内容传输到的Cloud Service实例中的本地AEM管理员组。 无特权的用户将无法检索访问令牌，进而无法使用内容传输工具。

* 在提取阶段，内容传输工具将在活动 AEM 源实例上执行。

* 作者的&#x200B;*摄取阶段*&#x200B;将会按比例缩小整个作者部署。这意味着作者 AEM 在整个摄取过程中将不可用。

* 当前，AEM作为Cloud Service作者实例的默认MongoDB大小为32GB。 建议对于大于20GB的区段存储大小，您应提交支持票证以增加MongoDB大小。

## 可用性 {#availability}

内容传输工具可从软件分发门户下载为zip文件。 您可以通过包管理器在源 Adobe Experience Manager (AEM) 实例上安装该包。确保下载最新版本。 有关最新版本的更多详细信息，请参 [阅发行说明](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html)。

>[!NOTE]
>从[软件分发](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)门户下载内容传输工具。

## 运行内容传输工具 {#running-tool}

>[!VIDEO](https://video.tv.adobe.com/v/35460/?quality=12&learn=on)

请阅读以下章节，了解如何使用内容传输工具将内容迁移至 AEM 云服务（创作/发布）：

1. 选择 Adobe Experience Manager 并导航到工具 -> **操作** -> **内容传输**。

   ![图像](/help/move-to-cloud-service/content-transfer-tool/assets/content1.png)

1. 创建第一个迁移集时，将显示以下控制台。 单击&#x200B;**创建迁移集**&#x200B;以创建新的迁移集。

   ![图像](/help/move-to-cloud-service/content-transfer-tool/assets/01-migration-set-overview.png)

   >[!NOTE]
   >如果您有现有迁移集，控制台将显示现有迁移集的列表及其当前状态。

1. 按如下所述填充&#x200B;**内容迁移集详细信息**&#x200B;屏幕中的字段。

   ![图像](/help/move-to-cloud-service/content-transfer-tool/assets/02-migration-set-creation.png)


   1. **名称**：输入迁移集的名称。
      >[!NOTE]
      >迁移集名称不允许使用特殊字符。

   1. **云服务配置**：输入目标 AEM 云服务作者 URL。

      >[!NOTE]
      >在内容传输活动期间，您一次最多可以创建和维护四个迁移集。
      >此外，您还必须为每个特定的环境（*暂存*、*开发*&#x200B;或&#x200B;*生产*）单独创建迁移。

   1. **访问令牌**：输入访问令牌。

      >[!NOTE]
      >您可以使用“打开访问令牌”按 **钮检索访问令牌** 。 您需要确保属于目标Cloud Service实例中的AEM管理员组。

   1. **参数**：选择以下参数以创建迁移集：

      1. **包含版本**：根据需要选择。

      1. **要包含的路径**：使用路径浏览器选择需要迁移的路径。路径选取器通过键入或选择接受输入。

         >[!IMPORTANT]
         >创建迁移集时，以下路径受到限制：
         >* `/apps`
         >* `/libs`
         >* `/home`
         >* `/etc`


1. 填充&#x200B;**内容迁移集详细信息**&#x200B;屏幕中的所有字段后，单击&#x200B;**保存**。

1. 您将在&#x200B;*概述*&#x200B;页面中查看迁移集。

   ![图像](/help/move-to-cloud-service/content-transfer-tool/assets/04-item-selection-and-quick-actions.png)

   此屏幕中的所有现有迁移集及其当前状态和状态信息都会显示在&#x200B;*概述*&#x200B;页面上。您可能会看到下面介绍的一些图标。

   * *红色云*&#x200B;表示您无法完成提取流程。
   * *绿色云*&#x200B;表示您可以完成完整的提取流程。
   * *黄色图标*&#x200B;表示您没有创建现有迁移集，而特定迁移集是由同一实例中的其他用户创建的。

1. 从“概述”页面中选择一个迁移集，然后单击&#x200B;**属性**&#x200B;以查看或编辑迁移集属性。编辑属性时，无法更改容器名称或服务URL。



### 内容传输中的提取流程 {#extraction-process}

请按照以下步骤从内容传输工具中提取迁移集：

1. 从&#x200B;*概述*&#x200B;页面中选择一个迁移集，然后单击&#x200B;**提取**&#x200B;以开始提取。The **Migration Set extraction** dialog box displays and click on **Extract** to start the extraction phase.

   ![图像](/help/move-to-cloud-service/content-transfer-tool/assets/06-content-extraction.png)

   >[!NOTE]
   >您可以选择在提取阶段覆盖暂存容器。


1. 提取 **字段** 现在显示“ **正在运行** ”状态，以指示提取正在进行中。

   ![图像](/help/move-to-cloud-service/content-transfer-tool/assets/07-extraction-job-running.png)

   提取完成后，迁移集的状态将更新为&#x200B;**已完成**，而且&#x200B;**信息**&#x200B;字段下会显示一个&#x200B;*纯绿色*&#x200B;的云朵图标。

   ![图像](/help/move-to-cloud-service/content-transfer-tool/assets/10-extraction-complete.png)

   >[!NOTE]
   >UI具有自动重新加载功能，每30秒重新加载一次概述页面。
   >提取阶段启动后，将创建写锁定并在 *60* 秒后将其释放。因此，如果停止提取，则需要等待一分钟以便释放锁定，之后才能再次开始提取。

#### 增补提取 {#top-up-extraction-process}

内容传输工具具备支持差异内容增补的功能，借助该功能，您可以仅传输自上次内容传输活动以来所做的更改。

>[!NOTE]
>初始内容传输完成后，建议在云服务上线之前，经常对差异内容进行增补，以缩短最终差异内容传输的内容冻结期。

完成提取流程后，可以使用增补提取方法传输增量内容。应遵循以下步骤：

1. 导航到&#x200B;*概述*&#x200B;页面，然后选择要对其执行增补提取的迁移集。单击&#x200B;**提取**&#x200B;以开始增补提取。此时将显示&#x200B;**迁移集提取**&#x200B;对话框。

   >[!IMPORTANT]
   >
   >您应该禁用&#x200B;**在提取期间覆盖暂存容器**&#x200B;选项。
   >
   >![图像](/help/move-to-cloud-service/content-transfer-tool/assets/11-topup-extraction.png)

### 内容传输中的摄取流程{#ingestion-process}

请按照以下步骤从内容传输工具中摄取迁移集：

1. 从&#x200B;*概述*&#x200B;页面中选择一个迁移集，然后单击&#x200B;**摄取**&#x200B;以开始提取。此时将显示&#x200B;**迁移集摄取**&#x200B;对话框。Click on **Ingest** to start the ingestion phase. 出于演示目的，禁用了&#x200B;**将内容摄取到创作实例**&#x200B;选项。否则其会将内容同时摄取到“创作”和“发布”。

   ![图像](/help/move-to-cloud-service/content-transfer-tool/assets/12-content-ingestion.png)

1. 完成摄取后，PUBLISH INGESTION字段中的 **状态将更** 新为 **FINISHED**。

   ![图像](/help/move-to-cloud-service/content-transfer-tool/assets/15-ingestion-complete.png)

#### 增补摄取 {#top-up-ingestion-process}

内容传输工具具备支持差异内容&#x200B;*增补*&#x200B;的功能，借助该功能，您可以仅传输自上次内容传输活动以来所做的更改。

>[!NOTE]
>
>初始内容传输完成后，建议在云服务上线之前，经常对差异内容进行增补，以缩短最终差异内容传输的内容冻结期。

完成摄取流程后，可以使用增补摄取方法传输增量内容。应遵循以下步骤：

1. 导航到&#x200B;*概述*&#x200B;页面，然后选择要对其执行增补摄取的迁移集。单击&#x200B;**摄取**&#x200B;以开始增补提取。此时将显示&#x200B;**迁移集摄取**&#x200B;对话框。

   >[!IMPORTANT]
   >
   >您应禁用“在摄 **取之前擦除云实例上的现有内容** ”选项，以防止从以前的摄取活动中删除现有内容。
   >
   >![图像](/help/move-to-cloud-service/content-transfer-tool/assets/16-topup-ingestion.png)

### 查看迁移集的日志 {#viewing-logs-migration-set}

您可以从&#x200B;*概述*&#x200B;页面查看现有迁移集的日志。应遵循以下步骤：

1. 导航到&#x200B;*概述*&#x200B;页面并选择您要删除的迁移集，然后单击操作栏中的&#x200B;**查看日志**。

   ![图像](/help/move-to-cloud-service/content-transfer-tool/assets/view-log1.png)

1. 此时将显示&#x200B;**日志**&#x200B;对话框。单击&#x200B;**提取日志**，以在新选项卡中查看日志。

   ![图像](/help/move-to-cloud-service/content-transfer-tool/assets/view-log2.png)
或者，

   您还可以从&#x200B;*概述*&#x200B;屏幕上查看迁移集的日志。选择迁移集，然后单击&#x200B;**提取**&#x200B;字段下的状态。在此例中，单击&#x200B;**已完成**&#x200B;以在新选项卡中查看日志。

   ![图像](/help/move-to-cloud-service/content-transfer-tool/assets/view-log3.png)

1. 要在不使用用户界面的情况下跟踪日志，您可以通过 SSH 连接到源 AEM 环境并跟踪 `crx-quickstart/cloud-migration/extraction-XXXXX/output.log file`。

### 删除迁移集 {#deleting-migration-set}

您可以从&#x200B;*概述*&#x200B;页面删除迁移集。应遵循以下步骤：

1. 导航到&#x200B;*概述*&#x200B;页面并选择您要删除的迁移集，然后单击操作栏中的&#x200B;**删除**。

   ![图像](/help/move-to-cloud-service/content-transfer-tool/assets/delete-1.png)

1. 单击&#x200B;**删除迁移集**&#x200B;对话框中的&#x200B;**删除**&#x200B;以确认删除。

   ![图像](/help/move-to-cloud-service/content-transfer-tool/assets/delete-3.png)

## 疑难解答 {#troubleshooting}

### 缺少 Blob ID {#missing-blobs}

如果报告缺少的 Blob ID（如下所述），则表明需要在现有存储库中执行一致性检查并还原缺少的 Blob。
`ERROR o.a.j.o.p.b.AbstractSharedCachingDataStore - Error retrieving record [ba45c53f8b687e7056c85dceebf8156a0e6abc7e]`

执行以下命令

>[!NOTE]
>
>`--verbose`标记在报告从中引用 Blob 的节点路径时需要使用。

**对于存储库 AEM 6.5（Oak 1.8 及更低版本）**

```shell
java -jar oak-run.jar datastorecheck --consistency --store [<SEGMENT_STORE_PATH>|<MONGO_URI>] --[s3ds|fds] <DATASTORE_CFG> --verbose <OUT_DIR> --dump
```

**对于拥有 Oak 1.10 以上版本的存储库**

```shell
java -jar oak-run.jar datastore --check-consistency [<SEGMENT_STORE_PATH>|<MONGO_URI>] --[s3ds|fds|azureds] <DATASTORE_CFG> --out-dir <OUT_DIR> --work-dir <TEMP_DIR> --verbose
```

有关更多详细信息，请参阅 [Oak Runnable Jar](https://github.com/apache/jackrabbit-oak/tree/trunk/oak-run)。

可以检查在上述指定 *OUT_DIR* 中为保持一致性而创建的文件是否存在缺少二进制文件的路径，以及是否执行了相应操作，例如从备份中还原、删除路径、重建索引等。

### UI 行为 {#ui-behavior}

作为用户，您可能会在内容传输工具的用户界面 (UI) 中看到以下行为更改：

* 用户为作者 URL（开发/暂存/生产）创建迁移集，并成功执行提取和摄取。

* 然后，用户为同一作者 URL 创建新的迁移集，并对新迁移集执行提取和摄取。UI 显示第一个迁移集的摄取状态更改为&#x200B;**失败**，并且没有日志可用。

* 这并不意味着第一个迁移集的摄取失败。出现此行为是因为启动新的摄取作业时，会删除以前的摄取作业。因此，应该忽略第一个迁移集上的更改状态。

* 内容传输工具 UI 中的图标可能与本指南中显示的屏幕截图有所不同，也可能根本不显示，这取决于源 AEM 实例的版本。


