---
title: Content Hub 常见问题 (FAQ)
description: 获取有关 Content Hub 的一些最常见问题 (FAQ) 的答复。
exl-id: 74b5c308-c1d3-4787-9f1f-f64cf09d298a
source-git-commit: a509cb6b2d6fea0d8c53c570c46b1feef2a15191
workflow-type: ht
source-wordcount: '1113'
ht-degree: 100%

---

# Content Hub 常见问题 {#content-hub-frequently-asked-questions}

| [搜索最佳实践](/help/assets/search-best-practices.md) | [元数据最佳实践](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | [具有 OpenAPI 功能的 Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets 开发人员文档](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

![Content Hub 常见问题](assets/content-hub-faqs.png)

>[!AVAILABILITY]
>
>Content Hub 指南现以 PDF 格式提供。下载完整指南并使用 Adobe Acrobat AI 助手来回答您的疑问。
>
>[!BADGE Content Hub 指南 PDF]{type=Informative url="https://helpx.adobe.com/cn/content/dam/help/en/experience-manager/aem-assets/content-hub.pdf"}

## 什么是 Content Hub？ {#what-is-content-hub}

Content Hub 是 Adobe Experience Manager Assets as a Cloud Service 的一项功能。

Content Hub 使更广泛的团队能够通过直观的门户轻松发现相关的、经过批准的资产，并快速根据他们的需求进行调整。此外，Content Hub 还提供了一种引入机制，允许用户在将资产上传到 DAM 时轻松地进行自助服务。这直接满足了组织对更高内容创建速度的需求，同时保持了品牌一致性并遵守了适当的保障措施。

## 为什么我无法在我的 Cloud Manager 程序/环境上启用 Content Hub？ {#cannot-enable-content-hub}

目前，Content Hub 仅在 AEM Cloud Manager 生产程序中可用，其中包括 Assets 许可证（Assets Cloud Service、Assets Ultimate、Assets Prime）。当您点击 [Content Hub](/help/assets/deploy-content-hub.md#enable-content-hub) 启用它时，它将会被部署，并会与该程序中 AEM 的作者生产环境相关联。有关详细信息和先决条件，请参阅[部署 Content Hub](/help/assets/deploy-content-hub.md)。

## 我在生产程序/环境上启用了 Content Hub，我可以禁用它吗？ {#can-i-disable-content-hub}

在生产程序上启用 Content Hub 会将其部署为生产基础设施的一部分。AEM Cloud Manager 不允许删除或禁用生产基础设施，以最大限度地降低人为错误对生产使用造成的风险。

如果您不想在部署后向用户提供 Content Hub，请不要在 Admin Console 中将任何用户分配给 Content Hub 产品配置文件。请参阅[部署 Content Hub](/help/assets/deploy-content-hub.md#content-hub-instance-product-profile) 了解详情。

## 鉴于 Content Hub 仅适用于生产程序/生产创作环境，我该如何评估我组织中的 Content Hub？ {#how-can-i-evaluate-content-hub}

Content Hub 是 Adobe 提供和维护的一项功能，它没有任何需要通过开发/中继/生产进行典型验证的自定义代码。此外，用户对该功能的访问完全由管理员控制，因此您可以在不向所有用户公开的情况下对其进行评估。

可以在不影响 AEM as a Cloud Service Assets 管理的用户/生产内容的情况下评估 Content Hub。评估程序可能如下所示：

* 在生产环境（Cloud Manager 程序）中[启用 Content Hub](/help/assets/deploy-content-hub.md#enable-content-hub)
* 将生产作者的 [AEM 管理员用户添加](/help/assets/deploy-content-hub.md#onboard-content-hub-administrator)到 Content Hub 产品配置文件中。
* AEM 管理员[配置 Content Hub](/help/assets/configure-content-hub-ui-options.md)
* AEM 生产作者上的 AEM 管理员或 AEM 用户[批准 Content Hub 的多项资产](/help/assets/approve-assets-content-hub.md)；如果您不想更改 DAM 中的任何生产内容，您可能需要在 AEM 作者实例中创建一个单独的评估文件夹，然后将一些资产从 DAM 上传/标记或复制到其中。
* Admin Console 管理员将[一些选定的用户](/help/assets/deploy-content-hub.md#onboard-content-hub-users)添加到 Content Hub 产品配置文件，以便他们可以开始评估。
* 评估完成后，作者实例中的 AEM 用户可以移除测试资产的审批，批准 Content Hub 的生产资产，然后 Admin Console 管理员可以添加所有需要访问 Content Hub 和批准内容的用户。恭喜，您的 Content Hub 现已上线。

在沙盒程序及其作者生产环境中，有一个早期访问 Content Hub 的计划。请参阅[沙盒程序简介](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md)，了解更多详细信息。若要了解详情有关早期访问计划的更多信息，请联系您的 Adobe 帐户团队。

目前，Content Hub 尚不适用于非生产环境（阶段和开发）。Assets Ultimate 的阶段/开发环境预计将于 2025 年 3 月可用。

## 为什么登录 Content Hub 后我看不到任何资产？ {#no-assets-in-content-hub}

在 Assets as a Cloud Service 中标记为已批准的资产将自动在 Content Hub 中可用。如果登录 Content Hub 后看不到任何资产，请使用 AEM as a Cloud Service 作者环境批准资产，以使其在 Content Hub 中可用。如需了解更多信息，请参阅[批准 Content Hub 的资产](/help/assets/approve-assets-content-hub.md)。

## 为什么我看不到使用 Content Hub 直接上传的资产或者使用 Content Hub 从 Dropbox 或 OneDrive 帐户导入的资产？ {#no-assets-uploaded-from-content-hub}

使用 Content Hub 上传的资产是否显示取决于您是否启用了“配置”用户界面上的[自动审批](/help/assets/configure-content-hub-ui-options.md#configure-import-options-content-hub)切换按钮：

* 如果启用了&#x200B;**自动审批**&#x200B;切换按钮，您使用 Content Hub 上传的资产将自动可用。

* 如果禁用&#x200B;**自动审批**&#x200B;切换，则您使用 Content Hub 上传的资产不会自动显示。这些资产可在 Assets as a Cloud Service 环境的 `hydrated-assets` 文件夹中找到。导航到该文件夹并将这些资产的状态[批量编辑](/help/assets/approve-assets-content-hub.md)为 `Approved`，以使这些资产在 Content Hub 中显示。

## 如何在 AEM as a Cloud Service 环境中快速查找使用 Content Hub 上传的资产？ {#find-uploaded-assets-on-aem-cloud}

您可以通过以下方式在 AEM as a Cloud Service 环境中快速找到使用 Content Hub 上传的资产：

1. 导航到 `hydrated-assets` 文件夹。

1. 点击&#x200B;**[!UICONTROL 筛选条件]**&#x200B;并在&#x200B;**[!UICONTROL 资产状态]**&#x200B;字段中设置&#x200B;**[!UICONTROL 无状态]**。

1. 使用&#x200B;**[!UICONTROL 修改日期]**&#x200B;字段对资产进行排序。

## 为什么我不使用资产信息卡上的 Adobe Express 选项查看编辑，以便能够重新混合资产以创建新的变体？ {#edit-using-express-not-available}

要查看资产信息卡上使用 Adobe Express 选项进行的编辑，您除了必须拥有 [Content Hub 用户的权限（有权将资产重新混合为新变体](#onboard-content-hub-users-add-assets)）之外，还必须拥有 Adobe Express 权限。Adobe Express 必须与 Adobe Experience Manager 部署在 Adobe Admin Console 中的同一组织中。

## 我可以设置 Content Hub，以便我的组织的品牌指南显示为主页上的关联吗？ {#content-hub-setup-brand-guidelines}

除了 Content Hub 主页上标准的“所有资产”、“收藏集“和”洞察“选项卡外，您还可以将自定义链接添加为单独的选项卡。有关如何设置的信息，请参阅[自定义关联](/help/assets/configure-content-hub-ui-options.md#configure-custom-links-content-hub)。

## 是否有将现有 Brand Portal 客户迁移至 Content Hub 的计划？ {#migration-brand-portal}

Adobe 提供从 Brand Portal 到 Content Hub 的迁移支持，您可以通过创建 Adobe 支持工单来使用该支持服务。

## 为什么我在 Content Hub 看不到产品设置/配置选项？ {#ui-configuration-option-missing}

要访问[配置用户界面](/help/assets/configure-content-hub-ui-options.md)，您需要成为 [Content Hub 管理员](/help/assets/deploy-content-hub.md##onboard-content-hub-administrator)。如果您在 Adobe Admin Console 中的生产作者实例中被分配到 AEM 管理员产品配置文件，但仍然看不到配置选项，请确保 AEM 管理员产品配置文件未重命名。有关更多详细信息，请参阅 [AEM as a Cloud Service 团队和产品配置文件](/help/onboarding/aem-cs-team-product-profiles.md)。
