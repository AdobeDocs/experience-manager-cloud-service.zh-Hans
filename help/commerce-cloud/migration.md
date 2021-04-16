---
title: 迁移到AEM Commerce Integration Framework(CIF)加载项
description: 如何从旧版本迁移到AEM Commerce Integration Framework(CIF)加载项
translation-type: tm+mt
source-git-commit: cda25048e171f6aacd5349706ad4192965e703db
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 1%

---

# Experience Manager Cloud Service{#cif-migration}的迁移指南

本指南有助于确定您需要更新的Experience Manager Cloud Service迁移区域。

## CIF附加

对于Experience Manager作为Cloud Service,CIF加载项是Adobe商务和第三方商务解决方案唯一支持的商务集成解决方案。 CIF插件是自动部署给Experience Manager客户的Cloud Service，无需手动部署。 请参阅[将AEM Commerce作为Cloud Service入门](getting-started.md)。

要支持部署CIFAdobe的项目，请提供[AEM CIF核心组件](https://github.com/adobe/aem-core-cif-components)。

CIF加载项也可通过[软件分发门户](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)用于AEM 6.5。 它兼容，并提供与Experience ManagerCIF附加功能相同的功能 — 无需调整。

具有其依赖项的经典CIF不再可用。 依赖使用`com.adobe.cq.commerce.api` Java API的CIF版本的代码必须调整为CIF加载项及其原则。

无法再安装以前可用的CIF连接器。 依赖此连接器的代码需要调整至CIF附件及其原理。

## 项目结构

了解[AEM项目结构](https://docs.adobe.com/content/help/zh-Hans/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html)以及AEM作为Cloud Service的特性。 将您的项目设置调整为AEM作为Cloud Service布局。
与AEM 6.5部署相比，以下两个主要区别：

* GraphQL客户端OSGI包&#x200B;**不能再**&#x200B;包含在AEM项目中，它通过CIF加载项进行部署
* GraphQL客户端和Graphql数据服务&#x200B;**的OSGI配置不能再**&#x200B;包含到AEM项目中

>[!TIP]
>
>查看GitHub上的[AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)项目。 此项目将Maven AEM用户档案作为Cloud Service和内部部署提供，并考虑到不同的框架条件。

## 产品目录

不再支持导入产品目录数据。 使用CIF附加承担者产品和目录请求是通过对外部商务解决方案的实时调用进行点播的。 转到“集成”一章，了解有关集成商务解决方案的更多信息。

>[!TIP]
>
>如果没有可用的实时API，则应使用具有API的外部产品缓存进行集成。 示例[Magento开放源](https://magento.com/products/magento-open-source)。

## 利用AEM渲染实现产品目录体验

如果将目录蓝图与Classic CIF一起使用，则需要更新产品目录工作流。 CIF加载项现在使用AEM目录模板实时呈现产品目录体验。 不再需要复制产品数据或产品页面。

## 不可缓存的数据和购物互动

客户端对不可缓存数据和交互（例如，添加到购物车、搜索）的请求应通过CDN/Dispatcher直接转到商务端点（商务解决方案或集成层）。 删除AEM仅是代理的任何调用。
