---
title: Content Hub常见问题解答(FAQ)
description: 获取对Content Hub的一些最常见问题(FAQ)的响应。
exl-id: 74b5c308-c1d3-4787-9f1f-f64cf09d298a
source-git-commit: ed7331647ea2227e6047e42e21444b743ee5ce6d
workflow-type: tm+mt
source-wordcount: '1128'
ht-degree: 1%

---

# Content Hub常见问题解答 {#content-hub-frequently-asked-questions}

| [搜索最佳实践](/help/assets/search-best-practices.md) | [元数据最佳实践](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | [具有 OpenAPI 功能的 Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets 开发人员文档](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

![Content Hub常见问题解答](assets/content-hub-faqs.png)

>[!AVAILABILITY]
>
>Content Hub指南现在提供了PDF格式。 下载整个指南，并使用Adobe Acrobat AI Assistant来回答您的疑问。
>
>[!BADGE Content Hub指南PDF]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/content-hub.pdf"}

## 什么是Content Hub？ {#what-is-content-hub}

Content Hub是Adobe Experience Manager Assetsas a Cloud Service的一项功能。

Content Hub使范围更广的团队能够通过直观的门户轻松发现相关的已批准资源，并快速调整这些资源以符合其需求。  此外，Content Hub提供了一个摄取机制，允许这些用户在将资源上传到DAM时轻松实现自助服务。 这直接满足了企业提高内容创建速度的需要，同时通过适当的保护机制来保持品牌一致性和法规遵从性。

## 为何无法在Cloud Manager项目/环境中启用Content Hub？ {#cannot-enable-content-hub}

目前，Content Hub仅在AEM Cloud Manager生产程序上可用，其中包括Assets许可证。 当您单击[Content Hub](/help/assets/deploy-content-hub.md#enable-content-hub)以启用它时，将部署它并与AEM在该程序中的创作生产环境相关联。 有关详细信息和先决条件，请参阅[部署Content Hub](/help/assets/deploy-content-hub.md)。

有一个程序可以提前访问沙盒程序/创作生产环境上的Content Hub 。 有关详细信息，请参阅[沙盒程序简介](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md)。 要了解有关抢先体验计划的更多信息，请联系您的Adobe客户团队。

在此阶段，Content Hub不适用于非生产环境（暂存、开发等）。

## 我在生产程序/环境中启用了Content Hub，可以禁用它吗？ {#can-i-disable-content-hub}

在生产程序上启用Content Hub会将其部署为生产基础架构的一部分。 AEM Cloud Manager不允许删除或禁用生产基础架构，从而最大限度地降低因人为错误导致的生产使用风险。

如果您不想在部署Content Hub后将其提供给用户，则不要在Admin Console中将任何用户分配给Content Hub产品配置文件。 有关详细信息，请参阅[部署Content Hub](/help/assets/deploy-content-hub.md#content-hub-instance-product-profile)。

## 如何在我的组织中评估Content Hub（因为它仅适用于生产程序/生产创作环境）？ {#how-can-i-evaluate-content-hub}

Content Hub是Adobe提供和维护的一项功能，它没有任何需要通过dev/stage/production进行典型验证的自定义代码。 此外，用户的功能访问权限完全由管理员控制，因此您可以评估该功能而无需将其公开给所有用户。

您可以评估Content Hub，而不会影响您在AEM as a Cloud Service Assets中管理的用户/生产内容。 评估过程可能如下所示：

* 在生产环境中[启用Content Hub](/help/assets/deploy-content-hub.md#enable-content-hub) (Cloud Manager程序)
* [将生产作者中的AEM管理员用户](/help/assets/deploy-content-hub.md#onboard-content-hub-administrator)添加到Content Hub产品配置文件。
* AEM管理员[配置Content Hub](/help/assets/configure-content-hub-ui-options.md)
* AEM管理员或AEM生产作者上的AEM用户批准了Content Hub](/help/assets/approve-assets-content-hub.md)的大量资源；如果您不想更改DAM中的任何生产内容，则可能需要在AEM创作实例中创建单独的评估文件夹，然后上传/标记或将DAM中的某些资源复制到其中。[
* Admin Console管理员将[一些选定的用户](/help/assets/deploy-content-hub.md#onboard-content-hub-users)添加到Content Hub产品配置文件，以便他们可以开始评估。
* 评估完成后，创作实例中的AEM用户可以删除测试资源中的批准项，批准Content Hub的生产资源，然后Admin Console管理员可以添加所有需要访问Content Hub和批准内容的用户。 恭喜，您的Content Hub现已上线。

Adobe还提供对暂存环境上的Content Hub的抢先访问程序 — 请参阅问题[为什么我无法在Cloud Manager程序/环境中启用Content Hub？](#cannot-enable-content-hub)以了解详细信息。

## 为什么在登录到Content Hub后看不到任何资源？ {#no-assets-in-content-hub}

在Assetsas a Cloud Service中标记为已批准的资源可在Content Hub中自动使用。 如果您在登录到Content Hub后看不到任何资源，请使用AEM as a Cloud Service创作环境批准资源，以便在Content Hub中可用。 有关详细信息，请参阅[批准Content Hub的资源](/help/assets/approve-assets-content-hub.md)。

## 为何看不到我使用Content Hub直接上传或使用Content Hub从Dropbox或OneDrive帐户导入的资源呢？ {#no-assets-uploaded-from-content-hub}

是否显示使用Content Hub上传的资源，取决于您是否在“配置”用户界面中启用了[自动审批](/help/assets/configure-content-hub-ui-options.md#configure-import-options-content-hub)切换开关：

* 如果启用了&#x200B;**自动审批**&#x200B;切换，则使用Content Hub上传的资源会自动可用。

* 如果禁用了&#x200B;**自动审批**&#x200B;切换功能，则使用Content Hub上传的资源不会自动显示。 这些资源位于Assetsas a Cloud Service环境的`hydrated-assets`文件夹中。 导航到文件夹，然后[批量编辑](/help/assets/approve-assets-content-hub.md)这些资源的状态并更改为`Approved`，以便这些资源显示在Content Hub中。

## 如何在AEM as a Cloud Service环境中快速查找使用Content Hub上传的资源？ {#find-uploaded-assets-on-aem-cloud}

您可以通过以下方式在AEM as a Cloud Service环境中快速找到使用Content Hub上传的资源：

1. 导航到`hydrated-assets`文件夹。

1. 单击&#x200B;**[!UICONTROL 筛选器]**&#x200B;并在&#x200B;**[!UICONTROL 资产状态]**&#x200B;字段中设置&#x200B;**[!UICONTROL 无状态]**。

1. 使用&#x200B;**[!UICONTROL 修改日期]**&#x200B;字段对资源排序。

## 为何无法在资源卡上查看使用Adobe Express编辑选项以混合资源以创建新变体？ {#edit-using-express-not-available}

要查看资源信息卡上的使用Adobe Express编辑选项，除了拥有[Content HubAdobe Express的权限之外，您还必须拥有将资源重新混合到新变体](#onboard-content-hub-users-add-assets)的权限。 Adobe Express必须在部署Adobe Experience Manager的AdobeAdmin Console的同一组织中部署。

## 我是否可以设置Content Hub，以便我的组织的品牌准则在主页中显示为链接？ {#content-hub-setup-brand-guidelines}

除了Content Hub主页上的标准“所有Assets”、“收藏集”和“分析”选项卡之外，您还可以将自定义链接添加为单独的选项卡。 有关如何设置的信息，请参阅[自定义链接](/help/assets/configure-content-hub-ui-options.md#configure-custom-links-content-hub)。

## 是否制定了将现有Brand Portal客户迁移到Content Hub的计划？ {#migration-brand-portal}

Adobe提供从Brand Portal到Content Hub的迁移支持，您可以通过创建Adobe支持票证来使用这些支持。

## 为什么在Content Hub中看不到产品设置/配置选项？ {#ui-configuration-option-missing}

若要访问[配置用户界面](/help/assets/configure-content-hub-ui-options.md)，您需要是[Content Hub管理员](/help/assets/deploy-content-hub.md##onboard-content-hub-administrator)。 如果您已被分配给Adobe Admin Console生产创作实例上的AEM管理员产品配置文件，并且您仍然看不到配置选项，请确保未重命名AEM管理员产品配置文件。 有关更多详细信息，请参阅[AEM as a Cloud Service团队和产品配置文件](/help/onboarding/aem-cs-team-product-profiles.md)。
