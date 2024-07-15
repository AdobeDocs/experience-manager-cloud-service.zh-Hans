---
title: 对Commerce integration framework(CIF)加载项的重要更改
description: 与旧版CIF相比，Commerce integration framework(CIF)发生了显着更改。
exl-id: 5a526960-96a1-421e-9fb0-0825e7df8f32
feature: Commerce Integration Framework
role: Admin
source-git-commit: 0e328d013f3c5b9b965010e4e410b6fda2de042e
workflow-type: tm+mt
source-wordcount: '427'
ht-degree: 0%

---

# 对Commerce integration framework(CIF)加载项的显着更改{#notable-changes}

Adobe Experience Manager as a Cloud Service为管理AEM项目提供了许多新功能和可能性。 若要了解有关这些功能的更多信息，请访问链接[对Experience Manageras a Cloud Service](/help/release-notes/aem-cloud-changes.md)的更改。

本文档重点介绍Commerce integration framework(CIF)加载项与旧版CIF(称为CIF Classic (Quickstart)和CIF Open-source)之间的重要差异。

## 安装和更新

AEM CIF加载项是通过Cloud Manager安装的。 安装需要CIF点数，但沙盒除外，在这里无需点数即可安装CIF。 通过在AEM合同中预配CIF加载项来自动接收积分。

此加载项会作为常规AEM as a Cloud Service更新的一部分自动更新。

**以前的CIF版本**

* CIF Classic：无需安装，CIF是快速入门的一部分。 CIF更新是常规AEM或Service Pack更新的一部分
* 适用于AEM内部部署的CIF开放源代码：通过GitHub进行安装。 更新是手动更新/维护工作的一部分。
* CIF Open-source for AEMAdobeManaged Services：通过Adobe客户团队进行安装。 更新是手动更新/维护工作的一部分。

## 端点配置

端点通过Cloud Manager UI或其CLI进行配置和更新。

**以前的CIF版本**

* CIF Classic：通过AEM中的OSGi配置
* CIF开放源代码：通过CIF配置浏览器

## 部署CIF Venia项目

[Cloud Manager Git存储库](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/managing-code/integrating-with-git.html)中可用的项目，并通过[Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/overview.html)完成部署

**以前的CIF版本**

* CIF Classic：通过AEM包安装
* CIF开源：通过[Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/introduction.html)

## 产品目录数据

通过对支持所需GraphQL API的外部端点的实时调用，可按需请求产品目录数据。 这些API支持在任何给定日期访问实时数据或暂存数据。 无需复制。

**以前的CIF版本**

* CIF Classic：通过完全或增量产品导入，在AEM Author上导入实时和暂存产品数据并将这些数据保留在JCR中。 将实时产品数据复制到AEM Publish。

## 具有AEM渲染的产品目录体验

AEM使用已分配给产品和类别的AEM目录模板动态呈现产品目录体验。 无需复制。

**以前的CIF版本**

* CIF Classic：AEM Author使用目录Blueprint工具为每个类别/产品创建一个AEM页面。 这些页面将复制到AEM Publish。

>[!NOTE]
>
>有关如何将CIF与AEM托管服务或AEM内部部署一起使用的其他文档，请参阅[Commerce integration framework](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/getting-started.html)
