---
title: 查看文件夹和收藏集中的资产
description: 为文件夹或收藏集中的资产设置审核工作流，并与审阅人或创意合作伙伴共享该工作流，以寻求反馈。
contentOwner: AG
feature: 收藏集，协作
role: Business Practitioner
exl-id: 1e5bdd66-2707-4584-87ed-a0ff1bde3718
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '795'
ht-degree: 24%

---

# 查看文件夹和收藏集中的资产{#review-folder-assets-and-collections}

使用Adobe Experience Manager Assets，您可以为文件夹或收藏集中的资产设置临时审核工作流。 您可以与审阅人或创意合作伙伴共享该组件，以征求他们的反馈。 您可以将审核工作流与项目关联或创建独立的审核任务。

共享资产后，审阅人可以批准或拒绝资产。 在工作流的各个阶段发送通知，以通知目标收件人有关各种任务的完成情况。 例如，当您共享文件夹或收藏集时，审阅人会收到一则通知，指出已共享文件夹/收藏集以供审阅。

审核人员完成审核（批准或拒绝资产）后，您会收到审核完成通知。

## 为文件夹{#creating-a-review-task-for-folders}创建审核任务

1. 从Assets用户界面中，选择要为其创建审核任务的文件夹。
1. 在工具栏中，点按/单击&#x200B;**[!UICONTROL 创建审核任务]**&#x200B;图标，以打开&#x200B;**[!UICONTROL 审核任务]**&#x200B;页面。如果您在工具栏中看不到该图标，请点按/单击&#x200B;**[!UICONTROL 更多]**，然后选择该图标。

   ![chlimage_1-403](assets/chlimage_1-403.png)

1. （可选）从&#x200B;**[!UICONTROL 项目]**&#x200B;列表中，选择要将审核任务关联到的项目。 默认情况下，选中&#x200B;**[!UICONTROL None]**&#x200B;选项。 如果不想将任何项目与审核任务关联，请保留此选择。

   >[!NOTE]
   >
   >只有您具有编辑器级别权限（或更高级别）的项目才会显示在&#x200B;**[!UICONTROL 项目]**&#x200B;列表中。

1. 输入审核任务的名称，然后从&#x200B;**[!UICONTROL 分配给]**&#x200B;列表中选择审批者。

   >[!NOTE]
   >
   >在&#x200B;**[!UICONTROL Assign To]**&#x200B;列表中，选定项目的成员/组可作为批准者。

1. 输入审核任务的说明、任务优先级和到期日期。

   ![task_details](assets/task_details.png)

1. 在高级选项卡中，输入用于创建URI的标签。

   ![review_name](assets/review_name.png)

1. 点按／单 **[!UICONTROL 击提交]**，然后点按／单 **[!UICONTROL 击完成]** ，关闭确认消息。 新任务的通知将发送给审批者。
1. 以审批者身份登录到[!DNL Experience Manager Assets]，然后导航到资产UI。 要批准资产，请单击/点按&#x200B;**[!UICONTROL 通知]**&#x200B;图标，然后从列表中选择审核任务。

   ![通知](assets/notification.png)

1. 在&#x200B;**[!UICONTROL 审查任务]**&#x200B;页面中，检查审查任务的详细信息，然后点按/单击&#x200B;**[!UICONTROL 审查]**。
1. 在&#x200B;**[!UICONTROL 审核任务]**&#x200B;页面中，选择资产，然后点按/单击&#x200B;**[!UICONTROL 批准/拒绝]**&#x200B;图标以批准或拒绝（根据需要）。

   ![review_task](assets/review_task.png)

1. 点按/单击工具栏中的&#x200B;**[!UICONTROL 完成]**&#x200B;图标。在对话框中，输入注释，然后点按/单击&#x200B;**[!UICONTROL 完成]**&#x200B;以确认。
1. 导航到资产UI，然后打开文件夹。 资产的批准状态图标会同时显示在卡片视图和列表视图中。

   **卡片视图**

   ![chlimage_1-404](assets/chlimage_1-404.png)

   **列表视图**

   ![review_status_listview](assets/review_status_listview.png)

## 为集合{#creating-a-review-task-for-collections}创建审核任务

1. 从收藏集页面中，选择要为其创建审阅任务的收藏集。
1. 在工具栏中，点按/单击&#x200B;**[!UICONTROL 创建审核任务]**&#x200B;图标，以打开&#x200B;**[!UICONTROL 审核任务]**&#x200B;页面。如果您在工具栏中看不到该图标，请点按/单击&#x200B;**[!UICONTROL 更多]**，然后选择该图标。

   ![chlimage_1-405](assets/chlimage_1-405.png)

1. （可选）从&#x200B;**[!UICONTROL 项目]**&#x200B;列表中，选择要将审核任务关联到的项目。 默认情况下，选中&#x200B;**[!UICONTROL None]**&#x200B;选项。 如果不想将任何项目与审核任务关联，请保留此选择。

   >[!NOTE]
   >
   >只有您具有编辑器级别权限（或更高级别）的项目才会显示在&#x200B;**[!UICONTROL 项目]**&#x200B;列表中。

1. 输入审核任务的名称，然后从&#x200B;**[!UICONTROL 分配给]**&#x200B;列表中选择审批者。

   >[!NOTE]
   >
   >在&#x200B;**[!UICONTROL Assign To]**&#x200B;列表中，选定项目的成员/组可作为批准者。

1. 输入审核任务的说明、任务优先级和到期日期。

   ![task_details-collection](assets/task_details-collection.png)

1. 点按／单 **[!UICONTROL 击提交]**，然后点按／单 **[!UICONTROL 击完成]** ，关闭确认消息。 新任务的通知将发送给审批者。
1. 以审批者身份登录到[!DNL Experience Manager Assets]，然后导航到资产控制台。 要批准资产，请点按/单击&#x200B;**[!UICONTROL 通知]**&#x200B;图标，然后从列表中选择审核任务。
1. 在&#x200B;**[!UICONTROL 审查任务]**&#x200B;页面中，检查审查任务的详细信息，然后点按/单击&#x200B;**[!UICONTROL 审查]**。
1. 收藏集中的所有资产都会在审核页面上可见。 选择资产，然后点按/单击&#x200B;**[!UICONTROL 批准/拒绝]**&#x200B;图标，以批准或拒绝资产（根据需要）。

   ![review_task_collection](assets/review_task_collection.png)

1. 点按/单击工具栏中的&#x200B;**[!UICONTROL 完成]**&#x200B;图标。在对话框中，输入注释，然后点按/单击&#x200B;**[!UICONTROL 完成]**&#x200B;以确认。
1. 导航到收藏集控制台并打开收藏集。 资产的批准状态图标会同时显示在卡片视图和列表视图中。

   **卡片视图**

   ![collection_reviewstatuscardview](assets/collection_reviewstatuscardview.png)

   **列表视图**

   ![collection_reviewstatuslistview](assets/collection_reviewstatuslistview.png)
