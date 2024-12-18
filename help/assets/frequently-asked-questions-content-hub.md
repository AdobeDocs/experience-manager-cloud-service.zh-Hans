---
title: Content Hub 常见问题 (FAQ)
description: 获取 Content Hub 一些最常见问题 (FAQ) 的答复。
exl-id: 74b5c308-c1d3-4787-9f1f-f64cf09d298a
source-git-commit: a509cb6b2d6fea0d8c53c570c46b1feef2a15191
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Content Hub 常见问题解答 {#content-hub-frequently-asked-questions}

| [搜索最佳实践](/help/assets/search-best-practices.md) | [元数据最佳实践](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | [具有 OpenAPI 功能的 Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets 开发人员文档](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

![Content Hub 常见问题解答](assets/content-hub-faqs.png)

>[!AVAILABILITY]
>
>Content Hub指南现在提供了PDF格式。 下载整个指南，并使用Adobe Acrobat AI Assistant来回答您的疑问。
>
>[!BADGE Content Hub指南PDF]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/content-hub.pdf"}

## 什么是 Content Hub？ {#what-is-content-hub}

Content Hub 是 Adobe Experience Manager Assets as a Cloud Service 的一项功能。

Content Hub 使更广泛的团队能够通过直观的门户轻松发现相关的、批准的资产，并快速根据他们的需求进行调整。此外，Content Hub 还提供了一种提取机制，允许用户在将资产上传到 DAM 时轻松地进行自助服务。这直接满足了组织对更高内容创建速度的需求，同时保持了品牌一致性并遵守了适当的保障措施。

## 为什么我无法在我的 Cloud Manager 程序/环境上启用 Content Hub？ {#cannot-enable-content-hub}

目前，Content Hub仅适用于AEM Cloud Manager生产程序，其中包括Assets许可证(AssetsCloud Service、Assets Ultimate、Assets Prime)。 当您点击 [Content Hub](/help/assets/deploy-content-hub.md#enable-content-hub) 为了启用它，它将被部署并与该程序中 AEM 的作者生产环境相关联。看 [部署 Content Hub](/help/assets/deploy-content-hub.md) 了解详细信息和先决条件。

## 我在生产程序/环境上启用了 Content Hub，我可以禁用它吗？ {#can-i-disable-content-hub}

在生产程序上启用 Content Hub 会将其部署为生产基础设施的一部分。AEM Cloud Manager 不允许删除或禁用生产基础设施，以最大限度地降低人为错误对生产使用造成的风险。

如果您不想在部署后向用户提供 Content Hub，请不要在 Admin Console 将任何用户分配给 Content Hub 产品轮廓。看 [部署 Content Hub](/help/assets/deploy-content-hub.md#content-hub-instance-product-profile) 了解详情。

## 鉴于 Content Hub 仅适用于生产程序/生产创作环境，我该如何评估我组织中的 Content Hub？ {#how-can-i-evaluate-content-hub}

Content Hub 是 Adobe 提供和维护的一项功能，它没有任何需要通过 dev/stage/production 进行典型验证的自定义代码。此外，用户对该功能的访问完全由管理员控制，因此您可以对其进行评估，而无需将其暴露给所有用户。

可以评估 Content Hub，而不会影响在 AEM as a Cloud Service 资产s 管理的用户/生产内容。
评估程序可能如下所示：

* [启用 Content Hub](/help/assets/deploy-content-hub.md#enable-content-hub) 在生产环境中（Cloud Manager 程序）
* [添加 AEM 管理员用户](/help/assets/deploy-content-hub.md#onboard-content-hub-administrator) 从制作作者到 Content Hub 产品轮廓。
* AEM 管理员 [配置 Content Hub](/help/assets/configure-content-hub-ui-options.md)
* AEM 管理员或 AEM 生产作者上的 AEM 用户 [批准了 Content Hub 的多项资产](/help/assets/approve-assets-content-hub.md)；如果您不想更改 DAM 中的任何生产内容，您可能需要在 AEM 作者实例中创建一个单独的评估文件夹，然后将一些资产从 DAM 上传/标记或复制到其中。
* Admin Console 管理员添加 [一些选定的用户](/help/assets/deploy-content-hub.md#onboard-content-hub-users) 到 Content Hub 产品轮廓，以便他们可以开始评估。
* 评估完成后，作者实例中的 AEM 用户可以删除测试资产的审批，批准 Content Hub 的生产资产，然后 Admin Console 管理员可以添加所有需要访问 Content Hub 和批准内容的用户。恭喜，您的 Content Hub 现已上线。

有一个程序可以提前访问沙盒程序及其创作生产环境上的Content Hub 。 请参阅[沙盒简介](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md)，了解更多详细信息。要了解详情有关早期访问计划的更多信息，请联系您的 Adobe 帐户团队。

Content Hub尚不适用于非生产环境（暂存和开发）。 Assets Ultimate的stage/dev环境预计将于2025年3月可用。

## 为什么登录 Content Hub 后我看不到任何资产？ {#no-assets-in-content-hub}

在 资产s as a Cloud Service 中标记为已批准的资产将自动在 Content Hub 中可用。如果登录 Content Hub 后看不到任何资产，请使用 AEM as a Cloud Service 作者环境批准资产，以使其在 Content Hub 中可用。如需了解更多信息，请参阅 [批准 Content Hub 的资产](/help/assets/approve-assets-content-hub.md)。

## 为什么我看不到使用 Content Hub 直接上传的资产或者使用 Content Hub 从 Dropbox 或 OneDrive 帐户导入的资产？ {#no-assets-uploaded-from-content-hub}

使用 Content Hub 上传的资产的显示取决于您是否启用了配置用户界面上的 [自动审批](/help/assets/configure-content-hub-ui-options.md#configure-import-options-content-hub) 切换按钮：

* 如果启用了 **自动批准** 切换按钮，您使用 Content Hub 上传的资产将自动可用。

* 如果禁用 **自动审批** 切换，则您使用 Content Hub 上传的资产不会自动显示。这些资产可在 资产s as a Cloud Service 环境的 `hydrated-资产s` `hydrated-assets` 文件夹中找到。导航到该文件夹并 [批量编辑](/help/assets/approve-assets-content-hub.md) 这些资产的状态以 `Approved` 使这些资产显示在 Content Hub。

## 如何在 AEM as a Cloud Service 环境中快速查找使用 Content Hub 上传的资产？ {#find-uploaded-assets-on-aem-cloud}

您可以通过以下方式在 AEM as a Cloud Service 环境中快速找到使用 Content Hub 上传的资产：

1. 导航到 `hydrated-assets` 文件夹。

1. 点击 **[!UICONTROL 筛选条件]** 并在 **[!UICONTROL 资产状态]** 字段中设置 **[!UICONTROL 无状态]** 。

1. 使用 **[!UICONTROL 修改日期]** 字段对资产进行排序。

## 为什么我无法在资产信息卡上查看使用 Adobe Express 选项进行编辑，从而无法重新混合资产来创建新的变体？ {#edit-using-express-not-available}

要查看资产信息卡上使用 Adobe Express 选项进行的编辑，您除了必须拥有 [Content Hub 用户的权限（有权将资产重新混合为新变体](#onboard-content-hub-users-add-assets)）之外，还必须拥有 Adobe Express 授权。Adobe Express 必须与 Adobe Experience Manager 部署在 Adobe Admin Console 中的同一组织中。

## 我可以设置 Content Hub，以便我的组织的品牌指南显示为主页上的关联吗？ {#content-hub-setup-brand-guidelines}

除了 Content Hub 主页上的标准 “所有 资产s”、“收藏 ”和 “Insights ”选项卡外，您还可以将自定义链接添加为单独的选项卡。有关如何设置的信息，请参阅 [自定义关联](/help/assets/configure-content-hub-ui-options.md#configure-custom-links-content-hub)。

## 是否有将现有 Brand Portal 帐户迁移至 Content Hub 的计划？ {#migration-brand-portal}

Adobe 提供从 Brand Portal 到 Content Hub 的迁移支持，您可以通过创建 Adobe 支持票证来使用该支持。

## 为什么我在 Content Hub 看不到产品设置/配置选项？ {#ui-configuration-option-missing}

要访问 [配置用户界面](/help/assets/configure-content-hub-ui-options.md)，您需要成为 [Content Hub 管理员](/help/assets/deploy-content-hub.md##onboard-content-hub-administrator)。如果您在 Adobe Admin Console 中的生产作者实例上被分配到 AEM 管理员产品轮廓，但仍然看不到配置选项，请确保 AEM 管理员产品轮廓未重命名。有关更多详细信息，请参阅 [AEM as a Cloud Service 团队和产品轮廓](/help/onboarding/aem-cs-team-product-profiles.md) 。
