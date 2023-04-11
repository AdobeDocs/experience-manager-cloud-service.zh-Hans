---
title: 将内容提取到目标
description: 将内容提取到目标
exl-id: d8c81152-f05c-46a9-8dd6-842e5232b45e
source-git-commit: 5475f9995513d09e61bd8f52242b3e74b8d4694c
workflow-type: tm+mt
source-wordcount: '1722'
ht-degree: 11%

---

# 将内容提取到目标 {#ingesting-content}

## 内容传输工具中的摄取流程 {#ingestion-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion"
>title="内容引入"
>abstract="引入是指将内容从迁移集引入到目标云服务实例中。内容传输工具具备支持差异内容增补的功能，借助该功能，您可以仅传输自上次内容传输活动以来所做的更改。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html#top-up-ingestion-process" text="增补摄取"

请按照以下步骤从内容传输工具中摄取迁移集：
>[!NOTE]
>您可以运行可选的预复制步骤以显着加快摄取阶段。 预复制步骤对于第1次完全提取和摄取最有效。 请参阅 [使用AzCopy摄取](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md#ingesting-azcopy) 以了解更多详细信息。

>[!NOTE]
>您是否记得为此摄取记录支持票证？ 请参阅 [使用内容传输工具之前的重要注意事项](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html#important-considerations) 以及帮助成功摄取的其他注意事项。

1. 转到Cloud Acceleration Manager。 单击您的项目卡片，然后单击内容传输卡片。 导航到 **摄取作业** 单击 **新摄取**

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-01.png)


1. 查看摄取检查列表，并确保完成了所有步骤。 这些是确保成功摄取的必要步骤。 您将能够继续 **下一个** 步骤。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/Ingestion-checklist.png)

1. 提供创建新摄取所需的信息。

   * 选择包含提取数据作为源的迁移集。
      * 迁移集将在长时间不活动后过期，因此，执行提取操作后预计摄取会相对较快进行。 审阅 [迁移集到期](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/overview-content-transfer-tool.md#migration-set-expiry) 以了解详细信息。
   * 选择目标环境。 这是将摄取迁移集内容的位置。 选择层。 （创作/发布）。 不支持快速开发环境。

   >[!NOTE]
   >
   >如果源是“作者”，则建议将其摄取到目标上的“创作”层。 同样，如果源为“发布”，则目标也应为“发布”。

   >[!NOTE]
   >
   >如果目标层为 `Author`，则创作实例将在摄取期间关闭，用户（例如，作者或执行维护的任何人员等）将无法使用。 这是为了保护系统，并防止任何可能丢失或导致引入冲突的更改。 请确保您的团队了解这一事实。 另请注意，环境将在创作摄取期间显示休眠。

   >[!NOTE]
   >
   >您可以运行可选的预复制步骤以显着加快摄取阶段。 请参阅 [使用AzCopy摄取](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md#ingesting-azcopy) 以了解更多详细信息。
   > 
   >如果使用带有预复制的摄取（对于S3或Azure数据存储），则建议先运行创作摄取。 这将在稍后运行发布摄取时加快其速度。

   >[!NOTE]
   >
   >摄取不支持快速开发环境(RDE)目标。 即使用户有权访问，它们也不会显示为可能的目标选项。

   >[!IMPORTANT]
   >
   >仅当您属于本地环境时，才能启动对目标环境的摄取 **AEM管理员** 目标Cloud Service创作服务上的组。 如果您无法启动摄取，请参阅 [无法启动摄取](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#unable-to-start-ingestion) 以了解更多详细信息。

   >[!IMPORTANT]
   >
   >如果设置 **划出** 在摄取之前启用，它会删除整个现有存储库并创建新存储库以将内容摄取到中。 这意味着它会重置所有设置，包括目标Cloud Service实例的权限。 对于添加到 **管理员** 群组。 您需要重新添加到管理员组才能开始摄取。

1. 单击 **摄取**

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam22.png)

1. 然后，您可以从摄取作业列表视图中监控摄取阶段，并使用摄取的操作菜单，在摄取进行时查看日志。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam23.png)

1. 完成摄取后，单击屏幕右上角的(i)按钮，以获取有关摄取作业的更多信息。

<!-- Alexandru: hiding temporarily, until it's reviewed 

1. The **Migration Set ingestion** dialog box displays. Content can be ingested to either Author instance or Publish instance at a time. Select the instance to ingest content to. Click on **Ingest** to start the ingestion phase. 

   ![image](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-02.png)

   >[!IMPORTANT]
   >If ingesting with pre-copy is used (for S3 or Azure Data Store), it is recommended to run Author ingestion first alone. This will speed up the Publish ingestion when it is run later. 

   >[!IMPORTANT]
   >When the **Wipe existing content on Cloud instance before ingestion** option is enabled, it deletes the entire existing repository and creates a new repository to ingest content into. This means that it resets all settings including permissions on the target Cloud Service instance. This is also true for an admin user added to the **administrators** group.

   ![image](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-03.png)

   Additionally, click on **Customer Care** to log a ticket, as shown in the figure below. 

   ![image](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-04.png)
   
   Also, refer to [Important Considerations for Using Content Transfer Tool](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html#important-considerations) to learn more.

1. Once the ingestion is complete, the status under **Author ingestion** updates to **FINISHED**.

   ![image](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-05.png) -->

## 增补摄取 {#top-up-ingestion-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion_topup"
>title="增补摄取"
>abstract="使用增补功能移动自上次内容转移活动以来修改的内容。引入完毕后，检查日志中是否有任何错误/警告。应立即通过处理所报告的问题或联系 Adobe 客户服务而纠正任何错误。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/viewing-logs.html" text="查看日志"

内容传输工具具备支持差异内容&#x200B;*增补*&#x200B;的功能，借助该功能，您可以仅传输自上次内容传输活动以来所做的更改。

>[!NOTE]
>初始内容传输完成后，建议在云服务上线之前，经常对差异内容进行增补，以缩短最终差异内容传输的内容冻结期。如果您已对第一个完整摄取使用了预复制步骤，则可以跳过对后续增补摄取的预复制步骤（如果增补迁移集大小小于200GB），因为这可能会为整个过程添加时间。

完成摄取流程后，要摄取增量内容，您需要运行 [增补提取](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process) 然后使用增补摄取方法。

为此，您可以创建新的摄取作业，并确保 **划出** 在摄取阶段被禁用，如下所示：

![图像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam24.png)

## 疑难解答 {#troubleshooting}

### CAM无法检索迁移令牌 {#cam-unable-to-retrieve-the-migration-token}

自动检索迁移令牌可能会因不同的原因（包括您）而失败 [通过Cloud Manager设置IP允许列表](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) (在目标Cloud Service环境中)。 在这些情况下，当您尝试启动摄取时，您将看到以下对话框：

![图像](/help/journey-migration/content-transfer-tool/assets-ctt/troubleshooting-token.png)

您将需要通过单击对话框中的“获取令牌”链接来手动检索迁移令牌。 这将打开另一个显示令牌的选项卡。 然后，您可以复制令牌并将其粘贴到 **迁移令牌输入** 字段。 现在，您应该能够开始摄取。

>[!NOTE]
>
>令牌将可供属于本地用户的用户使用 **AEM管理员** 目标Cloud Service创作服务上的组。

### 无法启动摄取 {#unable-to-start-ingestion}

仅当您属于本地环境时，才能启动对目标环境的摄取 **AEM管理员** 目标Cloud Service创作服务上的组。 如果您不属于AEM管理员组，则在尝试开始摄取时，您将看到如下所示的错误。 您可以要求管理员将您添加到本地 **AEM管理员** 或请求令牌本身，然后您可以将该令牌粘贴到 **迁移令牌输入** 字段。

![图像](/help/journey-migration/content-transfer-tool/assets-ctt/error_nonadmin_ingestion.png)

### 无法访问迁移服务 {#unable-to-reach-migration-service}

在请求获取后，可能会向用户显示如下消息：“目标环境中的迁移服务当前不可访问。 请稍后重试或联系Adobe支持。”

![图像](/help/journey-migration/content-transfer-tool/assets-ctt/error_cannot_reach_migser.png)

这表示Cloud Acceleration Manager无法访问目标环境的迁移服务以开始摄取。 这可能出于多种原因。

>[!NOTE]
> 
> 显示“迁移令牌”字段，因为在少数情况下，检索该令牌实际上是不允许的。 通过允许手动提供，用户可以快速开始摄取，而无需任何其他帮助。 如果提供了令牌，并且仍显示消息，但检索令牌不是问题。

* AEM as a Cloud Service维护环境状态，有时可能由于一些正常原因需要重新启动迁移服务。 如果该服务正在重新启动，则无法访问该服务，但该服务将很快可用。
* 可能正在实例上运行另一个进程。 例如，如果Release Orchestrator正在应用更新，则系统可能正忙，并且迁移服务经常不可用。 这以及损坏暂存或生产实例的可能性，就是强烈建议在摄取期间暂停更新的原因。
* 如果 [已应允许列表用IP](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) 通过Cloud Manager，将阻止Cloud Acceleration Manager访问迁移服务。 无法为摄取添加IP地址，因为其地址非常动态。 目前，唯一的解决方案是在摄取运行时禁用IP允许列表。
* 可能还有其他原因需要调查。 如果摄取仍然失败，请联系Adobe客户关怀团队。

### 仍启用通过Release Orchestrator进行的自动更新

Release Orchestrator通过自动应用更新来自动使环境保持最新。 如果在执行摄取时触发更新，则可能会导致不可预测的结果，包括环境损坏。 这是启动摄取之前应记录支持票证的原因之一（请参阅上面的“注意”），以便可以计划临时禁用Release Orchestrator。

如果启动摄取时Release Orchestrator仍在运行，则UI将显示此消息。 无论如何，您都可以选择继续，接受风险，方法是检查字段并再次按按钮。

![图像](/help/journey-migration/content-transfer-tool/assets-ctt/error_releaseorchestrator_ingestion.png)

### 增补摄取失败

一个 [增补摄取](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#top-up-ingestion-process) 失败是节点id中的冲突。 要识别此错误，请使用Cloud Acceleration Manager UI下载摄取日志，并查找如下条目：

>java.lang.RuntimeException:org.apache.jackrabbit.oak.api.CommitFailedException:OakConstraint0030:唯一性约束违反属性 [jcr:uuid] 具有值a1a1a1-b2b2-c3c3-d4d4-e5e5e5e5e5e5e5:/some/path/jcr:content， /some/other/path/jcr:content

AEM中的每个节点必须具有唯一的uuid。 此错误表示正在摄取的节点具有与目标实例上其他路径中已存在的节点相同的uuid。
如果在提取和后续操作之间在源上移动节点，则可能会发生这种情况 [增补提取](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process).
如果目标上的节点在摄取和后续增补摄取之间移动，则也可能会发生这种情况。

必须手动解决此冲突。 熟悉内容的人员必须决定必须删除这两个节点中的哪一个，同时要记住引用该节点的其他内容。 该解决方案可能要求在没有违规节点的情况下再次进行增补提取。

## 后续内容 {#whats-next}

完成将内容摄取到Target后，您可以查看每个步骤（提取和摄取）的日志并查找错误。 请参阅 [查看迁移集的日志](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/viewing-logs.html) 以了解更多。
