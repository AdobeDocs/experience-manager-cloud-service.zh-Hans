---
title: 通用编辑器2025.07.09发行说明
description: 这些是通用编辑器2025.07.09版的发行说明。
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: 199ee7e11f6706773bd426c3d27236d6ea791a6c
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 18%

---


# 通用编辑器2025.07.09发行说明 {#release-notes}

这些是通用编辑器2025年7月9日版本的发行说明。

>[!TIP]
>
>关于 Adobe Experience Manager as a Cloud Service 的最新发行说明，请参阅[本页面](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 新增功能 {#what-is-new}

* [在单击容器上的&#x200B;**添加**&#x200B;工具栏按钮时，](/help/sites-cloud/authoring/universal-editor/authoring.md#adding-components)如果仅允许一种组件类型，则立即插入该组件而不需要从下拉菜单进行选择。
* [身份验证标头工具栏选项](/help/sites-cloud/authoring/universal-editor/navigation.md#autentication-settings)已置于功能切换之后，因为它在大多数情况下并不有用。
* [由于属性面板中的多个字段不允许容器嵌套，](/help/implementing/universal-editor/field-types.md#fields)现在，渲染例程会从字段列表中过滤掉嵌套的容器，以防止无效的嵌套。

## 早期采用的功能 {#early-adopter}

如果您有兴趣测试这些即将推出的功能并分享您的反馈，请从与您的Adobe关联的电子邮件地址向您的Adobe ID客户成功经理发送电子邮件。

### 新建RTE {#new-rte}

现在，右侧面板中提供了新的ProseMirror RTE，它在链接对话框中提供了一个页面选取器。

### 还原/重做 {#undo-redo}

通用编辑器现已支持内容创作者使用撤销与重做功能。

* 此功能涵盖上下文中的编辑操作、通过属性面板进行的修改，以及区块的新增（或复制）、移动与删除。
* 撤销与重做功能仅限于当前浏览器会话内使用。

## 其他改进 {#other-improvements}

* 修复了在通过属性边栏进行编辑时无法删除单个资产引用的问题。
* 修复了属性面板无限加载的问题，因为资产引用会自动转换为数组，从而导致无限加载状态。
   * 资源引用值现在按原样存储，不会自动转换为数组。
* 修复了当模型已定义但不包含任何内容时，“属性”面板不显示字段的问题。
   * 这会导致“属性”面板针对空的空详细信息响应（如空的内容片段）处于无限加载状态。
* ESLint配置已重构以与版本9兼容，包括更新的规则和插件支持。

## 弃用 {#deprecations}

* `text-input`组件现已正式弃用。
   * 在`model-definition.json`中，使用文本组件为“属性”面板创建文本输入。
