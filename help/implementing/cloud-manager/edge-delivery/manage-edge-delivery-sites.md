---
title: 在 Cloud Manager 中管理 Edge Delivery Sites
description: 了解如何将 CDN 配置添加到 Edge Delivery Site 或删除 Edge Delivery Site。
feature: Cloud Manager, Developing
role: Admin, Developer
exl-id: 960aa3c6-27b9-44b1-81ea-ad8c5bbc99a5
source-git-commit: fc9f7f10d1797bda5f31d82005b0afbb6ea1e644
workflow-type: tm+mt
source-wordcount: '1103'
ht-degree: 64%

---

# 在 Cloud Manager 中管理 Edge Delivery Site {#manage-edge-delivery-sites}

了解如何通过向现有 Site 添加 CDN 配置来管理 Cloud Manager 中的 Edge Delivery Sites。或删除 Edge Delivery Site。

## 将域映射添加到一个现有的 Edge Delivery Site {#add-cdn-to-edge-delivery-site}

请参阅[添加域映射](/help/implementing/cloud-manager/domain-mappings/add-domain-mapping.md)。

## 重命名 Edge Delivery Site (#rename-edge-delivery-site)

在 Adobe Cloud Manager 中，您可能需要重命名 Edge Delivery Site，原因有几个：

* **清晰度和组织性**：更好地描述 Site 的目的或其相关环境（例如，生产、阶段）。
* **避免混淆**：如果使用多个 Sites，重命名可以帮助轻松区分它们，减少将配置或更新应用于错误 Site 的可能性。
* **标准化**：遵循与组织指导方针一致的命名惯例，以便于管理和审核。

**若要重命名 Edge Delivery Site：**

1. 登录 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 上的 Cloud Manager，然后选择合适的程序。
1. 在&#x200B;**[我的程序](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;控制台中，选择配置了 Edge Delivery Services 的程序，您要在其中添加 Edge Delivery Site。
1. 执行以下任一操作：

   * 从&#x200B;**程序概述**&#x200B;页面，单击 **Edge Delivery** 选项卡。在 Edge Delivery Site 表中，单击要重命名其 Site 的行末尾的省略号。单击&#x200B;**重命名**。
   * 在页面左上角，单击![显示菜单图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg)以显示左侧菜单。在&#x200B;**服务**&#x200B;标题下，单击 ![Web 页面图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_WebPages_18_N.svg) **Edge Delivery Sites**。
在 Edge Delivery Site 表中，单击要重命名其 Site 的行末尾的![更多图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)。单击&#x200B;**重命名**。

1. 在&#x200B;**编辑 Edge Delivery Site** 对话框中的 **Site 名称**&#x200B;文本字段内，输入 Site 的新名称。
1. 单击&#x200B;**编辑**。


## 为Edge Delivery站点(Beta)激活发布层 {#activate-publish-tier-for-eds}

>[!NOTE]
>
>此处介绍的发布功能位于Beta中。 要加入Beta，请使用您的Adobe组织ID和项目ID向[grp-beta_xwalk-publish_config@adobe.com](mailto:grp-beta_xwalk-publish_config@adobe.com)发送电子邮件。

此功能仅适用于启用了灵活发布层功能的程序中使用&#x200B;**AEM创作**&#x200B;选项创建的Edge Delivery站点。

如果您的Edge Delivery站点使用AEM创作，则默认情况下不配置发布层，因为Edge Delivery处理内容交付。 但是，如果网站需要，您可以随时激活发布层。 例如，如果您需要与Edge Delivery一起支持传统AEM发布。

在Cloud Manager中创建Edge Delivery站点且其状态显示&#x200B;**已验证**&#x200B;后，您可以使用AEM通用编辑器创作和发布内容。

**要从Cloud Manager访问通用编辑器，请执行以下操作：**

1. 在Edge Delivery选项卡的Edge Delivery站点列表中，找到您的站点。

   ![将内容从AEM作者发布到Edge Delivery。](/help/implementing/cloud-manager/edge-delivery/assets/eds-content-source-link.png)

1. 单击网站行中的&#x200B;**内容Source**&#x200B;链接。 该链接将打开AEM通用编辑器页面，您可以在其中创建和编辑站点的内容。—>

**要激活Edge Delivery网站的发布层，请执行以下操作：**

1. 在&#x200B;**项目概述**&#x200B;页面的&#x200B;**发布投放**&#x200B;选项卡下的&#x200B;**环境**&#x200B;信息卡中，单击“信息”图标。

1. 在信息性弹出窗口中，在&#x200B;**发布URL**&#x200B;下，选择&#x200B;**单击以激活**&#x200B;以在Cloud Manager用户界面中启用发布层配置。

   ![单击以激活发布层配置](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/click-to-activate-publish-tier-capabilities.png)

1. 在“激活发布层”对话框中，单击&#x200B;**激活**。

   ![激活发布层对话框](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/activate-publish-tier.png)

   激活后，将自动配置发布层。 或者，如果作者尝试直接从AEM用户界面发布内容，则可以自动配置发布层。

   成功激活并设置发布层后，**单击以激活**&#x200B;链接将变暗或不可用。

* 从AEM Author **中** — 在AEM创作界面中，单击&#x200B;**快速发布**，将内容直接发布到您的Edge Delivery网站。 Edge Delivery处理投放时，此操作不需要发布层。

发布后，可在网站的`.page` URL预览内容，或在`.live` URL上实时查看内容。—>

>[!NOTE]
>
>激活发布层会将发布基础架构添加到您的环境。 此功能可能会影响您项目的资源消耗。 要配置是否在程序级别需要发布层，请参阅[灵活发布层(Beta)](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#flexible-publish-tier)。


## 删除 Edge Delivery Site {#delete-edge-delivery-site}

如果删除 Edge Delivery Services Site，则任何相关的 CDN 配置也会被删除。此操作会断开自定义域与 Site 之间的连接。有关详细信息，请参阅 CDN 配置。<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/%5BKT%5D+Cloud+Manager+2024.9.0+Release -->

**要删除 Edge Delivery Site：**

1. 登录 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 上的 Cloud Manager，然后选择合适的程序。
1. 在&#x200B;**[我的程序](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;控制台中，选择配置了 Edge Delivery Services 的程序，您要在其中添加 Edge Delivery Site。
1. 执行以下任一操作：

   * 从&#x200B;**程序概述**&#x200B;页面，单击 **Edge Delivery** 选项卡。在 Edge Delivery Site 表中，单击要移除其 Site 的行末尾的![更多图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)。
单击![删除 Edge Delivery Site 图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Delete_18_N.svg)**删除**，然后再次单击&#x200B;**删除**&#x200B;以确认移除该 Site。

     ![从 Edge Delivery 选项卡添加 Edge Delivery Site](/help/implementing/cloud-manager/assets/cm-eds-delete1.png)

   * 在页面左上角，单击![显示菜单图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg)以显示左侧菜单。在&#x200B;**服务**&#x200B;标题下，单击 ![Edge Delivery Sites 图标的 Web 页面](https://spectrum.adobe.com/static/icons/workflow_18/Smock_WebPages_18_N.svg) **Edge Delivery Sites**。
在 Edge Delivery Site 表中，单击要移除其 Site 的行末尾的![更多图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)。单击![删除 Edge Delivery Site 图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Delete_18_N.svg)**删除**，然后再次单击&#x200B;**删除**&#x200B;以确认移除该 Site。

     ![通过 Edge Delivery Sites 按钮添加 Edge Delivery Site](/help/implementing/cloud-manager/assets/cm-eds-delete2.png)

## 管理 Helix 4 和 Helix 5 之间的 Edge Delivery Site

使用`/program/{programId}/site/{siteId}` API 端点在 Helix 4 和 Helix 5 之间迁移 Edge Delivery Site。

>[!IMPORTANT]
>
>Helix 4 网站的 CDN 配置无法自动迁移到 Helix 5。存在这种限制是因为客户生产 Sites 可能仍在 Helix 4 上运行，而他们的 Helix 5 版本仍在开发中。

**先决条件**

* `sitename` 必须已经存在。
* 了解适当的 `branchName`、Helix `version` 和 `repo` 值。
* 迁移仅更改 `branchName`、Helix `version` 和 `repo`。所有者字段无法更改。

**API 格式**

```http
PUT /api/program/{programId}/site/{siteId}
```

**请求正文参数**
为 EEdge Delivery Site 创建一个覆盖，以强制执行请求正文中指定的来源。

```json
{
  "sitename": "<required site name>",
  "branchName": "<git branch>",
  "version": "v4" | "v5",
  "repo": "<git repository name>"
}
```

### 示例 1：迁移到 Helix 5

**http**

```http
PUT /api/program/{programId}/site/{siteId}
```

**json**

```json
{
  "sitename": "test-site-new-helix5",
  "branchName": "branch",
  "version": "v5",
  "repo": "my-website"
}
```

**来源 URL 结果**
返回具有以下来源 URL 的 Edge Delivery Site：

`"origin": "branch--my-website–Teo48.aem.live"`


### 示例 2：迁移到 Helix 4

**http**

```http
PUT /api/program/{programId}/site/{siteId}
```

**json**

```json
{
  "sitename": "test-site-new-helix4",
  "branchName": "branch",
  "version": "v4",
  "repo": "my-website"
}
```

**来源 URL 结果**
返回具有以下来源 URL 的 Edge Delivery Site：

`"origin": "branch--my-website--Teo48.hlx.live"`

### 示例 3：将无重复 Site 迁移到 Helix 5

**http**

```http
PUT /api/program/{programId}/site/{siteId}
```

**json**

```json
{
  "sitename": "test-reposless-website",
  "branchName": "main",
  "version": "v5",
  "repo": "my-reposless-website"
}
```

**来源 URL 结果**
返回具有以下来源 URL 的 Edge Delivery Site：

`"origin": "main--my-repoless-website--Teo48.aem.live"`

## 记录支持工单 {#eds-support-ticket}

{{support-ticket}}
