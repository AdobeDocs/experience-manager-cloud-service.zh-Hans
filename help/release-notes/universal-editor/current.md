---
title: 通用编辑器2026.05.07发行说明
description: 这些是通用编辑器2026.05.07版的发行说明。
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: 4f66cd6048d7a78bea33c0f9c21017983b9032d5
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 12%

---


# 通用编辑器2026.05.07发行说明 {#release-notes}

这些是通用编辑器2026年5月7日版本的发行说明。

>[!TIP]
>
>如果您想在&#x200B;**即将推出的**&#x200B;通用编辑器发布之前对其功能进行测试，请参阅[通用编辑器预览发行说明。](/help/release-notes/universal-editor/preview.md)

>[!TIP]
>
>有关Adobe Experience Manager as a Cloud Service的最新发行说明，请参阅[此页面。](/help/release-notes/release-notes-cloud/release-notes-current.md)

## 新增功能 {#what-is-new}

* 您现在可以[在编辑器中拖放组件以移动它们。](/help/sites-cloud/authoring/universal-editor/authoring.md#drag-and-drop-move)
* 引入了Service Worker以减少通用编辑器UI和后端系统之间的延迟。
* 内容片段（AEM 6.5、OpenAPI和GraphQL）的所有适配器现在包括用于资源选择器的筛选器，以确保一致性和用户只能选择允许的资源。
* `content:patch`意图现已提供。
* 为了帮助实现无障碍功能，已定义创作流程和地标。

## 其他即将推出的改进 {#other-improvements}

* `assignImageDimensionFields`中不必要的类型声明已删除。
* 修复了`add`操作的服务器端处理迭代字符串值，将其视为对象而不是修补程序的问题。
