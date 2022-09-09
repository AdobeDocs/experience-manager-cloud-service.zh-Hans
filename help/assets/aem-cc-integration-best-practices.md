---
title: 与集成的最佳实践 [!DNL Adobe Creative Cloud]
description: 最佳实践是将Experience Manager部署与Adobe Creative Cloud集成，以简化资产传输工作流程并实现最高效率。
contentOwner: AG
mini-toc-levels: 1
feature: Collaboration,Adobe Asset Link,Desktop App
role: Architect,User,Admin
exl-id: cbed0d62-5148-45eb-b6a0-9fd164060fdc
source-git-commit: 0d0a3247e42e0f4a9b2965104814fe6bcd8e6128
workflow-type: tm+mt
source-wordcount: '3443'
ht-degree: 15%

---

# Adobe Experience Manager和Creative Cloud集成最佳实践 {#aem-and-creative-cloud-integration-best-practices}

Adobe Experience Manager Assets是一款数字资产管理(DAM)解决方案，它可以与Adobe Creative Cloud集成，以帮助DAM用户与创意团队合作，从而简化内容创建过程中的协作。

Adobe Creative Cloud为创意团队提供解决方案和服务生态系统，以帮助他们创建数字资产。 它包括桌面和移动应用程序、云服务（如具有桌面同步或Web体验的存储）以及市场(如Adobe Stock)。

请阅读相关内容，以了解根据您的用例在桌面与企业级DAM之间选择哪些集成，以及连接工作流的相关最佳实践。

>[!NOTE]
>
>Experience Manager到Creative Cloud文件夹共享现已弃用，不再涵盖以下内容。 Adobe建议使用Adobe资产链接或Experience Manager桌面应用程序等新功能，为创意用户提供对Experience Manager中管理的资产的访问权限。

## 创意人员、营销人员和DAM用户的协作需求 {#collaboration-need-of-creatives-marketers-and-dam-users}

| 要求 | 用例 | 涉及的曲面 |
|---|---|---|
| 简化桌面版创意人员的体验 | 简化从DAM访问资产的过程([!DNL Assets])，或者更广泛地，适用于使用本机资产创建应用程序的桌面用户。 他们需要一种简单明了的方法来发现、使用（打开）、编辑和保存对Experience Manager所做的更改，以及上传新文件。 | Win或Mac台式机；Creative Cloud应用程序 |
| 从提供高质量、可随时使用的资产 [!DNL Adobe Stock] | 营销人员通过协助资产采购和发现来帮助加快内容创建流程。 创意专业人士可直接在其创意工具中使用已批准的资产。 | [!DNL Assets]; [!DNL Adobe Stock] 市场；元数据字段 |
| 按组织分发和共享资产 | 内部部门/地方分支机构和外部合作伙伴、分销商和代理使用由父组织共享的已批准资产。 该组织希望安全、无缝地共享所创建的资产，以便更广泛地重复使用。 | [!DNL Brand Portal]、[!DNL Asset Share Commons] |
| 自动生成已上传资产的预定义变体 | 自动处理资产，利用Adobe独特的媒体处理和转换技术来执行预定义的操作。 创建自定义逻辑，以使用API和资产微服务定义您自己的操作。 | [!DNL Assets] 用户界面 |

## Adobe服务以支持协作需求 {#adobe-offerings-to-support-the-collaboration-need}

| 参与角色的价值主张 | Adobe服务 | 涉及的曲面 |
|---|---|---|
| 创意用户从 [!DNL Experience Manager]，打开并使用它们，编辑并上传对 [!DNL Experience Manager]，以及将新文件上传到 [!DNL Experience Manager]，而不离开 [!DNL Creative Cloud] 应用程序。 | [Adobe Asset Link](https://helpx.adobe.com/cn/enterprise/using/adobe-asset-link.html) | Photoshop、Illustrator和InDesign。 |
| 业务用户简化了资产的打开和使用、编辑和上传更改的过程 [!DNL Experience Manager]，以及将新文件上传到 [!DNL Experience Manager] 从桌面环境。 它们使用通用集成来打开本机桌面应用程序中的任何资产类型，包括非Adobe资产类型。 | [[!DNL Experience Manager] 桌面应用程序](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html) | Experience ManagerWin和Mac桌面上的桌面应用程序 |
| 营销人员和企业用户可在Experience Manager内发现、预览、许可和保存并管理Adobe Stock资产。 授权资产和已保存的资产可提供精选Adobe Stock元数据以更好地管理。 | [Experience Manager和Adobe Stock集成](aem-assets-adobe-stock.md) | [!DNL Experience Manager] web界面 |
| 改进数字产品设计人员与营销人员之间的协作。 让设计师在Adobe XD画布上的设计和线框模型中使用数字资产。 |  [!DNL Adobe XD] 的 [[!DNL Adobe Asset Link] ](https://helpx.adobe.com/cn/enterprise/using/adobe-asset-link-for-xd.html) | [!DNL Adobe XD] |
| 营销人员可以根据上传的资产和使用自定义功能创建的预定义操作，自动创建变体和衍生产品。 使用此自动化可提高内容速度并减少手动工作。 | [内容自动化](/help/assets/cc-api-integration.md) | [!DNL Experience Manager Assets] web界面 |

本文主要介绍协作需求的前两个方面。作为一个用例，简要提及了资产的大规模分发和采购。对于此类需求解决方案，请考虑 Adobe Brand Portal 或 Asset Share Commons。其他解决方案，例如 [Experience Manager AssetsBrand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html)，可基于 [资产共享共用](https://opensource.adobe.com/asset-share-commons/) 组件， [链接共享](share-assets.md)，使用 [Experience Manager Assets Web UI](/help/assets/manage-digital-assets.md) 应根据具体要求进行审查。

![Creative Cloud连接以进行Experience Manager:确定要使用的功能](assets/creative-connections-aem.png)

确定要使用的能力

### 用例映射和Adobe解决方案 {#mapping-of-use-cases-and-adobe-solutions}

| 用例 | Adobe Asset Link | Experience Manager 桌面应用程序 | 备注或替代方法 |
|----------------------------------------------------------|-----------------------------------------------------------------------------------|--------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------|
| Discover — 浏览文件夹 | 是 | Experience ManagerWeb UI +桌面操作 | 浏览网络共享时，关闭缩略图以避免下载资产的二进制文件。 |
| Discover — 访问收藏集 | 是 | Experience ManagerWeb UI +桌面操作 |  |
| Discover — 搜索资产 | 是 | Experience ManagerWeb UI +桌面操作 |  |
| 使用 — 打开的资产 | 是 | 是 — 适用于任何应用程序 | [从Web界面打开](/help/assets/manage-digital-assets.md#previewing-assets) 或从“查找器” |
| 使用 — 将资产从Experience Manager放入文档中 | 是 — 嵌入 | 是 — 链接或嵌入 | Experience Manager桌面应用程序允许将资产作为本地文件系统上的文件访问。 本机应用程序中的这些链接由本地路径表示。 |
| 编辑 — 打开进行编辑 | 是 — 签出操作 | 是 — 打开操作（在网络共享中） | [AAL中的结帐](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html) 默认情况下，会将资产保存到用户的creative cloud存储帐户(由Creative Cloud应用程序同步)。 |
| 编辑 — 在Experience Manager外进行中 | 是 — 用户的Creative Cloud存储帐户中可用的资产已同步到桌面。 | 是 |  |
| 编辑 — 上传更改 | 是 —  [签入操作](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html) 使用可选注释 | 是 |  |
| 上传 — 单个文件 | 是 — 上载当前活动文档 | 是 | [通过Web界面上传](/help/assets/manage-digital-assets.md#uploading-assets) |
| 上传 — 多个文件/分层文件夹结构 | 否 | 是 | [通过Web界面上传](/help/assets/manage-digital-assets.md#uploading-assets);自定义脚本或工具 |
| 杂项 — 用户和登录 | Creative Cloud用户登录Creative Cloud桌面应用程序后被识别(SSO) | Experience Manager用户/登录 | 两个解决方案的用户将根据Experience Manager用户配额进行计数。 |
| 杂项 — 网络和访问 | 需要从用户的桌面访问以通过网络Experience Manager部署 | 需要从用户的桌面访问以通过网络Experience Manager部署 | Adobe资产链接不共享网络代理环境。 |


<!-- Removing this row from table as migration guide is not yet final.
| Misc - Migrate large number of assets | No | No | [Migration Guide](/help/assets/assets-migration-guide.md) |
-->

要支持资产分发用例，请考虑以下选项：

* [Experience Manager AssetsBrand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) ，以供可配置的Assets加载项来发布资产。

* 自定义解决方案基于 [资产共享共用](https://opensource.adobe.com/asset-share-commons/) 代码库。
* Experience Manager [链接共享](/help/assets/share-assets.md) 共享临时资产（使用链接）。
* [资产Web界面](/help/assets/manage-digital-assets.md) 通过由Experience Manager访问控制设置保护外部方的区域，以及必要的IT/网络配置调整，使这些外部用户可以访问Experience Manager。

## 关键概念和用例 {#key-concepts-and-use-cases}

### 常用术语表 {#glossary-of-common-terms}

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

以下是Experience Manager和Creative Cloud集成最佳实践的简短摘要。 阅读本文档的其余部分，以详细了解这些内容。

* **对于在Photoshop、InDesign或Illustrator中工作的创意用户：** Adobe资产链接可提供最佳的用户体验，包括清理从Experience Manager中签出的正在进行的资产
* **简化从桌面访问任何通用文件格式或应用程序资产的操作：** 使用Experience Manager桌面应用程序
* **了解在 DAM 中存储资产的原因和时间：**&#x200B;将提供给组织中更广泛团队的更新
* **关注共享的资产数量：**&#x200B;如果您的用例是资产分发，则管理和安全可能是最重要的方面。考虑使用为大规模操作而构建的工具，如 Brand Portal。
* **了解资产生命周期：**&#x200B;了解组织中不同团队处理资产的方式
* **谨慎处理对资产的频繁保存：** Adobe Asset Link 通过 PS、AI、ID 为您提供相关服务。对于其他应用程序，除非您需要在 DAM 中完成所有更改，否则不要在映射/共享文件夹中执行正在进行的任务

### 从Experience Manager Assets访问Adobe Stock资产 {#access-to-adobe-stock-assets-from-aem-assets}

[Experience Manager和Adobe Stock集成](/help/assets/aem-assets-adobe-stock.md) 使Experience Manager用户能够从Adobe Stock中搜索、预览、授权和保存资产，并将资产保存到Experience Manager。 授权和保存的Adobe Stock资产已选择Stock元数据，该元数据可用于使用额外的过滤器搜索它们。

有关此集成的几个重要要点：

* 将Adobe库中的资产保存到Experience Manager后，这些资产将变成常规的Experience Manager Assets，并将二进制文件保存到Experience Manager存储库。 在Experience Manager中为资产保存了一些与Adobe Stock相关的元数据，否则，摄取过程与任何其他文件的过程相同。 例如，如果智能标记处于活动状态，则会在保存时将标记添加到这些资产中。
* 保存到Experience Manager的资产是一个副本，而不是返回到Adobe Stock的链接。

**在Creative Cloud中处理从Adobe Stock保存到Experience Manager的资产**. 此集成与Adobe资产链接无关，但Adobe资产链接可以这样识别从Stock中保存的这些资产，并在Photoshop、Illustrator或InDesign的Adobe资产链接扩展UI中，在这些资产上显示其他元数据和Stock图标。 这些文件可用于浏览、打开等操作 — 因为它们是保存到Experience Manager时的常规Experience Manager资产。
使用具有Adobe资产链接扩展的Creative Cloud应用程序的创意用户除了能够从Adobe Stock访问已获得许可的资产以进入Experience Manager外，还可以使用Creative Cloud库面板来搜索、预览和许可Adobe Stock资产。
获得Adobe Stock授权并保存到Experience Manager中的资产将可供访问Experience Manager Assets部署的更广泛的团队使用，而通过Creative Cloud库面板从Adobe Stock授权资产的创意人员仅可在其Creative Cloud帐户中默认自行使用。

## 关于在DAM中存储资产 {#about-storing-assets-in-a-dam}

要在创意团队和营销/业务线(LOB)团队之间设计一个高效的工作流并选择最佳支持功能，请务必了解资产何时以及为何存储在DAM中。

### 资产为何存储在DAM中 {#why-assets-are-stored-in-dam}

将资产存储在DAM中，可轻松访问和查找资产。 它可确保组织或生态系统（包括合作伙伴、客户等）中的众多用户都能够利用资产。

大多数组织选择仅存储与下游营销/LOB流程相关的资产(通过Experience Manager Sites发布到Web渠道等渠道，或Adobe Experience Cloud提供的其他渠道 — Marketing Cloud、Advertising Cloud，以及Analytics Cloud测量、提供给用户/合作伙伴等)。 此外，组织会在DAM中存储可能需要审核/批准流程的资产。 这样，DAM存储的资产大多数是极有可能被利用的资产，并避免存储闲置资产。

存储资产还需要考虑技术和资源利用方面的考虑因素。 DAM提供了有关存储资产的其他服务，包括提取元数据、版本控制、生成预览/转码、管理引用和添加访问控制信息。 这些服务需要额外的时间和基础架构资源。

通常，存储所有资产和更新是不可取的。 例如，如果对特定资产的更新质量不佳，并且消耗了过多的资源，则资产可能不会存储在DAM中。

#### 资产存储在DAM中时 {#when-assets-are-stored-in-dam}

创意团队（和组织）通常对在资产生命周期的每个阶段存储资产不感兴趣。 例如，在以下情况下，它们会避免存储资产：

* 尚未完成或有待试验的资产
* 未能通过创意/内部团队审阅周期的资产
* 与相关资产相比，团队有更好的候选人来向外部团队展示其工作

通常，以下类资产存储在DAM中：

* 已达到特定期限且被视为可共享的资产
* 创意团队预先选择的资产
* 根据特定合同或协议(例如，从原始JPG文件、TIFF/图像转换的PSD文件)，由营销部门使用或请求的特定资产格式

#### 资产更新存储在DAM中时 {#when-updates-to-assets-are-stored-in-dam}

作为规则，只应将与更广泛的DAM用户集相关的资产更新存储在DAM中。 它可确保用户（营销和类似功能）在DAM资产时间轴中仅看到相关版本。

通常与资产生命周期中的主要里程碑相关的更改。 例如，初始营销就绪资产或创意团队提供的基于请求/审阅的正式更新应存储在DAM中并进行版本控制。

创意团队在请求更改DAM中的现有资产后进行的更新（供营销团队审阅）便是相关更新的一个示例。 它应存储在DAM中并进行版本控制，以供进一步引用或还原到之前的版本。

以下是一些通常与之无关的更新示例：

* 在准备好进行营销审核之前，已上传资产的早期版本
* 在进行中的阶段中对资产进行频繁的创意更改，然后创意和营销团队才会确定资产已准备就绪

### 用户对DAM的访问权限 {#user-access-to-dam}

Experience Manager Assets根据用户对Experience Manager Assets部署的访问权限支持两种类型的用户。 通常，企业网络（防火墙）内的用户可以直接访问DAM。 企业网络外的其他用户将无法直接访问。 用户类型从技术角度决定可以使用哪些集成。

#### 直接访问DAM的创意用户 {#creative-users-with-direct-access-to-dam}

通常，内部创意团队或已载入内部网络的代理/创意专业人士有权访问DAM实例，包括Experience Manager登录。 Experience Manager和网络基础架构可以设置为允许直接访问外部方（通常是受信任的组织，如为客户工作的机构），以便能够通过网络(例如，通过VPN或IP允许列表)访问Experience Manager。

在这种情况下，Adobe资产链接或Experience Manager桌面应用程序可让您轻松访问最终/已批准的资产，并允许您将创意就绪资产保存到DAM。

#### 无权访问DAM的创意用户 {#creative-users-without-access-to-dam}

无法直接访问DAM实例的外部代理和自由职业者可能需要访问已批准的资产或希望将其新设计添加到DAM。

使用以下策略提供对最终/已批准资产的访问权限：

* 如果资产链接无法正常工作，请使用桌面应用程序。
* 使用 [Experience Manager AssetsBrand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) 用于将资产安全地分发给外部合作伙伴
* 使用基于 [资产共享共用](https://adobe-marketing-cloud.github.io/asset-share-commons/)
* 使用在Experience Manager和必要的网络基础架构（例如，允许列出的VPN和IP）中设置的访问控制，使外部方可以访问DAM中的专用内容区域。 他们可以使用Experience ManagerWeb UI获取资产并将新内容上传到您的DAM。

#### 正在从Experience Manager中处理资产 {#work-in-progress-on-assets-from-aem}

如本文档中所述，建议对资产进行重大更新（有时也称为正在进行中的工作），而不要将保存到本地文件的所有编辑内容也作为更改上传到Experience Manager。 这可加快桌面用户的工作速度，限制所用的网络带宽，并保持资产时间线清晰，并将重点放在受控的重大更新上。

Adobe资产链接为此用例提供了良好支持：

* 当Photoshop、InDesign或Illustrator中的用户意图编辑文件时，他们会对给定资产执行签出操作
* 资产会在后台下载，放入通过Creative Cloud桌面应用程序同步到磁盘的用户Creative Cloud帐户中，并在资产的Experience Manager中切换签出标记，以最大限度地减少编辑冲突
* 此后，用户将在同步位置本地存储的文件中工作，并且可以继续工作并保存所需的任何频率的必要更改
* 此外，由于资产位于Creative Cloud帐户中，因此它也可在用户可能拥有的其他设备上使用(例如，可以在专用的Creative Cloud移动应用程序中打开或编辑)，并且可以与其他Creative Cloud用户共享以进行协作。
* 完成更改后，创意用户可以在其Creative Cloud应用程序中对该文件执行签入操作，并提供可选注释。 Experience Manager中的相应资产将进行版本控制，并使用新的二进制文件更新为。 Experience Manager用户（如营销人员或LOB用户）有权通过Experience Manager资产时间轴UI访问主要资产更改或里程碑。

Experience Manager桌面应用程序为本机应用程序中打开的资产提供网络共享。 默认情况下，在本地完成的所有更改都会在短暂的一段时间后自动上传到Experience Manager。 通过这种配置，在进行中的阶段中频繁保存操作都将上传到Experience Manager并进行版本控制，从而产生大量网络流量和潜在的可扩展性挑战 — 更不用说Experience Manager中不必要的版本了。

此处推荐的方法是使用Experience Manager桌面应用程序中的选项来关闭自动更新，并利用应用程序的资产状态UI中的上传更改操作，手动将更改上传到Experience Manager。

#### 批量上传到DAM {#bulk-upload-to-dam}

在某些情况下，您可能需要同时将大量文件上传到DAM，例如：

* 上传照片拍摄或大型项目的结果
* 上传由创意代理提供的资产
* 如果选择在DAM之外完成，则从较大的集上传选定资产

请注意，此描述是指在桌面用户工作流中正常部分，在操作上（例如，每周或每张照片上）上传文件。 此处未介绍大型资产迁移。

您可以利用以下上传功能：

* 要批量上传大型/分层文件夹，请使用提供 [文件夹上传](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#bulk-upload-assets) 功能。 您还可以上传分层文件夹结构。 资产是在后台上传的，因此不会将其绑定到Web浏览器会话
* 要从单个文件夹上传几个文件，请将文件直接拖到Web界面，或使用Experience Manager Assets Web界面中的“创建”选项。
* 根据您的业务要求，您还可以使用自定义Uploader。

#### 直接从桌面管理数字资产 {#managing-digital-assets-directly-from-desktop}

如果您使用“网络文件共享”来管理数字资产，则只需使用由Experience Manager桌面应用程序映射的网络共享即可被视为一种便捷的替代方法。 从网络文件共享进行转换时，Experience ManagerWeb界面提供了丰富的数字资产管理功能集，这些功能远远超出了网络共享上的可能功能（搜索、收藏集、元数据、协作、预览等），而Experience Manager桌面应用程序提供了一个便捷的链接，用于将服务器端DAM存储库与桌面上的工作连接起来。

避免使用Experience Manager桌面应用程序直接在Experience Manager Assets的网络共享中管理资产。 例如，避免使用Experience Manager桌面应用程序移动/复制多个文件。 请改用Experience Manager Assets Web UI将文件夹从Finder/Explorer拖至网络共享，或使用Experience Manager Assets文件夹上传功能。
