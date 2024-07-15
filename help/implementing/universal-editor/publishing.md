---
title: 使用 Universal Editor 发布内容
description: 了解 Universal Editor 如何发布内容以及您的应用程序如何处理发布的内容。
exl-id: aee34469-37c2-4571-806b-06c439a7524a
source-git-commit: 0ad9f349c997c35862e4f571b4741ed4c0c947e2
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 82%

---


# 使用 Universal Editor 发布内容 {#publishing}

了解 Universal Editor 如何发布内容以及您的应用程序如何处理发布的内容。

{{universal-editor-status}}

## 与 AEM 的相似之处 {#similarities}

对于 AEM 用户，使用 Universal Editor 发布内容的过程与以往类似：在 AEM 中发布时，内容会从作者层复制到发布层。

## 差异 {#differences}

使用 Universal Editor 进行发布的不同之处，与其说是与编辑器本身相关，不如说是 Universal Editor 使应用程序的外部托管成为可能。

在外部托管时，Web 应用程序需要注意的是，确保当作者在编辑器中打开应用程序时从作者层加载内容，并在访问者访问应用程序时从发布层加载内容。

## 检测应用程序中的层级 {#detecting}

确定是否应访问作者或发布层可以通过在应用程序中加入简单的条件语句来完成，以便在检测到它正在编辑器中打开时选择适当的作者或发布端点。

另一种选择是将应用程序部署到配置不同的两个不同环境，以便一个从作者层检索其内容，另一个从发布层检索。要允许作者在通用编辑器中打开已发布的URL，可以创建一个小型脚本将发布端URL“转换”为创作环境中的等效项（例如，通过在前面`author`个子域中添加前缀），以便自动重定向作者。

## 摘要 {#summary}

Universal Editor 的目标是不强加任何特定模式，以便以完全解耦的方式最大限度地实现实施目标，同时仍然保持简单和直接的实施。

同样，Universal Editor 不对任何特定项目应如何确定从哪一层交付内容作出任何要求。相反，它可以启用多种可能性，并允许项目确定哪种解决方案最适合其自身需求。
