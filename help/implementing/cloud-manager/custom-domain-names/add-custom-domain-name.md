---
title: 添加自定义域名
description: 了解如何使用Cloud Manager添加自定义域名。
exl-id: 0fc427b9-560f-4f6e-ac57-32cdf09ec623
source-git-commit: 0febf4b4a59617e6cc4f8414963c4a91fcf8765e
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 1%

---

# 添加自定义域名 {#adding-cdn}

您可以在Cloud Manager中从两个位置添加自定义域名：

* [从“域设置”页面](#adding-cdn-settings)
* [从“环境”页面](#adding-cdn-environments)

>[!NOTE]
>
>用户必须具有 **业务所有者** 或 **部署管理器** 角色，以便在Cloud Manager中添加自定义域名

## 从“域设置”页面添加自定义域名 {#adding-cdn-settings}

请按照以下步骤从 **域设置** 页面。

1. 登录Cloud Manager(位于 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 并选择相应的组织和程序。

1. 导航到 **环境** 屏幕 **概述** 页面。

1. 单击 **域设置** 中。

   ![“域设置”窗口](/help/implementing/cloud-manager/assets/cdn/cdn-create.png)

1. 单击 **添加域** 按钮以打开 **添加域名** 对话框。

   ![“添加域”对话框](/help/implementing/cloud-manager/assets/cdn/add-cdn1.png)

1. 在 **域名** 字段。

   >[!NOTE]
   >
   >不包括 `http://`, `https://`、或空格。

1. 选择 **环境** 其服务将与域名关联。

1. 选择 **发布** 或 **预览** 服务。

1. 选择 **域SSL证书** 与域名关联，请从下拉菜单中选择 **继续**.

1. 的 **添加域名** 对话框，将带您进入域名验证过程。 按照提供的说明来证明您环境的域所有权。 单击 **创建**.

   ![域名验证](/help/implementing/cloud-manager/assets/cdn/cdn-create6.png)

CDN部署需要有效的SSL证书和成功的TXT验证。 状态指示 **已验证和部署**.

请参阅文档 [检查自定义域名状态](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) 了解有关各种状态以及如何解决潜在问题的更多信息。

>[!NOTE]
>
>由于DNS传播延迟，DNS验证可能需要数小时才能处理。
>
>Cloud Manager将验证所有权并更新状态，这些状态可在域设置表中查看。 请参阅文档 [检查自定义域名状态](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) 以了解更多详细信息。

>[!TIP]
>
>请参阅 [添加TXT记录](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md) 了解有关TXT记录的更多信息。

## “从环境添加自定义域名”页 {#adding-cdn-environments}

请按照以下步骤从 **环境** 页面。

1. 登录Cloud Manager(位于 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 并选择相应的组织和程序。

1. 导航到 **环境详细信息** 页面。

   ![在“环境详细信息”页面中输入域名](/help/implementing/cloud-manager/assets/cdn/cdn-create4.png)

1. 使用 **域名** 表来提交自定义域名。

   1. 输入自定义域名。
   1. 从下拉列表中选择与此名称关联的SSL证书。
   1. 单击 **+添加**.

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create3.png)

1. 检查 **添加域名** 对话框，单击 **继续**.

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create5.png)

   >[!NOTE]
   >
   >不包括 `http://`, `https://`、或在域名中输入空格。

1. 的 **添加域名** 对话框，将带您进入域名验证过程。 按照提供的说明来证明您环境的域所有权。 单击 **创建**.

   ![域名验证](/help/implementing/cloud-manager/assets/cdn/cdn-create6.png)

CDN部署需要有效的SSL证书和成功的TXT验证。 状态指示 **已验证和部署**.

请参阅文档 [检查自定义域名状态](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) 了解有关各种状态以及如何解决潜在问题的更多信息。

>[!NOTE]
>
>由于DNS传播延迟，DNS验证可能需要数小时才能处理。
>
>Cloud Manager将验证所有权并更新状态，这些状态可在域设置表中查看。 请参阅文档 [检查自定义域名状态](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) 以了解更多详细信息。

>[!TIP]
>
>请参阅 [添加TXT记录](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md) 了解有关TXT记录的更多信息。
