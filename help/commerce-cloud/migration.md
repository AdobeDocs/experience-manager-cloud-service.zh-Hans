---
title: 迁移到AEM Commerce Integration Framework(CIF)附加组件
description: 如何从旧版本迁移到AEM Commerce Integration Framework(CIF)加载项
exl-id: 0db03a05-f527-4853-b52f-f113bce929cf
source-git-commit: ef4abc74b90da80bfe556306f8ac93078b4958c7
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 1%

---

# {#cif-migration}Experience Manager Cloud Service的迁移指南

本指南可帮助确定您需要更新哪些区域才能进行Experience Manager Cloud Service迁移。

## CIF附加组件

对于Experience Manager作为Cloud Service,CIF加载项是Adobe商务和第三方商务解决方案唯一支持的商务集成解决方案。 CIF附加组件是作为Cloud Service在Experience Manager时自动为客户部署的，无需手动部署。 请参阅[AEM Commerce as a Cloud Service入门](getting-started.md)。

要支持部署CIFAdobe的项目，请提供[AEM CIF核心组件](https://github.com/adobe/aem-core-cif-components)。

AEM 6.5也可通过[软件分发门户](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)获取CIF附加组件。 它兼容，并且提供与Experience Manager的CIF加载项相同的功能 — 无需任何调整。

经典CIF及其依赖项不再可用。 必须根据使用`com.adobe.cq.commerce.api` Java API的此CIF版本的代码，将其调整为CIF附加组件及其原则。

无法再安装以前可用的CIF连接器。 依赖此连接器的代码需要根据CIF附加组件及其原则进行调整。

## 项目结构

了解[AEM项目结构](https://docs.adobe.com/content/help/zh-Hans/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html)以及AEM作为Cloud Service的特性。 将项目设置作为Cloud Service布局调整为AEM。
与AEM 6.5部署相比，以下两个主要区别：

* GraphQL客户端OSGI包&#x200B;**不能再**&#x200B;包含在AEM项目中，而是通过CIF附加组件进行部署
* GraphQL客户端和Graphql数据服务&#x200B;**的OSGI配置不能再**&#x200B;包含到AEM项目中

>[!TIP]
>
>在GitHub上查看[AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)项目。 此项目为AEM提供了Maven配置文件作为Cloud Service和内部部署，其中考虑了不同的框架条件。

## 产品目录

不再支持导入产品目录数据。 使用CIF附加承担者产品和目录请求是通过对外部商务解决方案的实时调用进行按需的。 转到章节集成，了解有关集成商务解决方案的更多信息。

>[!TIP]
>
>如果没有可用的实时API，则应使用包含API的外部产品缓存进行集成。 示例[Magento开源](https://magento.com/products/magento-open-source)。

## 具有AEM渲染的产品目录体验

如果将目录Blueprint与Classic CIF结合使用，则需要更新产品目录工作流。 CIF附加组件现在可使用AEM目录模板即时呈现产品目录体验。 不再需要复制产品数据或产品页面。

## 不可缓存数据和购物互动

对于不可缓存的数据和交互（例如，添加到购物车、搜索）的客户端请求应通过CDN / Dispatcher直接转到商务端点（商务解决方案或集成层）。 删除AEM只是代理的任何调用。
