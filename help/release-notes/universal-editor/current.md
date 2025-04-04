---
title: 通用编辑器 2025.03.10 发行说明
description: 这些是通用编辑器 2025.03.10 版本的发行说明。
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: beab4f94dc6d78c2b1ad87a02b9fe46dd0438bcc
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 68%

---


# 通用编辑器 2025.03.10 发行说明 {#release-notes}

这些是通用编辑器 2025 年 3 月 10 日版本的发行说明。

>[!TIP]
>
>关于 Adobe Experience Manager as a Cloud Service 的最新发行说明，请参阅[本页面](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 新增功能 {#what-is-new}

* **移动组件：** [在容器之间移动组件](/help/sites-cloud/authoring/universal-editor/authoring.md#reordering-components)现在会注意目标容器的组件过滤器。
   * 要在容器之间移动组件，现在不再要求为 Target 和目标容器都放置相同的[过滤器定义](/help/implementing/universal-editor/filtering.md)。
* **锁定页面：** 通用编辑器服务会观察到[页面的锁定状态](/help/sites-cloud/authoring/sites-console/managing-pages.md#locking-a-page)，并且仅写入未锁定的或被用户锁定的页面。

## 通用编辑器的新扩展 {#extensions}

已在[Extension Manager](https://developer.adobe.com/uix/docs/extension-manager/)上为通用编辑器发布了多个新扩展，增强了创作体验。

* **MSM扩展**：您现在可以使用此扩展中断组件/块的继承并重新实例化。
* **页面属性扩展**：使用此扩展可直接从通用编辑器访问页面的页面属性窗口。
* **工作流扩展**：在页面上使用此扩展进行检测的工作流和内容片段。
* **页面锁定扩展**：使用此扩展可以直接从通用编辑器锁定和解锁页面。

## 其他改进 {#other-improvements}

* 修复了无标头画布的正确验证问题。

## 弃用 {#deprecation}

* 通过 npm 或 `https://unviersal-editor-service.experiencecloud.live/corslib/*` 提供的 `universal-editor-cors` 库不再使用。
   * 应该使用指向 `https://universal-editor-service.adobe.io/cors.js` 的脚本标记。
   * 查看[面向 AEM 开发人员的通用编辑器概述](/help/implementing/universal-editor/developer-overview.md)，详细了解如何为使用通用编辑器正确配置页面。
   * 如果使用了错误的方法，用户将每天看到一次弃用消息。
