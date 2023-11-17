---
title: 如何将AEM自适应表单连接到Microsoft&reg； SharePoint List？
description: 将自适应表单连接到Microsoft&reg； SharePoint列表。 了解如何配置Microsoft&reg； SharePoint列表以及使用配置创建表单数据模型。 此外，您还可了解如何将FDM与自适应表单相集成。
role: User, Developer
keywords: 将AEM自适应表单连接到Microsoft SharePoint列表，将自适应表单连接到Microsoft SharePoint列表，将AEM自适应表单集成到Microsoft SharePoint列表，将自适应表单集成到Microsoft SharePoint列表，将自适应表单中的数据提交到SharePoint列表，将AEM工作流提交到SharePoint列表。
hide: true
hidefromToC: true
source-git-commit: e2505c0fec1da8395930f131bfc55e1e2ce05881
workflow-type: tm+mt
source-wordcount: '539'
ht-degree: 7%

---


# 将自适应表单连接到Microsoft® SharePoint列表

<span class="preview">这是一项预发布功能，可通过我们的[预发布渠道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html#new-features)访问。</span>

**Microsoft®SharePoint**：Microsoft® SharePoint通过为所有团队、部门和部门提供动态且高效的团队站点，实现了协作。 它可用于存储、组织、共享和访问使用任何Web浏览器(例如Microsoft®Edge、Internet Explorer、Chrome或Firefox)从任何设备获取的信息。 的两个主要组成部分 **Microsoft®SharePoint** 为：

* **Microsoft® SharePoint文档库**：Microsoft® SharePoint文档库显示文件和文件夹及其关键信息的列表，例如上次修改日期和文件所有者。 此功能使文件的组织和导航更轻松。
有关如何集成 **Microsoft® SharePoint文档库** 对于自适应表单，请参阅 [自适应表单提交操作](/help/forms/configuring-submit-actions.md#submit-to-sharepoint) 文章。

* **Microsoft® SharePoint列表**：Microsoft®SharePoint列表是数据的集合。 您可以为不同类型的数据添加列，并创建视图以有效地显示数据。 您可以轻松对列表进行分组、筛选、排序和格式化。

>[!VIDEO](https://video.tv.adobe.com/v/3424820/connect-aem-adaptive-form-to-sharepointlist/?quality=12&learn=on)

## 将自适应表单连接到Microsoft的先决条件® SharePoint列表 {#prerequisites}

将自适应表单连接到Microsoft® SharePoint List之前，请执行以下步骤：

1. [配置Microsoft](/help/forms/configure-data-sources.md#configure-microsoft-sharepoint-list)
1. [使用Microsoft创建表单数据模型](/help/forms/create-form-data-models.md)
1. [配置表单数据模型以检索和发送数据](/help/forms/work-with-form-data-model.md#configure-services)
1. [创建自适应表单](/help/forms/creating-adaptive-form-core-components.md)

现在，您可以：

* [连接Microsoft](#connect-an-adaptive-form-to-microsoft-sharepoint-list-connect-af-sharepoint-list)
* [连接Microsoft](#connect-sharepoint-list-workflow)

## 将自适应表单连接到Microsoft® SharePoint列表 {#connect-af-sharepoint-list}

要将Microsoft® SharePoint列表集成到您的自适应表单 [配置自适应表单以使用表单数据模型](/help/forms/creating-adaptive-form-core-components.md#configure-a-schema-or-form-data-model-for-an-adaptive-formconfigure-schema-or-data-model-for-form)

将自适应表单配置为使用表单数据模型后，您可以：

* [使用表单数据模型配置提交操作](/help/forms/configuring-submit-actions.md#submit-using-form-data-model)
* [配置规则编辑器以调用表单数据模型](/help/forms/rule-editor.md#invoke-form-data-model-service-invoke)

## 将Microsoft® SharePoint列表连接到AEM工作流 {#connect-sharepoint-list-workflow}

要将Microsoft®SharePoint列表集成到AEM工作流，请执行以下操作：

1. [创建工作流以调用表单数据模型](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html)

   <!--
    To create a workflow with the editor:
    1.  Go to your **AEM Forms Author** instance > **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]**.
    1.  Click **[!UICONTROL Create]** > **[!UICONTROL Create Model]**. The Add Workflow Model dialog appears. 
    1. Specify **[!UICONTROL Title]** and **[!UICONTROL Name (optional)]**.
    1. Click **[!UICONTROL Done]**. The new model is listed in the Workflow Models console.
    1. Select your new workflow, then use **[!UICONTROL Edit]** to open it for configuration.
    1. Add **[!UICONTROL Invoke Form Data Model Service]** step to your workflow.
    1. Confirm the changes with Sync (editor toolbar) to generate the runtime model.
    -->

1. [配置提交操作以调用AEM Workflow](/help/forms/configuring-submit-actions.md#invoke-an-aem-workflow)


了解如何 [使用AEM Workflow](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/workflow/use-workflow.html) 以协作、管理和处理自适应表单中的内容。

## 最佳实践 {#best-practices}

<!-- * For storing data in a tabular format or implementing data permissions, it is advisable to use Microsoft&reg; SharePoint List rather than Microsoft&reg; SharePoint Document Library. -->
* 在Microsoft® SharePoint List中，不支持以下列类型：
   * 图像列
   * 元数据列
   * 人员列
   * 外部数据列

## 另请参阅 {#see-also}

* [创建基于核心组件的自适应表单](/help/forms/creating-adaptive-form-core-components.md)
* [配置数据源](/help/forms/configuring-submit-actions.md)
* [创建表单数据模型](/help/forms/create-form-data-models.md)
* [使用以Forms为中心的AEM Workflows — 步骤参考以自动化业务流程](/help/forms/aem-forms-workflow-step-reference.md)
* [创建自适应Forms的自定义提交操作](/help/forms/custom-submit-action-form.md)
* [在AEM Sites页面上创建或添加自适应表单](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)
* [将自适应表单嵌入到AEM Sites页面](/help/forms/embed-adaptive-form-aem-sites.md)
* [在自适应表单中创建、使用和自定义主题](/help/forms/using-themes-in-core-components.md)







