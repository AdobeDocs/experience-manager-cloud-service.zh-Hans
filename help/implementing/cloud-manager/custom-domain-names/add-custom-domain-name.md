---
title: 添加自定义域名
description: 了解如何使用 Cloud Manager 添加自定义域名。
exl-id: 0fc427b9-560f-4f6e-ac57-32cdf09ec623
source-git-commit: 52466e091cf6e0ab1ac620e15568c04881a3b63a
workflow-type: tm+mt
source-wordcount: '680'
ht-degree: 73%

---


# 添加自定义域名 {#adding-cdn}

您可以从 Cloud Manager 中的两个位置添加自定义域名：

* [从“域设置”页面](#adding-cdn-settings)
* [从“环境”页面](#adding-cdn-environments)

>[!NOTE]
>
>用户必须具有 **业务负责人** 或 **部署管理员** 角色在Cloud Manager中添加自定义域名，并且您必须使用Fastly CDN。

## 从“域设置”页面添加自定义域名 {#adding-cdn-settings}

添加自定义域名时，将使用最具体且有效的证书为该域提供服务。 如果多个证书具有相同的域，则选择最近更新的证书。 Adobe建议您管理证书，这样就不会有重叠域。

按照以下这些步骤从&#x200B;**域设置**&#x200B;页面添加自定义域名。这些步骤基于Fastly。 如果您使用其他CDN，则必须使用您选择使用的CDN配置域。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织。

1. 在 **[我的项目群](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md#my-programs)** 屏幕上，选择程序。

1. 从&#x200B;**概述**&#x200B;页面导航到&#x200B;**环境**&#x200B;屏幕。

1. 单击 **域设置** （在左侧导航面板中）。

   ![域设置窗口](/help/implementing/cloud-manager/assets/cdn/cdn-create.png)

1. 单击 **添加域** 按钮打开 **添加域名** 对话框。

   ![“添加域”对话框](/help/implementing/cloud-manager/assets/cdn/add-cdn1.png)。

1. 在&#x200B;**域名**&#x200B;字段中输入自定义域名。

   >[!NOTE]
   >
   >输入域时不要包含 `http://`、`https://` 或空格。

1. 选择其服务与域名关联的&#x200B;**环境**。

1. 选择&#x200B;**发布**&#x200B;或&#x200B;**预览**&#x200B;服务。

1. 从下拉列表中选择与域名关联的&#x200B;**域 SSL 证书**，然后选择&#x200B;**继续**。

1. 此时会出现&#x200B;**添加域名**&#x200B;对话框，您将从此进入域名验证过程。 按照提供的说明，证明您环境的域所有权。 单击&#x200B;**创建**。

   ![域名验证](/help/implementing/cloud-manager/assets/cdn/cdn-create6.png)

CDN 部署需要有效的 SSL 证书和成功的 TXT 验证。 这由状态&#x200B;**已验证和已部署**&#x200B;表示。

请参阅[检查自定义域名状态](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md)，了解有关各种状态的更多信息以及如何解决潜在问题。

>[!TIP]
>
>阅读以下文章，了解其需要 [接下来添加CNAME或记录](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md) 避免在将DNS记录添加到自定义域时加倍努力。 TXT条目和CNAME或A记录可以同时在DNS管理服务器上设置。

>[!TIP]
>
>请参阅[添加 TXT 记录](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md)，了解有关 TXT 记录的更多信息。

>[!NOTE]
>
>由于 DNS 传播延迟，DNS 验证可能需要几个小时才能处理。
>
>Cloud Manager 将验证所有权并更新可在域设置表中看到的状态。 请参阅[检查自定义域名](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md)，了解更多详细信息。

## 从环境页面添加自定义域名 {#adding-cdn-environments}

按照以下步骤从&#x200B;**环境**&#x200B;页面添加自定义域名。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 上登录到 Cloud Manager 并选择适当的组织和项目。

1. 导航至&#x200B;**环境详细信息**&#x200B;页面，了解感兴趣的环境。

   ![在“环境详细信息”页面上输入域名](/help/implementing/cloud-manager/assets/cdn/cdn-create4.png)

1. 使用&#x200B;**域名**&#x200B;表提交自定义域名。

   1. 输入自定义域名。
   1. 从下拉列表中选择与此名称关联的 SSL 证书。
   1. 单击 **+添加**.

   ![添加自定义域名](/help/implementing/cloud-manager/assets/cdn/cdn-create3.png)

1. 检查&#x200B;**添加域名**&#x200B;对话框中选择的值，然后单击&#x200B;**继续**。

   ![域名窗口](/help/implementing/cloud-manager/assets/cdn/cdn-create5.png)

   >[!NOTE]
   >
   >输入域名时不要包含 `http://`、`https://` 或空格。

1. 此时会出现&#x200B;**添加域名**&#x200B;对话框，您将从此进入域名验证过程。 按照提供的说明，证明您环境的域所有权。 单击&#x200B;**创建**。

   ![域名验证](/help/implementing/cloud-manager/assets/cdn/cdn-create6.png)

CDN 部署需要有效的 SSL 证书和成功的 TXT 验证。 这由状态&#x200B;**已验证和已部署**&#x200B;表示。

请参阅[检查自定义域名状态](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md)，了解有关各种状态的更多信息以及如何解决潜在问题。

>[!NOTE]
>
>由于 DNS 传播延迟，DNS 验证可能需要几个小时才能处理。
>
>Cloud Manager 将验证所有权并更新可在域设置表中看到的状态。 请参阅[检查自定义域名](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md)，了解更多详细信息。

>[!TIP]
>
>请参阅[添加 TXT 记录](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md)，了解有关 TXT 记录的更多信息。
