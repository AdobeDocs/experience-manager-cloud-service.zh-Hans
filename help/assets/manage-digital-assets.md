---
title: 管理数字资产
description: 了解各种资源管理和编辑方法
contentOwner: AG
mini-toc-levels: 3
feature: Asset Management, Publishing,Collaboration, Asset Processing
role: User, Architect, Admin
exl-id: 51a26764-ac2b-4225-8d27-42a7fd906183
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '4277'
ht-degree: 10%

---

# 管理资源 {#manage-assets}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/manage-assets.html?lang=zh-Hans) |
| AEM as a Cloud Service | 本文 |

本文介绍了如何在[!DNL Adobe Experience Manager Assets]中管理和编辑资源。 要管理[!DNL Content Fragments]，请参阅[[!DNL Content Fragments]](content-fragments/content-fragments.md)资源。

## 创建文件夹 {#creating-folders}

组织资产集合（例如，所有`Nature`图像）时，您可以创建文件夹以将它们保持在一起。 您可以使用文件夹对资源进行分类和组织。 [!DNL Experience Manager Assets]不要求您组织文件夹中的资源才能更好地工作。

>[!NOTE]
>
>* 在共享到Experience Cloud时，不支持共享类型为`sling:OrderedFolder`的Assets文件夹。 如果要共享文件夹，请勿在创建文件夹时选择[!UICONTROL 已排序]。
>* Experience Manager不允许使用`subassets`单词作为文件夹的名称。 它是为包含复合资产的子资产的节点保留的关键字

1. 导航到数字资产文件夹中要创建文件夹的位置。 在菜单中，单击&#x200B;**[!UICONTROL 创建]**。 选择&#x200B;**[!UICONTROL 新文件夹]**。
1. 在&#x200B;**[!UICONTROL 标题]**&#x200B;字段中，提供文件夹名称。 默认情况下，DAM使用您提供的标题作为文件夹名称。 创建文件夹后，您可以覆盖默认文件夹名称并指定其他文件夹名称。
1. 单击&#x200B;**[!UICONTROL 创建]**。您的文件夹会显示在数字资产文件夹中。

不支持以下（以空格分隔的）字符：

* 资源文件名不能包含以下任一字符： `* / : [ \\ ] | # % { } ? &`
* 资产文件夹名称不能包含以下任一字符： `* / : [ \\ ] | # % { } ? \" . ^ ; + & \t`

## 上传资产 {#uploading-assets}

请参阅[将数字资源添加到Experience Manager](add-assets.md)。

## 提取ZIP存档 {#extract-zip-archives}

选择Experience Manager中管理的ZIP存档，并将文件直接提取到Experience Manager中而不下载它们。

要解压缩ZIP文件，请执行以下步骤：

1. 选择ZIP文件类型。
1. 单击操作栏上可用的&#x200B;**[!UICONTROL 提取存档]**&#x200B;选项。
1. 选择文件夹，您需要在该文件夹中保存压缩文件夹中可用的已提取资产。
1. 单击&#x200B;**[!UICONTROL 下一步]**。
1. 选择相应的行为来处理提取期间出现的文件名冲突。 您可以选择创建现有资源的版本，替换该资源，将两个资源都保留在目标文件夹中，或者跳过新资源的提取。
1. 单击&#x200B;**[!UICONTROL 提取]**。 Zip提取过程开始。 该过程完成后，您可以在目标文件夹中查看提取的资产。

   ![zip提取](assets/zip-extraction.png)

>[!NOTE]
>
>* 支持的最大ZIP文件大小为15 GB。
>* 一次最多可以提取三个ZIP文件。

## 预览资源 {#previewing-assets}

要预览资源，请执行以下步骤。

1. 从Assets用户界面中，导航到要预览的资源位置。
1. 选择所需的资产以将其打开。

1. 在预览模式下，缩放选项可用于[支持的图像类型](/help/assets/file-format-support.md)（通过交互式编辑）。

   要放大资产，请选择`+`（或选择资产上的放大镜）。 要缩小，请选择`-`。 放大时，可以通过平移仔细查看图像的任意区域。 重置缩放箭头将您带回原始视图。

   选择&#x200B;**[!UICONTROL 重置]**&#x200B;以将视图重置为原始大小。

## 编辑属性 {#editing-properties}

1. 导航到要编辑其元数据的资源的位置。

1. 选择资源，然后从工具栏中选择&#x200B;**[!UICONTROL 属性]**&#x200B;以查看资源属性。 或者，选择资产卡上的&#x200B;**[!UICONTROL 属性]**&#x200B;快速操作。

   ![properties_quickaction](assets/properties_quickaction.png)

1. 在[!UICONTROL 属性]页面中，编辑各种选项卡下的元数据属性。 例如，在&#x200B;**[!UICONTROL 基本]**&#x200B;选项卡下，编辑标题、描述等。

   >[!NOTE]
   >
   >[!UICONTROL 属性]页面的布局和可用的元数据属性取决于基础元数据架构。 要了解如何修改[!UICONTROL 属性]页面的布局，请参阅[元数据架构](/help/assets/metadata-schemas.md)。

1. 要计划资产激活的特定日期/时间，请使用&#x200B;**[!UICONTROL 开始时间]**&#x200B;字段旁边的日期选取器。

   ![日期选取器](assets/date-picker.png)

1. 要在特定持续时间后停用资产，请从&#x200B;**[!UICONTROL 关闭时间]**&#x200B;字段旁边的日期选取器中选择停用日期/时间。 停用日期应晚于资源的激活日期。 在[!UICONTROL 结束时间]后，无法通过Assets Web界面或HTTP API访问资源及其演绎版。

   <!--![chlimage_1-218](assets/chlimage_1-218.png)
1. 在&#x200B;**[!UICONTROL 标记]**&#x200B;字段中，选择一个或多个标记。 要添加自定义标记，请在框中键入标记的名称，然后选择`Enter`键。 新标记保存在[!DNL Experience Manager]中。

   YouTube需要使用Tags才能发布，并且具有YouTube链接（如果能够找到合适的链接）。

   >[!NOTE]
   >
   > 要创建标记，您必须在CRX存储库中的`/content/cq:tags/default`路径处具有写入权限。

1. 选择&#x200B;**[!UICONTROL 保存并关闭]**。

1. 导航到Assets用户界面。 编辑后的元数据属性（包括标题、描述和标记）将显示在卡片视图的资产卡片上，以及列表视图的相关列下。

<!-- TBD: Uncomment after verification for Dec release.

## View asset usage and references {#usage-and-references}

[!DNL Experience Manager] lets you track statistics about usage of a digital asset. The usage statistics include the following:

    * Number of times the asset was viewed or downloaded
    * Channels/devices through which the asset was used
    * Creative solutions where the asset was recently used

To view usage statistics for an asset, in the [!UICONTROL Properties] page, click the **[!UICONTROL Insights]** tab. For more details, see [Assets Insights](assets-insights.md).

[!DNL Experience Manager] also lets you check all the incoming references to an asset, that is, the usage of an asset in remote [!DNL Sites] and in compound assets. Authors of webpages on [!DNL Experience Manager Sites] deployment can use an asset on a remote [!DNL Assets] deployment using the Connected Assets functionality. The [!UICONTROL References] tab in an asset's [!UICONTROL Properties] page lists the local and remote references of the asset. That is, the use of assets in compound assets in [!DNL Assets] and its use in remote [!DNL Sites] pages.

-->

## 复制资产 {#copying-assets}

复制资产或文件夹时，将会复制整个资产或文件夹及其内容结构。 在目标位置复制复制的资产或文件夹。 源位置的资产不会更改。

资产的特定副本特有的几个属性不会结转。 一些示例包括：

* 资产ID、创建日期和时间以及版本和版本历史记录。 这些属性中的某些由属性`jcr:uuid`、`jcr:created`和`cq:name`指示。

* 每个资源及其每个演绎版的创建时间和引用路径都是唯一的。

其他属性和元数据信息将保留。 复制资产时，不会创建部分副本。

1. 从Assets UI中，选择一个或多个资源，然后从工具栏中选择&#x200B;**[!UICONTROL 复制]**&#x200B;图标。 或者，从资产卡中选择&#x200B;**[!UICONTROL 复制]** ![复制_图标](assets/copy_icon.png)快速操作。

   >[!NOTE]
   >
   >如果您使用[!UICONTROL 复制]快速操作，则一次只能复制一个资产。

1. 导航到要复制资产的位置。

   >[!NOTE]
   >
   >如果您在同一位置复制资产，[!DNL Experience Manager]将自动生成该名称的变体。 例如，如果您复制标题为`Square`的资产，[!DNL Experience Manager]会自动为其副本生成标题为`Square1`。

1. 单击工具栏中的&#x200B;**[!UICONTROL 粘贴]**&#x200B;资源图标。 Assets将会复制到此位置。

   <!--![chlimage_1-219](assets/chlimage_1-219.png)-->

   >[!NOTE]
   >
   >在粘贴操作完成之前，**[!UICONTROL 粘贴]**&#x200B;图标在工具栏中可用。

### 移动或重命名资源 {#moving-or-renaming-assets}

1. 导航到要移动的资产的位置。

1. 选择资源，然后从工具栏中选择&#x200B;**[!UICONTROL 移动]**&#x200B;图标![move_icon](assets/move_icon.png)。

1. 在“移动Assets”向导中，执行以下操作之一：

   * 在移动资源后指定资源的名称。 然后选择&#x200B;**[!UICONTROL 下一步]**&#x200B;以继续。

   * 选择&#x200B;**[!UICONTROL 取消]**&#x200B;以停止进程。

   >[!NOTE]
   >
   >* 如果新位置没有使用该名称的资源，则可以为该资源指定相同的名称。 但是，如果将资产移动到具有相同名称的资产存在的位置，则应该使用其他名称。 如果使用相同的名称，系统会自动生成该名称的变体。 例如，如果资产的名称为Square，则系统会为其副本生成名称Square1。
   >* 重命名时，文件名中不允许使用空格。

1. 在&#x200B;**[!UICONTROL 选择目标]**&#x200B;对话框中，执行以下操作之一：

   * 导航到资源的新位置，然后选择&#x200B;**[!UICONTROL 下一步]**&#x200B;以继续。

   * 选择&#x200B;**[!UICONTROL 返回]**&#x200B;以返回&#x200B;**[!UICONTROL 重命名]**&#x200B;屏幕。

1. 如果要移动的资产具有任何引用页面、资产或收藏集，则&#x200B;**[!UICONTROL 调整引用]**&#x200B;选项卡将出现在&#x200B;**[!UICONTROL 选择目标]**&#x200B;选项卡旁边。

   在&#x200B;**[!UICONTROL 调整引用]**&#x200B;屏幕中执行以下操作之一：

   * 指定基于新详细信息要调整的引用，然后选择&#x200B;**[!UICONTROL 移动]**&#x200B;以继续。

   * 在&#x200B;**[!UICONTROL 调整]**&#x200B;列中，选择/取消选择对资源的引用。
   * 选择&#x200B;**[!UICONTROL 返回]**&#x200B;以返回&#x200B;**[!UICONTROL 选择目标]**&#x200B;屏幕。

   * 选择&#x200B;**[!UICONTROL 取消]**&#x200B;以停止移动操作。

   如果不更新引用，它们将继续指向资产的上一个路径。 如果调整引用，它们将会更新为新的资产路径。

### 管理节目 {#managing-renditions}

1. 您可以添加或删除资源的演绎版，但原始演绎版除外。 导航到要添加或删除演绎版的资源的位置。

1. 选择资产以打开其资产页面。

   <!--![chlimage_1-220](assets/chlimage_1-220.png)-->

1. 选择GlobalNav图标，然后从列表中选择&#x200B;**[!UICONTROL 呈现版本]**。

   ![renditions_menu](assets/renditions_menu.png)

1. 在&#x200B;**[!UICONTROL 演绎版]**&#x200B;面板中，查看为资源生成的演绎版列表。

   ![renditions_panel](assets/renditions_panel.png)

   >[!NOTE]
   >
   >默认情况下，[!DNL Experience Manager Assets]不会在预览模式下显示资源的原始演绎版。 如果您是管理员，则可以使用叠加将[!DNL Assets]配置为在预览模式下显示原始演绎版。

1. 选择一个演绎版以查看或删除该演绎版。

   **正在删除节目**

   从&#x200B;**[!UICONTROL 呈现版本]**&#x200B;面板中选择呈现版本，然后从工具栏中选择&#x200B;**[!UICONTROL 删除呈现版本]**&#x200B;图标。 资产处理完成后无法批量删除演绎版。 对于单个资源，您可以从用户界面手动删除演绎版。 对于多个资源，您可以自定义[!DNL Experience Manager]以删除特定演绎版，或删除资源并重新上传已删除的资源。

   ![delete_renditionicon](assets/delete_renditionicon.png)

   **正在上传新演绎版**

   导航到资源的资源详细信息页面，然后选择工具栏中的&#x200B;**[!UICONTROL 添加演绎版]**&#x200B;图标以上传资源的新演绎版。

   <!--![chlimage_1-221](assets/chlimage_1-221.png)-->

   >[!NOTE]
   >
   >如果从&#x200B;**[!UICONTROL “演绎版”]**&#x200B;面板选择演绎版，则工具栏更改上下文并仅显示与该演绎版相关的那些操作。不显示“上传演绎版”图标等选项。 要在工具栏中查看这些选项，请导航到资产的详细信息页面。

   您可以为希望在图像或视频资源的详细信息页面中显示的演绎版配置尺寸。 根据您指定的维度，Assets将显示具有精确或最接近维度的演绎版。

   无法创建具有以下前缀的演绎版，因为这些前缀是Adobe的内部前缀：

   * cq5

   * cqdam

   * cq5dam

   要在资源详细信息级别配置图像的演绎版尺寸，请叠加 `renditionpicker` 节点 (`libs/dam/gui/content/assets/assetpage/jcr:content/body/content/content/items/assetdetail/items/col1/items/assetview/renditionpicker`) 并配置宽度属性的值。配置属性&#x200B;**[!UICONTROL 大小（长）(以 KB 计）]**&#x200B;代替宽度，以根据图像大小在资源详细信息页面上自定义演绎版。对于基于大小的自定义，如果匹配的演绎版的大小大于原始演绎版，则属性 `preferOriginal` 将首选项分配给原始演绎版。

   同样，您可以通过叠加`libs/dam/gui/content/assets/annotate/jcr:content/body/content/content/items/content/renditionpicker`来自定义注释页面图像。

   <!--![chlimage_1-222](assets/chlimage_1-222.png)-->

   要为视频资源配置演绎版维度，请导航到CRX存储库中位置`/libs/dam/gui/content/assets/assetpage/jcr:content/body/content/content/items/assetdetail/items/col1/items/assetview/videopicker`的`videopicker`节点，覆盖该节点，然后编辑相应的属性。

   >[!NOTE]
   >
   >仅当浏览器具有与HTML5兼容的视频格式时，才支持视频注释。 此外，根据浏览器的不同，支持不同的视频格式。 但是，视频注释尚不支持MXF视频格式。

## 删除资源 {#delete-assets}

要从其他页面解析或移除传入引用，请在删除资产之前更新相关引用。

此外，使用叠加禁用强制删除按钮，以禁止用户删除引用的资产并留下断开的链接。

1. 导航到要删除的资源的位置。

1. 选择资源，然后单击工具栏中的&#x200B;**[!UICONTROL 删除]** ![删除图标](assets/do-not-localize/delete-icon.png)。

1. 在确认对话框中，单击：

   * **[!UICONTROL 取消]**&#x200B;以停止操作
   * **[!UICONTROL 删除]**&#x200B;可确认操作：

      * 如果资产没有引用，则会删除资产。
      * 如果该资产具有引用，则会出现一条错误消息，通知您&#x200B;**[!UICONTROL 一个或多个资产被引用]**。 您可以选择&#x200B;**[!UICONTROL 强制删除]**&#x200B;或&#x200B;**[!UICONTROL 取消]**。

   >[!NOTE]
   >
   >您需要dam/asset的删除权限才能删除资产。 如果只有修改权限，则只能编辑资源元数据并向资源添加注释。 但是，无法删除资源或其元数据。

   >[!NOTE]
   >
   >要从其他页面解析或移除传入引用，请在删除资产之前更新相关引用。 您可以禁止删除引用的资产，因为它会导致链接断开。 使用覆盖禁用强制删除按钮。

## 下载资产 {#download-assets}

请参阅[从 [!DNL Experience Manager]](/help/assets/download-assets-from-aem.md)下载资源。

## 发布或取消发布资源 {#publish-assets}

1. 导航到要发布或者要从发布环境中移除（取消发布）的资源或资源文件夹的位置。

1. 选择要发布或取消发布的资源或文件夹，然后从工具栏中选择&#x200B;**[!UICONTROL 管理发布]** ![管理发布选项](assets/do-not-localize/globe-publication.png)选项。 或者，要快速发布，请从工具栏中选择&#x200B;**[!UICONTROL 快速发布]**&#x200B;选项。 如果要发布的文件夹包含空文件夹，则不会发布该空文件夹。

1. 根据需要选择&#x200B;**[!UICONTROL 发布]**&#x200B;或&#x200B;**[!UICONTROL 取消发布]**&#x200B;选项。

   ![取消发布操作](assets/unpublish_action.png)
   *图：发布和取消发布选项以及计划选项。*

1. 选择&#x200B;**[!UICONTROL 立即]**&#x200B;对资产执行操作，或选择&#x200B;**[!UICONTROL 稍后]**&#x200B;安排操作。 如果选择&#x200B;**[!UICONTROL 稍后]**&#x200B;选项，请选择日期和时间。 单击&#x200B;**[!UICONTROL 下一步]**。

1. 发布时，如果资产引用了其他资产，则向导中会列出其引用。 仅显示自上次发布以来未发布或修改的引用。 选择要发布的引用。

1. 取消发布时，如果资产引用了其他资产，请选择要取消发布的引用。 单击&#x200B;**[!UICONTROL 取消发布]**。在确认对话框中，单击&#x200B;**[!UICONTROL 取消]**&#x200B;以停止操作，或单击&#x200B;**[!UICONTROL 取消发布]**&#x200B;以确认在指定日期取消发布资源。

了解以下与发布或取消发布资产或文件夹相关的限制和提示：

* [!UICONTROL 管理发布]的选项仅对具有复制权限的用户帐户可用。
* 取消发布复杂资产时，请仅取消发布资产。 避免取消发布引用，因为其他已发布的资产可能会引用这些引用。
* 未发布空文件夹。
* 如果发布正在处理的资源，则仅发布原始内容。 缺少节目。 等待处理完成，然后在处理完成后发布或重新发布资产。

## 已关闭的用户组 {#closed-user-group}

封闭用户组(CUG)用于限制对从[!DNL Experience Manager]发布的特定资源文件夹的访问。 如果为文件夹创建CUG，则对该文件夹（包括文件夹资源和子文件夹）的访问权限将仅限于分配的成员或组。 要访问该文件夹，用户必须使用其安全凭据登录。

CUG是限制对资源的访问权限的额外方法。 您还可以配置文件夹的登录页面。

1. 从Assets UI中选择文件夹，然后从工具栏中选择属性图标以显示属性页面。
1. 从&#x200B;**[!UICONTROL 权限]**&#x200B;选项卡，在&#x200B;**[!UICONTROL 已关闭的用户组]**&#x200B;下添加成员或组。

   ![add_user](assets/add_user.png)

1. 要在用户访问该文件夹时显示登录屏幕，请选择&#x200B;**[!UICONTROL 启用]**&#x200B;选项。 然后，在[!DNL Experience Manager]中选择登录页面的路径，并保存更改。

   ![登录页面](assets/login_page.png)

   >[!NOTE]
   >
   >如果未指定登录页面的路径，[!DNL Experience Manager]会在发布实例中显示默认登录页面。

1. 发布文件夹，然后尝试从发布实例访问它。 将显示登录屏幕。
1. 如果您是CUG成员，请输入安全凭据。 [!DNL Experience Manager]验证您之后将显示文件夹。

## 搜索资产 {#search-assets}

搜索资产是使用数字资产管理系统的核心，无论它是供创意人员进一步使用、供商业用户和营销人员稳健管理资产，还是DAM管理员进行管理。

有关简单、高级和自定义搜索以发现和使用最合适的资源，请参阅[在 [!DNL Experience Manager]](/help/assets/search-assets.md)中搜索资源。

## 快速操作 {#quick-actions}

快速操作图标一次可用于单个资源。 根据您的设备，执行以下操作以显示快速操作图标：

* 触控设备：触控并按住。 例如，在iPad上，您可以选择并按住资产，以便显示快速操作。
* 非触控设备：悬停指针。 例如，在桌面设备上，如果将指针悬停在资产缩略图上，则会显示快速操作栏。

<!-- Hiding this topic via cqdoc-18707

## Edit images {#editing-images}

The editing tools in the [!DNL Experience Manager Assets] interface let you perform small editing jobs on image assets. You can crop, rotate, flip, and perform other editing jobs on images. You can also add image maps to assets.

>[!NOTE]
>
>For some components, the Full Screen mode has additional options available.

1. Do one of the following to open an asset in edit mode:

    * Select the asset and then select the **[!UICONTROL Edit]** icon in the toolbar.
    * Select the **[!UICONTROL Edit]** icon that appears on an asset in the Card view.
    * In the asset page, select the **[!UICONTROL Edit]** icon in the toolbar.

   ![edit_icon](assets/edit_icon.png)

1. To crop the image, select the **Crop** icon.

   ![chlimage_1-226](assets/chlimage_1-226.png)

1. Select the desired option from the list. The crop area appears on the image based on the option you choose. The **Free Hand** option lets you crop the image without any aspect ratio restrictions.

   ![chlimage_1-227](assets/chlimage_1-227.png)

1. Select the area to be cropped, and resize or reposition it on the image.
1. Use the **Finish** icon (top right corner) to crop the image. Clicking the **Finish** icon also triggers the regeneration of renditions.

   ![chlimage_1-228](assets/chlimage_1-228.png)

1. Use the **Undo** and **Redo** icons on the top right to revert to the uncropped image or retain the cropped image, respectively.

   ![chlimage_1-229](assets/chlimage_1-229.png)

1. Select the appropriate Rotate icon to rotate the image clockwise or anti-clockwise.

   ![chlimage_1-230](assets/chlimage_1-230.png)

1. Select the appropriate Flip icon to flip the image horizontally or vertically.

   ![chlimage_1-231](assets/chlimage_1-231.png)

1. Select the **Finish** icon to save the changes.

   ![chlimage_1-232](assets/chlimage_1-232.png)

>[!NOTE]
>
>Image editing is supported for BMP, GIF, PNG, and JPEG files formats.

>[!NOTE]
>
>To edit a TXT file, set **Day CQ Link Externalizer** from Configuration Manager.
-->

## 时间线 {#timeline}

时间轴允许您查看选定项目的各种事件，例如资产的活动工作流、注释/注释、活动日志和版本。

![排序资产的时间线条目](assets/sort_timeline.gif)
*图：对资产的时间线条目排序*

>[!NOTE]
>
>在[收藏集控制台](/help/assets/manage-collections.md#navigate-the-collections-console)中，**[!UICONTROL 显示全部]**&#x200B;列表提供了仅查看评论和工作流的选项。 此外，时间轴仅显示控制台中列出的顶级收藏集。 如果您在任何收藏集中导航，则不会显示此选项。

>[!NOTE]
>
>时间轴包含多个特定于内容片段[&#128279;](content-fragments/content-fragments.md)的选项。

## 为资源作批注 {#annotating}

注释是添加到图像或视频的注释或说明性注释。 注释为营销人员提供了协作和提供有关资产的反馈。

仅在HTML5兼容视频格式的浏览器上支持视频批注。 Assets支持的视频格式取决于浏览器。 但是，视频注释尚不支持MXF视频格式。

>[!NOTE]
>
>对于内容片段，在片段编辑器[&#128279;](content-fragments/content-fragments.md)中创建注释。

1. 导航到要将注释添加到的资源的位置。
1. 从以下任一选项中选择&#x200B;**[!UICONTROL 注释]**&#x200B;图标：

   * [快速操作](#quick-actions)
   * 选择资产或导航到资产页面后，从工具栏中选择

   <!--![chlimage_1-233](assets/chlimage_1-233.png)-->

1. 在时间轴底部的&#x200B;**[!UICONTROL 注释]**&#x200B;框中添加注释。或者，在图像上标出一个区域，然后在&#x200B;**[!UICONTROL 添加批注]**&#x200B;对话框中添加批注。

<!-- ![chlimage_1-234](assets/chlimage_1-234.png)-->

<!--
1. To notify a user about an annotation, specify the email address of the user and add the comment. For example, to notify Aaron MacDonald about an annotation, enter @aa. Hints for all matching users is displayed in a list. Select Aaron's email address from the list to tag her with the comment. Similarly, you can tag more users anywhere within the annotation or before or after it.
-->

>[!NOTE]
>
>对于非管理员用户，仅当该用户在CRXDE中具有`/home`的读取权限时，才会显示建议。

<!--![chlimage_1-235](assets/chlimage_1-235.png)-->

1. 添加注释后，单击&#x200B;**[!UICONTROL 添加]**&#x200B;以保存注释。 注释的通知将发送到Aaron。

   <!--![chlimage_1-236](assets/chlimage_1-236.png)-->

   >[!NOTE]
   >
   >在保存批注之前，可以添加多个批注。

1. 选择&#x200B;**[!UICONTROL 关闭]**&#x200B;以退出注释模式。
1. 要查看通知，请使用Aaron MacDonald的凭据登录到Assets，然后单击&#x200B;**[!UICONTROL 通知]**&#x200B;图标以查看通知。

   >[!NOTE]
   >
   >注释也可以添加到视频资产中。 在对视频添加注释时，播放器会暂停以允许您在帧上添加注释。 有关详细信息，请参阅[管理视频资产](manage-video-assets.md)。 但是，视频注释尚不支持MXF视频格式。

1. 要选择不同的颜色以便区分用户，请选择“配置文件”图标并选择&#x200B;**[!UICONTROL 我的首选项]**。

   <!--![chlimage_1-237](assets/chlimage_1-237.png)-->

   在&#x200B;**[!UICONTROL 批注颜色]**&#x200B;框中指定所需颜色，然后选择&#x200B;**[!UICONTROL 接受]**。

<!-- ![chlimage_1-238](assets/chlimage_1-238.png)-->

>[!NOTE]
>
>您还可以向收藏集添加注释。 但是，如果收藏集包含子收藏集，则只能将批注/注释添加到父收藏集。 “注释”选项不适用于子收藏集。

### 查看保存的注释 {#viewing-saved-annotations}

一次只能查看一个注释。

>[!NOTE]
>
>如果选择多个注释，则用户界面上将显示最新注释。
>
>仅支持将带注释的资源打印为PDF时使用多选。

1. 要查看资产的已保存批注，请导航到资产的位置，然后打开资产的资产页面。

1. 选择GlobalNav图标，然后从列表中选择&#x200B;**[!UICONTROL 时间线]**。

   <!--![chlimage_1-239](assets/chlimage_1-239.png)-->

1. 从时间线的&#x200B;**[!UICONTROL 显示全部]**&#x200B;列表中，选择&#x200B;**[!UICONTROL 注释]**&#x200B;以根据注释过滤结果。

   <!--![chlimage_1-240](assets/chlimage_1-240.png)-->

   在&#x200B;**[!UICONTROL 时间轴]**&#x200B;面板中选择评论以查看图像上的相应批注。

   <!--![chlimage_1-241](assets/chlimage_1-241.png)-->

   选择&#x200B;**[!UICONTROL 删除]**&#x200B;以删除特定评论。

### 打印批注 {#printing-annotations}

如果资产具有注释或遵循审阅工作流，您可以打印资产以及注释和审阅状态，并将其作为PDF文件进行离线审阅。

您还可以选择仅打印注释或审阅状态。

>[!NOTE]
>
>将带注释的资源打印为PDF时，您可以选择多个注释。

要打印注释和审阅状态，请选择&#x200B;**[!UICONTROL 打印]**&#x200B;图标，然后按照向导中的说明操作。 仅当资产至少分配了一个注释或审阅状态时，**[!UICONTROL 打印]**&#x200B;图标才会显示在工具栏中。

1. 从Assets UI中，打开资源的预览页面。
1. 执行下列操作之一：

   * 要打印所有注释和审阅状态，请跳过步骤3并直接转到步骤4。
   * 要打印特定注释和审阅状态，请打开[时间线](/help/assets/manage-digital-assets.md#timeline)，然后转到步骤3。

1. 要打印特定注释，请从时间轴中选择注释。

   <!--![chlimage_1-242](assets/chlimage_1-242.png)-->

   要仅打印审阅状态，请从时间线中选择它。

   <!--![chlimage_1-243](assets/chlimage_1-243.png)-->

1. 从工具栏中选择&#x200B;**[!UICONTROL 打印]**&#x200B;图标。

   <!--![chlimage_1-244](assets/chlimage_1-244.png)-->

1. 从“打印”对话框中，选择您希望批注/审阅状态显示在PDF上的位置。 例如，如果希望批注/状态在包含已打印图像的页面的右上角打印，则使用&#x200B;**左上**&#x200B;设置。 默认情况下，该复选框处于选中状态。

   <!--![chlimage_1-245](assets/chlimage_1-245.png)-->

   您可以根据希望在打印的 PDF 中显示批注/状态的位置选择其他设置。如果希望批注/状态显示在与打印资产不同的页面中，请选择&#x200B;**[!UICONTROL 下一页]**。

1. 单击&#x200B;**[!UICONTROL 打印]**。 根据您在步骤 2 中选择的选项，生成的 PDF 会在指定位置显示批注/状态。例如，如果您选择使用&#x200B;**左上角**&#x200B;设置打印批注和审阅状态，则生成的输出将类似于此处描述的 PDF 文件。

   <!--![chlimage_1-246](assets/chlimage_1-246.png)-->

1. 使用右上方的选项下载或打印PDF。

   <!--![chlimage_1-247](assets/chlimage_1-247.png)-->

   要修改渲染的PDF文件的外观，例如注释和状态的字体颜色、大小和样式、背景颜色，请从配置管理器中打开&#x200B;**[!UICONTROL 注释PDF配置]**，并修改所需的选项。 例如，要更改已批准状态的显示颜色，请修改相应字段中的颜色代码。 有关更改注释字体颜色的信息，请参阅[注释](/help/assets/manage-digital-assets.md#annotating)。

   返回到渲染的PDF文件并刷新它。 刷新的PDF反映了您所做的更改。

## 资源版本控制 {#asset-versioning}

版本控制可在特定的时间点创建数字资源的快照。 版本控制有助于以后将资源恢复到以前的状态。 例如，如果要撤消对资源所做的更改，请恢复该资源的未编辑版本。

以下是创建版本的情况：

* 您可以修改其他应用程序中的图像，然后将其上传到Assets。 将创建图像的版本，这样就不会覆盖原始图像。
* 您可以编辑资源的元数据。
* 您使用[!DNL Experience Manager]桌面应用程序签出现有资源并保存更改。 每次保存资产时都会创建一个新版本。

您还可以通过工作流启用自动版本控制。 在为资源创建版本时，元数据和演绎版与版本一起保存。 呈现版本是相同图像的替代版本，例如，上传的JPEG文件的PNG呈现版本。

版本控制功能允许您执行以下操作：

* 创建资源的版本。
* 查看资源的当前修订版本。
* 将资源还原到以前的版本。

1. 导航到要为其创建版本的资产的位置，然后选择该资产以打开其资产页面。

1. 选择GlobalNav图标，然后从菜单中选择&#x200B;**[!UICONTROL 时间轴]**。

   ![时间线](assets/timeline.png)

1. 选择底部的&#x200B;**[!UICONTROL 操作]** （箭头）图标以查看您可以对资源执行的可用操作。

   <!--![chlimage_1-249](assets/chlimage_1-249.png)-->

1. 选择&#x200B;**[!UICONTROL 另存为版本]**&#x200B;以创建该资产的版本。

<!--![chlimage_1-250](assets/chlimage_1-250.png)-->

1. 添加标签和注释，然后单击&#x200B;**[!UICONTROL 创建]**&#x200B;以创建版本。 或者，选择&#x200B;**取消**&#x200B;以退出操作。

   <!--![chlimage_1-251](assets/chlimage_1-251.png)-->

1. 要查看新版本，请从资产详细信 **[!UICONTROL 息页面或资产UI中打开时间轴中的显示全部]** ，然后选择版 **[!UICONTROL 本]**。 为资产创建的所有版本都列在时间轴选项卡下。 您可以通过单击下拉箭头并从列表中选择版本，来过滤列 **[!UICONTROL 表以显示]** “版本”。

   ![versions_option](assets/versions_option.png)

1. 选择资源的特定版本以预览资源或使其显示在Assets UI中。

   ![select_version](assets/select_version.png)

1. 为版本添加标签和注释以还原到Assets UI中的特定版本。

   ![save_version](assets/save_version.png)

1. 要生成该版本的预览，请选择&#x200B;**[!UICONTROL 预览版本]**。
1. 要在Assets UI中显示此版本，请选择&#x200B;**[!UICONTROL 还原到此版本]**。
1. 要比较两个版本，请转到资源的资源页面，然后选择要与当前版本进行比较的版本。

   ![select_version_tocompare](assets/select_version_tocompare.png)

1. 从时间轴中，选择要比较的版本，并将滑块拖动到左侧以将此版本叠加到当前版本上并进行比较。

   ![compare_versions](assets/compare_versions.png)

### 在资产上启动工作流 {#starting-a-workflow-on-an-asset}

1. 导航到要启动工作流的资产位置，然后选择资产以打开资产页面。
1. 选择GlobalNav图标，然后从菜单中选择&#x200B;**[!UICONTROL 时间轴]**&#x200B;以显示时间轴。

   ![时间线–1](assets/timeline-1.png)

1. 选择底部的&#x200B;**[!UICONTROL 操作]** （箭头）图标以打开可用于该资源的操作列表。

   <!--![chlimage_1-252](assets/chlimage_1-252.png)-->

1. 从列表中选择&#x200B;**[!UICONTROL 启动工作流]**。

   <!--![chlimage_1-253](assets/chlimage_1-253.png)-->

1. 在&#x200B;**[!UICONTROL 启动工作流]**&#x200B;对话框中，从列表中选择工作流模型。

   <!--![chlimage_1-254](assets/chlimage_1-254.png)-->

1. （可选）指定工作流的标题，该标题可用于引用工作流实例。

   <!--![chlimage_1-255](assets/chlimage_1-255.png)-->

1. 选择&#x200B;**[!UICONTROL 开始]**，然后在对话框中选择&#x200B;**[!UICONTROL 继续]**&#x200B;以进行确认。 工作流的每个步骤都会作为事件显示在时间轴中。

   <!--![chlimage_1-256](assets/chlimage_1-256.png)-->

## 收藏集 {#collections}

收藏集是一组经过排序的资源。 使用收藏集可在用户之间共享资源。

* 收藏集可以包含来自不同位置的资源，因为它们仅包含对这些资源的引用。 每个收藏集均保持资源的引用完整性。
* 您可以与具有不同权限级别（包括编辑、查看等）的多个用户共享收藏集。

要了解集合管理的详细信息，请参阅[管理集合](/help/assets/manage-collections.md)。

## 在桌面应用程序或Adobe Asset Link中查看资源时隐藏过期的资源 {#hide-expired-assets-via-acp-api}

[!DNL Experience Manager]桌面应用允许从Windows或Mac桌面访问DAM存储库。 Adobe Asset Link允许从支持的[!DNL Creative Cloud]桌面应用程序中访问资源。

从[!DNL Experience Manager]用户界面中浏览资源时，不显示过期的资源。 要在从桌面应用程序和Asset Link浏览资产时，阻止查看、搜索和获取过期的资产，管理员可以执行以下配置。 该配置适用于所有用户，而不管管理员权限如何。

执行以下CURL命令。 确保访问资产的用户的读取权限为`/conf/global/settings/dam/acpapi/`。 属于`dam-user`组的用户默认拥有权限。

```curl
curl -v -u admin:admin --location --request POST 'http://localhost:4502/conf/global/settings/dam/acpapi/configuration/_jcr_content' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'jcr:title=acpapiconfig' \
--data-urlencode 'hideExpiredAssets=true' \
--data-urlencode 'hideExpiredAssets@TypeHint=Boolean' \
--data-urlencode 'jcr:primaryType=nt:unstructured' \
--data-urlencode '../../jcr:primaryType=sling:Folder'
```

要了解更多信息，请参阅如何[使用桌面应用程序浏览DAM资源](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=zh-Hans#browse-search-preview-assets)和[如何使用Adobe Asset Link](https://helpx.adobe.com/cn/enterprise/admin-guide.html/enterprise/using/manage-assets-using-adobe-asset-link.ug.html)。

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
* [发布资源到 AEM 和 Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)
