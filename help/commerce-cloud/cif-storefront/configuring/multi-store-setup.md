---
title: Commerce多商店设置
description: 了解如何将多个商店视图从Adobe Commerce映射到Adobe Experience Manager。 这允许项目支持多租户和多语言用例。
sub-product: Commerce
version: Experience Manager as a Cloud Service
doc-type: technical-video
activity: setup
audience: administrator
feature: Commerce Integration Framework
kt: 3046
thumbnail: 28952.jpg
exl-id: 4385c9e5-2b25-4f95-952f-72349431cf94
role: Admin
index: false
source-git-commit: 856442039fcd25ec675a6258d182f7a35f590c3c
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 3%

---


# Commerce多商店设置 {#multi-store}

Adobe Experience Manager (AEM) CIF核心组件可用于多个AEM站点结构，并且底层GraphQL客户端实施可以连接到不同的Adobe Commerce商店/商店视图。 这允许项目实施复杂的多存储/多站点设置。

视频演练，详细介绍用于将多个Adobe Commerce Store视图与Adobe Experience Manager Sites集成的选项。

>[!VIDEO](https://video.tv.adobe.com/v/32824/?quality=12&captions=chi_hans)

Live Copy和Language Copy的AEM多站点管理功能可与Commerce integration framework配合使用，以全局方式跨地区和区域管理站点。

建议的设置是使用AEM网站与Adobe Commerce商店视图之间的1:1关系。

要将AEM站点和AEM CIF核心组件连接到专用商店视图，请执行以下操作：

## 配置 {#configuration}

1. 根据[Adobe Commerce网站、商店和视图中描述的模式配置多个商店和商店视图。](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html?lang=zh-Hans)

1. 确保AEM与Adobe Commerce之间的连接正常。

1. 按照以下步骤创建CIF Cloud Service配置的子配置：

   * 在AEM中，转到“工具”>“常规”>“[配置浏览器”。](/help/implementing/developing/introduction/configurations.md#using-configuration-browser)
   * 选择您创建的基本配置。
   * 使用上述第2点所述的步骤创建配置。

   此新配置是作为基础配置的子配置创建的。 您现在可以转到工具>常规>配置浏览器并创建配置设置。

   >[!TIP]
   >
   > Commerce目录可以通过使用ID或UID来寻址。 Adobe Commerce 2.4.2中引入了UID。仅当您的Commerce后端支持版本2.4.2或更高版本的GraphQL架构时，才启用此功能。

1. 将子配置分配给AEM站点。

   * 转到AEM Sites控制台。
   * 导航到站点的区域或语言根.structure。 例如，`/content/venia/us _or_ /content/venia/us/en`表示Venia示例页面。
   * 选择页面并打开页面属性。
   * 选择“高级”选项卡。
   * 在`Configuration`部分中，选择您在步骤3中创建的配置。

## 其他资源 {#additional-resources}

* [Adobe Commerce网站、商店和视图](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html?lang=zh-Hans)
* [AEM CIF核心组件 — 多存储/站点配置](https://github.com/adobe/aem-core-cif-components#multi-store--site-configuration)
* [使用多站点管理器](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/translation/multi-site-manager-feature-video-use.html?lang=zh-Hans)
* [重用内容：多站点管理器和 Live Copy](/help/sites-cloud/administering/msm/overview.md)
