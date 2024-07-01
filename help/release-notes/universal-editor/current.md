---
title: 通用编辑器2024.06.28发行说明
description: 这些是通用编辑器2024.06.28版的发行说明。
feature: Release Information
role: Admin
source-git-commit: cc94ad2ba42707bb7541217f0225b995f64ad84f
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 1%

---


# 通用编辑器2024.06.28发行说明 {#release-notes}

这些是通用编辑器2024年6月28日版本的发行说明。

>[!TIP]
>
>有关Adobe Experience Manager as a Cloud Service的最新发行说明，请参阅 [此页面。](/help/release-notes/release-notes-cloud/release-notes-current.md)

## 新增功能 {#what-is-new}

* **主页**：最近的页面显示为列表，没有预览图像。
* **位置栏**：添加了URL验证增强功能，强制实施HTTPS URL，并支持URL中的哈希以处理哈希路由的应用程序。
* **键盘导航**：页面叠加选择与属性边栏焦点分离，用于改进页面上的键盘导航而不会失去焦点。
* **项目标签**：标签现在使用的回退值 `data-aue-prop` 而不是 `data-aue-type` 以便在叠加和内容树中更清晰地识别。
* **RTE模式**：A **取消** 从属性面板中打开富文本编辑器模式时，该按钮被添加到富文本编辑器模式中。
* **节点上的UE服务**：重新引入了对Universal Editor服务的HTTP支持，因为所有HTTPS连接都在Dispatcher级别终止。
* **内部复制API**：向通用编辑器服务添加了一个用于复制组件的API，允许将来引入工具栏选项来复制和复制内容。

## 错误修复 {#bug-fixes}

* **属性面板痕迹导航**：修复了属性面板中用于深度嵌套项目的痕迹导航菜单，该菜单不会保持打开状态。
* **内容片段选择器**：改进了内容片段选择器，以确保它遵守内容片段模型或 `data-aue-filter`.
* **组件插入**：更正了用于插入在导航到其他页面后未准确更新的新组件的列表。
* **发布状态**：改进了发布状态的处理，以更加一致地发挥作用。
* **其他修复**：此版本还包含各种小修复、技术债务清理、安全增强功能，以及针对整体稳定性和性能的综合测试。
