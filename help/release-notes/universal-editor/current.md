---
title: 通用编辑器2025.09.04发行说明
description: 这些是通用编辑器2025.09.04版的发行说明。
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: 0c380e0faca1db0966d22d056dd1f824a731a7bc
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 67%

---


# 通用编辑器2025.09.04发行说明 {#release-notes}

这些是 2025 年 9 月 4 日发布的通用编辑器的发行说明。

>[!TIP]
>
>关于 Adobe Experience Manager as a Cloud Service 的最新发行说明，请参阅[本页面](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 新增功能 {#what-is-new}

* [早期采用者可以复制并粘贴](#copy-paste)

### 还原/重做 {#undo-redo}

通用编辑器现已支持内容创作者使用撤销与重做功能。

* 此功能涵盖上下文中的编辑操作、通过属性面板进行的修改，以及区块的新增（或复制）、移动与删除。
* 撤销与重做功能仅限于当前浏览器会话内使用。

## 早期采用的功能 {#early-adopter}

如果您有兴趣测试这些即将推出的功能并分享您的反馈，请使用与您的 Adobe ID 关联的电子邮件地址发送邮件至您的 Adobe 客户成功经理。

### 新 RTE {#new-rte}

全新的 ProseMirror RTE 现已在右侧面板中提供，链接对话框中引入了页面选择器功能。

### 复制/粘贴 {#copy-paste}

内容作者现在可以在同一页面中复制和粘贴组件。

## 其他改进 {#other-improvements}

* 编辑器工具栏的样式已更新，以更好地与即将推出的新RTE保持一致。
* 已恢复资产选取器对话框中的筛选器。

## 弃用 {#deprecations}

* `text-input` 和 `text-area` 组件已在[发行版本 2025.07.09](/help/release-notes/universal-editor/2025/2025-07-09.md) 中正式弃用。
   * 在 `model-definition.json` 中，请使用文本组件为属性面板创建文本输入字段。
