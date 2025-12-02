---
title: 添加域映射
description: 了解如何为Edge Delivery站点或Cloud Manager环境添加域映射。
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
exl-id: 672513d7-ee0a-4f6e-9ef0-7a41fabbaf9a
source-git-commit: 4935fbf5f0eb10f2f17280fb32f07d99f69eb875
workflow-type: tm+mt
source-wordcount: '584'
ht-degree: 5%

---


# 关于添加域映射 {#add-domain-mapping}

要将域与项目中由Adobe管理的CDN上的SSL证书链接，您必须添加CDN（内容分发网络）配置。

对于Adobe托管的CDN，在使用DV SSL证书时，只允许使用ACME验证的站点。

>[!IMPORTANT]
>
>您[是否已添加自定义域名](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)和[是否已分别添加SSL证书](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)？ 如果不能，则必须先完成这两项任务，然后才能添加CDN配置。

另请参阅[Adobe托管的CDN](https://www.aem.live/docs/byo-cdn-adobe-managed)。

**要添加域映射：**

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织。

1. 根据您的用例，执行以下操作之一：

   | 用例 | 步骤 |
   | --- | --- |
   | 我要将CDN配置添加到Cloud Manager中的&#x200B;*现有*&#x200B;个Edge Delivery站点 | a.在左侧菜单的&#x200B;**服务**&#x200B;下，单击![网页图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_WebPages_18_N.svg)**Edge Delivery站点**。<br>b。在Edge Delivery表格中，在无关联域的行的末尾，单击![更多图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)。<br>c。单击&#x200B;**配置CDN**。 |
   | 我想在Cloud Manager中添加CDN配置 | a.在左侧菜单的&#x200B;**服务**&#x200B;下，单击![社交网络图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_SocialNetwork_18_N.svg) **域映射**。<br>b。在“域映射”页面的右上角附近，单击&#x200B;**添加**。 |

1. 在&#x200B;**将域映射到CDN**&#x200B;对话框中，选择以下CDN类型之一：

   * **Adobe托管的CDN（推荐）** — 此配置使用了Adobe托管的CDN。 它包括自动设置和管理以及内置的安全功能。
   * **其他CDN提供商** — 此配置使用了自管理的CDN提供商网络。

1. 根据上一步中所选的CDN类型，执行以下操作：

   * **Adobe托管的CDN**

     ![选中Adobe托管的CDN单选按钮的“将域映射到CDN”对话框](/help/implementing/cloud-manager/assets/cdn/map-domain-to-cdn-adobe-managed.png)

      1. 在&#x200B;**Origin**&#x200B;下拉列表中，选择下列选项之一：

         | “来源”下拉列表 | 描述 |
         | --- | --- |
         | Sites | 选择Edge Delivery站点。 |
         | 环境 | 选择要在AEM设置中定位的特定Cloud Service环境。<br>在&#x200B;**层**&#x200B;下拉列表中，选择以下选项之一：<br>·选择&#x200B;**发布**&#x200B;以将内容交付给最终用户的实时生产环境作为目标。<br>·选择&#x200B;**预览**&#x200B;用于暂存或非生产环境，您可在这些环境中测试更改的上线时间。 |

      1. 在&#x200B;**域**&#x200B;下拉列表中，选择要使用的域名。<br>下拉列表中没有可用的验证域？ 请参阅[添加自定义域名称](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)。

      1. 在&#x200B;**SSL证书**&#x200B;下拉列表中选择要使用的证书。<br>下拉列表中没有SSL证书可用？ 请参阅[添加SSL证书](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)。

      1. 单击&#x200B;**保存**。

   * **其他CDN提供商**

     ![选中Adobe托管的CDN单选按钮的“将域映射到CDN”对话框](/help/implementing/cloud-manager/assets/cdn/map-domain-to-cdn-other-provider.png)

     使用列出的配置步骤在CDN中应用所需的设置并确认映射。 另请参阅[添加自定义域名](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)。

      1. 单击&#x200B;**我已配置我的CDN**。

   <!-- OLD IMAGE/UI (/help/implementing/cloud-manager/assets/configure-cdn-dialog.png)-->

   <!-- In the **Domain** field, enter the customer-facing hostname you want to serve (for example, `www.example.com`) -->

1. Adobe建议您测试域映射。

## 测试域映射 {#test-domain-mapping}

您可以验证新域映射在Adobe管理的CDN上是否处于活动状态，而无需等待公共DNS传播。

运行覆盖DNS解析并直接指向CDN边缘的&#x200B;**curl**&#x200B;命令：

```bash
curl -svo /dev/null https://www.example.com \
--resolve www.example.com:443:151.101.3.10
```

* 将`www.example.com`替换为您的域。
* IP地址`151.101.3.10`是可用于访问AEM Cloud Service的IP之一。 另请参阅[APEX记录](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md#adobe-managed-cert-apex-record)。

`--resolve`标记强制将请求发送到指定的IP，并且仅在域的证书和路由安装正确后才返回成功。

