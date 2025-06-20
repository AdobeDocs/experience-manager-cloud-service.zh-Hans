---
title: 页面属性
description: 了解页面可以具有的不同属性，以及这些属性如何控制页面行为以及如何管理页面。
exl-id: 27521a6d-c6e9-4f43-9ddf-9165b0316084
solution: Experience Manager Sites
feature: Authoring
role: User
mini-toc-levels: 2
source-git-commit: b9328a22ff544f2c663868d33d7b06e02819f1d7
workflow-type: tm+mt
source-wordcount: '2138'
ht-degree: 34%

---


# 页面属性 {#page-properties}

了解页面可以具有的不同属性，以及这些属性如何控制页面行为以及如何管理页面。

>[!TIP]
>
>有关如何编辑和更改页面属性的详细信息，请参阅文档[编辑页面属性。](/help/sites-cloud/authoring/sites-console/edit-page-properties.md)

## 概述和属性可用性 {#overview}

页面属性可以控制页面的许多方面，从页面的标题和品牌推广到其权限。 这些属性分布在多个选项卡中，其中一些选项卡可能会根据页面类型而隐藏。 与AEM中的大多数属性一样，可以继承[页面属性。](/help/sites-cloud/authoring/sites-console/edit-page-properties.md#inheritance)

>[!NOTE]
>
>本文档介绍了所有可能的页面属性。 根据页面类型，并非所有属性都可用。

## “基本”选项卡 {#basic}

### 标题和标记 {#title-tags}

* **标题** — 定义用于SEO的页面元标题以及页面内容中显示的标题（除非被覆盖）
   * 页面的标题显示在AEM UI中的各个位置，包括[站点控制台中的&#x200B;**站点**&#x200B;信息卡/列表视图。](/help/sites-cloud/authoring/sites-console/introduction.md)
   * 这是必填字段。
* **标记** — 定义用于SEO的页面元标记
   * 可以通过更新选择框中的列表在页面中添加或删除标记。
   * 使用下拉菜单从现有标记中进行选择。
   * 选择标记后，它会列在选择框下。您可以使用“x”从此列表中移除标记。
   * 可通过在空白选择框中键入名称输入全新标记。
      * 按 Enter 会创建新标记。
      * 随后将会显示新标记，其右侧带有一个小星星，表示该标记为新标记。
   * 当您将鼠标悬停在选择框中的标记条目上时，会显示 x，用于为此页面删除该标记。
   * 有关标记的详细信息，请参阅[使用标记。](/help/sites-cloud/authoring/sites-console/tags.md)
* **在导航中隐藏** — 指示在生成的站点的页面导航中是显示还是隐藏页面

### 品牌化 {#branding}

通过将品牌概要附加到每个页面标题，跨页面应用一致的品牌识别。此功能需要使用 2.14.0 版或更高版本的[核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hans)中的页面组件。

* **Brand Slug**
   * **覆盖** – 选中可在此页面上定义品牌概要。
      * 该值会由任何子页面继承，除非它们也设置了&#x200B;**覆盖**&#x200B;值。
   * **覆盖值** – 要附加到页面标题的品牌概要的文本。
      * 该值附加到页面标题后的竖线字符（如`Cycling Tuscany | Always ready for the WKND`）

### HTML ID {#html-id}

* **ID** – 要应用于组件的 HTML ID。

### 更多标题和说明 {#more-titles}

* **页面标题** — 要在页面上使用的标题
   * 这通常由标题组件使用。
   * 如果留空，则会使用&#x200B;**标题**。
* **导航标题** — 您可以指定单独的标题以在导航中使用（例如，如果您希望某些内容能更加简洁）。
   * 如果为空，则使用&#x200B;**页面标题**。
* **子标题** — 要在页面上使用的子标题
* **描述** — 页面的描述、用途或要添加的任何其他详细信息

### 开始/结束时间 {#on-off-time}

页面的打开/关闭时间是一种临时隐藏已发布内容的便捷方法。 关闭发布实例后，内容仍会保留在该实例上。 关闭页面不会取消发布内容。

* **开启时间** – 使已发布页面在发布环境中可见（呈现）的日期和时间。该页面必须手动发布或通过预配置的自动复制进行发布。

   * 如果已经[发布，](/help/sites-cloud/authoring/sites-console/publishing-pages.md)此页面在发布实例上可用，但在指定时间呈现之前保持隐匿（隐藏）状态。
   * 如果未发布并[配置为自动复制，](/help/operations/replication.md#on-and-off-times-trigger-configuratio)则页面将在指定的时间自动发布，然后呈现。
   * 如果未发布且未配置为自动复制，则该页面不会自动发布，因此在尝试访问该页面时将会显示404。

* **结束时间** – 与&#x200B;**开启时间**&#x200B;类似并且经常与其结合使用，可定义已发布页面在发布环境中隐藏的时间。

对于要发布的页面，请将这些字段（**开启时间**&#x200B;和&#x200B;**关闭时间**）留空，这些字段可立即在发布环境中使用并可用，直到它们被停用（一般场景）。

>[!NOTE]
>如果&#x200B;**开启时间**&#x200B;或&#x200B;**结束时间**&#x200B;是过去的时间，并且已配置自动复制，则会立即触发相关操作。

>[!TIP]
>
>开启/关闭时间严格处理已发布的内容（手动或通过自动复制）。 因此，发布工作流（例如批准内容的工作流）不会由触发为开启/关闭时间，并且开启/关闭时间不会影响页面的发布状态。 因此，打开/关闭时间最适合临时显示/隐藏已批准和发布的内容。
>
>如果要发布包含所有关联工作流的新内容，或从站点中完全删除（取消发布内容），请考虑[管理您的发布。](/help/sites-cloud/authoring/sites-console/publishing-pages.md#manage-publication)

### 虚 URL {#vanity-url}

通过此属性，您可以输入此页面的虚URL，这样可以具有更短的和/或更富表现性的URL。 例如，如果将网站 `http://example.com` 的虚 URL 设置为由路径 `/v1.0/startpage` 标识的 `welcome` 页面，则 `http://example.com/welcome` 将成为 `http://example.com/content/v1.0/startpage` 的虚 URL

>[!CAUTION]
>
>虚 URL：
>
>* 必须是唯一的。
>* 不支持正则表达式模式。
>* 不应设置为现有页面。

* **添加** — 选择此项可显示一个字段来定义页面的虚URL。
   * 再次选择可添加多个。
   * 选择&#x200B;**删除**&#x200B;图标以删除虚URL。
* **重定向虚URL** — 指示您希望页面使用虚URL还是重定向到页面的实际URL

## 高级 {#advanced}

### 设置 {#settings}

* **语言** – 页面语言
* **语言根** – 如果页面是语言副本的根，则必须选中
* **重定向** — 指示此页面应以HTML `302 Found`状态自动重定向到的页面
   * **永久重定向** – 选中后，页面将重定向到与 HTML `301 Moved Permanently` 状态一起提供的目标路径。
* **Design**
* **别名** – 指定要用于此页面的别名
   * 例如，如果您为页面 `/content/wknd/us/en/magazine/members-only` 定义别名 `private`，则也可以通过 `/content/wknd/us/en/magazine/private` 访问此页面
   * 创建别名将设置页面节点上的 `sling:alias` 属性，这只会影响资源，而不会影响存储库路径。
   * 无法发布编辑器中按别名处理的页面。编辑器中的[发布选项](/help/sites-cloud/authoring/sites-console/publishing-pages.md)仅适用于通过其实际路径访问的页面。
   * 有关详细信息，请参阅SEO和URL管理最佳实践下的[本地化页面名称](/help/overview/seo-and-url-management.md#localized-page-names)。

### 配置 {#configuration}

* **继承自&lt;path>** — 启用/禁用页面的&#x200B;**云配置**&#x200B;的继承
   * 切换&#x200B;**云配置**&#x200B;的可用性以进行编辑

* **云配置** – 所选配置的路径

### 模板设置 {#template-settings}

* **允许的模板** – [定义在此子分支内可用的模板的列表](/help/sites-cloud/authoring/page-editor/templates.md#enabling-and-allowing-a-template-template-author)
   * 每个值都必须是模板的绝对路径。
   * 使用`/.*`允许此路径下的所有模板。
* **将页面用作模板** - [基于当前页面创建新模板。](/help/sites-cloud/authoring/universal-editor/templates.md)
   * 仅适用于通过Edge Delivery Services与通用编辑器一起使用而创建的页面。

### 身份验证要求 {#authentication}

* **启用** — 允许使用身份验证访问页面

>[!NOTE]
>
>页面的已关闭的用户组在&#x200B;**[权限](#permissions)**&#x200B;选项卡上定义。

* **登录页面** – 要用于登录的页面

### 导出 {#export}

* **导出配置** – 指定导出配置

## SEO {#seo}

* **规范URL** — 用于覆盖页面的规范URL
   * 如果留空，则页面的URL是它的规范URL。

* **Robots标记** — 使用下拉菜单选择Robots标记以控制搜索引擎爬网程序的行为
   * 有些选项会相互冲突，在这种情况下，以更宽松的选项为准。

* **生成站点地图** — 在选中时，将为此页面及其后代生成`sitemap.xml`。

## 图像 {#images}

### 特色图像 {#featured-image}

此部分用于选择和配置要显示的图像。 这用于引用页面的组件；例如，Teaser、页面列表等。

* **图像** — 您可以&#x200B;**挑选**&#x200B;资源，或浏览要上传的文件，然后&#x200B;**编辑**&#x200B;或&#x200B;**清除**&#x200B;选定的图像。
* **替换文本** — 用于表示图像的含义和/或功能的文本，通常由屏幕阅读器使用
* **继承 — 取自DAM资源的值** — 选中后，将使用DAM中`dc:description`元数据的值填充替换文本。

### 缩略图 {#thumbnail}

此部分用于选择和配置页面的图像缩略图。 这用于引用页面的组件；例如，Teaser、页面列表等。

* **生成预览** – 生成要用作缩略图的页面预览
* **上传图像** – 上传要用作缩略图的图像
* **选择图像** — 选择要用作缩略图的现有资源
* **还原** – 在您对缩略图进行更改后，此选项将变得可用。如果不想保留您的更改，可以在保存前还原更改。

## Cloud Service {#cloud-services}

* **Cloud Service配置** — 定义用于页面的云服务的配置
* **继承自** — 对于活动副本和语言副本，默认从Blueprint继承云配置。
   * 取消选中以覆盖继承

## 个性化 {#personalization}

### ContextHub 配置 {#contexthub-config}

* **ContextHub 路径** – 定义 [ContextHub 配置](/help/sites-cloud/authoring/personalization/contexthub.md)
* **区段路径** – 定义[区段路径](/help/sites-cloud/authoring/personalization/contexthub-segmentation.md)

### 定位配置 {#targeting-config}

* **品牌** — 定义[品牌以指定定位的范围](/help/sites-cloud/authoring/personalization/targeted-content.md)
   * 此选项要求用户帐户属于`Target Administrators`组。

## 权限 {#permissions}

使用&#x200B;**权限**&#x200B;选项卡定义哪些用户、组或[封闭用户组(CUG)](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/advanced/closed-user-groups.html?lang=zh-Hans)可以访问和/或修改页面。

* **添加权限**
* **编辑已关闭的用户组**
* 查看&#x200B;**有效权限**

## Blueprint {#blueprint}

此选项卡仅对用作 Blueprint 的页面可见。Blueprint 用作 Live Copy 的基础，并且是[多站点管理](/help/sites-cloud/administering/msm/overview.md)的一部分。

* **转出** — 启动Blueprint内容到活动副本的转出
* **Live Copy概述** — 打开一个窗口以浏览Live Copy页面结构
* **当前活动副本** — 基于所选Blueprint页面的页面列表（即活动副本）

## Live Copy {#live-copy}

此选项卡仅对配置为 Live Copy 的页面可见。与[Blueprint一样，](#blueprint)活动副本是[多站点管理的一部分。](/help/sites-cloud/administering/msm/overview.md)

* **同步** — 将Live Copy与Blueprint同步，并保留本地修改
* **重置** — 将Live Copy重置为Blueprint的状态，并删除本地修改
* **暂停** – 暂停 Live Copy 以防止进一步的转出修改
* **分离** — 从Blueprint分离出Live Copy

### 源 {#source}

* 显示此 Live Copy 的 Blueprint 的路径

### 状态 {#status}

* 列出页面的当前 Live Copy 状态

### 配置 {#live-copy-config}

* **Live Copy继承** — 如果选中，Live Copy配置将在所有子项上都有效。
* **从父项继承转出配置** — 如果选中，则从页面的父项继承转出配置。
* **选择转出配置** – 定义从 Blueprint 传播修改的情况，并且仅在未选择&#x200B;**从父项继承转出配置**&#x200B;时可用
* **排除的路径列表**

## 预览 {#preview}

启用[预览环境](/help/sites-cloud/authoring/sites-console/previewing-content.md)后，可以使用以下详细信息：

* **预览URL** — 用于访问预览环境中的内容的URL

## 渐进式 Web 应用程序 {#progressive-web-app}

通过简单的配置，内容作者可以为在AEM Sites中创建的体验启用渐进式Web应用程序(PWA)功能。 然后，您的网站可以像本机应用程序一样运行，方法是将其安装在访客设备的主屏幕上并脱机使用。

{{pwa-deprecation}}

### 配置安装体验 {#config-pwa}

* **启用PWA** — 启用后，页面的访客可以安装站点作为PWA。
* **启动URL** — 用户启动Web应用时应加载的URL
   * 如果URL是相对的，则清单URL将用作要解析的基本URL
   * 如果为空，则使用安装应用程序时所在页面的URL。
   * 建议设置一个值。
* **显示模式** — 应如何隐藏浏览器或如何以其他方式将浏览器显示给本地设备上的用户
* **屏幕方向** - PWA如何处理设备方向
* **主题颜色** — 应用程序的颜色，它会影响本地用户的操作系统显示本机UI工具栏和导航控件的方式
* **背景颜色** — 应用程序的背景颜色，在应用程序加载时显示
* **图标** — 安装PWA时表示用户设备上应用程序的图标

### 缓存管理（高级） {#cache-management}

* **缓存策略和内容刷新频率** — 定义PWA的缓存模型。
* **为了脱机使用而要缓存的文件**
   * **文件预缓存（技术预览）** — 在AEM上托管的文件将在安装Service Worker时和使用它之前保存到本地浏览器缓存中。
   * **客户端库** — 要缓存的客户端库以提供脱机体验
   * **路径包含** — 已拦截定义路径的网络请求，并根据配置的缓存策略和内容刷新频率返回缓存的内容
   * **路径排除** — 无论文件预缓存和路径包含下的设置如何，绝不会缓存这些文件。

>[!NOTE]
>
>有关更多详细信息，请参阅[启用渐进式Web应用程序功能](/help/sites-cloud/authoring/sites-console/enable-pwa.md)。

