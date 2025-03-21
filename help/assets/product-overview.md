---
title: Content Hub 概览
description: 了解有关 Content Hub 的更多信息、其主要优势、如何访问它以及如何围绕 Content Hub 中的可用选项提供反馈。
exl-id: c5908058-f1ad-4aaa-9e8e-c0157e107ed1
source-git-commit: c82f84fe99d8a196adebe504fef78ed8f0b747a9
workflow-type: tm+mt
source-wordcount: '733'
ht-degree: 96%

---

# Content Hub 概览 {#overview-content-hub}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime和Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup><a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM Assets与Edge Delivery Services的集成</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>UI可扩展性</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新建</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>启用Dynamic Media Prime和Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>搜索最佳实践</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>元数据最佳实践</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>具有 OpenAPI 功能的 Dynamic Media</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>AEM Assets 开发人员文档</b></a>
        </td>
    </tr>
</table>

![Content Hub 概览](assets/content-hub-overview.png)

>[!AVAILABILITY]
>
>Content Hub 指南现以 PDF 格式提供。下载完整指南并使用 Adobe Acrobat AI 助手来回答您的疑问。
>
>[!BADGE Content Hub 指南 PDF]{type=Informative url="https://helpx.adobe.com/cn/content/dam/help/en/experience-manager/aem-assets/content-hub.pdf"}

Content Hub 是 Experience Manager Assets as a Cloud Service 的一部分，旨在为组织及其业务合作伙伴提供对品牌内容的普及化访问。它侧重于大规模分发资产以进行激活，并创建品牌内容变体，以提高营销敏捷度。

## 为什么使用 Content Hub？

Content Hub 具有以下主要优势：

**在直观的门户中查找和共享所有品牌认可的资产**

AEM Assets 是一个单一数据源，所有经过审批的资产都会自动以扁平层级结构的形式呈现在 Content Hub 上，以提升搜索体验。

**可配置的用户界面**

Content Hub 中最常见的属性，如搜索过滤器、添加或导入资产时可用的字段、资产属性、品牌横幅内容都是可配置的，管理员可以根据自己的要求轻松配置 Content Hub 用户界面。

**让非创意人员也能编辑和合成内容，同时保持品牌一致性**

Content Hub 允许您使用 Adobe Express 创建新内容（如果您有 Adobe Express 权限）。您可以使用易于使用的工具编辑现有内容，使用模板和品牌元素制作品牌变体，并使用 Adobe Firefly 的最新 GenAI功 能创建新内容。

**深入了解内容在团队间的使用情况**

[!DNL Content Hub] 提供了对资产的宝贵见解，解决了营销利益相关者经常遇到的共同挑战——营销活动、渠道和不同地区使用的资产使用情况统计数据。通过清楚地了解资产的性能和受欢迎程度，它提供了对增强用户体验至关重要的可操作见解。

## 先决条件 {#prerequisites-content-hub}

Content Hub 需要 Experience Manager as a Cloud Service 2024.6 版本或更高版本（最低版本为 2024.6.16799）的生产作者环境。

## 如何访问 Content Hub？ {#access-content-hub}

[设置 Content Hub](/help/assets/deploy-content-hub.md) 并将用户添加到 [Content Hub 产品配置文件](/help/assets/deploy-content-hub.md#content-hub-instance-product-profile)后，可以通过以下方式访问 Content Hub：

* 使用以下链接访问 Content Hub：

  `https://experience.adobe.com/#/assets/contenthub`

* 登录 [experience.adobe.com](https://auth.services.adobe.com/en_GB/index.html?callback=https%3A%2F%2Fims-na1.adobelogin.com%2Fims%2Fadobeid%2Fexc_app%2FAdobeID%2Ftoken%3Fredirect_uri%3Dhttps%253A%252F%252Fexperience.adobe.com%252F%2523old_hash%253Dold_hash%253D%252523%25252F%2526from_ims%253Dtrue%253Fclient_id%253Dexc_app%2526api%253Dauthorize%2526scope%253Dab.manage%252Caccount_cluster.read%252Cadditional_info%252Cadditional_info.job_function%252Cadditional_info.projectedProductContext%252Cadditional_info.roles%252CAdobeID%252Cadobeio.appregistry.read%252Cadobeio_api%252Caudiencemanager_api%252Ccreative_cloud%252Cmps%252Copenid%252Corg.read%252Cpps.read%252Cread_organizations%252Cread_pc%252Cread_pc.acp%252Cread_pc.dma_tartan%252Csession%26state%3D%257B%2522jslibver%2522%253A%2522v2-v0.31.0-2-g1e8a8a8%2522%252C%2522nonce%2522%253A%25222316022399331147%2522%257D%26code_challenge_method%3Dplain%26use_ms_for_expiry%3Dtrue&amp;client_id=exc_app&amp;scope=ab.manage%2Caccount_cluster.read%2Cadditional_info%2Cadditional_info.job_function%2Cadditional_info.projectedProductContext%2Cadditional_info.roles%2CAdobeID%2Cadobeio.appregistry.read%2Cadobeio_api%2Caudiencemanager_api%2Ccreative_cloud%2Cmps%2Copenid%2Corg.read%2Cpps.read%2Cread_organizations%2Cread_pc%2Cread_pc.acp%2Cread_pc.dma_tartan%2Csession&amp;state=%7B%22jslibver%22%3A%22v2-v0.31.0-2-g1e8a8a8%22%2C%22nonce%22%3A%222316022399331147%22%7D&amp;relay=64da7fa8-cd9e-47cf-9892-7f3ef3092f8c&amp;locale=en_GB&amp;flow_type=token&amp;dctx_id=v%3A2%2Cs%2Cf%2Cb8e64530-b013-11ee-a6c1-e721bdec0171&amp;idp_flow_type=login&amp;response_type=token&amp;profile_filter=%7B%22findFirst%22%3Atrue%2C+%22fallbackToAA%22%3Atrue%2C+%22preferForwardProfile%22%3Atrue%2C+%22searchEntireCluster%22%3Atrue%7D%3B+isOwnedByOrg%28%2776B329395DF155D60A495E2C%40AdobeOrg%27%29&amp;code_challenge_method=plain&amp;redirect_uri=https%3A%2F%2Fexperience.adobe.com%2F%23old_hash%3Dold_hash%3D%2523%252F%26from_ims%3Dtrue%3Fclient_id%3Dexc_app%26api%3Dauthorize%26scope%3Dab.manage%2Caccount_cluster.read%2Cadditional_info%2Cadditional_info.job_function%2Cadditional_info.projectedProductContext%2Cadditional_info.roles%2CAdobeID%2Cadobeio.appregistry.read%2Cadobeio_api%2Caudiencemanager_api%2Ccreative_cloud%2Cmps%2Copenid%2Corg.read%2Cpps.read%2Cread_organizations%2Cread_pc%2Cread_pc.acp%2Cread_pc.dma_tartan%2Csession&amp;use_ms_for_expiry=true#/) 并单击&#x200B;**[!UICONTROL 快速访问]**&#x200B;部分中的&#x200B;**[!UICONTROL Experience Manager Assets Content Hub]**：
  ![Content Hub Access](assets/access-content-hub.png)

* 登录 [experience.adobe.com](https://auth.services.adobe.com/en_GB/index.html?callback=https%3A%2F%2Fims-na1.adobelogin.com%2Fims%2Fadobeid%2Fexc_app%2FAdobeID%2Ftoken%3Fredirect_uri%3Dhttps%253A%252F%252Fexperience.adobe.com%252F%2523old_hash%253Dold_hash%253D%252523%25252F%2526from_ims%253Dtrue%253Fclient_id%253Dexc_app%2526api%253Dauthorize%2526scope%253Dab.manage%252Caccount_cluster.read%252Cadditional_info%252Cadditional_info.job_function%252Cadditional_info.projectedProductContext%252Cadditional_info.roles%252CAdobeID%252Cadobeio.appregistry.read%252Cadobeio_api%252Caudiencemanager_api%252Ccreative_cloud%252Cmps%252Copenid%252Corg.read%252Cpps.read%252Cread_organizations%252Cread_pc%252Cread_pc.acp%252Cread_pc.dma_tartan%252Csession%26state%3D%257B%2522jslibver%2522%253A%2522v2-v0.31.0-2-g1e8a8a8%2522%252C%2522nonce%2522%253A%25222316022399331147%2522%257D%26code_challenge_method%3Dplain%26use_ms_for_expiry%3Dtrue&amp;client_id=exc_app&amp;scope=ab.manage%2Caccount_cluster.read%2Cadditional_info%2Cadditional_info.job_function%2Cadditional_info.projectedProductContext%2Cadditional_info.roles%2CAdobeID%2Cadobeio.appregistry.read%2Cadobeio_api%2Caudiencemanager_api%2Ccreative_cloud%2Cmps%2Copenid%2Corg.read%2Cpps.read%2Cread_organizations%2Cread_pc%2Cread_pc.acp%2Cread_pc.dma_tartan%2Csession&amp;state=%7B%22jslibver%22%3A%22v2-v0.31.0-2-g1e8a8a8%22%2C%22nonce%22%3A%222316022399331147%22%7D&amp;relay=64da7fa8-cd9e-47cf-9892-7f3ef3092f8c&amp;locale=en_GB&amp;flow_type=token&amp;dctx_id=v%3A2%2Cs%2Cf%2Cb8e64530-b013-11ee-a6c1-e721bdec0171&amp;idp_flow_type=login&amp;response_type=token&amp;profile_filter=%7B%22findFirst%22%3Atrue%2C+%22fallbackToAA%22%3Atrue%2C+%22preferForwardProfile%22%3Atrue%2C+%22searchEntireCluster%22%3Atrue%7D%3B+isOwnedByOrg%28%2776B329395DF155D60A495E2C%40AdobeOrg%27%29&amp;code_challenge_method=plain&amp;redirect_uri=https%3A%2F%2Fexperience.adobe.com%2F%23old_hash%3Dold_hash%3D%2523%252F%26from_ims%3Dtrue%3Fclient_id%3Dexc_app%26api%3Dauthorize%26scope%3Dab.manage%2Caccount_cluster.read%2Cadditional_info%2Cadditional_info.job_function%2Cadditional_info.projectedProductContext%2Cadditional_info.roles%2CAdobeID%2Cadobeio.appregistry.read%2Cadobeio_api%2Caudiencemanager_api%2Ccreative_cloud%2Cmps%2Copenid%2Corg.read%2Cpps.read%2Cread_organizations%2Cread_pc%2Cread_pc.acp%2Cread_pc.dma_tartan%2Csession&amp;use_ms_for_expiry=true#/) 并单击产品切换器中的&#x200B;**[!UICONTROL Experience Manager Assets Content Hub]**：
  ![Content Hub 访问方法 3](assets/access-content-hub-alternate.png)



## 提供 Content Hub 反馈 {#provide-content-hub-feedback}

要推荐任何与产品相关的改进，请单击 Content Hub 用户界面顶部您的组织名称旁边的&#x200B;**[!UICONTROL 反馈]**。

指定主题、推荐说明，并在需要时附加文件。单击&#x200B;**[!UICONTROL 提交]**&#x200B;向 Adobe 提交反馈。

![Content Hub 反馈](assets/content-hub-feedback.png)

## 为团队设置 Content Hub {#setup-content-hub}

请按照以下步骤为您的团队设置 Content Hub：

1. [使用 Cloud Manager 启用 Content Center for Experience Manager Assets](deploy-content-hub.md#enable-content-hub)。

1. [加入 Content Hub 管理员](deploy-content-hub.md#onboard-content-hub-administrator)。

1. [添加关键 Content Hub 用户](deploy-content-hub.md#onboard-content-hub-consumer-users)。

1. [作为 DAM 作者或管理员在 Experience Manager Assets 中已批准的资产。](approve-assets.md)

1. [以管理员身份为其他用户配置 Content Hub 用户界面。](configure-content-hub-ui-options.md)

1. [授予团队中更多用户访问 Content Hub 的权限](deploy-content-hub.md#onboard-content-hub-consumer-users)。

1. [访问 Content Hub 门户网站](#access-content-hub)。

1. [提供 Content Hub 反馈](#provide-content-hub-feedback)。


## 详细了解关键功能 {#key-capabilities-content-module}

<table>
<td>
   <a href="/help/assets/configure-content-hub-ui-options.md">
   <img alt="部署 Content Hub" src="./assets/configure-assets.png" />
   </a>
   <div>
      <a href="/help/assets/configure-content-hub-ui-options.md">
      <strong>配置 Content Hub 用户界面</strong>
      </a>
   </div>
   <p>
      <em>了解管理员如何配置 Content Hub 用户界面。</em>
   </p>
</td>


<td>
   <a href="/help/assets/search-assets-content-hub.md">
   <img alt="在 Content Hub 搜索资产" src="./assets/search.png" />
   </a>
   <div>
      <a href="/help/assets/search-assets-content-hub.md">
      <strong>在 Content Hub 搜索资产</strong>
      </a>
   </div>
   <p>
      <em>了解如何利用各种功能来缩小搜索结果。</em>
   </p>
</td>
<td>
   <a href="/help/assets/edit-images-content-hub.md">
   <img alt="使用 Adobe Express 编辑图像" src="./assets/edit-images-content-hub.png" />
   </a>
   <div>
      <a href="/help/assets/edit-images-content-hub.md">
      <strong>使用 Adobe Express 编辑图像</strong>
      </a>
   </div>
   <p>
      <em>了解如何使用 Adobe Express 在 Content Hub 中创建图像变体</em>
   </p>
</td>
</table>
<table>
<td>
   <a href="/help/assets/share-assets-content-hub.md">
   <img alt="共享 Content Hub 中的可用资产" src="./assets/share-assets-banner.png" />
   </a>
   <div>
      <a href="/help/assets/share-assets-content-hub.md">
      <strong>在 Content Hub 共享资产</strong>
      </a>
   </div>
   <p>
      <em>了解如何以链接形式共享一个或多个资产，然后访问它们。</em>
   </p>
</td>
<td>
   <a href="/help/assets/collections-content-hub.md">
   <img alt="管理 Content Hub 中的收藏集" src="./assets/manage-collection.png" />
   </a>
   <div>
      <a href="/help/assets/collections-content-hub.md">
      <strong>管理 Content Hub 中的收藏集</strong>
      </a>
   </div>
   <p>
      <em>了解如何使用资产创建收藏集并管理它们。</em>
   </p>
</td>
<td>
   <a href="/help/assets/insights-content-hub.md">
   <img alt="共享 Content Hub 中的可用资产" src="./assets/asset-insights-banner.jpg" />
   </a>
   <div>
      <a href="/help/assets/insights-content-hub.md">
      <strong>在 Content Hub 中查看资产洞察</strong>
      </a>
   </div>
   <p>
      <em> 内容模块提供了对资产的宝贵见解，解决了营销利益相关者经常遇到的共同挑战</em>
   </p>
</td>
</table>
