---
title: 功能测试
description: 了解 AEM as a Cloud Service 部署过程内置的三种不同类型的功能测试，确保代码的质量和可靠性。
exl-id: 7eb50225-e638-4c05-a755-4647a00d8357
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '539'
ht-degree: 81%

---


# 功能测试 {#functional-testing}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_functionaltesting"
>title="功能测试"
>abstract="了解 AEM as a Cloud Service 部署过程内置的三种不同类型的功能测试，确保代码的质量和可靠性。"

了解 [AEM as a Cloud Service 部署过程](/help/implementing/cloud-manager/deploy-code.md)内置的三种不同类型的功能测试，确保代码的质量和可靠性。

## 范围

Cloud Manager 管道中功能测试步骤的目的是确保应用程序的基本功能按预期运行。

此测试阶段是将代码部署到生产环境之前的最后一级自动化测试。

功能测试不应取代，而应补充和扩展其他测试策略，如单元测试、集成测试或在 Cloud Manager 中的管道执行之外进行的功能测试。

## 概述 {#overview}

AEM as a Cloud Service 中有三种不同类型的功能测试。

* [产品功能测试](#product-functional-testing)
* [自定义功能测试](#custom-functional-testing)
* [自定义 UI 测试](#custom-ui-testing)

对于所有功能测试，测试的详细结果可以下载为 `.zip` 文件，使用 **下载内部版本日志** 按钮作为的一部分 [部署过程](/help/implementing/cloud-manager/deploy-code.md).

这些日志不包括实际 AEM 运行时进程的日志。 要访问这些日志，请参阅 [访问和管理日志](/help/implementing/cloud-manager/manage-logs.md) 了解更多详细信息。

产品功能测试和样本自定义功能测试都基于 [AEM 测试客户端](https://github.com/adobe/aem-testing-clients)。

### 产品功能测试 {#product-functional-testing}

产品功能测试是 AEM 中核心功能（如创作和复制任务）的一组稳定 HTTP 集成测试 (IT)。这些测试由 Adobe 维护，旨在防止在破坏核心功能的情况下部署对自定义应用程序代码的更改。

* [生产管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md)：每当您将新代码部署到 Cloud Manager 时，产品功能测试都会自动运行，不能跳过。
* [非生产管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)：可以选择在执行非生产管道时运行产品功能测试。

产品功能测试作为开源项目进行维护。参见 [产品功能测试](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke) 详细信息。

### 自定义功能测试 {#custom-functional-testing}

虽然产品功能测试由 Adobe 定义，但您可以为自己的应用程序编写自己的质量测试。 这类质量测试将作为自定义功能测试运行，作为[生产管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md)或（可选）[非生产管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)的一部分，用以确保应用程序的质量。

自定义功能测试会针对自定义代码部署和推送升级运行，这使得编写良好的功能测试尤为重要，这些测试可防止AEM代码更改破坏应用程序代码。 自定义功能测试步骤始终存在，不能跳过。

参见 [Java功能测试](/help/implementing/cloud-manager/java-functional-testing.md) 了解更多信息。


### 自定义 UI 测试 {#custom-ui-testing}

自定义 UI 测试是一项可选功能，可用于为应用程序创建和自动运行 UI 测试。 UI 测试是基于 Selenium 的测试，打包为 Docker 映像，并可选择多种语言和框架（如 Java 和 Maven、Node 和 WebDriver.io 或任何其他基于 Selenium 构建的框架和技术）。

参见 [自定义用户界面测试](/help/implementing/cloud-manager/ui-testing.md#custom-ui-testing) 了解更多信息。

