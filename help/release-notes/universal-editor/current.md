---
title: 通用编辑器 2024.12.02 发行说明
description: 这些是通用编辑器 2024.12.02 版本的发行说明。
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: 2aae8c63358680758e4f5324f38dea1bc2c47155
workflow-type: ht
source-wordcount: '300'
ht-degree: 100%

---


# 通用编辑器 2024.12.02 发行说明 {#release-notes}

这些是通用编辑器 2024 年 12 月 2 日版本的发行说明。

>[!TIP]
>
>关于 Adob&#x200B;&#x200B;e Experience Manager as a Cloud Service 的最新发行说明，请参阅[本页。](/help/release-notes/release-notes-cloud/release-notes-current.md)

## 新增功能 {#what-is-new}

* **内容树的键盘导航**：现在可以通过键盘完全访问侧面板中的[内容树](/help/sites-cloud/authoring/universal-editor/navigation.md#content-tree-mode)。
   * 作者可以使用标准键盘控件导航并与树视图项进行交互，还需遵守 [WCAG 2.1 可访问性指南](/help/sites-cloud/authoring/page-editor/accessible-content.md)。
   * 此增强功能可确保树中的所有交互元素都可以通过键盘操作，从而提高依赖键盘导航用户的包容性。
* **取消选择可编辑内容**：作者现在可以取消选择页面上先前选择的可编辑元素。
   * 当作者想要查看没有活动选择边框的页面时，这可以消除干扰。
* **片段选择器**：在 AEM as a Cloud Service 实例时，片段引用现在将片段选择器作为内容选取器打开，从而提供改进的功能，例如遵循允许的内容片段模型、搜索内容片段以及改进的整体体验。
   * 这与其他 Adobe UI 保持一致，并增强了一致性。
   * [在 AEM 6.5 环境中，](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-65/content/implementing/developing/headless/universal-editor/introduction)现有的内容选取器仍在使用。
* **容器描述**：[在属性面板中](/help/implementing/universal-editor/field-types.md#container)用于引用内容的[容器组件](/help/sites-cloud/authoring/universal-editor/navigation.md#properties-panel-properties-rail)现在支持描述属性，显示在容器字段上方。
   * 这一附加功能为作者提供了他们正在编辑的分组字段的上下文，提高了清晰度。

## 其他改进 {#other-improvements}

* **富文本字段同步**：属性面板中富文本字段内的原始内容和呈现内容的同步得到了改进，解决了 Edge Delivery Services 项目中富文本内容和呈现方案可能不同的问题。
* **编辑模式事件**：通用编辑器现在可以可靠地发出编辑模式事件，甚至在重新加载远程应用程序后也可以完成。
