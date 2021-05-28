---
title: 编辑页面属性
description: 为页面定义所需的属性
exl-id: 27521a6d-c6e9-4f43-9ddf-9165b0316084
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '1907'
ht-degree: 58%

---

# 编辑页面属性 {#editing-page-properties}

您可以为页面定义所需的属性。这些属性会因页面性质而异。例如，某些页面可能会连接到 Live Copy，而其他页面则可能不会，Live Copy 信息将在适当情况下才可用。

## 页面属性 {#page-properties}

属性分布于多个选项卡中。

### 基本 {#basic}

* **标题和标记**

   * **标题**  — 页面的标题会显示在不同的位置。例如，网站 **** 标签列表和站点标 **** 签/列表视图。
      * 这是必填字段。
   * **标记**  — 在此，您可以通过更新选择框中的列表在页面中添加或删除标记。
      * 选择标记后，它会列在选择框下。您可以使用“x”从此列表中删除标记。
      * 可通过在空白选择框中键入名称输入全新标记。
         * 按 Enter 将创建新标记。
         * 随后将会显示新标记，其右侧带有一个小星星，表示该标记为新标记。
      * 使用下拉列表功能，可从现有标记中进行选择。
      * 当您将鼠标悬停在选择框中的标记条目上时，会显示 x，用于为此页面删除该标记。
      * 有关标记的更多信息，请访问[使用标记](/help/sites-cloud/authoring/features/tags.md)。
   * **隐藏导航**  — 指示在生成的网站的页面导航中是否显示或隐藏页面。

* **品牌化**

   通过在每个页面标题后附加一个品牌辅助信息，在页面中应用一致的品牌标识。 此功能需要使用[核心组件2.14.0版或更高版本中的页面组件。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hans)

   * **覆盖**  — 选中以定义此页面上的品牌概要信息。
      * 任何子页面都将继承该值，除非它们还设置了其&#x200B;**Override**&#x200B;值。
   * **覆盖值**  — 要附加到页面标题的品牌辅助信息的文本。
      * 该值会在管道字符（如“循环托斯卡纳”）后附加到页面标题中 |始终为WKND做好准备”

* **HTML ID**

   * **ID**  — 应用于组件的HTML ID。

* **更多标题和说明**

   * **页面标题**  — 要在页面上使用的标题。通常由标题组件使用。如果留空，则将使用&#x200B;**标题**。
   * **导航标题**  — 您可以指定单独的标题以在导航中使用（例如，如果您希望某些内容能更加简洁）。 如果为空，则 **** 使用标题。
   * **子标题**  — 要在页面上使用的子标题。
   * **描述**  — 页面的描述、用途或要添加的任何其他详细信息。

* **开启/结束时间**

   * **On Time**  — 发布环境中显示（渲染）已发布页面的日期和时间。必须手动或通过预配置的自动复制来发布页面。

      >[!NOTE]
      >
      > 有关如何配置相关自动复制的详细信息，请参阅[开启和关闭时间 — 触发器配置](/help/operations/replication.md#on-and-off-times-trigger-configuration)。

      * 如果[已发布（手动）](/help/sites-cloud/authoring/fundamentals/publishing-pages.md)，则在指定时间渲染之前，此页面将保持休眠（隐藏）。
      * 如果未发布并配置了自动复制功能，则页面将在指定的时间自动发布并渲染。
      * 如果未发布，并且未配置为自动复制，则页面将不会自动发布，因此当尝试访问该页面时，将会看到404。
   * **关闭时间**  — 与“开启时间” **类似，它通常与“开启时间”**&#x200B;一起使用，它定义发布页面在发布环境中隐藏的时间。

   * 对于要立即发布的页面，请将这些字段（**开始时间**&#x200B;和&#x200B;**结束时间**）留空，并在发布环境中可用，直到停用它们（正常情况）。


* **虚 URL**

   * 允许您输入此页面的虚 URL，以便使用更短并且/或者含意更清楚的 URL。
   * 例如，如果将网站 `http://example.com` 的虚 URL 设置为由路径 `/v1.0/startpage` 标识的 `welcome` 页面，则 `http://example.com/welcome` 将成为 `http://example.com/content/v1.0/startpage` 的虚 URL

   >[!CAUTION]
   >
   >虚 URL：
   >
   >* 必须是唯一的，因此您应该确保该值没有被其他页面使用。
   >* 不支持正则表达式模式。
   >* 不应设置为现有页面。


   * **添加**  — 点按或单击以显示字段，以为页面定义虚URL。
      * 再次点按或单击可添加多个。
      * 点按或单击&#x200B;**删除**&#x200B;图标以删除虚URL。
   * **重定向虚URL**  — 指示您是否希望页面使用虚URL。




### 高级 {#advanced}

* **设置**

   * **语言**  — 页面语言
   * **语言根**  — 如果页面是语言副本的根，则必须选中
   * **重定向**  — 指示此页面应自动重定向到的页面
   * **设计**  — 指示在生成的网站的页面导航中是否显示或隐藏页面
   * **别名**  — 指定要与此页一起使用的别名

   >[!NOTE]
   >
   >别名会设置 `sling:alias` 属性以定义资源的别名（这仅会影响资源，不会影响路径）。
   >
   >例如：如果您为节点 `/content/we-retail/spanish` 定义别名 `latin-lang`，则可以通过 `/content/we-retail/latin-language` 访问此页面。
   >
   >有关详细信息，请参阅“SEO 和 URL 管理最佳实践”下的“本地化的页面名称”。

   <!--
  >For further details see [Localized page names under SEO and URL Management Best Practices](/help/managing/seo-and-url-management.md#localized-page-names).
  -->

* **配置**

   * **云配置**  — 配置的路径

* **模板设置**

   * **允许的模板**  -  [定义将在此子](/help/sites-cloud/authoring/features/templates.md#enabling-and-allowing-a-template-template-author) 分支中可用的模板列表

* **身份验证要求**

   * **启用**  — 启用身份验证以访问页面

      >[!NOTE]
      >
      >已关闭的用户组在&#x200B;**[权限](#permissions)**&#x200B;选项卡上定义。

   * **登录页面**  — 用于登录的页面

* **导出**

   * **导出配置**  — 指定导出配置

### 缩略图 {#thumbnail}

配置页面缩略图

* **生成预览**  — 生成要用作缩略图的页面预览
* **上传图像**  — 上传要用作缩略图的图像
* **选择图像**  — 选择一个现有资产作为缩略图
* **还原**  — 在对缩略图进行更改后，此选项将变为可用。如果不想保留您的更改，可以在保存前还原更改。

### 社交媒体 {#social-media}

* **社交媒体共享**

   定义页面上可用的共享选项。显示可用于[共享核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/sharing.html)的选项。

   * **为 Facebook 启用用户共享**
   * **为 Pinterest 启用用户共享**
   * **首选体验片段变量**
      * 定义用于为页面生成元数据的体验片段变量

### 云服务 {#cloud-services}

* **云服务配置**  — 为云服务定义属性

   <!--Define properties for [cloud services](/help/sites-developing/extending-cloud-config.md).
  -->

### 个性化 {#personalization}

* **ContextHub 配置**

   * **ContextHub路径**  — 定义ContextHub [配置](/help/sites-cloud/authoring/personalization/contexthub.md)
   * **区段路径**  — 定义区 [段路径](/help/sites-cloud/authoring/personalization/contexthub-segmentation.md)

* **定位配置**

   * **品牌**  — 定义一 [个品牌以指定定位的范围](/help/sites-cloud/authoring/personalization/targeted-content.md)。
   >[!NOTE]
   >此选项要求用户帐户属于 `Target Administrators` 组。

### 权限 {#permissions}

* **权限**

   * 添加权限
   * 编辑已关闭的用户组
   * 查看有效权限

   <!--[Add Permissions](/help/sites-administering/user-group-ac-admin.md) -->

   <!-- [Edit Closed User Group](/help/sites-administering/cug.md#applying-your-closed-user-group-to-content-pages)-->

   <!-- View the [Effective Permissions](/help/sites-administering/user-group-ac-admin.md)-->

### Blueprint {#blueprint}

此选项卡仅对用作蓝图的页面可见。 Blueprint用作Live Copy的基础是[多站点管理的一部分。](/help/sites-cloud/administering/msm/overview.md)

* **当前Live Copy**  — 列出基于（即此Blueprint页面的Live Copy）的页面

* **转出配置**  — 控制将修改传播到Live Copy的情况

### Live Copy {#live-copy}

* **同步**  — 将Live Copy与Blueprint同步，并保留本地修改
* **重置**  — 将Live Copy重置为Blueprint状态，删除本地修改
* **暂停**  — 暂停Live Copy以进一步转出修改
* **分离**  — 从Blueprint中分离Live Copy

* **源**

   * 显示此Live Copy的Blueprint的路径

* **状态**

   * 列出页面的当前Live Copy状态

* **配置**

   * **Live Copy继承**  — 如果选中此选项，则Live Copy配置对所有子项都有效
   * **从父项继承转出配置**  — 如果选中此选项，则转出配置将从页面的父项继承
   * **选择转出配置**  — 定义将从Blueprint传播修改的情况，并且仅在未选择从父项继承转出配 **置时** 可用

## 编辑页面属性 {#editing-page-properties-1}

* 从&#x200B;**站点**&#x200B;控制台中：
   * [创建一个新页面](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#creating-a-new-page)（一部分属性）
   * 单击或点按&#x200B;**属性**
      * 单个页面
      * 多个页面（只有一部分属性可用于整体编辑）
* 在页面编辑器中：
   * 使用&#x200B;**页面信息**（然后&#x200B;**打开属性**）

### 从“站点”控制台中 - 单个页面 {#from-the-sites-console-single-page}

单击或点按&#x200B;**属性**&#x200B;以定义页面属性：

1. 使用&#x200B;**站点**&#x200B;控制台，导航到要查看和编辑属性的页面位置。
1. 使用以下任一方式为所需的页面选择&#x200B;**属性**&#x200B;选项：
   * [快速操作](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions)
   * [选择模式](/help/sites-cloud/authoring/getting-started/basic-handling.md#selecting-resources)
   * 此时将使用相应的选项卡显示页面属性。
1. 查看或编辑所需的属性。
1. 然后，使用&#x200B;**保存**&#x200B;以保存您的更新，接着使用&#x200B;**关闭**&#x200B;以返回到控制台。

### 编辑页面时 {#when-editing-a-page}

在编辑页面时，您可以使用&#x200B;**页面信息**&#x200B;来定义页面属性：

1. 打开要编辑属性的页面。
1. 选择&#x200B;**页面信息**&#x200B;图标以打开选择菜单：
1. 选择&#x200B;**打开属性**，此时将打开一个用于编辑属性的对话框，这些属性按相应的选项卡进行排序。工具栏右侧还提供以下按钮：
   * **取消**
   * **保存并关闭**
1. 使用&#x200B;**保存并关闭**&#x200B;按钮以保存更改。

### 从“站点”控制台中 - 多个页面 {#from-the-sites-console-multiple-pages}

从“站 **点** ”控制台中，您可以选择多个页面，然后使用&#x200B;**查看属性** ，以查看和／或编辑页面属性。 这称为批量编辑页面属性。

>[!NOTE]
>
>也可以对资产使用批量编辑属性功能。其操作大体相同，只有少数几点差别。有关详细信息，请参阅编辑多个资产的属性。
>
>还有一个批量编辑器，通过该编辑器，您可以使用 GQL（Google 查询语言）从多个页面中搜索内容，接着直接在批量编辑器中编辑内容，然后将更改保存到原始页面中。

<!--
>Bulk editing of properties is also available for Assets. It is very similar, but differs in a few points. See [Editing Properties of Multiple Assets](/help/assets/managing-multiple-assets.md) for details.
>
>There is also the [Bulk Editor](/help/sites-administering/bulk-editor.md), which allows you to search for content from multiple pages using GQL (Google Query Language) and then edit the content directly in the bulk editor before saving your changes to the originating pages.
-->

可以通过多种方法选择要批量编辑的多个页面，这些方法包括：

* 在浏览&#x200B;**站点**&#x200B;控制台时
* 在使用&#x200B;**搜索**&#x200B;找到一组页面后

选择页面后，单击或点按&#x200B;**属性选项**，此时将会显示批量属性：

![批量编辑页面属性](/help/sites-cloud/authoring/assets/page-properties-bulk-edit.png)

只有符合以下条件的页面才能进行批量编辑：

* 属于同一资源类型
* 不是 Live Copy 的一部分
   * 如果有任何页面在 Live Copy 中，将会在属性打开时显示一条消息。

进入“批量编辑”后，您可以：

* **查看**

   * 受影响的页面列表
      * 您可以根据需要进行选择/取消选择
      * 选项卡
         * 与查看单个页面的属性时一样，这些属性按选项卡进行排序。
   * 一部分属性
      * 将显示所有选定页面的可用属性，这些属性已明确定义为可批量编辑。
      * 如果将选择的页面减少到一页，则会显示所有属性。
   * 具有相同值的通用属性
      * 在“查看”模式中，只显示具有相同值的属性。
      * 当字段有多个值时（例如“标记”），只有在&#x200B;*所有值*&#x200B;均相同的情况下，才会显示这些值。如果只有部分值相同，则仅在编辑时才显示它们。
      * 如果不存在具有相同值的属性，则会显示一条消息。

* **编辑**

   * 您可以更新可用字段中的值。
      * 当您选择&#x200B;**完成**&#x200B;时，新值将会应用于所有选定页面。
      * 当字段有多个值时（例如“标记”），您可以附加一个新值，也可以删除相同的值。
   * 如果不同页面具有相同的字段，但这些字段的值不同，则会用一个特殊的值表示它们，例如，文本 `<Mixed Entries>`。编辑此类字段时应格外小心，以防数据丢失。

>[!NOTE]
>
>可以对页面组件进行配置，以指定可批量编辑的字段。请参阅配置页面以批量编辑页面属性。

<!--
>The page component can be configured to specify the fields available for bulk editing. See [Configuring your page for bulk editing of page properties](/help/sites-developing/bulk-editing.md).
-->
