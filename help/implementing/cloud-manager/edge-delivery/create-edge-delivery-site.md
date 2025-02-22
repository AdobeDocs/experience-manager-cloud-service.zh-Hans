---
title: 在Cloud Manager中创建Edge Delivery站点
description: 了解如何通过单击按钮在Cloud Manager中快速创建Edge Delivery站点。
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 0e30cf827e764a356dde304df3124d0be3d2e58b
workflow-type: tm+mt
source-wordcount: '1101'
ht-degree: 30%

---


# 关于在Cloud Manager中创建Edge Delivery站点 {#about-one-click-edge-delivery-site}

创建Edge Delivery站点功能旨在帮助您在Cloud Manager中自动载入和部署Edge Delivery站点。 只需单击一个按钮即可，这大大简化了流程。单击即可设置所需的基础架构，与 GitHub 集成以进行版本控制，并在 Google Drive 中配置您的文档和资产存储。

这种自动化有助于减少设置初始 Site 所需的手动工作量。它可确保无缝的工作流和可扩展性，并在管理边缘内容时提高团队的绩效。

## 重要概念 {#key-concepts}

在Cloud Manager中通过一次单击创建Edge Delivery站点时的主要概念。

| 重要概念 | 描述 |
| --- | --- |
| 自动化 Edge 部署 | <ul><li>用户可以立即创建和配置 Edge Delivery Site。</li><li>通过使用Cloud Manager与CI/CD工作流的集成，它减少或消除了对手动载入流程的需求。</li><li>与 Cloud Manager 集成，实现无缝的 CI/CD 工作流。</li></ul> |
| 与 Cloud Manager 集成 | <ul><li>使用 Cloud Manager 的用户界面，触发一键式 Edge Delivery 流程。</li><li>提供对自动存储库创建和部署的访问。</li></ul> |
| 基于 GitHub 的版本控制 | <ul><li>使用预定义的样板模板在组织内创建 GitHub 存储库以标准化部署。</li><li>与 AEM Bot 链接以进行内容更新。</li></ul> |
| 文档和资产存储集成 | <ul><li>生成 Google Drive 文件夹用于存储。<li>在存储库上安装 AEM Code Sync 应用程序，确保无缝同步和部署。</li></li><li>协作者可以轻松管理文档。</li></ul> |
| 安全性和可扩展性 | <ul><li>确保遵守企业安全性标准。</li><li>在不同的Edge Delivery租户下支持多个Cloud Manager网站。</li></ul> |

<!-- >
## Practical use cases {#use-cases}

| Use case | Description |
| --- | --- |
| Website and application deployment | <ul><li>Automate the hosting and delivery of static or dynamic sites.</li><li>Ensure fast performance through edge caching. </li></ul> |
| API gateway and content delivery | <ul><li>Optimize API responses by caching data at the edge.</li><li>Reduce backend load and improved response times. </li></ul> |
| Real-time content updates | <ul><li>Instant deployment of new content across edge locations.</li><li>Support integration with automated content pipelines. </li></ul> |
| Edge computing workloads | <ul><li>Support serverless computing to process workloads closer to users.</li><li>Reduce latency and enhance performance. </li></ul> |
| Security and governance | <ul><li>Security is provided with integrated DDoS (Distributed Denial of Service) protection and WAF (Web Application Firewall) integration.</li><li>Ensure that content is delivered securely through TLS (Transport Security Layer) encryption. </li></ul> |
-->

## 在 Cloud Manager 中一键创建 Edge Delivery Site {#one-click-edge-delivery-site}

要通过一次单击创建Adobe Edge Delivery网站，您的组织必须具有可用的Edge Delivery Services许可证。 此许可证是 Adobe Experience Manager（AEM）的一部分，并且是在 Cloud Manager 中创建 Edge Delivery Services 所必需的。

在权限方面，您必须是业务负责人角色的成员或被授予适当的权限才能在 Cloud Manager 中添加或编辑程序。此访问级别允许您管理 Edge Delivery Services 与程序的集成。

请参阅 [Cloud Manager 中的 Edge Delivery Services 简介](/help/implementing/cloud-manager/edge-delivery/introduction-to-edge-delivery-services.md)。

<!-- PROPER AEM BOT CONFIGURATIONS MUST BE IN PLACE FIRST FOR AUTOMATIC CONTENT UPDATES? TRUE or FALSE? -->

**在 Cloud Manager 中一键创建 Edge Delivery Site：**

1. 通过 [`https://my.cloudmanager.adobe.com`](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的程序。
1. 在页面左上角，单击![显示菜单图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg)以显示左侧菜单。
1. 在左侧菜单的&#x200B;**项目**&#x200B;标题下，单击&#x200B;**概述**。
1. 在&#x200B;**计划概述**&#x200B;页面上，单击&#x200B;**Edge Delivery**&#x200B;选项卡。
1. 在Edge Delivery页面的&#x200B;**Edge Delivery待办事项列表**&#x200B;对话框中，在&#x200B;**添加Edge Delivery站点**&#x200B;群组框中，单击&#x200B;**立即创建站点**。
1. 在&#x200B;**创建Edge Delivery站点**&#x200B;对话框的&#x200B;**项目名称**&#x200B;文本字段中，输入站点名称，然后单击&#x200B;**立即创建站点**。

   屏幕顶部中央附近会显示一个toast，让您知道Edge Delivery站点配置已开始。

当Cloud Manager完成站点预配和验证时，**站点名称**（您之前输入的项目名称）将出现在Edge Delivery页面的&#x200B;**Edge Delivery站点**&#x200B;列表框中。 此外，存储库URL左侧还会显示一个绿色复选标记。


### 浏览通过一次单击创建的Edge Delivery站点 {#explore-one-click-ed-site}

1. 通过 [`https://my.cloudmanager.adobe.com`](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的程序。
1. 在页面左上角，单击![显示菜单图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg)以显示左侧菜单。
1. 在左侧菜单的&#x200B;**项目**&#x200B;标题下，单击&#x200B;**概述**。
1. 在&#x200B;**计划概述**&#x200B;页面上，单击&#x200B;**Edge Delivery**&#x200B;选项卡。
1. 在Edge Delivery页面上，执行以下任一操作：

   | 要探索的内容 | 步骤 |
   | --- | --- |
   | 站点的GitHub存储库 | <ul><li>在&#x200B;**Edge Delivery站点**&#x200B;列表框的&#x200B;**存储库**&#x200B;列标题下，单击刚刚创建的站点的URL。<br>您可能需要使用用户名或电子邮件地址和密码登录到GitHub。</li> |
   | 发布站点 | <ul><li> 在&#x200B;**Edge Delivery sites**&#x200B;列表框中，单击网站名称最右边的![更多图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)以打开下拉菜单。</li><li>在下拉菜单中单击![发布检查图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_PublishCheck_18_N.svg) **发布站点**。<br>出现toast消息，告知您已成功开始发布网站。</li></ul> |
   | 预览已发布的站点 | <ul><li>在&#x200B;**Edge Delivery站点**&#x200B;列表框的&#x200B;**站点名称**&#x200B;列标题下，单击您刚刚创建和发布的站点的URL。<br>在浏览器的URL地址栏中，请注意，网站的URL以`.page`结尾，表示您看到的是网站的预览。</li><li>若要实时查看网站，请在URL地址栏中手动将`.page`更改为`.live`。</li></ul> |
   | 授予用户访问Google Drive上内容存储库的权限 | <ul><li> 在&#x200B;**Edge Delivery sites**&#x200B;列表框中，单击网站名称最右边的![更多图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)以打开下拉菜单。</li><li>在下拉菜单中单击![用户添加图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_UsersAdd_18_N.svg) **获取对内容存储库的访问权限**。</li><li>在&#x200B;**将协作者添加到您的网站**&#x200B;对话框中，输入参与者的电子邮件地址，然后单击![复选标记图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Checkmark_18_N.svg)。</li><li>根据需要继续添加投稿人电子邮件。</li><li>完成后，单击&#x200B;**添加协作者**。</li><li>要与内容协作者共享链接，请在&#x200B;**Collaboration已成功添加**&#x200B;对话框中，单击&#x200B;**确定**。</li><li>在“Collaboration已成功添加”对话框中，单击![复制图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg)以复制链接并与协作者共享。<br>在共享链接之前，请确认协作者使用与其IMS帐户关联的电子邮件地址登录。 如果其IMS电子邮件帐户不可用，则必须使用添加为协作者的电子邮件地址。 这样做可确保协作者能够访问链接，并在Google驱动器中查看要编辑或更新的内容。</li><li>完成编辑后，在Cloud Manager中单击&#x200B;**发布站点**，如上所述。<br>或者，预览所做的更改，如上所述。</li></ul> |
   | 授予用户访问GitHub上基本存储库的权限 | <ul><li> 在&#x200B;**Edge Delivery sites**&#x200B;列表框中，单击网站名称最右边的![更多图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)以打开下拉菜单。</li><li>在下拉菜单中单击![代码图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Code_18_N.svg) **获取对基础存储库的访问权限**。</li><li>在&#x200B;**访问网站的基本存储库**&#x200B;对话框中，输入协作者的GitHub用户名，然后单击![复选标记图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Checkmark_18_N.svg)。</li><li>根据需要继续添加GitHub用户名。</li><li>完成后，单击&#x200B;**添加协作者**。</li>用户必须向自己的GitHub用户名授予访问权限才能查看存储库。 |




