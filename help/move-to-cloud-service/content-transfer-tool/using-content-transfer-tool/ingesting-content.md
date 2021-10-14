---
title: 将内容摄取到目标
description: 将内容摄取到目标
source-git-commit: 6a6fa69d2eb79e41c79a0916bfd6e34ecf490d34
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 28%

---


# 将内容摄取到目标 {#ingesting-content}

## 内容传输工具中的摄取流程 {#ingestion-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion"
>title="内容摄取"
>abstract="摄取是指将内容从迁移集摄取到目标Cloud Service实例。 内容传输工具具备支持差异内容增补的功能，借助该功能，您可以仅传输自上次内容传输活动以来所做的更改。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#top-up-ingestion-process" text="增补摄取"

请按照以下步骤从内容传输工具中摄取迁移集：
>[!NOTE]
>如果使用Amazon S3或Azure Data Store作为数据存储的类型，则可以运行可选的预复制步骤以显着加快摄取阶段。 有关更多详细信息，请参阅[使用AzCopy摄取](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en#ingesting-azcopy) 。

1. 从&#x200B;**内容传输**&#x200B;页面中选择迁移集，然后单击&#x200B;**摄取**&#x200B;以开始摄取。

   ![图像](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/ingestion-01.png)

1. 此时将显示&#x200B;**迁移集摄取**&#x200B;对话框。一次可以将内容摄取到创作实例或发布实例。 选择要将内容摄取到的实例。 单击&#x200B;**摄取**&#x200B;以开始摄取阶段。

   ![图像](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/ingestion-02.png)

   >[!IMPORTANT]
   >如果使用带有预复制的摄取（对于S3或Azure数据存储），则建议先运行创作摄取。 这将在稍后运行发布摄取时加快其速度。

   >[!IMPORTANT]
   >启用&#x200B;**在摄取**&#x200B;之前擦除云实例上的现有内容选项后，它将删除整个现有存储库并创建新存储库以将内容摄取到中。 这意味着它会重置所有设置，包括目标Cloud Service实例的权限。 对于添加到&#x200B;**administrators**&#x200B;组的管理员用户，也是如此。

   ![图像](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/ingestion-03.png)

   此外，单击&#x200B;**客户关怀**&#x200B;记录票证，如下图所示。

   ![图像](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/ingestion-04.png)

   另请参阅[使用内容传输工具的重要注意事项](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html?lang=en#important-considerations)以了解更多信息。

1. 完成摄取后，位于&#x200B;**创作摄取**&#x200B;下的状态将更新为&#x200B;**已完成**。

   ![图像](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/ingestion-05.png)

## 增补摄取 {#top-up-ingestion-process}

内容传输工具具备支持差异内容&#x200B;*增补*&#x200B;的功能，借助该功能，您可以仅传输自上次内容传输活动以来所做的更改。

>[!NOTE]
>初始内容传输完成后，建议在云服务上线之前，经常对差异内容进行增补，以缩短最终差异内容传输的内容冻结期。

完成摄取流程后，可以使用增补摄取方法传输增量内容。应遵循以下步骤：

1. 导航到&#x200B;**内容传输**&#x200B;向导，然后选择要对其执行增补摄取的迁移集。 单击&#x200B;**摄取**&#x200B;以开始增补提取。

   ![图像](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/topup-ingest1.png)


1. 此时将显示&#x200B;**迁移集摄取**&#x200B;对话框。

   ![图像](/help/move-to-cloud-service/content-transfer-tool/assets-ctt/topup-ingest2.png)

   >[!IMPORTANT]
   >您应该禁用&#x200B;**在摄取**&#x200B;之前擦除云实例上的现有内容选项，以防止从上一个摄取活动中删除现有内容。 此外，单击&#x200B;**客户关怀**&#x200B;记录票证，如上图所示。

## 下一步 {#whats-next}

在内容传输工具中了解将内容摄取到目标后，您便可以在每个步骤（提取和摄取）完成后查看日志并查找错误。 请参阅[查看迁移集的日志](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/viewing-logs.html?lang=en)以了解更多信息。
