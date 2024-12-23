---
title: 具有 OpenAPI 功能的 Dynamic Media
description: 了解关键概念，例如为什么使用具有 OpenAPI 功能的 Dynamic Media 以及如何启用它。
role: User
exl-id: 658b6eff-9f5a-4166-9ff6-5dc8eb92ada3
source-git-commit: ed7331647ea2227e6047e42e21444b743ee5ce6d
workflow-type: tm+mt
source-wordcount: '1109'
ht-degree: 96%

---

# 具有 OpenAPI 功能的 Dynamic Media {#new-dynaminc-media-apis-overview}

| [搜索最佳实践](/help/assets/search-best-practices.md) | [元数据最佳实践](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | [AEM Assets 开发人员文档](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|-----|

>[!AVAILABILITY]
>
>Dynamic Media with OpenAPI功能指南现在以PDF格式提供。 下载整个指南，并使用Adobe Acrobat AI Assistant来回答您的疑问。
>
>[!BADGE 具有OpenAPI功能的Dynamic Media指南PDF]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/dynamic-media-with-openapi-capabilities.pdf"}

在当今快节奏的数字世界中，充分释放品牌数字资产的潜力对于保持竞争优势至关重要。全面的数字资产管理 (DAM) 解决方案有助于资产治理、促进品牌一致性、加速内容传递，同时确保品牌完整性和卓越的客户体验。

具有 OpenAPI 功能的 Dynamic Media 将 DAM 置于敏捷高效的内容供应链生态系统的核心，以确保资产治理和传递。

## 为什么使用具有 OpenAPI 功能的 Dynamic Media？ {#dynamic-media-open-api-features}

具有 OpenAPI 功能的 Dynamic Media 具有以下主要优势：

* **无缝集成**：具有 OpenAPI 功能的 Dynamic Media 提供了一套全面的搜索和传递 API。它有助于开发人员轻松地[将资产传递与其应用程序集成](/help/assets/integrate-dynamic-media-open-apis.md)。这些应用程序包括 Adobe 以及第三方应用程序。它提供了一个[微前端资产选择器用户界面](/help/assets/overview-asset-selector.md)，用于搜索和选择已批准的资产。该选择器可以轻松地与基于 JavaScript 框架（如 React JS、Angular JS 和 Vanilla JS）的任何应用程序集成。

* **集中管理数字资产**：DAM 是所有数字资产的单一数据源。您的数字资产在 AEM Assets 中进行集中管理，并通过使用传递 URL 进行引用，无需复制资产二进制文件，即可传递给消费应用程序。

* **实时更新**：对 DAM 中已批准资产所做的任何更改（包括版本更新和元数据修改）都会自动反映在传递 URL 中。通过内容传递网络为具有 OpenAPI 功能的 Dynamic Media 配置了一个较短的生存时间 (TTL) 值，即 10 分钟，这样，在不到 10 分钟的时间内，更新就会在所有创作和发布的界面上显示出来。

* **品牌一致性**：只有[经过品牌批准的资产](/help/assets/approve-assets.md)才会暴露给下游应用程序。[品牌经理和营销人员对品牌资产保持严格控制](/help/assets/restrict-assets-delivery.md)。只有经过批准的最新版本资产可供使用，以确保所有渠道和应用程序的品牌一致性。

* **针对网络优化的传递**：数字资产以针对网络优化的格式传递，以提升您的数字体验的核心网页关键指标。这包括支持图像的 WebP 演绎版、通过 HLS 或 DASH 协议实现视频的自适应流式处理，以及文档的原始演绎版。

* **动态资产转换**：我们的系统允许使用称为图像修改器的 URL 参数进行即时图像转换。[例如宽度、高度、旋转、翻转、质量、裁切、格式和智能裁剪](/help/assets/deliver-assets-apis.md)。转换后的演绎版是动态生成的，并通过内容传递网络无缝传递。

* **安全传递资产**：具有 OpenAPI 功能的 Dynamic Media 提供了一种控制访问您的数字资产的机制。您可以将用户角色或组指定为要保护的资产的元数据，并设置预定义的时间范围，在此期间[只有授权用户才能访问这些资产](/help/assets/restrict-assets-delivery.md)。在限制期内，未经授权的用户无法解析受保护资产的传递 URL。

* **数据洞察有助于做出明智的决策（即将推出）**：除了资产管理和传递之外，它还可以捕获内容传递网络资产传递的传递数据洞察，从而使品牌经理能够跨渠道跟踪传递指标。它使他们能够基于数据做出决策，以持续优化资产治理和传递策略。

![Dynamic Media Open API 数据流图](assets/dm-openapi-dfd.png)

## 访问具有 OpenAPI 功能的 Dynamic Media 的先决条件 {#prerequisites-dynaminc-media-open-apis}

要访问具有 OpenAPI 功能的 Dynamic Media，您必须拥有以下许可证：

* AEM Assets as a Cloud Service

* AEM Dynamic Media 

## 如何启用具有 OpenAPI 功能的 Dynamic Media？ {#enable-dynamic-media-open-apis}

在提交请求以在 AEM as a Cloud Service 上启用具有 OpenAPI 功能的 Dynamic Media 之前，请确保该功能尚未启用。

在满足[先决条件](#prerequisites-dynaminc-media-open-apis)后，并且如果您的 AEM as a Cloud Service 上启用了具有 OpenAPI 功能的 Dynamic Media 实例，则存储库中每个已批准资产都有一个可用的传递 URL。有关如何复制传递 URL，请参阅[复制已批准资产的传递 URL](approve-assets.md#copy-delivery-url-approved-assets)。Adobe 建议使用此方法验证具有 OpenAPI 功能的 Dynamic Media 是否已在 AEM as a Cloud Service 上启用，然后再通过提交支持工单来启用它。

要在 AEM as a Cloud Service 上启用具有 OpenAPI 功能的 Dynamic Media，请提交包含以下详细信息的 Adobe 支持工单：

* Cloud Services 程序和环境 ID

* 通过集成具有 OpenAPI 功能的 Dynamic Media 来解决的用例的详细信息。

* 要与具有 OpenAPI 功能的 Dynamic Media 集成的下游应用程序的详细信息。

  >[!NOTE]
  >
  要与非 Adobe 应用程序集成，请将域名提供给托管该应用程序的允许列表。

* 参与集成项目的关键客户联系人的详细信息。

* Adobe 帐户团队主要成员列表（电子邮件）。

在提交支持工单后，Adobe 就会在您的 Cloud Services 环境中启用具有 OpenAPI 功能的 Dynamic Media，并会共享详细信息（例如 IMS 客户端 ID），以便您进行集成。

>[!NOTE]
>
从任何内容包中排除 `/conf/global/settings/dam/assets-configurations/assetdelivery`，以避免停用具有 OpenAPI 功能的 Dynamic Media。

## 深入了解关键功能 {#learn-more-key-capabilities}

<table>
<td>
   <a href="/help/assets/approve-assets.md">
   <img alt="在 Experience Manager Assets 中批准资产" src="./assets/approved-assets.jpeg" />
   </a>
   <div>
      <a href="/help/assets/approve-assets.md">
      <strong>在 Experience Manager Assets 中批准资产</strong>
      </a>
   </div>
   <p>
      <em>在 AEM Assets 中批准资产以简化资产管理，确保处理资产的流程可控且高效。</em>
   </p>
</td>
<td>
   <a href="/help/assets/integrate-dynamic-media-open-apis.md">
   <img alt="将 AEM Assets 与下游应用程序集成" src="./assets/asset-selector-integration.png" />
   </a>
   <div>
      <a href="/help/assets/integrate-dynamic-media-open-apis.md">
      <strong>将 AEM Assets 与下游应用程序集成</strong>
      </a>
   </div>
   <p>
      <em>使用搜索和传递 API 或使用 Adobe 的微型前端资产选择器，将您自己的自定义用户界面与 Experience Manager Assets 存储库集成。</em>
   </p>
</td>
<td>
   <a href="/help/assets/overview-asset-selector.md">
   <img alt="Adobe 的资产选择器" src="./assets/asset-selector-prereqs.png" />
   </a>
   <div>
      <a href="/help/assets/overview-asset-selector.md">
      <strong>Adobe 的微型前端资产选择器</strong>
      </a>
   </div>
   <p>
      <em>一个与 AEM Assets 存储库交互的用户界面，用于搜索资产，并在您的应用程序创作体验中使用它们。</em>
   </p>
</td>
</table>
<table>



<table>
<td>
   <a href="/help/assets/search-assets-api.md">
   <img alt="搜索资产 Experience Manager Assets 存储库" src="./assets/search-assets-api-overview.png" />
   </a>
   <div>
      <a href="/help/assets/search-assets-api.md">
      <strong>在 Experience Manager Assets 存储库中搜索资产</strong>
      </a>
   </div>
   <p>
      <em>在 AEM Assets 存储库中搜索资产，以便将其传送到下游应用程序。</em>
   </p>
</td>
<td>
   <a href="/help/assets/deliver-assets-apis.md">
   <img alt="将资产传递给下游应用程序" src="./assets/delivery-url.png" />
   </a>
   <div>
      <a href="/help/assets/deliver-assets-apis.md">
      <strong>将资产传递给下游应用程序</strong>
      </a>
   </div>
   <p>
      <em>使用传递 URL 将资产传递至经过集成的下游应用程序。</em>
   </p>
</td>
<td>
   <a href="/help/assets/restrict-assets-delivery.md">
   <img alt="限制对 Experience Manager 中的资产的访问" src="./assets/restricted-access.png" />
   </a>
   <div>
      <a href="/help/assets/restrict-assets-delivery.md">
      <strong>限制对 Experience Manager 中的资产的访问</strong>
      </a>
   </div>
   <p>
      <em> DAM 管理员或品牌经理通过在 AEM as a Cloud Service 作者实例上为已批准的资产配置角色来限制访问权限。</em>
   </p>
</td>

</table>
<table>
<td>
   <a href="/help/assets/integrate-remote-approved-assets-with-sites.md">
   <img alt="将远程 AEM Assets 与 AEM Sites 集成" src="./assets/connected-assets-rdam.png" />
   </a>
   <div>
      <a href="/help/assets/integrate-remote-approved-assets-with-sites.md">
      <strong>将远程 AEM Assets 与 AEM Sites 集成</strong>
      </a>
   </div>
   <p>
      <em>了解如何将远程 AEM Assets 与 AEM Sites 环境集成。 </em>
   </p>
</td>
<td>
   <a href="/help/assets/dynamic-media-open-apis-faqs.md">
   <img alt="具有 OpenAPI 功能的 Dynamic Media 常见问题解答" src="./assets/dynamic-media-faqs.jpeg" />
   </a>
   <div>
      <a href="/help/assets/dynamic-media-open-apis-faqs.md">
      <strong>具有 OpenAPI 功能的 Dynamic Media 常见问题解答</strong>
      </a>
   </div>
   <p>
      <em>获取有关具有 OpenAPI 功能的 Dynamic Media 最常见的问题的答案。</em>
   </p>
</td>
<td>
   <a href="/help/assets/configure-custom-domain.md">
   <img alt="配置自定义域" src="./assets/configure-custom-domain.jpeg" />
   </a>
   <div>
      <a href="/help/assets/configure-custom-domain.md">
      <strong>配置自定义域</strong>
      </a>
   </div>
   <p>
      <em>虽然 AEM as a Cloud Service 自带一个默认域，但您可以根据自己的需要进行定制</em>
   </p>
</td>

</table>
