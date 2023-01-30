---
title: 将 Dynamic Media 查看器与 Analytics 和 Adobe Experience Platform 标记集成
description: 了解适用于Experience Platform标记的Dynamic Media查看器扩展和Dynamic Media查看器5.13。它允许Adobe Analytics和Platform标记的客户在其Experience Platform标记配置中使用特定于Dynamic Media查看器的事件和数据。
contentOwner: Rick Brough
feature: Asset Reports
role: Admin,User
exl-id: a71fef45-c9a4-4091-8af1-c3c173324b7a
source-git-commit: 35caac30887f17077d82f3370f1948e33d7f1530
workflow-type: tm+mt
source-wordcount: '6679'
ht-degree: 7%

---

# 将 Dynamic Media 查看器与 Analytics 和 Adobe Experience Platform 标记集成 {#integrating-dynamic-media-viewers-with-adobe-analytics-and-adobe-launch}

## 什么是Dynamic Media查看器与Adobe Analytics和Experience Platform标记的集成？ {#what-is-dynamic-media-viewers-integration-with-adobe-analytics-and-adobe-launch}

<!-- Leave this hidden path here; it points to the topic source from Sasha https://wiki.corp.adobe.com/pages/viewpage.action?spaceKey=~oufimtse&title=Dynamic+Media+Viewers+integration+with+Adobe+Launch 

name used to be Experience Platform Launch. Changed to Experience Platform Data Collection-->

*Dynamic Media查看器* “Experience Platform标签”和“Dynamic Media查看器5.13”的扩展允许Adobe Analytics和“Experience Platform标签”客户在其“Experience Platform标签”配置中使用特定于Dynamic Media查看器的事件和数据。

此集成意味着您可以使用Adobe Analytics跟踪Dynamic Media查看器在您网站上的使用情况。 同时，您可以将查看器公开的事件和数据与来自Adobe或第三方的任何其他Experience Platform标记扩展一起使用。

要了解有关Adobe扩展或第三方扩展的更多信息，请参阅 [Adobe扩展](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/overview.html) Experience Platform标记用户指南中的。

**本主题旨在介绍以下内容：** 站点管理员、Adobe Experience Manager计划的开发人员和操作人员。

### 集成的限制 {#limitations-of-the-integration}

* Dynamic Media查看器的Experience Platform标记集成在“Experience Manager创作”节点中不起作用。 在WCM页面发布之前，您无法看到任何跟踪。
* “弹出”操作模式不支持Dynamic Media查看器的Experience Platform标记集成，在该模式下，查看器URL是使用“资产详细信息”页面上的“URL”按钮获取的。
* Experience Platform标记集成不能与旧版查看器Analytics集成(通过 `config2=` 参数)。
* 视频跟踪支持仅限于核心播放跟踪，如 [跟踪概述](https://experienceleague.adobe.com/docs/media-analytics/using/tracking/track-av-playback/track-core-overview.html?lang=en#player-events). 尤其是，不支持QoS、广告、章节/区段或错误跟踪。
* 数据元素不支持使用 *Dynamic Media查看器* 扩展。 存储持续时间必须设置为 **[!UICONTROL 无]**.

### 集成用例 {#use-cases-for-the-integration}

与Experience Platform标记集成的主要用例是同时使用Experience Manager Assets和Experience Manager Sites的客户。 在这些情况下，您可以在Experience Manager创作节点和Experience Platform标记之间设置标准集成，然后将您的站点实例与Experience Platform标记属性相关联。 之后，添加到站点页面的任何Dynamic Media WCM组件都将跟踪查看器中的数据和事件。

请参阅 [在Experience Manager Sites中跟踪Dynamic Media查看者](#tracking-dynamic-media-viewers-in-aem-sites).

集成支持的次要用例是仅使用Experience Manager Assets或Dynamic Media Classic的客户。 在这种情况下，您将获取查看器的嵌入代码，并将其添加到网站页面。 然后，从Experience Platform标记中获取Experience Platform标记库生产URL，并手动将其添加到网页代码中。

请参阅 [使用嵌入代码跟踪Dynamic Media查看器](#tracking-dynamic-media-viewers-using-embed-code).

## 数据和事件跟踪在集成中的工作原理 {#how-data-and-event-tracking-works-in-the-integration}

该集成利用了两种单独且独立的Dynamic Media查看器跟踪类型： *Adobe Analytics* 和 *Adobe Analytics for Audio and Video*.

### 关于使用Adobe Analytics跟踪  {#about-tracking-using-adobe-analytics}

通过Adobe Analytics，您可以跟踪最终用户在与您网站上的Dynamic Media查看器进行交互时所执行的操作。 Adobe Analytics还允许您跟踪特定于查看者的数据。 例如，您可以跟踪和记录视图加载事件以及资产名称、发生的任何缩放操作和视频播放操作。

在Experience Platform标记中， *数据元素* 和 *规则* 合作以启用Adobe Analytics跟踪。

#### 关于Experience Platform标记中的数据元素 {#about-data-elements-in-adobe-launch}

“Experience Platform标记”中的数据元素是一个命名的属性，其值可以静态定义，或根据网页或Dynamic Media查看器数据的状态进行动态计算。

可用于数据元素定义的选项取决于Experience Platform标记属性中安装的扩展列表。 “核心”扩展已预安装，可在任何配置中开箱即用。 此“核心”扩展允许定义一个数据元素，其值来自Cookie、JavaScript代码、查询字符串和许多其他源。

对于Adobe Analytics跟踪，必须安装其他几个扩展，如 [安装和设置扩展](#installing-and-setup-of-extensions). Dynamic Media查看器扩展添加了定义数据元素的功能，该值是Dynamic Viewer事件的参数。 例如，可以引用查看器类型或查看器在加载时报告的资产名称、最终用户缩放时报告的缩放级别等。

Dynamic Media查看器扩展会自动保持其数据元素的值处于最新状态。

定义数据元素后，可以使用数据元素选取器小组件在Experience Platform标记UI的其他位置使用数据元素。 特别是，为Dynamic Media查看器跟踪目的定义的数据元素被规则中Adobe Analytics扩展的Set Variables Action（设置变量操作）引用（请参阅下文）。

请参阅 [数据元素](https://experienceleague.adobe.com/docs/experience-platform/tags/ui/data-elements.html) Experience Platform标记用户指南中的。

#### 关于Experience Platform标记中的规则 {#about-rules-in-adobe-launch}

Experience Platform标记中的规则是一个不可知的配置，它定义了构成规则的三个区域： *事件*, *条件*&#x200B;和 *操作*:

* *事件* (if)告知Experience Platform标记何时触发规则。
* *条件* (if)告知Experience Platform标记触发规则时允许或禁止的其他限制。
* *操作* (then)告知Experience Platform标记在触发规则时要执行的操作。

“事件”、“条件”和“操作”部分中可用的选项取决于“Experience Platform标记属性”中安装的扩展。 的 *核心* 扩展已预安装，可在任何配置中现成使用。 该扩展为事件提供了多个选项，例如基本的浏览器级别操作，包括焦点更改、按键和表单提交。 此外，它还包含用于“条件”的选项，例如Cookie值、浏览器类型等。 对于Actions，只有Custom Code选项可用。

对于Adobe Analytics跟踪，必须安装其他一些扩展，如 [安装和设置扩展](#installing-and-setup-of-extensions). 具体说来：

* Dynamic Media查看器扩展将支持的事件列表扩展到特定于Dynamic Media查看器的事件，如查看器加载、资产交换、放大和视频播放。
* Adobe Analytics扩展使用向跟踪服务器发送数据所需的两个操作来扩展受支持的操作列表： *设置变量* 和 *发送信标*.

要跟踪Dynamic Media查看器，可以使用以下任何类型：

* 来自Dynamic Media查看器扩展、核心扩展或任何其他扩展的事件。
* 规则定义中的条件。 或者，您也可以将条件区域留空。

在“操作”部分中，您需要具有 *设置变量* 操作。 此操作可告知Adobe Analytics如何使用数据填充跟踪变量。 同时， *设置变量* 操作不会向跟踪服务器发送任何内容。

的 *设置变量* 操作后面必须有 *发送信标* 操作。 的 *发送信标* 操作会实际将数据发送到analytics跟踪服务器。 两个操作， *设置变量* 和 *发送信标*，来自Adobe Analytics扩展。

请参阅 [规则](https://experienceleague.adobe.com/docs/experience-platform/tags/ui/rules.html) Experience Platform标记用户指南中的。

#### 示例配置 {#sample-configuration}

Experience Platform标记中的以下示例配置演示了如何在查看器加载时跟踪资产名称。

1. 从 **[!UICONTROL 数据元素]** 选项卡，定义数据元素 `AssetName` 引用 `asset` 参数 `LOAD` 事件。

   ![image2019-11](assets/image2019-11.png)

1. 从 **[!UICONTROL 规则]** 选项卡，定义规则 *TrackAssetOnLoad*.

   在此规则中， **[!UICONTROL 事件]** 字段会使用 **[!UICONTROL 加载]** 事件。

   ![image2019-22](assets/image2019-22.png)

1. 操作配置有Adobe Analytics扩展中的两种操作类型：

   *设置变量*，可将您选择的分析变量映射到的值 `AssetName` 数据元素。

   *发送信标*，用于向Adobe Analytics发送跟踪信息。

   ![image2019-3](assets/image2019-3.png)

1. 生成的规则配置如下所示：

   ![image2019-4](assets/image2019-4.png)

### 关于用于音频和视频的Adobe Analytics {#about-adobe-analytics-for-audio-and-video}

订阅Experience Cloud帐户以使用Adobe Analytics for Audio and Video后，就足以在 *Dynamic Media查看器* 扩展设置。 视频量度在Adobe Analytics中变得可用。 视频跟踪取决于是否存在Adobe MediumAnalytics for Audio and Video扩展。

请参阅 [安装和设置扩展](#installing-and-setup-of-extensions).

目前，对视频跟踪的支持仅限于“核心播放”跟踪，如 [跟踪概述](https://experienceleague.adobe.com/docs/media-analytics/using/tracking/track-av-playback/track-core-overview.html?lang=en#player-events). 尤其是，不支持QoS、广告、章节/区段或错误跟踪。

## 使用Dynamic Media查看器扩展 {#using-the-dynamic-media-viewers-extension}

如 [集成用例](#use-cases-for-the-integration)，则可以在Experience Manager Sites中通过新的“Dynamic Media标记”集成和使用嵌入代码来跟踪Experience Platform查看器。

### 在Experience Manager Sites中跟踪Dynamic Media查看者 {#tracking-dynamic-media-viewers-in-aem-sites}

要在Experience Manager Sites中跟踪Dynamic Media查看器，请执行 [配置所有集成块](#configuring-all-the-integration-pieces) 部分。 具体而言，您必须创建IMS配置和Experience Platform标记云配置。

在进行正确配置后，您使用Dynamic Media支持的WCM组件将任何添加到站点页面的Dynamic Media查看器自动跟踪到Adobe Analytics或Adobe Analytics for Video的数据，或同时跟踪这两者的数据。

请参阅 [使用Dynamic Media Assets将Adobe添加到页面](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md).

### 使用嵌入代码跟踪Dynamic Media查看器 {#tracking-dynamic-media-viewers-using-embed-code}

未使用Experience Manager Sites或将Dynamic Media查看器嵌入到Experience Manager Sites以外的网页中，或者不使用两者的客户，仍可以使用Experience Platform标记集成。

完成 [配置Adobe Analytics](#configuring-adobe-analytics-for-the-integration) 和 [配置Experience Platform标记](#configuring-adobe-launch-for-the-integration) 中。 但是，不需要执行与Experience Manager相关的配置步骤。

正确配置后，您可以使用Dynamic Media查看器向网页添加Experience Platform标记支持。

请参阅 [添加Experience Platform标记嵌入代码](https://experienceleague.adobe.com/docs/platform-learn/implement-in-websites/configure-tags/add-embed-code.html) 以了解有关如何使用Experience Platform标记库嵌入代码的更多信息。

要详细了解如何使用Experience ManagerDynamic Media的嵌入代码功能，请参阅 [在网页上嵌入视频查看器或图像查看器](/help/assets/dynamic-media/embed-code.md).

**使用嵌入代码跟踪Dynamic Media查看器：**

1. 为嵌入Dynamic Media查看器准备网页。
1. 首先登录“Experience Platform标记”库以获取“Experience Platform标记”的嵌入代码(请参阅 [配置Experience Platform标记](#configuring-adobe-launch-for-the-integration))。
1. 选择 **[!UICONTROL 属性]**，然后选择 **[!UICONTROL 环境]** 选项卡。
1. 选取与网页环境相关的环境级别。 然后，在 **[!UICONTROL 安装]** 列中，选择框图标。
1. **[!UICONTROL 在Web安装说明中]** ，请复制完整的Experience Platform标记库嵌入代码以及周围的代码 `<script/>` 标记。

## Dynamic Media查看器扩展的参考指南 {#reference-guide-for-the-dynamic-media-viewers-extension}

### 关于Dynamic Media查看器配置 {#about-the-dynamic-media-viewers-configuration}

如果满足以下条件，则Dynamic Media Viewer扩展会自动与Experience Platform标记库集成：

* Experience Platform标记库全局对象( `_satellite`)。
* Dynamic Media查看器扩展函数 `_dmviewers_v001()` 定义于 `_satellite`.

* `config2=` 未指定查看器参数，这意味着查看器不使用旧版Analytics集成。

此外，还有一个选项，可通过指定 `launch=0` 参数。 此参数的默认值为 `1`.

### 配置Dynamic Media查看器扩展 {#configuring-the-dynamic-media-viewers-extension}

Dynamic Media查看器扩展的唯一配置选项是 **[!UICONTROL 启用Adobe Medium分析以进行音频和视频]**.

当您选中（启用）此选项，并安装和配置Adobe MediumAnalytics for Audio and Video扩展后，视频播放量度将发送到Adobe Analytics for Audio and Video解决方案。 禁用此选项会关闭视频跟踪。

如果启用此选项 *无* 已安装Adobe MediumAnalytics for Audio and Video扩展，此选项不起作用。

![image2019-7-22_12-4-23](assets/image2019-7-22_12-4-23.png)

### 关于Dynamic Media查看器扩展中的数据元素 {#about-data-elements-in-the-dynamic-media-viewers-extension}

Dynamic Media Viewers 扩展提供的唯一数据元素类型是&#x200B;**[!UICONTROL 数据元素类型]**&#x200B;下拉列表中的&#x200B;**[!UICONTROL 查看器事件]**。

选中此选项后，数据元素编辑器将呈现一个包含两个字段的表单：

* **[!UICONTROL DM 查看器事件数据类型]** - 一个下拉列表，标识了 Dynamic Media 查看器扩展支持的所有查看器事件（具有参数）以及特殊的 **[!UICONTROL COMMON]** 项目。**[!UICONTROL COMMON]** 项目表示事件参数列表，这些事件参数对查看器发送的所有类型事件都是通用的。
* **[!UICONTROL 跟踪参数]**  — 选定Dynamic Media查看器事件的参数。

![image2019-7-22_12-5-46](assets/image2019-7-22_12-5-46.png)

请参阅 [Dynamic Media查看器参考指南](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/c-html5-s7-aem-asset-viewers.html) 对于每种查看器类型支持的事件列表；转到“特定查看器”部分，然后选择“支持Adobe Analytics跟踪”子部分。 目前，《Dynamic Media查看器参考指南》未记录事件参数。

现在，我们来考虑一下Dynamic Media查看器的生命周期 *数据元素*. 在页面上发生相应的Dynamic Media查看器事件后，将填充此类数据元素的值。 例如，假定数据元素指向 **[!UICONTROL 加载]** 事件及其“asset”参数。 此类数据元素的值会在查看器首次运行LOAD事件后接收有效数据。 如果数据元素指向 **[!UICONTROL 缩放]** 事件及其“scale”参数中，此类数据元素的值将保持为空，直到查看器发送 **[!UICONTROL 缩放]** 事件。

同样，当查看器在页面上发送相应事件时，数据元素的值也会自动更新。即使在规则配置中未指定特定事件，也会发生值更新。例如，假设数据元素 **[!UICONTROL 缩放比例]** 为ZOOM事件的“scale”参数定义。 但是，规则配置中唯一存在的规则由 **[!UICONTROL 加载]** 事件。 的值 **[!UICONTROL 缩放比例]** 用户每次在查看器中运行缩放时，仍会更新缩放。

任何Dynamic media查看器在网页上都有唯一标识符。 数据元素会跟踪值本身以及填充该值的查看器。 例如，假定同一页面上有多个查看器，并且 **[!UICONTROL AssetName]** 指向 **[!UICONTROL 加载]** 事件及其“asset”参数。 的 **[!UICONTROL AssetName]** 数据元素会维护一个资产名称集合，这些资产名称与页面上加载的每个查看器相关联。

数据元素返回的确切值取决于上下文。 如果在由Dynamic Media查看器事件触发的规则中请求数据元素，则会为启动该规则的查看器返回数据元素值。 而且，数据元素是在由来自其他一些Experience Platform标记扩展的事件触发的规则中请求的。 此时，数据元素的值来自上次更新此数据元素的查看器。

**请考虑以下示例设置：**

* 具有两个Dynamic Media缩放查看器的网页： *查看器1* 和 *viewer2*.

* **[!UICONTROL 缩放比例]** 数据元素指向 **[!UICONTROL 缩放]** 事件及其“scale”参数。
* **[!UICONTROL TrackPan]** 具有以下项的规则：

   * 使用Dynamic Media查看器 **[!UICONTROL 盘]** 事件。
   * 发送的值 **[!UICONTROL 缩放比例]** 数据元素到Adobe Analytics。

* **[!UICONTROL TrackKey]** 具有以下项的规则：

   * 使用核心Experience Platform标记扩展中的按键事件作为触发器。
   * 发送的值 **[!UICONTROL 缩放比例]** 数据元素到Adobe Analytics。

现在，假设最终用户通过两个查看器加载网页。 在 *查看器1*&#x200B;放大到50%;然后，在 *viewer2*，则会放大到25%的比例。 在 *查看器1*，它们会在周围平移图像，最后在键盘上按下一个键。

最终用户的活动会导致对Adobe Analytics发起以下两个跟踪调用：

* 第一次调用是因为 **[!UICONTROL TrackPan]** 用户在 *查看器1*. 该调用会发送50%作为值 **[!UICONTROL 缩放比例]** 数据元素，因为数据元素知道规则是由 *查看器1* 并提取相应的比例值；
* 第二次调用是因为 **[!UICONTROL TrackKey]** 用户按下键盘上的键时，将触发规则。 该调用会发送25%作为值 **[!UICONTROL 缩放比例]** 数据元素，因为规则不是由查看器触发的。 因此，数据元素会返回最新值。

上述设置的示例还会影响数据元素值的生命周期。 即使在将查看器本身置于网页上，Dynamic Media查看器管理的Experience Platform元素值也会存储在Data Tags库代码中。 此功能意味着，如果存在由非Dynamic Media查看器扩展触发并引用此类数据元素的规则，则数据元素会返回最后一个已知值。 即使查看器不再存在于网页上。

无论如何，由Dynamic Media查看器驱动的数据元素的值都不会存储在本地存储或服务器上；而是仅在客户端Experience Platform标记库中保留。 此类数据元素的值在网页重新加载时消失。

通常，数据元素编辑器支持 [存储持续时间选择](https://experienceleague.adobe.com/docs/experience-platform/tags/ui/data-elements.html#create-a-data-element). 但是，使用Dynamic Media查看器扩展的数据元素仅支持的存储持续时间选项 **[!UICONTROL 无]**. 在用户界面中可以设置任何其他值，但在这种情况下，不会定义数据元素行为。 扩展可自行管理数据元素的值：在整个查看器生命周期中维护查看器事件参数值的数据元素。

### 关于Dynamic Media查看器扩展中的规则 {#about-rules-in-the-dynamic-media-viewers-extension}

在规则编辑器中，扩展会为事件编辑器添加新的配置选项。 此外，该编辑器还提供了一个选项，可作为一个短操作选项在操作编辑器中手动引用事件参数，而不是使用预配置的数据元素。

#### 关于事件编辑器 {#about-the-events-editor}

在事件编辑器中，Dynamic Media查看器扩展添加了 **[!UICONTROL 事件类型]** 调用 **[!UICONTROL 查看器事件]**.

选择后，事件编辑器会呈现下拉菜单 **[!UICONTROL Dynamic Media查看器事件]**，列出Dynamic Media查看器支持的所有可用事件。

![image2019-8-2_15-13-1](assets/image2019-8-2_15-13-1.png)

#### 关于操作编辑器 {#about-the-actions-editor}

通过Dynamic Media查看器扩展，您可以使用Dynamic Media查看器的事件参数映射到Adobe Analytics扩展的“设置变量”编辑器中的分析变量。

要实现此目的，最简单的方法是完成以下两步流程：

* 首先，定义一个或多个数据元素，其中每个数据元素表示Dynamic Media查看器事件的参数。
* 最后，在Adobe Analytics扩展的Set Variables编辑器中，选择数据元素选取器图标（三个堆叠的磁盘）以打开“选择数据元素”对话框，然后从中选择一个数据元素。

![image2019-7-10_20-41-52](assets/image2019-7-10_20-41-52.png)

但是，可以使用替代方法并绕过数据元素创建。您可以直接引用Dynamic Media查看器事件中的参数。 在 **[!UICONTROL 值]** Analytics变量分配的输入字段。 确保你周围有百分比(%)的符号。 例如，

`%event.detail.dm.LOAD.asset%`

![image2019-7-12_19-2-35](assets/image2019-7-12_19-2-35.png)

使用数据元素和直接事件参数引用之间有重要区别。 对于数据元素，不管是哪个事件触发Set Variables操作。 触发规则的事件可能与动态查看器无关（例如，从核心扩展中选择网页）。 但是，在使用直接参数引用时，务必确保触发规则的事件与它引用的事件参数相对应。

例如，如果规 `%event.detail.dm.LOAD.asset%` 则是由Dynamic Media Viewer扩展的 **[!UICONTROL LOAD]** 事件触发的，则引用将返回正确的资产名称。 但是，对于任何其他事件，它都会返回一个空值。

下表列出了Dynamic Media查看器事件及其支持的参数：

<table>
 <tbody>
  <tr>
   <td>查看器事件名称</td>
   <td>参数引用</td>
  </tr>
  <tr>
   <td><code>COMMON</code></td>
   <td><code>%event.detail.dm.objID%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.compClass%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.instName%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.timeStamp%</code></td>
  </tr>
  <tr>
   <td><code>BANNER</code> </td>
   <td><code>%event.detail.dm.BANNER.asset%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.BANNER.frame%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.BANNER.label%</code></td>
  </tr>
  <tr>
   <td><code>HREF</code></td>
   <td><code>%event.detail.dm.HREF.rollover%</code></td>
  </tr>
  <tr>
   <td><code>ITEM</code></td>
   <td><code>%event.detail.dm.ITEM.rollover%</code></td>
  </tr>
  <tr>
   <td><code>LOAD</code></td>
   <td><code>%event.detail.dm.LOAD.applicationname%</code></td>
  </tr>
  <tr>
   <td><strong> </strong></td>
   <td><code>%event.detail.dm.LOAD.asset%</code></td>
  </tr>
  <tr>
   <td><strong> </strong></td>
   <td><code>%event.detail.dm.LOAD.company%</code></td>
  </tr>
  <tr>
   <td><strong> </strong></td>
   <td><code>%event.detail.dm.LOAD.sdkversion%</code></td>
  </tr>
  <tr>
   <td><strong> </strong></td>
   <td><code>%event.detail.dm.LOAD.viewertype%</code></td>
  </tr>
  <tr>
   <td><strong> </strong></td>
   <td><code>%event.detail.dm.LOAD.viewerversion%</code></td>
  </tr>
  <tr>
   <td><code>METADATA</code></td>
   <td><code>%event.detail.dm.METADATA.length%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.METADATA.type%</code></td>
  </tr>
  <tr>
   <td><code>MILESTONE</code></td>
   <td><code>%event.detail.dm.MILESTONE.milestone%</code></td>
  </tr>
  <tr>
   <td><code>PAGE</code></td>
   <td><code>%event.detail.dm.PAGE.frame%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.PAGE.label%</code></td>
  </tr>
  <tr>
   <td><code>PAUSE</code></td>
   <td><code>%event.detail.dm.PAUSE.timestamp%</code></td>
  </tr>
  <tr>
   <td><code>PLAY</code></td>
   <td><code>%event.detail.dm.PLAY.timestamp%</code></td>
  </tr>
  <tr>
   <td><code>SPIN</code></td>
   <td><code>%event.detail.dm.SPIN.framenumber%</code></td>
  </tr>
  <tr>
   <td><code>STOP</code></td>
   <td><code>%event.detail.dm.STOP.timestamp%</code></td>
  </tr>
  <tr>
   <td><code>SWAP</code></td>
   <td><code>%event.detail.dm.SWAP.asset%</code></td>
  </tr>
  <tr>
   <td><code>SWATCH</code></td>
   <td><code>%event.detail.dm.SWATCH.frame%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.SWATCH.label%</code></td>
  </tr>
  <tr>
   <td><code>TARG</code></td>
   <td><code>%event.detail.dm.TARG.frame%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.TARG.label%</code></td>
  </tr>
  <tr>
   <td><code>ZOOM</code></td>
   <td><code>%event.detail.dm.ZOOM.scale%</code></td>
  </tr>
 </tbody>
</table>

## 配置所有集成块 {#configuring-all-the-integration-pieces}

**开始之前**

Adobe建议您仔细查看此部分之前的所有文档，以便了解完整的集成。

本节介绍将Dynamic Media查看器与Adobe Analytics和Adobe Analytics for Audio and Video集成所需的配置步骤。 虽然可以在“Dynamic Media标记”中将Experience Platform查看器扩展用于其他目的，但本文档未涵盖此类情景。

您将使用以下Adobe产品配置集成：

* Adobe Analytics — 用于配置跟踪变量和报表。
* Experience Platform标记 — 用于定义属性、一个或多个规则以及一个或多个数据元素以启用查看器跟踪。

此外，如果此集成解决方案与Experience Manager Sites一起使用，则必须完成以下配置：

* [Adobe Developer控制台](https://developer.adobe.com/console/home)  — 为Experience Platform标记创建集成。
* Experience Manager创作节点 — IMS配置和Experience Platform标记云配置。

在配置中，请确保您有权访问Adobe Experience Cloud中已启用Adobe Analytics和Experience Platform标记的公司。

## 为集成配置Adobe Analytics {#configuring-adobe-analytics-for-the-integration}

配置Adobe Analytics后，将为集成设置以下内容：

* 已放置并选择报表包。
* Analytics变量可用于接收跟踪数据。
* 报表可用于查看Adobe Analytics中收集的数据。

另请参阅 [Analytics实施指南](https://experienceleague.adobe.com/docs/analytics/implementation/home.html).

**要为集成配置Adobe Analytics，请执行以下操作：**

1. 首先，从Experience Cloud访问Adobe Analytics [主页](https://experience.adobe.com/#/home). 在菜单栏中，选择页面右上角附近的“解决方案”图标（一个三乘三个圆点表），然后选择 **[!UICONTROL Analytics]**.

   ![2019-07-22_18-08-47](assets/2019-07-22_18-08-47.png)

   现在，选择一个报表包。

### 选择报表包 {#selecting-a-report-suite}

1. 在 Adobe Analytics 页面的右上角附近，在&#x200B;**[!UICONTROL 搜索报告]**&#x200B;字段的右侧，从下拉列表中选择正确的报表包。如果有多个可用报表包，并且您不确定要使用哪个报表包，请与 Adobe Analytics 管理员联系，帮助您选择要使用的报表包。

   在以下示例中，用户创建了一个名为 *DynamicMediaViewersExtensionDoc* 并从下拉列表中选择它。 报表包名称仅是一个示例。 最终选择的报表包名称由您来决定。

   如果没有可用的报表包，则您或您的Adobe Analytics管理员必须先创建一个报表包，然后才能继续进行配置。

   请参阅 [报表和报表包](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/manage-report-suites/report-suites-admin.html) 和 [创建报表包](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/manage-report-suites/c-new-report-suite/t-create-a-report-suite.html).

   在Adobe Analytics中，报表包在 **[!UICONTROL 管理员]** > **[!UICONTROL 报表包]**.

   ![2019-07-22_18-09-49](assets/2019-07-22_18-09-49.png)

   现在设置Adobe Analytics变量。

### 设置Adobe Analytics变量 {#setting-up-adobe-analytics-variables}

1. 指定一个或多个要用于跟踪Adobe Analytics查看器在网页上的行为的Dynamic Media变量。

   可以使用Adobe Analytics支持的任何类型的变量。 有关变量类型（如自定义流量）的决策 [prop]，转化 [eVar])受Analytics实施特定需求的驱动。

   请参阅 [prop和eVar概述](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar.html#vars).

   就本文档而言，将仅使用自定义流量(prop)变量，因为在网页上发生操作后几分钟内，Analytics报表中就会提供这些变量。

   要启用新的自定义流量变量，请在工具栏的Adobe Analytics中，转到 **[!UICONTROL 管理员]** > **[!UICONTROL 报表包]**.

1. 在 **[!UICONTROL 报表包管理器]** ，选择正确的报表，然后在工具栏中，转到 **[!UICONTROL 编辑设置]** > **[!UICONTROL 流量]** > **[!UICONTROL 流量变量]**.
1. 选取一个未使用的变量，为其提供一个描述性名称( **[!UICONTROL 查看器资产(prop 30)]**)，然后将组合框更改为“已启用”列中的“已启用”。

   以下屏幕截图是自定义流量变量( **[!UICONTROL prop30]**)来跟踪查看器使用的资产名称：

   ![image2019-6-26_23-6-59](/help/assets/dynamic-media/assets/image2019-6-26_23-6-59.png)

1. 在变量列表的底部，选择 **[!UICONTROL 保存]**.

### 设置报表 {#setting-up-a-report}

1. 通常，在Adobe Analytics中设置报表是由特定项目需求驱动的。 因此，详细报表设置不在此集成的范围之内。

   但是，在中设置自定义流量变量后，您就可以知道自定义流量报表在Adobe Analytics中自动可用 **[设置Adobe Analytics变量](#setting-up-adobe-analytics-variables)**.

   例如， **[!UICONTROL 查看器资产(prop 30)]** 变量可在“报表”菜单中的 **[!UICONTROL 自定义流量]** > **[!UICONTROL 自定义流量21-30]** > **[!UICONTROL 查看器资产(prop 30)]**.

   在查看器资产(prop 30)创 **[!UICONTROL 建后直接访问此报告]** ，不显示任何数据；在整合的这一阶段，人们就会期待它。

   ![image2019-6-26_23-12-49](/help/assets/dynamic-media/assets/image2019-6-26_23-12-49.png)

## 为集成配置Experience Platform标记 {#configuring-adobe-launch-for-the-integration}

配置Experience Platform标记后，将为集成设置以下内容：

* 创建新属性以将所有配置保持一致。
* 扩展的安装和设置。 资产中安装的所有扩展的客户端代码会一起编译到库中。 此库稍后供网页使用。
* 数据元素和规则的配置。 此配置定义要从Dynamic Media查看器获取哪些数据、何时触发跟踪逻辑，以及在Adobe Analytics中将查看器数据发送到何处。
* 发布库。

**要为集成配置Experience Platform标记，请执行以下操作：**

1. 首先，从Experience Platform访问Experience Cloud标记 [主页](https://experience.adobe.com/#/home). 在菜单栏中，选择页面右上角附近的“解决方案”图标（三个乘以三个圆点表），然后选择 **[!UICONTROL 标记]**.

   您还可以 [打开Experience Platform标记直接](https://launch.adobe.com/).

   ![image2019-7-8_15-38-44](assets/image2019-7-8_15-38-44.png)

### 在Experience Platform标记中创建属性 {#creating-a-property-in-adobe-launch}

“Experience Platform标记”中的属性是一个命名配置，可将所有设置保持在一起。 系统会生成配置设置库，并将其发布到不同的环境级别（开发、暂存和生产）。

另请参阅 [配置点按属性](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/initial-configuration/configure-tags.html).

**要在Experience Platform标记中创建属性，请执行以下操作：**

1. 在Experience Platform标记中，选择 **[!UICONTROL 新建资产]**.
1. 在&#x200B;**[!UICONTROL 创建属性]**&#x200B;对话框的&#x200B;**[!UICONTROL 名称]**&#x200B;字段中，键入描述性名称，如网站的标题。例如，`DynamicMediaViewersProp.`
1. 在 **[!UICONTROL 域]** 字段，输入网站的域。
1. 在&#x200B;**[!UICONTROL 高级选项]**&#x200B;下拉框中，启用&#x200B;**[!UICONTROL 配置以进行扩展开发（以后无法修改）]**，以防您要使用的扩展（本例中为 *Dynamic Media 查看器*）尚未发布。

   ![image2019-7-8_16-3-47](assets/image2019-7-8_16-3-47.png)

1. 选择&#x200B;**[!UICONTROL 保存]**。

   选择新创建的属性，然后继续 *安装和设置扩展*.

### 安装和设置扩展 {#installing-and-setup-of-extensions}

Experience Platform标记中的所有可用扩展都列在 **[!UICONTROL 扩展]** > **[!UICONTROL 目录]**.

要安装扩展，请选择 **[!UICONTROL 安装]**. 如果需要，请执行一次性扩展配置，然后选择 **[!UICONTROL 保存]**.

如有必要，必须安装和配置以下扩展：

* （必需） *Experience CloudID服务* 扩展

无需其他配置，接受任何建议的值。 完成后，请确保选择 **[!UICONTROL 保存]**.

请参阅 [Experience CloudIdentity Service扩展](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/id-service/overview.html).

* （必需） *Adobe Analytics* 扩展

要配置此扩展，您需要在Adobe Analytics下的 **[!UICONTROL 管理员]** > **[!UICONTROL 报表包]**，在 **[!UICONTROL 报表包ID]** 列标题。

(仅出于演示目的， **[!UICONTROL DynamicMediaViewersExtensionDoc]** 以下屏幕截图中使用了报表包。 此 ID 在之前的[选择报表包](#selecting-a-report-suite)中创建并使用。)

![image2019-7-8_16-45-34](assets/image2019-7-8_16-45-34.png)

在“安装扩展”页面的&#x200B;**[!UICONTROL 开发报表包]**&#x200B;字段、**[!UICONTROL 测试报表包]**&#x200B;字段和&#x200B;**[!UICONTROL 生产报表包]**&#x200B;字段中输入报表包 ID。

![image2019-7-8_16-47-40](assets/image2019-7-8_16-47-40.png)

*仅当您打算使用视频跟踪时，才配置以下项目：*

在 **[!UICONTROL 安装扩展]** 页面，展开 **[!UICONTROL 常规]**，然后指定跟踪服务器。 跟踪服务器遵循模板 `<trackingNamespace>.sc.omtrdc.net`，其中 `<trackingNamespace>` 是在预配电子邮件中获取的信息。

选择&#x200B;**[!UICONTROL 保存]**。

请参阅 [Adobe Analytics扩展](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/analytics/overview.html).

* (可选. 仅当需要视频跟踪时才需要) *Adobe Medium用于音频和视频的Analytics* 扩展

填写跟踪服务器字段。 的跟踪服务器 *Adobe Medium用于音频和视频的Analytics* 扩展与用于Adobe Analytics的跟踪服务器不同。 它遵循模板 `<trackingNamespace>.hb.omtrdc.net`，其中 `<trackingNamespace>` 是预配电子邮件中的信息。

所有其他字段均为可选字段。

请参阅 [Adobe MediumAnalytics for Audio and Video扩展](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/media-analytics/overview.html).

* （必需） *Dynamic Media查看器* 扩展

选择&#x200B;**[!UICONTROL 启用 Adobe Analytics for Video]** 以启用（打开）视频检测信号跟踪。

自本文起， *Dynamic Media查看器* 仅当创建Experience Platform标记属性以进行开发时，扩展才可用。

请参阅 [在Experience Platform标记中创建属性](#creating-a-property-in-adobe-launch).

安装和设置扩展后，Extensions > Installed区域中将至少列出以下五个扩展（如果您没有跟踪视频，则为四个）。

![image2019-7-22_12-7-36](assets/image2019-7-22_12-7-36.png)

### 设置数据元素和规则 {#setting-up-data-elements-and-rules}

在Experience Platform标记中，创建跟踪Dynamic Media查看器所需的数据元素和规则。

请参阅 [数据和事件跟踪在集成中的工作原理](#how-data-and-event-tracking-works-in-the-integration) ，了解有关使用Experience Platform标记进行跟踪的概述。

请参阅 [示例配置](#sample-configuration) 有关Experience Platform标记中的示例配置，其中演示了如何在查看器加载时跟踪资产名称。

请参阅 [配置Dynamic Media查看器扩展](#configuring-the-dynamic-media-viewers-extension) 以详细了解扩展的功能。

### 发布库 {#publishing-a-library}

要更改Experience Platform标记配置（包括设置的属性、扩展、规则和数据元素），您必须 *发布* 这种变化。 在Experience Platform标记中发布，可从属性配置下的发布选项卡中执行。

Experience Platform标记可能具有多个开发环境、一个暂存环境和一个生产环境。 默认情况下，Experience Manager中的Experience Platform标记云配置将Experience Manager创作节点指向平台标记的暂存环境。 “Experience Manager发布”节点指向“Experience Platform标记”的生产环境。 这种安排意味着，使用默认的Experience Manager设置，必须将Experience Platform标记库发布到暂存环境。 这样，您便可以在Experience Manager作者中使用它。 然后，您可以将其发布到生产环境，以便用于Experience Manager发布。

请参阅 [环境](https://experienceleague.adobe.com/docs/experience-platform/tags/publish/environments/environments.html) 有关Experience Platform标记环境的更多信息。

发布库涉及以下两个步骤：

* 通过将所有必要的更改（新更改和更新）包含到库中，以添加和构建新库。
* 在不同的环境级别（从开发到暂存和生产）中向上移动库。

#### 添加和构建新库 {#adding-and-building-a-new-library}

1. 首次在“Experience Platform标记”中打开“发布”选项卡时，库列表为空。

   在左列中，选择 **[!UICONTROL 添加新库]**.

   ![image2019-7-15_14-43-17](assets/image2019-7-15_14-43-17.png)

1. 在Create New Library页面上，在 **[!UICONTROL 名称]** 字段，为新库输入描述性名称。 例如，

   *DynamicMediaViewersLib*

   从环境下拉列表中，选择环境级别。 最初，只有开发级别可供选择。 在页面的左下侧附近，选择 **[!UICONTROL Add All Changed Resources]**.

   ![image2019-7-15_14-49-41](assets/image2019-7-15_14-49-41.png)

1. 在页面的右上角附近，选择 **[!UICONTROL 保存并构建以用于开发]**.

   几分钟后，即会创建并准备使用库。

   ![image2019-7-15_15-3-34](assets/image2019-7-15_15-3-34.png)

   >[!NOTE]
   >
   >下次更改Experience Platform标记配置时，转到 **[!UICONTROL 发布]** 选项卡 **[!UICONTROL 属性]** 配置中，然后选择您之前创建的库。
   >
   >
   >从库发布屏幕中，选择 **[!UICONTROL Add All Changed Resources]**，然后选择 **[!UICONTROL 保存并构建以用于开发]**.

#### 在环境级别中向上移动库 {#moving-a-library-up-through-environment-levels}

1. 添加新库后，即可在开发环境中找到该库。 要将其移至暂存环境级别（对应于已提交列），请从库的下拉菜单中，选择 **[!UICONTROL 提交以供审批]**.

   ![image2019-7-15_15-52-37](assets/image2019-7-15_15-52-37.png)

1. 在确认对话框中，选择 **[!UICONTROL 提交]**.

   在库移到Submitted列后，从库的下拉菜单中，选择 **[!UICONTROL 为暂存环境构建]**.

   ![image2019-7-15_15-54-37](assets/image2019-7-15_15-54-37.png)

1. 要将库从暂存环境移动到生产环境（即“已发布”列），请执行类似的过程。

   首先，从下拉菜单中，选择 **[!UICONTROL 批准发布]**.

   ![image2019-7-15_16-7-39](assets/image2019-7-15_16-7-39.png)

1. 从下拉菜单中，选择 **[!UICONTROL 构建并发布到生产环境]**.

   ![image2019-7-15_16-8-9](assets/image2019-7-15_16-8-9.png)

   请参阅 [发布](https://experienceleague.adobe.com/docs/experience-platform/tags/publish/overview.html) 以详细了解“Experience Platform标记”中的发布过程。

## 为集成配置Adobe Experience Manager {#configuring-adobe-experience-manager-for-the-integration}

<!-- Prerequisites list below should be verified by Sasha -->

前提条件:

* Experience Manager同时运行创作实例和发布实例。
* Experience Manager创作节点在Dynamic Media中设置。 <!-- Scene7 run mode (dynamicmedia_s7) -->
* Dynamic Media WCM组件在Experience Manager Sites中已启用。

Experience Manager配置包含以下两个主要步骤：

* Experience ManagerIMS的配置
* 配置Experience Platform标记云。

### 配置Experience ManagerIMS {#configuring-aem-ims}

1. 在Experience Manager作者中，选择工具图标（锤子），然后转到 **[!UICONTROL 安全性]** > **[!UICONTROL Adobe IMS配置]**.

   ![2019-07-25_11-52-58](assets/2019-07-25_11-52-58.png)

1. 在“AdobeIMC配置”页的左上角附近，选择 **[!UICONTROL 创建]**.
1. 在 **[!UICONTROL Adobe IMS技术帐户配置]** 页面，在 **[!UICONTROL 云解决方案]** 下拉列表中，选择 **[!UICONTROL Experience Platform数据收集]**.
1. 启用 **[!UICONTROL 创建新证书]**，然后在文本字段中，为证书输入任何有意义的值。 例如， *AdobeLaunchIMSCert*. 选择 **[!UICONTROL 创建证书]**.

   将显示以下信息消息：

   *要检索有效的访问令牌，必须将新证书的公共密钥添加到Adobe Developer上的技术帐户！*

   要关闭“信息”对话框，请选择 **[!UICONTROL 确定]**.

   ![2019-07-25_12-09-24](assets/2019-07-25_12-09-24.png)

1. 选择 **[!UICONTROL 下载公钥]** 下载公钥文件(`*.crt`)到本地系统。

   >[!NOTE]
   >
   >此时， ***保持打开*** the **[!UICONTROL Adobe IMS技术帐户配置]** 页面； ***不*** 关闭页面，然后 ***不*** 选择 **[!UICONTROL 下一个]**. 您将在稍后的步骤中返回此页。

   ![2019-07-25_12-52-24](assets/2019-07-25_12-52-24.png)

1. 在新的浏览器选项卡中，导航到 [Adobe Developer控制台](https://developer.adobe.com/console/integrations).

1. 从 **[!UICONTROL Adobe I/O控制台集成]** 页面的右上角附近，选择 **[!UICONTROL 新集成]**.
1. 在 **[!UICONTROL 创建新集成]** 对话框，请确保 **[!UICONTROL 访问API]** 选择单选按钮，然后选择 **[!UICONTROL 继续]**.

![2019-07-25_13-04-20](assets/2019-07-25_13-04-20.png)

1. 第二天 **[!UICONTROL 创建新集成]** 页面，启用（打开） **[!UICONTROL Experience Platform标记API]** 按钮。 在页面的右下角，选择 **[!UICONTROL 继续]**.

   ![2019-07-25_13-13-54](assets/2019-07-25_13-13-54.png)

1. 第三 **[!UICONTROL 创建新集成]** 页面，请执行以下操作：

   * 在 **[!UICONTROL 名称]** 字段，输入描述性名称。 例如， *DynamicMediaViewersIO*.

   * 在 **[!UICONTROL 描述]** 字段，输入集成的描述。

   * 在 **[!UICONTROL 公钥证书]** 区域，上传公钥文件(`*.crt`)。

   * 在 **[!UICONTROL 为Experience Platform标记API选择角色]** 标题，选择 **[!UICONTROL 管理员]**.

   * 在 **[!UICONTROL 为Experience Platform标记API选择一个或多个产品配置文件]** 标题中，选择名为的产品用户档案 **[!UICONTROL 标记 —  &lt;your_company_name>]**.

   ![2019-07-25_13-49-18](assets/2019-07-25_13-49-18.png)

1. 选择 **[!UICONTROL 创建集成]**.
1. 在 **[!UICONTROL 已创建集成]** 页面，选择 **[!UICONTROL 继续查看集成详细信息]**.

   ![2019-07-25_14-16-33](assets/2019-07-25_14-16-33.png)

1. 此时会显示集成详细信息页面，如下所示：

   >[!NOTE]
   >
   >***保持打开此集成详细信息页面***。您需要 **[!UICONTROL 概述]** 和 **[!UICONTROL JWT]** 一会儿就到。

   ![2019-07-25_14-35-30](assets/2019-07-25_14-35-30.png)
   *集成详细信息页面*

1. 返回之前打开的 **[!UICONTROL Adobe IMS 技术帐户配置]**&#x200B;页面。在页面的右上角，选择 **[!UICONTROL 下一个]** 打开 **[!UICONTROL 帐户]** 页面 **[!UICONTROL Adobe IMS技术帐户配置]** 窗口。

   (如果您之前关闭了页面，请返回Experience Manager作者，然后转到 **[!UICONTROL 工具]** > **[!UICONTROL 安全性]** > **[!UICONTROL Adobe IMS配置]**. 选择&#x200B;**[!UICONTROL 创建]**。在 **[!UICONTROL 云解决方案]** 下拉列表中，选择 **[!UICONTROL Experience Platform标记]**. 在&#x200B;**[!UICONTROL 证书]**&#x200B;下拉列表中，选择之前创建的证书的名称。

   ![2019-07-25_20-57-50](assets/2019-07-25_20-57-50.png)
   *Adobe IMS技术帐户配置 — 证书页面*

1. 的 **[!UICONTROL 帐户]** 页面有五个字段，要求您使用上一步中“集成详细信息”页面中的信息填写。

   ![2019-07-25_20-42-45](assets/2019-07-25_20-42-45.png)
   *Adobe IMS技术帐户配置 — 帐户页面*

1. 在 **[!UICONTROL 帐户]** ，请填写以下字段：

   * **[!UICONTROL 标题]**  — 输入描述性帐户标题。
   * **[!UICONTROL 授权服务器]**  — 返回到您之前打开的集成详细信息页面。 选择 **[!UICONTROL JWT]** 选项卡。 复制服务器名称（不带路径），如下所示。

（示例服务器名称仅供说明）   返回到&#x200B;**[!UICONTROL 帐户]**&#x200B;页面，然后将名称粘贴到相应的字段中。例如， `https://ims-na1.adobelogin.com/`
（示例服务器名称仅供说明）

   ![2019-07-25_15-01-53](assets/2019-07-25_15-01-53.png)
   *集成详细信息页面 — JWT选项卡*

1. **[!UICONTROL API 密钥]** - 返回到“集成详细信息”页面。选择 **[!UICONTROL 概述]** ，然后单击 **[!UICONTROL API密钥（客户端ID）]** 字段，选择 **[!UICONTROL 复制]**.

   返回到&#x200B;**[!UICONTROL 帐户]**&#x200B;页面，然后将密钥粘贴到相应的字段中。

   ![2019-07-25_14-35-333](assets/2019-07-25_14-35-333.png)
   *集成详细信息页面*

1. **[!UICONTROL 客户端密钥]** - 返回到“集成详细信息”页面。从 **[!UICONTROL 概述]** 选项卡，选择 **[!UICONTROL 检索客户端密钥]**. 在 **[!UICONTROL 客户端密钥]** 字段，选择 **[!UICONTROL 复制]**.

   返回到&#x200B;**[!UICONTROL 帐户]**&#x200B;页面，然后将密钥粘贴到相应的字段中。

1. **[!UICONTROL 负载]**  — 返回到集成详细信息页面。 从 **[!UICONTROL JWT]** 选项卡，复制整个JSON对象代码。

   返回到&#x200B;**[!UICONTROL 帐户]**&#x200B;页面，然后将代码粘贴到相应的字段中。

   ![2019-07-25_21-59-12](assets/2019-07-25_21-59-12.png)
   *集成详细信息页面 — JWT选项卡*

   “帐户”页面（已填写所有字段）与以下内容类似：

   ![2019-07-25_22-08-30](assets/2019-07-25_22-08-30.png)

1. 在 **[!UICONTROL 帐户]** 页面，选择 **[!UICONTROL 创建]**.

   配置了Experience ManagerIMS后，您现在将在 **[!UICONTROL Adobe IMS配置]**.

   ![image2019-7-15_14-17-54](assets/image2019-7-15_14-17-54.png)

## 为集成配置Experience Platform标记云 {#configuring-adobe-launch-cloud-for-the-integration}

1. 在Experience Manager作者中，在左上角附近，选择工具图标（锤子），然后转到 **[!UICONTROL Cloud Services]** > **[!UICONTROL Experience Platform标记配置]**.

   ![2019-07-26_12-10-38](assets/2019-07-26_12-10-38.png)

1. 在 **[!UICONTROL Experience Platform标记配置]** 页面的左侧面板中，选择要对其应用Experience Manager标签配置的Experience Platform站点。

   仅供示例之用， **`We.Retail`** 在以下屏幕截图中选择了网站。

   ![2019-07-26_12-20-06](assets/2019-07-26_12-20-06.png)

1. 在页面的左上角附近，选择 **[!UICONTROL 创建]**.
1. 在 **[!UICONTROL 常规]** 第（1/3页）页 **[!UICONTROL 创建Experience Platform标记配置]** ，请填写以下字段：

   * **[!UICONTROL 标题]**  — 输入描述性配置标题。 例如：`We.Retail Tags cloud configuration`。

   * **[!UICONTROL 关联的Adobe IMS配置]**  — 选择您之前在 [配置Experience ManagerIMS](#configuring-aem-ims).

   * **[!UICONTROL 公司]**  — 从 **[!UICONTROL 公司]** 下拉列表中，选择您的Experience Cloud公司。 列表会自动填充。

   * **[!UICONTROL 属性]**  — 从属性下拉列表中，选择您之前创建的Experience Platform标记属性。 列表会自动填充。

填写完所有字段后， **[!UICONTROL 常规]** 页面将类似于以下内容：

![image2019-7-15_14-34-23](assets/image2019-7-15_14-34-23.png)

1. 在左上角附近，选择 **[!UICONTROL 下一个]**.
1. 在 **[!UICONTROL 暂存]** 第（2/3页）页 **[!UICONTROL 创建Experience Platform标记配置]** ，请填写以下字段：

   在 **[!UICONTROL 库URI]** （统一资源标识符）字段中，检查Experience Platform标记库暂存版本的位置。 Experience Manager会自动填充此字段。

   此步骤仅供说明之用，它使用部署到AdobeCDN的Experience Platform标记库。

   >[!NOTE]
   >
   >检查以确保自动填充的库URI（统一资源标识符）的格式不正确。 如有必要，请修复它，以便URI表示协议相对URI。 也就是说，它从双正斜杠开始。
   >
   >
   >例如：`//assets.adobetm.com/launch-xxxx`。

   您的 **[!UICONTROL 暂存]** 页面可能与以下内容类似。 的 **[!UICONTROL 存档]** 和 **[!UICONTROL 异步加载库]** 选项 ***not*** 设置：

   ![image2019-7-15_15-21-8](assets/image2019-7-15_15-21-8.png)

1. 在右上角附近，选择 **[!UICONTROL 下一个]**.
1. 在 **[!UICONTROL 生产]** 第（3/3页）页 **[!UICONTROL 创建Experience Platform标记配置]** 窗口，如果需要，请修复自动填充的生产URI，类似于在上一页中的操作 **[!UICONTROL 暂存]** 页面。
1. 在右上角附近，选择 **[!UICONTROL 创建]**.

   您的新Experience Platform标记云配置现已创建并列在您网站的旁边。

1. 选择您的新Experience Platform标记云配置（选择配置标题后，其左侧会显示一个复选标记）。 在工具栏中，选择 **[!UICONTROL 发布]**.

   ![image2019-7-15_15-47-6](assets/image2019-7-15_15-47-6.png)

目前，Experience Manager作者不支持将Dynamic Media查看器与Experience Platform标记集成。

但是，Experience Manager发布节点支持此功能。 使用“Experience Platform标签云配置”的默认设置，Experience Manager发布使用“Experience Platform标签”的生产环境。 因此，在测试期间，每次必须将Experience Platform标记库更新从开发推送到生产环境。

可以绕过此限制。 在上面用于Experience Platform发布的Experience Platform标记云配置中，指定Experience Manager标记库的开发或暂存URL。 这样做会使Experience Manager发布节点使用Experience Platform标记库的开发或暂存版本。

请参阅 [集成Experience Platform标记和Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/overview.html#integrations) 有关设置Experience Platform标记云配置的更多信息。
