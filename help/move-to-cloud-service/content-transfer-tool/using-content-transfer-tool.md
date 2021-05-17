---
title: 使用内容传输工具
description: 使用内容传输工具
exl-id: a19b8424-33ab-488a-91b3-47f0d3c8abf5
source-git-commit: 9fdc139f5a945de931a2bebb95e5ea006e5b91be
workflow-type: tm+mt
source-wordcount: '2762'
ht-degree: 43%

---

# 使用内容传输工具 {#using-content-transfer-tool}

## 使用内容传输工具的重要注意事项 {#pre-reqs}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_prereqs"
>title="使用内容传输工具的重要注意事项"
>abstract="查看使用内容传输工具的重要注意事项，包括Java和AEM版本、支持的数据存储类型、用户组注意事项等。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?lang=en#best-practices" text="最佳实践和准则"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#availability" text="下载内容传输工具"

请阅读以下章节，以了解运行内容传输工具时的重要注意事项：

* 内容传输工具的最低系统要求为 AEM 6.3 + 和 JAVA 8。如果您使用的是较低的AEM版本，则需要将内容存储库升级到AEM 6.5才能使用内容传输工具。

* 必须在AEM环境上配置Java，这样`java`命令就可以由开始AEM的用户执行。

* 在安装版本1.3.0时，建议卸载旧版内容传输工具，因为该工具在体系结构上发生了重大更改。 对于1.3.0，您还应创建新的迁移集，并重新运行新迁移集的提取和摄取。

* 内容传输工具可用于以下类型的数据存储：文件数据存储、S3数据存储、共享的S3数据存储和Azure Blob存储数据存储。

* 如果您使用&#x200B;*沙箱环境*，请确保环境为最新版本并升级到最新版本。 如果您使用的是“生产环境”**，则会自动更新。

* 要使用内容传输工具，您必须是源实例上的管理员用户，并且属于要将内容传输到的Cloud Service实例中的本地AEM **administrators**&#x200B;组。 无特权的用户将无法检索访问令牌，进而无法使用内容传输工具。

* 如果启用设置&#x200B;**在ingestion**&#x200B;之前擦除Cloud实例上的现有内容，则会删除整个现有存储库并创建新存储库以将内容收录到其中。 这意味着它会重置所有设置，包括目标Cloud Service实例的权限。 对于添加到&#x200B;**administrators**&#x200B;组的管理员用户，也是如此。 必须将用户重新添加到&#x200B;**administrators**&#x200B;组，以检索CTT的访问令牌。

* 访问令牌可以在特定时间段后或Cloud Service环境升级后定期过期。 如果访问令牌已过期，您将无法连接到Cloud Service实例，您需要检索新访问令牌。 与现有迁移集关联的状态图标将更改为红色云，并且当您将鼠标悬停在该云上方时，将显示一条消息。

* 内容传输工具(CTT)在将内容从源实例传输到目标实例之前不执行任何类型的内容分析。 例如，在将内容引入发布环境时，CTT不区分已发布和未发布的内容。 迁移集中指定的任何内容都将被引入所选的目标实例。 用户可以将迁移集引入Author实例或Publish实例中，或同时引入两者。 建议在将内容移到生产实例时，在源Author实例上安装CTT以将内容移到目标 Author实例，同样，在源Publish实例上安装CTT以将内容移到目标 Publish实例。

* 由内容传输工具传输的用户和用户组只是内容满足权限要求的用户和用户组。 *提取*&#x200B;进程将整个`/home`复制到迁移集中，而&#x200B;*Ingestion*&#x200B;进程将复制迁移内容ACL中引用的所有用户和组。 要自动将现有用户和用户组映射到其IMS ID，请参阅[使用用户映射工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#cloud-migration)。

* 在提取阶段，内容传输工具将在活动 AEM 源实例上执行。

* 在完成内容传输过程的&#x200B;*提取*&#x200B;阶段后，并在开始&#x200B;*摄取阶段*&#x200B;将内容作为Cloud Service *阶段*&#x200B;或&#x200B;*生产*&#x200B;实例引入AEM之前，您需要记录支持票证以通知Adobe您打算运行&#x200B;*Ingestion*，以便Adobe可确保在&#x200B;*Ingestion*&#x200B;过程中不发生中断。 您需要在计划的&#x200B;*Ingestion*&#x200B;日期之前1周记录支持票证。 一旦您提交了支持票证，支持团队将提供后续步骤的指导。
   * 使用以下详细信息记录支持票证：
      * 计划开始&#x200B;*摄取*&#x200B;阶段时，确切日期和估计时间（与时区一起）。
      * 环境类型（舞台或生产），您计划将数据引入其中。
      * 项目ID。

* 作者的&#x200B;*摄取阶段*&#x200B;将缩小整个作者部署。 这意味着作者 AEM 在整个摄取过程中将不可用。另外，请确保在运行&#x200B;*Ingestion*&#x200B;阶段时未执行Cloud Manager管道。

* 当将`Amazon S3`或`Azure`用作源AEM系统上的数据存储时，应配置数据存储，以便无法删除存储的块（垃圾回收）。 这确保了索引数据的完整性，并且未能配置这种方式可能会导致提取失败，因为此索引数据缺乏完整性。

* 如果使用自定义索引，则必须确保在运行内容传输工具之前使用`tika`节点配置自定义索引。 有关详细信息，请参阅[准备新索引定义](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=en#preparing-the-new-index-definition)。

## 可用性 {#availability}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_download"
>title="下载"
>abstract="内容传输工具可从软件分发门户下载为zip文件。 您可以通过包管理器在源 Adobe Experience Manager (AEM) 实例上安装该包。确保下载最新版本。"
>additional-url="https://docs.adobe.com/content/help/en/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html" text="发行说明"
>additional-url="https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html" text="软件分发门户"

内容传输工具可从软件分发门户下载为zip文件。 您可以通过包管理器在源 Adobe Experience Manager (AEM) 实例上安装该包。确保下载最新版本。 有关最新版本的详细信息，请参阅[发行说明](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html)。

>[!NOTE]
>从[软件分发](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)门户下载内容传输工具。

## 运行内容传输工具 {#running-tool}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_demo"
>title="运行内容传输工具"
>abstract="了解如何使用内容传输工具将内容作为Cloud Service（作者/发布）迁移到AEM。"
>additional-url="https://video.tv.adobe.com/v/35460/?quality=12&amp;learn=on" text=" 请参阅演示"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/migration/content-transfer-tool.html?lang=en#migration" text="教程 — 使用内容传输工具"

>[!VIDEO](https://video.tv.adobe.com/v/35460/?quality=12&learn=on)


请阅读以下章节，了解如何使用内容传输工具将内容迁移至 AEM as a Cloud Service （创作/发布）：

1. 选择Adobe Experience Manager并导航到工具 — > **Operations** -> **内容迁移**。

   ![图像](/help/move-to-cloud-service/content-transfer-tool/assets/ctt-entry-card01.png)

1. 从&#x200B;**内容迁移**&#x200B;向导中选择&#x200B;**内容传输**&#x200B;选项。

   ![图像](/help/move-to-cloud-service/content-transfer-tool/assets/ctt-entry-card02.png)


1. 创建第一个迁移集时将显示以下控制台。 单击&#x200B;**创建迁移集**&#x200B;以创建新的迁移集。

   ![图像](/help/move-to-cloud-service/content-transfer-tool/assets/01-create-migrationset.png)


   >[!NOTE]
   >如果您有现有的迁移集，控制台将显示现有迁移集的列表及其当前状态。

   此外，单击&#x200B;**创建用户映射配置**&#x200B;可访问[用户映射工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#using-user-mapping-tool)。

1. 按如下所述填充&#x200B;**创建迁移集**&#x200B;屏幕中的字段。

   ![图像](/help/move-to-cloud-service/content-transfer-tool/assets/migration-set-creation-04.png)

   1. **名称**：输入迁移集的名称。
      >[!NOTE]
      >迁移集名称不允许使用特殊字符。

   1. **Cloud Service 配置**：输入目标 AEM as a Cloud Service 作者 URL。

      >[!NOTE]
      >在内容传输活动期间，您一次最多可以创建和维护四个迁移集。
      >此外，您还必须为每个特定的环境（*暂存*、*开发*&#x200B;或&#x200B;*生产*）单独创建迁移。

   1. **访问令牌**：输入访问令牌。

      >[!NOTE]
      >可以使用&#x200B;**打开访问令牌**&#x200B;按钮检索访问令牌。 您需要确保您属于目标 Cloud Service实例中的AEM管理员组。

   1. **参数**：选择以下参数以创建迁移集：

      1. **包含版本**：根据需要选择。

      1. **包括来自IMS用户和组的映射**:选择选项以包括来自IMS用户和组的映射。有关详细信息，请参阅[用户映射工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html)。

      1. **要包含的路径**：使用路径浏览器选择需要迁移的路径。路径选取器通过键入或选择接受输入。

         >[!IMPORTANT]
         >创建迁移集时，以下路径受到限制：
         >* `/apps`
         >* `/libs`
         >* `/home`
         >* `/etc` (允 `/etc` 许在CTT中选择某些路径)


1. 在&#x200B;**创建迁移集**&#x200B;详细信息屏幕中填充所有字段后，单击&#x200B;**保存**。

1. 您将在&#x200B;*概述*&#x200B;页面中查看迁移集。

   ![图像](/help/move-to-cloud-service/content-transfer-tool/assets/04-item-selection-and-quick-actions.png)

   此屏幕上的所有现有迁移集都会显示在&#x200B;*概述*&#x200B;页面上，并显示其当前状态和状态信息。 您可能会看到下面介绍的一些图标。

   * *红色云*&#x200B;表示您无法完成提取流程。
   * *绿色云*&#x200B;表示您可以完成提取过程。
   * *黄色图标*&#x200B;表示您没有创建现有迁移集，而特定迁移集是由同一实例中的其他用户创建的。

1. 从“概述”页面中选择一个迁移集，然后单击&#x200B;**属性**&#x200B;以查看或编辑迁移集属性。编辑属性时，无法更改容器名称或服务URL。


### 内容传输中的提取流程 {#extraction-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_extraction"
>title="内容提取"
>abstract="提取是指将源AEM实例中的内容提取到称为迁移集的临时区域。 迁移集是 Adobe 提供的云存储区域，用于临时存储源 AEM 实例和云服务 AEM 实例之间的传输内容。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#ingestion-process" text="摄取过程"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#top-up-extraction-process" text="自上而上提取"

请按照以下步骤从内容传输工具中提取迁移集：

1. 从&#x200B;*概述*&#x200B;页面中选择一个迁移集，然后单击&#x200B;**提取**&#x200B;以开始提取。将显示&#x200B;**迁移集提取**&#x200B;对话框，并单击&#x200B;**Extract**&#x200B;以开始提取阶段。

   ![图像](/help/move-to-cloud-service/content-transfer-tool/assets/06-content-extraction.png)

   >[!NOTE]
   >您可以选择在提取阶段覆盖暂存容器。


1. **提取**&#x200B;字段现在显示&#x200B;**RUNNING**&#x200B;状态，以指示提取正在进行中。

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

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion"
>title="内容摄取"
>abstract="Ingestion是指将内容从&#x200B;*迁移集*&#x200B;引入目标Cloud Service实例。 内容传输工具具备支持差异内容增补的功能，借助该功能，您可以仅传输自上次内容传输活动以来所做的更改。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#extraction-process" text="提取流程"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#top-up-ingestion-process" text="增补摄取"

请按照以下步骤从内容传输工具中摄取迁移集：

1. 从&#x200B;*概述*&#x200B;页面中选择一个迁移集，然后单击&#x200B;**摄取**&#x200B;以开始提取。此时将显示&#x200B;**迁移集摄取**&#x200B;对话框。单击&#x200B;**收录**&#x200B;以开始摄取阶段。 否则其会将内容同时摄取到“创作”和“发布”。

   >[!IMPORTANT]
   >启用“在摄取&#x200B;**之前擦除Cloud实例上的现有内容”选项后，将删除整个现有存储库并创建新存储库以将内容摄取到其中。**&#x200B;这意味着它会重置所有设置，包括目标Cloud Service实例的权限。 对于添加到&#x200B;**administrators**&#x200B;组的管理员用户，也是如此。

   ![图像](/help/move-to-cloud-service/content-transfer-tool/assets/content-ingestion-01.png)

   此外，单击&#x200B;**客户关怀**&#x200B;可记录票证，如上图所示。 另外，请参阅[使用内容传输工具的重要注意事项](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#pre-reqs)以了解更多信息。

1. 完成摄取后，**PUBLISH INGESTION**&#x200B;字段中的状态将更新为&#x200B;**FINISHED**。

   ![图像](/help/move-to-cloud-service/content-transfer-tool/assets/15-ingestion-complete.png)

#### 增补摄取 {#top-up-ingestion-process}

内容传输工具具备支持差异内容&#x200B;*增补*&#x200B;的功能，借助该功能，您可以仅传输自上次内容传输活动以来所做的更改。

>[!NOTE]
>
>初始内容传输完成后，建议在云服务上线之前，经常对差异内容进行增补，以缩短最终差异内容传输的内容冻结期。

完成摄取流程后，可以使用增补摄取方法传输增量内容。应遵循以下步骤：

1. 导航到&#x200B;*概述*&#x200B;页面，然后选择要对其执行增补摄取的迁移集。单击&#x200B;**摄取**&#x200B;以开始增补提取。此时将显示&#x200B;**迁移集摄取**&#x200B;对话框。

   ![图像](/help/move-to-cloud-service/content-transfer-tool/assets/content-ingestion-01.png)

   >[!IMPORTANT]
   >您应禁用“在摄取&#x200B;**之前擦除Cloud实例上的现有内容”选项，以防止从以前的摄取活动中删除现有内容。**&#x200B;此外，单击&#x200B;**客户关怀**&#x200B;可记录票证，如上图所示。


### 查看迁移集的日志 {#viewing-logs-migration-set}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_logs"
>title="查看日志"
>abstract="完成Ingestion的提取后，检查日志中是否有错误/警告。 任何错误都应立即通过处理报告的问题或联系Adobe支持来解决。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#troubleshooting" text="疑难解答"
>additional-url="https://helpx.adobe.com/ca/enterprise/admin-guide.html/ca/enterprise/using/support-for-experience-cloud.ug.html" text="联系Adobe支持"

完成每个步骤(提取和摄取)后，请检查日志并查找错误。  任何错误都应立即通过处理报告的问题或联系Adobe支持来解决。

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

* 内容传输工具 UI 中的图标可能与本指南中显示的屏幕截图有所不同，也可能根本不显示，这取决于源 AEM 实例的版本。
