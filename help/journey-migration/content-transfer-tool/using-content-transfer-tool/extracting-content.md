---
title: 从源中提取内容
description: 从源中提取内容
exl-id: c5c08c4e-d5c3-4a66-873e-96986e094fd3
source-git-commit: 5a4592531377109fba88b5cdc9df027803feca7a
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 24%

---

# 从源中提取内容 {#extracting-content}

## 内容传输工具中的提取流程 {#extraction-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_extraction"
>title="内容提取"
>abstract="提取是指将内容从源AEM实例提取到称为迁移集的临时区域。 迁移集是 Adobe 提供的云存储区域，用于临时存储源 AEM 实例和云服务 AEM 实例之间的传输内容。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html#top-up-extraction-process" text="增补提取"


请按照以下步骤从内容传输工具中提取迁移集：

>[!NOTE]
>如果使用Amazon S3、Azure数据存储或文件数据存储作为数据存储类型，则可以运行可选的预复制步骤以显着加快提取阶段。 预复制步骤对于第一次完全提取和摄取最有效。 为此，您需要配置 `azcopy.config` 文件（在运行提取之前）。 请参阅 [处理大型内容存储库](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md) 了解更多详细信息。

1. 从中选择一个迁移集 **内容传输** 向导并单击 **Extract** 以开始提取。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam12.png)

   >[!IMPORTANT]
   >
   >确保提取密钥有效并且未接近其到期时间。 如果临近到期日期，您可以通过选择迁移集并单击“属性”来续订提取密钥。 单击 **续订**. 这会将您转到Cloud Acceleration Manager，您可以在其中单击 **复制提取密钥**. 每次单击 **复制提取密钥**，则会生成一个新的提取密钥，该密钥的有效期为自创建之日起14天。
   >![图像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam13.png)

1. 此时将显示提取对话框。 单击 **Extract** 以开始提取阶段。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam14.png)

   >[!NOTE]
   >您可以选择在提取阶段覆盖暂存容器。 如果 **覆盖暂存容器** 禁用。它可以加快内容路径或包含版本设置未更改的后续迁移的提取速度。 但是，如果内容路径或包含版本设置已更改，则 **覆盖暂存容器** 应该启用。

1. 此 **提取** 字段现在显示 **正在运行** 状态，表示提取正在进行中。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam15.png)

   您可以单击 **查看进度** 以获取正在进行的提取的精细视图。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam16.png)

   您还可以通过访问内容传输页面从Cloud Acceleration Manager监控提取阶段进度。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam17.png)

1. 提取完成后，查看其他列，例如 **来源** 和 **路径** 有关通过单击填充的迁移集的详细信息 **...** 然后打开 **查看详细信息**.

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam18.png)


## 增补提取 {#top-up-extraction-process}

内容传输工具具备支持差异内容增补的功能，借助该功能，您可以仅传输自上次内容传输活动以来所做的更改。

>[!NOTE]
>初始内容传输完成后，建议在云服务上线之前，经常对差异内容进行增补，以缩短最终差异内容传输的内容冻结期。如果您已使用预复制步骤进行第一次完整提取，则可以跳过预复制以进行后续增补提取（如果增补迁移集大小小于200 GB），因为它可能会增加整个过程的时间。
>此外，至关重要的是，现有内容的内容结构不应从初次提取时更改为运行增补提取时。 无法对自初始提取以来结构已更改的内容运行增补。 请确保在迁移过程中对此进行限制。

完成提取流程后，可以使用增补提取方法传输增量内容。

应遵循以下步骤：

1. 导航到 **内容传输** 向导并选择您要对其执行增补提取的迁移集。 单击&#x200B;**提取**&#x200B;以开始增补提取。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam19.png)

1. 此 **迁移集提取** 对话框随即显示。单击 **Extract**.

   >[!IMPORTANT]
   >您应该禁用&#x200B;**在提取期间覆盖暂存容器**选项。
   >![图像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam20.png)


## 后续内容 {#whats-next}

在内容传输工具中学习了从源中提取内容后，您现在就可以学习内容传输工具中的摄取过程了。 参见 [将内容引入目标](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md) 以了解如何从内容传输工具摄取迁移集。
