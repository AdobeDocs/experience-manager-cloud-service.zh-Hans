---
title: 如何在预览或发布实例上发布或取消发布表单？
description: 了解如何从AEM创作环境发布或取消发布表单以预览或发布实例。 无论您是在暂存环境中测试表单，还是为最终用户实时部署表单，AEM都提供了简化的工具来高效管理此过程。
Keywords: Manage publication, Forms Manage publication, AF Manage publication, Adaptive Forms Manage publication, Cloud Manage publication
feature: Adaptive Forms
feature-set: Experience Manager Assets,Experience Manager Sites,Experience Manager, Experience Manager Forms, Experience Manager Cloud Manager
role: User, Developer
level: Intermediate
exl-id: 6ade40f1-bad5-4f5e-aa0e-84b7c6a82e02
source-git-commit: dab2b94d1e456622f061741ba1b5192c9163c295
workflow-type: tm+mt
source-wordcount: '945'
ht-degree: 1%

---

# 在Experience Manager Forms中&#x200B;管理发布

作为Adobe Experience Manager (AEM) Forms管理员，您可以将表单从创作实例发布到Experience Manager Forms。 您还可以选择计划在稍后的日期或时间发布表单或文件夹。 发布后，用户可以访问和填写表单。

在Experience Manager Forms中，您可以使用以下方法之一发布表单：
* [发布选项](#publish-forms-using-the-publish-option)
* [“管理发布”选项](#publish-forms-using-the-manage-publication-option)

## 注意事项

* 只有`forms-users`组的成员可以使用&#x200B;**管理发布**&#x200B;选项发布表单。
* 在重新发布之前，对Experience Manager Forms中的表单或文件夹所做的更改不会显示在&#x200B;**发布**&#x200B;实例中。 这可以确保&#x200B;**发布**&#x200B;实例中正在进行的更新仍然不可用。 只有管理员明确发布的更改才会反映在&#x200B;**发布**&#x200B;实例中。

## 使用发布选项发布表单

通过&#x200B;**发布**&#x200B;选项，可立即发布表单。 要使用工具栏上的&#x200B;**发布**&#x200B;按钮发布Experience Manager表单，请执行以下操作： 要使用“发布”选项发布表单，请执行以下操作：

1. 在Experience Manager Forms控制台中，导航到父文件夹，然后选择要发布的表单。
1. 单击工具栏中的&#x200B;**发布**&#x200B;选项，查看将随表单一起发布的所有引用资源。
1. 单击&#x200B;**[!UICONTROL 发布]**。

   ![发布和取消发布表单](/help/edge/docs/forms/assets/publish-form-option.png)

   成功发布表单及其相关资源后，将显示&#x200B;**成功**&#x200B;对话框。
1. 单击&#x200B;**关闭**。

   ![“成功”对话框](/help/forms/assets/publish-success1.png)

### 取消发布表单

使用&#x200B;**发布**&#x200B;选项及其相关资产成功发布表单后，您甚至可以使用工具栏上提供的&#x200B;**[!UICONTROL 取消发布]**&#x200B;按钮取消发布它们。 要取消发布表单，请执行以下操作：

1. 要取消发布表单及其相关资源，请选择该表单，然后单击工具栏中的&#x200B;**[!UICONTROL 取消发布]**

   单击&#x200B;**[!UICONTROL 取消发布]**&#x200B;按钮时，将显示&#x200B;**取消发布资产**&#x200B;对话框。
1. 单击&#x200B;**[!UICONTROL 取消发布]**&#x200B;以开始取消发布过程

   ![取消对话框](/help/forms/assets/unpublish-asset.png)

   成功取消发布表单及其相关资源后，将显示&#x200B;**成功**&#x200B;对话框。
1. 单击&#x200B;**关闭**。

   ![取消发布成功](/help/forms/assets/unpublishing-start.png)

## 使用管理发布选项发布表单

管理发布允许您向所选目标发布内容或从中取消发布内容，将内容从`forms&documents`文件夹添加到发布列表，选择要发布的引用，以及安排发布到以后的日期或时间。  要使用&#x200B;**管理发布**&#x200B;选项发布表单，请执行以下操作：

1. 在Experience Manager Forms控制台中，导航到父文件夹，然后选择要发布的表单。
1. 单击工具栏中的&#x200B;**[!UICONTROL 管理发布]**&#x200B;选项。

   ![管理发布选项](/help/forms/assets/manage-publication-option.png)

   出现&#x200B;**管理发布** UI：

   ![管理发布](/help/forms/assets/manage-publication.png)

   以下选项在&#x200B;**管理发布** UI中可用：

   * **操作**

      * **发布**：将表单发布到所选目标
      * **取消发布**：从目标取消发布表单

   * **目标**

      * **发布**：将表单发布到Experience Manager Forms (AEM)发布实例。
      * **预览**：将表单发布到Experience Manager Forms (AEM)预览实例。

   * **计划**

      * **现在**：立即发布表单
      * **稍后**：发布基于&#x200B;**激活日期**&#x200B;或时间的表单

1. 单击&#x200B;**下一步**&#x200B;继续。
1. （可选）在&#x200B;**范围**&#x200B;选项卡中，使用[添加内容](#add-content)选项添加更多内容以进行发布。 例如，您可以添加更多Forms或记录文档文件。
   ![范围选项卡](/help/forms/assets/scope-tab.png)
1. 单击&#x200B;**[!UICONTROL 发布]**发布表单和相关资源，并显示成功消息。
   ![成功发布消息](/help/forms/assets/publish-successful.png)

### 添加内容

将发布到Experience Manager Forms允许您进一步向发布列表添加更多内容（表单）。
添加更多表单以进行发布：

1. 单击“**添加内容**”按钮可添加更多内容。

   ![添加内容](/help/forms/assets/add-content.png)

2. 从&#x200B;**选择路径**&#x200B;屏幕中选择表单。

   ![添加内容](/help/forms/assets/add-assets.png)

   >[!NOTE]
   >
   > 您可以从`formsanddocuments`文件夹向列表添加更多表单或文件夹。 但无法一次从多个文件夹添加表单。

3. 要将引用配置为发布或不发布表单，请选择该表单，然后单击&#x200B;**[!UICONTROL 已发布引用]**。

   ![已发布引用](/help/forms/assets/published-references.png)

4. 在&#x200B;**已发布的引用**&#x200B;对话框中，取消选中您计划不发布的资源，然后单击&#x200B;**[!UICONTROL 完成]**。
   ![已发布引用对话框](/help/forms/assets/published-references-dialog.png)

<!--
### Include Folder Settings
By default, publishing a folder to Experience Manager Forms publishes all the assets, subfolders, and their references. To filter the folder for publishing:

1. Click **[Include Folder Settings]** to filter the folder.

    ![Include folder](/help/forms/assets/include-folder.png)

    The **[UICONTROL Include Folder Settings]** dialog appears. 
    
    ![Include folder dialog](/help/forms/assets/include-folder-dialog.png)
    
    The **[UICONTROL Include Folder Settings]** includes following options:

    * **[!UICONTROL Include folder contents]** checkbox. 
        * If selected, all forms and assets in the chosen folder, its subfolders (including all forms and assets within them), and references are published.
        * If not selected, only the forms and assets in the selected folder are published, while subfolder forms and assets are not.

    * **[!UICONTROL Include only immediate folder contents]** checkbox
        Selecting the **[!UICONTROL Include folder contents]** checkbox enables the **[!UICONTROL Include only immediate folder contents]** checkbox for selection.

        * If you select both options, all the forms and assets of the selected folder, subfolders (empty), and references are published. The forms and assets of the subfolders are not published.
        * -->


### 稍后发布或取消发布表单

除了允许您在以后的日期和时间发布或取消发布表单外，发布或取消发布选项还允许您配置工作流。 工作流完成后，将发布或取消发布表单。

要计划表单以供发布或取消发布，请执行以下操作：

1. 在Experience Manager Forms控制台中，导航到父文件夹，然后选择要计划发布的表单。
1. 单击工具栏中的&#x200B;**[!UICONTROL 管理发布]**&#x200B;选项。

   ![管理发布](/help/forms/assets/manage-publication.png)

1. 单击&#x200B;**发布**&#x200B;或从&#x200B;**[!UICONTROL 操作]**&#x200B;中&#x200B;**取消发布**。
1. 选择要发布或取消发布内容的&#x200B;**[!UICONTROL 目标]**。
   * **预览**：使用&#x200B;**预览**&#x200B;选项发布或取消发布到Experience Manager Forms预览环境。 Experience Manager Forms预览环境用于测试开发表单。
   * **发布**：当表单准备在生产环境中使用后，使用Experience Manager Forms **发布**&#x200B;选项将表单发送到Experience Manager Forms发布环境。

1. 从&#x200B;**计划**&#x200B;中选择&#x200B;**[!UICONTROL 稍后]**。

   ![稍后管理发布](/help/forms/assets/manage-publication-later.png)

1. 选择&#x200B;**[!UICONTROL 激活日期]**&#x200B;并指定日期和时间。
1. 单击&#x200B;**[!UICONTROL 下一步]**。
1. （可选）在&#x200B;**范围**&#x200B;选项卡中，使用&#x200B;**[!UICONTROL 添加内容]**添加内容。
   ![稍后管理发布添加内容](/help/forms/assets/publish-later-add-content.png)
1. 单击&#x200B;**[!UICONTROL 下一步]**。
1. 在&#x200B;**工作流**&#x200B;选项卡中，指定&#x200B;**[!UICONTROL 工作流标题]**。
1. 单击&#x200B;**[!UICONTROL 稍后发布]**。

   ![管理发布工作流](/help/forms/assets/manage-publication-workflows.png)

## 确定发布状态

可通过多种方法确定发布状态：

* 登录到目标实例以验证发布的表单和其他资源（取决于计划的日期或时间）。

* 使用时间线视图确定发布状态。

* 使用自适应Forms编辑器中的页面信息菜单。
