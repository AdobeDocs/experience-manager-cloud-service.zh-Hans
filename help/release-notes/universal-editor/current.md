---
title: 通用编辑器2025.06.19发行说明
description: 这些是通用编辑器2025.06.19版的发行说明。
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: 5ffae9e548ca952975b3ea805808e227102ec99f
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 17%

---


# 通用编辑器2025.06.19发行说明 {#release-notes}

这些是通用编辑器2025年6月19日版本的发行说明。

>[!TIP]
>
>关于 Adobe Experience Manager as a Cloud Service 的最新发行说明，请参阅[本页面](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 新增功能 {#what-is-new}

* **支持属性边栏中的多个字段** -
  [容器组件](/help/implementing/universal-editor/field-types.md#container)现在可用于创建多字段属性。
* **支持嵌套属性** - [`name`字段](/help/implementing/universal-editor/field-types.md#nesting)现在支持启用属性嵌套的路径。
* **可调整大小的右侧面板** — 现在可以调整侧面板的大小，以便更好地考虑侧面板中显示的更长内容。

## 早期采用功能 {#early-adopter}

为了获得测试某些即将推出的功能的机会，加入Adobe的率先采用者计划。

### **撤消/重做** {#undo-redo}

“撤消”和“重做”功能现在可供通用编辑器内容作者使用。

* 其中包括在上下文中完成的编辑、通过“属性”面板完成的编辑，以及添加（或复制）、移动和删除块。
* “撤消”和“重做”仅限于当前浏览器会话。

如果您有兴趣测试此新功能并共享您的反馈，请使用与您的 Adobe ID 关联的电子邮件地址向您的 Adobe 帐户成功经理发送电子邮件。

## 其他改进 {#other-improvements}

* 修复了在容器之间移动块时的资源键冲突错误。
* 修复了导致复制容器的最后一个块失败的问题。
* 添加操作下拉列表现在仅列出具有`component-definition.json`文件中定义的合适插件的组件。
* 修复了发布对话框使用的修改日期，在某些情况下，页面未被识别为已修改且未重新发布。
* 修复了编辑容器时取消子节点继承的MSM继承行为。
* `fetchUrl`已修复，正在将移动块从一个容器还原到另一个容器。
