---
title: Commerce多商店设置
description: 了解如何将多个商店视图从Adobe Commerce映射到AEM。 这允许项目支持多租户和多语言用例。
sub-product: Commerce
version: Cloud Service
doc-type: technical-video
activity: setup
audience: administrator
feature: Commerce Integration Framework
kt: 3046
thumbnail: 28952.jpg
exl-id: 4385c9e5-2b25-4f95-952f-72349431cf94
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '384'
ht-degree: 2%

---

# Commerce多商店设置 {#multi-store}

AEM CIF核心组件可用于多个AEM站点结构，并且底层GraphQL客户端实施可以连接到不同的Adobe Commerce存储/存储视图。 这允许项目实施复杂的多存储/多站点设置。

视频演练，详细介绍用于将多个Adobe Commerce Store视图与Adobe Experience Manager Sites集成的选项。

>[!VIDEO](https://video.tv.adobe.com/v/28952/?quality=12)

Live Copy和Language Copy的AEM多站点管理功能与Commerce Integration Framework结合使用，以便在区域和区域设置之间全局管理站点。

建议的设置是在AEM站点与Adobe Commerce商店视图之间使用1:1关系。

要将AEM站点和AEM CIF核心组件连接到专用存储视图，请执行以下步骤：

## 配置 {#configuration}

1. 根据中所述的模式配置多个商店和商店视图 [Adobe Commerce网站、商店和视图](https://docs.magento.com/m2/ce/user_guide/stores/websites-stores-views.html)

2. 确保AEM与Adobe Commerce之间的连接正常工作。

3. 按照以下步骤创建CIFCloud Service配置的子配置：

   * 在AEM中，转到工具 — >常规 — > [配置浏览器](/help/implementing/developing/introduction/configurations.md#using-configuration-browser)
   * 选择您创建的基本配置
   * 使用上述第2点所述的步骤创建新配置

   此新配置作为基本配置的子配置创建。 您现在可以转到工具 — >常规 — >配置浏览器并创建配置设置。

   >[!TIP]
   >
   > 商业目录可以使用ID或UID来寻址。 Adobe Commerce 2.4.2中引入了UID。仅当您的Commerce后端支持2.4.2版或更高版本的GraphQL架构时，才启用此选项。

4. 将子配置分配给AEM站点

   * 转到AEM Sites控制台
   * 导航到站点结构的区域或语言根，例如/content/venia/us _或_ /content/venia/us/en ，用于Venia示例页面
   * 选择页面并打开页面属性
   * 选择“高级”选项卡
   * 在 `Configuration` 部分选择您在步骤3创建的配置

## 其他资源

* [Adobe Commerce网站、商店和视图](https://docs.magento.com/m2/ce/user_guide/stores/websites-stores-views.html)
* [AEM CIF核心组件 — 多存储/站点配置](https://github.com/adobe/aem-core-cif-components/wiki/configuration#multi-store--site-configuration)
* [使用多站点管理器](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/translation/multi-site-manager-feature-video-use.html)
* [重用内容：多站点管理器和 Live Copy](/help/sites-cloud/administering/msm/overview.md)
