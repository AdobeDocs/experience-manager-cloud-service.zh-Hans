---
title: CI/CD管线
description: 了解Cloud Manager的CI/CD管道，以及如何使用这些管道高效地部署代码。
index: true
exl-id: 40d6778f-65e0-4612-bbe3-ece02905709b
source-git-commit: 6c246444f48440c64af0951e75f2071c00e477fa
workflow-type: tm+mt
source-wordcount: '1377'
ht-degree: 1%

---

# Cloud Manager CI/CD管道 {#intro-cicd}

了解Cloud Manager的CI/CD管道，以及如何使用这些管道高效地部署代码。

## 简介 {#introduction}

Cloud Manager中的CI/CD管道是一种从源存储库构建代码并将其部署到环境的机制。 管道可以由事件触发，例如来自源代码存储库的拉取请求（即代码更改），或者按照与发行频率匹配的常规计划触发。

要配置管道，必须：

* 定义将启动管道的触发器。
* 定义控制生产部署的参数。
* 配置性能测试参数。

Cloud Manager提供两种类型的管道：

* [生产管道](#prod-pipeline)
* [非生产管道](#non-prod-pipeline)

![管道类型](/help/implementing/cloud-manager/assets/configure-pipeline/ci-cd-config1.png)

## 视频概述 {#video}

有关管道类型的快速概述，请观看此简短视频。

>[!VIDEO](https://video.tv.adobe.com/v/342363)

## 生产管道 {#prod-pipeline}

生产管道是专门构建的管道，包括一系列精心编排的步骤来部署源代码以供生产使用。 这些步骤包括：首先构建、打包、测试、验证并部署到所有暂存环境。 因此，只有在创建一组生产环境和暂存环境后，才能添加生产管道。

>[!TIP]
>
>请参阅文档 [配置生产管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) 以了解更多详细信息。

## 非生产管道 {#non-prod-pipeline}

非生产管道主要用于运行代码质量扫描或将源代码部署到开发环境。

>[!TIP]
>
>请参阅文档 [配置非生产管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md) 以了解更多详细信息。

## 代码源 {#code-sources}

除了生产和非生产之外，管道还可以根据其部署的代码类型进行区分。

* **[完整堆栈管道](#full-stack-pipeline)**  — 同时部署包含一个或多个AEM服务器应用程序以及HTTPD/Dispatcher配置的后端和前端代码构建
* **[前端管道](#front-end)**  — 部署包含一个或多个客户端UI应用程序的前端代码生成
* **[网层配置管道](#web-tier-config-pipelines)**  — 部署HTTPD/Dispatcher配置

本文档的后面部分对这些内容进行了详细描述。

### 了解Cloud Manager中的CI-CD管道 {#understand-pipelines}

下表汇总了Cloud Manager中可用的所有管道及其用法。

| 管道类型 | 部署或代码质量 | 源代码 | 用途 | 注释 |
|--- |--- |--- |---|---|
| 生产或非生产 | 部署 | 全栈 | 同时部署后端和前端代码内部版本以及HTTPD/Dispatcher配置 | 当前端代码必须与AEM服务器代码同时部署时。<br>当前端管道或Web层配置管道尚未采用时。 |
| 生产或非生产 | 部署 | 前端 | 部署包含一个或多个客户端UI应用程序的前端代码内部版本 | 支持多个并发前端管道<br>比全栈部署快得多 |
| 生产或非生产 | 部署 | 网层配置 | 部署HTTPD/Dispatcher配置 | 在几分钟内部署 |
| 非生产 | 代码质量 | 全栈 | 在无部署的全堆栈代码上运行代码质量扫描 | 支持多个管道 |
| 非生产 | 代码质量 | 前端 | 在没有部署的前端代码上运行代码质量扫描 | 支持多个管道 |
| 非生产 | 代码质量 | 网层配置 | 在没有部署的情况下对调度程序配置运行代码质量扫描 | 支持多个管道 |

下图说明了Cloud Manager的管道配置，这些配置采用传统的、单个前端存储库或独立的前端存储库设置。

![Cloud Manager管道配置](/help/implementing/cloud-manager/assets/configure-pipeline/cm-setup.png)

## 全栈管道 {#full-stack-pipeline}

全栈管道可同时将后端代码、前端代码和Web层配置部署到AEM运行时。

* 后端代码 — 不可变内容，如Java代码、OSGi配置、重新点以及可变内容
* 前端代码 — 应用程序UI资源，如JavaScript、CSS、字体
* Web层配置 — HTTPD/Dispatcher配置

全栈管道代表一个“uber”管道，可同时执行所有操作，同时为用户提供通过前端管道和Web层配置管道分别专门部署其前端代码或调度程序配置的选项。

全栈管道将前端代码(JavaScript/CSS)打包为 [AEM客户端库。](/help/implementing/developing/introduction/clientlibs.md)

如果 [网络层配置管道](#web-tier-config-pipelines) 未配置。

以下限制适用。

* 用户必须使用 **部署管理器** 角色来配置或运行管道。
* 在任何时候，每个环境只能有一个全栈管道。

此外，如果您选择引入 [网层配置管道。](#web-tier-config-pipelines)

* 如果存在相应的Web层配置管道，则环境的全栈管道将忽略调度程序配置。
* 如果环境的相应Web层配置管道不存在，则用户可以配置全栈管道包含或忽略Dispatcher配置。

全栈管道可以是代码质量管道或部署。

## 前端管道 {#front-end}

前端代码是用作静态文件的任何代码。 它与AEM提供的UI代码不同，可能包括网站主题、客户定义的SPA、Firefly SPA和其他解决方案。

前端管道支持加快后端开发的前端代码异步部署，从而帮助您的团队简化设计和开发流程。 此专用管道将JavaScript和CSS作为主题部署到AEM分发层，从而生成一个新的主题版本，该版本可以从AEM交付的页面中引用。

>[!IMPORTANT]
>
>您必须使用AEM版本 `2021.10.5933.20211012T154732Z ` 或更高版本，因为AEM Sites支持利用前端管道。

>[!NOTE]
>
>具有 **部署管理器** 角色可以同时创建和运行多个前端管道。
>
>但是，每个程序最多有300条管道（跨所有类型）。 这些可以是前端代码质量或前端部署管道。

前端管道可以是代码质量管道或部署。

### 在配置前端管道之前 {#before-start}

在配置前端管道之前，请查看 [AEM快速网站创建历程](/help/journey-sites/quick-site/overview.md) 了解易用的AEM快速站点创建工具的端到端指南。 此历程将帮助您简化前端开发，并允许您在不了解后端AEM知识的情况下快速自定义您的网站。

### 配置前端管线 {#configure-front-end}

要了解如何配置前端管道，请参阅以下文档。

* [添加生产管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#adding-production-pipeline)
* [添加非生产管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#adding-non-production-pipeline)

### 使用前端管道开发站点 {#developing-with-front-end-pipeline}

利用前端管道，前端开发人员可以获得更大的独立性，并加快开发过程。

请参阅该文档 [利用前端管道开发站点](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md) 了解此过程的工作方式以及需要注意的一些事项，以便充分挖掘此过程的潜力。

### 配置全栈管道 {#configure-full-stack}

要了解如何配置全栈管道，请参阅以下文档。

* [添加生产管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#adding-production-pipeline)
* [添加非生产管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#adding-non-production-pipeline)


## 网层配置管道 {#web-tier-config-pipelines}

Web层配置管道通过将HTTPD/Dispatcher配置与其他代码更改分离，可以将其独占部署到AEM运行时。 它是一个简化的管道，为希望仅部署调度程序配置更改的用户提供了支持，这是一种在几分钟内即可完成部署的加速方法。

>[!TIP]
>
>使用Web层配置管道，您可以选择将Web配置存储在与完整堆栈管道相同的源位置，还是存储在不同的位置，具体取决于哪个结构更适合您的项目。

以下限制适用。

* 您必须使用AEM版本 `2021.12.6151.20211217T120950Z` 或更新版本，以利用web层配置管道。
* 您必须 [选择启用调度程序工具的灵活模式](/help/implementing/dispatcher/disp-overview.md#validation-debug) 来利用web层配置管道。
* 用户必须使用 **部署管理器** 角色来配置或运行管道。
* 在任何时候，每个环境只能有一个Web层配置管道。
* 当用户运行相应的全栈管道时，用户无法配置Web层配置管道。
* Web层结构必须遵循文档中定义的灵活模式结构 [云中的调度程序。](/help/implementing/dispatcher/disp-overview.md#validation-debug)

此外，请注意 [全栈管道](#full-stack-pipeline) 引入web层管道时将会有所行为。

* 如果尚未为环境配置Web层配置管道，则用户可以在配置其相应的全栈管道以在执行和部署期间包含或忽略Dispatcher配置时进行选择。
* 为环境配置Web层配置管道后，其相应的全栈管道（如果存在）将在执行和部署期间忽略调度程序配置。
* 删除Web层配置管道后，其相应的全栈管道将被重置，以在执行调度程序配置期间部署该配置。

Web层配置管道的类型可以是代码质量或部署。

### 配置网层配置管道 {#configure-web-tier-config-pipelines}

要了解如何配置Web层配置管道，请参阅以下文档。

* [添加生产管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#adding-production-pipeline)
* [添加非生产管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#adding-non-production-pipeline)
