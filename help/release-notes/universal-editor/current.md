---
title: 通用编辑器2054.01.16发行说明
description: 这些是通用编辑器2025.01.16版的发行说明。
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: 14bc45917f56ecf358278848e7e830afb1fedccd
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 8%

---


# 通用编辑器2025.01.16发行说明 {#release-notes}

这些是通用编辑器2025年1月16日版本的发行说明。

>[!TIP]
>
>关于 Adobe Experience Manager as a Cloud Service 的最新发行说明，请参阅[本页。](/help/release-notes/release-notes-cloud/release-notes-current.md)

## 新增功能 {#what-is-new}

* **弃用CORS库&lt; 3.0.0** — 为了确保未来的兼容性和增强安全性，通用编辑器现在仅支持3.0.0或更高版本
  `@Adobe Express/universal-editor-cors`库。
   * 库现在仅通过[`universal-editor-service.adobe.io/cors.js`.](http://universal-editor-service.adobe.io/cors.js)提供
   * 当用户打开使用旧版CORS库的页面时，将会向用户显示弃用通知，提示他们进行更新。
* **登陆页面的扩展点** - [已引入新的扩展点](/help/implementing/universal-editor/customizing.md#extending)，扩展将出现在通用编辑器登陆页面的侧边栏中。
   * 现在，开发人员可以指定扩展是适用于编辑器、登陆页面还是两者，从而提供更好的自定义和可用性。

## 其他改进 {#other-improvements}

* **修复了登陆页面上“最近”项目中的无效URL** — 解决了在通用编辑器登陆页面的“最近”列表中显示的URL损坏的问题。
* **Unified Shell中的主题同步** — 通用编辑器现在将主题与系统的Unified Shell设置动态同步，并在浅色模式和深色模式之间自动调整。
   * 这可以确保跨微前端（包括片段和资产选择器）的一致可视外观。
