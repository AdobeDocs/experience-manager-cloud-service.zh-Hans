---
title: 通用编辑器 2025.07.09 发行说明
description: 这些是通用编辑器 2025.07.09 版本的发行说明。
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: 199ee7e11f6706773bd426c3d27236d6ea791a6c
workflow-type: ht
source-wordcount: '368'
ht-degree: 100%

---


# 通用编辑器 2025.07.09 发行说明 {#release-notes}

这些是通用编辑器 2025 年 7 月 9 日版本的发行说明。

>[!TIP]
>
>关于 Adobe Experience Manager as a Cloud Service 的最新发行说明，请参阅[本页面](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 新增功能 {#what-is-new}

* [当单击容器上的&#x200B;**添加**&#x200B;工具栏按钮时，](/help/sites-cloud/authoring/universal-editor/authoring.md#adding-components)如果仅允许一种组件类型，则会直接插入该组件，而无需从下拉菜单中进行选择。
* 由于大多数情况下用处不大，[身份验证标头工具栏选项](/help/sites-cloud/authoring/universal-editor/navigation.md#autentication-settings)已被置于功能开关之后。
* [由于属性面板中的多字段不允许容器嵌套，](/help/implementing/universal-editor/field-types.md#fields)渲染流程现在会从字段列表中过滤嵌套的容器，以防止出现无效嵌套。

## 早期采用的功能 {#early-adopter}

如果您有兴趣测试这些即将推出的功能并分享您的反馈，请使用与您的 Adobe ID 关联的电子邮件地址发送邮件至您的 Adobe 客户成功经理。

### 新 RTE {#new-rte}

全新的 ProseMirror RTE 现已在右侧面板中提供，链接对话框中引入了页面选择器功能。

### 还原/重做 {#undo-redo}

通用编辑器现已支持内容创作者使用撤销与重做功能。

* 此功能涵盖上下文中的编辑操作、通过属性面板进行的修改，以及区块的新增（或复制）、移动与删除。
* 撤销与重做功能仅限于当前浏览器会话内使用。

## 其他改进 {#other-improvements}

* 已修复一个问题：通过属性边栏编辑时，无法移除单个资源引用。
* 已修复一个问题：由于资源引用被自动转换为数组，导致属性面板无限加载。
   * 资源引用值现在将按原样存储，不再自动转换为数组。
* 已修复一个问题：当模型已定义但未包含任何内容时，属性面板未能显示字段。
   * 该问题会导致属性面板在遇到空的详情响应（如空的内容片段）时进入无限加载状态。
* ESLint 配置已重构以兼容第 9 版，涵盖规则更新及插件支持的调整。

## 弃用 {#deprecations}

* `text-input` 组件现已正式弃用。
   * 在 `model-definition.json` 中，请使用文本组件为属性面板创建文本输入字段。
