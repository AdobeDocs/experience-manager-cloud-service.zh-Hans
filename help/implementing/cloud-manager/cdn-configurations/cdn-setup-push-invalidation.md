---
title: 设置推送失效
description: 了解如何配置推送失效以构建您自己的生产CDN。
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
hide: true
source-git-commit: 3941b7f97d434946a3cb796633f306b89e68c0a4
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 2%

---

# 设置推送失效

推送失效可确保在发布时作者所做的内容更新会自动从托管内容交付网络(CDN)中删除，从而仅提供最新的内容。

系统会根据特定URL和缓存标记或键清除内容，从而确保清除过时的版本。

要启用推送失效，必须将特定属性添加到项目的配置文件中。 例如，SharePoint中名为`.helix/config.xlsx`的Microsoft Excel工作簿，或Google Drive中名为`.helix/config`的Google工作表。

以下配置属性定义生产主机的名称和CDN管理的类型：

| 键 | 值 | 个评论 |
| --- | --- | --- |
| `cdn.prod.host` | `<Production Host>` | 生产站点的主机名。 例如：`www.example.com`。 |
| `cdn.prod.type` | 受管 |   |

一旦对配置工作表进行了更改，用户必须使用[Sidekick工具](/help/edge/docs/sidekick.md)来预览和激活它们以应用更新。
