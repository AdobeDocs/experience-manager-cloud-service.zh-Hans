---
title: 如何将基于核心组件的自适应表单另存为草稿？
description: 了解如何将基于核心组件的自适应表单另存为草稿、创建Forms Portal并在AEM Sites页面上使用现成的核心组件。
feature: Adaptive Forms, Core Components
exl-id: c0653bef-afeb-40c1-b131-7d87ca5542bc
role: User, Developer, Admin
source-git-commit: 2b76f1be2dda99c8638deb9633055e71312fbf1e
workflow-type: tm+mt
source-wordcount: '1072'
ht-degree: 2%

---

<span class="preview"> 本文包含预发行版功能的内容。 预发行功能只能通过我们的 [预发行渠道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html#new-features).

# 将基于核心组件的自适应表单另存为草稿 {#save-af-form}

将自适应表单另存为草稿是提高用户效率和准确性的重要功能。 此功能允许用户保存进度并在以后返回以完成任务，而不会丢失任何输入的信息。 提供  `save-as-draft` 选项可确保灵活管理时间，降低数据丢失风险，并维护提交的准确性。 您可以将表单另存为草稿以便稍后完成。

## 注意事项

* [为您的环境启用自适应Forms核心组件。](/help/forms/enable-adaptive-forms-core-components.md)

* 确保 [核心组件设置为版本3.0.24或更高版本](https://github.com/adobe/aem-core-forms-components) 以使用此功能。
* 确保您拥有 [Azure存储帐户和访问密钥](https://learn.microsoft.com/en-us/azure/storage/common/storage-account-keys-manage?tabs=azure-portal) 以授权访问Azure存储帐户。

## 将自适应表单另存为草稿

[!DNL Experience Manager Forms] 数据集成(data-integration.md)提供 [!DNL Azure] 用于集成表单的存储配置 [!DNL Azure] 存储服务。 表单数据模型(FDM)可用于创建与交互的自适应Forms [!DNL Azure] 服务器启用业务工作流。

要将表单另存为草稿，请确保您拥有Azure存储帐户和访问密钥以授权访问 [!DNL Azure] 存储帐户。 要将表单另存为草稿，请执行以下步骤：

1. [创建 Azure 存储配置](#create-azure-storage-configuration)
1. [为Forms Portal配置统一存储连接器](#configure-usc-forms-portal)
1. [创建规则以将自适应表单另存为草稿](#rule-to-save-adaptive-form-as-draft)


### 1.创建Azure存储配置 {#create-azure-storage-configuration}

一旦你拥有Azure存储帐户和访问密钥，可授权访问 [!DNL Azure] 请执行以下步骤以创建Azure存储配置：

1. 导航到 **[!UICONTROL 工具]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Azure存储]**.

   ![Azure存储卡选择](/help/forms/assets/save-form-as-draft-azure-card.png)

1. 选择配置文件夹以创建配置，然后选择 **[!UICONTROL 创建]**.

   ![选择Azure存储配置文件夹](/help/forms/assets/save-form-as-draft-select-config-folder.png)

1. 在中指定配置的标题 **[!UICONTROL 标题]** 字段。
1. 指定 [!DNL Azure] 中的存储帐户 **[!UICONTROL Azure存储帐户]** 和 **[!UICONTROL Azure访问密钥]** 字段。

   ![Azure 存储配置](/help/forms/assets/save-form-as-draft-azure-storage.png)

1. 单击&#x200B;**保存**。

>[!NOTE]
>
> 您可以检索 **[!UICONTROL Azure存储帐户]** 和 **[!UICONTROL Azure访问密钥]** 从 [Microsoft Azure门户](https://learn.microsoft.com/en-us/azure/storage/common/storage-account-keys-manage?tabs=azure-portal).


### 2.为Forms门户配置统一存储连接器 {#configure-usc-forms-portal}

成功创建Azure存储配置后，请使用以下步骤为Forms Portal配置统一存储连接器：

1. 导航到 **[!UICONTROL 工具]** > **[!UICONTROL Forms]** > **[!UICONTROL 统一存储连接器]**.

   ![统一的连接器存储](/help/forms/assets/save-form-as-draft-unified-connector.png)

1. 在 **[!UICONTROL Forms门户]** 部分，选择 **[!UICONTROL Azure]** 从 **[!UICONTROL 存储]** 下拉列表。
1. 指定 [Azure存储配置的配置路径](#create-azure-storage-configuration) 在 **[!UICONTROL 存储配置路径]** 字段。

   ![统一连接器存储设置](/help/forms/assets/save-form-as-draft-unified-connector-storage.png)

1. 选择 **[!UICONTROL 保存]** 然后选择 **[!UICONTROL Publish]** 以发布配置。

### 3.创建规则以将自适应表单另存为草稿 {#rule-to-save-adaptive-form-as-draft}

要将表单另存为草稿，请创建 **保存表单** 表单组件上的规则，例如按钮。 单击按钮时，将触发规则，并将表单另存为草稿。 执行以下步骤以创建 **保存表单** 按钮组件上的规则：

1. 在创作实例中，以编辑模式打开自适应表单。
1. 从左窗格中，选择 ![“组件”图标](assets/components_icon.png) 并拖动 **[!UICONTROL 按钮]** 组件添加到表单。
1. 选择 **[!UICONTROL 按钮]** 组件，然后选择 ![“配置”图标](assets/configure_icon.png).
1. 选择 **[!UICONTROL 编辑规则]** 图标以打开规则编辑器。
1. 选择 **[!UICONTROL 创建]** 以配置和创建规则。
1. 在 **[!UICONTROL 时间]** 部分，选择 **已单击** 和 **[!UICONTROL 则]** 部分，选择 **保存表单** 选项。
1. 选择 **[!UICONTROL 完成]** 以保存规则。

![为按钮创建规则](/help/forms/assets/save-form-as-drfat-create-rule.png)

预览自适应表单时，请填写该表单，然后单击 **保存表单** 按钮时，表单将另存为草稿以供将来使用。

## 草稿和提交组件可在AEM Sites页面上列出草稿

AEM Forms提供 **草稿和提交** 开箱即用的门户组件，用于在AEM Sites页面上显示已保存的表单。 此 **草稿和提交** 组件显示另存为草稿以供以后完成的表单以及已提交的表单。 此组件通过列出与用户创建的自适应Forms相关的草稿和提交，为任何登录用户提供个性化体验。

您可以使用现成的Forms Portal组件在AEM Sites页面中列出表单草稿。 执行以下步骤以使用 **草稿和提交** 门户组件：

1. [启用草稿和提交Forms门户组件](#enable-component)
2. [在AEM Sites页面中添加草稿和提交组件](#Add-drafts-submissions-component)
3. [配置草稿和提交组件](#configure-drafts-submissions-component)

### 1.启用草稿和提交Forms门户组件{#enable-component}

要启用 **[!UICONTROL 草稿和提交]** 组件时，请执行以下步骤：

1. 在中打开AEM Sites页面 **编辑** 模式。
1. 转到 **[!UICONTROL 页面信息]** > **[!UICONTROL 编辑模板]**
   ![编辑模板策略](/help/forms/assets/save-form-as-draft-edit-template.png)

1. 单击 **[!UICONTROL 策略]** 并选择 **[!UICONTROL 草稿和提交]**  复选框 **[AEM原型项目名称] - Forms和通信门户**.

   ![策略选择](/help/forms/assets/save-form-as-draft-enable-policy.png)

1. 单击&#x200B;**[!UICONTROL 完成]**。

启用门户组件后，您可以在AEM Sites页面的创作实例中使用它。

### 2.在AEM Sites页面中添加草稿和提交组件{#Add-drafts-submissions-component}

您可以通过添加和配置门户组件，在使用AEM创作的网站上创建和自定义Forms门户。 确保 [已启用草稿和提交组件](#enable-component) 在AEM Sites页面中使用它们之前。

要添加组件，请将组件从 **草稿和提交** 组件窗格到页面上的布局容器中，或选择布局容器上的添加图标，然后从以下位置添加组件： **[!UICONTROL 插入新组件]** 对话框。

![添加草稿和提交组件](/help/forms/assets/save-form-as-draft-add-dns.png)

### 3.配置草稿和提交组件 {#configure-drafts-submissions-component}

此 **草稿和提交** 组件显示另存为草稿以供以后填写和提交的表单。 配置 **草稿和提交**，请执行以下步骤：
1. 选择 **草稿和提交** 组件。
1. 单击 ![“配置”图标](assets/configure_icon.png) 此时将显示对话框。
1. 在 **[!UICONTROL 草稿和提交]** 对话框，请指定以下内容：
   * **标题** 要在站点页面中标识组件，默认情况下，标题显示在组件顶部。
   * **类型**：将表单指示为草稿或已提交的表单。
   * **布局**：以卡片或列表格式显示列表草稿表单或已提交的表单。

   ![草稿和提交组件属性](/help/forms/assets/save-form-as-draft-dns-properties.png)

1. 单击&#x200B;**完成**。

时间 **[!UICONTROL 选择类型]** 被选为 **草稿Forms**，将显示另存为草稿的表单：
![“草稿”图标](assets/drafts-component.png)

时间 **[!UICONTROL 选择类型]** 被选为 **已提交Forms**，则会显示提交的表单：

![提交图标](assets/submission-listing.png)

您可以通过单击相应的表单来打开该表单。

<!--

### Configure Search & Lister Component {#configure-search-lister-component}

The Search & Lister component is used to list adaptive forms on a page and to implement search on the listed forms. 

![Search and Lister icon](assets/search-and-lister-component.png)

To configure, select the component and then select the ![Configure icon](assets/configure_icon.png). The [!UICONTROL Search and Lister] dialog opens.

1. In the [!UICONTROL Display] tab, configure the following:
    * In **[!UICONTROL Title]**, specify the title for the Search & Lister component. An indicative title enables the users perform quick search across the list of forms.
    * From the **[!UICONTROL Layout]** list, select the layout to represent the forms in card or list format.
    * Select **[!UICONTROL Hide Search]** and **[!UICONTROL Hide Sorting]** to hide the search and sort by features.
    * In **[!UICONTROL Tooltip]**, provide the tooltip that appears when you hover over the component. 
1. In the [!UICONTROL Asset Folder] tab, specify the location from where the forms are pulled and listed on the page. You can configure multiple folder locations.
1. In the [!UICONTROL Results] tab, configure the maximum number of forms to display per page. The default is eight forms per page.

### Configure Link Component {#configure-link-component}

The link component enables you to provide links to an adaptive form on the page. To configure, select the component and then select the ![Configure icon](assets/configure_icon.png). The [!UICONTROL Edit Link Component] dialog opens.

1. In the [!UICONTROL Display] tab, provide the link caption and tooltip to ease identification of the forms represented by the link.
1. In the [!UICONTROL Asset Info] tab, specify the repository path where the asset is stored. 
1. In the [!UICONTROL Query Params] tab, specify the additional parameters in the key-value pair format. When the link is clicked, these additional parameters and passed along with the form.

## Configure Asynchronous Form Submission Using Adobe Sign {#configure-asynchronous-form-submission-using-adobe-sign}

You can configure to submit an adaptive form only when all the recipients have completed the signing ceremony. Follow the steps below to configure the setting using Adobe Sign.

1. In the author instance, open an Adaptive Form in the edit mode.
1. From the left pane, select the Properties icon and expand the **[!UICONTROL ELECTRONIC SIGNTATURE]** option.
1. Select **[!UICONTROL Enable Adobe Sign]**. Various configuration options display. 
1. In the [!UICONTROL Submit the form] section, select the **[!UICONTROL after every recipient completes signing ceremony]** option to configure the Submit Form action, where the form is first sent to all the recipients for signing. Once all the recipients have signed the form, only then the form is submitted. 

## Save Adaptive Forms As Drafts {#save-adaptive-forms-as-drafts}

You can save forms as Drafts for completing them later. There are two ways in which a form is saved as a draft:

* Create a "Save Form" rule on a form component, for example, a button. On clicking the button, the rule triggers and the form are saved a draft.
* Enable Auto-Save feature, which saves the form as per the specified event or after a configured interval of time.

### Create Rules to Save an Adaptive Form as Draft {#rule-to-save-adaptive-form-as-draft}

To create a "Save Form" rule on a form component, for example, a button, follow the steps below:

1. In the author instance, open an Adaptive Form in edit mode.
1. From the left pane, select ![Components icon](assets/components_icon.png) and drag the [!UICONTROL Button] component to the form.
1. Select the [!UICONTROL Button] component and then select the ![Configure icon](assets/configure_icon.png). 
1. Select the [!UICONTROL Edit Rules] icon to open the Rule Editor. 
1. Select **[!UICONTROL Create]** to configure and create the rule.
1. In the [!UICONTROL When] section, select "is clicked" and in the [!UICONTROL Then] section, select the "Save Form" options.
1. Select **[!UICONTROL Done]** to save the rule.

### Enable Auto-save {#enable-auto-save}

You can configure the auto-save feature for an adaptive form as follows:

1. In the author instance, open an Adaptive Form in edit mode.
1. From the left pane, select the ![Properties icon](assets/configure_icon.png) and expand the [!UICONTROL AUTO-SAVE] option.
1. Select the **[!UICONTROL Enable]** check box to enable auto-save of the form. You can configure the following:
* By default, the [!UICONTROL Adaptive Form Event] is set to "true", which implies that the form is auto-saved after every event.
* In [!UICONTROL Trigger], configure to trigger auto-save based on the occurrence of an event or after a specific interval of time.
-->

## 另请参阅 {#see-also}

{{see-also}}



<!--

>[!MORELIKETHIS]
>
>* [Configure data sources for AEM Forms](/help/forms/configure-data-sources.md)
>* [Configure Azure storage for AEM Forms](/help/forms/configure-azure-storage.md)
>* [Integrate Microsoft Dynamics 365 and Salesforce with Adaptive Forms](/help/forms/configure-msdynamics-salesforce.md)

-->
