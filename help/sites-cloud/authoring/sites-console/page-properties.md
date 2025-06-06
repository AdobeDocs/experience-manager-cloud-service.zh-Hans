---
title: 编辑页面属性
description: 了解如何定义在 AEM 中管理页面所需的属性。
exl-id: 27521a6d-c6e9-4f43-9ddf-9165b0316084
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 8d31907392e09bc5b3c669b8f8f23d6a2a26ced4
workflow-type: tm+mt
source-wordcount: '2454'
ht-degree: 83%

---

# 编辑页面属性 {#editing-page-properties}

您可以为页面定义所需的属性。这些属性会因页面性质而异。例如，某些页面可能会连接到 Live Copy，而其他页面则可能不会，Live Copy 信息在适当情况下才可用。

## 页面属性 {#page-properties}

属性分布于多个选项卡中。

### 基本 {#basic}

* **标题和标记**

   * **标题** — 页面的标题显示在各种不同的位置。 例如，**网站**&#x200B;选项卡列表和&#x200B;**站点**&#x200B;卡片/列表视图。
      * 这是必填字段。
   * **标记** – 在此处，可以通过更新选择框中的列表在页面中添加或移除标记。
      * 选择标记后，它会列在选择框下。您可以使用“x”从此列表中移除标记。
      * 可通过在空白选择框中键入名称输入全新标记。
         * 按 Enter 会创建新标记。
         * 随后将会显示新标记，其右侧带有一个小星星，表示该标记为新标记。
      * 使用下拉列表功能，可从现有标记中进行选择。
      * 当您将鼠标悬停在选择框中的标记条目上时，会显示 x，用于为此页面删除该标记。
      * 有关标记的更多信息，请访问[使用标记](/help/sites-cloud/authoring/sites-console/tags.md)。
   * **在导航中隐藏** – 指示在生成的站点的页面导航中是显示还是隐藏页面。

* **品牌化**

  通过将品牌概要附加到每个页面标题，跨页面应用一致的品牌识别。此功能需要使用2.14.0版或更高版本的[核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hans)中的页面组件。

   * **Brand Slug**

      * **覆盖** – 选中可在此页面上定义品牌概要。
         * 该值会由任何子页面继承，除非它们也设置了&#x200B;**覆盖**&#x200B;值。
      * **覆盖值** – 要附加到页面标题的品牌概要的文本。
         * 该值附加到页面标题后的竖线字符后，例如“骑行 Tuscany | 始终准备好使用 WKND”

* **HTML ID**

   * **ID** – 要应用于组件的 HTML ID。

* **更多标题和描述**

   * **页面标题** – 要在页面上使用的标题。通常由标题组件使用。如果留空，则会使用&#x200B;**标题**。
   * **导航标题** – 您可以指定单独的标题以便在导航中使用（例如，当您希望某些内容能更加简洁时）。如果留空，则会使用&#x200B;**标题**。
   * **标题** — 页面上使用的子标题。
   * **描述** – 页面的描述、用途或要添加的任何其他详细信息。

* **开启/结束时间**

  >[!NOTE]
  >
  > 请参阅[开启和结束时间 – 触发器配置](/help/operations/replication.md#on-and-off-times-trigger-configuration)，了解有关如何配置相关自动复制的详细信息。

  >[!NOTE]
  >如果&#x200B;**开启时间**&#x200B;或&#x200B;**结束时间**&#x200B;是过去的时间，并且已配置自动复制，则会立即触发相关操作。

   * **开启时间** – 使已发布页面在发布环境中可见（呈现）的日期和时间。该页面必须手动发布或通过预配置的自动复制进行发布。

      * 如果已经[发布（手动）](/help/sites-cloud/authoring/sites-console/publishing-pages.md)，此页面会保持隐匿（隐藏）状态，直到在指定时间才呈现。
      * 如果未发布并配置为自动复制，则页面会在指定时间自动发布并呈现。
      * 如果未发布且未配置为自动复制，则该页面不会自动发布，因此，在尝试访问该页面时会显示 404。

   * **结束时间** – 与&#x200B;**开启时间**&#x200B;类似并且经常与其结合使用，可定义已发布页面在发布环境中隐藏的时间。

   * 对要立即发布并在发布环境中可用的页面，将这两个字段（**开启时间**&#x200B;和&#x200B;**结束时间**）保留为空，直到它们被停用（一般场景）。

* **虚 URL**

   * 让您输入此页面的虚 URL，以便使用更短并且/或者含意更清楚的 URL。
   * 例如，如果将网站 `http://example.com` 的虚 URL 设置为由路径 `/v1.0/startpage` 标识的 `welcome` 页面，则 `http://example.com/welcome` 将成为 `http://example.com/content/v1.0/startpage` 的虚 URL

  >[!CAUTION]
  >
  >虚 URL：
  >
  >* 必须是唯一的，因此您应该确保该值没有被其他页面使用。
  >* 不支持正则表达式模式。
  >* 不应设置为现有页面。

   * **添加** — 选择此项可显示一个字段来定义页面的虚URL。
      * 再次选择可添加多个。
      * 选择&#x200B;**删除**&#x200B;图标以删除虚URL。
   * **重定向虚 URL** – 指示您是否希望页面使用虚 URL。

### 高级 {#advanced}

* **设置**

   * **语言** – 页面语言
   * **语言根** – 如果页面是语言副本的根，则必须选中
   * **重定向** — 指示此页面应以HTML `302 Found`状态自动重定向到的页面。
      * **永久重定向** – 选中后，页面将重定向到与 HTML `301 Moved Permanently` 状态一起提供的目标路径。
   * **设计** – 指示在生成的站点的页面导航中是显示还是隐藏页面
   * **别名** – 指定要用于此页面的别名
      * 例如，如果您为页面 `/content/wknd/us/en/magazine/members-only` 定义别名 `private`，则也可以通过 `/content/wknd/us/en/magazine/private` 访问此页面
      * 创建别名将设置页面节点上的 `sling:alias` 属性，这只会影响资源，而不会影响存储库路径。
      * 无法发布编辑器中按别名处理的页面。编辑器中的[发布选项](/help/sites-cloud/authoring/sites-console/publishing-pages.md)仅适用于通过其实际路径访问的页面。
      * 请参阅SEO和URL管理最佳实践下的[本地化页面名称](/help/overview/seo-and-url-management.md#localized-page-names)。

* **配置**

   * **从 &lt;path> 继承** – 启用/禁用继承；切换&#x200B;**云配置**&#x200B;的可用性以供选择

   * **云配置** – 所选配置的路径

* **模板设置**

   * **允许的模板** – [定义在此子分支内可用的模板的列表](/help/sites-cloud/authoring/page-editor/templates.md#enabling-and-allowing-a-template-template-author)
   * **将页面用作模板** - [基于当前页面创建新模板。](/help/sites-cloud/authoring/universal-editor/templates.md)
      * 仅适用于通过Edge Delivery Services与通用编辑器一起使用而创建的页面。

* **身份验证要求**

   * **启用** – 允许使用身份验证来访问页面

     >[!NOTE]
     >
     >页面的已关闭的用户组在&#x200B;**[权限](#permissions)**&#x200B;选项卡上定义。

   * **登录页面** – 要用于登录的页面

* **导出**

   * **导出配置** – 指定导出配置

* **SEO**

   * **规范 URL** – 可用于覆盖页面的规范 URL；如果留空，则页面的 URL 是其规范 URL

   * **机器人标记** – 选择机器人标记来控制搜索引擎爬网程序的行为。

     >[!NOTE]
     >
     >部分选项之间是相互冲突的。如果发生冲突，以更宽松的选项为准。

   * **生成 Sitemap** – 如果选中，则系统会为此页面及其子级页面生成 sitemap.xml。

### 图像 {#images}

* **特色图像**

  选择并配置要突出显示的图像。这用在引用页面的组件中；例如，Teaser、页面列表等。

   * **图像**

     您可以&#x200B;**选取**&#x200B;资源，或浏览找到要上传的文件，然后选择&#x200B;**编辑**&#x200B;或&#x200B;**清除**。

   * **替换文本** – 用于表示图像的含义和/或功能的文本；例如，供屏幕阅读器使用。

   * **继承 – 从 DAM 资源中提取的值** – 如果选中，这将使用 DAM 中 `dc:description` 元数据的值填充替换文本

* **缩略图**

  配置页面缩略图

   * **生成预览** – 生成要用作缩略图的页面预览
   * **上传图像** – 上传要用作缩略图的图像
   * **选择图像** – 选择要用作缩略图的现有资源
   * **还原** – 在您对缩略图进行更改后，此选项将变得可用。如果不想保留您的更改，可以在保存前还原更改。

### Cloud Service {#cloud-services}

* **Cloud Service 配置** – 定义 Cloud Service 的属性

### 个性化 {#personalization}

* **ContextHub 配置**

   * **从 &lt;path> 继承** – 启用/禁用继承；切换&#x200B;**ContextHub 路径**&#x200B;和&#x200B;**区段路径**&#x200B;的可用性以供选择

   * **ContextHub 路径** – 定义 [ContextHub 配置](/help/sites-cloud/authoring/personalization/contexthub.md)
   * **区段路径** – 定义[区段路径](/help/sites-cloud/authoring/personalization/contexthub-segmentation.md)

* **定位配置**

   * **品牌** – 定义一个[品牌以指定定位的范围](/help/sites-cloud/authoring/personalization/targeted-content.md)。

  >[!NOTE]
  >此选项要求用户帐户属于 `Target Administrators` 组。

### 权限 {#permissions}

* **权限**

   * **添加权限**
   * **编辑已关闭的用户组**
   * 查看&#x200B;**有效权限**

### Blueprint {#blueprint}

此选项卡仅对用作 Blueprint 的页面可见。Blueprint 用作 Live Copy 的基础，并且是[多站点管理](/help/sites-cloud/administering/msm/overview.md)的一部分。

* **当前 Live Copy** – 列出基于此 Blueprint 页面的页面（即 Live Copy 页面）

* **转出配置** – 控制修改内容会传播到 Live Copy 的情况

### Live Copy {#live-copy}

此选项卡仅对配置为 Live Copy 的页面可见。与 Blueprint 一样，Live Copy 是[多站点管理](/help/sites-cloud/administering/msm/overview.md)的一部分。

* **同步** – 将 Live Copy 与 Blueprint 同步，并保留本地修改
* **重置** – 将 Live Copy 重置为 Blueprint 的状态，并删除本地修改
* **暂停** – 暂停 Live Copy 以防止进一步的转出修改
* **分离** – 从 Blueprint 分离出 Live Copy

* **来源**

   * 显示此 Live Copy 的 Blueprint 的路径

* **状态**

   * 列出页面的当前 Live Copy 状态

* **配置**

   * **Live Copy 继承** – 如果选中，Live Copy 配置将在所有子项上都有效
   * **从父项继承转出配置** – 如果选中，则从页面的父页面继承转出配置
   * **选择转出配置** – 定义从 Blueprint 传播修改的情况，并且仅在未选择&#x200B;**从父项继承转出配置**&#x200B;时可用

### 预览 {#preview}

启用“预览”环境后，您将看到以下内容：

* 预览 URL – 用于访问预览环境中的内容的 URL

### 渐进式 Web 应用程序 {#progressive-web-app}

通过简单配置，内容作者现在可以为在 AEM Sites 中创建的体验启用渐进式 Web 应用程序 (PWA) 功能。

>[!NOTE]
>
>有关更多详细信息，请参阅[启用渐进式Web应用程序功能](/help/sites-cloud/authoring/sites-console/enable-pwa.md)。

{{pwa-deprecation}}

* **配置安装体验**

   * **启用 PWA** – 启用/禁用该功能；允许用户将站点作为 PWA 安装
   * **StartupURL** – 首选启动 URL
   * **显示模式** – 如何隐藏浏览器或如何以其他方式将浏览器提供给本地设备上的用户
   * **屏幕方向** – PWA 将如何处理设备方向
   * **主题颜色** – 应用程序的颜色，将影响本地用户的操作系统显示本机 UI 工具栏和导航控件的方式
   * **背景颜色** – 应用程序的背景颜色，此颜色在应用程序加载时显示
   * **图标** – 在用户设备上表示应用程序的图标

* **缓存管理（高级）**

   * **缓存策略和内容刷新频率** – 定义 PWA 的缓存模型
   * **为了脱机使用而要缓存的文件**
      * **文件预缓存（技术预览版）** – 托管于 AEM 上的文件会在安装 Service Worker 时和使用它之前保存到本地浏览器缓存中
      * **客户端库** – 用于缓存以提供脱机体验的客户端库
      * **路径包含** – 根据配置的缓存策略和内容刷新频率，拦截定义路径的网络请求并返回缓存内容
      * **路径排除** – 绝不会缓存这些文件，不管文件预缓存和路径包含下的设置如何

## 编辑页面属性 {#editing-page-properties-1}

* 从&#x200B;**Sites**&#x200B;控制台中：
   * [创建一个新页面](/help/sites-cloud/authoring/sites-console/creating-pages.md#creating-a-new-page)（一部分属性）
   * 单击或点按&#x200B;**属性**
      * 单页面
      * 多个页面（只有一部分属性可用于整体编辑）
* 从页面编辑器中：
   * 使用&#x200B;**页面信息**（然后&#x200B;**打开属性**）

### 从 Sites 控制台中 – 单个页面 {#from-the-sites-console-single-page}

单击或点按&#x200B;**属性**&#x200B;以定义页面属性：

1. 使用&#x200B;**Sites**&#x200B;控制台，导航到要查看和编辑属性的页面位置。
1. 使用以下任一方式为所需的页面选择&#x200B;**属性**&#x200B;选项：
   * [快速操作](/help/sites-cloud/authoring/basic-handling.md#quick-actions)
   * [选择模式](/help/sites-cloud/authoring/basic-handling.md#selecting-resources)
   * 此时会使用相应的选项卡显示页面属性。
1. 查看或编辑所需的属性。
1. 然后，使用&#x200B;**保存**&#x200B;来保存您的更新，接着使用&#x200B;**关闭**&#x200B;返回到控制台。

### 编辑页面时 {#when-editing-a-page}

在编辑页面时，您可以使用&#x200B;**页面信息**&#x200B;来定义页面属性：

1. 打开要编辑属性的页面。
1. 选择&#x200B;**页面信息**&#x200B;图标以打开选择菜单：
1. 选择&#x200B;**打开属性**，此时将打开一个对话框，允许您编辑按相应选项卡排序的属性。 工具栏右侧还提供以下按钮：
   * **取消**
   * **保存并关闭**
1. 使用&#x200B;**保存并关闭**&#x200B;按钮以保存更改。

### 从 Sites 控制台中 – 多个页面 {#from-the-sites-console-multiple-pages}

从&#x200B;**Sites**&#x200B;控制台中，您可以选择多个页面，然后使用&#x200B;**查看属性**，查看和／或编辑页面属性。这称为批量编辑页面属性。

可以通过多种方法选择要批量编辑的多个页面，这些方法包括：

* 在浏览 **Sites** 控制台时
* 在使用&#x200B;**搜索**&#x200B;找到一组页面后

选择页面后，单击或点按&#x200B;**属性选项**，此时会显示批量属性：

![批量编辑页面属性](/help/sites-cloud/authoring/assets/page-properties-bulk-edit.png)

只有符合以下条件的页面才能进行批量编辑：

* 属于同一资源类型
* 不是 Live Copy 的一部分
   * 如果有任何页面在 Live Copy 中，则会在属性打开时显示一条消息。

进入“批量编辑”后，您可以：

* **查看**

   * 受影响的页面列表
      * 您可以根据需要进行选择/取消选择
      * 选项卡
         * 与查看单页面的属性时一样，这些属性按选项卡进行排序。
   * 一部分属性
      * 将显示所有选定页面的可用属性，这些属性已明确定义为可批量编辑。
      * 如果将选择的页面减少到一页，则会显示所有属性。
   * 具有相同值的通用属性
      * 在“查看”模式中，只显示具有相同值的属性。
      * 当字段为多值（例如，标记）时，只有在&#x200B;*所有*&#x200B;为通用时，才会显示值。 如果只有一些是通用的，则仅在编辑时才显示它们。
      * 如果不存在具有相同值的属性，则会显示一条消息。

* **编辑**

   * 您可以更新可用字段中的值。
      * 当您选择&#x200B;**完成**&#x200B;时，新值会应用于所有选定页面。
      * 当字段有多个值时（例如，“标记”），您可以附加新值或删除公共值。
   * 如果不同页面具有相同的字段，但这些字段的值不同，则会用一个特殊的值表示它们，例如，文本 `<Mixed Entries>`。

## 属性继承 {#inheritance}

如果页面基于Blueprint或从其他页面继承内容，则继承会反映在单个字段的&#x200B;**页面属性**&#x200B;窗口中。

![继承的属性](assets/property-inhertiance.png)

无法编辑继承的属性。 点按或单击特定字段旁边的&#x200B;**取消继承**&#x200B;图标以中断其继承。

![取消继承](assets/cancel-inheritance.png)

在&#x200B;**取消继承**&#x200B;模式中确认取消。

![取消继承确认模式](assets/cancel-inheriance-confirmation.png)

取消字段的继承后，该字段将变为可编辑。

![已取消继承](assets/property-inheritance-broken.png)

要恢复继承，请点击或单击字段旁边的&#x200B;**还原继承**&#x200B;图标。

![还原继承](assets/revert-inheritance.png)

在&#x200B;**还原继承**&#x200B;模式中确认还原。

![还原继承确认模式](assets/revert-inhertiance-confirmation.png)

选择&#x200B;**恢复继承后同步页面**&#x200B;以使用Blueprint中的最新值更新字段。 如果不这样做，则下次同步LiveCopy时将更新值。

>[!TIP]
>
>有关继承的详细信息，请参阅文档[多站点管理器和翻译](/help/sites-cloud/administering/msm-and-translation.md)
