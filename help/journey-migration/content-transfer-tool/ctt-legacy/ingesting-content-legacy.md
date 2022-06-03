---
title: 将内容摄取到Target（旧版）
description: 将内容提取到目标
hide: true
hidefromtoc: true
source-git-commit: 1fb4d0f2a3b3f9a27f5ab1228ec2d419149e0764
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 27%

---

# 将内容摄取到Target（旧版） {#ingesting-content}

## 内容传输工具中的摄取流程 {#ingestion-process}

请按照以下步骤从内容传输工具中摄取迁移集：
>[!NOTE]
>您可以运行可选的预复制步骤以显着加快摄取阶段。 请参阅 [使用AzCopy摄取](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en#ingesting-azcopy) 以了解更多详细信息。

1. 从中选择迁移集 **内容传输** 页面，单击 **摄取** 开始摄取。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-01.png)

1. 此时将显示&#x200B;**迁移集摄取**&#x200B;对话框。一次可以将内容摄取到创作实例或发布实例。 选择要将内容摄取到的实例。 单击 **摄取** 以启动摄取阶段。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-02.png)

   >[!IMPORTANT]
   >如果使用带有预复制的摄取（对于S3或Azure数据存储），则建议先运行创作摄取。 这将在稍后运行发布摄取时加快其速度。

   >[!IMPORTANT]
   >当 **摄取前擦除云实例上的现有内容** 选项时，它会删除整个现有存储库并创建新存储库以将内容摄取到中。 这意味着它会重置所有设置，包括目标Cloud Service实例的权限。 对于添加到 **管理员** 群组。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-03.png)

   此外，单击 **客户关怀** 记录票证，如下图所示。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-04.png)

   另外，请参阅 [使用内容传输工具的重要注意事项](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html?lang=en#important-considerations) 以了解更多。

1. 完成摄取后， **创作摄取** 更新至 **已完成**.

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-05.png)

## 增补摄取 {#top-up-ingestion-process}

内容传输工具具备支持差异内容&#x200B;*增补*&#x200B;的功能，借助该功能，您可以仅传输自上次内容传输活动以来所做的更改。

>[!NOTE]
>初始内容传输完成后，建议在云服务上线之前，经常对差异内容进行增补，以缩短最终差异内容传输的内容冻结期。

完成摄取流程后，可以使用增补摄取方法传输增量内容。应遵循以下步骤：

1. 导航到 **内容传输** 向导，然后选择要对其执行增补摄取的迁移集。 单击&#x200B;**摄取**&#x200B;以开始增补提取。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/topup-ingest1.png)


1. 此时将显示&#x200B;**迁移集摄取**&#x200B;对话框。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/topup-ingest2.png)

   >[!IMPORTANT]
   >您应该禁用 **摄取前擦除云实例上的现有内容** 选项，以防止从上一个摄取活动中删除现有内容。 此外，单击 **客户关怀** 记录票证，如上图所示。

## 接下来呢？ {#whats-next}

在内容传输工具中了解将内容摄取到目标后，您便可以在每个步骤（提取和摄取）完成后查看日志并查找错误。 请参阅 [查看迁移集的日志](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/viewing-logs.html?lang=en) 以了解更多。
