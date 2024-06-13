---
title: 将 Edge Delivery Services 与现有 AEM 项目结合使用
description: 了解如何在现有 AEM 项目中利用 Edge Delivery Services 的优势
feature: Edge Delivery Services
exl-id: f54aac3a-1d0c-4be0-9aa6-616217e0e458
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: ht
source-wordcount: '324'
ht-degree: 100%

---


# 将 Edge Delivery Services 与现有 AEM 项目结合使用 {#existing-projects}

您无需等待创建新 AEM 项目即可从 Edge Delivery Services 受益。可将 Edge Delivery Services 集成到您现有的 AEM 项目中，以使您可立即利用其性能提升。

## AEM 页面编辑器限制 {#page-editor}

在 Edge Delivery Services 出现之前，AEM 中管理的内容是使用 AEM 页面编辑器进行编辑的。如果您的项目在引入 Edge Delivery Services 之前开始，则几乎可以肯定您正在使用页面编辑器。

AEM 页面编辑器仅适用于 [AEM 组件](/help/implementing/developing/components/overview.md)，例如 [核心组件。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) 这些组件与 Edge Delivery Services 不兼容。因此，需要两个阶段才能将 Edge Delivery Services 引入现有 AEM 项目：

* [第 1 阶段 - 替换前端](#replace-front-end)
* [第 2 阶段 - 切换到通用编辑器](#switch-ue)

## 第 1 阶段 - 替换前端 {#replace-front-end}

在第一阶段，您可以继续使用现有的 AEM 站点结构、组件和创作工具。网站渲染将通过使用 JavaScript 和 CSS 的区块进行重建，并将通过 Edge Delivery Services 进行交付。

请参阅 Edge Delivery Services 文档中的[构建部分](/help/edge/developer/block-collection.md)，了解有关区块以及如何开发 Edge Delivery Services 的更多详细信息。

需要使用应用程序生成器上的转换器转换 AEM 渲染的 HTML 输出，并将其发送到 Edge Delivery Services。

![发布流程中的内容转换器](assets/content-converter.png)

第二阶段通过消除技术重叠来完成该流程：AEM Author 上带有 HTL 和 Java 的 AEM 核心组件、Edge Delivery 上基于 JS 的区块以及基于 NodeJS 的转换器。

## 第 2 阶段 - 切换到通用编辑器 {#switch-ue}

在此阶段，AEM 页面编辑器会被通用编辑器替代。由于通用编辑器可以直接使用区块，因此不再需要 AEM 核心组件和转换器。

