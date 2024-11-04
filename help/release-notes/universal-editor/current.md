---
title: 通用编辑器2024.09.3发行说明
description: 这些是通用编辑器2024.09.3版的发行说明。
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: b70acef8dc259fff3041617abe0a89f7eb73dfab
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 1%

---


# 通用编辑器2024.09.3发行说明 {#release-notes}

这些是通用编辑器2024年9月3日版本的发行说明。

>[!TIP]
>
>有关Adobe Experience Manager as a Cloud Service的最新发行说明，请参阅[此页面。](/help/release-notes/release-notes-cloud/release-notes-current.md)

## 新增功能 {#what-is-new}

* **`rootPath`现在可用于内容选取器**：现在可以为内容选取器提供`rootPath`，以便在使用[AEM内容、](/help/implementing/universal-editor/field-types.md#aem-content) [内容片段、](/help/implementing/universal-editor/field-types.md#content-fragment)和[体验片段](/help/implementing/universal-editor/field-types.md#experience-fragment)字段类型时，向用户呈现目标内容选择。
   * 因此，内容选择仅限于指定路径和任何子目录中的内容。

## 提前采用6.5支持计划 {#early-adoption}

现在，在早期采用者程序中使用AEM 6.5时，通用编辑器可用于Headless用例。

如果您有兴趣测试这项新功能并分享您的反馈，请通过与您的Adobe ID关联的电子邮件地址向您的Adobe代表发送电子邮件。

## 错误修复 {#bug-fixes}

* **跨容器拖放**： [通过拖放在不同容器之间移动组件](/help/sites-cloud/authoring/universal-editor/authoring.md#reordering-components)现在在源和目标中均遵循[组件筛选器](/help/implementing/universal-editor/customizing.md#filtering-components)。
