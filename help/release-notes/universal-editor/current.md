---
title: 通用编辑器2025.07.31发行说明
description: 这些是通用编辑器2025.07.31版的发行说明。
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: 91799e32f363aca268a89a7eebcb5001c5295cc5
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 52%

---


# 通用编辑器2025.07.31发行说明 {#release-notes}

这些是通用编辑器 2025 年 7 月 31 日版本的发行说明。

>[!TIP]
>
>关于 Adobe Experience Manager as a Cloud Service 的最新发行说明，请参阅[本页面](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 新增功能 {#what-is-new}

* [身份验证标题工具栏选项](/help/sites-cloud/authoring/universal-editor/navigation.md#autentication-settings)保持在[版本2025.07.09.](/help/release-notes/universal-editor/2025/2025-07-09.md)中引入的功能切换之后
   * 但是，现在默认启用它。
* [RTE早期采用者的新功能](#new-rte)
   * 添加了深色模式支持。
   * 添加了文本对齐支持。
      * 默认情况下处于禁用状态，并且仅适用于Headless项目
   * 添加了缩进支持。
      * 默认情况下处于禁用状态，并且仅适用于Headless项目
   * 现在在Shift+Enter键上插入分隔符(`<br>`)。

## 早期采用的功能 {#early-adopter}

如果您有兴趣测试这些即将推出的功能并分享您的反馈，请使用与您的 Adobe ID 关联的电子邮件地址发送邮件至您的 Adobe 客户成功经理。

### 新 RTE {#new-rte}

全新的 ProseMirror RTE 现已在右侧面板中提供，链接对话框中引入了页面选择器功能。

### 还原/重做 {#undo-redo}

通用编辑器现已支持内容创作者使用撤销与重做功能。

* 此功能涵盖上下文中的编辑操作、通过属性面板进行的修改，以及区块的新增（或复制）、移动与删除。
* 撤销与重做功能仅限于当前浏览器会话内使用。

## 其他改进 {#other-improvements}

* 早期采用者RTE的修复
   * 按Enter键现在会在列表内创建一个新的列表项(`<li>`)。
* 使用远程DAM时，视频现在可以正确更新。
* 为6.5 LTS添加了服务支持。

## 弃用 {#deprecations}

* `text-input`和`text-area`组件已正式在[版本2025.07.09.](/help/release-notes/universal-editor/2025/2025-07-09.md)中弃用
   * 在 `model-definition.json` 中，请使用文本组件为属性面板创建文本输入字段。
