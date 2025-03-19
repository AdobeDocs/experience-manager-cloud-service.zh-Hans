---
title: 通用编辑器2025.03.10发行说明
description: 这些是通用编辑器2025.03.10版的发行说明。
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: b3c98f5e41dbc5e1714d0ed418a317199c735b73
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 10%

---


# 通用编辑器2025.03.10发行说明 {#release-notes}

这些是通用编辑器2025年3月10日版本的发行说明。

>[!TIP]
>
>关于 Adobe Experience Manager as a Cloud Service 的最新发行说明，请参阅[本页面](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 新增功能 {#what-is-new}

* **移动组件：** [在容器之间移动组件](/help/sites-cloud/authoring/universal-editor/authoring.md#reordering-components)现在会观察目标容器的组件筛选器。
   * 不再要求为目标和目标容器设置相同的[筛选器定义](/help/implementing/universal-editor/filtering.md)，以便在容器之间移动组件。
* **锁定的页面：**&#x200B;通用编辑器服务观察页面](/help/sites-cloud/authoring/sites-console/managing-pages.md#locking-a-page)的[锁定状态，并且只写入未锁定或被用户锁定的页面。

## 其他改进 {#other-improvements}

* 已修复对Headless画布的验证问题。

## 弃用 {#deprecation}

* 应不再使用通过npm或`https://unviersal-editor-service.experiencecloud.live/corslib/*`提供的`universal-editor-cors`库。
   * 应改用指向`https://universal-editor-service.adobe.io/cors.js`的脚本标记。
   * 有关如何正确检测页面以便与通用编辑器一起使用的详细信息，请参阅[面向AEM开发人员的通用编辑器概述](/help/implementing/universal-editor/developer-overview.md)。
   * 如果使用错误的方法，用户每天会看到一次弃用消息。
