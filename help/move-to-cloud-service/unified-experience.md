---
title: 代码重构工具的统一体验
description: 代码重构工具的统一体验
translation-type: tm+mt
source-git-commit: c00b10b4d564e05099740b9ff991624db4f37a3d
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 0%

---


# 代码重构工具的统一体验 {#unified-experience}

为客户提供不同交互点的多个工具会创建脱节的体验，并增加使用工具的复杂性，每个工具在安装、设置和执行方面的执行要求都不同。

## 优势 {#benefits}

代码重构工具的统一体验调用并执行所有代码重构工具，这些工具在同一位置处理源代码。

代码重构工具与配套存储库的统一体验允许：

* 将处理源代码迁移的所有工具统一到一个公开的 `node.js` 应用程序中， `aio-cli plugin` 为用户提供一致的用户体验。

* 通过单个命令进行整体迁移，同时根据需要灵活执行一个特定工具。

* 简化将来新增工具（如向插件添加新工具）的添加，只需为开发人员添加新命令和为用户添加简单的插件更新，体验就与增加价值保持一致。

### 了解应用程序设计

此工具将所有代码重构工具统一到一个节点。js应用程序中，该节点。js应用程 `aio-cli plugin` 序公开为用户提供一致的用户体验。

插件由两个主要部分组成：

* **用户界面**

   `aio-cli` 命令执行一个或多个迁移工具(通过链接要按顺序执行的工具`config.yaml` )，该迁移工具引入所需的输入参数

* **底层迁移工具套件**

   迁移工具通过以下方式执行其功能：

   * 扫描客户代码的各个部分并执行迁移（根据代码实施以获得最佳实践），以生成输出，然后验证并部署输出。

   * 以一致的顺序记录迁移时执行的操作以生成摘要报告。

## 使用插件 {#using-plugin}

重新 `aio-cli-plugin-aem-cloud-service-migration` 调整客户本地机器上的客户代码、存储库结构或配置。 本页介绍了统一体验的详细要求和设计决策。
它可作为开放源，供社区扩展以用于自定义用例。

## 可用性 {#availability}

您可以通过(当前仅 `aio-cli-plugin-aem-cloud-service-migration` 与调 `aio-cli` 度程序转换器集成)安装和使用。

请参阅 [Git资源：aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration) ，了解用法以及如何为此工具贡献内容。

插件代码已在Github中开放。

