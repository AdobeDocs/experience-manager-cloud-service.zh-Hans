---
title: 域验证 (DV) 证书
description: 了解如何在Cloud Manager中管理域验证(DV)证书。
exl-id: 7f2c71b6-15c3-4919-9f51-a3e26d0d48d4
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 8%

---

# 域验证 (DV) 证书 {#domain-validated-certificates}

了解如何在Cloud Manager中管理域验证(DV)证书。

>[!NOTE]
>
>此功能仅适用于[早期采用者计划。](/help/implementing/cloud-manager/release-notes/current.md#early-adoption)

## 简介 {#introduction}

Cloud Manager允许您自助生成和管理域验证(DV) SSL证书。 这为您提供了最快、最简单、最经济高效的解决方案，可为您的在线业务创建安全的网站。

域验证的证书对[生产和沙盒程序均可用。](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)

## 添加自定义域 {#adding-domain}

要添加域验证(DV)证书，您必须先配置自定义域。 此过程与文档[自定义域名简介中的详细过程大致相同。](/help/implementing/cloud-manager/custom-domain-names/introduction.md)但是，该功能已稍作扩展。

1. 验证域时，您可以选择在域中使用Adobe管理证书或自管理证书。 选择&#x200B;**Adobe托管证书**&#x200B;以便稍后添加DV证书。

   ![选择Adobe托管](assets/verify-domain-dialog.png)

1. 要使用Adobe托管证书，您需要将CNAME记录添加到DNS，如&#x200B;**验证域**&#x200B;对话框中所述。

   ![添加CNAME条目](assets/verify-domain-dialog-adobe-managed.png)

1. 创建域后，点按或单击域列表中的省略号按钮，然后选择&#x200B;**验证**&#x200B;以验证域。

   ![验证域](assets/verify-domain.png)

## 添加DV证书 {#adding}

正确配置域后，要添加DV证书，请点按或单击“SSL证书”窗口中的&#x200B;**添加SSL证书**&#x200B;按钮。

![正在添加DC证书](/help/implementing/cloud-manager/assets/ssl/add-dv-certificate.png)

1. 选择选项&#x200B;**Adobe托管(DV)**。
1. 在&#x200B;**选择域**&#x200B;下拉列表中选择域名。
1. 点按或单击&#x200B;**保存**。

成功添加后，证书在&#x200B;**SSL证书**&#x200B;窗口中的名称将处于待处理状态，带有黄色警告符号。

![待处理DV证书](assets/pending-dv-certificate.png)

成功颁发证书后，证书在&#x200B;**SSL证书**&#x200B;窗口中的名称将带有绿色复选标记。

![颁发的DV证书](assets/issued-dv-certificate.png)

有关添加SSL证书和SSL证书窗口的详细信息，请参阅文档[添加SSL证书。](add-ssl-certificate.md)

## 添加CDN配置 {#add-cdn}

要使用Fastly CDN使用SSL配置域，必须完成此步骤。

按照以下步骤使用Cloud Manager添加CDN配置。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织。

1. 选择&#x200B;**CDN配置**&#x200B;选项卡，然后单击或点按工具栏中的&#x200B;**添加**。

1. 在&#x200B;**配置CDN**&#x200B;对话框中，提供必要的信息。

   * 选择&#x200B;**原点**。 可以添加的资源包括：
      * Cloud Service环境
      * Edge Delivery Services网站
   * 选择您的CDN类型。
   * 选择域。
   * 选择SSL证书。
      * 仅对于Adobe管理的CDN是必需的。

   ![配置CDN对话框](assets/configure-cdn-dialog.png)

>
>
>对于由Adobe管理的CDN，在使用DV证书时，只允许使用ACME验证的站点。
