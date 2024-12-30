---
title: 为 Edge Delivery 网站设置推送验证
description: 了解如何为 Edge Delivery 网站配置推送失效机制，以确保高效的内容更新和缓存控制。
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
exl-id: 7cded93c-325c-4a4b-8644-e6a2379d5179
source-git-commit: 1a391837ded0af0c5bb436c34a5818f418436308
workflow-type: ht
source-wordcount: '172'
ht-degree: 100%

---

# 设置推送失效机制

推送失效机制可确保作者所做的内容更新在发布时自动从托管的内容分发网络 (CDN) 中移除。这样做可以确保只提供最新的内容。

系统会根据特定的 URL 和缓存标签或键来清除内容，以确保清除过时的版本。

要启用推送失效机制，必须将特定属性添加到项目的配置文件中。例如，SharePoint 中名为 `.helix/config.xlsx` 的 Microsoft Excel 工作簿，或 Google Drive 中名为 `.helix/config` 的 Google Sheet。

以下配置属性定义生产主机的名称和 CDN 管理的类型：

| 键 | 值 | 注释 |
| --- | --- | --- |
| `cdn.prod.host` | `<Production Host>` | 生产网站的主机名。例如 `www.example.com`。 |
| `cdn.prod.type` | 托管 |   |

在对配置表进行更改后，用户必须使用 [Sidekick 工具](/help/edge/docs/sidekick.md)进行预览并激活，以应用更新。

另请参阅[关于 Cloud Manager 中的 Edge Delivery 待办事项列表](/help/implementing/cloud-manager/edge-delivery/introduction-to-edge-delivery-services.md#ed-todo-list)。
