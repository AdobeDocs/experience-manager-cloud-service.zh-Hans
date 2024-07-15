---
title: 从源中提取内容
description: 了解如何从源Adobe Experience Manager (AEM)实例提取内容，以便稍后将其传输到Cloud ServiceAEM实例。
exl-id: c5c08c4e-d5c3-4a66-873e-96986e094fd3
feature: Migration
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '728'
ht-degree: 19%

---

# 从源中提取内容 {#extracting-content}

## 内容转移工具中的提取流程 {#extraction-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_extraction"
>title="内容提取"
>abstract="提取是指将内容从源 Adobe Experience Manager (AEM) 实例提取到称为迁移集的临时区域。迁移集是 Adobe 提供的一个云存储区域，用于临时存储在存储源 AEM 实例与云服务 AEM 实例之间转移的内容。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=zh-Hans#top-up-extraction-process" text="增补提取"


请按照以下步骤从内容传输工具中提取迁移集：

>[!NOTE]
>如果使用Amazon S3、Azure数据存储或文件数据存储作为数据存储类型，则可以运行可选的预复制步骤以提高提取阶段的速度。 预复制步骤对首次完全提取和摄取最有效。 有关详细信息，请参阅[处理大型内容存储库](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md)。

1. 从&#x200B;**内容传输**&#x200B;向导中选择一个迁移集，然后单击&#x200B;**提取**&#x200B;开始提取。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam12.png)

   >[!TIP]
   >现在，提取成功后，可以将摄取计划为立即自动开始。 有关详细信息，请参阅[将内容摄取到Target](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md)。

   >[!IMPORTANT]
   >
   >确保提取密钥有效并且不在到期之前。 如果密钥即将到期，您可以通过选择迁移集并单击属性来续订提取密钥。 单击&#x200B;**续订**。 这会将您转到Cloud Acceleration Manager，您可以在其中单击&#x200B;**复制提取密钥**。 每次单击&#x200B;**复制提取密钥**时，都会生成一个新的提取密钥，该密钥自创建之日起有效14天。
   >![图像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam13.png)

1. 此时会显示“提取”对话框。 单击&#x200B;**提取**&#x200B;开始提取阶段。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam14b.png)

   >[!NOTE]
   >您可以选择在提取阶段覆盖暂存容器。 如果禁用&#x200B;**覆盖暂存容器**，它可以加快内容路径或包含版本设置未更改的后续迁移的提取。 但是，如果内容路径或包含版本设置已更改，则应启用&#x200B;**覆盖暂存容器**。

1. **提取**&#x200B;字段现在显示&#x200B;**正在运行**&#x200B;状态以指示提取正在进行。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam15.png)

   您可以单击&#x200B;**查看进度**&#x200B;以获取正在进行的提取的粒度视图。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam16.png)

   您还可以通过访问“内容传输”页面从Cloud Acceleration Manager中监视提取阶段进度，并通过单击&#x200B;**...** > **查看详细信息**&#x200B;查看详细信息。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam17.png)

1. 提取完成时，请查看其他列(如&#x200B;**Source**&#x200B;和&#x200B;**路径**)以了解您填充的迁移集的详细信息。 单击&#x200B;**...** > **查看详细信息**&#x200B;以查看详细信息，包括提取每个步骤的持续时间。 在提取期间查看此对话框，以便您能够查看步骤的进展情况。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam18b.png)


## 增补提取 {#top-up-extraction-process}

内容传输工具具备支持差异内容增补的功能，借助该功能，您可以仅传输自上次内容传输活动以来所做的更改。

>[!NOTE]
>初始内容传输后，建议在Cloud Service上线之前，经常对差异内容进行增补，以缩短最终差异内容传输的内容冻结期。 如果您对第一次完整提取使用了预复制步骤，则可以跳过预复制以用于后续增补提取（如果增补迁移集大小小于200 GB）。 原因是它可能会增加整个过程的时间。
>此外，现有内容的内容结构不应从初次提取时更改为运行增补提取时。 无法对自初始提取以来结构已更改的内容运行增补。 确保在迁移过程中对此进行限制。

提取过程完成后，可以使用增补提取方法传输增量内容。

应遵循以下步骤：

1. 导航到&#x200B;**内容传输**&#x200B;向导，并选择要对其执行增补提取的迁移集。 单击&#x200B;**提取**&#x200B;以开始增补提取。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam19.png)

1. 此时将显示&#x200B;**迁移集提取**&#x200B;对话框。 单击&#x200B;**提取**。

   >[!IMPORTANT]
   >您应该禁用&#x200B;**在提取期间覆盖暂存容器**选项。
   >![图像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam20.png)


## 后续内容 {#whats-next}

在内容传输工具中学习了从Source提取内容后，您现在可以在内容传输工具中学习摄取流程。 请参阅[将内容摄取到Target](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md)，了解如何从内容传输工具中摄取迁移集。
