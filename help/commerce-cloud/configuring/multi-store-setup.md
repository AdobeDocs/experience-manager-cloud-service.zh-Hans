---
title: 多商店设置
description: 多商店设置
translation-type: tm+mt
source-git-commit: 69756d6831678151b0e8eb73db81113d49f17447
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 0%

---


# 多商店设置 {#multi-store}

AEM CIF核心组件可用于多个AEM站点结构，基础GraphQL客户端实现可连接到不同Magento存储／存储视图。 这允许项目实施复杂的多商店／多站点设置。

一个视频演练，详细介绍将多个Magento商店视图与Adobe Experience Manager Sites集成的选项。

>[!VIDEO](https://video.tv.adobe.com/v/28952/?quality=12)

AEM Live Copy和Language Copy的多站点管理功能与Commerce Integration Framework结合使用，以全局管理跨区域和区域设置的站点。

建议的设置是在AEM站点和Magento商店视图之间使用1:1关系。

要将AEM站点和AEM CIF核心组件连接到专用商店视图，请执行以下步骤：

## 配置 {#configuration}

1. 根据视图网站、商店和Magento中描述的模式配 [置多个商店和视图](https://docs.magento.com/m2/ce/user_guide/stores/websites-stores-views.html)

2. 确保AEM和Magento之间的连接正常工作。

3. 按照以下步骤创建CIFCloud Service配置的子配置：

   * 在AEM中，转到工具->常规->配 [置浏览器](/help/implementing/developing/introduction/configurations.md#using-configuration-browser)
   * 选择您创建的基本配置
   * 使用上面第2点所述的步骤创建新配置

   此新配置将创建为基本配置的子配置。 您现在可以转到工具->常规->配置浏览器并创建配置设置。

4. 将子配置分配给AEM站点

   * 转到AEM Sites控制台
   * 导航到站点结构的区域或语言根，例如/content/venia/us _或_ /content/venia/us/en，用于Venia示例页面
   * 选择页面并打开页面属性
   * 选择高级选项卡
   * 在部分 `Configuration` 中，选择您在步骤中创建的配置

## 其他资源

* [Magento网站、商店和视图](https://docs.magento.com/m2/ce/user_guide/stores/websites-stores-views.html)
* [AEM CIF核心组件——多商店／站点配置](https://github.com/adobe/aem-core-cif-components/wiki/configuration#multi-store--site-configuration)
* [使用多站点管理器](https://docs.adobe.com/content/help/en/experience-manager-learn/sites/translation/multi-site-manager-feature-video-use.html)
* [重用内容：多站点管理器和Live Copy](https://helpx.adobe.com/experience-manager/6-5/sites/administering/using/msm.html)
