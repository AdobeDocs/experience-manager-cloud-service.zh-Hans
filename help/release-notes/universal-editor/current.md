---
title: 通用编辑器 2054.01.16 发行说明
description: 这些是通用编辑器 2025.01.16 版本的发行说明。
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 77%

---


# 通用编辑器 2025.01.16 发行说明 {#release-notes}

这些是通用编辑器 2025 年 1 月 16 日版本的发行说明。

>[!TIP]
>
>有关Adobe Experience Manager as a Cloud Service的最新发行说明，请参阅[此页面](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 新增功能 {#what-is-new}

* **弃用 CORS 库 &lt; 3.0.0**  - 为确保未来的兼容性并增强安全性，通用编辑器现在仅支持 3.0.0 或更高版本的
  `@Adobe Express/universal-editor-cors` 库。
   * 库现在仅通过[`universal-editor-service.adobe.io/cors.js`](http://universal-editor-service.adobe.io/cors.js)提供。
   * 当用户打开使用旧版本 CORS 库的页面时，会出现弃用通知，以提示他们进行更新。
* **登陆页的扩展点** - [引入了一个新的扩展点](/help/implementing/universal-editor/customizing.md#extending)，以便扩展功能可以显示在通用编辑器登陆页面的侧边栏中。
   * 现在开发人员可以指定扩展是否适用于编辑器、登录页面或两者均适用，从而提供更高的定制性和可用性。

## 其他改进 {#other-improvements}

* **修复了登陆页面上“最近”项目中的无效URL** — 解决了在通用编辑器登陆页面的“最近”列表中显示的URL损坏的问题。
* **Unified Shell 中的主题同步**  - 通用编辑器现在可以将主题与系统的 Unified Shell 设置动态同步，并在明暗模式之间自动调整。
   * 这确保了微前端之间，包括片段和资产选择器在内，具有一致的视觉外观。
