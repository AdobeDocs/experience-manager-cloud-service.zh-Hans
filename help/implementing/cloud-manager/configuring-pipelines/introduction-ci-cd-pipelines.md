---
title: CI/CD 管道
description: 了解 Cloud Manager 的 CI/CD 管道，以及如何使用它们高效地部署代码。
index: true
exl-id: 40d6778f-65e0-4612-bbe3-ece02905709b
source-git-commit: 3348662e3da4dad75b851d7af7251d456321a3ec
workflow-type: ht
source-wordcount: '1368'
ht-degree: 100%

---


# Cloud Manager CI/CD 管道 {#intro-cicd}

了解 Cloud Manager 的 CI/CD 管道，以及如何使用它们高效地部署代码。

## 简介 {#introduction}

Cloud Manager 中的 CI/CD 管道是一种从源存储库构建代码并将其部署到环境中的机制。 管道可以由事件触发，例如源代码存储库的拉取请求（即代码更改），也可以按常规计划触发，匹配发布节奏。

要配置管道，必须：

* 定义将启动管道的触发器。
* 定义用于控制生产部署的参数。
* 配置性能测试参数。

Cloud Manager 提供两种类型的管道：

* [生产管道](#prod-pipeline)
* [非生产管道](#non-prod-pipeline)

![管道类型](/help/implementing/cloud-manager/assets/configure-pipeline/ci-cd-config1.png)

## 视频概述 {#video}

要快速概述管道类型，请观看此短视频。

>[!VIDEO](https://video.tv.adobe.com/v/342363)

## 生产管道 {#prod-pipeline}

生产管道是一种专门构建的管道，包括一系列协调的步骤，可部署用于生产的源代码。 这些步骤包括初次构建、打包、测试、验证和部署到所有暂存环境中。 因此，只有在创建了一组生产和暂存环境后，才能添加生产管道。

>[!TIP]
>
>请参阅[配置生产管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md)文档，了解更多信息。

## 非生产管道  {#non-prod-pipeline}

非生产管道主要用于运行代码质量扫描或将源代码部署到开发环境中。

>[!TIP]
>
>请参阅[配置非生产管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)文档，了解更多信息。

## 代码源 {#code-sources}

除了生产和非生产，管道还可以根据其部署的代码类型进行区分。

* **[全栈管道](#full-stack-pipeline)** – 同时部署后端和前端代码构建，其中包含一个或多个 AEM 服务器应用程序以及 HTTPD/Dispatcher 配置。 
* **[前端管道](#front-end)** – 部署包含一个或多个客户端 UI 应用程序的前端代码版本。
* **[Web 层配置管道](#web-tier-config-pipelines)** – 部署 HTTPD/Dispatcher 配置

这些将在本文档后面详细描述。

### 了解 Cloud Manager 中的 CI-CD 管道 {#understand-pipelines}

下表总结了 Cloud Manager 中可用的所有管道及其用法。

| 管道类型 | 部署或代码质量 | 源代码 | 用途 | 注释 |
|--- |--- |--- |---|---|
| 生产或非生产 | 部署 | 全栈 | 同时部署后端和前端代码构建以及 HTTPD/Dispatcher 配置 | 前端代码必须与 AEM 服务器代码同时部署时。<br>尚未采用前端管道或 Web 层配置管道时。 |
| 生产或非生产 | 部署 | 前端 | 部署包含一个或多个客户端 UI 应用程序的前端代码版本 | 支持多个并存前端管道<br>比全栈部署快得多 |
| 生产或非生产 | 部署 | Web 层配置 | 部署 HTTPD/Dispatcher 配置 | 几分钟即可部署 |
| 非生产 | 代码质量 | 全栈 | 在不部署的情况下对全栈代码运行代码质量扫描 | 支持多条管道 |
| 非生产 | 代码质量 | 前端 | 在不部署的情况下对前端代码运行代码质量扫描 | 支持多条管道 |
| 非生产 | 代码质量 | Web 层配置 | 在不部署的情况下对 Dispatcher 配置运行代码质量扫描 | 支持多条管道 |

下图说明了 Cloud Manager 的管道配置，包括传统的、单个前端存储库或独立的前端存储库设置。

![Cloud Manager 管道配置](/help/implementing/cloud-manager/assets/configure-pipeline/cm-setup.png)

## 全栈管道 {#full-stack-pipeline}

全栈管道将后端代码、前端代码和 Web 层配置同时部署到 AEM 运行时。

* 后端代码 – 不可变内容，如 Java 代码、OSGi 配置、Repoinit 以及可变内容
* 前端代码 – 应用程序 UI 资源，如 JavaScript、CSS、字体
* Web 层配置管道 – HTTPD/Dispatcher 配置

全栈管道表示一个“uber”管道，可以同时完成所有操作，同时使用户可以选择分别通过前端管道和 Web 层配置管道专门部署其前端代码或 Dispatcher 配置。

全栈管道将前端代码 (JavaScript/CSS) 打包为 [AEM 客户端库](/help/implementing/developing/introduction/clientlibs.md)。

如果未配置 [Web 层配置管道](#web-tier-config-pipelines)，则全栈管道可能会部署 Web 层配置。

以下限制适用。

* 用户必须以&#x200B;**部署管理员**&#x200B;角色登录，才能配置或运行管道。
* 在任何时候，每个环境只能有一个全栈管道。

此外，如果您选择引入 [Web 层配置管道](#web-tier-config-pipelines)，请注意全栈管道的行为。

* 如果存在相应的 Web 层配置管道，则环境的完整堆栈管道将忽略 Dispatcher 配置。
* 如果环境的相应 Web 层配置管道不存在，则用户可以配置全栈管道，包括或忽略 Dispatcher 配置。

全栈管道可以是代码质量管道或部署。

## 前端管道 {#front-end}

前端代码是用作静态文件的任何代码。 它独立于 AEM 提供的 UI 代码，可能包括站点主题、客户定义的 SPA、Firefly SPA 和其他解决方案。

前端管道通过加速后端开发的前端代码异步部署，帮助您的团队简化设计和开发过程。 这个专用管道将 JavaScript 和 CSS 作为主题部署到 AEM 分发层，从而产生一个新的主题版本，可以从 AEM 交付的页面中引用。

>[!IMPORTANT]
>
>您必须使用 AEM 版本 `2021.10.5933.20211012T154732Z ` 或更高版本，并启用 AEM Sites 以利用前端管道。

>[!NOTE]
>
>具有&#x200B;**部署管理员**&#x200B;角色的用户可以同时创建和运行多个前端管道。
>
>但是，每个程序（所有类型）的最大管道数限制为 300 条。

前端管道可以是代码质量管道或部署管道。

### 配置前端管道之前 {#before-start}

在配置前端管道之前，请查看[AEM 快速网站创建历程](/help/journey-sites/quick-site/overview.md)，全面了解易于使用的“AEM 快速站点创建”工具的端到端指南。此过程将帮助您简化前端开发，并允许您在不了解后端 AEM 的情况下快速定制站点。

### 配置前端管道 {#configure-front-end}

要了解如何配置前端管道，请参阅以下文档。

* [添加生产管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#adding-production-pipeline)
* [添加非生产管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#adding-non-production-pipeline)

### 使用前端管道开发站点 {#developing-with-front-end-pipeline}

有了前端管道，前端开发人员可以获得更多的独立性，可加快开发过程。

请参阅文档[使用前端管道开发站点](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md)，了解此流程的工作方式以及一些需要注意的事项，以便充分发挥此流程的潜力。

### 配置全栈管道 {#configure-full-stack}

要了解如何配置全栈管道，请参阅以下文档。

* [添加生产管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#adding-production-pipeline)
* [添加非生产管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#adding-non-production-pipeline)


## Web 层配置管道 {#web-tier-config-pipelines}

Web 层配置管道通过将 HTTPD/Dispatcher 配置与其他代码更改分离，实现了对 AEM 运行时的独占部署。 该管道已经简化，为只希望部署 Dispatcher 配置更改的用户提供了加速方法，只需几分钟即可完成部署。

>[!TIP]
>
>使用 Web 层配置管道，您可以选择将 Web 配置存储在与全栈管道相同的源位置，或者存储在不同的位置，具体取决于哪个结构更适合您的项目。

以下限制适用。

* 您必须使用 AEM 版本 `2021.12.6151.20211217T120950Z` 或更新版本才能使用 Web 层配置管道。
* 您必须[选择启用 Dispatcher 工具的灵活模式](/help/implementing/dispatcher/disp-overview.md#validation-debug)才能使用 Web 层配置管道。
* 用户必须以&#x200B;**部署管理员**&#x200B;角色登录，才能配置或运行管道。
* 在任何时候，每个环境只能有一个 Web 层配置管道。
* 当相应的全栈管道正在运行时，用户无法配置 Web 层配置管道。
* Web 层结构必须遵循灵活的模式结构，如文档[云中 Dispatcher](/help/implementing/dispatcher/disp-overview.md#validation-debug)中所定义。

此外，请注意[全栈管道](#full-stack-pipeline)在引入 Web 层管道时的行为。

* 如果尚未为环境配置 Web 层配置管道，则用户可以在配置其相应的全栈管道时进行选择，以便在执行和部署期间包括或忽略 Dispatcher 配置。
* 一旦为环境配置了 Web 层配置管道，其相应的全栈管道（如果存在）将在执行和部署期间忽略 Dispatcher 配置。
* 一旦删除了 Web 层配置管道，其相应的全栈管道将重置为在执行期间部署 Dispatcher 配置。

Web 层配置管道可以是代码质量类型或部署类型。

### 配置 Web 层配置管道 {#configure-web-tier-config-pipelines}

要了解如何配置 Web 层管道，请参阅以下文档。

* [添加生产管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#adding-production-pipeline)
* [添加非生产管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#adding-non-production-pipeline)
