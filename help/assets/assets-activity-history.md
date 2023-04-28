---
title: 时间轴中的活动流
description: 本文介绍了如何在时间轴上显示资产的活动日志。
contentOwner: AG
feature: Asset Reports,Asset Management
role: Admin,User
exl-id: 8dd82c31-f88e-4407-9b6d-c87033d7a823
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 29%

---

# 在活动流中查看资产操作日志 {#activity-stream-in-timeline}

此功能可在时间轴上显示资产的活动日志。 如果您在 [!DNL Experience Manager Assets]，活动流功能会更新时间轴以反映活动。

活动流中记录以下操作：

* 创建
* 删除
* 下载（包括演绎版）
* 发布
* 取消发布
* 批准
* 拒绝
* 移动

时间轴中显示的活动日志是从 CRX 中的 `/var/audit/com.day.cq.dam/content/dam` 位置获取的，日志文件就存储在该位置。此外，当上传新资产或修改现有资产并签入时，会记录时间轴活动 [!DNL Experience Manager] 通过 [Adobe资产链接](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html) 或 [[!DNL Experience Manager] 桌面应用程序](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/release-notes.html).

>[!NOTE]
>
>临时工作流不会显示在时间轴中，因为没有保存这些工作流的历史记录信息。

要查看活动流，请对资产执行一个或多个操作，选择资产，然后选择 **[!UICONTROL 时间轴]** GlobalNav列表中。

<!-- ![timeline-2](assets/timeline-2.png) -->

时间轴显示您对资产执行的操作的活动流。

<!-- ![activity_stream](assets/activity_stream.png) -->

>[!NOTE]
>
>**[!UICONTROL 发布]**&#x200B;和&#x200B;**[!UICONTROL 取消发布]**&#x200B;任务的默认日志存储位置为 `/var/audit/com.day.cq.replication/content`。对于&#x200B;**[!UICONTROL 移动]**&#x200B;任务，默认位置为 `/var/audit/com.day.cq.wcm.core.page`。

**另请参阅**

* [翻译资产](translate-assets.md)
* [Assets HTTP API](mac-api-assets.md)
* [资产支持的文件格式](file-format-support.md)
* [搜索资源](search-assets.md)
* [连接的资产](use-assets-across-connected-assets-instances.md)
* [资源报表](asset-reports.md)
* [元数据架构](metadata-schemas.md)
* [下载资源](download-assets-from-aem.md)
* [管理元数据](manage-metadata.md)
* [搜索 Facet](search-facets.md)
* [管理收藏集](manage-collections.md)
* [批量元数据导入](metadata-import-export.md)
