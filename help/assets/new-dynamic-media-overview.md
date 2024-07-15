---
title: 具有OpenAPI功能的Dynamic Media
description: 了解关键概念，例如为何将Dynamic Media与OpenAPI功能结合使用以及如何启用它。
role: User
source-git-commit: 0ad9f349c997c35862e4f571b4741ed4c0c947e2
workflow-type: tm+mt
source-wordcount: '906'
ht-degree: 1%

---

# 具有OpenAPI功能的Dynamic Media {#new-dynaminc-media-apis-overview}

在当今快节奏的数字世界中，释放品牌数字资产的全部潜力对于保持竞争优势，至关重要。 全面的数字Assets管理(DAM)解决方案可帮助进行资产治理、促进品牌一致性，并加快内容交付，同时确保品牌完整性和卓越的客户体验。

具有OpenAPI功能的Dynamic Media将DAM置于灵活而高效的内容供应链生态系统的核心，以确保资产治理和交付。

## 为何将Dynamic Media与OpenAPI功能一起使用？ {#new-dynamic-media-api-features}

具有OpenAPI功能的Dynamic Media提供以下主要优势：

* **无缝集成**：具有OpenAPI功能的Dynamic Media提供了一组全面的搜索和交付API。 它允许开发人员轻松[将资产交付与其应用程序](/help/assets/integrate-new-dynamic-media-apis.md)集成。 这些应用程序包括Adobe和第三方应用程序。 此外，它还提供了[Micro Frontend资产选择器用户界面](/help/assets/asset-selector.md)来搜索和选择批准的资产。 该选择器可以轻松地与任何基于JavaScript框架的应用程序(如React JS、AngularJS和Vanilla JS)集成。

* **数字资产的集中管理**： DAM是所有数字资产的单一真实来源。 您的数字资源在AEM Assets中进行集中管理，并通过使用交付URL引用交付给使用应用程序，而无需复制资源二进制文件。

* **实时更新**：对DAM中的已批准资源所做的任何更改（包括版本更新和元数据修改）都会自动反映在投放URL中。 由于通过CDN为Dynamic Media的OpenAPI功能配置了10分钟的短生存时间(TTL)值，因此，在10分钟之内即可看到所有创作和发布界面的更新。

* **品牌一致性**：只有[品牌批准的资产](/help/assets/approved-assets.md)对下游应用程序公开。 [品牌经理和营销人员对品牌资产有严格的控制](/help/assets/restrict-assets-delivery.md)。 只有获得批准的最新版本的资产才可供使用，从而确保跨所有渠道和应用程序的品牌一致性。

* **Web优化投放**：数字资产以Web优化格式投放，以增强您的数字体验的核心Web虚拟。 这包括支持图像的WebP演绎版、视频的通过HLS或DASH协议实现的自适应流式传输，以及文档的原始演绎版。

* **动态资产转换**：我们的系统允许使用称为图像修饰符的URL参数进行动态图像转换。 [例如，宽度、高度、旋转、翻转、质量、裁切和格式](/help/assets/deliver-assets-apis.md)。 具有OpenAPI功能的Dynamic Media还支持图像智能裁剪功能。 转换后的呈现版本会动态生成，并通过CDN无缝交付。

* **安全交付资源**：具有OpenAPI功能的Dynamic Media提供了一种控制数字资源访问权限的机制。 您可以将用户角色或组指定为要保护的资产的元数据，并设置一个预定义的时间范围，在此期间仅[授权用户可以访问这些资产](/help/assets/restrict-assets-delivery.md)。 在限制期间，受保护资产的投放URL不会解析为未授权用户。

* **用于做出明智决策的数据分析**：除了资产管理和交付之外，它还捕获有关CDN上资产交付的交付数据分析，从而允许品牌经理跨渠道跟踪交付量度。 这使他们能够做出数据驱动型决策，以持续优化资产治理和投放策略。

![新 Dynamic Media 数据流图](assets/dm-openapi-dfd.png)

## 使用OpenAPI功能访问Dynamic Media的先决条件 {#prerequisites-new-dynaminc-media-apis}

要访问具有OpenAPI功能的Dynamic Media，您必须具有以下功能的许可证：

* AEM Assets as a Cloud Service

* AEM Dynamic Media

## 如何通过OpenAPI功能启用Dynamic Media？ {#enable-new-dynamic-media-apis}

在提交在AEM as a Cloud Service上启用具有OpenAPI功能的Dynamic Media的请求之前，请确保尚未启用它。 要验证它是否已启用，请执行以下步骤：

1. 待工程和产品管理部门确认

要在AEM as a Cloud Service上启用具有OpenAPI功能的Dynamic Media，请提交Adobe支持工单，其中包含以下详细信息：

* Cloud Service项目和环境ID

* 通过Dynamic Media与OpenAPI功能集成解决的用例详细信息

* 要与Dynamic Media与OpenAPI功能集成的下游应用程序的详细信息。

  >[!NOTE]
  >
  > 要与非Adobe应用程序集成，请提供域名以将应用程序托管位置列入白名单。

* 集成项目中涉及的关键客户联系人的详细信息。

提交支持工单后，Adobe将在您的Cloud Service环境中启用具有OpenAPI功能的Dynamic Media，并共享详细信息（如IMS客户端ID），以便您继续集成。

## 深入了解关键功能 {#learn-more-key-capabilities}

<table>
<td>
   <a href="/help/assets/approved-assets.md">
   <img alt="在Experience Manager Assets中批准资源" src="./assets/approved-assets.jpeg" />
   </a>
   <div>
      <a href="/help/assets/approved-assets.md">
      <strong>在Experience Manager Assets中批准资源</strong>
      </a>
   </div>
   <p>
      <em>在AEM Assets中批准资源以简化资源管理，确保处理资源的过程受到控制且高效。</em>
   </p>
</td>
<td>
   <a href="/help/assets/integrate-new-dynamic-media-apis.md">
   <img alt="将AEM Assets与下游应用程序集成" src="./assets/asset-selector-integration.png" />
   </a>
   <div>
      <a href="/help/assets/integrate-new-dynamic-media-apis.md">
      <strong>将AEM Assets与下游应用程序集成</strong>
      </a>
   </div>
   <p>
      <em>使用搜索和交付API将您自己的自定义用户界面与Experience Manager Assets存储库集成，或使用Adobe的微前端资源选择器。</em>
   </p>
</td>
<td>
   <a href="/help/assets/asset-selector.md">
   <img alt="Adobe的资源选择器" src="./assets/asset-selector-prereqs.png" />
   </a>
   <div>
      <a href="/help/assets/asset-selector.md">
      <strong>Adobe的微前端资源选择器</strong>
      </a>
   </div>
   <p>
      <em>与AEM Assets存储库交互以搜索资产，然后在应用程序创作体验中使用这些资产的用户界面。</em>
   </p>
</td>
</table>
<table>
<td>
   <a href="/help/assets/search-assets-api.md">
   <img alt="搜索资源Experience Manager Assets存储库" src="./assets/search-assets-api-overview.png" />
   </a>
   <div>
      <a href="/help/assets/search-assets-api.md">
      <strong>搜索Experience Manager Assets存储库中的资源</strong>
      </a>
   </div>
   <p>
      <em>搜索AEM Assets存储库中的资源，以便将其传递到下游应用程序。</em>
   </p>
</td>
<td>
   <a href="/help/assets/deliver-assets-apis.md">
   <img alt="将资产交付给下游应用程序" src="./assets/delivery-url.png" />
   </a>
   <div>
      <a href="/help/assets/deliver-assets-apis.md">
      <strong>将资产交付给下游应用程序</strong>
      </a>
   </div>
   <p>
      <em>使用投放URL将资产交付给集成的下游应用程序。</em>
   </p>
</td>
<td>
   <a href="/help/assets/restrict-assets-delivery.md">
   <img alt="限制对Experience Manager中资源的访问" src="./assets/restricted-access.png" />
   </a>
   <div>
      <a href="/help/assets/restrict-assets-delivery.md">
      <strong>限制对Experience Manager中资源的访问</strong>
      </a>
   </div>
   <p>
      <em> DAM管理员或品牌管理员通过在AEM as a Cloud Service创作实例上为批准的资源配置角色来限制访问。</em>
   </p>
</td>
</table>

