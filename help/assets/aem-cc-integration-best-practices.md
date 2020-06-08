---
title: Adobe Experience Manager和Adobe Creative Cloud集成最佳实践
description: 将AEM实例与Adobe Creative Cloud集成的最佳实践，可简化资产转让工作流并实现最高效率。
contentOwner: AG
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 82dd9bd69fe994f74c7be8a571e386f0e902f6a1
workflow-type: tm+mt
source-wordcount: '3300'
ht-degree: 18%

---


# AEM和Creative Cloud集成最佳实践 {#aem-and-creative-cloud-integration-best-practices}

Adobe Experience Manager(AEM)资产是一款数字资产管理(DAM)解决方案，可与Adobe Creative Cloud集成，帮助DAM用户与创意团队协作，从而简化内容创建过程中的协作。

Adobe Creative Cloud为创意团队提供解决方案和服务生态系统，帮助他们创建数字资产。 它包括桌面和移动应用程序、云服务(如存储与桌面同步或Web体验)以及Adobe Stock等市场。

阅读以了解根据您的用例在桌面和企业级DAM之间选择哪些集成，以及连接工作流的相关最佳实践。

>[!NOTE]
>
>AEM到Creative Cloud文件夹共享现已弃用，下文不再涵盖。 Adobe建议使用Adobe Asset Link或AEM桌面应用程序等更新的功能，使创意用户能够访问在AEM中管理的资产。

## 创意人员、营销人员和DAM用户的协作需求 {#collaboration-need-of-creatives-marketers-and-dam-users}


| 要求 | 用例 | 涉及的表面 |
|---|---|---|
| 简化桌面创意人员的体验 | 简化创意专业人士（或更广泛地说，是使用桌面设备、使用本机资产创建应用程序的用户）从DAM（AEM资产）访问资产的过程。 他们需要一种简单明了的方法来发现、使用（打开）、编辑和保存对AEM所做的更改，以及上传新文件。 | Win或Mac桌面； Creative Cloud应用程序 |
| 从Adobe Stock提供高质量、随时可用的资源 | 营销人员通过协助资产采购和发现来帮助加快内容创建流程。 创意专业人士直接在其创意工具中使用获准的资产。 | AEM Assets; Adobe Stock市场； 元数据字段 |
| 按组织分发和共享资产 | 内部部门／地方分支机构和外部合作伙伴、分销商和代理使用父组织共享的已批准资产。 该组织希望安全、无缝地共享创建的资产，以扩大重用范围。 | Brand Portal, Asset Share Commons |

## 支持协作需求的Adobe产品 {#adobe-offerings-to-support-the-collaboration-need}

| 相关角色的价值主张 | Adobe产品 | 涉及的表面 |
|---|---|---|
| 创意用户无需离开Creative Cloud应用程序，即可发现AEM中的资产、打开并使用资产、编辑更改并上传到AEM，以及将新文件上传到AEM。 | [Adobe Asset Link](https://helpx.adobe.com/cn/enterprise/using/adobe-asset-link.html) | Photoshop、Illustrator和InDesign |
| 商业用户简化了资产的打开和使用、编辑和上传对AEM的更改，以及从桌面环境将新文件上传到AEM。 他们使用通用集成在本机桌面应用程序中打开任何资产类型，包括非Adobe资产类型。 | [AEM 桌面应用程序](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html) | Win和Mac桌面上的AEM桌面应用程序 |
| 营销人员和商业用户可在AEM中发现、预览、许可、保存和管理Adobe Stock资产。 许可和保存的资源提供精选的Adobe Stock元数据以更好地进行管理。 | [Experience Manager与Adobe Stock集成](aem-assets-adobe-stock.md) | AEM Web界面 |

本文主要介绍协作需求的前两个方面。作为一个用例，简要提及了资产的大规模分发和采购。对于此类需求解决方案，请考虑 Adobe Brand Portal 或 Asset Share Commons。其他解决方案，如 [AEM Assets Brand Portal](https://helpx.adobe.com/cn/experience-manager/brand-portal/user-guide.html)，可基于 [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/) 组件构建的解决方案， [Link Share](share-assets.md)[](/help/assets/manage-digital-assets.md) ，使用AEM Assets Web UI，应根据特定要求审查这些解决方案。

![适用于AEM的Creative Cloud连接： 确定要使用的功能](assets/creative-connections-aem.png)

确定要使用的功能

### 用例映射和Adobe解决方案 {#mapping-of-use-cases-and-adobe-solutions}

| 用例 | Adobe Asset Link | AEM 桌面应用程序 | 备注或替代方法 |
|----------------------------------------------------------|-----------------------------------------------------------------------------------|--------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------|
| 发现——浏览AEM文件夹 | 是 | AEM Web UI +桌面操作 | 浏览网络共享时，关闭缩略图以避免下载资源的二进制文件。 |
| 发现——访问AEM集合 | 是 | AEM Web UI +桌面操作 |  |
| 发现——从AEM搜索资产 | 是 | AEM Web UI +桌面操作 |  |
| 使用——打开资产 | 是 | 是 -适用于任何应用程序 | [从Web界面或Finder](/help/assets/manage-digital-assets.md#previewing-assets) 打开 |
| 使用——将资产从AEM置入文档 | 是——嵌入 | 是——链接或嵌入 | AEM桌面应用程序允许以文件形式访问本地文件系统中的资产。 本机应用程序中的这些链接由本地路径表示。 |
| 编辑——打开进行编辑 | 是——结帐操作 | 是——打开操作（在网络共享中） | [默认情况下](https://helpx.adobe.com/cn/enterprise/using/manage-assets-using-adobe-asset-link.html) ,AAL中的注销会将资产保存到用户的Creative Cloud存储帐户（由Creative Cloud应用程序同步）。 |
| 编辑——在AEM外进行中的工作 | 是——用户的Creative Cloud存储帐户中的可用资产已同步到桌面。 | 是 |  |
| 编辑——上传更改 | 是- [带可选注释的签入](https://helpx.adobe.com/cn/enterprise/using/manage-assets-using-adobe-asset-link.html) 操作 | 是 |  |
| 上传——单个文件 | 是——上载当前活动文档 | 是 | [通过Web界面上传](/help/assets/manage-digital-assets.md#uploading-assets) |
| 上传——多个文件／分层文件夹结构 | 否 | 是 | [通过Web界面上传](/help/assets/manage-digital-assets.md#uploading-assets); 自定义脚本或工具 |
| 杂项——用户和登录名 | 登录到Creative Cloud桌面应用程序的Creative Cloud用户可被识别(SSO) | AEM用户／登录 | 两个解决方案的用户均计入AEM用户配额。 |
| 杂项——网络和访问 | 需要从用户桌面访问网络上的AEM部署 | 需要从用户桌面访问网络上的AEM部署 | Adobe Asset Link不共享网络代理环境。 |


<!-- Removing this row from table as migration guide is not yet final.
| Misc - Migrate large number of assets | No | No | [Migration Guide](/help/assets/assets-migration-guide.md) |
-->

要支持资产分发使用案例，应考虑其他解决方案：

* [AEM Assets Brand Portal](https://helpx.adobe.com/cn/experience-manager/brand-portal/user-guide.html) ，用于向AEM Assets添加可配置的SaaS加载项以发布资产。

* 自定义解决方案是基于资 [产共享共享共享](https://adobe-marketing-cloud.github.io/asset-share-commons/) 共享代码库创建的。
* AEM链 [接共享](/help/assets/share-assets.md) ，以使用链接临时共享资产。
* [AEM Assets Web界面](/help/assets/manage-digital-assets.md) ，其中包含由AEM访问控制设置保护的外部方的区域以及必要的IT/网络配置调整，使这些外部用户能够访问AEM。

## 主要概念和用例 {#key-concepts-and-use-cases}

### 常用术语表 {#glossary-of-common-terms}

* **正在进行的工作或正在进行的创意工作 (WIP)：**&#x200B;资产生命周期中的一个阶段，在此阶段中，资产会经历多次更改，通常尚未准备好与更广的团队共享。
* **创意就绪资产：**&#x200B;已准备好与更广的团队共享的资产，或者已经由创意团队选择/批准与营销或 LOB 团队共享的资产。

* **资产批准：**&#x200B;为已上传到 DAM 的资产运行的批准流程，通常包括品牌批准、法律批准等。
* **最终资产：**&#x200B;已完成所有批准/元数据标记并可供更广的团队使用的资产。此类资产存储在 DAM 中，可供所有（或所有感兴趣的）用户使用。它可用于营销渠道或由创意团队用来创建设计。

* **次要资产更新/更改：**&#x200B;对数字资产进行快速、微小的更改。它通常是响应润饰或次要编辑请求、资产审阅或批准（例如，重新定位、更改文本大小、调整饱和度/亮度、颜色等）而生成的。
* **主要资产更新/更改：**&#x200B;需要大量工作，并且有时必须在较长的一段时间内完成的数字资产更改。它通常包括多项更改。更新资产时必须多次保存。主要资产更新通常会导致资产进入 WIP 阶段。
* **DAM：**&#x200B;数字资产管理。在本文档中，除非另有特别说明，否则它与 AEM Experience Manager Assets 同义。
* **创意用户：**&#x200B;使用 Creative Cloud 应用程序和服务创建数字资产的创意专业人士。在某些情况下，创意用户可能是使用 Creative Cloud 但不创建数字资产的创意团队成员（如创意总监或创意团队经理）。
* **DAM 用户：** DAM 系统的典型用户。根据组织的不同，DAM 用户可以是营销或非营销用户，例如业务线 (LOB) 用户、管理员、销售人员等。

### 使用AEM和Creative Cloud集成时的注意事项 {#considerations-when-using-aem-and-creative-cloud-integration}

<!--incomplete and TBD: 

* DA2.0 best practices: See troubleshooting.md
* Stock integration: See ?
* AAL: See ?
* BP: See ?

-->

这是AEM和Creative Cloud集成最佳实践的简要总结。 阅读本文档的其余部分，详细了解这些内容。

* **对于使用 Photoshop、InDesign 或 Illustrator 的创意用户：** Adobe Asset Link 提供了最佳用户体验，包括清晰处理从 AEM 中签出的正在进行的资产
* **简化从桌面访问任何通用文件格式或应用程序资产的操作：**&#x200B;请使用 AEM 桌面应用程序
* **了解在 DAM 中存储资产的原因和时间：**&#x200B;将提供给组织中更广泛团队的更新
* **关注共享的资产数量：**&#x200B;如果您的用例是资产分发，则管理和安全可能是最重要的方面。考虑使用为大规模操作而构建的工具，如 Brand Portal。
* **了解资产生命周期：**&#x200B;了解组织中不同团队处理资产的方式
* **谨慎处理对资产的频繁保存：** Adobe Asset Link 通过 PS、AI、ID 为您提供相关服务。对于其他应用程序，除非您需要在 DAM 中完成所有更改，否则不要在映射/共享文件夹中执行正在进行的任务

### 从AEM资产访问Adobe Stock资产 {#access-to-adobe-stock-assets-from-aem-assets}

[AEM和Adobe Stock集成](/help/assets/aem-assets-adobe-stock.md) 使AEM用户能够从Adobe Stock中搜索、预览、许可和将资产保存到AEM中。 已授权和保存的Adobe Stock资源已选择Stock元数据，该元数据可用于通过额外的过滤器搜索它们。

有关此集成的几个要点：

* 将Adobe Stock中的资产保存到AEM后，这些资产将成为常规AEM资产，并将二进制文件保存到AEM存储库。 某些与Adobe Stock相关的元数据会在AEM中为资产保存，否则，摄取过程与任何其他文件的过程一样。 例如，如果智能标记处于活动状态，则在保存这些资产时会向其添加标记。
* 保存到AEM的资产是副本，而不是返回到Adobe Stock的链接。

**处理从Adobe Stock保存到Creative Cloud中的AEM的资源**。 此集成与Adobe Asset Link无关，但Adobe Asset Link可以识别从Stock保存的这些资源，并在Photoshop、Illustrator或InDesign的Adobe Asset Link扩展UI中在这些资源上显示其他元数据和Stock图标。 这些文件可用于浏览、打开等操作——因为它们是保存到AEM时的常规AEM资产。
使用Creative Cloud应用程序并带有Adobe Asset Link扩展的创意用户除了可以访问已授权的资源（从Adobe Stock到AEM）外，还可以使用Creative Cloud库面板搜索、预览和许可Adobe Stock资源。
获得许可并保存到AEM中的Adobe Stock资源可供访问AEM资产部署的更多团队使用，而通过Creative Cloud库面板从Adobe Stock授权的创意人员仅可在其Creative Cloud帐户中默认自行使用。

## 关于在DAM中存储资产 {#about-storing-assets-in-a-dam}

要在创意团队和营销／业务线(LOB)团队之间设计一个高效的工作流程并选择最佳支持功能，请务必了解资产何时以及为何存储在DAM中。

### 资产存储在DAM中的原因 {#why-assets-are-stored-in-dam}

将资产存储在DAM中，使资产易于访问和查找。 它确保整个组织或生态系统（包括合作伙伴、客户等）中的大量用户都能利用资产。

大多数组织选择只存储与下游营销/LOB流程相关的资产(通过AEM Sites发布到Web渠道等渠道，或Adobe Experience Cloud - Marketing Cloud、Advertising Cloud提供的其他渠道，并通过Analytics Cloud进行衡量，向用户／合作伙伴提供信息等)。 此外，组织会存储在DAM中可能要经过审核／批准流程的资产。 这样，DAM存储的资产大多具有很高的杠杆利用机会，并避免存储闲置资产。

存储资产还需要考虑技术和资源利用方面的考虑因素。 DAM围绕存储的资产提供其他服务，包括提取元数据、版本控制、生成预览/转码、管理引用和添加访问控制信息。 这些服务会消耗更多的时间和基础架构资源。

通常，存储所有资产和更新是不可取的。 例如，如果对特定资产的更新质量不佳，并且会消耗大量资源，则资产可能不会存储在DAM中。

#### 资产存储在DAM中时 {#when-assets-are-stored-in-dam}

创意团队（和组织）通常对在资产生命周期的每个阶段存储资产不感兴趣。 例如，在以下情况下，它们会避免存储资产：

* 尚未完成或有待试验的资产
* 未能通过创意／内部团队审阅周期的资源
* 与相关资产相比，团队有更好的候选人来向外部团队展示其工作

通常，以下类资产存储在DAM中：

* 达到一定期限且被视为可共享的资产
* 创意团队预先选择的资源
* 根据特定合同或协议（例如，从RAW文件转换的JPG文件、从PSD原始文件转换的TIFF/图像），市场营销可使用或请求的特定资产格式

#### 资产更新存储在DAM中时 {#when-updates-to-assets-are-stored-in-dam}

通常，只应将与更广泛的DAM用户集相关的资产更新存储在DAM中。 它确保用户（营销和类似功能）只能在DAM资产时间轴中看到相关版本。

通常与资产生命周期中的重大里程碑相关的更改。 例如，创意团队提供的初始营销就绪资产或基于请求／审阅的正式更新应存储在DAM中并进行版本控制。

创意团队在请求更改DAM中现有资产后进行更新以供营销团队审阅，这是相关更新的示例。 它应存储在DAM中并进行版本控制，以便进一步参考或还原到先前版本。

以下是通常不相关的更新示例：

* 上传资产的早期版本，在准备好进行营销审阅之前
* 在创作和营销团队确定资产已准备就绪之前，在进行中工作阶段经常对资产进行创意更改

### 用户访问DAM {#user-access-to-dam}

AEM资产根据用户对AEM资产部署的访问权限支持两种类型的用户。 通常，企业网络（防火墙）内的用户可以直接访问DAM。 企业网络之外的其他用户将无法直接访问。 用户类型决定从技术角度可以使用哪些集成。

#### 直接访问DAM的创意用户 {#creative-users-with-direct-access-to-dam}

通常，已加载到内部网络的内部创意团队或代理／创意专业人士有权访问DAM实例，包括AEM登录名。 可以设置AEM和网络基础架构，以允许直接访问外部方（通常是受信任的组织，如为客户端工作的机构），从而通过网络（例如，通过VPN或IP白名单）访问AEM。

在这种情况下，Adobe Asset Link或AEM桌面应用程序可让您轻松访问最终／批准的资产，并允许您将创意就绪型资产保存到DAM。

#### 无权访问DAM的创意用户 {#creative-users-without-access-to-dam}

没有直接访问DAM实例的外部机构和自由职业者可能需要访问已批准的资产或希望将其新设计添加到DAM。

使用以下策略提供对最终／批准资产的访问：

* 如果资产链接不起作用，请使用桌面应用程序。
* 使用 [AEM Assets Brand](https://helpx.adobe.com/cn/experience-manager/brand-portal/user-guide.html) Portal将资产安全分发给外部合作伙伴
* 使用基于资源共享的分发和采购门户的自 [定义实现](https://adobe-marketing-cloud.github.io/asset-share-commons/)
* 使用在AEM中设置的访问控制和必要的网络基础架构（例如，VPN和IP白名单），使外部方能够访问DAM中的专用内容区域。 他们可以使用AEM Web UI获取资产并将新内容上传到您的DAM。

#### 正在从AEM处理资产 {#work-in-progress-on-assets-from-aem}

如本文档所述，建议对资产（有时称为进行中的工作）进行重要更新，而不要将保存到本地文件的所有编辑也作为更改上传到AEM。 这可加快桌面用户的工作速度、限制网络带宽的使用，并使资源时间线保持整洁，并将精力集中在受控的重要更新上。

Adobe Asset Link优惠对此用例提供良好支持：

* 当Photoshop、InDesign或Illustrator中的用户想要编辑文件时，他们会对给定资源执行签出操作
* 资产后台下载，通过Creative Cloud桌面应用程序将其同步到磁盘的用户放入Creative Cloud帐户，并在资产的AEM中切换注销标志，以最大限度地减少编辑冲突
* 从此，用户在同步位置本地存储的文件中工作，并可以继续工作并以任何所需频率保存必要的更改
* 此外，由于资产位于Creative Cloud帐户中，因此也可在用户可能拥有的其他设备上使用（例如，可在专用的Creative Cloud移动应用程序中打开或编辑），并可与其他Creative Cloud用户共享以进行协作。
* 创意用户完成更改后，可在其Creative Cloud应用程序中对该文件执行签入操作，并添加可选注释。 AEM中的相应资产已进行版本控制，并已使用新的二进制文件进行更新。 AEM用户（如营销人员或LOB用户）可通过AEM资产时间轴UI访问重大资产更改或里程碑。

AEM桌面应用程序为在本机应用程序中打开的资产提供网络共享。 默认情况下，在短暂的一段时间后，在本地完成的所有更改将自动上传到AEM。 通过这种配置，在进行中的工作阶段中频繁保存的内容将全部上传到AEM并进行版本控制，从而产生大量网络流量和潜在的可扩展性挑战——更不用说AEM中不必要的版本了。

此处建议的方法是使用AEM桌面应用程序中的选项关闭自动更新，并利用应用程序的资产状态UI中的上传更改操作，手动将资产更改上传到AEM。

#### 批量上传到DAM {#bulk-upload-to-dam}

在某些情况下，您可能需要同时将大量文件上传到DAM，例如：

* 上传照片拍摄或较大项目的结果
* 上传创意机构提供的资产
* 如果在DAM之外完成选择，则从较大的集上传选定资产

请注意，此描述是指将文件作为桌面用户工作流程的常规部分进行操作（例如，每周或每张照片）上传。 此处未涵盖大型资产迁移。

您可以利用以下上传功能：

* 要批量上传大型／分层文件夹，请使用提供文件夹上传功能的AEM [桌面应用](https://helpx.adobe.com/experience-manager/desktop-app/aem-desktop-app.html#bulkupload) 程序。 您还可以上传分层文件夹结构。 资源在后台上传，因此不会绑定到Web浏览器会话
* 要从单个文件夹上传几个文件，请直接将文件拖动到Web界面，或使用AEM Assets Web界面中的创建选项。
* 根据您的业务要求，您还可以使用自定义上传程序。

#### 直接从桌面管理数字资产 {#managing-digital-assets-directly-from-desktop}

如果您使用网络文件共享管理数字资产，则仅使用AEM桌面应用程序映射的网络共享可被视为便捷的替代方式。 从网络文件共享转换时，AEM Web界面提供一组丰富的数字资产管理功能，这些功能远远超出了网络共享(搜索、集合、元数据、协作、预览等)的可能，而AEM桌面应用程序提供一个用于将服务器端DAM存储库与桌面工作连接的便捷链接。

避免使用AEM桌面应用程序直接在AEM资产的网络共享中管理资产。 例如，避免使用AEM桌面应用程序移动／复制多个文件。 请改用AEM Assets Web UI将文件夹从Finder/Explorer拖动到网络共享，或使用AEM Assets文件夹上传功能。

<!-- 
#### Asset migration {#asset-migration}

To plan and execute asset migrations from existing system to a new system or migration of large volume of assets stored on servers, see the [Migration Guide](/help/assets/assets-migration-guide.md). AEM desktop app and AEM to Creative Cloud integrations do not support such migrations. Due to the large volumes of assets to be ingested, and additional requirements around metadata mapping, transformation, and ingestion, migrations should be handled using different tools and approaches.
-->
