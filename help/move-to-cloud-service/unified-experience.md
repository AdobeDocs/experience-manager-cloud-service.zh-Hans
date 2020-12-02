---
title: 代码重构工具的统一体验
description: 代码重构工具的统一体验
translation-type: tm+mt
source-git-commit: 5d2b14c827603297a59cba7180fc1a68de0c841a
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 1%

---


# 代码重构工具{#unified-experience}的统一体验

我们开发了一些工具，以自动执行某些代码重构任务，这些Cloud Service与AEM兼容。 为了降低与安装和设置不同代码重构工具相关的复杂性，我们开发了一个插件来统一在代码和存储库上运行的工具。

## 优势{#benefits}

统一体验插件具有以下优点：

* 将处理源代码的工具统一到作为`aio-cli `插件公开的`node.js`应用程序中，为用户提供一致的用户体验。

* 提供通过单个命令执行所有工具的功能，同时提供根据需要执行特定工具的灵活性。

* 提供可扩展性以简化新工具的添加，同时保持体验的一致性。

## 了解插件{#understanding-plugin}

`aio-cli-plugin-aem-cloud-service-migration`插件由两个主要部分组成：

* **用户界面**

   * `aio-cli` 命令执行一个或多个代码重构工具（通过链接要按顺序执行的工具）。
   * `config.yaml` 它需要输入参数。

* **基础代码重构工具套件**

   代码重构工具通过以下方式执行其功能：

   * 扫描客户代码的各个部分并操作代码（根据最佳实践的代码实现）以生成输出，然后验证和部署输出。

   * 生成摘要报告以记录执行过程中执行的操作。

## 可用性 {#availability}

请参阅[Git资源：aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration)以了解用法以及如何对此插件代码进行贡献，该插件代码在GitHub中是开放源码。

>[!NOTE]
>目前，该插件已与AEM Dispatcher Converter和Repository Modernizer集成。
