---
title: 对商务集成框架(CIF)附加组件的显着更改
description: 与旧的CIF版本相比，商务集成框架(CIF)发生了显着更改。
exl-id: 5a526960-96a1-421e-9fb0-0825e7df8f32
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 2%

---

# 对商务集成框架(CIF)附加组件的显着更改{#notable-changes}

Adobe Experience Manager as a Cloud Service为管理AEM项目提供了许多新功能和可能性。 要进一步了解这些功能，请访问 [更改Experience Manageras a Cloud Service](/help/release-notes/aem-cloud-changes.md).

本文档重点介绍了商务集成框架(CIF)附加组件与旧CIF版本(主要称为CIF Classic（快速入门）和CIF开源版本)之间的重要区别。

## 安装和更新

AEM CIF加载项将通过Cloud Manager安装。 安装需要CIF信用，但沙箱除外，在沙箱中，CIF可以安装，而无信用。 通过在您的AEM合同中预配CIF附加组件，可自动接收点数。

该加载项将作为常规AEMas a Cloud Service更新的一部分自动更新。

**早期CIF版本**

* CIF Classic:无需安装，CIF是快速入门的一部分。 CIF更新是常规AEM或Service Pack更新的一部分
* AEM内部部署的CIF开源：通过GitHub进行安装。 更新是手动更新/维护工作的一部分。
* 适用于AEM Adobe Managed Services的CIF开源版本：通过客户成功经理进行安装。 更新是手动更新/维护工作的一部分。

## 端点配置

端点通过Cloud Manager UI或其CLI进行配置和更新。

**早期CIF版本**

* CIF Classic:通过AEM中的OSGi配置
* CIF开源：通过CIF配置浏览器

## 部署CIF维尼亚项目

中可用的项目 [Cloud Manager Git存储库](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/managing-code/integrating-with-git.html) 通过 [Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html)

**早期CIF版本**

* CIF Classic:通过AEM包安装
* CIF开源：通过 [Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html?lang=zh-Hans)

## 产品目录数据

通过对支持所需GraphQL API的外部端点的实时调用，按需请求产品目录数据。 这些API支持在任何给定日期访问实时或暂存数据。 无需复制。

**早期CIF版本**

* CIF Classic:通过完整或增量产品导入，将在AEM创作的JCR中导入和保留实时和暂存产品数据。 实时产品数据会复制到AEM发布。

## 具有AEM渲染的产品目录体验

AEM使用已分配给产品和类别的AEM目录模板即时渲染产品目录体验。 无需复制。

**早期CIF版本**

* CIF Classic:AEM作者使用目录Blueprint工具为每个类别/产品创建一个AEM页面。 这些页面会被复制到AEM发布。

>[!NOTE]
>
>有关如何将CIF与AEM托管服务或AEM On-premise结合使用的其他文档，请参阅 [商务集成框架](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/getting-started.html)
