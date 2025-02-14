---
title: 在Cloud Manager中只需单击一下即可创建Edge Delivery站点
description: 了解如何通过单击按钮在 Cloud Manager 中快速创建 Edge Delivery Site。
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 8034fc8454fca41c2430fa1179f80d2d2ab80563
workflow-type: tm+mt
source-wordcount: '657'
ht-degree: 71%

---


# 关于在Cloud Manager中通过一次单击创建Edge Delivery站点 {#about-one-click-edge-delivery-site}

一键式 Edge Delivery Service（EDS）旨在自动完成 Cloud Manager 中 Edge Delivery Site 的加入和部署。只需单击一个按钮即可，这大大简化了流程。单击即可设置所需的基础架构，与 GitHub 集成以进行版本控制，并在 Google Drive 中配置您的文档和资产存储。

这种自动化有助于减少设置初始 Site 所需的手动工作量。它可确保无缝的工作流和可扩展性，并在管理边缘内容时提高团队的绩效。

## 重要概念 {#key-concepts}

使用一次单击创建Edge Delivery站点时的主要概念。

| 重要概念 | 描述 |
| --- | --- |
| 自动化 Edge 部署 | <ul><li>用户可以立即创建和配置Edge Delivery站点。</li><li>它通过使用Cloud Manager与CI/CD工作流的集成，减少或消除了对手动载入流程的需求。</li><li>与Cloud Manager集成，以实现无缝的CI/CD工作流。</li></ul> |
| 与 Cloud Manager 集成 | <ul><li>使用 Cloud Manager 的用户界面，触发一键式 Edge Delivery 流程。</li><li>提供对自动存储库创建和部署的访问。</li></ul> |
| 基于 GitHub 的版本控制 | <ul><li>使用预定义的样板模板在组织内创建 GitHub 存储库以标准化部署。</li><li>与 AEM Bot 链接以进行内容更新。</li></ul> |
| 文档和资产存储集成 | <ul><li>生成 Google Drive 文件夹用于存储。<li>在存储库上安装 AEM Code Sync 应用程序，确保无缝同步和部署。</li></li><li>允许多个协作者轻松管理文档。</li></ul> |
| 安全性和可扩展性 | <ul><li>确保遵守企业安全性标准。</li><li>支持不同 Cloud Manager 租户下的多个 Edge Delivery Site。</li></ul> |



## 只需单击一下即可在Cloud Manager中创建Edge Delivery站点 {#one-click-edge-delivery-site}

若要一键创建一个Adobe Edge Delivery网站，您的组织必须拥有可用的Edge Delivery Services许可证。 此许可证是Adobe Experience Manager (AEM)的一部分，是在Cloud Manager中创建Edge Delivery Services所必需的。

在权限方面，您必须是业务负责人角色的成员或被授予适当的权限才能在 Cloud Manager 中添加或编辑程序。此访问级别允许您管理 Edge Delivery Services 与程序的集成。

请参阅 [Cloud Manager 中的 Edge Delivery Services 简介](/help/implementing/cloud-manager/edge-delivery/introduction-to-edge-delivery-services.md)。

是否必须首先完成适当的 AEM BOT 配置才能实现自动内容更新？真？假？

**要在Cloud Manager中通过一次单击创建Edge Delivery站点，请执行以下操作：**

1. 通过 [`https://my.cloudmanager.adobe.com`](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的程序。
1. 在页面左上角，单击![显示菜单图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg)以显示左侧菜单。
1. 在左侧菜单中，**服务**&#x200B;标题下，单击 ![Web 页面图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_WebPages_18_N.svg) **Edge Delivery Site**。
1. 在 Edge Delivery 页面，**Edge Delivery 待办事项列表**&#x200B;对话框，**完成前提条件**&#x200B;组框中，单击&#x200B;**设置**。
1. 在&#x200B;**设置 Edge Delivery Site** 对话框，**程序名称**&#x200B;文本字段中，输入 Site 名称，然后单击&#x200B;**设置**。
屏幕顶部中央附近会出现一个提示，通知您 Edge Delivery Site 设置已开始。
当设置完成并且您的 Site 通过验证后，Site 名称将出现在 Edge Delivery 页面的 **Edge Delivery Site** 区域中。

### 浏览新创建的Edge Delivery站点


1. 单击 Site 名称右侧的 Git 存储库链接。

发布。

单击站点名称，

进行一些更改，然后发布

在预览中查看页面，然后更改 URL 以查看实时版本。

添加协作者。


## 预览一键式Edge Delivery网站

## 发布一键式Edge Delivery网站





## 通过一次单击将协作者添加到Edge Delivery网站


































这些增强功能旨在提高自动化程度、简化设置流程并增强 Edge Delivery Services 用户的协作。<!-- CMGR-59362 -->

![单击一下即可创建Edge Delivery站点](/help/implementing/cloud-manager/release-notes/assets/eds-one-click-60.png)

![配置 Edge Delivery Site 对话框](/help/implementing/cloud-manager/release-notes/assets/eds-provision-60.png)