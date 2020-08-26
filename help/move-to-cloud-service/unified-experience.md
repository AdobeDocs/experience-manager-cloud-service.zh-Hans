---
title: 代码重构工具的统一体验
description: 代码重构工具的统一体验
translation-type: tm+mt
source-git-commit: 9ef0681f93c8c25a1e5115cccb987d2db32c318e
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 0%

---


# 代码重构工具的统一体验 {#unified-experience}

代码重构的统一体验工具将AEM的执行体验统一为Cloud Service代码重构工具，它可以对调度程序文件、代码和存储库进行操作。

此工具降低了使用代码重构工具的复杂性，每个工具在安装、设置和执行方面具有不同的执行要求。

![图像](/help/move-to-cloud-service/assets/unified-one.png)

## 优势 {#benefits}

代码重构的统一体验工具调用并执行所有代码重构工具，这些工具可在同一位置处理源代码。

这些工具以及配套存储库允许：

* 将处理源代码迁移的所有工具统一到一个公开 `node.js` 的应用程序 `aio-cli plugin` 中，为用户提供一致的用户体验。

* 通过单个命令进行配置以执行整体迁移，同时根据需要提供执行一个特定工具的灵活性。

* 简化将来添加的新工具（如向插件添加新工具），只需为开发人员添加新命令和为用户添加简单的插件更新，体验将与增加更多价值保持一致。

## 了解插件 {#understanding-plugin}

重新 `aio-cli-plugin-aem-cloud-service-migration` 调整客户本地机器上的客户代码、存储库结构或配置。 本页介绍了统一体验的详细要求和设计决策。
它可作为开放源，供社区扩展以用于自定义用例。

此工具将所有代码重构工具统一到一个节点。js应用程序中，该节点。js应用程 `aio-cli plugin` 序公开为用户提供一致的用户体验。 该插件扫描客户的本地代码库，并生成AEM作为Cloud Service兼容代码、配置和包，然后部署到Cloud Service环境。

插件由两个主要部分组成：

* **用户界面**

   `aio-cli` 命令执行一个或多个迁移工具(通过链接要按顺序执行的工具`config.yaml` )，该迁移工具引入所需的输入参数

* **底层迁移工具套件**

   迁移工具通过以下方式执行其功能：

   * 扫描客户代码的各个部分并执行迁移（根据代码实施以获得最佳实践），以生成输出，然后验证并部署输出。

   * 以一致的顺序记录迁移时执行的操作以生成摘要报告。

## 可用性 {#availability}

您可以通过安装和 `aio-cli-plugin-aem-cloud-service-migration` 使用 `aio-cli`。

>[!NOTE]
>目前，此工具仅与调度程序转换器集成。

请参阅 [Git资源：aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration) ，了解用法以及如何为GitHub中开放源码的此插件代码提供内容。

