---
title: 为发布层配置自定义域
description: 了解如何在AdobeCloud Manager中为发布层配置自定义域。
source-git-commit: f6c0e8e5c1d7391011ccad5aa2bad4a6ab7d10c3
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 6%

---


# 为发布层配置自定义域{#configure-custom-domain}

在AdobeCloud Manager中，您可以通过添加自定义域让您的网站脱颖而出。 虽然AEM as a Cloud Service附带默认域，但您可以根据需要对其进行自定义。

## 开始之前

* 您必须具有多SAN（使用者替代名称）TLS或SSL证书。
* 对于为同一域中的发布层映射的证书，SSL证书应具有不同的SAN。
* 证书策略必须遵循扩展验证(EV)或组织验证(OV)，而不是域验证(DV)策略。


## 添加自定义域

要为发布层配置自定义域，请执行以下步骤：

1. 转到 **[!UICONTROL AdobeCloud Manager]** > **[!UICONTROL 项目概述]** > **[!UICONTROL SSL证书]**，并添加您的SSL证书。
   ![图像](/help/assets/assets/ssl-certificate.png)
了解如何添加 [SSL证书](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) 在AdobeCloud Manager中。

1. 添加SSL证书后，添加自定义域。 单击 **[!UICONTROL 域设置]** 并指定针对的自定义域 **[!UICONTROL Publish服务]** 选项。
了解有关 [自定义域](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md).

1. 添加2 [CNAME记录](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md) 在与发布域相对应的DNS记录中。
由于 DNS 传播延迟，DNS 验证可能需要几个小时才能处理。

1. 记录支持案例以促进自定义域的配置，确保它定向到交付层。

>[!NOTE]
>
> 确保将自定义域添加到资产选择器的IMS客户端中允许的重定向URL列表中。<br>与相应的Adobe团队协调，通过提供自定义域字符串来执行此任务。
