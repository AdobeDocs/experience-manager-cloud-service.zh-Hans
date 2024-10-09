---
title: CI/CD管道简介
description: 了解Cloud Manager的CI/CD管道以及如何使用它们高效地部署代码。
index: true
exl-id: 40d6778f-65e0-4612-bbe3-ece02905709b
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 7a370ee0ab77046d128ae260af2575d50e655254
workflow-type: tm+mt
source-wordcount: '1488'
ht-degree: 35%

---


# Cloud Manager CI/CD 管道 {#intro-cicd}

了解Cloud Manager的CI/CD（持续集成/持续交付）管道，以及如何使用它们高效地部署代码。

## CI/CD管道简介 {#introduction}

Cloud Manager 中的 CI/CD 管道是一种从源存储库构建代码并将其部署到环境中的机制。事件触发管道，例如来自源代码存储库（如Git）的拉取请求（即代码更改）。 或者，也可以定期触发以匹配发布节奏。

要配置管道，必须执行以下操作：

* 定义启动管道的触发器。
* 定义用于控制生产部署的参数。
* 配置性能测试参数。

Cloud Manager 提供两种类型的管道：

* [生产管道](#prod-pipeline)
* [非生产管道](#non-prod-pipeline)

![管道类型](/help/implementing/cloud-manager/assets/configure-pipeline/ci-cd-config1.png)

## 生产管道 {#prod-pipeline}

生产管道是一种专门构建的管道，包括一系列协调的步骤，可部署用于生产的源代码。这些步骤包括初次构建、打包、测试、验证和部署到所有暂存环境中。因此，只有在创建了一组生产和暂存环境后，才能添加生产管道。

>[!TIP]
>
>请参阅[配置生产管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md)。

## 非生产管道 {#non-prod-pipeline}

非生产管道主要用于运行代码质量扫描或将源代码部署到开发环境中。

>[!TIP]
>
>请参阅[配置非生产管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)。

## 代码源 {#code-sources}

除了生产环境和非生产环境外，管道还可能会因它们部署的代码类型而异。

* **[全栈管道](#full-stack-pipeline)** — 同时部署包含一个或多个AEM服务器应用程序以及HTTPD/Dispatcher配置的后端和前端代码构建。
* **[配置管道](#config-deployment-pipeline)** — 您可以快速部署日志转发和清除相关维护任务等功能的配置。 它还包含各种CDN（内容分发网络）配置，例如流量过滤器规则，包括Web应用程序防火墙(WAF)规则。 此外，您还可以管理请求和响应转换、源选择器、客户端重定向、错误页面、CDN密钥、清除API密钥和基本身份验证。 有关详细信息，请参阅[使用配置管道](/help/operations/config-pipeline.md)。
* **[前端管道](#front-end)** — 部署包含一个或多个客户端用户界面应用程序的前端代码版本。
* **[Web层配置管道](#web-tier-config-pipelines)** — 部署HTTPD/Dispatcher配置。

本文档稍后将详细介绍这些管道类型。

### 了解Cloud Manager中的CI-CD管道 {#understand-pipelines}

下表总结了Cloud Manager中可用的管道及其用法。

| 管道类型 | 部署或代码质量 | Source代码 | 用途 | 注释 |
| --- | --- | --- | --- | ---|
| 生产或非生产 | 部署 | 全栈 | 同时部署后端和前端代码构建以及 HTTPD/Dispatcher 配置 | 当前端代码必须与AEM服务器代码同时部署时使用。 在尚未采用前端管道或Web层配置管道时使用。 |
| 生产或非生产 | 部署 | 前端 | 部署包含一个或多个客户端 UI 应用程序的前端代码版本 | 支持多个并发的前端管道<br>比全栈部署快得多。 |
| 生产或非生产 | 部署 | Web层配置 | 部署 HTTPD/Dispatcher 配置 | 几分钟即可部署 |
| 生产或非生产 | 部署 | 配置 | 为与CDN、日志转发和清除维护任务相关的许多功能](/help/operations/config-pipeline.md)部署[配置 | 几分钟即可部署 |
| 非生产 | 代码质量 | 全栈 | 在不部署的情况下对全栈代码运行代码质量扫描 | 支持多条管道 |
| 非生产 | 代码质量 | 前端 | 在不部署的情况下对前端代码运行代码质量扫描 | 支持多条管道 |
| 非生产 | 代码质量 | Web层配置 | 在不部署的情况下对Dispatcher配置运行代码质量扫描 | 支持多条管道 |

下图说明了 Cloud Manager 的管道配置，包括传统的、单个前端存储库或独立的前端存储库设置。

![Cloud Manager 管道配置](/help/implementing/cloud-manager/assets/configure-pipeline/cm-setup.png)

## 全栈管道 {#full-stack-pipeline}

全栈管道将后端代码、前端代码和Web层配置同时部署到AEM运行时。

* 后端代码 – 不可变内容，如 Java 代码、OSGi 配置、Repoinit 以及可变内容
* 前端代码 – 应用程序 UI 资源，如 JavaScript、CSS、字体
* Web 层配置管道 – HTTPD/Dispatcher 配置

全栈管道表示“uber”管道。 它同时处理所有内容，同时还允许用户单独部署其前端代码或Dispatcher配置。 此部署分别通过前端管道和Web层配置管道进行。

全栈管道将前端代码 (JavaScript/CSS) 打包为 [AEM 客户端库。](/help/implementing/developing/introduction/clientlibs.md)

如果未配置 [Web 层配置管道](#web-tier-config-pipelines)，则全栈管道可能会部署 Web 层配置。

以下限制适用。

* 用户必须以&#x200B;**部署管理员**&#x200B;角色登录，才能配置或运行管道。
* 在任何时候，每个环境只能有一个全栈管道。

此外，如果您选择引入[Web层配置管道](#web-tier-config-pipelines)，请注意全栈管道的行为。

* 如果存在相应的Web层配置管道，则环境的全栈管道将忽略Dispatcher配置。
* 如果环境的相应 Web 层配置管道不存在，则用户可以配置全栈管道，包括或忽略 Dispatcher 配置。

全栈管道可以是代码质量管道或部署。

### 配置全栈管道 {#configure-full-stack}

请参阅[添加生产管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#full-stack-code)。
请参阅[添加非生产管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#full-stack-code)。

## 配置管道 {#config-deployment-pipeline}

使用配置管道，您可以快速部署用于日志转发、清除相关的维护任务和各种CDN配置的设置，包括流量过滤器规则(如WAF （Web应用程序防火墙）规则)。 此外，您还可以管理请求和响应转换、源选择器、客户端重定向、错误页面、客户管理的CDN密钥、清除API密钥和基本身份验证。

请参阅[使用配置管道](/help/operations/config-pipeline.md)获取受支持功能的完整列表，并了解如何管理存储库中的配置以使它们正确部署。

### 配置配置管道 {#configure-config-deployment}

请参阅[添加生产管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#targeted-deployment)。
请参阅[添加非生产管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#targeted-deployment)。

## 前端管道 {#front-end}

前端代码是用作静态文件的任何代码。它独立于 AEM 提供的 UI 代码，可能包括站点主题、客户定义的 SPA、SPA 和其他解决方案。

前端管道通过加速前端代码的部署（后端开发的异步）帮助您的团队简化设计和开发过程。 此专用管道将JavaScript和CSS作为主题部署到AEM分发层，从而生成新的主题版本，可以从AEM交付的页面中引用。

>[!NOTE]
>
>具有&#x200B;**部署管理员**&#x200B;角色的用户可以同时创建和运行多个前端管道。
>
>但是，每个程序（所有类型）的最大管道数限制为 300 条。

前端管道可以是代码质量管道或部署管道。

### 配置前端管道之前 {#before-start}

在配置前端管道之前，请查看[AEM 快速网站创建历程](/help/journey-sites/quick-site/overview.md)，全面了解易于使用的“AEM 快速站点创建”工具的端到端指南。此历程可帮助您简化前端开发，并让您无需了解后端AEM即可快速自定义站点。

### 配置前端管道 {#configure-front-end}

请参阅[添加生产管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#adding-production-pipeline)。
请参阅[添加非生产管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#adding-non-production-pipeline)。

### 使用前端管道开发站点 {#developing-with-front-end-pipeline}

有了前端管道，前端开发人员可以获得更多的独立性，可加快开发过程。

请参阅[使用前端管道开发站点](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md)，了解此过程的工作方式以及一些需要注意的事项，以便充分发挥此过程的潜力。

## Web层配置管道 {#web-tier-config-pipelines}

Web层配置管道允许向AEM运行时独占部署HTTPD/Dispatcher配置，并将其与其他代码更改分离。 它是一个简化的管道，为只希望部署Dispatcher配置更改的用户提供了加速方法，只需几分钟即可完成部署。

>[!TIP]
>
>通过Web层配置管道，您可以将Web配置存储在与全栈管道相同的源位置或不同的源位置，具体取决于最适合您的项目结构的位置。

以下限制适用。

* 在AEM版本`2021.12.6151.20211217T120950Z`或更高版本上以使用Web层配置管道。
* [选择启用Dispatcher工具的灵活模式](/help/implementing/dispatcher/disp-overview.md#validation-debug)以使用Web层配置管道。
* 用户必须以&#x200B;**部署管理员**&#x200B;角色登录，才能配置或运行管道。
* 在任何时候，每个环境只能有一个 Web 层配置管道。
* 当相应的全栈管道正在运行时，用户无法配置Web层配置管道。
* Web 层结构必须遵循灵活的模式结构，如文档[云中 Dispatcher](/help/implementing/dispatcher/disp-overview.md#validation-debug)中所定义。

此外，请注意[全栈管道](#full-stack-pipeline)在引入 Web 层管道时的行为。

* 如果没有为环境设置Web层配置管道，则用户可以在配置全栈管道时选择包含或忽略Dispatcher配置。 在执行和部署期间进行此选择。
* 为环境配置Web层配置管道后，其相应的全栈管道（如果存在）将在执行和部署期间忽略Dispatcher配置。
* 删除 Web 层配置管道后，其相应的全栈管道会重置为在执行期间部署 Dispatcher 配置。

Web层配置管道可以是`Code quality`或`Deployment`类型。

### 配置Web层管道 {#configure-web-tier}

请参阅[添加生产管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#targeted-deployment)。
请参阅[添加非生产管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#targeted-deployment)。

## 有关管道类型的视频概述 {#video}

要快速概述管道类型，请观看以下视频（2分钟、26秒）。

>[!VIDEO](https://video.tv.adobe.com/v/342363)
