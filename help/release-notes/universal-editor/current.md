---
title: 通用编辑器2026.03.19发行说明
description: 这些是通用编辑器2026.03.19版的发行说明。
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: 8d9d162ec5bba99afb1ae86252a49a9880be4e68
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 28%

---


# 通用编辑器2026.03.19发行说明 {#release-notes}

这些是通用编辑器 2026 年 3 月 19 日版本的发行说明。

>[!TIP]
>
>如果您想在&#x200B;**即将推出的**&#x200B;通用编辑器发布之前对其功能进行测试，请参阅[通用编辑器预览发行说明。](/help/release-notes/universal-editor/preview.md)

>[!TIP]
>
>关于 Adobe Experience Manager as a Cloud Service 的最新发行说明，请参阅[本页面](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 新增功能 {#what-is-new}

* 现在，导航回[主屏幕时，属性中的项目将折叠。](/help/sites-cloud/authoring/universal-editor/navigation.md#home-button)
* [资源选择器](/help/implementing/universal-editor/configure-assets-selector.md)现在支持[筛选器定义。](/help/implementing/universal-editor/filtering.md)
* 如果所选项目没有可用的操作，[上下文菜单](/help/sites-cloud/authoring/universal-editor/authoring.md#context-menu)将不再显示用于访问操作的V形。

## 其他改进 {#other-improvements}

* 如果存在模型/过滤器/组件定义，则在编辑器中，从一个应用程序切换到另一个应用程序时会重新获取该定义。
* 使用DA作为后端时，删除图像不再保留空的图像标记。
* 现在，在使用DA作为后端时，可以正确处理块中的类。
* 现在，Open API将远程资产正确地另存为对象。

## 重大更改 {#breaking-change}

* 所有扩展都应更新为`@adobe/uix-guest` >= `1.1.7`以提高稳定性。
