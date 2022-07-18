---
title: 将内容提取到目标
description: 将内容提取到目标
exl-id: d8c81152-f05c-46a9-8dd6-842e5232b45e
source-git-commit: 0a5b74427bedfa7b1e802a91632b0765adfb8248
workflow-type: tm+mt
source-wordcount: '908'
ht-degree: 13%

---

# 将内容提取到目标 {#ingesting-content}

## 内容传输工具中的摄取流程 {#ingestion-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion"
>title="内容摄取"
>abstract="摄取是指将内容从迁移集摄取到目标Cloud Service实例。 内容传输工具具备支持差异内容增补的功能，借助该功能，您可以仅传输自上次内容传输活动以来所做的更改。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#top-up-ingestion-process" text="增补摄取"

请按照以下步骤从内容传输工具中摄取迁移集：
>[!NOTE]
>您可以运行可选的预复制步骤以显着加快摄取阶段。 预复制步骤对于第1次完全提取和摄取最有效。 请参阅 [使用AzCopy摄取](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md#ingesting-azcopy) 以了解更多详细信息。

1. 转到Cloud Acceleration Manager。 单击您的项目卡片，然后单击内容传输卡片。 导航到 **摄取作业** 单击 **新摄取**

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-01.png)

1. 提供创建新摄取所需的信息。

   * 选择您刚才提取的迁移集作为源
   * 选择目标环境。 这是将摄取迁移集内容的位置。 选择层。 （创作/发布）。

   >[!NOTE]
   >
   >如果源是“作者”，则建议将其摄取到目标上的“创作”层。 同样，如果源为“发布”，则目标也应为“发布”。

   >[!NOTE]
   >
   >您可以运行可选的预复制步骤以显着加快摄取阶段。 请参阅 [使用AzCopy摄取](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md#ingesting-azcopy) 以了解更多详细信息。
   > 
   >如果使用带有预复制的摄取（对于S3或Azure数据存储），则建议先运行创作摄取。 这将在稍后运行发布摄取时加快其速度。

   >[!IMPORTANT]
   >
   >仅当您属于本地环境时，才能将摄取启动到目标环境 **AEM管理员** 目标Cloud Service创作服务上的组。 如果您无法启动摄取，请参阅 [无法启动摄取](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#unable-to-start-ingestion) 以了解更多详细信息。

   >[!IMPORTANT]
   >
   >如果设置 **划出** 在摄取之前启用，它会删除整个现有存储库并创建新存储库以将内容摄取到中。 这意味着它会重置所有设置，包括目标Cloud Service实例的权限。 对于添加到 **管理员** 群组。 您需要重新添加到管理员组才能开始摄取。

1. 单击 **摄取**

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam22.png)

1. 然后，您可以从摄取作业列表视图中监控摄取阶段

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
   
   Also, refer to [Important Considerations for Using Content Transfer Tool](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html?lang=en#important-considerations) to learn more.

1. Once the ingestion is complete, the status under **Author ingestion** updates to **FINISHED**.

   ![image](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-05.png) -->

## 增补摄取 {#top-up-ingestion-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion_topup" title="Top Up Ingestion"
>abstract="使用增补功能移动自上次内容传输活动以来修改的内容。 完成摄取后，检查日志中是否存在任何错误/警告。 任何错误都应立即通过处理报告的问题或联系Adobe客户关怀团队来解决。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/viewing-logs.html?lang=en" text="查看日志"

内容传输工具具备支持差异内容&#x200B;*增补*&#x200B;的功能，借助该功能，您可以仅传输自上次内容传输活动以来所做的更改。

>[!NOTE]
>初始内容传输完成后，建议在云服务上线之前，经常对差异内容进行增补，以缩短最终差异内容传输的内容冻结期。如果您已对第一个完整摄取使用了预复制步骤，则可以跳过对后续增补摄取的预复制步骤（如果增补迁移集大小小于200GB），因为这可能会为整个过程添加时间。

完成摄取流程后，要摄取增量内容，您需要运行 [增补提取](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process) 然后使用增补摄取方法。

为此，您可以创建新的摄取作业，并确保 **划出** 在摄取阶段被禁用，如下所示：

![图像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam24.png)

## 疑难解答 {#troubleshooting}

### CAM无法检索迁移令牌 {#cam-unable-to-retrieve-the-migration-token}

自动检索迁移令牌可能会因不同的原因（包括您）而失败 [通过Cloud Manager设置IP允许列表](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) (在目标Cloud Service环境中)。  在这些情况下，当您尝试启动摄取时，您将看到以下对话框：

![图像](/help/journey-migration/content-transfer-tool/assets-ctt/troubleshooting-token.png)

您将需要通过单击对话框中的“获取令牌”链接来手动检索迁移令牌。 这将打开另一个显示令牌的选项卡。 然后，您可以复制令牌并将其粘贴到 **迁移令牌输入** 字段。 现在，您应该能够开始摄取。

>[!NOTE]
>
>令牌将可供属于本地用户的用户使用 **AEM管理员** 目标Cloud Service创作服务上的组。

### 无法启动摄取 {#unable-to-start-ingestion}

仅当您属于本地环境时，才能将摄取启动到目标环境 **AEM管理员** 目标Cloud Service创作服务上的组。 如果您不属于AEM管理员组，则在尝试开始摄取时，您将看到如下所示的错误。 您可以要求管理员将您添加到本地 **AEM管理员** 或请求令牌本身，然后您可以将该令牌粘贴到 **迁移令牌输入** 字段。

![图像](/help/journey-migration/content-transfer-tool/assets-ctt/error_nonadmin_ingestion.png)

## 下一步 {#whats-next}

在内容传输工具中了解将内容摄取到目标后，您便可以在每个步骤（提取和摄取）完成后查看日志并查找错误。 请参阅 [查看迁移集的日志](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/viewing-logs.html?lang=en) 以了解更多。
