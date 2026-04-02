---
title: 一键创建您的第一个 Edge Delivery Site
description: 了解如何在 Cloud Manager 中一键快速创建 Edge Delivery Site。
feature: Cloud Manager, Developing
role: Admin, Developer
exl-id: 292bf0b4-990b-4980-b971-91b8aedde3de
source-git-commit: fc9f7f10d1797bda5f31d82005b0afbb6ea1e644
workflow-type: tm+mt
source-wordcount: '1373'
ht-degree: 64%

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

1. 在[experience.adobe.com](https://experience.adobe.com)登录Cloud Manager。
   1. 在&#x200B;**快速访问**&#x200B;部分，单击 **Experience Manager**。
   1. 在左侧面板中点击 **Cloud Manager**。
   1. 选择所需的组织。
1. 在&#x200B;**我的程序**&#x200B;控制台上，单击一个程序。
1. 在页面左上角，单击![显示菜单图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg)以显示左侧菜单。
1. 在左侧菜单中，在&#x200B;**程序**&#x200B;标题下，单击&#x200B;**概述**。
1. 在&#x200B;**程序概述**&#x200B;页面上，单击 **Edge Delivery** 选项卡。
1. 在Edge Delivery页面的&#x200B;**Edge Delivery待办事项列表**&#x200B;对话框中，在&#x200B;**添加Edge Delivery站点**&#x200B;群组框中，单击&#x200B;**立即创建站点**。
1. 在&#x200B;**创建Edge Delivery站点**&#x200B;对话框的&#x200B;**项目名称**&#x200B;文本字段中，输入站点的名称。
1. 在&#x200B;**创作选项**&#x200B;下，选择以下选项之一：
   * **文档创作** — 在Google Drive或SharePoint中创作内容。 此选项是默认选项，不需要AEM环境。
   * **AEM创作(Beta)** — 使用通用编辑器在AEM中创作内容。 如果选择此选项，请在&#x200B;**选择模板**&#x200B;下，为Edge Delivery站点选择初始模板。

   ![选定“Edge Delivery创作”的“创建AEM站点”对话框。](/help/implementing/cloud-manager/edge-delivery/assets/eds-create-aem-authoring.png)

1. 在&#x200B;**创作环境**&#x200B;下拉列表中，选择要用于创作的AEM环境。 您的项目中必须已存在此环境。 仅需要创作层；当Edge Delivery处理投放时，不需要发布层。 请参阅[灵活发布层(Beta)](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#flexible-publish-tier)。

1. 单击&#x200B;**立即创建站点**。

   屏幕顶部中央附近会出现一个提示，通知您 Edge Delivery Site 设置已开始。

当 Cloud Manager 完成 Site 设置和验证后，**Site 名称**（您之前输入的项目名称）将会出现在 Edge Delivery 页面上的 **Edge Delivery Sites** 列表框中。此外，“已验证状态”列的左侧将显示一个绿色圆点。

另请参阅[将内容从AEM作者发布到Edge Delivery](#publish-from-aem-author)。

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
   | 授予用户访问 Google Drive 上的内容存储库的权限 | <ul><li> 在 **Edge Delivery Sites** 列表框中，在 Site 名称的最右侧，单击![更多图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)以打开下拉菜单。</li><li>单击下拉菜单中的![用户添加图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_UsersAdd_18_N.svg) **获取内容存储库的访问权限**。</li><li>在&#x200B;**`Add collaborators to your site`**&#x200B;对话框中，输入投稿人的电子邮件地址，然后单击![复选标记图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Checkmark_18_N.svg)。</li><li>如果需要，继续添加投稿人的电子邮件。</li><li>完成后，单击&#x200B;**添加协作者**。</li><li>要与内容协作者共享链接，请在&#x200B;**协作添加成功**&#x200B;对话框中，单击&#x200B;**确认**。</li><li>在“协作添加成功”对话框中，单击![复制图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg)来复制链接并与您的协作者分享。<br>在共享链接之前，请确认协作者已使用与其 IMS 帐户关联的电子邮件地址登录。如果他们的 IMS 电子邮件帐户不可用，他们必须使用作为协作者添加的电子邮件地址。这样做可确保协作者可以访问该链接，并查看要在 Google Drive 上编辑或更新的内容。</li><li>完成编辑后，在 Cloud Manager 中单击&#x200B;**发布 Site**，如上所述。<br>或者，预览所做的更改，如上所述。</li></ul> |
   | 授予用户访问 GitHub 上的基本存储库的权限 | <ul><li> 在 **Edge Delivery Sites** 列表框中，在 Site 名称的最右侧，单击![更多图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)以打开下拉菜单。</li><li>在下拉菜单中，单击![代码图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Code_18_N.svg) **获取基本存储库的访问权限**。</li><li>在&#x200B;**访问您 Site 的基本存储库**&#x200B;对话框中，输入协作者的 GitHub 用户名，然后单击![复选标记图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Checkmark_18_N.svg)。</li><li>根据需要继续添加 GitHub 用户名。</li><li>完成后，单击&#x200B;**添加协作者**。</li>用户必须授予自己的 GitHub 用户名访问权限才能查看存储库。 |

## 将内容从AEM Author发布到Edge Delivery (Beta) {#publish-from-aem-author}

>[!NOTE]
>
>此处介绍的发布功能位于Beta中。 要加入Beta，请使用您的Adobe组织ID和项目ID向[grp-beta_xwalk-publish_config@adobe.com](mailto:grp-beta_xwalk-publish_config@adobe.com)发送电子邮件。

此功能仅适用于使用Edge Delivery创作选项创建的AEM站点。

在Cloud Manager中创建并&#x200B;**验证** Edge Delivery站点后，您可以使用AEM通用编辑器创作和发布内容。

**要从Cloud Manager访问通用编辑器，请执行以下操作：**

1. 在Edge Delivery选项卡的Edge Delivery站点列表中，找到您的站点。

   ![将内容从AEM作者发布到Edge Delivery](/help/implementing/cloud-manager/edge-delivery/assets/eds-content-source-link.png)

1. 单击网站行中的&#x200B;**内容Source**&#x200B;链接。 该链接将打开AEM通用编辑器页面，您可以在其中创建和编辑网站内容。

**要发布内容：**

* 来自Cloud Manager **的** -

   1. 在&#x200B;**概述**&#x200B;页面的&#x200B;**发布投放**&#x200B;选项卡的&#x200B;**环境**&#x200B;信息卡中，单击突出显示的![信息或信息图标](https://spectrum.adobe.com/static/icons/ui_18/InfoMedium.svg)。

   1. 在信息性弹出窗口中，选择&#x200B;**单击以激活**&#x200B;以在Cloud Manager用户界面中启用发布层配置。

      ![单击以激活发布层配置](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/click-to-activate-publish-tier-capabilities.png)

   1. 在“激活发布层”对话框中，单击&#x200B;**激活**。

      ![激活发布层对话框](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/activate-publish-tier.png)

      激活后，将自动配置发布层。 或者，如果作者尝试直接从AEM用户界面发布内容，则可以自动配置发布层。

      成功激活并设置发布层后，**单击以激活**&#x200B;链接将变暗或不可用。

* 从AEM Author **中** — 在AEM创作界面中，单击&#x200B;**快速发布**，将内容直接发布到您的Edge Delivery网站。 Edge Delivery处理投放时，此操作不需要发布层。

发布后，可在网站的`.page` URL预览内容，或在`.live` URL上实时查看内容。—>

