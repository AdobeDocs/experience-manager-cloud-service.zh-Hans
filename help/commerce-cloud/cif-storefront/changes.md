---
title: 对Commerce integration framework (CIF)加载项的重要更改
description: 与旧版CIF相比，Commerce integration framework (CIF)发生了显着更改。
exl-id: 5a526960-96a1-421e-9fb0-0825e7df8f32
feature: Commerce Integration Framework
role: Admin
source-git-commit: 856442039fcd25ec675a6258d182f7a35f590c3c
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 0%

---


# 对Commerce integration framework (CIF)加载项的显着更改 {#notable-changes}

Adobe Experience Manager as a Cloud Service为管理AEM项目提供了许多新功能和可能性。 要了解有关这些功能的更多信息，请访问链接[对Experience Manager as a Cloud Service的更改。](/help/release-notes/aem-cloud-changes.md)

本文档重点介绍Commerce integration framework (CIF)加载项与旧版CIF(称为CIF Classic (Quickstart)和CIF开放源代码)之间的重要差异。

## 安装和更新

AEM CIF加载项是通过Cloud Manager安装的。 安装需要CIF点数，但沙盒除外，因为沙盒无需点数即可安装CIF。 通过在AEM合同中配置CIF加载项来自动接收积分。

此加载项会作为常规AEM as a Cloud Service更新的一部分自动更新。

### 早期CIF版本 {#previous-versions-installation}

* CIF Classic：无需安装，CIF是快速入门的一部分。 CIF更新是常规AEM或Service Pack更新的一部分
* 适用于AEM的CIF开源内部部署：通过GitHub安装。 更新是手动更新/维护工作的一部分。
* 适用于AEM的CIF开放源Adobe Managed Services：通过Adobe客户团队安装。 更新是手动更新/维护工作的一部分。

## 端点配置 {#endpoint-configuration}

端点通过Cloud Manager UI或其CLI进行配置和更新。

### 早期CIF版本 {#previous-versions-endpoint}

* CIF Classic：通过AEM中的OSGi配置
* CIF开放源代码：通过CIF Configuration Browser

## 部署CIF Venia项目 {#venia-project}

[Cloud Manager Git存储库](/help/implementing/cloud-manager/managing-code/integrating-with-git.md)中提供了项目，并通过[Cloud Manager.](/help/implementing/deploying/overview.md)完成了部署。

### 早期CIF版本 {#previous-versions-venia}

* CIF Classic：通过AEM包安装
* CIF开源：通过[Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/introduction.html)

## 产品目录数据 {#product-catalog-data}

通过对支持所需GraphQL API的外部端点的实时调用，可按需请求产品目录数据。 这些API支持在任何给定日期访问实时数据或暂存数据。 无需复制。

### 早期CIF版本 {#previous-versions-catalog}

* CIF Classic：通过完全或增量产品导入，在AEM Author上导入实时和暂存产品数据并将这些数据保留在JCR中。 将实时产品数据复制到AEM Publish。

## 具有AEM渲染的产品目录体验 {#catalog-experiences}

AEM使用已分配给产品和类别的AEM目录模板动态呈现产品目录体验。 无需复制。

### 早期CIF版本 {#previous-cif-versions}

* CIF Classic：AEM Author使用目录Blueprint工具为每个类别/产品创建一个AEM页面。 这些页面将复制到AEM Publish。

>[!NOTE]
>
>有关如何将CIF与AEM Managed Service或AEM On-premise结合使用的其他文档，请参阅[Commerce integration framework。](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/getting-started.html)
