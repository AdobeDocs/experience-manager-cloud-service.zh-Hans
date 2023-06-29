---
title: 用于代码重构工具的统一体验
description: 用于代码重构工具的统一体验
exl-id: daee0e2d-1e2b-41a3-acab-fc59142d0e05
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 1%

---

# 用于代码重构工具的统一体验 {#unified-experience}

我们开发了工具，用于自动执行与AEMas a Cloud Service兼容所需的一些代码重构任务。 为了降低与安装和设置不同的代码重构工具相关的复杂性，我们开发了一个插件，以统一在代码和存储库上操作的工具。

## 好处 {#benefits}

Unified Experience插件具有以下优势：

* 将处理源代码的工具统一为一个 `node.js` 应用程序公开为 `aio-cli ` 插件，以便为用户提供一致的用户体验。

* 提供通过单个命令执行所有工具的功能，同时还提供根据需要执行特定工具的灵活性。

* 提供可扩展性以简化新工具的添加，同时保持体验的一致性。

## 了解插件 {#understanding-plugin}

此 `aio-cli-plugin-aem-cloud-service-migration` 插件包含两个主要部分：

* **用户界面**

   * `aio-cli` 执行一个或多个代码重构工具的命令（通过链接要按顺序执行的工具）。
   * `config.yaml` 它会采用所需的输入参数。

* **底层代码重构工具包**

  代码重构工具通过以下方式执行其功能：

   * 扫描客户代码的相应部分并处理代码（基于代码实施以获得最佳实践）以生成输出，然后可以验证和部署输出。

   * 生成摘要报告，以记录执行期间执行的操作。

## 可用性 {#availability}

参见 [Git资源：aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration) 了解使用情况以及如何向此源自GitHub的插件代码投稿。

>[!NOTE]
>目前，该插件已与AEM Dispatcher Converter和Repository Modernizer集成。
