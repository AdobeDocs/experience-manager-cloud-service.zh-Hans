---
title: 迁移到AEM Commerce Integration Framework(CIF)附加组件
description: 如何从旧版本迁移到AEM Commerce Integration Framework(CIF)加载项
exl-id: 0db03a05-f527-4853-b52f-f113bce929cf
source-git-commit: 05a412519a2d2d0cba0a36c658b8fed95e59a0f7
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 27%

---

# 适用于Experience Manager Cloud Service的迁移指南 {#cif-migration}

本指南帮助确定您需要为 Experience Manager Cloud Service 迁移而更新的领域。

## CIF附加组件

对于 Experience Manager as a Cloud Service，CIF 加载项是 Adobe Commerce 和第三方 Commerce 唯一支持的 Commerce 集成解决方案。CIF 加载项自动为 Experience Manager as a Cloud Service 上的客户部署，无需手动部署。请参阅 [AEM Commerce as a Cloud Service 快速入门](getting-started.md)。

支持部署CIFAdobe的项目 [AEM CIF核心组件](https://github.com/adobe/aem-core-cif-components).

CIF 加载项可用于 AEM 6.5 以及通过[软件分发门户](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)使用。它是兼容的，提供了与 Experience Manager as a Cloud Service 的 CIF 加载项相同的功能，无需调整。

Classic CIF 及其依赖项不再可用。依赖此CIF版本的代码使用 `com.adobe.cq.commerce.api` 必须根据CIF附加组件及其原则调整Java API。

无法再安装以前可用的CIF连接器。 依赖此连接器的代码需要根据CIF附加组件及其原则进行调整。

## 项目结构

了解 [AEM项目结构](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html) 以及AEMas a Cloud Service的特性。 将项目设置调整为AEMas a Cloud Service布局。
与AEM 6.5部署相比，以下两个主要区别：

* GraphQL客户端OSGI包 **必须** 包含到AEM项目中，则会通过CIF附加组件进行部署
* GraphQL客户端和Graphql数据服务的OSGI配置 **必须** 已包含到AEM项目中

>[!TIP]
>
>查看 [AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia) 项目。 此项目为AEMas a Cloud Service部署和内部部署提供了Maven配置文件，这些部署考虑了不同的框架条件。

## 产品目录

不再支持导入产品目录数据。 使用CIF附加承担者产品和目录请求是通过对外部商务解决方案的实时调用进行按需的。 转到章节集成，了解有关集成商务解决方案的更多信息。

>[!TIP]
>
>如果没有可用的实时API，则应使用包含API的外部产品缓存进行集成。 示例 [Magento开源](https://business.adobe.com/products/magento/open-source.html).

## 具有AEM渲染的产品目录体验

如果将目录Blueprint与Classic CIF结合使用，则需要更新产品目录工作流。 CIF附加组件现在可使用AEM目录模板即时呈现产品目录体验。 不再需要复制产品数据或产品页面。

## 不可缓存数据和购物互动

对于不可缓存的数据和交互（例如，添加到购物车、搜索）的客户端请求应通过CDN / Dispatcher直接转到商务端点（商务解决方案或集成层）。 删除AEM只是代理的任何调用。
