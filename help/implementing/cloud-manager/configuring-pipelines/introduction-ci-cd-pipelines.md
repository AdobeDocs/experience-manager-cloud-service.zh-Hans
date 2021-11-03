---
title: CI-CD管线
description: 可查看本页以了解有关Cloud Manager CI-CD管道的信息
index: false
source-git-commit: 65898bd90e057cf5d646c5183ba6d2c8bdcac06e
workflow-type: tm+mt
source-wordcount: '826'
ht-degree: 0%

---


# Cloud Manager CI-CD管道 {#intro-cicd}

## 简介 {#introduction}

Cloud Manager中的CI/CD管道可由某种事件触发，例如源代码存储库的拉取请求（即代码更改），或与发行频率匹配的某种常规计划。

>[!NOTE]
>要配置管道，必须：
>* 定义将启动管道的触发器
>* 定义控制生产部署的参数
>* 配置性能测试参数


在Cloud Manager中，有两种类型的管道：

* [生产管道](#prod-pipeline)
* [非生产管道](#non-prod-pipeline)

![](/help/implementing/cloud-manager/assets/configure-pipeline/ci-cdpipeline-overview.png)

## 生产管道 {#prod-pipeline}

生产管道是用于构建管道的目的，管道包括一系列经过编排的步骤，以将源代码一直引入生产环境。 这些步骤包括首先构建、打包、测试、验证并部署到所有Stage环境中。 不用说，只有在创建生产和暂存环境集后，才能添加生产管道。

请参阅 [配置生产管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) 以了解更多详细信息。


## 非生产管道 {#non-prod-pipeline}

非生产管道旨在运行代码质量扫描或将源代码部署到开发环境。

请参阅 [配置非生产管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md) 以了解更多详细信息。

## 了解Cloud Manager中的CI-CD管道 {#understand-pipelines}

下表汇总了Cloud Manager中的所有管道及其用法。

| 管道类型 | 部署或代码质量 | 源代码 | 使用时间 | 何时或为何应使用？ |
|--- |--- |--- |---|---|---|
| 生产或非生产 | 部署 | 前端 | 部署前端代码。 前端代码是用作静态文件的任何代码。 它与AEM提供的UI代码不同。 它包括Sites主题、客户定义的SPA、Firefly SPA和任何其他解决方案。 必须为AEM版本。 | 快速部署时间<br> 可以为每个环境同时配置和运行多个前端管道 |
|  | 部署 | 完整堆栈 | 以同时部署后端、前端和HTTPD/调度程序配置。 有些限制适用。 | 当前端管道尚未采用时。 |
| 非生产 | 代码质量 | 前端 | 在前端代码上运行代码质量扫描 | 快速部署时间<br> 可以配置和运行多个管道 |
|  | 代码质量 | 完整堆栈 | 对完整堆栈代码运行代码质量扫描 | 快速部署时间<br> 可以配置和运行多个管道 |

下图说明了Cloud Manager管道配置采用传统的单一前端存储库或独立的前端存储库设置：

![](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-configurations.png)

## Cloud Manager前端管道 {#front-end}

前端管道通过支持用于部署前端代码的加速前端管道，帮助您的团队简化设计和开发流程。 此差异化的管道将JavaScript和CSS作为主题部署到AEM分发层，从而生成一个新的主题版本，该版本可以从AEM运行时交付的页面中引用。 前端代码是用作静态文件的任何代码。 它与AEM提供的UI代码不同。 它包括Sites主题、客户定义的SPA、Firefly SPA和任何其他解决方案。

>[!NOTE]
>以部署管理员角色登录的用户可以同时创建和运行多个前端管道。 但是，每个程序最多有300条管道（跨所有类型）。

这些类型可以是前端代码质量或前端部署管道类型。

### 配置前端管道之前 {#before-start}

在开始配置前端管道之前，请通过易于使用的AEM快速站点创建工具，查看端到端工作流的AEM快速站点创建历程。 此文档网站将帮助您简化AEM网站的前端开发，并在不了解AEM后端知识的情况下快速自定义您的网站。

### 配置前端管道 {#configure-front-end}

要了解如何配置前端管道，请参阅：

* 添加生产管道
* 添加非生产管道

## 完整堆栈管道 {#full-stack-pipeline}

完整堆栈管道为用户提供了同时部署后端、前端和HTTPD/调度程序配置的选项。  它将代码和内容部署到AEM运行时，包括打包为AEM客户端库的前端代码(JavaScript/CSS)。 如果未配置网层管道，则可以部署网层配置。 这表示“uber”管道，同时为用户提供了通过前端管道和Web层配置管道分别专门部署其前端代码或调度程序配置的选项。

将应用以下限制：

1. 用户必须以部署管理器身份登录才能配置或运行管道。

1. 在任何时候，每个环境只能有一个完整堆栈管道。

1. 如果环境的相应Web层配置管道不存在，则用户可以配置环境的完整堆栈管道以忽略或不忽略调度程序配置。

1. 如果环境的相应Web层配置管道存在，则环境的完整堆栈管道将忽略调度程序配置。

这些类型可以是“完整堆栈 — 代码质量”或“完整堆栈 — 部署”管道。

### 配置完整堆栈管道 {#configure-full-stack}

要了解如何配置完整堆栈管道，请参阅：

* 添加生产管道
* 添加非生产管道