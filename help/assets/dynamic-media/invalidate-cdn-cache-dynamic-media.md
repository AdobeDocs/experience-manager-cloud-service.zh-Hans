---
title: 通过Dynamic Media使内容交付网络缓存失效
description: 了解如何使CDN（内容分发网络）缓存内容失效，以便快速更新由Dynamic Media交付的资产，而无需等待缓存过期。
feature: Asset Management
role: Admin,User
exl-id: c631079b-8082-4ff7-a122-dac1b20d8acd
source-git-commit: 5c8e3a7ea87b70707b2613ffc7b4f51341303614
workflow-type: tm+mt
source-wordcount: '1384'
ht-degree: 1%

---

# 通过 Dynamic Media 使 CDN 缓存失效 {#invalidating-cdn-cache-for-dm-assets-in-aem-cs}

Dynamic Media资产由CDN（内容交付网络）缓存，以便快速交付给客户。 但是，当您更新这些资产时，您希望这些更改在您的网站上立即生效。 通过清除或使CDN缓存失效，您可以快速更新由Dynamic Media交付的资产。 您不再需要使用TTL（生存时间）值（默认为十小时）等待缓存过期。 相反，您可以从Dynamic Media用户界面中发送请求，让缓存在几分钟内过期。

>[!NOTE]
>
>此功能要求您使用Adobe Experience Manager Dynamic Media附带的Adobe捆绑CDN。 此功能不支持任何其他自定义CDN。

<!-- REMOVED MARCH 28, 2022 BECAUSE OF 404; NO REDIRECT WAS PUT IN PLACE BY SUPPORT See also [Cache overview in Dynamic Media](https://helpx.adobe.com/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html). -->

如果已启用 [智能成像](/help/assets/dynamic-media/imaging-faq.md) 在您的帐户上，如果您使用Adobe捆绑的CDN，则可以通过清除单个基本URL来清除具有不同查询字符串的所有URL。

例如，使用 `https://weekendsite.scene7.com/is/image/grundfos/image`，还会使以下URL失效：

* `https://weekendsite.scene7.com/is/image/grundfos/image`
* `https://weekendsite.scene7.com/is/image/grundfos/image?wid=300`
* `https://weekendsite.scene7.com/is/image/grundfos/image?$PLP$`
* 等等。

但是，不支持智能成像的通用域(例如， `s7d1.scene7.com`. 此类域仍需要完整的URL才能成功失效。

**要通过Dynamic Media使CDN缓存失效，请执行以下操作：**

*第1部分（共2部分）：创建CDN失效模板*

1. 在Adobe Experience Manager as a Cloud Service，转到 **[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL CDN失效模板]**.

   ![CDN验证功能](/help/assets/assets-dm/cdn-invalidation-template.png)

1. 在 **[!UICONTROL CDN失效模板]** ，请根据您的情景执行以下选项之一：

   | 方案 | 选项 |
   | --- | --- |
   | 我过去曾使用Dynamic Media Classic创建过CDN失效模板。 | 的 **[!UICONTROL 创建模板]** 文本字段中预先填充了模板数据。 在这种情况下，您可以编辑模板，也可以继续下一步。 |
   | 我必须创建一个模板。 我要输入什么？ | 在 **[!UICONTROL 创建模板]** 文本字段中，输入引用了 `<ID>`，而不是像以下示例中那样使用特定的图像ID:<br>`https://my.publishserver.com/is/image/company_name/<ID>?$product$`<br>如果模板仅包含 `<ID>`，然后Dynamic Media填充 `https://<publishserver_name>/is/image/<company_name>/<ID>` where `<publishserver_name>` 是在Dynamic Media Classic的“常规设置”中定义的发布服务器名称。 的 `<company_name>` 是与此Experience Manager实例关联的公司根目录的名称， `<ID>` 通过资产选取器选择的资产无效。<br>以下任何预设/修饰符 `<ID>` 在URL定义中按原样复制。<br>只有图像， `/is/image` — 可基于模板自动形成。<br>对于 `/is/content/`，则使用资产选取器添加资产(如视频或PDF)不会自动生成URL。 您而是必须在CDN失效模板中指定此类资产，或在 *第2部分：设置CDN失效选项*.<br>**示例：**<br>&#x200B;在第一个示例中，失效模板包含 `<ID>` 以及具有 `/is/content`. 例如：`http://my.publishserver.com:8080/is/content/dms7snapshot/<ID>`。Dynamic Media根据此路径(使用 `<ID>` 通过要失效的资产选取器选择的资产。<br>在第二个示例中，失效模板包含您的Web属性中使用的资产的完整URL，其中包含 `/is/content` （不取决于资产选取器）。 例如， `http://my.publishserver.com:8080/is/content/dms7snapshot/backpack` 其中，背包是资产ID。<br>Dynamic Media中支持的资产格式有资格失效。 以下资产文件类型 *not* 支持CDN失效功能，包括PostScript®、封装的PostScript®、Adobe Illustrator、Adobe InDesign、Microsoft® Powerpoint、Microsoft® Excel、Microsoft® Word和富文本格式。<br><br>·创建模板时，请务必注意语法和拼写错误；Dynamic Media不执行任何模板验证。<br>· CDN失效模板最多可保存2500个字符的文本。<br>·在此CDN失效模板或 **[!UICONTROL 添加URL]** 文本字段 *第2部分：设置CDN失效选项。*<br>· CDN失效模板中的每个条目必须位于其自身的行上。<br>·以下CDN失效模板示例仅供演示之用。 |

   ![CDN失效模板 — 创建](/help/assets/assets-dm/cdn-invalidation-template-create-2.png)

   >[!NOTE]
   >
   >CDN失效模板最多可保存2500个字符的文本。

1. 位于的右上角 **[!UICONTROL CDN失效模板]** 页面，选择 **[!UICONTROL 保存]**，然后选择 **[!UICONTROL 确定]**.<br>

   *第2部分：设置CDN失效选项*
   <br>

1. 在Experience Manageras a Cloud Service中，转到 **[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL CDN失效]**.

   ![CDN验证功能](/help/assets/assets-dm/cdn-invalidation-path.png)

1. 在 **[!UICONTROL CDN失效]** - **[!UICONTROL 添加详细信息]** 页面，选择要使CDN失效的资产。

   ![CDN失效 — 添加详细信息](/help/assets/assets-dm/cdn-invalidation-add-details-2.png)

   >[!NOTE]
   >
   >如果您决定保留选项 **[!UICONTROL 在CDN中使与资产关联的图像预设失效]** *和* **[!UICONTROL 基于模板无效]** 如果未选中，则会为失效而形成选定资产的基本URL。 仅对图像使用此选项排列。


   | 选项 | 描述 |
   | --- | --- |
   | **[!UICONTROL 使 CDN 中与资产关联的图像预设失效]** | （可选）选中此选项后，为使缓存失效，会自动形成选定资产及其所有关联的图像预设URL。<br>资产及其关联的预定义预设URL会自动形成为失效。 此选项仅适用于图像资产。 |
   | **[!UICONTROL 基于模板的失效]** | （可选）选中此选项可仅使用定义的模板进行URL形成。 |
   | **[!UICONTROL 添加资产]** | 使用资产选取器选择要失效的资产。 您可以选择已发布或未发布的资产。<br>CDN上的缓存基于URL，而不是基于资产。 因此，您必须了解您网站上的完整URL。 确定这些URL后，可以将其添加到模板中。 然后，您可以选择并添加这些资产，并在一个步骤中使URL失效。 <br>将此选项与 **[!UICONTROL 在CDN中使与资产关联的图像预设失效]**&#x200B;或 **[!UICONTROL 基于模板的失效]**，或两者兼有。 |
   | **[!UICONTROL 添加 URL]** | 手动向要使其CDN缓存失效的Dynamic Media资产添加或粘贴完整URL路径。 如果您未在 ***第1部分（共2部分）：创建CDN失效模板***，并且只有少数资产要失效。<br>**重要信息：** 您添加的每个URL都必须位于其自身的行上。<br>您一次最多可以使1000个URL失效。 如果 **[!UICONTROL 添加URL]** 文本字段大于1000，则无法选择 **[!UICONTROL 下一个]**. 在这种情况下，您必须选择 **[!UICONTROL X]** ，以将其从失效列表中删除。<br>在CDN失效模板或此模板中为图像智能裁剪指定URL **[!UICONTROL 添加URL]** 文本。 |

1. 在页面的右上角附近，选择 **[!UICONTROL 下一个]**.
1. 在 **[!UICONTROL CDN失效]** - **[!UICONTROL 确认]** 页面，在 **[!UICONTROL URL]** 列表框中，您会看到一个或多个URL列表，这些URL来自您之前创建的CDN失效模板以及您刚才添加的资产。

   例如，使用前面步骤中显示的CDN失效模板示例，假设您添加了一个名为 `spinset`. 当您 **[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL CDN失效]**，则会在 **[!UICONTROL CDN失效 — 确认]** 用户界面：

   ![CDN失效 — 确认](/help/assets/assets-dm/cdn-invalidation-confirm-2.png)

   如有必要，请选择 **X** ，以将其从失效过程中删除。

1. 在页面的右上角附近，选择 **[!UICONTROL 提交]** 开始CDN失效过程。

## 对CDN失效错误进行故障诊断

在所有情况下，都会处理整个批次以使其失效，或者整个批次失败。

| 错误 | 说明 |
| --- | --- |
| *无法检索选定资产的URL。* | 在满足以下任何情况时发生：<br> — 未找到Dynamic Media配置。<br> — 检索用于读取Dynamic Media配置的服务用户时出现异常。<br>- Dynamic Media配置中缺少用于构成URL的发布服务器或公司根目录。 |
| *某些URL定义不正确。 更正并重新提交。* | 在IPS CDN缓存失效API返回错误时发生。 该错误表示URL引用的是其他公司，或者URL无效，因为IPS cdnCacheInvalidation API已完成验证。 |
| *无法使CDN缓存失效。* | 在CDN缓存失效请求因任何其他原因失败时发生。 |
| *输入的URL无效。* | 如果 **[!UICONTROL CDN失效]** - **[!UICONTROL 确认]** 页面时，您会选择 **[!UICONTROL 提交]**. |


<!--  | I do not want to create a template. | Near the upper-right corner of the page, select **[!UICONTROL Cancel]**, then continue with ***Part 2: Working with CDN Invalidation***. Note that while you are not required to create a template to use CDN Invalidation, Adobe recommends that you create one, especially if you have numerous assets that you need to update immediately, on a regular basis. The template is used at the time you set CDN invalidation options. | -->
