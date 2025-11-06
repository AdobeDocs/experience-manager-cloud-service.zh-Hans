---
title: 检查域名状态
description: 了解如何验证Cloud Manager是否已成功确认您的自定义域名。
exl-id: 8fdc8dda-7dbf-46b6-9fc6-d304ed377197
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '863'
ht-degree: 19%

---


# 检查域名状态 {#check-status}

了解如何验证Cloud Manager是否已成功确认您的自定义域名。

## 检查自定义域名的状态 {#how-to}

在Cloud Manager中检查域名状态之前，请确保已按照[添加客户管理的SSL证书](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md##add-customer-managed-ssl-cert)中的说明为自定义域添加了客户管理的(OV/EV) SSL证书。

**检查自定义域名的状态：**

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织。

1. 在&#x200B;**[我的程序](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;控制台上，选择该程序。

1. 从&#x200B;**概述**&#x200B;页面导航到&#x200B;**环境**&#x200B;屏幕。

1. 单击左侧菜单中的&#x200B;**域设置**。

1. 单击域名的&#x200B;**状态**&#x200B;图标。

将显示状态详细信息。 当显示&#x200B;**域已验证和部署**&#x200B;状态时，您的自定义域即可使用。 有关不同状态及其含义的详细信息，请参阅[下一部分](#statuses)。

>[!NOTE]
>
>如果您正在域中使用&#x200B;*Adobe托管(DV) SSL证书*，则当您在&#x200B;**添加自定义域名**&#x200B;时单击“验证域”对话框中的[验证](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)时，Cloud Manager会自动触发验证。
>
>如果您计划使用&#x200B;**客户管理的(OV/EV) SSL证书**，请在&#x200B;*之后*&#x200B;验证您的域[添加OV/EV SSL证书](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)。


## 验证状态 {#statuses}

Cloud Manager通过客户管理的(OV/EV) SSL证书验证域所有权。 完成后，它会显示以下状态消息之一：

| 状态 | 描述 |
| --- | --- |
| 域验证失败 | 客户管理的EV/OV证书缺失或检测到错误。<br>按照状态消息中提供的说明解决问题。 准备就绪后，您必须选择状态旁边的&#x200B;**再次验证**&#x200B;图标。 |
| 正在进行域验证 | 正在进行验证。<br>选择状态旁边的&#x200B;**再次验证**&#x200B;图标后，通常会看到此状态。 由于 DNS 传播延迟，DNS 验证可能需要几个小时才能处理。 |
| 已验证 — 部署失败 | EV/OV证书验证成功，但CDN部署失败。<br>在这种情况下，请联系您的Adobe代表。 |
| 域已验证和部署 | 此状态表示您的自定义域名已准备好使用。<br>此时，您的自定义域名已准备好进行测试并指向Cloud Manager域名。 请参阅[添加自定义域名](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)以了解详情。 |
| 正在删除 | 正在删除自定义域名。 |
| 删除失败 | 删除自定义域名失败，必须重试。<br>请参阅[管理自定义域名](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md)以了解详情。 |


## 域名错误 {#domain-error}

以下是常见的域名验证错误及其典型解决方案。

### 域未安装错误 {#domain-not-installed}

<!-- This error may occur during domain validation of the EV/OV certificate even after you have checked that the certificate has been updated appropriately. -->

当您尝试在Cloud Manager中添加域映射时，可能会遇到以下错误消息：

*域已安装在Fastly帐户中。 请先将它从此处删除，然后再添加到Cloud Service。*

<!-- This message indicates that the domain is currently associated with a different Fastly account—typically outside of Adobe's control. To proceed, the domain must be disassociated from the other account before it can be added to the Adobe-managed Cloud Service. This issue usually occurs when the same domain is already mapped to a different origin in a non-Adobe Fastly configuration. -->

**错误原因**
Fastly将域锁定到首先注册它的帐户，而其他帐户必须请求权限来注册子域。 此外，Fastly 只允许您将一个 Apex 域和关联子域分配给一个 Fastly 服务和帐户。如果您现有的Fastly帐户链接了AEM Cloud Service域使用的相同Apex和子域，则会看到此错误。

**错误解决**
错误修复如下：

* 在 Cloud Manager 中安装域之前，请从现有帐户中移除 Apex 和子域。

* 使用此选项将 Apex 域和所有子域链接到 AEM as a Cloud Service Fastly 帐户。有关更多详细信息，请参阅Fastly文档中的[使用域](https://www.fastly.com/documentation/guides/getting-started/domains/working-with-domains/working-with-domains/)。

* 如果您的Apex域有多个子域用于AEM as a Cloud Service和非AEM网站，并且这些子域需要链接到不同的Fastly帐户，请尝试在Cloud Manager中安装该域。 此过程有助于管理不同Fastly帐户之间的子域连接。 如果域安装失败，请使用Fastly创建客户支持工单，以便Adobe可以代表您跟进Fastly。

>[!TIP]
>
>使用 Fastly 解决域授权问题通常需要 1-2 个工作日。因此，建议在上线日期之前安装好域。

>[!NOTE]
>
>如果域未成功安装，请不要将站点的 DNS 路由到 AEM as a Cloud Service IP 的 DNS。

## 自定义域名的预先存在CDN配置 {#pre-existing-cdn}

如果您的自定义域名已有CDN （内容分发网络）配置，则会在&#x200B;**自定义域名**&#x200B;和&#x200B;**环境**&#x200B;页面上显示一条信息性消息。 它鼓励您通过UI添加这些配置，以便在Cloud Manager中管理和查看它们。

使用UI迁移所有预先存在的环境配置后，消息将消失。 消息可能需要 1 – 2 个工作日才能消失。

有关详细信息，请参阅[添加自定义域名](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)。

## 后续步骤 {#next-steps}

在Cloud Manager中验证域状态后，通过添加指向AEM as a Cloud Service的DNS、CNAME或APEX记录来配置DNS设置。 继续文档[添加自定义域名](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)以继续设置自定义域名。
