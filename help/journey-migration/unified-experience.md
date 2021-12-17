---
title: 代码重构工具的统一体验
description: 代码重构工具的统一体验
source-git-commit: a6d225943c5d23ebd960fda0b0912a81f1f80014
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 1%

---

# 代码重构工具的统一体验 {#unified-experience}

我们开发了一些工具来自动执行与AEMas a Cloud Service兼容所需的一些代码重构任务。 为了降低与安装和配置不同代码重构工具相关的复杂性，我们开发了一个插件来统一在代码和存储库上运行的工具。

## 优点 {#benefits}

统一体验插件具有以下优势：

* 将处理源代码的工具统一到一个中 `node.js` 应用程序显示为 `aio-cli ` 插件，为用户提供一致的用户体验。

* 提供通过单个命令执行所有工具的功能，同时提供根据需要执行特定工具的灵活性。

* 提供了可扩展性以简化新工具的添加，同时保持体验的一致性。

## 了解插件 {#understanding-plugin}

的 `aio-cli-plugin-aem-cloud-service-migration` 插件包含两个主要部分：

* **用户界面**

   * `aio-cli` 命令来执行一个或多个代码重构工具（通过链接要按顺序执行的工具）。
   * `config.yaml` 输入所需的输入参数。

* **基础代码重构工具包**

   代码重构工具通过以下方式执行其功能：

   * 扫描客户代码的相应部分并处理代码（基于代码实现以了解最佳实践）以生成输出，然后验证和部署输出。

   * 生成摘要报告，以记录执行期间执行的操作。

## 可用性 {#availability}

请参阅 [Git资源：aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration) 了解此插件代码的使用情况以及如何对此插件代码贡献内容（此插件代码源于GitHub中）。

>[!NOTE]
>当前，该插件已与AEM Dispatcher Converter和Repository Modernizer集成。
