---
title: 对Commerce Integration Framework (CIF)加载项的显着更改
description: 与旧版CIF相比，Commerce Integration Framework (CIF)发生了显着更改。
exl-id: 5a526960-96a1-421e-9fb0-0825e7df8f32
source-git-commit: b81ac7529e7757fbd9f9fbc48e47e740ab9ecbf3
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 1%

---

# 对Commerce Integration Framework (CIF)加载项的显着更改{#notable-changes}

Adobe Experience Manager as a Cloud Service为管理AEM项目提供了许多新功能和可能性。 要了解有关这些功能的更多信息，请访问链接 [对Experience Manageras a Cloud Service的更改](/help/release-notes/aem-cloud-changes.md).

本文档重点介绍Commerce Integration Framework (CIF)加载项与旧CIF版本(称为CIF Classic (Quickstart)和CIF Open-source)之间的重要差异。

## 安装和更新

AEM CIF加载项通过Cloud Manager进行安装。 安装需要CIF点数，但沙盒除外，因为沙盒可以安装CIF而不需要点数。 通过预配AEM合同中的CIF加载项，可自动接收积分。

加载项在常规AEMas a Cloud Service更新期间自动更新。

**早期CIF版本**

* CIF Classic：无需安装，CIF是快速入门的一部分。 CIF更新是定期AEM或Service Pack更新的一部分
* 内部部署的AEM的CIF开放源代码：通过GitHub安装。 更新是手动更新/维护工作的一部分。
* CIF Open-source for AEM Adobe Managed Services：通过Adobe帐户团队进行安装。 更新是手动更新/维护工作的一部分。

## 端点配置

端点通过Cloud Manager UI或其CLI进行配置和更新。

**早期CIF版本**

* CIF Classic：通过AEM中的OSGi配置
* CIF开源：通过CIF配置浏览器

## 部署CIF Venia项目

中可用的项目 [Cloud Manager Git存储库](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/managing-code/integrating-with-git.html) 和部署，通过 [Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/overview.html)

**早期CIF版本**

* CIF Classic：通过AEM包安装
* CIF开源：通过 [Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/introduction.html)

## 产品目录数据

通过对支持所需GraphQL API的外部端点的实时调用，可按需请求产品目录数据。 这些API支持在任何给定日期访问实时数据或暂存数据。 无需复制。

**早期CIF版本**

* CIF Classic：通过完整或增量产品导入，在AEM Author上导入实时和暂存产品数据并将其保留在JCR中。 将实时产品数据复制到AEM Publish。

## 具有AEM渲染的产品目录体验

AEM使用已分配给产品和类别的AEM目录模板动态呈现产品目录体验。 无需复制。

**早期CIF版本**

* CIF Classic：AEM作者使用目录Blueprint工具为每个类别/产品创建一个AEM页面。 这些页面将复制到AEM Publish。

>[!NOTE]
>
>有关如何将CIF与AEM Managed Service或AEM On-premise结合使用的其他文档，请参阅 [Commerce集成框架](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/getting-started.html)
