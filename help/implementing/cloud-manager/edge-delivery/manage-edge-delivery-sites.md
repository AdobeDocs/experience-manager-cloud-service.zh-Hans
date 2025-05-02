---
title: 在 Cloud Manager 中管理 Edge Delivery Sites
description: 了解如何将 CDN 配置添加到 Edge Delivery Site或删除 Edge Delivery Site。
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
exl-id: 960aa3c6-27b9-44b1-81ea-ad8c5bbc99a5
source-git-commit: f8135fea6cb1e43ec27a250d4664b12fa577ed4b
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 76%

---

# 在 Cloud Manager 中管理 Edge Delivery Site {#manage-edge-delivery-sites}

了解如何通过向现有 Site 添加 CDN 配置来管理 Cloud Manager 中的 Edge Delivery Sites。或删除 Edge Delivery Site。

## 将 CDN 配置添加到现有的 Edge Delivery Site {#add-cdn-to-edge-delivery-site}

请参阅[添加 CDN 配置](/help/implementing/cloud-manager/cdn-configurations/add-cdn-config.md)。

## 重命名 Edge Delivery Site (#rename-edge-delivery-site)

在 Adobe Cloud Manager 中，您可能需要重命名 Edge Delivery Site，原因有几个：

* **清晰度和组织性**：更好地描述 Site 的目的或其相关环境（例如，生产、阶段）。
* **避免混淆**：如果使用多个 Sites，重命名可以帮助轻松区分它们，减少将配置或更新应用于错误 Site 的可能性。
* **标准化**：遵循与组织指导方针一致的命名惯例，以便于管理和审核。

**若要重命名 Edge Delivery Site：**

1. 登录 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 上的 Cloud Manager，然后选择合适的程序。
1. 在&#x200B;**[我的程序](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;控制台中，选择配置了 Edge Delivery Services 的程序，您要在其中添加 Edge Delivery Site。
1. 执行以下任一操作：

   * 从&#x200B;**程序概览**&#x200B;页面，单击 **Edge Delivery** 选项卡。在 Edge Delivery Site 表中，单击要重命名其 Site 的行末尾的省略号。单击&#x200B;**重命名**。
   * 在页面左上角，单击![显示菜单图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg)以显示左侧菜单。在&#x200B;**服务**&#x200B;标题下，单击 ![Web 页面图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_WebPages_18_N.svg) **Edge Delivery Sites**。
在 Edge Delivery Site 表中，单击要重命名其 Site 的行末尾的![更多图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)。单击&#x200B;**重命名**。

1. 在&#x200B;**编辑 Edge Delivery Site** 对话框中的 **Site 名称**&#x200B;文本字段内，输入 Site 的新名称。

1. 单击&#x200B;**编辑**。

## 删除 Edge Delivery Site {#delete-edge-delivery-site}

如果删除 Edge Delivery Services Site，则任何相关的 CDN 配置也会被删除。此操作会断开自定义域与 Site 之间的连接。有关详细信息，请参阅 CDN 配置。<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/%5BKT%5D+Cloud+Manager+2024.9.0+Release -->

**要删除 Edge Delivery Site：**

1. 登录 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 上的 Cloud Manager，然后选择合适的程序。
1. 在&#x200B;**[我的程序](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;控制台中，选择配置了 Edge Delivery Services 的程序，您要在其中添加 Edge Delivery Site。
1. 执行以下任一操作：

   * 从&#x200B;**程序概览**&#x200B;页面，单击 **Edge Delivery** 选项卡。在 Edge Delivery Site 表中，单击要移除其 Site 的行末尾的![更多图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)。
单击![删除 Edge Delivery Site 图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Delete_18_N.svg)**删除**，然后再次单击&#x200B;**删除**&#x200B;以确认移除该 Site。

     ![从 Edge Delivery 选项卡添加 Edge Delivery Site](/help/implementing/cloud-manager/assets/cm-eds-delete1.png)

   * 在页面左上角，单击![显示菜单图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg)以显示左侧菜单。在&#x200B;**服务**&#x200B;标题下，单击 ![Edge Delivery Sites 图标的 Web 页面](https://spectrum.adobe.com/static/icons/workflow_18/Smock_WebPages_18_N.svg) **Edge Delivery Sites**。
在 Edge Delivery Site 表中，单击要移除其 Site 的行末尾的![更多图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)。单击![删除 Edge Delivery Site 图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Delete_18_N.svg)**删除**，然后再次单击&#x200B;**删除**&#x200B;以确认移除该 Site。

     ![通过 Edge Delivery Sites 按钮添加 Edge Delivery Site](/help/implementing/cloud-manager/assets/cm-eds-delete2.png)

## 在Helix 4和Helix 5之间管理Edge Delivery站点

使用`/program/{programId}/site/{siteId}` API端点在Helix 4和Helix 5之间迁移Edge Delivery站点。

无法将Helix 4网站的CDN配置自动迁移到Helix 5。 存在此限制是因为客户生产站点可能仍在Helix 4上运行，而其Helix 5版本仍在开发中。

**前提条件**

* `sitename`必须已存在。
* 了解相应的`branchName`、Helix `version`和`repo`值。
* 迁移仅修改`branchName`、Helix `version`和`repo`。 无法更改所有者字段。

**API格式**

```http
PUT /api/program/{programId}/site/{siteId}
```

**请求正文参数**
为Edge Delivery站点创建覆盖，以强制实施请求正文中指定的来源。

```json
{
  "sitename": "<required site name>",
  "branchName": "<git branch>",
  "version": "v4" | "v5",
  "repo": "<git repository name>"
}
```

### 示例1：迁移到Helix 5

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

**源URL结果**
返回具有以下源URL的Edge Delivery网站：

`"origin": "branch--my-website–Teo48.aem.live"`


### 示例2：迁移到Helix 4

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

**源URL结果**
返回具有以下源URL的Edge Delivery Site：

`"origin": "branch--my-website--Teo48.hlx.live"`

### 示例3：将可重写站点迁移到Helix 5

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

**源URL结果**
返回具有以下源URL的Edge Delivery网站：

`"origin": "main--my-repoless-website--Teo48.aem.live"`

## 记录支持工单 {#eds-support-ticket}

{{support-ticket}}
