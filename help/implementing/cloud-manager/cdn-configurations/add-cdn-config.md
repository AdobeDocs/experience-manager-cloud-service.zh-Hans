---
title: 添加CDN配置
description: 了解如何为Edge Delivery站点或Cloud Manager环境添加CDN配置。
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
exl-id: 672513d7-ee0a-4f6e-9ef0-7a41fabbaf9a
source-git-commit: b222b4384b1c2a21ecbb244d149ce7e51cc7990f
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 6%

---


# 添加 CDN 配置 {#add-cdn}

要将域与项目中由Adobe管理的CDN上的SSL证书链接，您必须添加CDN（内容分发网络）配置。

对于Adobe托管的CDN，在使用DV证书时，只允许使用ACME验证的站点。

>[!IMPORTANT]
>
>您[是否已添加自定义域名](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)和[是否已分别添加SSL证书](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)？ 如果不能，则必须先完成这两项任务，然后才能添加CDN配置。

**添加CDN配置：**

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织。

1. 根据您的用例，执行以下操作之一：

   | 用例 | 步骤 |
   | --- | --- |
   | 我要将CDN配置添加到Cloud Manager中的&#x200B;*现有*&#x200B;个Edge Delivery站点 | a.在左侧导航面板中的&#x200B;**服务**&#x200B;下，单击&#x200B;**Edge Delivery站点**。<br>b。在Edge Delivery表中，在没有关联域的行的末尾，单击省略号。<br>c。单击&#x200B;**配置CDN**。  ![单击“为Edge Delivery站点配置CDN”](/help/implementing/cloud-manager/assets/cm-eds-config-cdn.png) |
   | 我想在Cloud Manager中添加CDN配置 | a.在左侧导航面板中的&#x200B;**服务**&#x200B;下，单击&#x200B;**CDN配置**。<br>b。在“CDN配置”页面的右上角附近，单击&#x200B;**添加**。 |

1. 在&#x200B;**配置CDN**&#x200B;对话框的&#x200B;**原点**&#x200B;下拉列表中，选择以下选项之一：

   ![配置CDN对话框](/help/implementing/cloud-manager/assets/configure-cdn-dialog.png)

   | 来源 | 描述 |
   | --- | --- |
   | Sites | 选择Edge Delivery站点。 |
   | 环境 | 选择要在AEM设置中定位的特定Cloud Service环境。<br>在&#x200B;**层**&#x200B;下拉列表中，选择以下任一项：<br>·选择&#x200B;**Publish**&#x200B;以将内容交付给最终用户的实时生产环境作为目标。<br>·选择&#x200B;**预览**&#x200B;用于暂存或非生产环境，您可在这些环境中测试更改的上线时间。 |

1. 通过选择以下任一选项来选择您的CDN类型和关联的配置：

   | CDN类型 | 配置详情 |
   | --- | --- |
   | Adobe 管理的 CDN | 在&#x200B;**配置详细信息**&#x200B;下，执行以下操作：<br>a。在&#x200B;**域**&#x200B;下拉列表中，选择要使用的域名。<br>下拉列表中没有可用的验证域？ 请参阅[添加自定义域名](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)。<br>b。在&#x200B;**SSL证书**&#x200B;下拉列表中选择要使用的证书。<br>下拉列表中没有SSL证书可用？ 请参阅[添加SSL证书](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)。 |
   | 其他 CDN 提供商 | 如果您使用的是自己的CDN提供商，而不是您可用的Adobe托管的CDN，请选择此选项。<br>在&#x200B;**配置详细信息**&#x200B;下，在&#x200B;**域**&#x200B;下拉列表中，选择要使用的域名。<br>下拉列表中没有可用的验证域？ 请参阅[添加自定义域名](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)。 |

1. 单击&#x200B;**保存**。
