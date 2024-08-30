---
title: 如何将基于核心组件的自适应表单另存为草稿，并使用草稿和提交组件列出草稿和提交？
description: 了解如何将基于核心组件的自适应表单另存为草稿。 还了解如何使用草稿和提交组件为登录用户列出草稿和提交？
feature: Adaptive Forms, Core Components
exl-id: c0653bef-afeb-40c1-b131-7d87ca5542bc
role: User, Developer
source-git-commit: 2933b3be569724800a77b4ea93e91441046746f6
workflow-type: tm+mt
source-wordcount: '1384'
ht-degree: 3%

---


# 将表单另存为草稿并将其在站点页面上列出

<span class="preview">本文包含有关&#x200B;**自动保存**&#x200B;功能（预发布功能）的内容。 该预发布功能仅可通过我们的[预发布渠道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html#new-features)访问。</span>

以某个用户为例，该用户开始填写表单，但需要暂停并稍后返回。 AEM提供了一个`save-as-draft`选项，允许用户将表单另存为草稿以供将来完成。 为方便起见，AEM提供了现成的&#x200B;**草稿和提交** Forsm Portal组件，该组件在AEM Sites页面上显示草稿和提交。 该组件列出已另存为草稿以供以后完成的表单以及已提交的表单。 只有登录的用户才能编辑其草稿或查看其提交的表单。 但是，如果匿名用户使用&#x200B;**搜索和列表程序**&#x200B;组件浏览表单列表并将表单另存为草稿，则&#x200B;**草稿和提交**&#x200B;组件不会列出该草稿。 要查看草稿和提交，用户必须在提交表单时登录。

![草稿图标](assets/drafts-component.png)

## 先决条件

* [为您的环境启用自适应Forms核心组件。](/help/forms/enable-adaptive-forms-core-components.md)

  将最新的核心组件部署到环境后，即可在创作环境中访问Forms Portal组件。

* [为草稿和提交Forms门户组件配置Azure Storage和统一存储连接器](#configure-azure-storage-and-unified-storage-connector-for-drafts--submissions-forms-portal-component)

### 为草稿和提交Forms门户组件配置Azure Storage和统一存储连接器

**草稿和提交**&#x200B;组件需要存储设置才能在AEM Sites页面上保存和列出草稿。 统一存储连接器提供了一个将AEM与外部存储关联的框架。 要将表单另存为草稿，请确保您拥有Azure存储帐户和访问密钥以授权访问[!DNL Azure]存储帐户。 拥有Azure存储帐户和访问密钥后，请执行以下步骤以创建Azure存储配置：

1. 导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Azure存储]**。

   ![Azure存储卡选择](/help/forms/assets/save-form-as-draft-azure-card.png)

1. 选择配置文件夹以创建配置，然后选择&#x200B;**[!UICONTROL 创建]**。

   ![选择Azure存储配置文件夹](/help/forms/assets/save-form-as-draft-select-config-folder.png)

1. 在&#x200B;**[!UICONTROL 标题]**&#x200B;字段中指定配置的标题。
1. 在&#x200B;**[!UICONTROL Azure存储帐户]**&#x200B;和&#x200B;**[!UICONTROL Azure访问密钥]**&#x200B;字段中指定[!DNL Azure]存储帐户的名称。

   ![Azure 存储配置](/help/forms/assets/save-form-as-draft-azure-storage.png)

   在`Azure Storage Account`文本框中输入`Connection String`，在`Azure Access key`文本框中输入`Azure Key`。

1. 单击&#x200B;**保存**。

   >[!NOTE]
   >
   > 您可以从[Microsoft Azure门户](https://learn.microsoft.com/en-us/azure/storage/common/storage-account-keys-manage?tabs=azure-portal)检索&#x200B;**[!UICONTROL Azure存储帐户]**&#x200B;和&#x200B;**[!UICONTROL Azure访问密钥]**。

   成功创建Azure Storage配置后，请使用以下步骤为Forms Portal配置统一存储连接器：

1. 导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Forms]** > **[!UICONTROL 统一存储连接器]**。

   ![统一连接器存储](/help/forms/assets/save-form-as-draft-unified-connector.png)

1. 在&#x200B;**[!UICONTROL Forms门户]**&#x200B;部分中，从&#x200B;**[!UICONTROL 存储]**&#x200B;下拉列表中选择&#x200B;**[!UICONTROL Azure]**。
1. 在&#x200B;**[!UICONTROL 存储配置路径]**&#x200B;字段中指定Azure存储配置的配置路径。

   ![统一连接器存储设置](/help/forms/assets/save-form-as-draft-unified-connector-storage.png)

1. 选择&#x200B;**[!UICONTROL 保存]**。

>[!NOTE]
>
> 如果需要配置Azure以外的存储选项，请从官方电子邮件地址写入aem-forms-ea@adobe.com并提供详细要求。

成功配置Azure Storage和Unified Storage Connector以存储草稿和已提交的表单后，请在AEM Sites页面上添加&#x200B;**草稿和提交**&#x200B;组件。

## 如何将草稿和提交组件添加到AEM Sites页面？

您可以使用现成的Forms Portal组件在Sites页面上列出草稿和提交内容。 执行以下步骤以添加&#x200B;**草稿和提交**&#x200B;门户组件：

1. 以&#x200B;**编辑**&#x200B;模式打开AEM Sites页面。
1. 转到&#x200B;**[!UICONTROL 页面信息]** > **[!UICONTROL 编辑模板]**
   ![编辑模板策略](/help/forms/assets/save-form-as-draft-edit-template.png)

1. 单击&#x200B;**[!UICONTROL 策略]**&#x200B;并选择&#x200B;**[AEM原型项目名称] - Forms和通信门户**&#x200B;下的&#x200B;**[!UICONTROL 草稿和提交]**&#x200B;复选框。

   ![策略选择](/help/forms/assets/save-form-as-draft-enable-policy.png)

1. 单击&#x200B;**[!UICONTROL 完成]**。
1. 现在，在创作模式下重新打开AEM Sites页面。
1. 在页面编辑器中找到用于添加Forms Portal组件的部分。
1. 单击&#x200B;**添加**&#x200B;图标。 图标是一个加号(+)，表示添加新组件的选项。

   单击&#x200B;**添加**&#x200B;图标会显示&#x200B;**插入新组件**&#x200B;对话框，其中显示了要插入的各种组件。

   >[!NOTE]
   >
   > 或者，您也可以拖放组件。

1. 浏览对话框中的可用组件，并从列表中选择所需的组件。 例如，从列表中选择&#x200B;**草稿和提交**&#x200B;组件以添加&#x200B;**草稿和提交** Forms门户组件。

   ![添加草稿和提交组件](/help/forms/assets/save-form-as-draft-add-dns.png)

现在，根据需要配置&#x200B;**草稿和提交**&#x200B;组件的属性。

## 配置草稿和提交组件的属性

您可以配置&#x200B;**草稿和提交**&#x200B;的属性：
1. 选择&#x200B;**草稿和提交**&#x200B;组件。
1. 单击![配置图标](assets/configure_icon.png)，此时将显示对话框。
1. 在&#x200B;**[!UICONTROL 草稿和提交]**&#x200B;对话框中，指定以下内容：
   * **标题**&#x200B;为了识别站点页面中的组件，默认情况下，标题显示在组件顶部。
   * **选择类型**：将表单列为草稿或已提交的表单。 如果选择&#x200B;**草稿Forms**，将显示另存为草稿的表单。 或者，选择&#x200B;**已提交的Forms**&#x200B;将显示由登录用户提交的表单。
   * **布局**：以卡片或列表格式显示列表草稿表单或已提交的表单。

   ![草稿和提交组件属性](/help/forms/assets/save-form-as-draft-dns-properties.png)

## 配置表单以另存为草稿

您可以通过以下两种方式配置自适应Forms，以将它们另存为草稿以供将来使用：
* [用户操作](#user-action)
* [自动保存](#auto-save)

### 用户操作

>[!NOTE]
>
> 确保[核心组件版本设置为3.0.24或更高版本](https://github.com/adobe/aem-core-forms-components)以使用&#x200B;**保存表单**&#x200B;规则将表单另存为草稿。

要将表单另存为草稿，请在表单组件上创建&#x200B;**保存表单**&#x200B;规则，如按钮。 单击按钮时，将触发规则，并将表单另存为草稿。 执行以下步骤以在按钮组件上创建&#x200B;**保存表单**&#x200B;规则：

1. 在编辑模式下打开自适应表单。
1. 选择&#x200B;**[!UICONTROL 编辑规则]**&#x200B;图标以打开&#x200B;**按钮**&#x200B;组件的规则编辑器。
1. 选择&#x200B;**[!UICONTROL 创建]**&#x200B;以配置和创建按钮的规则。
1. 在&#x200B;**[!UICONTROL When]**&#x200B;部分中，选择&#x200B;**已单击**，在&#x200B;**[!UICONTROL Then]**&#x200B;部分中，选择&#x200B;**保存表单**&#x200B;选项。
1. 选择&#x200B;**[!UICONTROL 完成]**&#x200B;以保存规则。

   ![为按钮](/help/forms/assets/save-form-as-drfat-create-rule.png)创建规则

当您预览自适应表单并填写该表单并单击&#x200B;**保存表单**&#x200B;按钮时，该表单将另存为草稿。

### 自动保存

>[!NOTE]
>
> 确保将[核心组件版本设置为3.0.52或更高版本](https://github.com/adobe/aem-core-forms-components)以使用自动保存功能将表单另存为草稿。

您还可以将自适应表单配置为根据基于时间的事件自动保存，从而确保在指定的持续时间后保存表单。 当您[为环境启用Forms Portal组件](/help/forms/list-forms-on-sites-page.md#enable-forms-portal-components-for-your-existing-environment)时，**自动保存**&#x200B;选项卡将出现在Forms容器属性中。 您可以为自适应表单配置自动保存功能：

1. 在创作实例中，以编辑模式打开自适应表单。
1. 打开内容浏览器，然后选择自适应表单的&#x200B;**[!UICONTROL 指南容器]**&#x200B;组件。
1. 单击指南容器属性![指南属性](/help/forms/assets/configure-icon.svg)图标，然后打开&#x200B;**[!UICONTROL 自动保存]**&#x200B;选项卡。

   ![自动保存](/help/forms/assets/auto-save.png)

1. 选中&#x200B;**[!UICONTROL 启用]**&#x200B;复选框以启用表单的自动保存。
1. 将&#x200B;**[!UICONTROL 触发器]**&#x200B;配置为&#x200B;**基于时间**，以便在特定时间间隔后自动保存表单<!--based on the occurrence of an event or-->。
1. 以&#x200B;**[!UICONTROL 自动保存此间隔（秒）]**&#x200B;为单位指定时间间隔，以设置按定义的时间间隔触发表单自动保存的持续时间。
1. 单击&#x200B;**[!UICONTROL 完成]**。

## 使用草稿和提交组件在Sites页面上查看草稿/提交的表单

要查看已保存的草稿或已提交的表单，请使用&#x200B;**草稿和提交** Forms门户组件。
在草稿和提交组件](#configure-properties-of-the-drafts--submissions-component)的[配置对话框中选择&#x200B;**[!UICONTROL 选择类型]**&#x200B;作为&#x200B;**草稿Forms**&#x200B;时，另存为草稿的表单将显示在站点页面上。 您可以通过单击省略号(...)打开草稿以完成表单。

![草稿图标](assets/drafts-component.png)

在草稿和提交组件](#configure-properties-of-the-drafts--submissions-component)的[配置对话框中选择&#x200B;**[!UICONTROL 选择类型]**&#x200B;作为&#x200B;**已提交的Forms**&#x200B;时，将显示已提交的表单。 您可以查看已提交的表单，但无法编辑它们。

![提交图标](assets/submission-listing.png)

也可以通过单击表单右下角显示的省略号(...)来放弃表单。

## 后续步骤

在下一篇文章中，让我们了解如何使用](/help/forms/add-form-link-to-aem-sites-page.md)链接Forms门户组件在“站点”页面上添加对表单的引用[。

## 相关文章

{{forms-portal-see-also}}

## 另请参阅 {#see-also}

{{see-also}}