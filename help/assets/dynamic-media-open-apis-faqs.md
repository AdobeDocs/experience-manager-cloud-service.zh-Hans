---
title: 具有 OpenAPI 功能的 Dynamic Media 常见问题解答
description: 具有 OpenAPI 功能的 Dynamic Media 常见问题解答
role: User
exl-id: 3450e050-4b0b-4184-8e71-5e667d9ca721
source-git-commit: ed7331647ea2227e6047e42e21444b743ee5ce6d
workflow-type: tm+mt
source-wordcount: '1546'
ht-degree: 97%

---

# 具有 OpenAPI 功能的 Dynamic Media 常见问题解答 {#new-dynaminc-media-apis-frequently-asked-questions}

| [搜索最佳实践](/help/assets/search-best-practices.md) | [元数据最佳实践](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | [具有 OpenAPI 功能的 Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets 开发人员文档](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

>[!AVAILABILITY]
>
>Dynamic Media with OpenAPI功能指南现在以PDF格式提供。 下载整个指南，并使用Adobe Acrobat AI Assistant来回答您的疑问。
>
>[!BADGE 具有OpenAPI功能的Dynamic Media指南PDF]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/dynamic-media-with-openapi-capabilities.pdf"}

+++**在 Experience Manager Assets as a Cloud Service 存储库中的所有资产是否都可以通过具有 OpenAPI 功能的 Dynamic Media 进行搜索和传递？**

否，只有[经过批准的最新版本资产](/help/assets/approve-assets.md)才可通过具备 OpenAPI 功能的 Dynamic Media 进行搜索和传递，以确保所有渠道和应用程序中的品牌一致性。

+++

+++**管理员如何将添加到文件夹中的新资产和现有资产标记为已批准？**

Experience Manager Assets 中资产状态由 `jcr:content/metadata/dam:status` 属性控制。此属性的值可以是：

* 已批准

* 已拒绝

* 请求的更改

Experience Manager Assets 通过资产卡片上的已批准图标来区分“已批准”状态，如下列出的管理员视图和资产视图的图像所示：

**管理员视图**

![管理员视图中的已批准资产](/help/assets/assets/approved-assets-thumbs-up.png)

**资产视图**

![资产视图中的已批准资产](/help/assets/assets/approved-assets-thumbs-up-assets-view.png)


要批准文件夹中的所有资产，请参阅有关[如何批量批准文件夹中的资产](/help/assets/approve-assets.md#bulk-approve-assets)的说明。还有一个视频展示了整个过程。

在设置了一个用于批量审批的文件夹后，所有添加到该文件夹的新资产都会自动获得批准。所有现有资产都会在重新处理资产后获得批准。有关如何重新处理资产的说明，请参阅[重新处理数字资产](/help/assets/reprocessing.md)。如果您从任何其他文件夹复制或移动未经批准的资产，您需要[重新处理这些资产](/help/assets/reprocessing.md)。

如果管理员指定了 `Rejected` 或 `Changes requested` 值，则该资产会被标记为 `Rejected`。Experience Manager Assets 使用管理员视图中资产卡片上的![拒绝资产](/help/assets/assets/do-not-localize/reject-assets.svg)来区分“已拒绝”状态。

同样地，Experience Manager Assets 在资产视图中通过使用资产卡片上的下列“已拒绝”状态来区分“已拒绝”状态：

![资产视图中被拒绝的资产](/help/assets/assets/rejected-assets-admin-view.png)


+++

+++**如何获取 Adobe IMS（Adobe 身份管理服务）的用户或组 ID，以便在 Experience Manager 管理员视图中设置资产上的角色，从而确保传递和搜索体验？**

需要访问 Experience Manager 作者环境的用户在 Adobe 的 Admin Console 中作为 Adobe IMS 用户进行管理。关于 Adobe IMS 用户的定义，以及如何在 Admin Console 中访问和管理这些用户，请参见 [Adobe IMS 用户](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-learn/cloud-service/accessing/adobe-ims-users)。

+++

+++**您可以同时批准一个文件夹内的多个资产吗？**

您可以同时批准一个文件夹内的多个资产吗？

执行以下步骤可在 [!DNL Experience Manager Assets Admin view] 中同时批准多个资产：

1. 选择资产并点击&#x200B;**[!UICONTROL 属性]**。
1. 在&#x200B;**[!UICONTROL 基本]**&#x200B;选项卡中，向下滚动到&#x200B;**[!UICONTROL 审核状态]**。
1. 将审核状态更改为&#x200B;**[!UICONTROL 已批准]**。
1. 单击&#x200B;**[!UICONTROL 保存并关闭]**。

同样，要在“资产”视图中同时批准文件夹内的多个资产：

1. 选择资产并点击&#x200B;**[!UICONTROL 批量编辑元数据]**。

1. 在右侧面板的[!UICONTROL 属性]部分，选择&#x200B;**[!UICONTROL 状态]**&#x200B;字段中的&#x200B;**[!UICONTROL 已批准]**。

1. 单击&#x200B;**[!UICONTROL 保存]**。


+++

+++**如何确保资产安全传递，并搜索 Dynamic Media OpenAPI？**

在 Experience Manager 中，中央资产治理允许 DAM 管理员或品牌经理管理对资产的访问。他们可以通过配置角色，或在创作端为已批准的资产设置激活和停用时间来限制访问，特别是在 AEM as a Cloud Service 作者实例中。

成功通过授权流程后，搜索或使用传递 URL 的最终用户可以访问受限资产。

有关更多信息，请参阅[限制对 Experience Manager 中资产的访问](restrict-assets-delivery.md#authoring)。

+++

+++**如何获得编辑资产审批状态的权限？**

作为DAM用户，您可能没有权限[审批资产](approve-assets.md#approve-assets)。要获得编辑资产审批状态的权限，管理员可以编辑应用于资产文件夹的默认或任何其他元数据架构，以提供对&#x200B;**[!UICONTROL 查看状态]**&#x200B;字段的编辑权限。有关更多信息，请参阅[如何禁用对“查看状态”字段的编辑](approve-assets.md#configuration)。

+++

+++**具有 OpenAPI 功能的 Dynamic Media 与 Dynamic Media 解决方案有何不同？**

具有 OpenAPI 功能的 Dynamic Media 和 Dynamic Media 代表了不同的解决方案，每种解决方案都提供了其专门的传递能力。请务必彻底审查您的具体要求，以确定最符合您需求的解决方案。

Adobe 的一般建议是，对于任何集成用例（第一方或第三方应用程序）中，利用带有 OpenAPI 堆栈的 Dynamic Media。如果已经存在与 Dynamic Media 堆栈的集成，则建议不要更改它，因为 OpenAPI 堆栈 URL 的结构有所不同。只有对于任何新的集成用例，才可以利用 OpenAPI 堆栈。如果您的用例需要 OpenAPI 堆栈未提供的高级修饰符，那么在 Adobe 补这一空白之前，请避免使用 OpenAPI 堆栈。即使对于 AEM Assets Cloud Services 的基本原生传递，只要您的用例包含 OpenAPI 堆栈可用的修饰符，就可以对 OpenAPI 堆栈进行评估。总之，根据用例的性质，Dynamic Media 和具有 OpenAPI 堆栈的 Dynamic Media 可以共存。

以下是具有 OpenAPI 功能的 Dynamic Media 与 Dynamic Media 之间的一些主要区别：

| 具有 OpenAPI 功能的 Dynamic Media  | Dynamic Media |
|---|---|
| [仅适用于 Assets as a Cloud Service](/help/assets/dynamic-media-open-apis-overview.md#prerequisites-dynaminc-media-open-apis) | 也可通过内部部署或 Adobe Managed Services 获得，但需要额外的配置和设置步骤。 |
| [支持的图像修改器有限，如宽度、高度、旋转、翻转、质量和格式](/help/assets/deliver-assets-apis.md) | 丰富的可用图像修改器集 |
| [基于用户、角色、日期和时间的受限资产传递](/help/assets/restrict-assets-delivery.md) | 发布到 Dynamic Media 上的资产可供所有用户访问 |
| 大多数开发者都熟悉 OpenAPI 规范。通过使用[微前端资产选择器](/help/assets/overview-asset-selector.md)，AEM Assets 的可扩展性变得非常简单。 | 基于 SOAP 的 API 在开发集成定制时成为了一个障碍。 |
| 在 DAM 中对已批准的资产所做的任何更改，包括版本更新和元数据修改，都会自动反映在传递 URL 中。通过 CDN 为具有 OpenAPI 功能的 Dynamic Media 配置了 10 分钟的短生存时间 (TTL) 值，更新将在 10 分钟内即可在所有创作和发布界面上显示。 | 建议的 CDN TTL 为 10 小时。您可以使用缓存失效操作来覆盖 TTL 值。 |
| 只有经过批准的资产才能用于向下游应用程序传递资产，从而确保在数字体验中使用品牌认可的资产。 | 对 Dynamic Media 已发布的资产所做的任何更新都会自动发布，无需经过任何审批流程，这无法确保数字体验中使用品牌认可的资产。 |
| 基于已传递资产数量的使用情况报告。这项功能即将推出。 | 使用情况报告不可用。这项功能即将推出。 |
| 在 Assets as a Cloud Service 存储库上标记为“过期”的资产不再可供下游应用程序使用。 | 无固有的资产到期。资产在从 AEM as a Cloud Service 存储库中删除之前保持公共状态。 |
| 不支持图像预设和视频智能裁剪功能。 | 支持图像预设和视频智能裁剪功能。 |
| Dynamic Video 编码，确保根据输入视频提供最佳编码。原生视频传递不需要设置。 | 标准 3 编码与输入视频无关（可能会影响视频传递性能）。您需要为不同的视频比特率手动设置不同的编码。 |
| 难以猜测基于资产 UID 的 URL（允许 URL 混淆），但已经过 SEO 优化。 | URL 混淆仅适用于 URL 查询参数。URL 中的资产 ID（资产名称）是可识别的。 |

+++

+++**具有 OpenAPI 功能的 Dynamic Media 如何解决互联资产功能的局限性？**

下表概述了两种解决方案之间的主要区别：

| 具有 OpenAPI 功能的 Dynamic Media  | 连接的资产 |
|---|---|
| 远程 DAM 部署上的资产在 AEM as a Cloud Service 上可用。 | 远程 DAM 部署上的资产在 AEM as a Cloud Service 或 Adobe Managed Services 上可用。 |
| 当远程 DAM 部署上的资产在 AEM Sites 实例中可用时，不会复制资产二进制文件。 | 当远程 DAM 部署上的资产在 AEM Sites 实例上可用时，会复制资产二进制文件。 |
| 支持 AEM Assets 支持的所有资产格式类型。 | 不支持视频。 |
| 在从远程 DAM 部署获取资产时，您可以在本地 Sites 部署上使用 Dynamic Media。 | 本地 Sites 上的 Dynamic Media 部署是只读的。 |
| 对连接到远程 DAM 部署的 AEM Sites 实例的数量没有限制。您可以通过为远程 DAM 上已批准的资产配置角色来[限制对 Sites 实例上资产的访问](/help/assets/restrict-assets-delivery.md)。 | 限制将不超过 4 个 AEM Sites 实例连接到远程 DAM 部署。数量增加需要额外的测试。 |
| 资产选择器和具有 OpenAPI 功能的 Dynamic Media 都是可扩展的，可以进行自定义集成。 | Connected Assets API 不可扩展，因此无法进行自定义集成。 |
| 对远程 DAM 部署上可用的已批准资产所做的任何更改，包括版本更新和元数据修改，都会在10分钟的短生存时间 (TTL) 值内自动反映在 Sites 实例上。 | 远程 DAM 部署上的资产更新是通过生命周期事件自动处理的，但与具有 OpenAPI 功能的 Dynamic Media 相比，需要更多的时间。 |
| 远程 DAM 上的资产元数据在 AEM Sites 实例上也可用。 | 远程 DAM 上的资产元数据在 AEM Sites 实例上不可用。 |

+++
