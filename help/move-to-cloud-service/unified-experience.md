---
title: 代码重构工具的统一体验
description: 代码重构工具的统一体验
translation-type: tm+mt
source-git-commit: d6fa0d8bb7d5e251e51a3e4ffd93d6aaa1c7980c
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 1%

---


# 代码重构工具的统一体验 {#unified-experience}

我们开发了一些工具，以自动执行某些代码重构任务，这些Cloud Service与AEM兼容。 为了降低与安装和设置不同代码重构工具相关的复杂性，我们开发了一个插件来统一在代码和存储库上运行的工具。

## 优势 {#benefits}

统一体验插件具有以下优点：

* 将处理源代码的工具统一到一个作为插件 `node.js` 公开的应 `aio-cli ` 用程序中，为用户提供一致的用户体验。

* 提供通过单个命令执行所有工具的功能，同时提供根据需要执行特定工具的灵活性。

* 提供可扩展性以简化新工具的添加，同时保持体验的一致性。

## 了解插件 {#understanding-plugin}

插 `aio-cli-plugin-aem-cloud-service-migration` 件由两个主要部分组成：

* **用户界面**

   * `aio-cli` 命令执行一个或多个代码重构工具（通过链接要按顺序执行的工具）。
   * `config.yaml` 它需要输入参数。

* **基础代码重构工具套件**

   代码重构工具通过以下方式执行其功能：

   * 扫描客户代码的各个部分并操作代码（根据最佳实践的代码实现）以生成输出，然后验证和部署输出。

   * 生成摘要报告以记录执行过程中执行的操作。

## 可用性 {#availability}

请参阅 [Git资源：aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration) ，了解用法以及如何对此插件代码进行贡献（该插件在GitHub中是开放源码）。

>[!NOTE]
>目前，只有Dispatcher Converter与插件集成。
