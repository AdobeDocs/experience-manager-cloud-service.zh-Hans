---
title: 将 Dynamic Media 查看器与 Analytics 和 Adobe Experience Platform 标记集成
description: 了解适用于Experience Platform标记和Dynamic Media Viewers 5.13的Dynamic Media Viewers扩展。它允许Adobe Analytics和Platform Tags的客户在其Experience Platform标记配置中使用特定于Dynamic Media Viewers的事件和数据。
contentOwner: Rick Brough
feature: Asset Reports
role: Admin,User
exl-id: a71fef45-c9a4-4091-8af1-c3c173324b7a
source-git-commit: a01583483fa89f89b60277c2ce4e1c440590e96c
workflow-type: tm+mt
source-wordcount: '6665'
ht-degree: 7%

---

# 将 Dynamic Media 查看器与 Analytics 和 Adobe Experience Platform 标记集成 {#integrating-dynamic-media-viewers-with-adobe-analytics-and-adobe-launch}

## Dynamic Media Viewers与Adobe Analytics和Experience Platform标记有何集成？ {#what-is-dynamic-media-viewers-integration-with-adobe-analytics-and-adobe-launch}

<!-- Leave this hidden path here; it points to the topic source from Sasha https://wiki.corp.adobe.com/pages/viewpage.action?spaceKey=~oufimtse&title=Dynamic+Media+Viewers+integration+with+Adobe+Launch 

name used to be Experience Platform Launch. Changed to Experience Platform Data Collection-->

*Dynamic Media查看器* 通过Experience Platform Tags和Dynamic Media Viewers 5.13的扩展，Adobe Analytics和Experience Platform Tags客户可在其Experience PlatformTags配置中使用特定于Dynamic Media Viewers的事件和数据。

此集成意味着您可以使用Adobe Analytics跟踪网站上Dynamic Media查看器使用情况。 同时，您可以将查看器公开的事件和数据与来自Adobe或第三方的任何其他Experience Platform标记扩展结合使用。

要了解有关Adobe扩展或第三方扩展的更多信息，请参阅 [Adobe扩展](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/overview.html) 《Experience Platform标签用户指南》中的。

**本主题适用于以下内容：** Adobe Experience Manager项目的站点管理员、开发人员和运营人员。

### 集成的限制 {#limitations-of-the-integration}

* Dynamic Media查看器的Experience Platform标记集成在Experience Manager创作节点中不起作用。 在WCM页面发布之前，您无法从中看到任何跟踪。
* “弹出窗口”操作模式不支持Dynamic Media查看器的Experience Platform标记集成，在该模式下，查看器的URL是使用“资源详细信息”页面上的“URL”按钮获得的。
* Experience Platform标记集成不能与旧版查看器Analytics集成同时使用(通过 `config2=` 参数)。
* 对视频跟踪的支持仅限于核心播放跟踪，如中所述 [跟踪概述](https://experienceleague.adobe.com/docs/media-analytics/using/tracking/track-av-playback/track-core-overview.html?lang=en#player-events). 特别是，不支持QoS、广告、章节/区段或错误跟踪。
* 使用的数据元素不支持数据元素的存储持续时间配置。 *Dynamic Media查看器* 扩展。 存储持续时间必须设置为 **[!UICONTROL 无]**.

### 集成的用例 {#use-cases-for-the-integration}

与Experience Platform标记集成的主要用例是同时使用Experience Manager Assets和Experience Manager Sites的客户。 在此类场景中，您可以设置Experience Manager创作节点和Experience Platform标记之间的标准集成，然后将站点实例与Experience Platform标记属性关联。 之后，添加到Sites页面的任何Dynamic Media WCM组件都将跟踪来自查看者的数据和事件。

参见 [在Experience Manager Sites中跟踪Dynamic Media查看器](#tracking-dynamic-media-viewers-in-aem-sites).

集成支持的辅助用例是仅使用Experience Manager Assets或Dynamic Media Classic的客户。 在这种情况下，您需要获取查看器的嵌入代码，并将其添加到网站页面。 然后，从Experience Platform标签中获取Experience Platform标签库的生产URL，并将其手动添加到网页代码中。

参见 [使用嵌入代码跟踪Dynamic Media查看器](#tracking-dynamic-media-viewers-using-embed-code).

## 数据和事件跟踪在集成中的工作原理 {#how-data-and-event-tracking-works-in-the-integration}

该集成利用了两种独立的Dynamic Media查看器跟踪类型： *Adobe Analytics* 和 *适用于音频和视频的Adobe Analytics*.

### 关于使用Adobe Analytics进行跟踪  {#about-tracking-using-adobe-analytics}

通过Adobe Analytics，您可以跟踪最终用户在您的网站上与Dynamic Media查看器交互时执行的操作。 Adobe Analytics还允许您跟踪特定于查看器的数据。 例如，您可以跟踪和记录视图加载事件以及资源名称、发生的任何缩放操作和视频播放操作。

在Experience Platform标签中， *数据元素* 和 *规则* 共同启用Adobe Analytics跟踪。

#### 关于Experience Platform标记中的数据元素 {#about-data-elements-in-adobe-launch}

Experience Platform标记中的数据元素是一个命名属性，其值是静态定义的，或根据网页或Dynamic Media查看器数据的状态进行动态计算。

数据元素定义中可用的选项取决于Experience Platform标记属性中安装的扩展列表。 “核心”扩展已预安装，可在任何配置中开箱即用。 此“核心”扩展允许定义数据元素，其值来自Cookie、JavaScript代码、查询字符串和许多其他源。

对于Adobe Analytics跟踪，必须安装其他多个扩展，如中所述 [扩展的安装和设置](#installing-and-setup-of-extensions). Dynamic Media Viewers扩展添加了定义数据元素的功能，该数据元素的值是动态查看器事件的参数。 例如，可以引用查看器类型或查看器加载时报告的资产名称、最终用户缩放时报告的缩放级别等。

Dynamic Media Viewer扩展会自动使其数据元素的值保持最新。

定义数据元素后，可以使用数据元素选取器小组件，将数据元素用于Experience Platform标记UI的其他位置。 特别是，为Dynamic Media查看器跟踪而定义的数据元素由规则中Adobe Analytics扩展的Set Variables操作引用（请参阅下文）。

参见 [数据元素](https://experienceleague.adobe.com/docs/experience-platform/tags/ui/data-elements.html) 《Experience Platform标签用户指南》中的。

#### 关于Experience Platform标记中的规则 {#about-rules-in-adobe-launch}

Experience Platform标记中的规则是一种不可知配置，它定义了构成规则的三个区域： *事件*， *条件*、和 *操作*：

* *事件* (if)告知Experience Platform标签何时触发Rule。
* *条件* （如果）在触发Experience Platform时，告知规则标记还应该允许或禁止哪些其他限制。
* *操作* (then)告知Experience Platform标签在触发规则时执行的操作。

Events、Conditions和Actions部分中可用的选项取决于Experience Platform标记资产中安装的扩展。 此 *核心* 扩展已预安装，并且在任何配置中均可开箱即用。 扩展为事件提供了多个选项，例如基本的浏览器级别操作，包括焦点更改、按键和表单提交。 它还包含适用于条件的选项，例如Cookie值、浏览器类型等。 对于“操作”，只有“自定义代码”选项可用。

对于Adobe Analytics跟踪，必须安装其他多个扩展，如中所述 [扩展的安装和设置](#installing-and-setup-of-extensions). 具体来说：

* Dynamic Media Viewers扩展将受支持的事件列表扩展到Dynamic Media查看器特定的事件，例如查看器加载、资源交换、放大和视频播放。
* Adobe Analytics扩展扩展了支持的操作列表，添加了向跟踪服务器发送数据所需的两个操作： *设置变量* 和 *发送信标*.

要跟踪Dynamic Media查看器，可以使用以下任何类型：

* 来自Dynamic Media Viewers扩展、核心扩展或任何其他扩展的事件。
* 规则定义中的条件。 或者，您可以将conditions区域留空。

在操作部分，您需要拥有 *设置变量* 操作。 此操作可告知Adobe Analytics如何使用数据填充跟踪变量。 同时， *设置变量* 操作不会将任何内容发送到跟踪服务器。

此 *设置变量* 操作后必须跟有 *发送信标* 操作。 此 *发送信标* 操作实际上会将数据发送到analytics跟踪服务器。 这两个操作， *设置变量* 和 *发送信标*，来自Adobe Analytics扩展。

参见 [规则](https://experienceleague.adobe.com/docs/experience-platform/tags/ui/rules.html) 《Experience Platform标签用户指南》中的。

#### 示例配置 {#sample-configuration}

Experience Platform标记中的以下示例配置演示了如何在加载查看器时跟踪资源名称。

1. 从 **[!UICONTROL 数据元素]** 选项卡，定义数据元素 `AssetName` 引用 `asset` 的参数 `LOAD` Dynamic Media查看器扩展中的事件。

   ![image2019-11](assets/image2019-11.png)

1. 从 **[!UICONTROL 规则]** 选项卡，定义规则 *TrackAssetOnLoad*.

   在此规则中， **[!UICONTROL 事件]** 字段使用 **[!UICONTROL 加载]** Dynamic Media查看器扩展中的事件。

   ![image2019-22](assets/image2019-22.png)

1. “操作”配置具有Adobe Analytics扩展中的两种操作类型：

   *设置变量*，将您选择的analytics变量映射到的 `AssetName` 数据元素。

   *发送信标*，会将跟踪信息发送到Adobe Analytics。

   ![image2019-3](assets/image2019-3.png)

1. 生成的规则配置如下所示：

   ![image2019-4](assets/image2019-4.png)

### 关于Adobe Analytics for Audio and Video {#about-adobe-analytics-for-audio-and-video}

当订阅Experience Cloud帐户以使用Adobe Analytics for Audio and Video时，即足以在中启用视频跟踪 *Dynamic Media查看器* 扩展设置。 视频量度在Adobe Analytics中可用。 视频跟踪取决于Adobe Medium Analytics for Audio and Video扩展的存在。

参见 [扩展的安装和设置](#installing-and-setup-of-extensions).

目前，对视频跟踪的支持仅限于“核心播放”跟踪，如中所述 [跟踪概述](https://experienceleague.adobe.com/docs/media-analytics/using/tracking/track-av-playback/track-core-overview.html?lang=en#player-events). 特别是，不支持QoS、广告、章节/区段或错误跟踪。

## 使用Dynamic Media查看器扩展 {#using-the-dynamic-media-viewers-extension}

如中所述 [集成的用例](#use-cases-for-the-integration)，即可通过Experience Manager Sites中的新Experience Platform标记集成以及使用嵌入代码来跟踪Dynamic Media查看器。

### 在Experience Manager Sites中跟踪Dynamic Media查看器 {#tracking-dynamic-media-viewers-in-aem-sites}

要在Experience Manager Sites中跟踪Dynamic Media查看器，请在 [配置所有集成片段](#configuring-all-the-integration-pieces) 必须执行section。 具体而言，您必须创建IMS配置和Experience PlatformTags Cloud配置。

在正确配置后，您使用Dynamic Media支持的WCM组件添加到站点页面的任何Dynamic Media查看器都会自动跟踪数据到Adobe Analytics或Adobe Analytics for Video，或者跟踪两者。

参见 [使用Adobe站点将Dynamic Media资产添加到页面](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md).

### 使用嵌入代码跟踪Dynamic Media查看器 {#tracking-dynamic-media-viewers-using-embed-code}

对于未使用Experience Manager Sites或（或）将Dynamic Media查看器嵌入到Experience Manager Sites外部的网页中的客户，仍可以使用Experience Platform标记集成。

完成配置步骤，从 [配置Adobe Analytics](#configuring-adobe-analytics-for-the-integration) 和 [配置Experience Platform标记](#configuring-adobe-launch-for-the-integration) 部分。 但是，不需要执行与Experience Manager相关的配置步骤。

在正确配置后，您可以使用Dynamic Media查看器将Experience Platform标记支持添加到网页。

参见 [添加Experience Platform标记嵌入代码](https://experienceleague.adobe.com/docs/platform-learn/implement-in-websites/configure-tags/add-embed-code.html) 详细了解如何使用Experience Platform标签库嵌入代码。

要详细了解如何使用Experience ManagerDynamic Media的嵌入代码功能，请参阅 [在网页上嵌入视频查看器或图像查看器](/help/assets/dynamic-media/embed-code.md).

**使用嵌入代码跟踪Dynamic Media查看器：**

1. 设置一个网页以便嵌入Dynamic Media查看器。
1. 通过首次登录“Experience Platform标签”获取“Experience Platform标签”库的嵌入代码(请参阅 [配置Experience Platform标记](#configuring-adobe-launch-for-the-integration))。
1. 选择 **[!UICONTROL 属性]**，然后选择 **[!UICONTROL 环境]** 选项卡。
1. 选取与网页环境相关的环境级别。 然后，在 **[!UICONTROL 安装]** 列中，选择框图标。
1. **[!UICONTROL 在Web安装说明中]** 对话框中，复制完整的Experience PlatformTags库嵌入代码以及周围的 `<script/>` 标记之间。

## Dynamic Media Viewers扩展参考指南 {#reference-guide-for-the-dynamic-media-viewers-extension}

### 关于Dynamic Media查看器配置 {#about-the-dynamic-media-viewers-configuration}

如果满足以下条件，则Dynamic Media Viewer扩展会自动与Experience Platform标记库集成：

* Experience Platform标签库全局对象( `_satellite`)显示在页面上。
* Dynamic Media查看器扩展函数 `_dmviewers_v001()` 定义于 `_satellite`.

* `config2=` 未指定查看器参数，这意味着查看器不使用旧版Analytics集成。

此外，还有一个选项，即指定以下内容以在查看器中明确禁用Experience Platform标记集成 `launch=0` 查看者配置中的参数。 此参数的默认值为 `1`.

### 配置Dynamic Media查看器扩展 {#configuring-the-dynamic-media-viewers-extension}

Dynamic Media Viewers扩展的唯一配置选项是 **[!UICONTROL 为音频和视频启用Adobe Medium Analytics]**.

如果选中（启用）此选项，并且安装并配置了Adobe Medium Analytics for Audio and Video扩展，则会将视频播放量度发送到Adobe Analytics for Audio and Video解决方案。 禁用此选项将关闭视频跟踪。

如果启用此选项 *不含* 如果安装了Adobe Medium Analytics for Audio and Video扩展，则选项无效。

![image2019-7-22_12-4-23](assets/image2019-7-22_12-4-23.png)

### 关于Dynamic Media查看器扩展中的数据元素 {#about-data-elements-in-the-dynamic-media-viewers-extension}

Dynamic Media Viewers 扩展提供的唯一数据元素类型是&#x200B;**[!UICONTROL 数据元素类型]**&#x200B;下拉列表中的&#x200B;**[!UICONTROL 查看器事件]**。

选中后，数据元素编辑器将渲染包含两个字段的表单：

* **[!UICONTROL DM 查看器事件数据类型]** - 一个下拉列表，标识了 Dynamic Media 查看器扩展支持的所有查看器事件（具有参数）以及特殊的 **[!UICONTROL COMMON]** 项目。**[!UICONTROL COMMON]** 项目表示事件参数列表，这些事件参数对查看器发送的所有类型事件都是通用的。
* **[!UICONTROL 跟踪参数]**  — 选定Dynamic Media查看器事件的参数。

![image2019-7-22_12-5-46](assets/image2019-7-22_12-5-46.png)

请参阅 [Dynamic Media查看器参考指南](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/c-html5-s7-aem-asset-viewers.html) 有关每种查看器类型支持的事件列表；请转到特定的查看器部分，然后选择支持Adobe Analytics跟踪子部分。 目前，《Dynamic Media查看器参考指南》未记录事件参数。

现在，让我们考虑Dynamic Media查看器的生命周期 *数据元素*. 此类数据元素的值会在页面上发生相应的Dynamic Media查看器事件后填充。 例如，假设数据元素指向 **[!UICONTROL 加载]** 事件及其“asset”参数。 在查看器首次运行LOAD事件后，此数据元素的值会收到有效数据。 如果数据元素指向 **[!UICONTROL 缩放]** 事件及其“缩放”参数时，此类“数据元素”的值将保持为空，直到查看器发送 **[!UICONTROL 缩放]** 第一次发生事件了。

同样，当查看器在页面上发送相应事件时，数据元素的值也会自动更新。即使在规则配置中未指定特定事件，也会发生值更新。例如，假设数据元素 **[!UICONTROL 缩放比例]** 为ZOOM事件的“缩放”参数定义。 但是，规则配置中唯一存在的规则是由触发的 **[!UICONTROL 加载]** 事件。 的值 **[!UICONTROL 缩放比例]** 每次用户在查看器中运行缩放时仍会更新。

任何Dynamic media查看器在网页上都有唯一标识符。 数据元素会跟踪值本身，以及填充该值的查看器。 例如，假设同一页面上有多个查看器，并且 **[!UICONTROL 资产名称]** 指向 **[!UICONTROL 加载]** 事件及其“asset”参数。 此 **[!UICONTROL 资产名称]** 数据元素会维护与页面上加载的每个查看器关联的资产名称集合。

数据元素返回的确切值取决于上下文。 如果在由Dynamic Media查看器事件触发的规则中请求数据元素，则会为启动该规则的查看器返回数据元素值。 此外，数据元素是在某个规则中请求的，该规则由某个其他Experience Platform标记扩展中的事件触发。 此时，数据元素的值来自上次更新此数据元素的查看器。

**请考虑以下示例设置：**

* 具有两个Dynamic Media缩放查看器的网页： *查看器1* 和 *查看器2*.

* **[!UICONTROL 缩放比例]** 数据元素指向 **[!UICONTROL 缩放]** 事件及其“规模”参数。
* **[!UICONTROL Trackpan]** 具有以下特征的规则：

   * 使用Dynamic Media查看器 **[!UICONTROL 平移]** 事件作为触发器。
   * 发送值 **[!UICONTROL 缩放比例]** 将数据元素添加到Adobe Analytics。

* **[!UICONTROL TrackKey]** 具有以下特征的规则：

   * 使用核心Experience Platform标记扩展中的按键事件作为触发器。
   * 发送值 **[!UICONTROL 缩放比例]** 将数据元素添加到Adobe Analytics。

现在，假定最终用户加载网页时带有两个查看器。 In *查看器1*，则将缩放比例放大到50%；然后，放大 *查看器2*，则将缩放比例放大到25%。 In *查看器1*，他们四处平移图像，最后按键盘上的键。

最终用户的活动会导致向Adobe Analytics发出以下两个跟踪调用：

* 第一次调用是因为 **[!UICONTROL Trackpan]** 当用户进入时触发规则 *查看器1*. 该调用发送50%作为值 **[!UICONTROL 缩放比例]** 数据元素，因为数据元素知道规则触发自 *查看器1* 并提取相应的比例值；
* 第二次调用是因为 **[!UICONTROL TrackKey]** 用户按下键盘上的键时会触发规则。 该调用发送25%作为值 **[!UICONTROL 缩放比例]** 数据元素，因为规则不是由查看器触发的。 因此，数据元素会返回最新的值。

以上设置的示例也会影响数据元素值的生命周期。 Dynamic Media查看器管理的数据元素的值存储在Experience Platform标记库代码中，即使查看器本身已放置在网页上也是如此。 这项功能意味着，如果存在由非Dynamic Media Viewer扩展触发的规则，并且引用了此类数据元素，则数据元素将返回最后一个已知值。 即使查看者不再出现在网页上。

无论如何，由Dynamic Media Viewers驱动的数据元素值不会存储在本地存储或服务器上；而是仅保留在客户端Experience Platform标签库中。 当网页重新加载时，此类数据元素的值消失。

通常，数据元素编辑器支持 [存储持续时间选择](https://experienceleague.adobe.com/docs/experience-platform/tags/ui/data-elements.html#create-a-data-element). 但是，使用Dynamic Media Viewers扩展的数据元素仅支持存储持续时间选项 **[!UICONTROL 无]**. 可以在用户界面中设置任何其他值，但此时未定义数据元素行为。 扩展可自行管理数据元素的值：在整个查看器生命周期中维护查看器事件参数值的数据元素。

### 关于Dynamic Media查看器扩展中的规则 {#about-rules-in-the-dynamic-media-viewers-extension}

在规则编辑器中，扩展会为事件编辑器添加新的配置选项。 此外，该编辑器还提供了一个选项，让您可以在操作编辑器中手动引用事件参数作为短手选项，而不是使用预配置的数据元素。

#### 关于事件编辑器 {#about-the-events-editor}

在事件编辑器中， Dynamic Media Viewers扩展将添加 **[!UICONTROL 事件类型]** 已调用 **[!UICONTROL 查看器事件]**.

选中后，事件编辑器将呈现下拉列表 **[!UICONTROL Dynamic Media Viewer事件]**，列出Dynamic Media查看器支持的所有可用事件。

![image2019-8-2_15-13-1](assets/image2019-8-2_15-13-1.png)

#### 关于操作编辑器 {#about-the-actions-editor}

通过Dynamic Media查看器扩展，您可以使用Dynamic Media查看器的事件参数来映射到Adobe Analytics扩展的“设置变量”编辑器中的Analytics变量。

最简单的方法是完成以下两步过程：

* 首先，定义一个或多个数据元素，其中每个数据元素表示Dynamic Media Viewer事件的参数。
* 最后，在Adobe Analytics扩展的“设置变量”编辑器中，选择“数据元素”选取器图标（三个栈叠的磁盘）以打开“选择数据元素”对话框，然后从中选择一个数据元素。

![image2019-7-10_20-41-52](assets/image2019-7-10_20-41-52.png)

但是，可以使用替代方法并绕过数据元素创建。您可以直接引用Dynamic Media Viewer事件中的参数。 在中输入事件参数的完全限定名称 **[!UICONTROL 值]** Analytics变量分配的输入字段。 请务必用百分号(%)括起来。 例如，

`%event.detail.dm.LOAD.asset%`

![image2019-7-12_19-2-35](assets/image2019-7-12_19-2-35.png)

使用数据元素与直接事件参数引用之间有一个重要的区别。 对于数据元素，哪个事件触发Set Variables操作并不重要。 触发规则的事件可能与动态查看器无关（例如从核心扩展中选择网页）。 但是，在使用直接参数引用时，请务必确保触发规则的事件对应于它引用的事件参数。

例如，如果规 `%event.detail.dm.LOAD.asset%` 则是由Dynamic Media Viewer扩展的 **[!UICONTROL LOAD]** 事件触发的，则引用将返回正确的资产名称。 但是，对于任何其他事件，它都会返回一个空值。

下表列出了Dynamic Media Viewer事件及其支持的参数：

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
   <td><code>BANNER</code><br /> </td>
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

## 配置所有集成片段 {#configuring-all-the-integration-pieces}

**开始之前**

Adobe建议您仔细阅读本节之前的所有文档，以便了解整个集成。

此部分介绍了将Dynamic Media查看器与Adobe Analytics和用于音频和视频的Adobe Analytics集成所需的配置步骤。 虽然可以将Dynamic Media查看器扩展用于Experience Platform标记中的其他目的，但本文档未介绍此类场景。

您即将使用以下Adobe产品配置集成：

* Adobe Analytics — 用于配置跟踪变量和报表。
* Experience Platform标记 — 用于定义资产、一个或多个规则以及一个或多个数据元素，以启用查看器跟踪。

此外，如果此集成解决方案与Experience Manager Sites一起使用，则必须完成以下配置：

* [Adobe Developer控制台](https://developer.adobe.com/console/home)  — 为Experience Platform标记创建集成。
* Experience Manager创作节点 — IMS配置和Experience Platform标记云配置。

在配置过程中，确保您有权访问Adobe Experience Cloud中一家已启用Adobe Analytics和Experience Platform标签的公司。

## 配置Adobe Analytics以进行集成 {#configuring-adobe-analytics-for-the-integration}

配置Adobe Analytics后，将为该集成设置以下内容：

* 已放置并选择一个报表包。
* Analytics变量可用于接收跟踪数据。
* 报表可用于查看Adobe Analytics中收集的数据。

另请参阅 [Analytics实施指南](https://experienceleague.adobe.com/docs/analytics/implementation/home.html).

**要配置Adobe Analytics以进行集成，请执行以下操作：**

1. 首先从Experience Cloud访问Adobe Analytics [主页](https://experience.adobe.com/#/home). 在菜单栏上，选择页面右上角附近的解决方案图标（一个三乘三的圆点表），然后选择 **[!UICONTROL 分析]**.

   ![2019-07-22_18-08-47](assets/2019-07-22_18-08-47.png)

   现在，选择一个报表包。

### 选择报表包 {#selecting-a-report-suite}

1. 在 Adobe Analytics 页面的右上角附近，在&#x200B;**[!UICONTROL 搜索报告]**&#x200B;字段的右侧，从下拉列表中选择正确的报表包。如果有多个可用报表包，并且您不确定要使用哪个报表包，请与 Adobe Analytics 管理员联系，帮助您选择要使用的报表包。

   在以下示例中，用户创建了一个名为的报表包 *DynamicMediaViewersExtensionDoc* 并从下拉列表中选择它。 报表包名称只是一个示例。 您最终选择的报表包的名称由您决定。

   如果没有可用的报表包，则您必须或您的Adobe Analytics管理员创建一个报表包，然后才能继续配置。

   参见 [报表和报表包](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/manage-report-suites/report-suites-admin.html) 和 [创建报表包](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/manage-report-suites/c-new-report-suite/t-create-a-report-suite.html).

   在Adobe Analytics中，报表包位于下方 **[!UICONTROL 管理员]** > **[!UICONTROL 报表包]**.

   ![2019-07-22_18-09-49](assets/2019-07-22_18-09-49.png)

   现在设置Adobe Analytics变量。

### 设置Adobe Analytics变量 {#setting-up-adobe-analytics-variables}

1. 指定一个或多个要用于跟踪Dynamic Media查看器行为的Adobe Analytics变量。

   可以使用Adobe Analytics支持的任何类型的变量。 关于变量类型的决策（如自定义流量） [prop]，转化 [eVar])由Analytics实施的特定需求驱动。

   参见 [prop和eVar概述](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar.html#vars).

   对于此文档，仅使用自定义流量(prop)变量，因为它们在Analytics报表中在网页上发生操作后几分钟内变为可用。

   要启用新的自定义流量变量，请在Adobe Analytics的工具栏上，转到 **[!UICONTROL 管理员]** > **[!UICONTROL 报表包]**.

1. 在 **[!UICONTROL 报表包管理器]** 页面上，选择正确的报表，然后在工具栏上，转到 **[!UICONTROL 编辑设置]** > **[!UICONTROL 流量]** > **[!UICONTROL 流量变量]**.
1. 选取一个未使用的变量，为其指定一个描述性名称( **[!UICONTROL 查看器资产(prop 30)]**)，然后在“已启用”列中将组合框更改为“已启用”。

   以下屏幕截图是自定义流量变量( **[!UICONTROL prop30]**)，以跟踪查看器使用的资源名称：

   ![image2019-6-26_23-6-59](/help/assets/dynamic-media/assets/image2019-6-26_23-6-59.png)

1. 在变量列表的底部，选择 **[!UICONTROL 保存]**.

### 设置报告 {#setting-up-a-report}

1. 通常，在Adobe Analytics中设置报表是由特定项目需求驱动的。 因此，详细报表设置超出了此集成的范围。

   但是，在中设置自定义流量变量后，只需了解自定义流量报表即可在Adobe Analytics中自动可用 **[设置Adobe Analytics变量](#setting-up-adobe-analytics-variables)**.

   例如，报告 **[!UICONTROL 查看器资产(prop 30)]** 变量可从“报表”菜单的 **[!UICONTROL 自定义流量]** > **[!UICONTROL 自定义流量21 - 30]** > **[!UICONTROL 查看器资产(prop 30)]**.

   在查看器资产(prop 30)创 **[!UICONTROL 建后直接访问此报告]** ，不显示任何数据；在整合的这一阶段，人们就会期待它。

   ![image2019-6-26_23-12-49](/help/assets/dynamic-media/assets/image2019-6-26_23-12-49.png)

## 为集成配置Experience Platform标记 {#configuring-adobe-launch-for-the-integration}

配置Experience Platform标记后，将为该集成设置以下内容：

* 创建一个新资产，将所有配置放在一起。
* 扩展的安装和设置。 资产中安装的所有扩展的客户端代码将一起编译到一个库中。 此库稍后供网页使用。
* 数据元素和规则的配置。 此配置定义要从Dynamic Media查看器获取哪些数据，何时触发跟踪逻辑，以及在Adobe Analytics中将查看器数据发送到何处。
* 库发布。

**要为集成配置Experience Platform标记，请执行以下操作：**

1. 首先从Experience Cloud访问Experience Platform标签 [主页](https://experience.adobe.com/#/home). 在菜单栏上，选择页面右上角附近的解决方案图标（三乘三点表），然后选择 **[!UICONTROL 标记]**.

   您还可以 [直接打开Experience Platform标签](https://launch.adobe.com/).

   ![image2019-7-8_15-38-44](assets/image2019-7-8_15-38-44.png)

### 在Experience Platform标签中创建资产 {#creating-a-property-in-adobe-launch}

Experience Platform标记中的资产是一个命名配置，可将所有设置保留在一起。 将生成配置设置库，并将其发布到不同的环境级别（开发、暂存和生产）。

另请参阅 [配置Tap属性](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/initial-configuration/configure-tags.html).

**要在“Experience Platform标签”中创建资产，请执行以下操作：**

1. 在Experience Platform标记中，选择 **[!UICONTROL 新建属性]**.
1. 在&#x200B;**[!UICONTROL 创建属性]**&#x200B;对话框的&#x200B;**[!UICONTROL 名称]**&#x200B;字段中，键入描述性名称，如网站的标题。例如，`DynamicMediaViewersProp.`
1. 在 **[!UICONTROL 域]** 字段中，输入您网站的域。
1. 在&#x200B;**[!UICONTROL 高级选项]**&#x200B;下拉框中，启用&#x200B;**[!UICONTROL 配置以进行扩展开发（以后无法修改）]**，以防您要使用的扩展（本例中为 *Dynamic Media 查看器*）尚未发布。

   ![image2019-7-8_16-3-47](assets/image2019-7-8_16-3-47.png)

1. 选择&#x200B;**[!UICONTROL 保存]**。

   选择新创建的资产，然后继续执行 *扩展的安装和设置*.

### 安装和设置扩展 {#installing-and-setup-of-extensions}

Experience Platform标记中的所有可用扩展都列在 **[!UICONTROL 扩展]** > **[!UICONTROL 目录]**.

要安装扩展，请选择 **[!UICONTROL 安装]**. 如果需要，请执行一次性扩展配置，然后选择 **[!UICONTROL 保存]**.

在需要时，必须安装和配置以下扩展：

* （必需） *Experience CloudID服务* 扩展

无需其他配置，接受任何建议值。 完成后，请确保选择 **[!UICONTROL 保存]**.

参见 [Experience CloudIdentity Service扩展](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/id-service/overview.html).

* （必需） *Adobe Analytics* 扩展

要配置此扩展，您需要在Adobe Analytics中位于下的报表包ID **[!UICONTROL 管理员]** > **[!UICONTROL 报表包]**，位于 **[!UICONTROL 报表包ID]** 列标题。

(仅供演示之用，的报表包ID **[!UICONTROL DynamicMediaViewersExtensionDoc]** 在以下屏幕截图中使用报表包。 此 ID 在之前的[选择报表包](#selecting-a-report-suite)中创建并使用。)

![image2019-7-8_16-45-34](assets/image2019-7-8_16-45-34.png)

在“安装扩展”页面的&#x200B;**[!UICONTROL 开发报表包]**&#x200B;字段、**[!UICONTROL 测试报表包]**&#x200B;字段和&#x200B;**[!UICONTROL 生产报表包]**&#x200B;字段中输入报表包 ID。

![image2019-7-8_16-47-40](assets/image2019-7-8_16-47-40.png)

*仅当您打算使用视频跟踪时，才配置以下项目：*

在 **[!UICONTROL 安装扩展]** 页面，展开 **[!UICONTROL 常规]**，然后指定跟踪服务器。 跟踪服务器遵循模板 `<trackingNamespace>.sc.omtrdc.net`，其中 `<trackingNamespace>` 是在配置电子邮件中获取的信息。

选择&#x200B;**[!UICONTROL 保存]**。

参见 [Adobe Analytics扩展](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/analytics/overview.html).

* (可选. 仅在需要视频跟踪时才需要) *Adobe Medium Analytics for Audio and Video* 扩展

填写跟踪服务器字段。 的跟踪服务器 *Adobe Medium Analytics for Audio and Video* 扩展不同于用于Adobe Analytics的跟踪服务器。 它会遵循模板 `<trackingNamespace>.hb.omtrdc.net`，其中 `<trackingNamespace>` 是预配电子邮件中的信息。

所有其他字段都是可选的。

参见 [Adobe Medium Analytics for Audio and Video扩展](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/media-analytics/overview.html).

* （必需） *Dynamic Media查看器* 扩展

选择&#x200B;**[!UICONTROL 启用 Adobe Analytics for Video]** 以启用（打开）视频检测信号跟踪。

截至本文撰稿时， *Dynamic Media查看器* 仅当为开发创建Experience Platform标记属性时，扩展才可用。

参见 [在Experience Platform标签中创建资产](#creating-a-property-in-adobe-launch).

安装并设置扩展后，Extensions > Installed区域中至少会列出以下五个扩展（如果不跟踪视频，则四个）。

![image2019-7-22_12-7-36](assets/image2019-7-22_12-7-36.png)

### 设置数据元素和规则 {#setting-up-data-elements-and-rules}

在Experience Platform标记中，创建跟踪Dynamic Media查看器所需的数据元素和规则。

参见 [数据和事件跟踪在集成中的工作原理](#how-data-and-event-tracking-works-in-the-integration) 有关使用Experience Platform标记进行跟踪的概述。

参见 [示例配置](#sample-configuration) Experience Platform标记中的示例配置，用于演示如何在查看器加载时跟踪资源名称。

参见 [配置Dynamic Media查看器扩展](#configuring-the-dynamic-media-viewers-extension) 以了解有关扩展功能的深入信息。

### 发布库 {#publishing-a-library}

要更改Experience Platform标记配置（包括属性、扩展、规则和数据元素设置），您必须 *发布* 这样的变化。 在Experience Platform标记中发布是从Property配置下的Publishing选项卡执行的。

Experience Platform标记可能具有多个开发环境、一个暂存环境和一个生产环境。 默认情况下，Experience Manager中的Experience Platform标签云配置将Experience Manager创作节点指向Platform Tags的暂存环境。 Experience Manager发布节点指向Experience Platform标记的生产环境。 这种安排意味着在默认Experience Manager设置下，有必要将Experience Platform标记库发布到暂存环境。 这样，您就可以在Experience Manager创作中使用它。 然后，您可以将其发布到生产环境中，以便在Experience Manager发布中使用。

参见 [环境](https://experienceleague.adobe.com/docs/experience-platform/tags/publish/environments/environments.html?lang=zh-Hans) 有关Experience Platform标签环境的更多信息。

发布库涉及以下两个步骤：

* 通过将所有必需的更改（新更改和更新）添加到库中来添加和构建新库。
* 在不同环境级别（从开发到暂存和生产）中向上移动库。

#### 添加和构建新库 {#adding-and-building-a-new-library}

1. 首次在Experience Platform标签中打开“发布”选项卡时，库列表为空。

   在左列中，选择 **[!UICONTROL 添加新库]**.

   ![image2019-7-15_14-43-17](assets/image2019-7-15_14-43-17.png)

1. 在“创建新库”页面上，使用 **[!UICONTROL 名称]** 字段中，输入新库的描述性名称。 例如，

   *DynamicMediaViewersLib*

   从“环境”下拉列表中，选择“环境”级别。 最初，仅开发级别可供选择。 在页面的左下角附近，选择 **[!UICONTROL 添加所有更改的资源]**.

   ![image2019-7-15_14-49-41](assets/image2019-7-15_14-49-41.png)

1. 在页面的右上角附近，选择 **[!UICONTROL 保存并构建用于开发]**.

   几分钟后，库即创建完毕，可供使用。

   ![image2019-7-15_15-3-34](assets/image2019-7-15_15-3-34.png)

   >[!NOTE]
   >
   >下次更改Experience Platform标签配置时，转到 **[!UICONTROL 发布]** 选项卡 **[!UICONTROL 属性]** 配置，然后选择您之前创建的库。
   >
   >
   >从库发布屏幕中，选择 **[!UICONTROL 添加所有更改的资源]**，然后选择 **[!UICONTROL 保存并构建用于开发]**.

#### 在环境级别中向上移动库 {#moving-a-library-up-through-environment-levels}

1. 添加新库后，即可在开发环境中找到它。 要将其移动到暂存环境级别（与“已提交”列相对应），请从库的下拉菜单中，选择 **[!UICONTROL 提交以供审批]**.

   ![image2019-7-15_15-52-37](assets/image2019-7-15_15-52-37.png)

1. 在确认对话框中，选择 **[!UICONTROL 提交]**.

   在库移至Submitted列后，从库的下拉菜单中选择 **[!UICONTROL 为暂存环境构建]**.

   ![image2019-7-15_15-54-37](assets/image2019-7-15_15-54-37.png)

1. 要将库从暂存环境移动到生产环境（即“已发布”列），请执行类似的过程。

   首先，从下拉菜单中选择 **[!UICONTROL 批准以发布]**.

   ![image2019-7-15_16-7-39](assets/image2019-7-15_16-7-39.png)

1. 从下拉菜单中，选择 **[!UICONTROL 构建并发布到生产环境]**.

   ![image2019-7-15_16-8-9](assets/image2019-7-15_16-8-9.png)

   参见 [发布](https://experienceleague.adobe.com/docs/experience-platform/tags/publish/overview.html) 有关Experience Platform标记中发布过程的详细信息。

## 配置Adobe Experience Manager以进行集成 {#configuring-adobe-experience-manager-for-the-integration}

<!-- Prerequisites list below should be verified by Sasha -->

前提条件:

* Experience Manager同时运行创作实例和发布实例。
* Experience Manager创作节点是在Dynamic Media中设置的。 <!-- Scene7 run mode (dynamicmedia_s7) -->
* Dynamic Media WCM组件已在Experience Manager Sites中启用。

Experience Manager配置包含以下两个主要步骤：

* Experience ManagerIMS的配置。
* Experience Platform标签云的配置。

### 配置Experience ManagerIMS {#configuring-aem-ims}

1. 在“Experience Manager创作”中，选择“工具”图标（锤子），然后转到 **[!UICONTROL 安全性]** > **[!UICONTROL Adobe IMS配置]**.

   ![2019-07-25_11-52-58](assets/2019-07-25_11-52-58.png)

1. 在“AdobeIMC配置”页面的左上角附近，选择 **[!UICONTROL 创建]**.
1. 在 **[!UICONTROL Adobe IMS技术帐户配置]** 页面，在 **[!UICONTROL 云解决方案]** 下拉列表，选择 **[!UICONTROL Experience Platform数据收集]**.
1. 启用 **[!UICONTROL 创建新证书]**，然后在文本字段中，为您的证书输入任何有意义的值。 例如， *AdobeLaunchIMSCert*. 选择 **[!UICONTROL 创建证书]**.

   将显示以下信息消息：

   *要检索有效的访问令牌，必须将新证书的公共密钥添加到Adobe Developer上的技术帐户中！*

   要关闭“信息”对话框，请选择 **[!UICONTROL 确定]**.

   ![2019-07-25_12-09-24](assets/2019-07-25_12-09-24.png)

1. 选择 **[!UICONTROL 下载公钥]** 要下载公钥文件(`*.crt`)。

   >[!NOTE]
   >
   >此时， ***保持打开*** 此 **[!UICONTROL Adobe IMS技术帐户配置]** 页面； ***不要*** 关闭页面并 ***不要*** 选择 **[!UICONTROL 下一个]**. 您稍后将在步骤中返回此页面。

   ![2019-07-25_12-52-24](assets/2019-07-25_12-52-24.png)

1. 在新的浏览器选项卡中，导航到 [Adobe Developer控制台](https://developer.adobe.com/console/integrations).

1. 从 **[!UICONTROL Adobe I/O控制台集成]** 页面，右上角附近，选择 **[!UICONTROL 新集成]**.
1. 在 **[!UICONTROL 创建新集成]** 对话框，请确保 **[!UICONTROL 访问API]** 单选按钮处于选中状态，然后选择 **[!UICONTROL 继续]**.

![2019-07-25_13-04-20](assets/2019-07-25_13-04-20.png)

1. 第二个 **[!UICONTROL 创建新集成]** 页面，启用（打开） **[!UICONTROL Experience Platform标记API]** 单选按钮。 在页面的右下角，选择 **[!UICONTROL 继续]**.

   ![2019-07-25_13-13-54](assets/2019-07-25_13-13-54.png)

1. 在第三个 **[!UICONTROL 创建新集成]** 页面，请执行以下操作：

   * 在 **[!UICONTROL 名称]** 字段，输入描述性名称。 例如， *DynamicMediaViewersIO*.

   * 在 **[!UICONTROL 描述]** 字段中，输入集成的说明。

   * 在 **[!UICONTROL 公钥证书]** 区域，上传您的公钥文件(`*.crt`)之前，您在这些步骤中下载的。

   * 在 **[!UICONTROL 为Experience Platform标记API选择角色]** 标题，选择 **[!UICONTROL 管理员]**.

   * 在 **[!UICONTROL 为Experience Platform标记API选择一个或多个产品配置文件]** 标题，选择名为的产品配置文件 **[!UICONTROL 标记 —  &lt;your_company_name>]**.

   ![2019-07-25_13-49-18](assets/2019-07-25_13-49-18.png)

1. 选择 **[!UICONTROL 创建集成]**.
1. 在 **[!UICONTROL 已创建集成]** 页面，选择 **[!UICONTROL 继续查看集成详细信息]**.

   ![2019-07-25_14-16-33](assets/2019-07-25_14-16-33.png)

1. 此时将显示集成详细信息页面，如下所示：

   >[!NOTE]
   >
   >***保持打开此集成详细信息页面***。您将需要 **[!UICONTROL 概述]** 和 **[!UICONTROL JWT]** 一会儿就跳卡。

   ![2019-07-25_14-35-30](assets/2019-07-25_14-35-30.png)
   *集成详细信息页面*

1. 返回之前打开的 **[!UICONTROL Adobe IMS 技术帐户配置]**&#x200B;页面。在页面的右上角，选择 **[!UICONTROL 下一个]** 以打开 **[!UICONTROL 帐户]** 中的页面 **[!UICONTROL Adobe IMS技术帐户配置]** 窗口。

   (如果您之前关闭了页面，请返回Experience Manager作者，然后转到 **[!UICONTROL 工具]** > **[!UICONTROL 安全性]** > **[!UICONTROL Adobe IMS配置]**. 选择&#x200B;**[!UICONTROL 创建]**。在 **[!UICONTROL 云解决方案]** 下拉列表，选择 **[!UICONTROL Experience Platform标记]**. 在&#x200B;**[!UICONTROL 证书]**&#x200B;下拉列表中，选择之前创建的证书的名称。

   ![2019-07-25_20-57-50](assets/2019-07-25_20-57-50.png)
   *Adobe IMS技术帐户配置 — 证书页面*

1. 此 **[!UICONTROL 帐户]** 页面包含五个字段，需要您使用上一步中集成详细信息页面中的信息填写。

   ![2019-07-25_20-42-45](assets/2019-07-25_20-42-45.png)
   *Adobe IMS技术帐户配置 — 帐户页面*

1. 在 **[!UICONTROL 帐户]** 页面中，填写以下字段：

   * **[!UICONTROL 标题]**  — 输入描述性帐户标题。
   * **[!UICONTROL 授权服务器]**  — 返回之前打开的集成详细信息页面。 选择 **[!UICONTROL JWT]** 选项卡。 复制服务器名称（不含路径），如下所示。

   返回到&#x200B;**[!UICONTROL 帐户]**&#x200B;页面，然后将名称粘贴到相应的字段中。例如， `https://ims-na1.adobelogin.com/`
（示例服务器名称仅用于解释）

   ![2019-07-25_15-01-53](assets/2019-07-25_15-01-53.png)
   *集成详细信息页面 — JWT选项卡*

1. **[!UICONTROL API 密钥]** - 返回到“集成详细信息”页面。选择 **[!UICONTROL 概述]** 选项卡，然后 **[!UICONTROL API密钥（客户端ID）]** 字段，选择 **[!UICONTROL 复制]**.

   返回到&#x200B;**[!UICONTROL 帐户]**&#x200B;页面，然后将密钥粘贴到相应的字段中。

   ![2019-07-25_14-35-333](assets/2019-07-25_14-35-333.png)
   *集成详细信息页面*

1. **[!UICONTROL 客户端密钥]** - 返回到“集成详细信息”页面。从 **[!UICONTROL 概述]** 选项卡，选择 **[!UICONTROL 检索客户端密码]**. 右侧 **[!UICONTROL 客户端密码]** 字段，选择 **[!UICONTROL 复制]**.

   返回到&#x200B;**[!UICONTROL 帐户]**&#x200B;页面，然后将密钥粘贴到相应的字段中。

1. **[!UICONTROL 有效负荷]**  — 返回集成详细信息页面。 从 **[!UICONTROL JWT]** 选项卡，在JWT有效负载字段中，复制整个JSON对象代码。

   返回到&#x200B;**[!UICONTROL 帐户]**&#x200B;页面，然后将代码粘贴到相应的字段中。

   ![2019-07-25_21-59-12](assets/2019-07-25_21-59-12.png)
   *集成详细信息页面 — JWT选项卡*

   填写了所有字段的“帐户”页显示如下：

   ![2019-07-25_22-08-30](assets/2019-07-25_22-08-30.png)

1. 在右上角附近 **[!UICONTROL 帐户]** 页面，选择 **[!UICONTROL 创建]**.

   在配置Experience ManagerIMS后，您现在有一个新的IMSAccount列在下 **[!UICONTROL Adobe IMS配置]**.

   ![image2019-7-15_14-17-54](assets/image2019-7-15_14-17-54.png)

## 为集成配置Experience Platform标签云 {#configuring-adobe-launch-cloud-for-the-integration}

1. 在“Experience Manager创作”的左上角附近，选择“工具”图标（锤子），然后转到 **[!UICONTROL Cloud Services]** > **[!UICONTROL Experience Platform标记配置]**.

   ![2019-07-26_12-10-38](assets/2019-07-26_12-10-38.png)

1. 在 **[!UICONTROL Experience Platform标记配置]** 页面上，在左侧面板中，选择要为其应用Experience Manager标签配置的Experience Platform站点。

   仅出于示例目的， **`We.Retail`** 在下面的屏幕快照中选择了站点。

   ![2019-07-26_12-20-06](assets/2019-07-26_12-20-06.png)

1. 在页面的左上角附近，选择 **[!UICONTROL 创建]**.
1. 在 **[!UICONTROL 常规]** 第（1/3页） **[!UICONTROL 创建Experience Platform标记配置]** 窗口中，填写以下字段：

   * **[!UICONTROL 标题]**  — 输入描述性配置标题。 例如：`We.Retail Tags cloud configuration`。

   * **[!UICONTROL 关联的Adobe IMS配置]**  — 选择您之前在中创建的IMS配置 [配置Experience ManagerIMS](#configuring-aem-ims).

   * **[!UICONTROL 公司]**  — 从 **[!UICONTROL 公司]** 从下拉列表中，选择您的Experience Cloud公司。 该列表会自动填充。

   * **[!UICONTROL 属性]**  — 从“属性”下拉列表中，选择您之前创建的“Experience Platform标记”属性。 该列表会自动填充。

填写完所有字段后， **[!UICONTROL 常规]** 页面将类似于以下内容：

![image2019-7-15_14-34-23](assets/image2019-7-15_14-34-23.png)

1. 在左上角附近，选择 **[!UICONTROL 下一个]**.
1. 在 **[!UICONTROL 暂存]** 第（2/3页） **[!UICONTROL 创建Experience Platform标记配置]** 窗口中，填写以下字段：

   在 **[!UICONTROL 库URI]** （统一资源标识符）字段，请检查Experience Platform标记库的暂存版本的位置。 Experience Manager会自动填充此字段。

   此步骤使用部署到Experience PlatformCDN的Adobe标记库，仅供解释。

   >[!NOTE]
   >
   >检查以确保自动填充的库URI（统一资源标识符）的格式不正确。 如有必要，请修复该错误，以使URI表示协议相关的URI。 也就是说，它从双正斜线开始。
   >
   >
   >例如：`//assets.adobetm.com/launch-xxxx`。

   您的 **[!UICONTROL 暂存]** 页面可能类似于以下内容。 此 **[!UICONTROL 存档]** 和 **[!UICONTROL 异步加载库]** 选项包括 ***非*** 设置：

   ![image2019-7-15_15-21-8](assets/image2019-7-15_15-21-8.png)

1. 在右上角附近，选择 **[!UICONTROL 下一个]**.
1. 在 **[!UICONTROL 生产]** 第（3/3页） **[!UICONTROL 创建Experience Platform标记配置]** 窗口，如果需要，请修复自动填充的生产URI，类似于在上一个窗口中完成的情况 **[!UICONTROL 暂存]** 页面。
1. 在右上角附近，选择 **[!UICONTROL 创建]**.

   您的新Experience Platform标签云配置现已创建并列在网站旁边。

1. 选择新的Experience Platform标记云配置（选中后，配置标题左侧会显示一个复选标记）。 在工具栏上，选择 **[!UICONTROL Publish]**.

   ![image2019-7-15_15-47-6](assets/image2019-7-15_15-47-6.png)

目前，Experience Manager作者不支持将Dynamic Media查看器与Experience Platform标记集成。

但是，Experience Manager发布节点支持此功能。 使用Experience Platform标签云配置的默认设置，Experience Manager发布会使用Experience Platform标签的生产环境。 因此，每次在测试期间都必须将Experience Platform标签库更新从开发环境推送到生产环境。

可以绕过此限制。 在上面的Experience Platform发布的Experience Platform标记云配置中，指定Experience Manager标记库的开发或暂存URL。 这样做会使Experience Manager发布节点使用Experience Platform标记库的开发版本或暂存版本。

参见 [集成Experience Platform标签和Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/overview.html#integrations) 有关设置Experience Platform标签云配置的更多信息。
