---
title: 将内容提取到目标
description: 了解如何使用内容传输工具将内容从迁移集摄取到Cloud Service实例中。
exl-id: d8c81152-f05c-46a9-8dd6-842e5232b45e
source-git-commit: f7ffe727ecc7f1331c1c72229a5d7f940070c011
workflow-type: tm+mt
source-wordcount: '1941'
ht-degree: 11%

---

# 将内容提取到目标 {#ingesting-content}

## 内容传输工具中的摄取流程 {#ingestion-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion"
>title="内容引入"
>abstract="引入是指将内容从迁移集引入到目标云服务实例中。内容传输工具具备支持差异内容增补的功能，借助该功能，您可以仅传输自上次内容传输活动以来所做的更改。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=zh-Hans" text="增补摄取"

请按照以下步骤从内容传输工具中摄取迁移集：

>[!NOTE]
>是否记得为此引入记录支持工单？ 请参阅 [使用内容传输工具之前的重要注意事项](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html#important-considerations) 以了解这些注意事项以及其他有助于成功摄取的注意事项。

1. 转到Cloud Acceleration Manager。 单击项目信息卡，然后单击内容传输信息卡。 导航到 **引入作业** 并单击 **新建引入**

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-01.png)

1. 查看摄取核对清单，并确保已完成所有步骤。 要确保成功引入，必须执行以下步骤。 继续到 **下一个** 仅当核对清单完成时执行此步骤。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/Ingestion-checklist.png)

1. 提供创建引入所需的信息。

   * 选择包含提取的数据作为源的迁移集。
      * 迁移集将在长时间不活动后过期，因此预计摄取将在执行提取后不久进行。 审核 [迁移集到期](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/overview-content-transfer-tool.md#migration-set-expiry) 以了解详细信息。
   * 选择目标环境。 在此环境中摄取迁移集的内容。 选择层。 （创作/发布）。 不支持快速开发环境。

   >[!NOTE]
   >以下注释适用于摄取内容：
   > 如果源是“作者”，则建议将其摄取到目标上的“作者”层。 同样，如果源是Publish，则目标也应是Publish。
   > 如果目标层为 `Author`时，创作实例会在摄取期间关闭，并对用户（例如，作者或执行维护的任何人）不可用。 原因是为了保护系统，并防止任何可能丢失或导致引入冲突的更改。 确保您的团队了解此事实。 另请注意，环境在创作引入期间似乎处于休眠状态。
   > 您可以运行可选的预复制步骤，以显着加快摄取阶段。 请参阅 [使用AzCopy引入](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md#ingesting-azcopy) 以了解更多详细信息。
   > 如果使用预复制引入（对于S3或Azure数据存储），建议先单独运行创作引入。 这样做可加快稍后运行的发布引入。
   > 摄取不支持快速开发环境(RDE)目标，即使用户有权访问，摄取也不会显示为可能的目标选择。

   >[!IMPORTANT]
   > 以下重要注意事项适用于摄取内容：
   > 仅当属于本地环境时，才能启动到目标环境的引入 **AEM管理员** Cloud Service创作服务上的组。 如果您无法开始引入，请参阅 [无法开始引入](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#unable-to-start-ingestion) 以了解更多详细信息。
   > 如果设置 **擦除** 在摄取之前启用，它会删除整个现有存储库并创建一个可以将内容摄取到的存储库。 此工作流意味着它会重置所有设置，包括目标Cloud Service实例上的权限。 对于添加到中的管理员用户，此重置也为true **管理员** 组。 必须准备好管理员组才能开始引入。

1. 单击 **摄取**.

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam22.png)

1. 然后，您可以从“摄取作业”列表视图中监视摄取阶段，并在摄取过程中使用摄取的操作菜单查看日志。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam23.png)

1. 单击 **(i)** 按钮，以了解有关摄取作业的详细信息。 您可以通过单击来查看摄取操作在运行或完成时每个步骤的持续时间 **...**，然后单击 **查看持续时间**. 该提取中的信息还显示出来，以实现所摄取的内容。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam23b.png)

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
   
   Also, see [Important Considerations for Using Content Transfer Tool](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html#important-considerations) to learn more.

1. Once the ingestion is complete, the status under **Author ingestion** updates to **FINISHED**.

   ![image](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-05.png) -->

## 增补摄取 {#top-up-ingestion-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion_topup"
>title="增补摄取"
>abstract="使用增补功能移动自上次内容转移活动以来修改的内容。引入完毕后，检查日志中是否有任何错误/警告。应立即通过处理所报告的问题或联系 Adobe 客户服务而纠正任何错误。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/viewing-logs.html?lang=zh-Hans" text="查看日志"

内容传输工具具备支持差异内容&#x200B;*增补*&#x200B;的功能，借助该功能，您可以仅传输自上次内容传输活动以来所做的更改。

>[!NOTE]
>初始内容传输完成后，建议在云服务上线之前，经常对差异内容进行增补，以缩短最终差异内容传输的内容冻结期。如果您对第一次完整摄取使用了预复制步骤，则可以跳过后续增补摄取的预复制（如果增补迁移集大小小于200 GB）。 原因是它可能会增加整个过程的时间。

摄取过程完成后，要摄取增量内容，您必须运行 [增补提取](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process)，然后使用增补摄取方法。

从创建引入作业开始，并确保 **擦除** 在摄取阶段被禁用，如下所示：

![图像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam24.png)

## 疑难解答 {#troubleshooting}

### CAM无法检索迁移令牌 {#cam-unable-to-retrieve-the-migration-token}

自动检索迁移令牌可能会由于各种原因而失败，其中包括您 [通过Cloud Manager设置IP允许列表](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) 在目标Cloud Service环境中。 在这种情况下，当您尝试开始摄取时，您将看到以下对话框：

![图像](/help/journey-migration/content-transfer-tool/assets-ctt/troubleshooting-token.png)

通过单击对话框中的“获取令牌”链接，手动检索迁移令牌。 此时将打开另一个显示令牌的选项卡。 然后，您可以复制令牌并将其粘贴到 **迁移令牌输入** 字段。 现在，您应该能够开始引入。

>[!NOTE]
>
>令牌可供属于本地的用户使用 **AEM管理员** Cloud Service创作服务上的组。

### 无法开始引入 {#unable-to-start-ingestion}

仅当属于本地环境时，才能启动到目标环境的引入 **AEM管理员** Cloud Service创作服务上的组。 如果您不属于AEM管理员组，则在尝试开始引入时会看到如下所示的错误。 您可以请求管理员将您添加到本地 **AEM管理员** 或者询问令牌本身，然后您可以将它粘贴到 **迁移令牌输入** 字段。

![图像](/help/journey-migration/content-transfer-tool/assets-ctt/error_nonadmin_ingestion.png)

### 无法访问迁移服务 {#unable-to-reach-migration-service}

请求引入后，可能会向用户显示如下消息：“无法访问目标环境中的迁移服务。 如果是这样的话，请稍后重试或与Adobe支持人员联系。”

![图像](/help/journey-migration/content-transfer-tool/assets-ctt/error_cannot_reach_migser.png)

此消息表示Cloud Acceleration Manager无法访问目标环境的迁移服务以开始引入。 这种情况可能由于各种原因出现。

>[!NOTE]
> 
> 显示“迁移令牌”字段，因为在某些情况下，实际上不允许检索该令牌。 通过允许手动提供，它可让用户无需任何其他帮助即可快速开始引入。 如果提供了令牌，但仍显示消息，则检索令牌不是问题。

* AEMas a Cloud Service会维护环境状态，有时由于各种正常原因必须重新启动迁移服务。 如果该服务正在重新启动，则无法访问，但最终可用。
* 可能正在实例上运行另一个进程。 例如，如果Release Orchestrator正在应用更新，则系统可能忙碌，并且迁移服务定期不可用。 这以及破坏暂存或生产实例的可能性，因此强烈建议在摄取期间暂停更新。
* 如果 [已应用IP允许列表](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) 它通过Cloud Manager阻止Cloud Acceleration Manager访问迁移服务。 无法为摄取添加IP地址，因为其地址是动态的。 目前，唯一的解决方案是在摄取运行时禁用IP允许列表。
* 可能有其他原因需要调查。 如果摄取仍然失败，请联系Adobe客户关怀部门。

### 通过Release Orchestrator进行的自动更新仍处于启用状态

Release Orchestrator通过自动应用更新来自动使环境保持最新。 如果在执行摄取时触发更新，则可能会导致不可预测的结果，包括环境损坏。 有充分理由在开始引入之前记录客户支持工单（请参阅上面的“注意”），以便可以计划暂时禁用Release Orchestrator。

如果在开始引入时Release Orchestrator仍在运行，则用户界面会显示此消息。 无论如何您都可以选择继续，通过检查字段并再次按按钮来接受风险。

>[!NOTE]
>
> Release Orchestrator现在将部署到开发环境，因此也应该暂停对这些环境的更新。

![图像](/help/journey-migration/content-transfer-tool/assets-ctt/error_releaseorchestrator_ingestion.png)

### 由于违反唯一性约束，增补摄取失败

导致此问题的常见原因 [增补摄取](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#top-up-ingestion-process) 失败是节点ID中的冲突。 要识别此错误，请使用Cloud Acceleration Manager UI下载摄取日志，并查找如下条目：

>java.lang.RuntimeException： org.apache.jackrabbit.oak.api.CommitFailedException： OakConstraint0030：违反了唯一性约束 [jcr：uuid] 值为a1a1a1a1-b2b2-c3c3-d4d4-e5e5e5e5e5： /some/path/jcr：content， /some/other/path/jcr：content

AEM中的每个节点都必须具有一个唯一的uuid。 此错误表示正在摄取的节点与位于目标实例上不同路径的其他位置的节点具有相同的uuid。
如果在提取和后续操作之间在源上移动节点，则可能会发生这种情况 [增补提取](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process).
如果目标上的节点在摄取和后续增补摄取之间移动，也会发生这种情况。

必须手动解决此冲突。 熟悉内容的用户必须确定必须删除这两个节点中的哪个节点，并牢记引用该节点的其他内容。 解决方案可能要求再次执行增补提取而不考虑违规节点。

### 由于无法删除引用的节点，增补摄取失败

导致问题的另一个常见原因 [增补摄取](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#top-up-ingestion-process) 失败是目标实例上特定节点的版本冲突。 要识别此错误，请使用Cloud Acceleration Manager UI下载摄取日志，并查找如下条目：
>java.lang.RuntimeException： org.apache.jackrabbit.oak.api.CommitFailedException： OakIntegrity0001：无法删除引用的节点：8a2289f4-b904-4bd0-8410-15e41e0976a8

如果在摄取和后续增补摄取之间修改了目标上的节点，以便创建了新版本，则可能会发生这种情况。 如果引入启用了“包含版本”，则可能会发生冲突，因为目标现在具有由版本历史记录和其他内容引用的较新版本。 摄取进程将无法删除违规版本节点，因为它已被引用。

解决方案可能要求再次执行增补提取而不考虑违规节点。 或者，创建一个包含违规节点的小型迁移集，但禁用“包含版本”。

最佳实践表明，如果必须使用划出=false和“包含版本”=true来运行引入，则在迁移历程完成之前，必须尽可能少地修改目标上的内容。 否则，可能会发生这些冲突。


## 后续内容 {#whats-next}

完成将内容摄取到Target中后，您可以查看每个步骤（提取和摄取）的日志并查找错误。 请参阅 [查看迁移集的日志](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/viewing-logs.html?lang=zh-Hans) 了解更多信息。
