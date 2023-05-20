---
title: 内容传输工具概述（旧版）
description: 内容传输工具概述
hide: true
hidefromtoc: true
exl-id: dd031580-e9d7-461e-8689-9bc3dbb2121b
source-git-commit: 3c8035e4db5729f58bae29136a32a0b9944d6a2f
workflow-type: tm+mt
source-wordcount: '475'
ht-degree: 70%

---

# 内容传输工具概述（旧版） {#overview-content-transfer-tool}

内容传输工具是 Adobe 开发的一个工具，可用于将现有内容从源 AEM 实例（内部部署或 AMS）移动到目标 AEM Cloud Service 实例。

此工具还会自动传输主体（用户或组）。

## 内容传输工具中的阶段 {#phases-content-transfer-tool}

内容传输有两个相关阶段：

1. **提取**：提取是指将内容从源 AEM 实例提取到称为&#x200B;*迁移集*&#x200B;的临时区域。*迁移集*&#x200B;是 Adobe 提供的云存储区域，用于临时存储源 AEM 实例和云服务 AEM 实例之间的传输内容。

   有关更多详细信息，请参阅[内容传输中的提取流程](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/extracting-content.html)。

   >[!NOTE]
   >在提取階段中執行「使用者對應工具」。 有关更多详细信息，请参阅[使用用户映射工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/legacy-user-mapping-tool/using-user-mapping-tool-legacy.html?lang=en)。

1. **摄取**：摄取是指将内容从&#x200B;*迁移集*&#x200B;摄取到目标云服务实例。

   有关更多详细信息，请参阅[内容传输中的摄取流程](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/ingesting-content.html)。

## 迁移集的属性 {#attributes-migration-set}

迁移集具有以下属性：

* 在内容传输活动期间，一次最多可以创建和维护 10 个迁移集。
* 每个迁移集应具有唯一的名称。
* 如果移轉集閒置超過30天，則會自動刪除。
* 每当您创建迁移集时，它都会与特定环境关联。您只能摄取到同一环境的创作或发布实例中。


内容传输工具具备支持差异内容增补的功能，借助该功能，您可以仅传输自上次内容传输活动以来所做的更改。

>[!NOTE]
>初始内容传输完成后，建议在云服务上线之前，经常对差异内容进行增补，以缩短最终差异内容传输的内容冻结期。

在提取階段，移至 ***加值*** 現有的移轉集， *覆寫* 選項必須停用。 有关更多详细信息，请参阅[增补提取](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/extracting-content.html?lang=en#top-up-extraction-process)。

在摄取阶段，要在当前内容之上应用增量内容，则必须禁用&#x200B;*划出*&#x200B;选项。有关更多详细信息，请参阅[增补摄取](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/ingesting-content.html?lang=en#top-up-ingestion-process)。

## 后续内容 {#whats-next}

在您瞭解內容轉移工具及其概觀後，此工具可用於將現有內容從來源AEM例項（內部部署或AMS）移動到目標AEM Cloud Service例項。 檢閱 [內容轉移工具的先決條件](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/prerequisites-content-transfer-tool.html?lang=en).
