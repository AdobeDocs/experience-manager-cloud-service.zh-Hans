---
title: 配置 Content Hub 用户界面
description: 配置 Content Hub 用户界面
exl-id: e9e22862-9bcd-459a-bcf4-7f376a0b329a
source-git-commit: 323fe1ba95b027f3c0d625e122b1885723e94b0f
workflow-type: tm+mt
source-wordcount: '1718'
ht-degree: 14%

---

# 配置 Content Hub 用户界面 {#configure-content-hub-user-interface}

| [搜索最佳实践](/help/assets/search-best-practices.md) | [元数据最佳实践](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | [具有 OpenAPI 功能的 Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets 开发人员文档](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

>[!CONTEXTUALHELP]
>id="configure_content_hub"
>title="配置 Content Hub 用户界面"
>abstract="管理员使用 Experience Manager Assets 可以配置 Content Hub 用户界面上可用的选项。根据管理员选择的配置选项，Content Hub 用户可以查看 Content Hub 上的字段。配置选项包括导入资产时的元数据、过滤器、资产属性、搜索资产时的元数据、个性化品牌以及任何自定义链接。"
>additional-url="https://images-tv.adobe.com/mpcv3/4477/74a81d1c-0cfe-41f4-8a06-18ff70604e45_1732023385.854x480at800_h264.mp4" text="观看视频"

<!-- ![Download assets](assets/download-asset.jpg) -->

![在Content Hub上配置资源](assets/configure-assets.png)

>[!AVAILABILITY]
>
>Content Hub指南现在提供了PDF格式。 下载整个指南，并使用Adobe Acrobat AI Assistant来回答您的疑问。
>
>[!BADGE Content Hub指南PDF]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/content-hub.pdf"}

管理员使用 Experience Manager Assets 可以配置 Content Hub 用户界面上可用的选项。根据管理员选择的配置选项，Content Hub 用户可以查看 Content Hub 上的字段。配置选项包括：

* 用户在搜索资产时可用的筛选器。

* 每个资源的可用资源详细信息或属性。

* 向Content Hub添加资源时，用户可以使用的元数据字段。

* 可在Content Hub上搜索的资源元数据字段。

* 您需要为组织显示的品牌推广内容。

* 除了资源、收藏集和分析之外，您需要在Content Hub中包含的任何自定义链接。

## 先决条件 {#prerequisites-configuration-ui}

[Content Hub管理员](/help/assets/deploy-content-hub.md#step-3-onboard-content-hub-administrator)可以为组织内的其他用户设置配置选项。

## 访问Content Hub上的配置选项 {#access-configuration-options-content-hub}

要在Content Hub上访问配置选项，请执行以下操作：

1. 单击右窗格中的用户图标。

1. 在&#x200B;**[!UICONTROL 产品设置]**&#x200B;部分中，选择&#x200B;**[!UICONTROL 配置]**。

   ![访问Content Hub上的配置选项](assets/access-content-hub-configuration-ui.png)

## 在Content Hub上管理配置选项 {#manage-configuration-options}

作为管理员，为您的用户管理以下配置选项：

* [导入](#configure-import-options-content-hub)

* [过滤器](#configure-filters-content-hub)

* [资源详情](#configure-asset-details-content-hub)
* [资产卡](#asset-card)

* [搜索](#configure-metadata-search-content-hub)

* [品牌化](#configure-branding-content-hub)

* [过期资产](#expired-assets-content-hub)

* [演绎版](#renditions-content-hub)

* [自定义链接](#configure-custom-links-content-hub)

### 导入 {#configure-import-options-content-hub}

您可以配置在将资源上传或导入到Content Hub门户时向用户显示的元数据字段，例如促销活动名称、关键字、渠道、时间范围、区域等。 若要禁用，请执行以下步骤：

1. 在[配置](#access-configuration-options-content-hub)用户界面上，单击&#x200B;**[!UICONTROL 导入]**。

1. 单击&#x200B;**[!UICONTROL 添加元数据]**。

1. 指定属性的标签，使用&#x200B;**[!UICONTROL 元数据]**&#x200B;字段将其映射到属性，然后选择新资源元数据的输入类型。

1. 单击&#x200B;**[!UICONTROL 必填字段]**&#x200B;切换可让上传新资产时的新元数据字段成为用户必须指定的字段。

1. 单击&#x200B;**[!UICONTROL 确认]**。 新元数据将显示在现有资源属性列表中。

1. 单击&#x200B;**[!UICONTROL 保存]**&#x200B;以应用更改。

同样，在使用&#x200B;**[!UICONTROL 必填字段]**&#x200B;切换上载资产时，您可以单击每个可用属性旁边的![编辑图标](assets/do-not-localize/edit_icon.svg)以编辑标签，使这些字段对用户是必填字段或非必填字段，或者单击“删除”图标以删除任何元数据属性。

如果您需要自动批准添加到Experience Manager Assets存储库的所有资源，以便这些资源立即在Content Hub中可用，请单击&#x200B;**[!UICONTROL 自动批准]**&#x200B;切换开关。 否则，DAM作者或管理员需要手动批准资源，才能在Content Hub上使用这些资源。 默认情况下，切换设置为“关闭”状态。

完成所有修改后单击&#x200B;**[!UICONTROL 保存]**&#x200B;以应用更改。

在Content Hub上![配置UI上传详细信息](assets/configuration-ui-upload-details.png)

在配置用户界面中启用的元数据将显示在资源上传页面上：

在Content Hub上![上载元数据](assets/configuration-ui-add-assets.png)

### 过滤器 {#configure-filters-content-hub}

Content Hub允许管理员配置在搜索资源时显示的过滤器。 执行以下步骤以添加新筛选器：

1. 在[配置](#access-configuration-options-content-hub)用户界面上，单击&#x200B;**[!UICONTROL 筛选器]**。

1. 单击&#x200B;**[!UICONTROL 添加筛选器]**。

1. 指定筛选器的标签，使用&#x200B;**[!UICONTROL 元数据]**&#x200B;字段将其映射到属性，然后选择新筛选器的输入类型。
1. 单击&#x200B;**[!UICONTROL 确认]**。 新筛选器显示在现有筛选器的列表中。

1. 单击&#x200B;**[!UICONTROL 保存]**&#x200B;以应用更改，以便在筛选资产时，新筛选器将显示在“搜索”页面上。

   >[!NOTE]
   >
   仅当存储库中还有另一个资源与筛选条件匹配时，新筛选器才会显示在“搜索”页面上。

同样，您可以单击每个可用筛选器旁边的![编辑图标](assets/do-not-localize/edit_icon.svg)来编辑标签，或者单击删除图标来删除任何现有筛选器。 完成所有修改后单击&#x200B;**[!UICONTROL 保存]**&#x200B;以应用更改。

在Content Hub上![配置UI筛选器](assets/configuration-ui-filters.png)

“搜索”页上将显示在“配置用户界面”中启用的过滤器：

![在Content Hub上搜索](assets/filters-for-search.png)


### 资源详情 {#configure-asset-details-content-hub}

您还可以配置为每个资源显示的资源属性，例如文件名、标题、格式、大小等。 若要禁用，请执行以下步骤：

1. 在[配置](#access-configuration-options-content-hub)用户界面上，单击&#x200B;**[!UICONTROL 资源详细信息]**。

1. 单击&#x200B;**[!UICONTROL 添加元数据]**。

1. 指定属性的标签，使用&#x200B;**[!UICONTROL 元数据]**&#x200B;字段将其映射到属性，然后选择新资源元数据的输入类型。
1. 单击&#x200B;**[!UICONTROL 确认]**。 新元数据将显示在现有资源属性列表中。

1. 单击&#x200B;**[!UICONTROL 保存]**&#x200B;以应用更改，以便在资产详细信息页面上显示新属性。

同样，您可以单击每个可用属性旁边的![编辑图标](assets/do-not-localize/edit_icon.svg)来编辑标签，或者单击删除图标来删除任何现有资源详细信息。 完成所有修改后单击&#x200B;**[!UICONTROL 保存]**&#x200B;以应用更改。

在Content Hub上![配置UI资源详细信息](assets/configuration-ui-asset-details.png)

在“配置用户界面”中启用的属性将显示在“资产详细信息”页面上：

Content Hub上的![资源属性](assets/config-ui-asset-properties.png)

### 资产卡 {#asset-card}

您还可以配置需要在&#x200B;**资产卡**&#x200B;上显示的关键元数据字段，最多可显示6个字段。 若要禁用，请执行以下步骤：

![资源信息卡上的关键元数据](/help/assets/assets/asset-card-key-metadata.png)

1. 在[配置](#access-configuration-options-content-hub)用户界面上，单击&#x200B;**资产卡**。
2. 单击&#x200B;**添加元数据**。 显示&#x200B;**添加资源卡元数据**&#x200B;对话框。
3. 在&#x200B;**标签**&#x200B;字段中指定元数据名称，并在&#x200B;**元数据**&#x200B;字段中选择元数据属性。
4. 单击&#x200B;**确认**，然后单击&#x200B;**保存**以应用更改，以便新属性显示在资源详细信息页面上。
   ![资产卡](/help/assets/assets/asset-card.png)

同样，单击每个可用属性旁边可用的![编辑](/help/assets/assets/edit-content-hub.svg)以进行任何必需的修改，或单击![删除](/help/assets/assets/delete-content-hub.svg)删除任何现有的元数据属性。 完成所有修改后单击&#x200B;**保存**&#x200B;以应用更改。

### 搜索 {#configure-metadata-search-content-hub}

管理员可以定义在用户在Content Hub上指定搜索条件时搜索的元数据字段。 执行以下步骤：

1. 在[配置](#access-configuration-options-content-hub)用户界面上，单击&#x200B;**[!UICONTROL 添加元数据]**。

1. 指定元数据字段并单击&#x200B;**[!UICONTROL 确认]**。

1. 单击&#x200B;**[!UICONTROL 保存]**&#x200B;以应用更改，以便新的元数据属性显示在元数据字段列表中。

同样，您可以单击每个可用元数据属性旁边的![编辑图标](assets/do-not-localize/edit_icon.svg)来编辑该属性，或者单击删除图标来删除任何现有属性。 完成所有修改后单击&#x200B;**[!UICONTROL 保存]**&#x200B;以应用更改。

在Content Hub上![配置UI搜索](assets/configuration-ui-metadata-search.png)


### 品牌化 {#configure-branding-content-hub}

管理员还可以根据您的品牌要求，个性化Content Hub门户横幅上的标题和正文文本。 若要禁用，请执行以下步骤：

1. 在[配置](#access-configuration-options-content-hub)用户界面上，单击&#x200B;**[!UICONTROL 品牌]**。

1. 指定横幅&#x200B;]**的**[!UICONTROL &#x200B;标题文本和横幅&#x200B;]**字段的**[!UICONTROL &#x200B;正文文本。

1. 单击&#x200B;**[!UICONTROL 保存]**&#x200B;以应用更改。

Content Hub上的![配置UI品牌](assets/configuration-ui-branding.png)

在配置用户界面上启用的品牌更新将显示在Content Hub门户横幅上：

Content Hub上的![配置UI品牌](assets/configuration-ui-branding-updates.png)

### 过期资产{#expired-assets-content-hub}

管理员可以控制是否需要在Content Hub上显示过期的资源。 如果过期的资产可见，他们还可以定义用户是否可以下载它们。

默认情况下，Content Hub中不显示过期的资源。

若要禁用，请执行以下步骤：

1. 在[配置](#access-configuration-options-content-hub)用户界面上，单击&#x200B;**[!UICONTROL 过期的Assets]**。

1. 在&#x200B;**[!UICONTROL 可见]**&#x200B;部分中，启用&#x200B;**[!UICONTROL 允许用户查看过期的资源]**&#x200B;切换功能，以便在Content Hub上显示所有过期的资源。

1. 启用资产可见性后，您可以使用&#x200B;**[!UICONTROL 允许用户下载过期的资产]**&#x200B;切换启用或禁用下载过期的资产的功能。

1. 单击&#x200B;**[!UICONTROL 保存]**&#x200B;以应用更改。

   ![Content Hub 上的资产已过期](assets/expired-assets-content-hub.png)

启用资源的可见性后，您可以在Content Hub上查看过期的资源，如下图所示：

![Content Hub 上的资产已过期](assets/view-download-expired-assets.png)

如果管理员启用了下载，则Content Hub用户也可以下载它们，如图像中突出显示的内容。

如果启用了过期资源的可见性，Content Hub还会使用资源卡上的`Expiring in n days`消息突出显示未来15天内过期的资源。

### 演绎版 {#renditions-content-hub}

演绎版是数字资产（如图像、文档等）的自定义版本，专为不同的设备和平台而设计，可确保实现最佳性能。 在Adobe Experience Manager Assets](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/assets-view/renditions)中查看有关[呈现形式的更多信息。

Content Hub允许下载静态演绎版。 静态演绎版是本机生成的资源原始文件的不同表示形式。 示例包括缩略图或移动优化呈现版本。 管理员可以管理和控制资源演绎版的可用性；并管理您是否可以下载原始资源。

若要禁用，请执行以下步骤：

在[配置](#access-configuration-options-content-hub)用户界面上，单击&#x200B;**[!UICONTROL 呈现版本]**。 以下选项可供选择：

* 启用[!UICONTROL 启用静态呈现的可用性]切换功能，使所有静态呈现在Content Hub中可见。

* 启用或禁用&#x200B;**[!UICONTROL 允许用户下载原始资产]**&#x200B;切换开关以控制下载原始资产的可用性。

  ![在Content Hub上配置演绎版](assets/config-renditions.png)

有关如何在Content Hub中查看和下载静态呈现版本的信息，请参阅[在Content Hub中下载资源](/help/assets/download-assets-content-hub.md)。

### 自定义链接 {#configure-custom-links-content-hub}

除了横幅正下方的Content Hub门户上的标准&#x200B;**[!UICONTROL 所有Assets]**、**[!UICONTROL 收藏集]**&#x200B;和&#x200B;**[!UICONTROL 分析]**&#x200B;选项卡外，您还可以添加自定义选项卡。 若要禁用，请执行以下步骤：

1. 在[配置](#access-configuration-options-content-hub)用户界面上，单击&#x200B;**[!UICONTROL 自定义链接]**。

1. 单击&#x200B;**[!UICONTROL 添加链接]**。

1. 在&#x200B;**[!UICONTROL 标签]**&#x200B;和&#x200B;**[!UICONTROL URL]**&#x200B;字段中指定文本。 您定义的标签显示为选项卡，单击该标签时，您可以导航到&#x200B;**[!UICONTROL URL]**&#x200B;字段中定义的URL。

1. 单击&#x200B;**[!UICONTROL 确认]**。

1. 单击&#x200B;**[!UICONTROL 保存]**&#x200B;以应用更改。

同样，您可以单击每个URL旁边的![编辑图标](assets/do-not-localize/edit_icon.svg)来编辑链接，或者单击删除图标来删除任何现有的URL。 完成所有修改后单击&#x200B;**[!UICONTROL 保存]**&#x200B;以应用更改。

Content Hub上的![配置UI自定义链接](assets/configuration-ui-custom-links.png)

自定义链接在Content Hub主页的“分析”选项卡旁边显示为新选项卡。

![Content Hub上的配置UI自定义链接选项卡](assets/configuration-ui-custom-link-tab.png)
