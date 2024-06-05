---
title: 在内容传输工具中删除迁移集
description: 了解如何在内容传输工具中删除迁移集。
exl-id: 7ec1c5ca-bac7-4617-8068-78569d7cb503
feature: Migration
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 8%

---

# 删除迁移集 {#delete-migration-set}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_delete_migrationset"
>title="删除迁移集"
>abstract="了解删除迁移集。"

可以从Cloud Acceleration Manager中删除迁移集。

## 删除迁移集的步骤 {#deleting-migration-set}

要删除迁移集，请执行以下步骤：

1. 导航至Cloud Acceleration Manager中的迁移集列表视图，然后单击三个圆点(**...**)来修改要删除的迁移集。 此 **删除** 操作应可见，如下所示。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/migration-delete1.png)

1. 当您单击 **删除** 您将看到一个用于确认删除操作的对话框。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/migration-delete2.png)

>[!NOTE]
>
>从Cloud Acceleration Manager (CAM)中删除迁移集不会从内容传输工具中删除它。 一旦从CAM中删除迁移集，用户将无法从“内容传输向导”中对该迁移集运行提取。 但是，如果从“内容传输向导”中删除了迁移集，则用户可以重新创建，前提是迁移集在Cloud Acceleration Manager中仍然可用。
>
>要使内容传输工具与Cloud Acceleration Manager保持同步，用户也可以从内容传输工具中删除迁移集。

要从内容传输向导中删除迁移集，请选择迁移集，然后单击 **删除** 在操作栏中。

![图像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam27.png)
