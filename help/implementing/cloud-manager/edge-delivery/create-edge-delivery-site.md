---
title: 一键创建您的第一个 Edge Delivery Site
description: 了解如何在 Cloud Manager 中一键快速创建 Edge Delivery Site。
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
exl-id: 292bf0b4-990b-4980-b971-91b8aedde3de
source-git-commit: bc422429d4a57bbbf89b7af2283b537a1f516ab5
workflow-type: ht
source-wordcount: '945'
ht-degree: 100%

---

# 一键创建您的第一个 Edge Delivery Site{#about-one-click-edge-delivery-site}

一键创建您的第一个 Edge Delivery Site，旨在帮助您自动完成 Cloud Manager 中 Edge Delivery Sites 的加入和部署。只需单击一个按钮即可，这大大简化了流程。单击即可设置所需的基础架构，与 GitHub 集成以进行版本控制，并在 Google Drive 中配置您的文档和资产存储。

这种自动化有助于减少设置初始 Site 所需的手动工作量。它可确保无缝的工作流和可扩展性，并在管理边缘内容时提高团队的绩效。

<!-- Check out this quick 2-minute video for a step-by-step walkthrough on creating your first Edge Delivery site—no hassle, just one click.

>[!VIDEO](https://video.tv.adobe.com/v/3458975?quality=12&learn=on) -->



<!--
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

要一键创建 Adobe Edge Delivery Site，您的组织必须拥有可用的 Edge Delivery Services 许可证。此许可证是 Adobe Experience Manager（AEM）的一部分，并且是在 Cloud Manager 中创建 Edge Delivery Services 所必需的。

在权限方面，您必须是业务负责人角色的成员或被授予适当的权限才能在 Cloud Manager 中添加或编辑程序。此访问级别允许您管理 Edge Delivery Services 与程序的集成。

请参阅 [Cloud Manager 中的 Edge Delivery Services 简介](/help/implementing/cloud-manager/edge-delivery/introduction-to-edge-delivery-services.md)。

<!-- PROPER AEM BOT CONFIGURATIONS MUST BE IN PLACE FIRST FOR AUTOMATIC CONTENT UPDATES? TRUE or FALSE? -->

**在 Cloud Manager 中一键创建 Edge Delivery Site：**

1. 通过 [`https://my.cloudmanager.adobe.com`](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的程序。
1. 在页面左上角，单击![显示菜单图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg)以显示左侧菜单。
1. 在左侧菜单中，在&#x200B;**程序**&#x200B;标题下，单击&#x200B;**概述**。
1. 在&#x200B;**程序概述**&#x200B;页面上，单击 **Edge Delivery** 选项卡。
1. 在 Edge Delivery 页面上的 **Edge Delivery 待办事项列表**&#x200B;对话框中，在&#x200B;**添加 Edge Delivery Site** 组框中，单击&#x200B;**立即创建 Site**。
1. 在&#x200B;**创建 Edge Delivery Site** 对话框的&#x200B;**项目名称**&#x200B;文本字段中，输入 Site 的名称，然后单击&#x200B;**立即创建 Site**。


   屏幕顶部中央附近会出现一个提示，通知您 Edge Delivery Site 设置已开始。

当 Cloud Manager 完成 Site 设置和验证后，**Site 名称**（您之前输入的项目名称）将会出现在 Edge Delivery 页面上的 **Edge Delivery Sites** 列表框中。此外，存储库 URL 的左侧会出现一个绿色复选标记。


### 浏览一键创建的 Edge Delivery Site {#explore-one-click-ed-site}

1. 通过 [`https://my.cloudmanager.adobe.com`](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的程序。
1. 在页面左上角，单击![显示菜单图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg)以显示左侧菜单。
1. 在左侧菜单中，在&#x200B;**程序**&#x200B;标题下，单击&#x200B;**概述**。
1. 在&#x200B;**程序概述**&#x200B;页面上，单击 **Edge Delivery** 选项卡。
1. 在 Edge Delivery 页面上，执行以下任一操作：

   | 需要浏览的内容 | 步骤 |
   | --- | --- |
   | Site 的 GitHub 存储库 | <ul><li>在 **Edge Delivery Sites** 列表框的&#x200B;**存储库**&#x200B;列标题下，单击您刚刚创建的 Site 的 URL。<br>您可能需要使用您的用户名或电子邮件地址和密码登录 GitHub。</li> |
   | 发布 Site | <ul><li> 在 **Edge Delivery Sites** 列表框中，在 Site 名称的最右侧，单击![更多图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)以打开下拉菜单。</li><li>单击下拉菜单中的![发布检查图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_PublishCheck_18_N.svg) **发布 Site**。<br>系统会显示一条提示消息，通知您已成功开始发布 Site。</li></ul> |
   | 预览已发布的 Site | <ul><li>在 **Edge Delivery Sites** 列表框中的 **Site 名称**&#x200B;列标题下，单击您刚刚创建并发布的 Site 的 URL。<br>在浏览器的 URL 地址栏中，请注意该 Site 的 URL 以 `.page` 结尾，表示您正在查看该 Site 的预览版本。</li><li>要实时查看 Site，请在 URL 地址栏中将 `.page` 手动更改到 `.live`。</li></ul> |
   | 授予用户访问 Google Drive 上的内容存储库的权限 | <ul><li> 在 **Edge Delivery Sites** 列表框中，在 Site 名称的最右侧，单击![更多图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)以打开下拉菜单。</li><li>单击下拉菜单中的![用户添加图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_UsersAdd_18_N.svg) **获取内容存储库的访问权限**。</li><li>在&#x200B;**在您的 Site 中添加协作者**&#x200B;对话框中，输入投稿人的电子邮件地址，然后单击![复选标记图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Checkmark_18_N.svg)。</li><li>如果需要，继续添加投稿人的电子邮件。</li><li>完成后，单击&#x200B;**添加协作者**。</li><li>要与内容协作者共享链接，请在&#x200B;**协作添加成功**&#x200B;对话框中，单击&#x200B;**确认**。</li><li>在“协作添加成功”对话框中，单击![复制图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg)来复制链接并与您的协作者分享。<br>在共享链接之前，请确认协作者已使用与其 IMS 帐户关联的电子邮件地址登录。如果他们的 IMS 电子邮件帐户不可用，他们必须使用作为协作者添加的电子邮件地址。这样做可确保协作者可以访问该链接，并查看要在 Google Drive 上编辑或更新的内容。</li><li>完成编辑后，在 Cloud Manager 中单击&#x200B;**发布 Site**，如上所述。<br>或者，预览所做的更改，如上所述。</li></ul> |
   | 授予用户访问 GitHub 上的基本存储库的权限 | <ul><li> 在 **Edge Delivery Sites** 列表框中，在 Site 名称的最右侧，单击![更多图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)以打开下拉菜单。</li><li>在下拉菜单中，单击![代码图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Code_18_N.svg) **获取基本存储库的访问权限**。</li><li>在&#x200B;**访问您 Site 的基本存储库**&#x200B;对话框中，输入协作者的 GitHub 用户名，然后单击![复选标记图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Checkmark_18_N.svg)。</li><li>根据需要继续添加 GitHub 用户名。</li><li>完成后，单击&#x200B;**添加协作者**。</li>用户必须授予自己的 GitHub 用户名访问权限才能查看存储库。 |
