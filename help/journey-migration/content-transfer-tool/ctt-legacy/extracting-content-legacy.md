---
title: 从源中提取内容（旧版）
description: 从源中提取内容
hide: true
hidefromtoc: true
exl-id: 9f43356c-ba51-48bc-97f5-f1f5db81e7f3
source-git-commit: 22bbf15e33ab3d5608dc01ed293bb04b07cb6c8c
workflow-type: tm+mt
source-wordcount: '537'
ht-degree: 36%

---

# 从源中提取内容（旧版） {#extracting-content}

## 内容传输工具中的提取流程 {#extraction-process}

请按照以下步骤从内容传输工具中提取迁移集：
>[!NOTE]
>如果使用Amazon S3或Azure Data Store作为数据存储的类型，则可以运行可选的预复制步骤以显着加快提取阶段。 为此，您需要配置 `azcopy.config` 文件之前，请执行提取。 请参阅 [处理大型内容存储库](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en) 以了解更多详细信息。

>[!IMPORTANT]
>在从源中提取内容之前，应运行用户映射工具。 请参阅 [使用用户映射工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/user-mapping-tool/using-user-mapping-tool.html?lang=en) 以了解更多详细信息。

1. 从中选择迁移集 **内容传输** 向导，单击 **Extract** 开始提取。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/extraction-01.png)

1. 的 **迁移集提取** 对话框，单击 **Extract** 开始提取阶段。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/extraction-02.png)

   >[!NOTE]
   >您可以选择在提取阶段覆盖暂存容器。

   >[!IMPORTANT]
   >如果在从源中提取内容之前尚未对此迁移集运行用户映射，您将看到一条警告，显示“用户映射”步骤处于待处理状态，如下图所示。 单击 **映射用户** 以运行用户映射工具。
   >![图像](/help/journey-migration/content-transfer-tool/assets-ctt/user-mapping-extract.png)

1. 的 **提取** 字段 **正在运行** 状态，指示提取正在进行中。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/extraction-03.png)

   提取完成后，迁移集的状态将更新为&#x200B;**已完成**，而且&#x200B;**信息**&#x200B;字段下会显示一个&#x200B;*纯绿色*&#x200B;的云朵图标。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/extraction-04.png)

   >[!IMPORTANT]
   >UI具有自动重新加载功能，可重新加载 **内容传输** 向导。
   >提取阶段启动后，将创建写锁定并在 *60* 秒后将其释放。因此，如果停止提取，则需要等待一分钟以便释放锁定，之后才能再次开始提取。

## 增补提取 {#top-up-extraction-process}

内容传输工具具备支持差异内容增补的功能，借助该功能，您可以仅传输自上次内容传输活动以来所做的更改。

>[!NOTE]
>初始内容传输完成后，建议在云服务上线之前，经常对差异内容进行增补，以缩短最终差异内容传输的内容冻结期。
>此外，必须从采用初始提取到运行增补提取时，不要更改现有内容的内容结构。 无法对自初始提取以来结构已更改的内容运行增补。 请确保在迁移过程中限制此操作。

完成提取流程后，可以使用增补提取方法传输增量内容。

应遵循以下步骤：

1. 导航到 **内容传输** 向导，然后选择要对其执行增补提取的迁移集。 单击&#x200B;**提取**&#x200B;以开始增补提取。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/extraction-05.png)

1. 的 **迁移集提取** 对话框。单击 **Extract**.

   >[!IMPORTANT]
   >您应该禁用&#x200B;**在提取期间覆盖暂存容器**选项。
   >![图像](/help/journey-migration/content-transfer-tool/assets-ctt/extraction-06.png)


## 下一步 {#whats-next}

在内容传输工具中学习了从源提取内容后，您现在便可以学习内容传输工具中的摄取流程。 请参阅 [将内容摄取到目标](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md) 了解如何从内容传输工具中摄取迁移集。
