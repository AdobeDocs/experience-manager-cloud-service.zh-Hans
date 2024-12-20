---
title: Content Hub概述
description: 详细了解Content Hub、其主要优势、如何访问它以及如何就Content Hub中提供的选项提供反馈。
exl-id: c5908058-f1ad-4aaa-9e8e-c0157e107ed1
source-git-commit: ed7331647ea2227e6047e42e21444b743ee5ce6d
workflow-type: tm+mt
source-wordcount: '704'
ht-degree: 7%

---

# Content Hub概述 {#overview-content-hub}

| [搜索最佳实践](/help/assets/search-best-practices.md) | [元数据最佳实践](/help/assets/metadata-best-practices.md) | [具有 OpenAPI 功能的 Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets 开发人员文档](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |----|-----|

![Content Hub概述](assets/content-hub-overview.png)

>[!AVAILABILITY]
>
>Content Hub指南现在提供了PDF格式。 下载整个指南，并使用Adobe Acrobat AI Assistant来回答您的疑问。
>
>[!BADGE Content Hub指南PDF]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/content-hub.pdf"}

Content Hub 是 Experience Manager Assets as a Cloud Service 的一部分，旨在让组织及其业务合作伙伴能够民主化地访问品牌内容。它侧重于分发资产以供大规模激活，并创建品牌内内容变体以提高营销敏捷性。

## 为什么选择Content Hub？

Content Hub提供以下主要优势：

**在直观的门户中查找并共享所有品牌批准的资产**

AEM Assets作为单个事实来源，所有批准的资源都会以平面层次结构在Content Hub中自动可用，以改善搜索体验。

**可配置的用户界面**

Content Hub中最常见的属性（如搜索筛选器）是在添加或导入资源时可用的字段、资源属性、用于品牌推广的横幅内容是可配置的，管理员可以轻松地根据自己的要求配置Content Hub用户界面。

**使非创意人员能够编辑和重新混合内容，同时继续使用品牌**

Content Hub允许您使用Adobe Express(如果您具有Adobe Express权限)创建新内容。 您可以通过易于使用的工具编辑现有内容，使用模板和品牌元素生成品牌内变体，以及通过Adobe Firefly中的最新GenAI功能创建新内容。

**了解如何跨团队使用内容**

[!DNL Content Hub]提供了有关资产的宝贵见解，解决了营销利益相关者经常遇到的共同挑战 — 营销活动、渠道和不同区域中使用的资产使用情况统计数据。 通过清楚地了解资产的性能和受欢迎程度，它可提供对增强用户体验必不可少的可操作洞察。

## 先决条件 {#prerequisites-content-hub}

Content Hub需要2024.6版本或更高版本的as a Cloud ServiceExperience Manager的生产创作环境(最低版本为2024.6.16799)。

## 如何访问Content Hub？ {#access-content-hub}

[在设置Content Hub](/help/assets/deploy-content-hub.md)并将用户添加到[Content Hub产品配置文件](/help/assets/deploy-content-hub.md#content-hub-instance-product-profile)后，可以使用以下方式访问Content Hub：

* 使用以下链接访问Content Hub：

  `https://experience.adobe.com/#/assets/contenthub`

* 登录到experience.adobe com，然后单击&#x200B;**[!UICONTROL 快速访问]**&#x200B;部分中的&#x200B;**[!UICONTROL Experience Manager Assets Content Hub]**：
  ![Content Hub访问权限](assets/access-content-hub.png)

* 登录到experience.adobe com，然后单击产品切换器中提供的&#x200B;**[!UICONTROL Experience Manager Assets Content Hub]**：
  ![Content Hub访问方法3](assets/access-content-hub-alternate.png)



## 提供Content Hub反馈 {#provide-content-hub-feedback}

要推荐任何与产品相关的改进，请单击Content Hub用户界面顶部您的组织名称旁边的&#x200B;**[!UICONTROL 反馈]**。

根据需要指定主题、建议描述和附加文件。 单击&#x200B;**[!UICONTROL 提交]**&#x200B;将反馈提交给Adobe。

![Content Hub反馈](assets/content-hub-feedback.png)

## 为您的团队设置Content Hub {#setup-content-hub}

请按照以下步骤为团队设置Content Hub：

1. [使用Cloud Manager为Experience Manager Assets启用Content Hub](deploy-content-hub.md#enable-content-hub)。

1. [载入Content Hub管理员](deploy-content-hub.md#onboard-content-hub-administrator)。

1. [添加关键的Content Hub用户](deploy-content-hub.md#onboard-content-hub-consumer-users)。

1. [要使用Experience Manager资源批准资源的DAM作者或管理员](approve-assets.md)。

1. [管理员可以为其他用户配置Content Hub用户界面](configure-content-hub-ui-options.md)。

1. [向团队中的更多用户授予Content Hub访问权限](deploy-content-hub.md#onboard-content-hub-consumer-users)。

1. [访问Content Hub门户](#access-content-hub)。

1. [提供Content Hub反馈](#provide-content-hub-feedback)。


## 了解关于关键功能的更多信息 {#key-capabilities-content-module}

<table>
<td>
   <a href="/help/assets/configure-content-hub-ui-options.md">
   <img alt="部署 Content Hub" src="./assets/configure-assets.png" />
   </a>
   <div>
      <a href="/help/assets/configure-content-hub-ui-options.md">
      <strong>配置Content Hub用户界面</strong>
      </a>
   </div>
   <p>
      <em>了解管理员如何配置Content Hub用户界面。</em>
   </p>
</td>


<td>
   <a href="/help/assets/search-assets-content-hub.md">
   <img alt="搜索Content Hub中的可用资源" src="./assets/search.png" />
   </a>
   <div>
      <a href="/help/assets/search-assets-content-hub.md">
      <strong>在Content Hub中搜索可用的资源</strong>
      </a>
   </div>
   <p>
      <em>了解如何利用各种功能缩小搜索结果的范围。</em>
   </p>
</td>
<td>
   <a href="/help/assets/edit-images-content-hub.md">
   <img alt="使用 Adobe Express 编辑图像" src="./assets/edit-images-content-hub.png" />
   </a>
   <div>
      <a href="/help/assets/edit-images-content-hub.md">
      <strong>使用Adobe Express编辑图像</strong>
      </a>
   </div>
   <p>
      <em>了解如何使用Adobe Express在Content Hub中创建图像变体</em>
   </p>
</td>
</table>
<table>
<td>
   <a href="/help/assets/share-assets-content-hub.md">
   <img alt="在Content Hub中共享可用资源" src="./assets/share-assets-banner.png" />
   </a>
   <div>
      <a href="/help/assets/share-assets-content-hub.md">
      <strong>在Content Hub中共享可用资源</strong>
      </a>
   </div>
   <p>
      <em>了解如何将一个或多个资源共享为链接，然后访问它们。</em>
   </p>
</td>
<td>
   <a href="/help/assets/collections-content-hub.md">
   <img alt="管理 Content Hub 里的收藏集" src="./assets/manage-collection.png" />
   </a>
   <div>
      <a href="/help/assets/collections-content-hub.md">
      <strong>在Content Hub中管理收藏集</strong>
      </a>
   </div>
   <p>
      <em>了解如何使用资源创建收藏集，然后管理它们。</em>
   </p>
</td>
<td>
   <a href="/help/assets/insights-content-hub.md">
   <img alt="在Content Hub中共享可用资源" src="./assets/asset-insights-banner.jpg" />
   </a>
   <div>
      <a href="/help/assets/insights-content-hub.md">
      <strong>在Content Hub中查看资源分析</strong>
      </a>
   </div>
   <p>
      <em>内容模块提供了有关资产的宝贵见解，解决了营销利益相关者经常遇到的共同挑战</em>
   </p>
</td>
</table>
