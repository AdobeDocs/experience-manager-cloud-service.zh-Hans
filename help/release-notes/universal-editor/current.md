---
title: 通用编辑器 2025.06.19 发行说明
description: 这些是通用编辑器 2025.06.19 版本的发行说明。
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: 5ffae9e548ca952975b3ea805808e227102ec99f
workflow-type: ht
source-wordcount: '297'
ht-degree: 100%

---


# 通用编辑器 2025.06.19 发行说明 {#release-notes}

这些是通用编辑器 2025.06.19 版本的发行说明。

>[!TIP]
>
>关于 Adobe Experience Manager as a Cloud Service 的最新发行说明，请参阅[本页面](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 新增功能 {#what-is-new}

* **属性侧边栏支持多字段功能**—
  [容器组件](/help/implementing/universal-editor/field-types.md#container)现在可用于创建多字段属性。
* **支持嵌套属性**— [`name` 字段](/help/implementing/universal-editor/field-types.md#nesting)现已支持路径形式，可实现属性嵌套。
* **可调整大小的右侧面板** — 现在可根据侧边栏中显示的较长内容调整其宽度，以获得更佳的查看体验。

## 早期采用的功能 {#early-adopter}

加入 Adobe 早期采用者计划，即有机会测试一些即将推出的功能。

### **还原/重做** {#undo-redo}

通用编辑器现已支持内容创作者使用撤销与重做功能。

* 此功能涵盖上下文中的编辑操作、通过属性面板进行的修改，以及区块的新增（或复制）、移动与删除。
* 撤销与重做功能仅限于当前浏览器会话内使用。

如果您有兴趣测试此新功能并共享您的反馈，请使用与您的 Adobe ID 关联的电子邮件地址向您的 Adobe 客户成功经理发送电子邮件。

## 其他改进 {#other-improvements}

* 已修复在容器间移动区块时出现的资源键冲突错误。
* 已修复复制容器中最后一个区块时可能失败的问题。
* “添加操作”下拉菜单现在仅显示在 `component-definition.json` 文件中已定义了相应插件的组件。
* 已修复发布对话框中用于识别修改状态的日期问题，该问题曾导致在某些情况下页面未被识别为已修改，从而未被重新发布。
* 已修复 MSM 继承行为的问题：此前编辑容器会导致其子节点的继承关系被取消。
* 已修复 `fetchUrl` 问题，恢复了区块在不同容器之间移动的功能。
