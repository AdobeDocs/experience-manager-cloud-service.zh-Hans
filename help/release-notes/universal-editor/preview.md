---
title: 通用编辑器预览发行说明
description: 这些是通用编辑器预览版的发行说明。
feature: Release Information
role: Admin
exl-id: e8d031aa-4676-4e45-977b-e5dffcc404c4
source-git-commit: f3ba70f276ab534e0becea47390fe58bf8a825d2
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 35%

---


# 通用编辑器预览发行说明 {#preview}

这些是通用编辑器&#x200B;**预览版**&#x200B;的发行说明。 这些功能当前在通用编辑器的&#x200B;**预览环境**&#x200B;中可用。 这些功能计划于2026年5月7日正式发布。

这些&#x200B;**预览**&#x200B;发行说明是为了方便您了解即将对通用编辑器进行哪些更改，并且您可以通过[切换到预览版本来测试这些更改。](/help/sites-cloud/authoring/universal-editor/navigation.md#user-properties)

>[!TIP]
>
>有关通用编辑器的&#x200B;**当前发行说明**，请参阅文档[通用编辑器发行说明。](/help/release-notes/universal-editor/current.md)

>[!NOTE]
>
>实际发布的内容和发布日期可能会发生变化。

## 即将推出的功能 {#upcoming-features}

* 引入了Service Worker以减少通用编辑器UI和后端系统之间的延迟。
* 内容片段（AEM 6.5、OpenAPI和GraphQL）的所有适配器现在包括用于资源选择器的筛选器，以确保一致性和用户只能选择允许的资源。
* `content:patch`意图现已提供。
* 为了帮助实现无障碍功能，已定义创作流程和地标。

## 其他即将推出的改进 {#other-improvements}

* `assignImageDimensionFields`中不必要的类型声明已删除。
* 修复了`add`操作的服务器端处理迭代字符串值，将其视为对象而不是修补程序的问题。
