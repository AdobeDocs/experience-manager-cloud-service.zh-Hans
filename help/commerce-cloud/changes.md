---
title: Commerce Integration Framework(CIF)加载项的显着更改
description: 与旧版CIF相比，商务集成框架(CIF)发生了显着变化。
exl-id: c136763f-56aa-450e-8796-bc84bf6c205d
translation-type: tm+mt
source-git-commit: 97574c964e757ffa4d108340f6a4d1819050d79a
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 5%

---

# 对Commerce Integration Framework(CIF)Add-on{#notable-changes}的显着更改

Adobe Experience Manager作为一名Cloud Service，为管理AEM项目提供了许多新功能和可能。 要进一步了解这些功能，请按照链接将[更改为Experience Manager](/help/release-notes/aem-cloud-changes.md)。

本文档强调了商务集成框架(CIF)附加组件与旧CIF版本(主要称为CIF Classic(Quickstart))和CIF开放源代码之间的重要区别。

## 安装和更新

AEM CIF加载项通过云管理器安装。 安装需要CIF信用，但沙箱除外，在安装CIF时无需信用。 您的AEM合同中通过CIF附加项预配自动收到积分。

此插件会作为常规AEM的一部分自动更新，作为Cloud Service更新。

**先前的CIF版本**

* CIF经典：无需安装，CIF是快速启动的一部分。 CIF更新是常规AEM或Service Pack更新的一部分
* CIF Open-source for AEM On-ormess:通过GitHub进行安装。 更新是手动更新/维护工作的一部分。
* AEM Adobe Managed Services的CIF开放源：通过客户成功经理进行安装。 更新是手动更新/维护工作的一部分。

## 端点配置

通过Cloud Manager UI或其CLI配置和更新终结点。

**先前的CIF版本**

* CIF经典：通过AEM中的OSGi配置
* CIF开放源：通过CIF配置浏览器

## CIF维尼亚项目的部署

在[Cloud Manager Git存储库](https://docs.adobe.com/content/help/zh-Hans/experience-manager-cloud-service/implementing/managing-code/integrating-with-git.html)中可用的项目，并通过[Cloud Manager](https://docs.adobe.com/content/help/zh-Hans/experience-manager-cloud-service/implementing/deploying/overview.html)完成部署

**先前的CIF版本**

* CIF经典：通过AEM包安装
* CIF开放源：通过[云管理器](https://docs.adobe.com/content/help/zh-Hans/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html)

## 产品目录数据

通过对支持所需GraphQL API的外部端点的实时调用，按需获取产品目录数据。 这些API支持在任何给定日期访问实时或分阶段数据。 无需复制。

**先前的CIF版本**

* CIF经典：通过完全或增量产品导入，实时和分阶段产品数据会在AEM作者的JCR中导入并保留。 将实时产品数据复制到AEM发布。

## 利用AEM渲染实现产品目录体验

AEM使用已分配给产品和类别的AEM目录模板，即时呈现产品目录体验。 无需复制。

**先前的CIF版本**

* CIF经典：AEM作者使用目录蓝图工具为每个类别/产品创建一个AEM页面。 这些页面将被复制到AEM发布。

>[!NOTE]
>
>有关如何将CIF与AEM Managed Service或AEM On-premise一起使用的其他文档，请参阅[Commerce Integration Framework](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/getting-started.html)
