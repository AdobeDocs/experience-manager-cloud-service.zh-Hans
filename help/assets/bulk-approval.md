---
title: 查看文件夹和收藏集中的资产
description: 为文件夹或集合中的资产设置审阅工作流程，并与审阅者或创意合作伙伴共享它以寻求反馈。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 991d4900862c92684ed92c1afc081f3e2d76c7ff

---


# 查看文件夹和收藏集中的资产 {#review-folder-assets-and-collections}

使用Adobe Experience Manager(AEM)资产，您可以为文件夹或集合中的资产设置临时审核工作流。 您可以与审阅者或创意合作伙伴共享它以征求他们的反馈。 您可以将审核工作流与项目关联，或创建独立的审核任务。

共享资产后，审阅者可以批准或拒绝资产。 通知在工作流的不同阶段发送，以通知目标收件人完成各种任务。 例如，当您共享文件夹或集合时，审阅人会收到一条通知，指示已共享文件夹／集合以供审阅。

审阅人完成审阅（批准或拒绝资产）后，您会收到审阅完成通知。

## 为文件夹创建审阅任务 {#creating-a-review-task-for-folders}

1. 从资产用户界面中，选择要为其创建审核任务的文件夹。
1. 在工具栏中，点按／单击创 **[!UICONTROL 建审核任务图标]** ，以打开审核任 **[!UICONTROL 务页面]** 。 如果您在工具栏中看不到该图标，请点按／单 **[!UICONTROL 击更多]** ，然后选择该图标。

   ![chlimage_1-403](assets/chlimage_1-403.png)

1. （可选）从“项 **[!UICONTROL 目]** ”列表中，选择要将审核任务关联到的项目。 默认情况下，选 **[!UICONTROL 择“无]** ”选项。 如果不希望将任何项目与审核任务关联，请保留此选择。

   >[!NOTE]
   >
   >只有您具有编辑者级别权限（或更高）的项目才会显示在“项目”列 **[!UICONTROL 表中]** 。

1. 输入审核任务的名称，然后从分配到列表中选择 **[!UICONTROL 审批人]** 。

   >[!NOTE]
   >
   >选定项目的成员／组在“分配到”列表中可作 **[!UICONTROL 为批准者]** 。

1. 输入审核任务的说明、任务优先级和到期日期。

   ![task_details](assets/task_details.png)

1. 在高级选项卡中，输入用于创建URI的标签。

   ![review_name](assets/review_name.png)

1. 点按／单 **[!UICONTROL 击提交]**，然后点按／单 **[!UICONTROL 击完成]** ，关闭确认消息。 新任务的通知将发送给审批者。
1. 以批准者身份登录到AEM资产，然后导航到资产UI。 要批准资产，请单击／点按通 **[!UICONTROL 知图标]** ，然后从列表中选择审核任务。

   ![通知](assets/notification.png)

1. 在“审 **[!UICONTROL 核任务]** ”页面中，检查审核任务的详细信息，然后点按／单击审 **[!UICONTROL 核]**。
1. 在审核任 **[!UICONTROL 务页面中]** ，选择资产，然后点按／单击批准／拒绝图 **** 标以批准或拒绝（视情况而定）。

   ![review_task](assets/review_task.png)

1. 点按/单击工具栏中的&#x200B;**[!UICONTROL 完成]**&#x200B;图标。在对话框中，输入评论，然后点按／单击完 **[!UICONTROL 成]** 以确认。
1. 导航到资产UI，然后打开文件夹。 资产的批准状态图标会同时显示在卡片视图和列表视图中。

   **卡片视图**

   ![chlimage_1-404](assets/chlimage_1-404.png)

   **列表视图**

   ![review_status_listview](assets/review_status_listview.png)

## 为集合创建审阅任务 {#creating-a-review-task-for-collections}

1. 从“收藏集”页面中，选择要为其创建审核任务的收藏集。
1. 在工具栏中，点按／单击创 **[!UICONTROL 建审核任务图标]** ，以打开审核任 **[!UICONTROL 务页面]** 。 如果您在工具栏中看不到该图标，请点按／单 **[!UICONTROL 击更多]** ，然后选择该图标。

   ![chlimage_1-405](assets/chlimage_1-405.png)

1. （可选）从“项 **[!UICONTROL 目]** ”列表中，选择要将审核任务关联到的项目。 默认情况下，选 **[!UICONTROL 择“无]** ”选项。 如果不希望将任何项目与审核任务关联，请保留此选择。

   >[!NOTE]
   >
   >只有您具有编辑者级别权限（或更高）的项目才会显示在“项目”列 **[!UICONTROL 表中]** 。

1. 输入审核任务的名称，然后从分配到列表中选择 **[!UICONTROL 审批人]** 。

   >[!NOTE]
   >
   >选定项目的成员／组在“分配到”列表中可作 **[!UICONTROL 为批准者]** 。

1. 输入审核任务的说明、任务优先级和到期日期。

   ![task_details_collection](assets/task_details-collection.png)

1. 点按／单 **[!UICONTROL 击提交]**，然后点按／单 **[!UICONTROL 击完成]** ，关闭确认消息。 新任务的通知将发送给审批者。
1. 以批准者身份登录到AEM资产，然后导航到资产控制台。 要批准资产，请点按／单击通 **[!UICONTROL 知图标]** ，然后从列表中选择审核任务。
1. 在“审 **[!UICONTROL 核任务]** ”页面中，检查审核任务的详细信息，然后点按／单击审 **[!UICONTROL 核]**。
1. 集合中的所有资产都显示在审核页面上。 Select the assets and tap/click the **[!UICONTROL Approve/Reject]** icon to approve or reject assets, as appropriate.

   ![review_task_collection](assets/review_task_collection.png)

1. 点按/单击工具栏中的&#x200B;**[!UICONTROL 完成]**&#x200B;图标。在对话框中，输入评论，然后点按／单击完 **[!UICONTROL 成]** 以确认。
1. 导航到收藏集控制台，然后打开收藏集。 资产的批准状态图标会同时显示在卡片视图和列表视图中。

   **卡片视图**

   ![collection_reviewstatuscardview](assets/collection_reviewstatuscardview.png)

   **列表视图**

   ![collection_reviewstatuslistview](assets/collection_reviewstatuslistview.png)

