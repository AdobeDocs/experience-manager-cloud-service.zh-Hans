---
title: 具有OpenAPI功能的Dynamic Media常见问题解答
description: 具有OpenAPI功能的Dynamic Media常见问题解答
role: User
source-git-commit: 0ad9f349c997c35862e4f571b4741ed4c0c947e2
workflow-type: tm+mt
source-wordcount: '1197'
ht-degree: 0%

---

# 具有OpenAPI功能的Dynamic Media常见问题解答 {#new-dynaminc-media-apis-frequently-asked-questions}

+++**Experience Manager Assetsas a Cloud Service存储库中的所有资源是否都可供使用具有OpenAPI功能的Dynamic Media进行搜索和交付？**

不需要，只有[批准的和最新版本的资产](/help/assets/approved-assets.md)可用于使用具有OpenAPI功能的Dynamic Media进行搜索和交付，从而确保所有渠道和应用程序之间的品牌一致性。

+++

+++**管理员如何将添加到文件夹的新资源和现有资源标记为已批准？**

Experience Manager Assets中资源的状态受`jcr:content/metadata/dam:status`属性控制。 此属性的值可以是：

* 已批准

* 已拒绝

* 已请求更改

Experience Manager Assets使用资源信息卡上提供的![批准Assets](assets/thumbs-up-icon.svg)来区分批准状态，如下图所示：

已批准资产的![图标](/help/assets/assets/approved-assets-thumbs-up.png)

要批准文件夹中的所有资源，请参阅[有关如何批量批准文件夹](/help/assets/approved-assets.md#bulk-approve-assets)中的资源的说明。 还有一个视频描述了整个过程。

在设置文件夹以进行批量审批后，会自动批准添加到该文件夹的所有新资产。 重新处理资产后，将批准所有现有资产。 有关如何重新处理资产的说明，请参阅[重新处理数字资产](/help/assets/reprocessing.md)。 如果您从任何其他文件夹复制或移动未批准的资产，则需要[重新处理这些资产](/help/assets/reprocessing.md)。

如果管理员指定`Rejected`或`Changes requested`值，则将该资源标记为`Rejected`。 Experience Manager Assets使用资源信息卡上提供的![拒绝Assets](/help/assets/assets/do-not-localize/reject-assets.svg)来区分已拒绝状态。

+++

+++**如何获取Adobe IMS(AdobeIdentity Management服务)用户或组ID，以便在“Experience Manager管理员”视图中设置资源的角色，从而保护投放和搜索体验？**

需要访问Experience Manager创作环境的用户在AdobeAdmin Console中作为Adobe IMS用户进行管理。 有关什么是Adobe IMS用户以及如何在Admin Console中访问和管理这些用户的信息，请参阅[Adobe IMS用户](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/adobe-ims-users.html?lang=en)。

+++

+++**能否在一个文件夹中同时批准多个资源？**

是，您可以同时批准一个文件夹中的多个资源。

执行以下步骤以在[!DNL Experience Manager Assets]中同时批准多个资源：

1. 选择资产并单击&#x200B;**[!UICONTROL 属性]**。
1. 在&#x200B;**[!UICONTROL 基本]**&#x200B;选项卡中，向下滚动到&#x200B;**[!UICONTROL 审核状态]**。
1. 将审阅状态更改为&#x200B;**[!UICONTROL 已批准]**。
1. 单击“**[!UICONTROL 保存并关闭]**”。

+++

+++**如何保护资源交付并搜索Dynamic Media OpenAPI？**

Experience Manager中的中央资产治理允许DAM管理员或Brand Manager管理对资产的访问。 他们可以通过在创作端(特别是在AEM as a Cloud Service创作实例上)为批准的资源配置角色来限制访问。

搜索或利用投放URL的最终用户在成功通过授权流程后，可以获得对受限制资产的访问权限。

有关详细信息，请参阅[限制对Experience Manager](restrict-assets-delivery.md#authoring)中资源的访问。

+++

+++**如何获取编辑资产审批状态的权限？**

作为DAM用户，您可能没有[批准资产](approved-assets.md#approve-assets)的权限。 要获得编辑资源的审批状态的权限，管理员可以编辑应用于资源文件夹的默认架构或任何其他元数据架构，以提供&#x200B;**[!UICONTROL 审核状态]**&#x200B;字段的编辑权限。 有关详细信息，请参阅[如何禁用对“审阅状态”](approved-assets.md#configuration)字段的编辑。

+++

+++**具有OpenAPI功能的Dynamic Media与Dynamic Media解决方案有何不同？**

具有OpenAPI功能的Dynamic Media和Dynamic Media分别代表不同的解决方案，每个解决方案都提供其专业化的交付功能。 必须彻底审查您的特定要求，以确定符合您需求的最合适的解决方案。

以下是具有OpenAPI功能的Dynamic Media与Dynamic Media之间的一些主要区别：

| 具有OpenAPI功能的Dynamic Media | Dynamic Media |
|---|---|
| [仅适用于Assetsas a Cloud Service](/help/assets/new-dynamic-media-overview.md#prerequisites-new-dynaminc-media-apis) | 内部部署或AdobeManaged Services中也有提供，其中包含其他配置和配置步骤。 |
| [受支持的图像修饰符集有限，例如宽度、高度、旋转、翻转、质量和格式](/help/assets/deliver-assets-apis.md) | 丰富的可用图像修饰符集 |
| [基于用户和角色的受限资源投放](/help/assets/restrict-assets-delivery.md) | 发布到Dynamic Media的Assets可供所有用户访问 |
| 支持图像智能裁剪 | 支持图像和视频智能裁切 |
| 基于OpenAPI规范的栈栈，大多数开发人员都采用这种规范。 通过使用[Micro Frontend Asset Selector](/help/assets/asset-selector.md)，AEM Assets的可扩展性变得非常简单。 | 基于SOAP的API，在开发集成自定义时会遇到障碍。 |
| 对DAM中的已批准资产所做的任何更改（包括版本更新和元数据修改）都会自动反映在投放URL中。 由于通过CDN为Dynamic Media的OpenAPI功能配置了10分钟的短生存时间(TTL)值，因此，在10分钟之内即可看到所有创作和发布界面的更新。 | 建议的CDN TTL为10小时。 您可以使用缓存失效操作覆盖TTL值。 |
| 只有已获批准的资产可用于将资产交付到下游应用程序，从而在数字体验中启用品牌批准的资产。 投放的资源将遵循AEM as a Cloud Service存储库创作实例上的资源到期状态。 | 对Dynamic Media发布资产的任何更新无需任何审批工作流即可自动发布，这无法确保在数字体验中拥有品牌批准的资产。 没有固有资产到期。 在从AEM as a Cloud Service存储库中删除资产之前，该资产将一直保持公共状态。 |
| 使用情况报表基于交付的资产数量。 | 使用情况报告不可用。 |

+++

+++**具有OpenAPI功能的Dynamic Media如何解决连接的Assets功能的限制？**

下表概述了两种解决方案之间的主要区别：

| 具有OpenAPI功能的Dynamic Media | 连接的资源 |
|---|---|
| 远程DAM部署中的Assets在AEM as a Cloud Service上可用。 | 远程DAM部署上的Assets可在AEM as a Cloud Service或AdobeManaged Services上使用。 |
| 当远程DAM部署中的资源在AEM Sites实例中可用时，不会复制资源二进制文件。 | 当远程DAM部署中的资源在AEM Sites实例上可用时，将会复制资源二进制文件。 |
| 支持AEM Assets支持的所有资源格式类型。 | 不支持视频。 |
| 支持图像智能裁剪。 | 支持Dynamic Media图像智能裁剪和图像预设。 |
| 从远程DAM部署获取资产时，您可以在本地Sites部署上使用Dynamic Media 。 | 本地Sites部署上的Dynamic Media为只读。 |
| 对连接到远程DAM部署的AEM Sites实例的数量没有限制。 您可以[通过为远程DAM上的已批准资源配置角色](/help/assets/restrict-assets-delivery.md)，限制对Sites实例上资源的访问。 | 限制最多可将4个AEM Sites实例连接到远程DAM部署。 增加的测试次数需要额外的测试。 |
| 资产选择器和带OpenAPI功能的Dynamic Media都可以扩展，以允许自定义集成。 | 连接的Assets API不可扩展，无法允许自定义集成。 |
| 对远程DAM部署中可用的已批准资产所做的任何更改（包括版本更新和元数据修改）都会在10分钟的短生存时间(TTL)值内自动反映在Sites实例上。 | 远程DAM部署的资源更新通过生命周期事件自动处理，但与具有OpenAPI功能的Dynamic Media相比，需要的时间要长得多。 |
| 远程DAM上的资源元数据在AEM Sites实例上也可用。 | 远程DAM上的资源元数据在AEM Sites实例上不可用。 |

+++



