---
title: 用于代码重构工具的统一体验
description: 了解适用于代码重构工具的统一体验。
exl-id: daee0e2d-1e2b-41a3-acab-fc59142d0e05
source-git-commit: 78ead5f15c2613d9c3bed3025b43423a66805c59
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 1%

---

# 用于代码重构工具的统一体验 {#unified-experience}

Adobe开发了一些工具，用于自动执行与Adobe Experience Manager (AEM)as a Cloud Service兼容所需的一些代码重构任务。 为了降低与安装和设置各种代码重构工具相关的复杂性，Adobe开发了一个插件，以统一在代码和存储库上操作的工具。

## 好处 {#benefits}

统一的Experience插件具备以下优势：

* 将处理源代码的工具统一到一起 `node.js` 应用程序公开为 `aio-cli ` 插件，以便为用户提供一致的用户体验。

* 通过单个命令运行所有工具，同时还提供了根据需要运行特定工具的灵活性。

* 简化新工具的添加，同时保持体验的一致性。

## 了解插件 {#understanding-plugin}

此 `aio-cli-plugin-aem-cloud-service-migration` 插件包含两个主要部分：

* **用户界面**

   * `aio-cli` 命令来执行一个或多个代码重构工具（通过链接按顺序运行的工具）。
   * `config.yaml` 它会采用所需的输入参数。

* **底层代码重构工具套件**

  代码重构工具通过以下方式执行其功能：

   * 扫描客户代码的相应部分并处理代码（基于最佳实践的代码实施）以生成输出，然后可以验证和部署输出。

   * 生成摘要报告以记录执行期间执行的操作。

## 可用性 {#availability}

请参阅 [Git资源：aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration) 在这里，您可以了解使用情况以及如何向此源自GitHub的插件代码投稿。

>[!NOTE]
>目前，该插件已与AEM Dispatcher Converter和Repository Modernizer集成。
