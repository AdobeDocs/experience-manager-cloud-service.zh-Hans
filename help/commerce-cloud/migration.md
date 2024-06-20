---
title: 迁移到AEMCommerce integration framework(CIF)加载项
description: 如何从旧版本迁移到AEMCommerce integration framework(CIF)加载项
exl-id: 0db03a05-f527-4853-b52f-f113bce929cf
feature: Commerce Integration Framework
role: Admin
source-git-commit: 0e328d013f3c5b9b965010e4e410b6fda2de042e
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 20%

---

# Experience Manager Cloud Service迁移指南 {#cif-migration}

本指南帮助确定您需要为 Experience Manager Cloud Service 迁移而更新的领域。

## CIF加载项

对于Experience Manageras a Cloud Service，CIF加载项是唯一受Adobe Commerce和第三方商务解决方案支持的商务集成解决方案。 CIF 加载项自动为 Experience Manager as a Cloud Service 上的客户部署，无需手动部署。请参阅 [AEM Commerce as a Cloud Service 快速入门](getting-started.md)。

要支持部署CIF的项目，请提供Adobe [AEM CIF核心组件](https://github.com/adobe/aem-core-cif-components).

CIF 加载项可用于 AEM 6.5 以及通过[软件分发门户](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)使用。它是兼容的，提供了与 Experience Manager as a Cloud Service 的 CIF 加载项相同的功能，无需调整。

Classic CIF 及其依赖项不再可用。依赖此CIF版本的代码，使用 `com.adobe.cq.commerce.api` 必须将Java API调整为CIF加载项及其原则。

无法再安装以前可用的CIF连接器。 依赖此连接器的代码需要调整为CIF加载项及其原则。

## 项目结构

了解 [AEM项目结构](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html) 以及AEMas a Cloud Service的特点。 使项目设置适应AEMas a Cloud Service布局。
与AEM 6.5部署相比，以下两个主要区别：

* GraphQL客户端OSGI捆绑包 **不得** 将被继续包含到AEM项目中，它是通过CIF加载项部署的
* GraphQL客户端和Graphql数据服务的OSGI配置 **不得** 已包含在AEM项目中

>[!TIP]
>
>查看 [AEM Venia参考存储](https://github.com/adobe/aem-cif-guides-venia) 项目。 此项目为AEMas a Cloud Service部署和内部部署提供Maven配置文件，其中考虑到不同的框架条件。

## 产品目录

不再支持导入产品目录数据。 使用CIF附加组件主参与者产品和目录请求是通过实时调用外部商务解决方案来按需发出的。 转到集成一章，了解有关集成商业解决方案的更多信息。

>[!TIP]
>
>如果没有可用的实时API，则应使用具有API的外部产品缓存进行集成。 示例 [Magento开源](https://business.adobe.com/products/magento/open-source.html).

## 具有AEM渲染的产品目录体验

如果您将目录Blueprint与Classic CIF一起使用，则需要更新产品目录工作流程。 CIF加载项现在可使用AEM目录模板动态呈现产品目录体验。 不再需要复制产品数据或产品页面。

## 不可缓存的数据和购物交互

对不可缓存的数据和交互的客户端请求（例如，添加到购物车、搜索）应通过CDN/Dispatcher直接转到商业端点（商业解决方案或集成层）。 删除AEM只是代理的任何调用。
