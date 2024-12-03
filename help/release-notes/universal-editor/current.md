---
title: 通用编辑器2024.12.02发行说明
description: 这些是通用编辑器2024.12.02版的发行说明。
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: 2aae8c63358680758e4f5324f38dea1bc2c47155
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 7%

---


# 通用编辑器2024.12.02发行说明 {#release-notes}

这些是通用编辑器2024年12月2日版本的发行说明。

>[!TIP]
>
>关于 Adob&#x200B;&#x200B;e Experience Manager as a Cloud Service 的最新发行说明，请参阅[本页。](/help/release-notes/release-notes-cloud/release-notes-current.md)

## 新增功能 {#what-is-new}

* **内容树的键盘导航**： [可在侧面板中使用的内容树](/help/sites-cloud/authoring/universal-editor/navigation.md#content-tree-mode)现在可通过键盘完全访问。
   * 作者可以使用标准键盘控件导航树视图项目并与之交互，请遵守[WCAG 2.1准则](/help/sites-cloud/authoring/page-editor/accessible-content.md)以获得辅助功能。
   * 此增强功能可确保树中的所有交互元素均可使用键盘操作，从而提高依赖键盘导航的用户包容性。
* **取消选择可编辑内容**：作者现在可以取消选择页面上以前选择的可编辑元素。
   * 当作者希望查看没有活动选择边框的页面时，这可以消除干扰。
* **片段选择器**：在AEM as a Cloud Service实例上，片段引用现在会打开片段选择器作为内容选择器，从而提供改进的功能，例如遵循允许的内容片段模型、搜索内容片段以及改进的整体体验。
   * 这与其他AdobeUI保持一致，并增强了一致性。
   * [对于AEM 6.5环境，](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-65/content/implementing/developing/headless/universal-editor/introduction)现有内容选取器仍在使用中。
* **容器描述**： [在[属性面板](/help/sites-cloud/authoring/universal-editor/navigation.md#properties-panel-properties-rail)中用于引用内容的容器组件](/help/implementing/universal-editor/field-types.md#container)现在支持显示在容器字段上方的描述属性。
   * 此添加内容通过向作者提供有关他们正在编辑的分组字段的上下文而提高了清晰度。

## 其他改进 {#other-improvements}

* **富文本字段同步**：属性面板中富文本字段内原始内容和呈现内容的同步已得到改进，解决了富文本内容和呈现呈现方式可能不同的Edge Delivery Services项目中的问题。
* **编辑模式事件**：通用编辑器现在可靠地发出编辑模式事件，包括在重新加载远程应用程序之后。
