---
title: 時間軸中的活動資料流
description: 本文說明如何在時間軸上顯示資產的活動記錄。
contentOwner: AG
feature: Asset Reports,Asset Management
role: Admin,User
exl-id: 8dd82c31-f88e-4407-9b6d-c87033d7a823
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 34%

---

# 在活動資料流中檢視資產操作記錄 {#activity-stream-in-timeline}

此功能會在時間軸上顯示資產的活動記錄。 如果您在中執行下列任何資產相關作業 [!DNL Experience Manager Assets]，活動資料流功能會更新時間軸以反映活動。

活動資料流中會記錄下列作業：

* 创建
* 删除
* 下載（包括轉譯）
* 发布
* 取消发布
* 批准
* 拒绝
* 移动

时间轴中显示的活动日志是从 CRX 中的 `/var/audit/com.day.cq.dam/content/dam` 位置获取的，日志文件就存储在该位置。此外，上傳新資產或修改現有資產並簽入時，會記錄時間軸活動 [!DNL Experience Manager] 透過 [Adobe資產連結](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html) 或 [[!DNL Experience Manager] 案頭應用程式](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/release-notes.html).

>[!NOTE]
>
>暫時性工作流程不會顯示在時間軸中，因為沒有為這些工作流程儲存歷史記錄資訊。

若要檢視活動資料流，請在資產上執行一或多個作業、選取資產，然後選擇 **[!UICONTROL 時間表]** 從GlobalNav清單。

<!-- ![timeline-2](assets/timeline-2.png) -->

時間軸會顯示您對資產執行之作業的活動資料流。

<!-- ![activity_stream](assets/activity_stream.png) -->

>[!NOTE]
>
>**[!UICONTROL 发布]**&#x200B;和&#x200B;**[!UICONTROL 取消发布]**&#x200B;任务的默认日志存储位置为 `/var/audit/com.day.cq.replication/content`。对于&#x200B;**[!UICONTROL 移动]**&#x200B;任务，默认位置为 `/var/audit/com.day.cq.wcm.core.page`。

**另请参阅**

* [翻译资源](translate-assets.md)
* [Assets HTTP API](mac-api-assets.md)
* [资源支持的文件格式](file-format-support.md)
* [搜索资源](search-assets.md)
* [连接的资源](use-assets-across-connected-assets-instances.md)
* [资源报告](asset-reports.md)
* [元数据架构](metadata-schemas.md)
* [下载资源](download-assets-from-aem.md)
* [管理元数据](manage-metadata.md)
* [搜索 Facet](search-facets.md)
* [管理收藏集](manage-collections.md)
* [批量元数据导入](metadata-import-export.md)
