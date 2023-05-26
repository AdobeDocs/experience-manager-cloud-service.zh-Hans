---
title: 查看文件夹和收藏集中的资产
description: 为文件夹或收藏集中的资产设置审阅工作流，并与审阅人或创意合作伙伴共享该工作流以寻求反馈。
contentOwner: AG
feature: Collections,Collaboration
role: User
exl-id: 1e5bdd66-2707-4584-87ed-a0ff1bde3718
source-git-commit: 80ac947976bab2b0bfedb4ff9d5dd4634de6b4fc
workflow-type: tm+mt
source-wordcount: '845'
ht-degree: 25%

---

# 查看文件夹和收藏集中的资产 {#review-folder-assets-and-collections}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/bulk-approval.html?lang=en) |
| AEM as a Cloud Service | 本文 |

使用Adobe Experience Manager Assets，您可以为文件夹或收藏集中的资源设置临时审核工作流。 您可以与审阅人或创意合作伙伴共享该内容，以征求他们的反馈。 您可以将审阅工作流与项目关联，也可以创建独立的审阅任务。

共享资产后，审核者可以批准或拒绝资产。 通知会在工作流的各个阶段发送，以通知目标收件人有关各种任务的完成。 例如，当您共享文件夹或收藏集时，审阅人会收到一则通知，指出已共享文件夹/收藏集以供审阅。

在审核者完成审核（批准或拒绝资产）后，您将收到审核完成通知。

## 为文件夹创建审核任务 {#creating-a-review-task-for-folders}

1. 从Assets用户界面中，选择要为其创建审阅任务的文件夹。
1. 在工具栏中，点按/单击&#x200B;**[!UICONTROL 创建审核任务]**&#x200B;图标，以打开&#x200B;**[!UICONTROL 审核任务]**&#x200B;页面。如果您在工具栏中看不到该图标，请点按/单击&#x200B;**[!UICONTROL 更多]**，然后选择该图标。

   ![chlimage_1-403](assets/chlimage_1-403.png)

1. （可选）从 **[!UICONTROL 项目]** 列表中，选择要与审阅任务关联的项目。 默认情况下， **[!UICONTROL 无]** 选项。 如果不想将任何项目与审阅任务相关联，请保留此选择。

   >[!NOTE]
   >
   >只有您具有编辑器级别权限（或更高版本）的项目才会在中显示 **[!UICONTROL 项目]** 列表。

1. 输入审核任务的名称，然后从中选择一个批准者 **[!UICONTROL 分配给]** 列表。

   >[!NOTE]
   >
   >所选项目的成员/组可作为批准者出现在 **[!UICONTROL 分配给]** 列表。

1. 输入审阅任务的描述、任务优先级和到期日。

   ![task_details](assets/task_details.png)

1. 在高级选项卡中，输入要用于创建URI的标签。

   ![review_name](assets/review_name.png)

1. 点按／单 **[!UICONTROL 击提交]**，然后点按／单 **[!UICONTROL 击完成]** ，关闭确认消息。 新任务的通知将发送给审批者。
1. 登录 [!DNL Experience Manager Assets] 以审批者身份导航到Assets UI。 要批准资产，请单击/点按 **[!UICONTROL 通知]** 图标，然后从列表中选择审阅任务。

   ![通知](assets/notification.png)

1. 在&#x200B;**[!UICONTROL 审查任务]**&#x200B;页面中，检查审查任务的详细信息，然后点按/单击&#x200B;**[!UICONTROL 审查]**。
1. 在&#x200B;**[!UICONTROL 审核任务]**&#x200B;页面中，选择资产，然后点按/单击&#x200B;**[!UICONTROL 批准/拒绝]**&#x200B;图标以批准或拒绝（根据需要）。

   ![review_task](assets/review_task.png)

1. 点按/单击 **[!UICONTROL 完成]** 图标。 在对话框中，输入注释并点按/单击  **[!UICONTROL 完成]** 以确认。
1. 导航到资产UI，然后打开文件夹。 资产的审批状态图标会同时显示在“信息卡”和“列表”视图中。

   **信息卡视图**

   ![chlimage_1-404](assets/chlimage_1-404.png)

   **列表视图**

   ![review_status_listview](assets/review_status_listview.png)

## 为收藏集创建审核任务 {#creating-a-review-task-for-collections}

1. 从“收藏集”页面中，选择要为其创建审阅任务的收藏集。
1. 在工具栏中，点按/单击&#x200B;**[!UICONTROL 创建审核任务]**&#x200B;图标，以打开&#x200B;**[!UICONTROL 审核任务]**&#x200B;页面。如果您在工具栏中看不到该图标，请点按/单击&#x200B;**[!UICONTROL 更多]**，然后选择该图标。

   ![chlimage_1-405](assets/chlimage_1-405.png)

1. （可选）从 **[!UICONTROL 项目]** 列表中，选择要与审阅任务关联的项目。 默认情况下， **[!UICONTROL 无]** 选项。 如果不想将任何项目与审阅任务相关联，请保留此选择。

   >[!NOTE]
   >
   >只有您具有编辑器级别权限（或更高版本）的项目才会在中显示 **[!UICONTROL 项目]** 列表。

1. 输入审核任务的名称，然后从中选择一个批准者 **[!UICONTROL 分配给]** 列表。

   >[!NOTE]
   >
   >所选项目的成员/组可作为批准者出现在 **[!UICONTROL 分配给]** 列表。

1. 输入审阅任务的描述、任务优先级和到期日。

   ![task_details — 收藏集](assets/task_details-collection.png)

1. 点按／单 **[!UICONTROL 击提交]**，然后点按／单 **[!UICONTROL 击完成]** ，关闭确认消息。 新任务的通知将发送给审批者。
1. 登录 [!DNL Experience Manager Assets] 以审批者身份导航到资产控制台。 要批准资产，请点按/单击 **[!UICONTROL 通知]** 图标，然后从列表中选择审阅任务。
1. 在&#x200B;**[!UICONTROL 审查任务]**&#x200B;页面中，检查审查任务的详细信息，然后点按/单击&#x200B;**[!UICONTROL 审查]**。
1. 收藏集中的所有资产均显示在审核页面上。 选择资产并点按/单击 **[!UICONTROL 批准/拒绝]** 图标以批准或拒绝资产（根据需要）。

   ![review_task_collection](assets/review_task_collection.png)

1. 点按/单击 **[!UICONTROL 完成]** 图标。 在对话框中，输入注释并点按/单击 **[!UICONTROL 完成]** 以确认。
1. 导航到收藏集控制台并打开收藏集。 资产的审批状态图标会同时显示在“信息卡”和“列表”视图中。

   **信息卡视图**

   ![collection_reviewstatuscardview](assets/collection_reviewstatuscardview.png)

   **列表视图**

   ![collection_reviewstatuslistview](assets/collection_reviewstatuslistview.png)

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
