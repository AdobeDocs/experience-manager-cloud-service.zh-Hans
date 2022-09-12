---
title: 从源中提取内容
description: 从源中提取内容
exl-id: c5c08c4e-d5c3-4a66-873e-96986e094fd3
source-git-commit: a2e14d73fd6b8138799799c6408a0846224cd8c9
workflow-type: tm+mt
source-wordcount: '765'
ht-degree: 21%

---

# 从源中提取内容 {#extracting-content}

## 内容传输工具中的提取流程 {#extraction-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_extraction"
>title="内容提取"
>abstract="提取是指将内容从源AEM实例提取到称为迁移集的临时区域。 迁移集是 Adobe 提供的云存储区域，用于临时存储源 AEM 实例和云服务 AEM 实例之间的传输内容。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#top-up-extraction-process" text="增补提取"


请按照以下步骤从内容传输工具中提取迁移集：

>[!NOTE]
>如果将Amazon S3、Azure数据存储或文件数据存储用作数据存储类型，则可以运行可选的预复制步骤以显着加快提取阶段。 预复制步骤对于第1次完全提取和摄取最有效。 为此，您需要配置 `azcopy.config` 文件之前，请执行提取。 请参阅 [处理大型内容存储库](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en) 以了解更多详细信息。

>[!IMPORTANT]
>在从源中提取内容之前，应运行用户映射工具。 请参阅 [使用用户映射工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/user-mapping-tool/using-user-mapping-tool.html?lang=en) 以了解更多详细信息。

1. 从中选择迁移集 **内容传输** 向导，单击 **Extract** 开始提取。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam12.png)

   >[!IMPORTANT]
   >
   >确保提取键值有效且未接近其过期时间。 如果提取键值接近过期日期，您可以通过选择迁移集并单击属性来续订提取键值。 单击 **续订**. 这会将您转到Cloud Acceleration Manager，您可以在其中单击 **复制提取键值**. 每次您点击 **复制提取键值**，则会生成一个新的提取键值，其有效期为创建之日起14天。
   >[!图像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam13.png)

1. 此时将显示提取对话框。 单击 **Extract** 开始提取阶段。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam14.png)

   >[!NOTE]
   >您可以选择在提取阶段覆盖暂存容器。 如果 **覆盖暂存容器** 如果禁用，则它可以加快提取速度，以便在内容路径或包含版本设置未更改的情况下进行后续迁移。 但是，如果内容路径或包含版本设置已更改，则 **覆盖暂存容器** 应启用。

   >[!IMPORTANT]
   >如果在从源中提取内容之前尚未对此迁移集运行用户映射，您将看到一条警告，显示用户映射步骤处于待处理状态，如上图所示。 单击 **映射用户** 以运行用户映射工具。

1. 的 **提取** 字段 **正在运行** 状态，指示提取正在进行中。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam15.png)

   您可以单击 **查看进度** 以详细了解正在进行的提取。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam16.png)

   您还可以通过访问内容传输页面来监控从Cloud Acceleration Manager提取阶段的进度。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam17.png)

1. 提取完成后，查看其他列，如 **来源** 和 **路径** 有关通过单击 **...** 然后 **查看详细信息**.

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam18.png)


## 增补提取 {#top-up-extraction-process}

内容传输工具具备支持差异内容增补的功能，借助该功能，您可以仅传输自上次内容传输活动以来所做的更改。

>[!NOTE]
>初始内容传输完成后，建议在云服务上线之前，经常对差异内容进行增补，以缩短最终差异内容传输的内容冻结期。如果您已使用第一次完全提取的预复制步骤，则可以跳过对后续增补提取的预复制步骤（如果增补迁移集大小小于200GB），因为这可能会为整个过程添加时间。
>此外，必须从采用初始提取到运行增补提取时，不要更改现有内容的内容结构。 无法对自初始提取以来结构已更改的内容运行增补。 请确保在迁移过程中限制此操作。

完成提取流程后，可以使用增补提取方法传输增量内容。

应遵循以下步骤：

1. 导航到 **内容传输** 向导，然后选择要对其执行增补提取的迁移集。 单击&#x200B;**提取**&#x200B;以开始增补提取。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam19.png)

1. 的 **迁移集提取** 对话框。单击 **Extract**.

   >[!IMPORTANT]
   >您应该禁用&#x200B;**在提取期间覆盖暂存容器**选项。
   >![图像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam20.png)


## 下一步 {#whats-next}

在内容传输工具中学习了从源提取内容后，您现在便可以学习内容传输工具中的摄取流程。 请参阅 [将内容摄取到目标](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md) 了解如何从内容传输工具中摄取迁移集。
