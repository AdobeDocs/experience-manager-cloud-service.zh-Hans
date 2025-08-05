---
title: 配置 Content Hub 用户界面
description: 配置 Content Hub 用户界面
exl-id: e9e22862-9bcd-459a-bcf4-7f376a0b329a
source-git-commit: 4125f6d99c1c1d63b9234d66dc552695bd30e7bc
workflow-type: tm+mt
source-wordcount: '2089'
ht-degree: 10%

---

# 配置 Content Hub 用户界面 {#configure-content-hub-user-interface}

>[!CONTEXTUALHELP]
>id="configure_content_hub"
>title="配置 Content Hub 用户界面"
>abstract="管理员使用 Experience Manager Assets 可以配置 Content Hub 用户界面上可用的选项。根据管理员选择的配置选项，Content Hub 用户可以查看 Content Hub 上的字段。配置选项包括导入资产时的元数据、过滤器、资产属性、搜索资产时的元数据、个性化品牌以及任何自定义链接。"
>additional-url="https://images-tv.adobe.com/mpcv3/4477/74a81d1c-0cfe-41f4-8a06-18ff70604e45_1732023385.854x480at800_h264.mp4" text="观看视频"

<!-- ![Download assets](assets/download-asset.jpg) -->

![在Content Hub上配置资源](assets/configure-assets.png)

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

* [资产详情](#configure-asset-details-content-hub)
* [资产卡](#asset-card)

* [搜索](#configure-metadata-search-content-hub)

* [品牌化](#configure-branding-content-hub)

* [过期资产](#expired-assets-content-hub)

* [演绎版](#renditions-content-hub)

* [自定义链接](#configure-custom-links-content-hub)

* [收藏集和共享](#configure-collections-content-hub)

<!--* [Enable public link sharing](#enable-public-link-sharing)-->

### 导入 {#configure-import-options-content-hub}

您可以配置在将资源上传或导入到Content Hub门户时向用户显示的元数据字段，例如促销活动名称、关键字、渠道、时间范围、区域等。 若要禁用，请执行以下步骤：

1. 在[配置](#access-configuration-options-content-hub)用户界面上，单击&#x200B;**[!UICONTROL 导入]**。

1. 单击&#x200B;**[!UICONTROL 添加元数据]**。

1. 指定属性的标签，使用&#x200B;**[!UICONTROL 元数据]**&#x200B;字段将其映射到属性，然后选择新资源元数据的输入类型。

1. 单击&#x200B;**[!UICONTROL 必填字段]**&#x200B;切换可让上传新资产时的新元数据字段成为用户必须指定的字段。

1. 单击&#x200B;**[!UICONTROL 确认]**。 新元数据将显示在现有资源属性列表中。

1. 单击&#x200B;**[!UICONTROL 保存]**&#x200B;以应用更改。

同样，在使用![必填字段](assets/do-not-localize/edit_icon.svg)切换上载资产时，您可以单击每个可用属性旁边的&#x200B;**[!UICONTROL 编辑图标]**&#x200B;以编辑标签，使这些字段对用户是必填字段或非必填字段，或者单击“删除”图标以删除任何元数据属性。

如果您需要自动批准添加到Experience Manager Assets存储库的所有资源，以便这些资源立即在Content Hub中可用，请单击&#x200B;**[!UICONTROL 自动批准]**&#x200B;切换开关。 否则，DAM作者或管理员需要手动批准资源，才能在Content Hub上使用这些资源。 默认情况下，切换设置为“关闭”状态。

完成所有修改后单击&#x200B;**[!UICONTROL 保存]**&#x200B;以应用更改。

在Content Hub上![配置UI上传详细信息](/help/assets/assets/import-content-hub1.png)

在配置用户界面中启用的元数据将显示在资源上传页面上：
在Content Hub上![上载元数据](assets/add-assets-for-approval1.png)

### 过滤器 {#configure-filters-content-hub}

Content Hub允许管理员配置在搜索资源时显示的过滤器。 执行以下步骤以添加新筛选器：

1. 在[配置](#access-configuration-options-content-hub)用户界面上，单击&#x200B;**[!UICONTROL 筛选器]**。

1. 单击&#x200B;**[!UICONTROL 添加筛选器]**。

1. 指定筛选器的标签，使用&#x200B;**[!UICONTROL 元数据]**&#x200B;字段将其映射到属性，然后选择新筛选器的输入类型。
1. 单击&#x200B;**[!UICONTROL 确认]**。 新筛选器显示在现有筛选器的列表中。

1. 单击&#x200B;**[!UICONTROL 保存]**&#x200B;以应用更改，以便在筛选资产时，新筛选器将显示在“搜索”页面上。

   >[!NOTE]
   >
   >仅当存储库中至少有一个资源与筛选条件匹配时，新筛选器才会显示在“搜索”页面上。

同样，您可以单击每个可用筛选器旁边的![编辑图标](assets/do-not-localize/edit_icon.svg)来编辑标签，或者单击删除图标来删除任何现有筛选器。 完成所有修改后单击&#x200B;**[!UICONTROL 保存]**&#x200B;以应用更改。
在Content Hub上![配置UI筛选器](assets/configuration-filter1.png)

“搜索”页上将显示在“配置用户界面”中启用的过滤器：
![在Content Hub上搜索](assets/content-hub-filters1.png)

### 资产详情 {#configure-asset-details-content-hub}

您还可以配置为每个资源显示的资源属性，例如文件名、标题、格式、大小等。 若要禁用，请执行以下步骤：

1. 在[配置](#access-configuration-options-content-hub)用户界面上，单击&#x200B;**[!UICONTROL 资源详细信息]**。

1. 单击&#x200B;**[!UICONTROL 添加元数据]**。

1. 指定属性的标签，使用&#x200B;**[!UICONTROL 元数据]**&#x200B;字段将其映射到属性，然后选择新资源元数据的输入类型。
1. 单击&#x200B;**[!UICONTROL 确认]**。 新元数据将显示在现有资源属性列表中。

1. 单击&#x200B;**[!UICONTROL 保存]**&#x200B;以应用更改，以便在资产详细信息页面上显示新属性。

同样，您可以单击每个可用属性旁边的![编辑图标](assets/do-not-localize/edit_icon.svg)来编辑标签，或者单击删除图标来删除任何现有资源详细信息。 完成所有修改后单击&#x200B;**[!UICONTROL 保存]**&#x200B;以应用更改。

在Content Hub上![配置UI资源详细信息](assets/configuration-asset-details.png)

在“配置用户界面”中启用的属性将显示在“资产详细信息”页面上：

Content Hub上的![资源属性](assets/asset-details-page-content-hub1.png)

### 资产卡 {#asset-card}

您还可以配置需要在&#x200B;**资产卡**&#x200B;上显示的密钥元数据属性，最多可显示6个字段。
资产卡上的![密钥元数据](/help/assets/assets/asset-card-metadata.png)
执行以下步骤可配置元数据属性以将其显示在&#x200B;**[!UICONTROL 资产卡片]**&#x200B;上：

1. 在[配置](#access-configuration-options-content-hub)用户界面上，单击&#x200B;**资产卡**。
2. 单击&#x200B;**添加元数据**。 显示&#x200B;**添加资源卡元数据**&#x200B;对话框。
3. 在&#x200B;**标签**&#x200B;字段中指定元数据名称，并在&#x200B;**元数据**&#x200B;字段中选择元数据属性。
4. 单击&#x200B;**确认**，然后单击&#x200B;**保存**&#x200B;以应用更改，以便新属性显示在资源详细信息页面上。
   ![资产卡](/help/assets/assets/configuration-asset-card1.png)
同样，单击每个可用属性旁边可用的![编辑](/help/assets/assets/edit-content-hub.svg)以进行任何必需的修改，或单击![删除](/help/assets/assets/delete-content-hub.svg)删除任何现有的元数据属性。 完成所有修改后单击&#x200B;**保存**&#x200B;以应用更改。

### 搜索 {#configure-metadata-search-content-hub}

管理员可以定义在用户在Content Hub上指定搜索条件时搜索的元数据字段。 执行以下步骤：

1. 在[配置](#access-configuration-options-content-hub)用户界面上，单击&#x200B;**[!UICONTROL 添加元数据]**。

1. 指定元数据字段并单击&#x200B;**[!UICONTROL 确认]**。

1. 单击&#x200B;**[!UICONTROL 保存]**&#x200B;以应用更改，以便新的元数据属性显示在元数据字段列表中。

同样，您可以单击每个可用元数据属性旁边的![编辑图标](assets/do-not-localize/edit_icon.svg)来编辑该属性，或者单击删除图标来删除任何现有属性。 完成所有修改后单击&#x200B;**[!UICONTROL 保存]**&#x200B;以应用更改。
在Content Hub上![配置UI搜索](assets/configuration-search.png)

### 品牌化 {#configure-branding-content-hub}

作为管理员，自定义您的[!DNL Content Hub]门户以满足您的品牌要求。
![重置默认值](/help/assets/assets/reset-default-content-hub.png)
在![品牌](/help/assets/assets/ColorPalette.svg) **[!UICONTROL 品牌]**&#x200B;页面上，使用&#x200B;**[!UICONTROL 横幅]**、**[!UICONTROL 颜色]**&#x200B;和&#x200B;**[!UICONTROL 横幅图像]**&#x200B;部分执行以下自定义设置：

1. [从[!UICONTROL 横幅图像]部分更改横幅图像](#Change-the-banner-image)
1. [更新横幅上的标题和正文文本，并更改[!UICONTROL 横幅]部分的文本颜色](#Add-title-and-body-text-to-your-banner-and-change-the-text-color)
1. [从[!UICONTROL 颜色]部分更改主要颜色和次要颜色，以应用与品牌主题一致的颜色方案](#Change-the-primary-and-secondary-color)

选择&#x200B;**[!UICONTROL 重置默认值]**&#x200B;选项以还原您的更改并还原默认主题。

#### 更改横幅图像{#Change-the-banner-image}

在![品牌](/help/assets/assets/ColorPalette.svg) **[!UICONTROL 品牌]**&#x200B;页面上，执行以下步骤以更改[!DNL Content Hub]部署的横幅图像：

1. 单击![选择图像](/help/assets/assets/Browse.svg) **[!UICONTROL 从图库中选择]**&#x200B;以使用“资产选择器”对话框选择横幅图像。 资源选择器仅显示批准的图像。
1. 选择图像，单击&#x200B;**[!UICONTROL 选择]**，然后单击&#x200B;**[!UICONTROL 保存]**&#x200B;以将其显示为[!DNL Content Hub]部署的横幅图像。
   ![横幅图像](/help/assets/assets/banner-image-content-hub1.png)

#### 将标题和正文文本添加到横幅并更改文本颜色{#Add-title-and-body-text-to-your-banner-and-change-the-text-color}

在![品牌](/help/assets/assets/ColorPalette.svg) **[!UICONTROL 品牌]**&#x200B;页面上，使用&#x200B;**[!UICONTROL 横幅]**&#x200B;部分中的相应字段将标题和正文添加到横幅中。
单击&#x200B;**[!UICONTROL 横幅文本颜色]**&#x200B;旁边的方框可从横幅文本的拾色器中选择文本颜色，或在拾色器方框旁边的字段中指定颜色的十六进制代码。
![横幅文本内容中心](/help/assets/assets/banner-text-content-hub.png)

#### 更改主颜色和次颜色{#Change-the-primary-and-secondary-color}

在![品牌](/help/assets/assets/ColorPalette.svg) **[!UICONTROL 品牌]**&#x200B;页面上，使用&#x200B;**[!UICONTROL 颜色]**&#x200B;部分设置主要颜色和次要颜色，方法为使用拾色器选择颜色或定义颜色的十六进制代码。 这些颜色可设置UI元素的背景、文本和图标颜色，以使您的[!DNL Content Hub] UI与品牌主题保持一致。
![主颜色和辅助颜色](/help/assets/assets/primary-secondary-color-content-hub1.png)
**[!UICONTROL 主颜色]：**&#x200B;主颜色方案适用于选择操作、交互元素（如复选框、搜索栏）以及跨[!DNL Content Hub]切换开关（包括[!DNL Content Hub]主页和[!UICONTROL 配置]页）。 它还适用于主[!DNL Content Hub]界面上可用的操作选项，如&#x200B;**[!UICONTROL 所有Assets]**&#x200B;和&#x200B;**[!UICONTROL 收藏集]**&#x200B;页面上可用的选项。

**[!UICONTROL 次要颜色]：**&#x200B;在[!DNL Content Hub]主页上，次要颜色方案应用于对话框中可用的UI选项和输入字段。 它适用于[!UICONTROL 配置]页面上可用的所有配置菜单选项，但选择操作、复选框、搜索栏和切换开关除外。

### 资产可见性{#asset-visibility-content-hub}

管理员可以控制是否需要在Content Hub上显示过期的资源。 如果过期的资产可见，他们还可以定义用户是否可以下载它们。

默认情况下，Content Hub中不显示过期的资源。

若要禁用，请执行以下步骤：

1. 在[配置](#access-configuration-options-content-hub)用户界面上，单击&#x200B;**[!UICONTROL 资产可见性]**。

1. 在&#x200B;**[!UICONTROL 可见]**&#x200B;部分中，启用&#x200B;**[!UICONTROL 允许用户查看过期的资源]**&#x200B;切换功能，以便在Content Hub上显示所有过期的资源。

1. 启用资产可见性后，您可以使用&#x200B;**[!UICONTROL 允许用户下载过期的资产]**&#x200B;切换启用或禁用下载过期的资产的功能。
1. 启用&#x200B;**[!UICONTROL 允许用户查看已批准交付的资产]**&#x200B;切换功能，在Content Hub中显示已批准交付的所有资产。
1. 单击&#x200B;**[!UICONTROL 保存]**&#x200B;以应用更改。

   ![Content Hub 上的资产已过期](assets/asset-visibility-content-hub1.png)

启用资源的可见性后，您可以在Content Hub上查看过期的资源，如下图所示：

![Content Hub 上的资产已过期](assets/view-download-expired-assets.png)

如果管理员启用了下载，则Content Hub用户也可以下载它们，如图像中突出显示的内容。

如果启用了过期资源的可见性，Content Hub还会使用资源卡上的`Expiring in n days`消息突出显示未来15天内过期的资源。

### 演绎版 {#renditions-content-hub}

演绎版是数字资产（如图像、文档等）的自定义版本，专为不同的设备和平台而设计，可确保实现最佳性能。 在Adobe Experience Manager Assets[中查看有关](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/assets/assets-view/renditions)呈现形式的更多信息。

若要禁用，请执行以下步骤：

在[配置](#access-configuration-options-content-hub)用户界面上，单击&#x200B;**[!UICONTROL 呈现版本]**。 以下选项可供选择：

* 启用[!UICONTROL 启用演绎版可用性]切换功能，使所有演绎版在Content Hub上可见。

* 启用或禁用&#x200B;**[!UICONTROL 允许用户下载原始资产]**&#x200B;切换开关以控制下载原始资产的可用性。

  ![在Content Hub上配置演绎版](assets/configuration-renditions1.png)

有关如何在Content Hub中查看和下载演绎版的信息，请参阅[在Content Hub中下载资源](/help/assets/download-assets-content-hub.md)。

### 自定义链接 {#configure-custom-links-content-hub}

除了横幅正下方的Content Hub门户上的标准&#x200B;**[!UICONTROL 所有Assets]**、**[!UICONTROL 收藏集]**&#x200B;和&#x200B;**[!UICONTROL 分析]**&#x200B;选项卡外，您还可以添加自定义选项卡。 若要禁用，请执行以下步骤：

1. 在[配置](#access-configuration-options-content-hub)用户界面上，单击&#x200B;**[!UICONTROL 自定义链接]**。

1. 单击&#x200B;**[!UICONTROL 添加链接]**。

1. 在&#x200B;**[!UICONTROL 标签]**&#x200B;和&#x200B;**[!UICONTROL URL]**&#x200B;字段中指定文本。 您定义的标签显示为选项卡，单击该标签时，您可以导航到&#x200B;**[!UICONTROL URL]**&#x200B;字段中定义的URL。

1. 单击&#x200B;**[!UICONTROL 确认]**。

1. 单击&#x200B;**[!UICONTROL 保存]**&#x200B;以应用更改。

同样，您可以单击每个URL旁边的![编辑图标](assets/do-not-localize/edit_icon.svg)来编辑链接，或者单击删除图标来删除任何现有的URL。 完成所有修改后单击&#x200B;**[!UICONTROL 保存]**&#x200B;以应用更改。
Content Hub上的![配置UI自定义链接](assets/configuration-custom-links1.png)

自定义链接在Content Hub主页的“分析”选项卡旁边显示为新选项卡。
![Content Hub上的配置UI自定义链接选项卡](assets/configuration-ui-custom-link-tab.png)

### 收藏集和共享 {#configure-collections-content-hub}

管理员可以在创建收藏集时定义用户权限。 要启用这些设置，请执行以下步骤：

1. 在[配置](#access-configuration-options-content-hub)用户界面上，单击&#x200B;**[!UICONTROL 收藏集]**。

1. 启用&#x200B;**[!UICONTROL 启用公共链接]**&#x200B;切换功能，以允许创建外部用户无需登录到Content Hub即可访问和下载资源的公共链接。

1. 启用&#x200B;**[!UICONTROL 仅查看收藏集]**&#x200B;切换功能，允许所有人访问但只有创建者和管理员才能编辑的收藏集。

1. 启用&#x200B;**[!UICONTROL 公共收藏集]**&#x200B;切换功能，以允许所有人都可以访问和编辑收藏集。 如果禁用&#x200B;**[!UICONTROL 仅查看收藏集]**&#x200B;和&#x200B;**[!UICONTROL 公共收藏集]**&#x200B;切换，则默认情况下，非管理员用户只能创建专用收藏集。

1. 单击&#x200B;**[!UICONTROL 保存]**&#x200B;以应用更改。

   Content Hub上的![配置集合选项卡](assets/collections-and-sharing1.png)

<!--
### Enable public link sharing {#enable-public-link-sharing}

Enable the following setting on the Configurations user interface to allow Content Hub users to generate a public link:

1. On the [Configurations](#access-configuration-options-content-hub) user interface, click **[!UICONTROL Collections and Sharing]**.

1. Enable the **[!UICONTROL Enable Public Link]** toggle and click **[!UICONTROL Save]** to apply the changes.

    ![Enable public link sharing in Content Hub](assets/enable-public-link-sharing-tab.png)

-->

了解有关[在 [!DNL Content Hub]](share-assets-content-hub.md)中共享资产的更多信息。