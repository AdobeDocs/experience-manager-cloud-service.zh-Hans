---
title: 具有OpenAPI功能的Dynamic Media常见问题解答
description: 具有OpenAPI功能的Dynamic Media常见问题解答
role: User
source-git-commit: 540aa876ba7ea54b7ef4324634f6c5e220ad19d3
workflow-type: tm+mt
source-wordcount: '1495'
ht-degree: 0%

---

# 具有OpenAPI功能的Dynamic Media常见问题解答 {#new-dynaminc-media-apis-frequently-asked-questions}

+++**使用具有OpenAPI功能的Experience Manager Assetsas a Cloud Service存储库中，是否所有资源都可供搜索和交付Dynamic Media？**

否，仅限 [已批准和最新版本的资产](/help/assets/approve-assets.md) 可用于使用具有OpenAPI功能的Dynamic Media进行搜索和交付，从而确保跨所有渠道和应用程序的品牌一致性。

+++

+++**管理员如何将添加到文件夹的新资源和现有资源标记为已批准？**

Experience Manager Assets中资源的状态受约束 `jcr:content/metadata/dam:status` 属性。 此属性的值可以是：

* 已批准

* 已拒绝

* 已请求更改

Experience Manager Assets使用资源信息卡上提供的已批准图标来区分已批准状态，如下面的管理员视图和资源视图图像所示：

**管理员视图**

![在“管理员”视图中批准的资产](/help/assets/assets/approved-assets-thumbs-up.png)

**Assets视图**

![Assets视图中的已批准资源](/help/assets/assets/approved-assets-thumbs-up-assets-view.png)


要批准文件夹中的所有资产，请参阅以下说明： [如何批量批准文件夹中的资产](/help/assets/approve-assets.md#bulk-approve-assets). 还有一个视频描述了整个过程。

在设置文件夹以进行批量审批后，会自动批准添加到该文件夹的所有新资产。 重新处理资产后，将批准所有现有资产。 请参阅 [重新处理数字资产](/help/assets/reprocessing.md) 以获取有关如何重新处理资产的说明。 如果您从任何其他文件夹复制或移动未批准的资产，则需要 [重新处理资产](/help/assets/reprocessing.md).

资产已标记为 `Rejected`，如果管理员指定 `Rejected` 或 `Changes requested` 值。 Experience Manager Assets使用区分已拒绝状态 ![拒绝Assets](/help/assets/assets/do-not-localize/reject-assets.svg) 在“管理员”视图的资产卡上可用。

同样，Experience Manager Assets会使用资源信息卡上的以下已拒绝状态来区分Assets视图中的已拒绝状态：

![在Assets视图中拒绝的资源](/help/assets/assets/rejected-assets-admin-view.png)


+++

+++**如何获取Adobe IMS(AdobeIdentity Management服务)用户或组ID，以便在“Experience Manager管理员”视图中设置资源的角色，进而保护交付和搜索体验？**

需要访问Experience Manager创作环境的用户在AdobeAdmin Console中作为Adobe IMS用户进行管理。 有关什么是Adobe IMS用户以及如何在Admin Console中访问和管理这些用户的信息，请参阅 [Adobe IMS用户](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/adobe-ims-users.html?lang=en).

+++

+++**能否在一个文件夹中同时批准多个资产？**

是，您可以同时批准一个文件夹中的多个资源。

执行以下步骤以同时审批多个资产 [!DNL Experience Manager Assets Admin view]：

1. 选择资产并单击 **[!UICONTROL 属性]**.
1. 在 **[!UICONTROL 基本]** 选项卡，向下滚动到 **[!UICONTROL 审核状态]**.
1. 将审核状态更改为 **[!UICONTROL 已批准]**.
1. 单击“**[!UICONTROL 保存并关闭]**”。

同样，要在Assets视图的文件夹中同时批准多个资源，请执行以下操作：

1. 选择资产并单击 **[!UICONTROL 批量元数据编辑]**.

1. 选择 **[!UICONTROL 已批准]** 在 **[!UICONTROL 状态]** 中的可用字段 [!UICONTROL 属性] 区段。

1. 单击&#x200B;**[!UICONTROL 保存]**。


+++

+++**如何保护资源交付和Dynamic Media OpenAPI搜索安全？**

Experience Manager中的中央资产治理允许DAM管理员或Brand Manager管理对资产的访问。 他们可以通过配置角色或在创作端为批准的资源设置激活和停用时间(特别是在AEM as a Cloud Service创作实例上)来限制访问。

搜索或利用投放URL的最终用户在成功通过授权流程后，可以获得对受限制资产的访问权限。

有关更多信息，请参阅 [限制对Experience Manager中资源的访问](restrict-assets-delivery.md#authoring).

+++

+++**您如何获得权限以编辑资源的审批状态？**

作为DAM用户，您可能没有 [批准资源](approve-assets.md#approve-assets). 要获得编辑资源的批准状态的权限，管理员可以编辑应用于资源文件夹的默认或任何其他元数据架构，从而提供对的编辑权限 **[!UICONTROL 审核状态]** 字段。 有关更多信息，请参阅 [如何禁用对审阅状态的编辑](approve-assets.md#configuration) 字段。

+++

+++**具有OpenAPI功能的Dynamic Media与Dynamic Media解决方案有何不同？**

具有OpenAPI功能的Dynamic Media和Dynamic Media分别代表不同的解决方案，每个解决方案都提供其专业化的交付功能。 必须彻底审查您的特定要求，以确定符合您需求的最合适的解决方案。

Adobe的一般指导是将带有OpenAPI栈栈的Dynamic Media用于任何集成用例（第一方或第三方应用程序）。 如果已存在与Dynamic Media栈栈的集成，则建议不要更改该集成，因为OpenAPI栈栈URL的结构不同。 仅对于任何全新的集成用例，利用OpenAPI栈栈。 如果您的用例需要在OpenAPI栈栈中不可用的高级修饰符，请避免OpenAPI栈栈，直到Adobe弥合这一差距。 即使从AEM AssetsCloud Service进行基本的本机交付，也可以评估OpenAPI栈栈，前提是您的用例包含OpenAPI栈栈提供的修饰符。 总之，根据用例的性质，Dynamic Media和带有OpenAPI栈栈的Dynamic Media可以共存。

以下是具有OpenAPI功能的Dynamic Media与Dynamic Media之间的一些主要区别：

| 具有OpenAPI功能的Dynamic Media | Dynamic Media |
|---|---|
| [仅适用于Assetsas a Cloud Service](/help/assets/dynamic-media-open-apis-overview.md#prerequisites-dynaminc-media-open-apis) | 内部部署或AdobeManaged Services中也有提供，其中包含其他配置和配置步骤。 |
| [受支持的图像修饰符集的限制，例如宽度、高度、旋转、翻转、质量和格式](/help/assets/deliver-assets-apis.md) | 丰富的可用图像修饰符集 |
| [基于用户、角色、日期和时间的受限资产投放](/help/assets/restrict-assets-delivery.md) | 发布到Dynamic Media的Assets可供所有用户访问 |
| 大多数开发人员熟悉OpenAPI规范。 通过使用，AEM Assets的可扩展性变得非常简单 [微型前端资产选择器](/help/assets/asset-selector.md). | 基于SOAP的API，在开发集成自定义时会遇到障碍。 |
| 对DAM中的已批准资产所做的任何更改（包括版本更新和元数据修改）都会自动反映在投放URL中。 由于通过CDN为Dynamic Media的OpenAPI功能配置了10分钟的短生存时间(TTL)值，因此，在10分钟之内即可看到所有创作和发布界面的更新。 | 建议的CDN TTL为10小时。 您可以使用缓存失效操作覆盖TTL值。 |
| 只有已获批准的资产可用于将资产交付到下游应用程序，从而在数字体验中启用品牌批准的资产。 | 对Dynamic Media发布资产的任何更新无需任何审批工作流即可自动发布，这无法确保在数字体验中拥有品牌批准的资产。 |
| 使用情况报表基于交付的资产数量。 此功能即将推出。 | 使用情况报告不可用。 此功能即将推出。 |
| 在Assetsas a Cloud Service存储库中标记为已过期的Assets不再可用于下游应用程序。 | 没有固有资产到期。 在从AEM as a Cloud Service存储库中删除资产之前，该资产将一直保持公共状态。 |
| 不支持图像预设和视频智能裁剪功能。 | 支持图像预设和视频智能裁剪功能。 |
| 动态视频编码，确保根据输入视频提供最佳编码。 无需进行设置即可进行本机视频交付。 | 无论输入视频如何，标准3都会进行编码（可能影响视频交付性能）。 您需要为不同的视频比特率手动设置不同的编码。 |
| 很难猜测基于资产UID的URL（启用URL模糊处理），但SEO已优化。 | URL模糊处理仅可用于URL查询参数。 URL中的Assets ID（资源名称）是可识别的。 |

+++

+++**具有OpenAPI功能的Dynamic Media如何解决连接的Assets功能的限制？**

下表概述了两种解决方案之间的主要区别：

| 具有OpenAPI功能的Dynamic Media | 连接的资源 |
|---|---|
| 远程DAM部署中的Assets在AEM as a Cloud Service上可用。 | 远程DAM部署上的Assets可在AEM as a Cloud Service或AdobeManaged Services上使用。 |
| 当远程DAM部署中的资源在AEM Sites实例中可用时，不会复制资源二进制文件。 | 当远程DAM部署中的资源在AEM Sites实例上可用时，将会复制资源二进制文件。 |
| 支持AEM Assets支持的所有资源格式类型。 | 不支持视频。 |
| 从远程DAM部署获取资产时，您可以在本地Sites部署上使用Dynamic Media 。 | 本地Sites部署上的Dynamic Media为只读。 |
| 对连接到远程DAM部署的AEM Sites实例的数量没有限制。 您可以 [通过配置角色限制对站点实例上资源的访问](/help/assets/restrict-assets-delivery.md) 远程DAM上已批准的资产。 | 限制最多可将4个AEM Sites实例连接到远程DAM部署。 增加的测试次数需要额外的测试。 |
| 资产选择器和带OpenAPI功能的Dynamic Media都可以扩展，以允许自定义集成。 | 连接的Assets API不可扩展，无法允许自定义集成。 |
| 对远程DAM部署中可用的已批准资产所做的任何更改（包括版本更新和元数据修改）都会在10分钟的短生存时间(TTL)值内自动反映在Sites实例上。 | 远程DAM部署的资源更新通过生命周期事件自动处理，但与具有OpenAPI功能的Dynamic Media相比，需要的时间要长得多。 |
| 远程DAM上的资源元数据在AEM Sites实例上也可用。 | 远程DAM上的资源元数据在AEM Sites实例上不可用。 |

+++



