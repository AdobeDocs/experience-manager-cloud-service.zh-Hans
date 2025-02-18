---
title: 通用编辑器2025.02.17发行说明
description: 这些是通用编辑器2025.02.17版的发行说明。
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: af04ad7e3f89247580c48c276cb371d78ac56a49
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 10%

---


# 通用编辑器2025.02.17发行说明 {#release-notes}

这些是通用编辑器2025年2月17日版本的发行说明。

>[!TIP]
>
>关于 Adobe Experience Manager as a Cloud Service 的最新发行说明，请参阅[本页面](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 新增功能 {#what-is-new}

* **发布到预览** — 使用通用编辑器发布（或取消发布）内容时，除了发布环境外，您现在可以选择是否希望发布到预览环境
   * 这样可在公开发布之前审查您的内容。
* **可以在组件定义中定义模型和筛选器** — 您现在可以定义组件在组件定义中使用的模型和筛选器。
   * 此信息可在定义中集中维护，无需在检测中指定。
   * 这允许您跨容器移动组件。
* **容器的子元素隐式被视为组件** — 如果将具有`data-aue-resource`的项作为直接子项放入容器中，则它被视为组件，无需指定`data-aue-behavior="component"`即可移动。

## 其他改进 {#other-improvements}

* **AEM 6.5资源选择器** — 现在，使用AEM 6.5运行通用编辑器时，可以正确打开6.5资源选择器。

