---
title: 要与集成的最佳实践 [!DNL Adobe Creative Cloud]
description: 最佳实践将Experience Manager部署与Adobe Creative Cloud集成，以简化资产传输工作流并实现最高效率。
contentOwner: AG
mini-toc-levels: 1
feature: Collaboration,Adobe Asset Link,Desktop App
role: Architect,User,Admin
exl-id: cbed0d62-5148-45eb-b6a0-9fd164060fdc
source-git-commit: 80ac947976bab2b0bfedb4ff9d5dd4634de6b4fc
workflow-type: tm+mt
source-wordcount: '3495'
ht-degree: 16%

---

# Adobe Experience Manager和Creative Cloud集成最佳实践 {#aem-and-creative-cloud-integration-best-practices}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/aem-cc-integration-best-practices.html?lang=zh-Hans) |
| AEM as a Cloud Service | 本文 |

Adobe Experience Manager Assets是一种数字资源管理(DAM)解决方案，可与Adobe Creative Cloud集成以帮助DAM用户与创意团队合作，从而简化内容创建过程中的协作。

Adobe Creative Cloud为创意团队提供了一个解决方案和服务生态系统，以帮助他们创建数字资产。 它包括桌面和移动应用程序、云服务（如具有桌面同步或Web体验的存储设备）以及Adobe Stock等市场。

请阅读并了解根据您的用例在桌面版和企业级DAM之间选择哪些集成，以及连接工作流的关联最佳实践是什么。

>[!NOTE]
>
>Creative Cloud文件夹共享的Experience Manager现已弃用，不再包含以下内容。 Adobe建议使用诸如Adobe资产链接或Experience Manager桌面应用程序等较新功能，以便创意用户能够访问Experience Manager中管理的资产。

## 创意人员、营销人员和DAM用户的协作需求 {#collaboration-need-of-creatives-marketers-and-dam-users}

| 要求 | 用例 | 涉及的曲面 |
|---|---|---|
| 简化创意人员在台式机上的体验 | 简化从DAM访问资产的操作([!DNL Assets])适用于创意专业人士或更广义地说，适用于在本机资产创建应用程序中工作的桌面版用户。 他们需要一种简单直接的方式来发现、使用（打开）、编辑和保存对Experience Manager所做的更改，以及上传新文件。 | Win或Mac桌面；Creative Cloud应用程序 |
| 从以下位置提供高质量、现成可用的资产： [!DNL Adobe Stock] | 营销人员通过协助进行资产来源和发现，帮助加快内容创建过程。 创意专业人士直接在其创意工具中使用批准的资产。 | [!DNL Assets]； [!DNL Adobe Stock] 商城；元数据字段 |
| 按组织分发和共享资产 | 内部部门/本地分支机构以及外部合作伙伴、分销商和代理机构使用由上级组织共享的批准资产。 公司希望安全、无缝地共享所创建的资产，以便更广泛地重复使用。 | [!DNL Brand Portal]、[!DNL Asset Share Commons] |
| 自动生成已上传资产的预定义变体 | 利用Adobe独特的介质处理和转换技术自动处理资源，以执行预定义操作。 创建自定义逻辑以使用API和资产微服务定义您自己的操作。 | [!DNL Assets] 用户界面 |

## 支持协作需要的Adobe产品 {#adobe-offerings-to-support-the-collaboration-need}

| 对所涉角色的价值主张 | Adobe产品 | 涉及的曲面 |
|---|---|---|
| 创意用户从中发现资源 [!DNL Experience Manager]，打开并使用它们，编辑和上传更改到 [!DNL Experience Manager]，并将新文件上传到 [!DNL Experience Manager]，无需离开他们的 [!DNL Creative Cloud] 应用程序。 | [Adobe Asset Link](https://helpx.adobe.com/cn/enterprise/using/adobe-asset-link.html) | Photoshop、Illustrator和InDesign。 |
| 企业用户可简化资产的打开和使用以及对资产的编辑和上传更改 [!DNL Experience Manager]，并将新文件上传到 [!DNL Experience Manager] 桌面环境中的。 它们使用通用集成来打开本机桌面应用程序中的任何资源类型，包括非Adobe资源类型。 | [[!DNL Experience Manager] 桌面应用程序](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html) | 在Win和Mac桌面上Experience Manager桌面应用程序 |
| 营销人员和企业用户可在Experience Manager中发现、预览、许可并保存和管理Adobe Stock资源。 许可和保存的资源提供选定的Adobe Stock元数据以便更好地管理。 | [Experience Manager与Adobe Stock集成](aem-assets-adobe-stock.md) | [!DNL Experience Manager] Web界面 |
| 改进数字产品设计师和营销人员之间的协作。 让设计人员在Adobe XD画布上的设计和线框模型中使用数字资源。 |  [!DNL Adobe XD] 的 [[!DNL Adobe Asset Link] ](https://helpx.adobe.com/cn/enterprise/using/adobe-asset-link-for-xd.html) | [!DNL Adobe XD] |
| 营销人员可以根据上传的资产和使用自定义创建的预定义操作自动创建变体和衍生品。 使用此自动化可以提高内容速度并减少手动操作。 | [内容自动化](/help/assets/cc-api-integration.md) | [!DNL Experience Manager Assets] Web界面 |

本文主要介绍协作需求的前两个方面。作为一个用例，简要提及了资产的大规模分发和采购。对于此类需求解决方案，请考虑 Adobe Brand Portal 或 Asset Share Commons。替代解决方案，例如 [Experience Manager Assets Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html)，可基于以下项构建的解决方案 [资产共享公域](https://opensource.adobe.com/asset-share-commons/) 组件， [链接共享](share-assets.md)，使用 [Experience Manager Assets Web UI](/help/assets/manage-digital-assets.md) 应根据特定要求进行审查。

![用于Experience Manager的Creative Cloud连接：决定使用哪种功能](assets/creative-connections-aem.png)

决定使用哪种功能

### 用例和Adobe解决方案的映射 {#mapping-of-use-cases-and-adobe-solutions}

| 用例 | Adobe Asset Link | Experience Manager 桌面应用程序 | 备注或备用方法 |
|----------------------------------------------------------|-----------------------------------------------------------------------------------|--------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------|
| 发现 — 浏览文件夹 | 是 | Experience ManagerWeb UI +桌面操作 | 浏览网络共享时，请关闭缩略图以避免下载资产的二进制文件。 |
| 发现 — 访问收藏集 | 是 | Experience ManagerWeb UI +桌面操作 |  |
| 发现 — 搜索资源 | 是 | Experience ManagerWeb UI +桌面操作 |  |
| 使用 — 打开资源 | 是 | 是 — 适用于任何应用程序 | [从Web界面打开](/help/assets/manage-digital-assets.md#previewing-assets) 或从Finder访问 |
| 使用 — 将资源从Experience Manager放入文档中 | 是 — 嵌入 | 是 — 链接或嵌入 | Experience Manager桌面应用程序允许将资源作为文件访问本地文件系统。 本机应用程序中的这些链接由本地路径表示。 |
| 编辑 — 打开以进行编辑 | 是 — 签出操作 | 是 — 打开操作（在网络共享中） | [在AAL中签出](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html) 默认情况下，将资源保存到用户的creative cloud storage帐户(由Creative Cloud应用程序同步)。 |
| 编辑 — 在Experience Manager之外正在进行工作 | 是 — 用户的Creative Cloud存储帐户中可用的资源已同步到桌面。 | 是 |  |
| 编辑 — 上传更改 | 是 —  [签入操作](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html) 带有可选注释 | 是 |  |
| 上传 — 单个文件 | 是 — 上传当前活动文档 | 是 | [通过Web界面上传](/help/assets/manage-digital-assets.md#uploading-assets) |
| 上传 — 多个文件/分层文件夹结构 | 否 | 是 | [通过Web界面上传](/help/assets/manage-digital-assets.md#uploading-assets)；自定义脚本或工具 |
| 其他 — 用户和登录 | 可识别登录到Creative Cloud桌面应用程序的Creative Cloud用户(SSO) | Experience Manager用户/登录 | 这两个解决方案的用户都计算在Experience Manager用户配额中。 |
| 杂项 — 网络和访问 | 需要从用户桌面访问通过网络进行Experience Manager部署 | 需要从用户桌面访问通过网络进行Experience Manager部署 | AdobeAsset Link不共享网络代理环境。 |


<!-- Removing this row from table as migration guide is not yet final.
| Misc - Migrate large number of assets | No | No | [Migration Guide](/help/assets/assets-migration-guide.md) |
-->

要支持资产分发用例，请考虑以下选项：

* [Experience Manager Assets Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) 用于可配置的Assets加载项以发布资产。

* 自定义解决方案是根据 [资产共享公域](https://opensource.adobe.com/asset-share-commons/) 代码库。
* Experience Manager [链接共享](/help/assets/share-assets.md) 使用链接临时共享资产。
* [Assets Web界面](/help/assets/manage-digital-assets.md) 通过Experience Manager访问控制设置保护外部参与方的区域，以及必要的IT/网络配置调整，使这些外部用户能够访问Experience Manager。

## 主要概念和用例 {#key-concepts-and-use-cases}

### 常用术语词汇表 {#glossary-of-common-terms}

* **正在进行的工作或正在进行的创意工作 (WIP)：**&#x200B;资产生命周期中的一个阶段，在此阶段中，资产会经历多次更改，通常尚未准备好与更广的团队共享。
* **创意就绪资产：**&#x200B;已准备好与更广的团队共享的资产，或者已经由创意团队选择/批准与营销或 LOB 团队共享的资产。

* **资产批准：**&#x200B;为已上传到 DAM 的资产运行的批准流程，通常包括品牌批准、法律批准等。
* **最终资产：**&#x200B;已完成所有批准/元数据标记并可供更广的团队使用的资产。此类资产存储在 DAM 中，可供所有（或所有感兴趣的）用户使用。它可用于营销渠道或由创意团队用来创建设计。

* **次要资产更新/更改：**&#x200B;对数字资产进行快速、微小的更改。它通常是响应润饰或次要编辑请求、资产审阅或批准（例如，重新定位、更改文本大小、调整饱和度/亮度、颜色等）而生成的。
* **主要资产更新/更改：**&#x200B;需要大量工作，并且有时必须在较长的一段时间内完成的数字资产更改。它通常包括多项更改。更新资产时必须多次保存。主要资产更新通常会导致资产进入 WIP 阶段。
* **DAM：**&#x200B;数字资产管理。在本文档中，除非另有特别说明，否则它与 Experience Manager Assets 同义。
* **创意用户：**&#x200B;使用 Creative Cloud 应用程序和服务创建数字资产的创意专业人士。在某些情况下，创意用户可能是使用 Creative Cloud 但不创建数字资产的创意团队成员（如创意总监或创意团队经理）。
* **DAM 用户：** DAM 系统的典型用户。根据组织的不同，DAM 用户可以是营销或非营销用户，例如业务线 (LOB) 用户、管理员、销售人员等。

### 使用Experience Manager和Creative Cloud集成时的注意事项 {#considerations-when-using-aem-and-creative-cloud-integration}

<!--incomplete and TBD: 

* DA2.0 best practices: See troubleshooting.md
* Stock integration: See ?
* AAL: See ?
* BP: See ?

-->

这是Experience Manager和Creative Cloud集成的最佳实践的简短摘要。 请阅读本文档的其余部分以获得对这些内容的详细了解。

* **对于在Photoshop、InDesign或Illustrator中工作的创意用户：** AdobeAsset Link提供了最佳用户体验，包括清晰处理从Experience Manager中签出的正在进行的资源
* **简化从桌面访问任何通用文件格式或应用程序资产的操作：** 使用Experience Manager桌面应用程序
* **了解在 DAM 中存储资产的原因和时间：**&#x200B;将提供给组织中更广泛团队的更新
* **关注共享的资产数量：**&#x200B;如果您的用例是资产分发，则管理和安全可能是最重要的方面。考虑使用为大规模操作而构建的工具，如 Brand Portal。
* **了解资产生命周期：**&#x200B;了解组织中不同团队处理资产的方式
* **谨慎处理对资产的频繁保存：** Adobe Asset Link 通过 PS、AI、ID 为您提供相关服务。对于其他应用程序，除非您需要在 DAM 中完成所有更改，否则不要在映射/共享文件夹中执行正在进行的任务

### 从Experience Manager Assets访问Adobe Stock资源 {#access-to-adobe-stock-assets-from-aem-assets}

[Experience Manager与Adobe Stock集成](/help/assets/aem-assets-adobe-stock.md) 让Experience Manager用户能够从Adobe Stock搜索、预览、许可和保存资源并将其保存到Experience Manager中。 已许可和保存的Adobe Stock资源已选择Stock元数据，这些元数据可用于通过额外的筛选器搜索这些资源。

有关此集成的一些要点：

* 将Adobe库存中的资源保存到Experience Manager后，这些资源会变成常规Experience Manager Assets，其中二进制文件会保存到Experience Manager存储库中。 会将资源的一些与Adobe Stock相关的元数据保存在Experience Manager中，否则摄取过程将与任何其他文件相同。 例如，如果智能标记处于活动状态，则会在保存时将标记添加到这些资产中。
* 保存到Experience Manager的资源是一个副本，而不是返回到Adobe Stock的链接。

**使用从Adobe Stock保存到Creative CloudExperience Manager中的资源**. 此集成独立于Adobe Asset Link，但Adobe Asset Link可以识别通过这种方式从Stock中保存的这些资源，并在Photoshop、Illustrator或InDesign的Adobe Asset Link扩展UI中在这些资源上显示其他元数据和库存图标。 这些文件可用于浏览、打开等 — 因为它们是保存到Experience Manager时的常规Experience Manager资源。
在Creative Cloud具有AdobeAsset Link扩展的应用程序中工作的创意用户除了可以从Adobe Stock访问已获得许可的资产以进行Experience Manager之外，还可以使用Creative Cloud库面板来搜索、预览和许可Adobe Stock资产。
Adobe Stock中许可并保存为Experience Manager的资产可供访问Experience Manager Assets部署的更广泛团队使用，而创意人员通过Creative Cloud库面板从Adobe Stock中许可资产，则默认情况下仅可在其Creative Cloud帐户中供他们自己使用。

## 关于在DAM中存储资产 {#about-storing-assets-in-a-dam}

要在创意团队和营销/业务线(LOB)团队之间设计有效的工作流并选择最佳支持功能，务必要了解资产存储在DAM中的时间和原因。

### 为何将资产存储在DAM中 {#why-assets-are-stored-in-dam}

将资产存储在DAM中可轻松访问和查找。 它确保资产可供整个组织或生态系统（包括合作伙伴、客户等）中的众多用户利用。

大多数组织选择仅存储与下游营销/LOB流程相关的资产(通过Experience Manager Sites发布到Web渠道等渠道，或发布到Adobe Experience Cloud提供的其他渠道(Marketing Cloud、Advertising Cloud和Analytics Cloud衡量的渠道，提供给用户/合作伙伴等)。 此外，组织还会在DAM中存储可能接受审查/批准流程的资产。 这样，DAM存储的大部分资产都极有可能被利用，并且避免了存储闲置资产。

存储资产还受技术和资源利用率考虑的约束。 DAM围绕存储的资产提供其他服务，包括提取元数据、版本控制、生成预览/转码、管理引用和添加访问控制信息。 这些服务会消耗额外的时间和基础架构资源。

通常，不希望存储所有资产和更新。 例如，如果对特定资产的更新质量不佳并占用过多资源，则资产可能不会存储在DAM中。

#### 当资产存储在DAM中时 {#when-assets-are-stored-in-dam}

创意团队（和组织）通常对存储资产生命周期每个阶段的资产不感兴趣。 例如，他们避免在以下情况下存储资产：

* 尚未完成或有待试验的资产
* 未通过创意/内部团队审核周期的资产
* 与相关资产相比，该团队拥有更好的候选人来代表他们的工作对外团队

通常，以下类资产存储在DAM中：

* 达到一定到期日并被视为可共享资产
* 创意团队预先选定的资产
* 营销活动可使用或请求的特定资源格式，具体取决于特定合同或协议(例如，从RAW文件转换的JPG文件、来自PSD原始文件的TIFF/图像)

#### 当资产的更新存储在DAM中时 {#when-updates-to-assets-are-stored-in-dam}

作为规则，只有与更广泛的DAM用户集相关的资产更新才应存储在DAM中。 它确保用户（营销和类似功能）只能在DAM资产时间轴中看到相关版本。

通常与资产生命周期中的主要里程碑相关的更改。 例如，初始营销就绪型资产或基于创意团队提供的请求/审阅的正式更新应存储在DAM中并进行版本控制。

在请求更改DAM中的现有资产后，创意团队的更新以供营销团队查看，这是相关更新的示例。 它应存储在DAM中并对其进行版本控制，以备进一步参考或还原到以前的版本。

以下是通常无关的更新示例：

* 在资产准备好进行营销审查之前上传资产的早期版本
* 在创意和营销团队确定资产已准备就绪之前，在创作中阶段对资产进行频繁的创意更改

### 用户对DAM的访问权限 {#user-access-to-dam}

根据用户对Experience Manager Assets部署的访问权限，Experience Manager Assets支持两种类型的用户。 通常，企业网络（防火墙）内的用户可以直接访问DAM。 企业网络以外的其他用户无法直接访问。 用户类型从技术角度确定可以使用哪些集成。

#### 直接访问DAM的创意用户 {#creative-users-with-direct-access-to-dam}

通常，内部创意团队或载入内部网络的代理/创意专业人士有权访问DAM实例，包括Experience Manager登录。 可以设置Experience Manager和网络基础设施来允许直接访问外部各方（通常是受信任的组织，如为客户端工作的机构）来访问通过网络进行的Experience Manager，例如，通过VPN或IP允许列表。

在这种情况下，AdobeAsset Link或Experience Manager桌面应用程序可让您轻松访问最终/批准的资源，并可将创意就绪资源保存到DAM。

#### 无权访问DAM的创意用户 {#creative-users-without-access-to-dam}

无法直接访问DAM实例的外部机构和自由职业者可能需要访问批准的资产，或希望将其新设计添加到DAM。

使用以下策略提供对最终/已批准资产的访问权限：

* 如果Asset Link不起作用，请使用桌面应用程序。
* 使用 [Experience Manager Assets Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) 用于将资产安全地分发给外部合作伙伴
* 使用基于的分发和采购门户的自定义实施 [资产共享公域](https://adobe-marketing-cloud.github.io/asset-share-commons/)
* 使用在Experience Manager和必要的网络基础设施（例如，VPN和IP允许列表）中设置的访问控制，允许外部各方访问DAM中的专用内容区域。 他们可以使用Experience ManagerWeb UI获取资源并将新内容上传到您的DAM。

#### 正在从Experience Manager处理资源 {#work-in-progress-on-assets-from-aem}

如本文档中所述，建议对资源执行重大更新，有时也称为正在进行的工作，而不需将保存到本地文件的所有编辑内容也作为更改上传到Experience Manager。 这可以加快桌面用户的工作，限制使用的网络带宽，保持资产时间线整洁并专注于受控制的重大更新。

AdobeAsset Link对此用例提供了良好的支持：

* 当Photoshop、InDesign或Illustrator中的用户打算编辑文件时，他们对给定资源执行签出操作
* 在后台下载资源，通过Creative Cloud桌面应用程序将其放入与磁盘同步的Creative Cloud用户帐户中，并在资源上的Experience Manager中切换签出标记以最大限度地减少编辑冲突
* 从此处，用户可在本地存储在同步位置的文件中工作，并可按所需的任何频率继续工作和保存必要的更改
* 此外，由于资产位于Creative Cloud帐户中，因此该资产也可在用户可能拥有的其他设备上使用(例如，可以在专用的Creative Cloud移动设备应用程序中打开或编辑该资产)，并可与其他Creative Cloud用户共享以用于协作目的。
* 当创意用户完成更改后，他们可以在其Creative Cloud应用程序中对该文件执行签入操作，并带有可选注释。 Experience Manager中的相应资源将进行版本控制，并使用新二进制文件更新为。 Experience Manager用户（如营销人员或LOB用户）可以通过Experience Manager资源时间线UI访问主要资源更改或里程碑。

Experience Manager桌面应用程序为在本机应用程序中打开的资产提供网络共享。 默认情况下，在本地完成的所有更改都会在短时间内自动上传到Experience Manager。 有了这样的配置，工作进行阶段频繁进行的保存操作都将上载到Experience Manager并进行版本控制，从而带来大量网络流量和潜在的可扩展性难题，更不用说Experience Manager中的不必要版本了。

此处推荐的方法是，使用Experience Manager桌面应用程序中的选项来关闭自动更新，并利用应用程序的资源状态UI中的上传更改操作将更改上传到资源以手动Experience Manager。

#### 批量上传至DAM {#bulk-upload-to-dam}

在某些情况下，您可能要求同时将大量文件上传到DAM，例如：

* 上传照片拍摄或较大项目的结果
* 上传创意机构提供的资产
* 如果在DAM外部完成选择，则从更大的集中上传选定的资产

请注意，此描述是指以可操作方式上传文件（例如，每周或每次拍照），作为桌面用户工作流的正常部分。 此处不涉及大型资产迁移。

您可以利用以下上传功能：

* Experience Manager要批量上传大型/分层文件夹，请使用提供 [文件夹上传](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#bulk-upload-assets) 功能。 您还可以上载分层文件夹结构。 资产在后台上传，因此不会绑定到Web浏览器会话
* 要从单个文件夹上传几个文件，请将这些文件直接拖到Web界面，或使用Experience Manager Assets Web界面中的“创建”选项。
* 根据您的业务要求，您还可以使用自定义上传程序。

#### 直接从桌面管理数字资产 {#managing-digital-assets-directly-from-desktop}

如果您使用网络文件共享来管理数字资源，则只需使用Experience Manager桌面应用程序映射的网络共享即可被视为一种方便的替代方法。 从网络文件共享过渡时，Experience ManagerWeb界面提供了一组丰富的数字资产管理功能，这些功能远远超出了网络共享上可提供的功能（搜索、收藏集、元数据、协作、预览等），而Experience Manager桌面应用程序则提供用于将服务器端DAM存储库与桌面上的工作关联的方便链接。

避免使用Experience Manager桌面应用程序直接在Experience Manager Assets的网络共享中管理资产。 例如，避免使用Experience Manager桌面应用程序移动/复制多个文件。 请改用Experience Manager Assets Web UI将文件夹从Finder/Explorer拖到网络共享中，或使用Experience Manager Assets文件夹上传功能。

**另请参阅**

* [翻译资源](translate-assets.md)
* [Assets HTTP API](mac-api-assets.md)
* [资源支持的文件格式](file-format-support.md)
* [搜索资源](search-assets.md)
* [连接的资源](use-assets-across-connected-assets-instances.md)
* [资源报告](asset-reports.md)
* [元数据架构](metadata-schemas.md)
* [下载资源](download-assets-from-aem.md)
* [管理元数据](manage-metadata.md)
* [搜索 Facet](search-facets.md)
* [管理收藏集](manage-collections.md)
* [批量元数据导入](metadata-import-export.md)
