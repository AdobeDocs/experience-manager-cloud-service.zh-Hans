---
title: 使用配置管道
description: 了解如何使用配置管道来部署各种配置AEM as a Cloud Service，例如日志转发设置、清除相关的维护任务和各种CDN配置。
feature: Operations
role: Admin
exl-id: bd121d31-811f-400b-b3b8-04cdee5fe8fa
source-git-commit: 3d0abce117cf94d7bf521e78be2ec019f216aa08
workflow-type: tm+mt
source-wordcount: '973'
ht-degree: 1%

---

# 使用配置管道 {#config-pipelines}

了解如何使用配置管道来部署各种配置AEM as a Cloud Service，例如日志转发设置、清除相关的维护任务和各种CDN配置。

## 概述 {#overview}

Cloud Manager配置管道将配置文件（以YAML格式创建）部署到目标环境。 通过这种方式，可以配置AEM as a Cloud Service中的许多功能，包括日志转发、清除相关的维护任务和几个CDN功能。

配置管道可以通过Cloud Manager部署到生产（非沙盒）程序中的开发、暂存和生产环境类型。 不支持RDE。

本文档的以下部分概述了有关如何使用配置管道以及如何为其构建配置的重要信息。 它描述了在配置管道支持的所有功能或功能子集之间共享的一般概念。

* [支持的配置](#configurations) — 可以使用配置管道部署的配置列表
* [创建和管理配置管道](#creating-and-managing) — 如何创建配置管道。
* [通用语法](#common-syntax) — 跨配置共享的语法
* [文件夹结构](#folder-structure) — 描述配置预期的结构配置管道
* [机密环境变量](#secret-env-vars) — 使用环境变量不泄露配置中的机密的示例

## 支持的配置 {#configurations}

下表提供了此类配置的完整列表，并包含指向专用文档的链接，该文档介绍了其不同的配置语法和其他信息。

| 类型 | YAML `kind`值 | 描述 |
|---|---|---|
| [流量筛选器规则，包括WAF](/help/security/traffic-filter-rules-including-waf.md) | `CDN` | 声明规则以阻止恶意流量 |
| [请求转换](/help/implementing/dispatcher/cdn-configuring-traffic.md#request-transformations) | `CDN` | 声明规则以转换流量请求的形状 |
| [响应转换](/help/implementing/dispatcher/cdn-configuring-traffic.md#response-transformations) | `CDN` | 声明规则以转换给定请求的响应形状 |
| [客户端重定向](/help/implementing/dispatcher/cdn-configuring-traffic.md#client-side-redirectors) | `CDN` | 声明301/302样式客户端重定向 |
| [来源选择器](/help/implementing/dispatcher/cdn-configuring-traffic.md#origin-selectors) | `CDN` | 声明规则以将流量路由到其他后端，包括非Adobe应用程序 |
| [CDN错误页面](/help/implementing/dispatcher/cdn-error-pages.md) | `CDN` | 如果无法访问AEM源，则覆盖默认错误页面，并引用配置文件中自托管静态内容的位置 |
| [CDN清除](/help/implementing/dispatcher/cdn-credentials-authentication.md#purge-API-token) | `CDN` | 声明用于清除CDN的清除API密钥 |
| [客户管理的CDN HTTP令牌](/help/implementing/dispatcher/cdn-credentials-authentication.md#purge-API-token#CDN-HTTP-value) | `CDN` | 声明从客户CDN调用AdobeCDN所需的X-AEM-Edge-Key的值 |
| [基本身份验证](/help/implementing/dispatcher/cdn-credentials-authentication.md#purge-API-token#basic-auth) | `CDN` | 声明基本身份验证对话框的用户名和密码，以保护某些URL [（仅适用于早期采用者）](/help/release-notes/release-notes-cloud/release-notes-current.md#foundation-early-adopter) |
| [版本清除维护任务](/help/operations/maintenance.md#purge-tasks) | `MaintenanceTasks` | 通过声明有关应清除内容版本的规则来优化AEM存储库 |
| [审核日志清除维护任务](/help/operations/maintenance.md#purge-tasks) | `MaintenanceTasks` | 通过声明有关应清除日志时间的规则，优化AEM审核日志以提高性能 |
| [日志转发](/help/implementing/developing/introduction/log-forwarding.md) | `LogForwarding` | 尚不可用 — 配置用于将日志转发到各种目标（例如Splunk、Datadog、HTTPS）的端点和凭据 |

## 创建和管理配置管道 {#creating-and-managing}

有关如何创建和配置管道的信息，请参阅文档[CI/CD管道。](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#config-deployment-pipeline)

在Cloud Manager中创建配置管道时，请确保在配置管道时选择&#x200B;**目标部署**，而不是&#x200B;**全栈代码**。

## 通用语法 {#common-syntax}

每个配置文件都以类似于以下示例片段的属性开头：

```yaml
  kind: "LogForwarding"
  version: "1"
  metadata:
    envTypes: ["dev"]
```

| 属性 | 描述 | 默认 |
|---|---|---|
| `kind` | 一个字符串，可确定哪种类型的配置，例如日志转发、流量过滤器规则或请求转换 | 必需，无默认值 |
| `version` | 表示架构版本的字符串 | 必需，无默认值 |
| `envTypes` | 此字符串数组是`metadata`节点的子属性。 可能的值包括dev、stage、prod或任何组合，它确定将处理配置的环境类型。 例如，如果数组仅包含`dev`，则不会将配置加载到暂存或生产环境中，即使已在该环境中部署配置也是如此。 | 所有环境类型（开发、暂存、生产） |

您可以使用`yq`实用程序在本地验证配置文件的YAML格式（例如，`yq cdn.yaml`）。

## 文件夹结构 {#folder-structure}

名为`/config`或类似的文件夹应位于树顶部，并在其下方的树中放置一个或多个YAML文件。

例如：

```text
/config
  cdn.yaml
```

或

```text
/config
  /dev
    cdn.yaml
```

`/config`下的文件夹名称和文件名是任意的。 但是，YAML文件必须包含有效的[`kind`属性值。](#configurations)

通常，配置会部署到所有环境。 如果每个环境的所有属性值都相同，则单个YAML文件就足够了。 但是，属性值在环境中不同是常见的现象，例如，在测试较低环境时。

以下各节说明了构造文件的一些策略。

### 适用于所有环境的单个配置文件 {#single-file}

文件结构将类似于以下内容：

```text
/config
  cdn.yaml
  logForwarding.yaml
```

当相同的配置足以用于所有环境和所有类型的配置（CDN、日志转发等）时，请使用此结构。 在此方案中，`envTypes`数组属性将包含所有环境类型。

```yaml
   kind: "cdn"
   version: "1"
   metadata:
     envTypes: ["dev", "stage", "prod"]
```

使用密钥类型的环境变量，每个环境的[密钥属性](#secret-env-vars)可能会有所不同，如`${{SPLUNK_TOKEN}}`参考中所述

```yaml
kind: "LogForwarding"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  splunk:
    default:
      enabled: true
      host: "splunk-host.example.com"
      token: "${{SPLUNK_TOKEN}}"
      index: "AEMaaCS"
```

### 每种环境类型一个单独的文件 {#file-per-env}

文件结构将类似于以下内容：

```text
/config
  cdn-dev.yaml
  cdn-stage.yaml
  cdn-prod.yaml
  logForwarding-dev.yaml
  logForwarding-stage.yaml
  logForwarding-prod.yaml
```

当属性值可能存在差异时，请使用此结构。 在文件中，可以预期`envTypes`数组值与后缀相对应，例如
值为`["dev"]`的`cdn-dev.yaml`和`logForwarding-dev.yaml`、值为`["stage"]`的`cdn-stage.yaml`和`logForwarding-stage.yaml`等。

### 每个环境的文件夹 {#folder-per-env}

在此策略中，每个环境有一个单独的`config`文件夹，并在Cloud Manager中为每个环境声明了一个单独的管道。

如果您有多个开发环境，并且每个环境都具有唯一的属性值，则此方法特别有用。

文件结构将类似于以下内容：

```text
/config/dev1
  cdn.yaml
  logForwarding.yaml
/config/dev2
  cdn.yaml
  logForwarding.yaml
/config/prod  
  cdn.yaml
  logForwarding.yaml
```

此方法的一个变体是为每个环境维护一个单独的分支。

## 机密环境变量 {#secret-env-vars}

配置文件支持&#x200B;**secret**&#x200B;类型的Cloud Manager环境变量，因此无需将敏感信息存储在源代码管理中。 对于某些配置（包括日志转发），某些属性必须包含机密环境变量。

以下代码片段是如何在配置中使用机密环境变量`${{SPLUNK_TOKEN}}`的示例。

```
kind: "LogForwarding"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  splunk:
    default:
      enabled: true
      host: "splunk-host.example.com"
      token: "${{SPLUNK_TOKEN}}"
      index: "AEMaaCS"
```

有关如何使用环境变量的详细信息，请参阅文档[Cloud Manager环境变量](/help/implementing/cloud-manager/environment-variables.md)。
