---
title: 在Cloud Manager中只需单击一下即可创建Edge Delivery站点
description: 了解如何通过单击按钮在Cloud Manager中快速创建Edge Delivery站点。
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 8034fc8454fca41c2430fa1179f80d2d2ab80563
workflow-type: tm+mt
source-wordcount: '657'
ht-degree: 7%

---


# 关于在Cloud Manager中通过一次单击创建Edge Delivery站点 {#about-one-click-edge-delivery-site}

一键式Edge Delivery服务(EDS)旨在自动载入和部署Cloud Manager中的Edge Delivery站点。 它通过单击单个按钮大大简化了流程。 通过单击即可配置所需的基础架构、与GitHub集成以进行版本控制，以及在Google Drive中配置文档和资产存储。

此自动化功能有助于减少设置初始站点所需的手动操作。 它确保在边缘管理内容时实现无缝的工作流和可扩展性，并提高团队的性能。

## 重要概念 {#key-concepts}

使用一次单击创建Edge Delivery站点时的主要概念。

| 关键概念 | 描述 |
| --- | --- |
| 自动Edge部署 | <ul><li>用户可以立即创建和配置Edge Delivery站点。</li><li>它通过使用Cloud Manager与CI/CD工作流的集成，减少或消除了对手动载入流程的需求。</li><li>与Cloud Manager集成，以实现无缝的CI/CD工作流。</li></ul> |
| 与Cloud Manager集成 | <ul><li>使用Cloud Manager的用户界面触发“一键式Edge Delivery”流程。</li><li>提供对自动存储库创建和部署的访问。</li></ul> |
| 基于GitHub的版本控制 | <ul><li>使用预定义的样板模板在组织内创建GitHub存储库以标准化部署。</li><li>AEM机器人链接，以获取内容更新。</li></ul> |
| 文档和资产存储集成 | <ul><li>生成用于存储的Google驱动器文件夹。<li>在存储库上安装AEM代码同步应用程序，以确保无缝同步和部署。</li></li><li>允许多个协作者轻松管理文档。</li></ul> |
| 安全性和可扩展性 | <ul><li>确保遵守企业安全标准。</li><li>在不同的Edge Delivery租户下支持多个Cloud Manager Sites。</li></ul> |



## 只需单击一下即可在Cloud Manager中创建Edge Delivery站点 {#one-click-edge-delivery-site}

若要一键创建一个Adobe Edge Delivery网站，您的组织必须拥有可用的Edge Delivery Services许可证。 此许可证是Adobe Experience Manager (AEM)的一部分，是在Cloud Manager中创建Edge Delivery Services所必需的。

在权限方面，您必须是业务负责人角色的成员或已获得在Cloud Manager中添加或编辑项目的相应权限。 利用此访问级别，您可以管理将Edge Delivery Services集成到程序中的操作。

请参阅 [Cloud Manager 中的 Edge Delivery Services 简介](/help/implementing/cloud-manager/edge-delivery/introduction-to-edge-delivery-services.md)。

必须首先设置正确的AEM机器人配置才能自动更新内容？ 是真的吗？ 假？

**要在Cloud Manager中通过一次单击创建Edge Delivery站点，请执行以下操作：**

1. 通过 [`https://my.cloudmanager.adobe.com`](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的程序。
1. 在页面的左上角，单击![显示菜单图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg)以显示左侧菜单。
1. 在左侧菜单的&#x200B;**服务**&#x200B;标题下，单击![网页图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_WebPages_18_N.svg) **Edge Delivery站点**。
1. 在Edge Delivery页面的&#x200B;**Edge Delivery待办事项列表**&#x200B;对话框中，在&#x200B;**完成先决条件**&#x200B;组框中，单击&#x200B;**设置**。
1. 在&#x200B;**设置Edge Delivery站点**&#x200B;对话框的&#x200B;**项目名称**&#x200B;文本字段中，输入站点名称，然后单击&#x200B;**设置**。
屏幕顶部中央附近会显示一个toast，让您知道Edge Delivery站点配置已开始。
配置完成并验证站点后，站点名称将显示在Edge Delivery页面的**Edge Delivery站点**&#x200B;区域中。

### 浏览新创建的Edge Delivery站点


1. 单击网站名称右侧的Git存储库链接。

发布。

单击站点名称，

进行一些更改，然后发布

在预览中查看页面，然后更改URL以查看实时版本。

添加协作者。


## 预览一键式Edge Delivery网站

## 发布一键式Edge Delivery网站





## 通过一次单击将协作者添加到Edge Delivery网站


































这些增强功能旨在提高自动化程度、简化设置流程并增强 Edge Delivery Services 用户的协作。<!-- CMGR-59362 -->

![单击一下即可创建Edge Delivery站点](/help/implementing/cloud-manager/release-notes/assets/eds-one-click-60.png)

![配置 Edge Delivery 站点对话框](/help/implementing/cloud-manager/release-notes/assets/eds-provision-60.png)