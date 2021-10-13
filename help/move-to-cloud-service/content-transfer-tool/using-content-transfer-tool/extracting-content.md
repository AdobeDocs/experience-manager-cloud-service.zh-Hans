---
title: 在内容传输工具中从源提取内容
description: 在内容传输工具中从源提取内容
source-git-commit: 5b569ab1b1cca7e5ec46b872f8726fddfc8b8d14
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 53%

---


# 在内容传输工具中从源提取内容 {#extracting-content}

## 内容传输工具中的提取流程 {#extraction-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_extraction"
>title="内容提取"
>abstract="提取是指将内容从源AEM实例提取到称为迁移集的临时区域。 迁移集是 Adobe 提供的云存储区域，用于临时存储源 AEM 实例和云服务 AEM 实例之间的传输内容。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#top-up-extraction-process" text="增补提取"

请按照以下步骤从内容传输工具中提取迁移集：
>[!NOTE]
>如果使用Amazon S3或Azure Data Store作为数据存储的类型，则可以运行可选的预复制步骤以显着加快提取阶段。 为此，您需要先配置`azcopy.config`文件，然后再运行提取。 有关更多详细信息，请参阅[处理大内容存储库](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en)。

1. 从&#x200B;*概述*&#x200B;页面中选择一个迁移集，然后单击&#x200B;**提取**&#x200B;以开始提取。此时将显示&#x200B;**迁移集提取**&#x200B;对话框，然后单击&#x200B;**提取**&#x200B;以开始提取阶段。

   ![图像](/help/move-to-cloud-service/content-transfer-tool/assets/06-content-extraction.png)

   >[!NOTE]
   >您可以选择在提取阶段覆盖暂存容器。


1. 现在， **EXTRACTION**&#x200B;字段显示&#x200B;**RUNNING**&#x200B;状态，以指示提取正在进行中。

   ![图像](/help/move-to-cloud-service/content-transfer-tool/assets/07-extraction-job-running.png)

   提取完成后，迁移集的状态将更新为&#x200B;**已完成**，而且&#x200B;**信息**&#x200B;字段下会显示一个&#x200B;*纯绿色*&#x200B;的云朵图标。

   ![图像](/help/move-to-cloud-service/content-transfer-tool/assets/10-extraction-complete.png)

   >[!NOTE]
   >UI具有自动重新加载功能，每30秒重新加载一次概述页面。
   >提取阶段启动后，将创建写锁定并在 *60* 秒后将其释放。因此，如果停止提取，则需要等待一分钟以便释放锁定，之后才能再次开始提取。

## 增补提取 {#top-up-extraction-process}

内容传输工具具备支持差异内容增补的功能，借助该功能，您可以仅传输自上次内容传输活动以来所做的更改。

>[!NOTE]
>初始内容传输完成后，建议在云服务上线之前，经常对差异内容进行增补，以缩短最终差异内容传输的内容冻结期。
>此外，必须从采用初始提取到运行增补提取时，不要更改现有内容的内容结构。 无法对自初始提取以来结构已更改的内容运行增补。 请确保在迁移过程中限制此操作。

完成提取流程后，可以使用增补提取方法传输增量内容。应遵循以下步骤：

1. 导航到&#x200B;*概述*&#x200B;页面，然后选择要对其执行增补提取的迁移集。单击&#x200B;**提取**&#x200B;以开始增补提取。此时将显示&#x200B;**迁移集提取**&#x200B;对话框。

   >[!IMPORTANT]
   >
   >您应该禁用&#x200B;**在提取期间覆盖暂存容器**&#x200B;选项。
   >
   >![图像](/help/move-to-cloud-service/content-transfer-tool/assets/11-topup-extraction.png)
