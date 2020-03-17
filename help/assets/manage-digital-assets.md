---
title: 在Experience Manager中管理您的数字资产
description: 了解各种资产管理和编辑方法。
contentOwner: AG
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 913339d0892b37814df1bd04bc352cfadf32b3e6

---


# Manage assets {#manage-assets}

本文介绍如何在Adobe Experience Manager(AEM)资产中管理和编辑资产。 要管理内容片段，请参阅 [内容片段](content-fragments/content-fragments.md) 。

## 创建文件夹 {#creating-folders}

在组织资产集合（例如，所有图像）时，您 `Nature` 可以创建文件夹以将它们放在一起。 您可以使用文件夹对资产进行分类和组织。 AEM资产不要求您组织文件夹中的资产以更好地工作。

>[!NOTE]
>
>* 共享到Marketing Cloud时，不 `sling:OrderedFolder`支持共享类型的“资产”文件夹。 如果要共享文件夹，请勿在创建文件夹 [!UICONTROL 时选择] “已排序”。
>* Experience Manager不允许将单 `subassets` 词用作文件夹的名称。 它是为包含复合资产子资产的节点保留的关键字


1. 导航到数字资产文件夹中要创建新文件夹的位置。 在菜单中，单击“创 **[!UICONTROL 建”]**。 选择“ **[!UICONTROL 新建文件夹]**”。
1. 在“标 **[!UICONTROL 题]** ”字段中，提供文件夹名称。 默认情况下，DAM使用您提供的标题作为文件夹名称。 创建文件夹后，您可以覆盖默认文件夹并指定其他文件夹名称。
1. 单击&#x200B;**[!UICONTROL 创建]**。您的文件夹会显示在数字资产文件夹中。

不支持以下（以空格分隔的）字符列表：

* 资产文件名中不能包含以下任意字符： `* / : [ \\ ] | # % { } ? &`
* 资产文件夹名称不能包含以下任意字符： `* / : [ \\ ] | # % { } ? \" . ^ ; + & \t`

## Upload assets {#uploading-assets}

有关详 [细信息，请参阅将数字资产添加到Experience Manager](add-assets.md)。

## 预览资产 {#previewing-assets}

要预览资产，请按照以下步骤操作。

1. 在资产用户界面中，导航到要预览的资产所在的位置。
1. 点按所需的资产以将其打开。

1. 在预览模式中，缩放选项可用于支持的图 [像类型](/help/assets/file-format-support.md) （通过交互式编辑）。

   要放大资产，请点按／单 `+` 击（或点按／单击资产上的放大镜）。 要缩小，请点按／单击 `-`。 放大时，可以通过平移来仔细查看图像上的任意区域。重置缩放箭头可返回原始视图。

   Tap **[!UICONTROL Reset]** to reset the view to the original size.

## 编辑属性 {#editing-properties}

1. 导航到要编辑元数据的资产所在的位置。

1. 选择资产，然后点按／单击工 **[!UICONTROL 具栏中]** 的属性以查看资产属性。 或者，选择资产 **[!UICONTROL 卡上的]** “属性”快速操作。

   ![properties_quickaction](assets/properties_quickaction.png)

1. 在“属 [!UICONTROL 性] ”页中，编辑各个选项卡下的元数据属性。 例如，在“基 **[!UICONTROL 本]** ”选项卡下，编辑标题、说明等。

   >[!NOTE]
   >
   >“属性”页面的布 [!UICONTROL 局] ，以及可用的元数据属性取决于基础元数据架构。 要了解如何修改“属性”页的布 [!UICONTROL 局] ，请参阅元 [数据架构](/help/assets/metadata-schemas.md)。

1. 要计划资产激活的特定日期/时间，请使用&#x200B;**[!UICONTROL 开始时间]**&#x200B;字段旁边的日期选取器。

   ![chlimage_1-217](assets/chlimage_1-217.png)

1. 要在特定持续时间后取消激活资产，请从“结束时间”字段旁边的日期选取器中选择取消激 **[!UICONTROL 活日期]** /时间。 取消激活日期应晚于资产的激活日期。 结束 [!UICONTROL 时间后]，资产及其演绎版不能通过资产Web界面或通过HTTP API使用。

   ![chlimage_1-218](assets/chlimage_1-218.png)

1. 在“标 **[!UICONTROL 记]** ”字段中，选择一个或多个标记。 要添加自定义标记，请在框中键入标记的名称，然后按Enter键。 新标记将保存在AEM中。

   YouTube需要“标记”才能发布，并且有一个指向YouTube的链接（如果可以找到合适的链接）。

   >[!NOTE]
   >
   >要创建标记，您必须在CRX存储库的路 `/content/cq:tags/default` 径上具有写入权限。

1. 要查看资产的使用情况统计信息，请单击／点按 **[!UICONTROL 分析]** 选项卡。

   使用情况统计信息包括：

   * 查看或下载资产的次数
   * 使用资产的渠道／设备
   * 最近使用该资产的创意解决方案
   有关详细信息，请参阅 [资产分析](assets-insights.md)。

1. 点按／单击保 **[!UICONTROL 存并关闭]**。

1. 导航到资产用户界面。 编辑的元数据属性（包括标题、说明和标记）显示在“卡片”视图的资产卡片上以及“列表”视图的相关列下。

## 复制资产 {#copying-assets}

复制资产或文件夹时，会复制整个资产或文件夹及其内容结构。 复制的资产或文件夹会复制到目标位置。 源位置的资产不会更改。

资产特定副本的一些属性不会结转。 例如：

* 资产ID、创建日期和时间以及版本和版本历史记录。 其中一些属性由属性、 `jcr:uuid`和 `jcr:created`表示 `cq:name`。

* 每个资产及其每个演绎版的创建时间和引用路径都是唯一的。

其他属性和元数据信息将被保留。 复制资产时不会创建部分副本。

1. 从资产UI中，选择一个或多个资产，然后点按／单击工具栏中 **[!UICONTROL 的复制]** 图标。 或者，从资 **[!UICONTROL 产卡]**![中选择Copy](assets/copy_icon.png) _copy_icon快速操作。

   >[!NOTE]
   >
   >如果您使用复 [!UICONTROL 制快速操作] ，则一次只能复制一个资产。

1. 导航到要将资产复制到的位置。

   >[!NOTE]
   >
   >如果您在同一位置复制资产，AEM会自动生成该名称的变体。 For example, if you copy an asset titled `Square`, AEM automatically generates the title for its copy as `Square1`.

1. Click the **[!UICONTROL Paste]** asset icon from the toolbar. 资产会复制到此位置。

   ![chlimage_1-219](assets/chlimage_1-219.png)

   >[!NOTE]
   >
   >The **[!UICONTROL Paste]** icon is available in the toolbar until the paste operation is completed.

### 移动或重命名资产 {#moving-or-renaming-assets}

1. 导航到要移动的资产所在的位置。

1. 选择资产，然后点按／单击工 **[!UICONTROL 具栏中]**![的移动图标move_icon](assets/move_icon.png) 。

1. 在“移动资产”向导中，执行下列操作之一：

   * 指定资产在移动后的名称。 然后点按／单击 **[!UICONTROL 下一步]** ，以继续。

   * 点按／单 **[!UICONTROL 击取消]** ，以停止该过程。
   >[!NOTE]
   >
   >* 您可以为资产指定相同的名称，前提是新位置中没有使用该名称的资产。但是，如果您将资产移动到存在同名资产的位置，则应使用其他名称。 如果使用相同的名称，系统会自动生成该名称的变体。 例如，如果您的资产的名称为“Square”，则系统会为其副本生成名称“Square1”。
   >* 重命名时，文件名中不允许有空格。


1. On the **[!UICONTROL Select Destination]** dialog, do one of the following:

   * Navigate to the new location for the assets, and then tap/click **[!UICONTROL Next]** to proceed.

   * Tap/click **[!UICONTROL Back]** to return to the **[!UICONTROL Rename]** screen.

1. 如果被移动的资产具有任何引用页面、资产或集合，则“选择目标”选 **[!UICONTROL 项卡旁边将显示]** “调整引 **[!UICONTROL 用”选项卡]** 。

   在“调整引用”屏幕中，执行 **[!UICONTROL 下列操作之一]** :

   * Specify the references to be adjusted based on the new details, and then tap/click **[!UICONTROL Move]** to proceed.

   * From the **[!UICONTROL Adjust]** column, select/unselect references to the assets.
   * Tap/click **[!UICONTROL Back]** to return to the **[!UICONTROL Select Destination]** screen.

   * 点按／单击 **[!UICONTROL 取消]** ，以停止移动操作。
   如果您不更新引用，则它们会继续指向资产的上一个路径。 如果您调整引用，这些引用将更新为新的资产路径。

### 管理再现 {#managing-renditions}

1. 您可以为资产添加或删除演绎版，但原始形式除外。导航到您要为其添加或删除演绎版的资产所在的位置。

1. 点按／单击资产以打开其资产页面。

   ![chlimage_1-220](assets/chlimage_1-220.png)

1. 点按／单击GlobalNav图标，然后从列 **[!UICONTROL 表中选择]** “演绎版”。

   ![renditions_menu](assets/renditions_menu.png)

1. 在&#x200B;**[!UICONTROL 演绎版]**&#x200B;面板中，查看为资产生成的演绎版列表。

   ![renditions_panel](assets/renditions_panel.png)

   >[!NOTE]
   >
   >默认情况下，AEM资产不会在预览模式下显示资产的原始演绎版。 如果您是管理员，则可以使用叠加将AEM资产配置为在预览模式下显示原始演绎版。

1. 选择一个演绎版以进行查看或删除。

   **删除再现**

   Select a rendition from the **[!UICONTROL Renditions]** panel, and then tap/click the **[!UICONTROL Delete Rendition]** icon from the toolbar.

   ![delete_rendition图标](assets/delete_renditionicon.png)

   **上传新再现**

   导航到资产的资产详细信息页面，然后点按／单击工具栏中的 **[!UICONTROL 添加演绎版]** ，以上传资产的新演绎版。

   ![chlimage_1-221](assets/chlimage_1-221.png)

   >[!NOTE]
   >
   >如果您从演绎版面板中选 **[!UICONTROL 择了演绎版]** ，工具栏会更改上下文并仅显示与演绎版相关的那些操作。 不显示“上传演绎版”图标等选项。 要在工具栏中查看这些选项，请导航到资产的详细信息页面。

   您可以配置要在图像或视频资产的详细信息页面中显示的再现的尺寸。 根据您指定的维，AEM资产会显示具有精确或最接近的维度的再现。

   要在资产详细信息级别配置图像的演绎版尺寸，请叠 `renditionpicker` 加节点(`libs/dam/gui/content/assets/assetpage/jcr:content/body/content/content/items/assetdetail/items/col1/items/assetview/renditionpicker`)并配置width属性的值。 配置属性大 **[!UICONTROL 小（长）(以KB]** )代替宽度，以根据图像大小在资产详细信息页面上自定义再现。 对于基于大小的自定义，如果匹 `preferOriginal` 配的再现的大小大于原始再现，则属性会为原始再现分配首选项。

   同样，您也可以通过覆盖来自定义“注释”页面图像 `libs/dam/gui/content/assets/annotate/jcr:content/body/content/content/items/content/renditionpicker`。

   ![chlimage_1-222](assets/chlimage_1-222.png)

   要为视频资产配置再现维度，请导航到CRX存储库中位于 `videopicker` 该位置的节点，覆盖该节点 `/libs/dam/gui/content/assets/assetpage/jcr:content/body/content/content/items/assetdetail/items/col1/items/assetview/videopicker`，然后编辑相应的属性。

   >[!NOTE]
   >
   >视频注释功能仅在提供 HTML5 兼容视频格式的浏览器上受支持。此外，该功能支持不同的视频格式，具体视浏览器而定。

## Delete assets {#delete-assets}

要从其他页面解析或删除传入的引用，请在删除资产之前更新相关引用。

此外，使用叠加禁用强制删除按钮，以禁止用户删除引用的资产和离开断开的链接。

1. 导航至要删除的资产所在的位置。

1. 选择资产，然后点按／单击工 **[!UICONTROL 具栏中]** 的删除图标。

   ![delete_icon](assets/delete_icon.png)

1. 在确认对话框中，单击：

   * **[!UICONTROL 取消]** ，停止操作
   * **[!UICONTROL 删除]**，以确认操作：

      * 如果资产没有引用，则资产会被删除。
      * 如果资产具有引用，则会出现一条错误消息，通知您&#x200B;**一个或多个资产被引用**。您可以选择&#x200B;**[!UICONTROL 强制删除]**&#x200B;或&#x200B;**[!UICONTROL 取消]**。
   >[!NOTE]
   >
   >您需要对dam/asset具有删除权限才能删除资产。 如果您只具有修改权限，则只能编辑资产元数据并向资产添加注释。 但是，您无法删除资产或其元数据。

   >[!NOTE]
   >
   >要从其他页面解析或删除传入的引用，请在删除资产之前更新相关引用。
   >
   >
   >此外，使用叠加禁用强制删除按钮，以禁止用户删除引用的资产和离开断开的链接。

## 下载资产 {#download-assets}

See [Download assets from AEM](/help/assets/download-assets-from-aem.md).

## Publish assets {#publish-assets}

<!--
>[!NOTE]
>
>For more information specific to Dynamic Media, see [Publishing Dynamic Media Assets.](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)
-->

1. 导航到要发布的资产／文件夹所在的位置。

1. 从资产卡中选择&#x200B;**[!UICONTROL 发布]**&#x200B;以进行快速操作，或选择资产，然后点按/单击工具栏中的&#x200B;**[!UICONTROL 快速发布]**&#x200B;图标。
1. 如果资产引用了其他资产，向导中便会列出这些引用。只显示自上次发布／取消发布以来未发布或已修改的引用。 选择要发布的引用。

   ![chlimage_1-225](assets/chlimage_1-225.png)

   >[!NOTE]
   >
   >如果要发布的文件夹包含空文件夹，则不会发布空文件夹。

1. Tap/click **[!UICONTROL Publish]** to confirm the activation for the assets.

>[!CAUTION]
>
>如果您发布的资产正在被处理，则仅会发布原始内容。 缺少再现。 等待处理完成，然后在处理完成后发布或重新发布资产。

## 取消发布资产 {#unpublishing-assets}

1. 导航到要从发布环境中删除的资产／资产文件夹的位置（取消发布）。

1. 选择要取消发布的资产／文件夹，然后点按／单击工 **[!UICONTROL 具栏中的管理发布]** 图标。

   ![manage_publication](assets/manage_publication.png)

1. 从列表 **[!UICONTROL 中选择]** “取消发布”操作。

   ![unpublish_action](assets/unpublish_action.png)

1. To unpublish the asset later, select **[!UICONTROL Unpublish Later]**, and then select a date for unpublishing the asset.
1. 计划一个资产在发布环境中不再可用的日期。
1. 如果资产引用了其他资产，请选择要取消发布的引用。 点按／单击取 **[!UICONTROL 消发布]**。
1. 在确认对话框中，点按／单击：

   * **[!UICONTROL 取消]** ，停止操作
   * **[!UICONTROL 取消发布]** ，以确认在指定日期已取消发布资产（在发布环境中不再可用）。
   >[!NOTE]
   >
   >取消发布复杂资产时，仅取消发布资产。 请避免取消发布引用，因为其他已发布的资产可能会引用这些引用。

## Closed user group {#closed-user-group}

已关闭的用户组(CUG)用于限制对从AEM发布的特定资产文件夹的访问。 如果为文件夹创建了CUG，则仅对分配的成员或用户组具有对文件夹（包括文件夹资源和子文件夹）的访问权限。 要访问文件夹，他们必须使用其安全凭据登录。

CUG是限制对资产访问的额外方式。 您还可以为文件夹配置登录页面。

1. 从资产UI中选择一个文件夹，然后点按／单击工具栏中的属性图标以显示属性页面。
1. 从“权 **[!UICONTROL 限]** ”选项卡，在“已关闭的用户组”下添加 **[!UICONTROL 成员或组]**。

   ![add_user](assets/add_user.png)

1. 要在用户访问文件夹时显示登录屏幕，请选择“启 **[!UICONTROL 用]** ”选项。 然后，在AEM中选择登录页面的路径，并保存更改。

   ![login_page](assets/login_page.png)

   >[!NOTE]
   >
   >如果未指定登录页面的路径，AEM将在发布实例中显示默认登录页面。

1. 发布文件夹，然后尝试从发布实例访问它。 将显示登录屏幕。
1. 如果您是CUG成员，请输入您的安全凭据。 AEM对您进行身份验证后，将显示该文件夹。

## 搜索资产 {#search-assets}

搜索资产是数字资产管理系统使用的核心——无论是供创意人员进一步使用、供商业用户和营销人员对资产进行可靠管理还是供DAM管理员管理。

要进行简单、高级和自定义搜索以发现和使用最合适的资产，请参阅 [在AEM中搜索资产](/help/assets/search-assets.md)。

## 快速操作 {#quick-actions}

快速操作图标一次只能用于单个资产。根据设备的不同，执行以下操作以显示快速操作图标：

* 触控设备：触控并按住。 例如，在iPad上，您可以点按并按住资产，以便显示快速操作。
* 非触控设备：悬停指针。 例如，在桌面设备上，如果将指针悬停在资产缩略图上，则会显示快速操作栏。

## 编辑图像 {#editing-images}

AEM资产界面中的编辑工具可让您对图像资产执行小型编辑作业。 您可以对图像进行裁剪、旋转、翻转和执行其他编辑作业。 您还可以向资产添加图像映射。

>[!NOTE]
>
>对于某些组件，全屏模式还有其他可用选项。

1. 执行以下操作之一以在编辑模式下打开资产：

   * 选择资产，然后单击／点按工 **[!UICONTROL 具栏中]** 的编辑图标。
   * Tap/click the **[!UICONTROL Edit]** icon that appears on an asset in the Card view.
   * 在资产页面中，点按／单击工 **[!UICONTROL 具栏中]** 的编辑图标。
   ![edit_icon](assets/edit_icon.png)

1. To crop the image, tap/click the **Crop** icon.

   ![chlimage_1-226](assets/chlimage_1-226.png)

1. 从列表中选择所需的选项。图像上会根据您选择的选项显示裁剪区域。利用&#x200B;**手绘**&#x200B;选项，您可以不受纵横比限制裁剪图像。

   ![chlimage_1-227](assets/chlimage_1-227.png)

1. 选择要裁剪的区域，并在图像上调整其大小或位置。
1. 使用“ **完成** ”图标（右上角）裁剪图像。 Clicking the **Finish** icon also triggers the regeneration of renditions.

   ![chlimage_1-228](assets/chlimage_1-228.png)

1. 使用右 **上角的** “撤消”和 **** “重做”图标分别恢复到未裁剪的图像或保留裁剪的图像。

   ![chlimage_1-229](assets/chlimage_1-229.png)

1. 点按／单击相应的旋转图标以顺时针或逆时针旋转图像。

   ![chlimage_1-230](assets/chlimage_1-230.png)

1. 点按／单击相应的翻转图标，以水平或垂直翻转图像。

   ![chlimage_1-231](assets/chlimage_1-231.png)

1. Tap/click the **Finish** icon to save the changes.

   ![chlimage_1-232](assets/chlimage_1-232.png)

>[!NOTE]
>
>BMP、GIF、PNG和JPEG文件格式支持图像编辑。

<!-- You can also add image maps using the image editor. For details, see [Adding Image Maps](/help/assets/image-maps.md). -->

>[!NOTE]
>
>要编辑TXT文件，请从“配置 **管理器”中设置Day CQ Link Externalizer** 。

## 时间轴 {#timeline}

时间轴允许您查看选定项目的各种事件，如资产的活动工作流、注释／注释、活动日志和版本。

![对资产的时间轴条目排序](assets/sort_timeline.gif)*图：对资产的时间轴条目进行排序*

>[!NOTE]
>
>在“收藏 [集”控制台中](/help/assets/manage-collections.md#navigate-the-collections-console),“显 **[!UICONTROL 示全部]** ”列表提供了仅查看注释和工作流的选项。 此外，时间轴仅对控制台中列出的顶级集合显示。 如果您在任何集合中导航，则不会显示该集合。

>[!NOTE]
>
>时间轴包含特 [定于内容片段的多个选项](content-fragments/content-fragments.md)。

## 批注 {#annotating}

注释是指添加到图像或视频的评论或解释性说明。通过注释，营销人员可以协作并保留有关资产的反馈。

视频注释功能仅在提供 HTML5 兼容视频格式的浏览器上受支持。AEM资产支持的视频格式取决于浏览器。

>[!NOTE]
>
>对于内容片段， [将在片段编辑器中创建注释](content-fragments/content-fragments.md)。

1. 导航到要添加注释的资产所在的位置。
1. 点按／单击以 **[!UICONTROL 下任一]** :

   * [快速操作](#quick-actions)
   * 在选择资产或导航到资产页面后，从工具栏中
   ![chlimage_1-233](assets/chlimage_1-233.png)

1. 在时间轴底部的&#x200B;**[!UICONTROL 注释]**&#x200B;框中添加注释。或者，在图像上标出一个区域，然后在&#x200B;**[!UICONTROL 添加批注]**&#x200B;对话框中添加批注。

   ![chlimage_1-234](assets/chlimage_1-234.png)

<!--
1. To notify a user about an annotation, specify the email address of the user and add the comment. For example, to notify Aaron MacDonald about an annotation, enter @aa. Hints for all matching users is displayed in a list. Select Aaron's email address from the list to tag her with the comment. Similarly, you can tag more users anywhere within the annotation or before or after it.

   >[!NOTE]
   >
   >For a non-administrator user, suggestions appear only if the user has Read permissions at `/home` in CRXDE.

   ![chlimage_1-235](assets/chlimage_1-235.png)

1. After adding the annotation, click **[!UICONTROL Add]** to save it. A notification for the annotation is sent to Aaron.

   ![chlimage_1-236](assets/chlimage_1-236.png)

   >[!NOTE]
   >
   >You can add multiple annotations, before you save them.

1. Tap/click **[!UICONTROL Close]** to exit from the Annotation mode.
1. To view the notification, log in to AEM Assets with Aaron MacDonald's credentials and click the **[!UICONTROL Notifications]** icon to view the notification.

   >[!NOTE]
   >
   >Annotations can also be added to video assets. While annotating videos, the player pauses to let you annotate on a frame. For details, see [managing video assets](manage-video-assets.md).

1. To choose a different color so you can differentiate between users, click/tap the Profile icon and click/tap **[!UICONTROL My Preferences]**.

   ![chlimage_1-237](assets/chlimage_1-237.png)

   Specify the desired color in the **[!UICONTROL Annotation Color]** box and then click/tap **[!UICONTROL Accept]**.

   ![chlimage_1-238](assets/chlimage_1-238.png)

>[!NOTE]
>
>You can also add annotations to a collection. However, if a collection contains child collections, you can add annotations/comments to the parent collection only. The Annotate option is not available for child collections.

### View saved annotations {#viewing-saved-annotations}

1. To view saved annotations for an asset, navigate to the location of the asset and open the asset page for the asset.

1. Tap/click the GlobalNav icon, and choose **[!UICONTROL Timeline]** from the list.

   ![chlimage_1-239](assets/chlimage_1-239.png)

1. From the **[!UICONTROL Show All]** list in the timeline, select **[!UICONTROL Comments]** to filter the results based on annotations.

   ![chlimage_1-240](assets/chlimage_1-240.png)

   Tap/click a comment in the **[!UICONTROL Timeline]** panel to view the corresponding annotation on the image.

   ![chlimage_1-241](assets/chlimage_1-241.png)

   Tap/click **[!UICONTROL Delete]**, to delete a particular comment.

### Print annotations {#printing-annotations}

If an asset has annotations or it has been subjected to a review workflow, you can print the asset along with annotations and review status as a PDF file for offline review.

You can also choose to print only the annotations or review status.

To print the annotations and review status, tap/click the **[!UICONTROL Print]** icon and follow the instructions in the wizard. The **[!UICONTROL Print]** icon appears in the toolbar only when the asset has at least one annotation or review status assigned to it.

1. From the Assets UI, open the preview page for an asset.
1. Do one of the following:

    * To print all the annotations and the review status, skip step 3 and directly go to step 4.
    * To print specific annotations and review status, open the [timeline](/help/assets/manage-digital-assets.md#timeline) and then go to step 3.

1. To print specific annotations, select the annotations from the timeline.

   ![chlimage_1-242](assets/chlimage_1-242.png)

   To print the review status only, select it from the timeline.

   ![chlimage_1-243](assets/chlimage_1-243.png)

1. Tap/click the **[!UICONTROL Print]** icon from the toolbar.

   ![chlimage_1-244](assets/chlimage_1-244.png)

1. From the Print dialog, choose the position you want the annotations/review status to be displayed on the PDF. For example, if you want the annotations/status to be printed at the top-right of the page that contains the printed image, use the **Top-Left** setting. It is selected by default.

   ![chlimage_1-245](assets/chlimage_1-245.png)

   You can choose other settings depending on the position where you want the annotations/status to appear in the printed PDF. If you want the annotations/status to appear in a page that is separate from the printed asset, choose **[!UICONTROL Next Page]**.

   >[!NOTE]
   >
   >Lengthy annotations may not render properly in the PDF file. For optimal rendering, Adobe recommends that you limit annotations to 50 words.

1. Tap/click **[!UICONTROL Print]**. Depending upon the option you choose in step 2, the generated PDF displays the annotations/status at the specified position. For example, if you choose to print both annotations and the review status using the **Top-Left** setting, the generated output resembles the PDF file depicted here.

   ![chlimage_1-246](assets/chlimage_1-246.png)

1. Download or print the PDF using the options at the top-right.

   ![chlimage_1-247](assets/chlimage_1-247.png)

   To modify the appearance of the rendered PDF file, for example the font color, size, and style, background color of the comments and statuses, open the **[!UICONTROL Annotation PDF configuration]** from Configuration Manager, and modify the desired options. For example, to change the display color of the approved status, modify the color code in the corresponding field. For information around changing the font color of annotations, see [Annotating](/help/assets/manage-digital-assets.md#annotating).

   ![chlimage_1-248](assets/chlimage_1-248.png)

   Return to the rendered PDF file and refresh it. The refreshed PDF reflects the changes you made.

## Asset versioning {#asset-versioning}

Versioning creates a snapshot of digital assets at a specific point in time. Versioning helps restore assets to a previous state at a later time. For example, if you want to undo a change that you made to an asset, restore the unedited version of the asset.

The following are scenarios where you create versions:

* You modify an image in a different application and upload to AEM Assets. A version of the image is created so your original image is not overwritten.
* You edit the metadata of an asset.
* You use AEM desktop app to checkout an existing asset and save your changes. A new version is created everytime the asset is saved.

You can also enable automatic versioning through a workflow. When you create a version for an asset, the metadata and renditions are saved along with the version. Renditions are rendered alternatives of the same images, for example, a PNG rendition of an uploaded JPEG file.

The versioning functionality lets you do the following:

* Create a version of an asset.
* View the current revision for an asset.
* Restore the asset to a previous version.

1. Navigate to the location of the asset for which you want to create a version, and tap/click it to open its asset page.

1. Tap/click the GlobalNav icon, and the choose **[!UICONTROL Timeline]** from the menu.

   ![timeline](assets/timeline.png)

1. Tap/click the **[!UICONTROL Actions]** (arrow) icon at the bottom to view the available actions you can perform on the asset.

   ![chlimage_1-249](assets/chlimage_1-249.png)

1. Tap/click **[!UICONTROL Save as Version]** to create a version for the asset.

   ![chlimage_1-250](assets/chlimage_1-250.png)

1. Add a label and comment, and then click **[!UICONTROL Create]** to create a version. Alternatively, tap/click **Cancel** to exit the operation.

   ![chlimage_1-251](assets/chlimage_1-251.png)

1. To view the new version, open the **[!UICONTROL Show All]** list in the timeline from the asset details page or the Assets UI, and choose **[!UICONTROL Versions]**. All versions created for an asset are listed under the timeline tab. You can filter the list to show Versions, by clicking the drop arrow and selecting **[!UICONTROL Versions]** from the list.

   ![versions_option](assets/versions_option.png)

1. Select a specific version for the asset to preview it or enable it to appear in the Assets UI.

   ![select_version](assets/select_version.png)

1. Add a label and comment for the version to revert to the particular version in the Assets UI.

   ![save_version](assets/save_version.png)

1. To generate a preview for the version, tap/click **[!UICONTROL Preview Version]**.
1. To display this version in the Assets UI, select **[!UICONTROL Revert to this Version]**.
1. To compare between two versions, go to asset page of the asset and tap/click the version to be compared with the current version.

   ![select_version_tocompare](assets/select_version_tocompare.png)

1. From the timeline, select the version you want to compare and drag the slider to the left to superimpose this version over the current version and compare.

   ![compare_versions](assets/compare_versions.png)

### Starte a workflow on an asset {#starting-a-workflow-on-an-asset}

1. Navigate to the location of the asset for which you want to start a workflow, and tap/click the asset to open the asset page.
1. Tap/click the GlobalNav icon, and the choose **[!UICONTROL Timeline]** from the menu to display the timeline.

   ![timeline-1](assets/timeline-1.png)

1. Tap/click the **[!UICONTROL Actions]** (arrow) icon at the bottom to open the list of actions available for the asset.

   ![chlimage_1-252](assets/chlimage_1-252.png)

1. Tap/click **[!UICONTROL Start Workflow]** from the list.

   ![chlimage_1-253](assets/chlimage_1-253.png)

1. In the **[!UICONTROL Start Workflow]** dialog, select a workflow model from the list.

   ![chlimage_1-254](assets/chlimage_1-254.png)

1. (Optional) Specify a title for the workflow, which can be used to reference the workflow instance.

   ![chlimage_1-255](assets/chlimage_1-255.png)

1. Tap/click **[!UICONTROL Start]** and then tap/click **[!UICONTROL Proceed]** in the dialog to confirm. Each step of workflow is displayed in the timeline as an event.

   ![chlimage_1-256](assets/chlimage_1-256.png)

## Collections {#collections}

A collection is an ordered set of assets. Use collections to share assets between users.

* A collection can include assets from different locations because they only contain references to these assets. Each collection maintains the referential integrity of assets.
* You can share collections with multiple users with different privilege levels, including editing, viewing, and so on.

See [Managing Collections](/help/assets/manage-collections.md) for details on collection management.
