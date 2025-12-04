---
title: 使用配置管道
description: 了解如何使用配置管道在AEM as a Cloud Service中部署各种配置，例如日志转发设置、清除相关的维护任务和各种CDN配置。
feature: Operations
role: Admin
exl-id: bd121d31-811f-400b-b3b8-04cdee5fe8fa
source-git-commit: ac04829b63ca5e2fee71f6c71d0730f21c576382
workflow-type: tm+mt
source-wordcount: '1405'
ht-degree: 2%

---

# 使用配置管道 {#config-pipelines}

了解如何使用配置管道在AEM as a Cloud Service中部署各种配置，例如日志转发设置、清除相关的维护任务和各种CDN配置。

## 概述 {#overview}

Cloud Manager配置管道将配置文件（以YAML格式创建）部署到目标环境。 通过这种方式，可以配置AEM as a Cloud Service中的许多功能，包括日志转发、清除相关的维护任务和几个CDN功能。

对于&#x200B;**发布投放**&#x200B;项目，可通过Cloud Manager将配置管道部署到开发、暂存和生产环境类型。 配置文件可以使用[命令行工具](/help/implementing/developing/introduction/rapid-development-environments.md#deploy-config-pipeline)部署到快速开发环境(RDE)。

也可以通过Cloud Manager为&#x200B;**Edge Delivery**&#x200B;项目部署配置管道。

本文档的以下部分概述了有关如何使用配置管道以及如何为其构建配置的重要信息。 它描述了在配置管道支持的所有功能或功能子集之间共享的一般概念。

* [支持的配置](#configurations) — 可以使用配置管道部署的配置列表。
* [创建和管理配置管道](#creating-and-managing) — 如何创建配置管道
* [通用语法](#common-syntax) — 跨配置共享的语法。
* [文件夹结构](#folder-structure) — 描述配置所需的结构配置管道。
* [机密环境变量](#secret-env-vars) — 使用环境变量不泄露配置中的机密的示例。
* [机密管道变量](#secret-pipeline-vars) — 使用环境变量在Edge Delivery Services项目之前不公开配置中的机密的示例。

## 支持的配置 {#configurations}

下表提供了此类配置的完整列表，并包含指向专用文档的链接，该文档介绍了其不同的配置语法和其他信息。

| 类型 | YAML `kind`值 | 描述 | 发布投放 | Edge Delivery |
|---|---|---|---|---|
| [流量筛选器规则，包括WAF](/help/security/traffic-filter-rules-including-waf.md) | `CDN` | 声明规则以阻止恶意流量 | X | X |
| [请求转换](/help/implementing/dispatcher/cdn-configuring-traffic.md#request-transformations) | `CDN` | 声明规则以转换流量请求的形状 | X | X |
| [响应转换](/help/implementing/dispatcher/cdn-configuring-traffic.md#response-transformations) | `CDN` | 声明规则以转换给定请求的响应形状 | X | X |
| [服务器端重定向](/help/implementing/dispatcher/cdn-configuring-traffic.md#server-side-redirectors) | `CDN` | 声明301/302样式的服务器端重定向 | X | X |
| [来源选择器](/help/implementing/dispatcher/cdn-configuring-traffic.md#origin-selectors) | `CDN` | 声明规则以将流量路由到其他后端，包括非Adobe应用程序 | X | X |
| [CDN错误页面](/help/implementing/dispatcher/cdn-error-pages.md) | `CDN` | 如果无法访问AEM源页面，请覆盖默认错误页面，并引用配置文件中自托管静态内容的位置 | X |  |
| [CDN清除](/help/implementing/dispatcher/cdn-credentials-authentication.md#purge-API-token) | `CDN` | 声明用于清除CDN的清除API密钥 | X |  |
| [客户管理的CDN HTTP令牌](/help/implementing/dispatcher/cdn-credentials-authentication.md#purge-API-token#CDN-HTTP-value) | `CDN` | 声明从客户CDN调用Adobe CDN所需的X-AEM-Edge-Key的值 | X |  |
| [基本身份验证](/help/implementing/dispatcher/cdn-credentials-authentication.md#purge-API-token#basic-auth) | `CDN` | 为保护某些URL的基本身份验证对话框声明用户名和密码。 | X | X |
| [版本清除维护任务](/help/operations/maintenance.md#purge-tasks) | `MaintenanceTasks` | 通过声明应何时清除内容版本的规则来优化AEM存储库 | X |  |
| [审核日志清除维护任务](/help/operations/maintenance.md#purge-tasks) | `MaintenanceTasks` | 通过声明有关应清除日志时间的规则，优化AEM审核日志以提高性能 | X |  |
| [工作流清除维护任务](/help/operations/maintenance.md) | `MaintenanceTasks` | 最大限度地减少工作流实例的数量，以帮助提高工作流引擎的性能。<br><br>另请参阅[定期清除工作流实例](/help/sites-cloud/administering/workflows-administering.md#regular-purging-of-workflow-instances) | X |  |
| [日志转发](/help/implementing/developing/introduction/log-forwarding.md) | `LogForwarding` | 配置用于将日志转发到各种目标的端点和凭据，包括Azure Blob Storage、Datadog、HTTPS、Elasticsearch、Splunk | X | X |
| [正在注册客户端ID](/help/implementing/developing/open-api-based-apis.md) | `API` | 通过注册客户端ID，可将Adobe Developer Console API项目范围设置为特定的AEM环境。 使用需要身份验证的基于OpenAPI的API时需要 | X |  |

## 创建和管理配置管道 {#creating-and-managing}

有关如何创建和配置&#x200B;**发布投放**&#x200B;配置管道的信息，请参阅[CI/CD管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#config-deployment-pipeline)。 在Cloud Manager中创建配置管道时，请确保在配置管道时选择&#x200B;**目标部署**，而不是&#x200B;**全栈代码**。 如前所述，RDE的配置是使用[命令行工具](/help/implementing/developing/introduction/rapid-development-environments.md#deploy-config-pipeline)而不是管道部署的。

有关如何创建和配置&#x200B;**Edge Delivery**&#x200B;配置管道的信息，请参阅[添加Edge Delivery管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-edge-delivery-pipeline.md)一文。

## 常用语法 {#common-syntax}

每个配置文件都以类似于以下示例片段的属性开头：

```yaml
   kind: "CDN"
   version: "1"
   metadata: ...
   data: ...
```

| 属性 | 描述 | 默认 |
|---|---|---|
| `kind` | 一个字符串，可确定哪种类型的配置，如日志转发、流量过滤器规则或请求转换 | 必需，无默认值 |
| `version` | 表示架构版本的字符串 | 必需，无默认值 |
| `metadata` | （可选）这包含一个字符串`envTypes`的数组，该数组可确定处理配置的环境类型。 对于&#x200B;**发布投放**，可能的值为`dev`、`stage`和`prod`。 对于&#x200B;**Edge Delivery**，只应使用值`prod`。 例如，如果数组仅包含`dev`，则不会将配置加载到暂存或生产环境中，即使已在该环境中部署配置也是如此。 | 所有环境类型，即(dev、stage、prod) for Publish Delivery或just prod for Edge Delivery。 |

您可以使用`yq`实用程序在本地验证配置文件的YAML格式（例如，`yq cdn.yaml`）。

## 发布投放 {#yamls-for-aem}

**发布投放**&#x200B;配置将部署到目标环境。 当定位多个环境时，可以采用不同的方式组织不同的文件。 例如，如果数组仅包含`dev`，则不会将配置加载到暂存或生产环境中，即使已在该环境中部署配置也是如此。

```yaml
   kind: "CDN"
   version: "1"
   metadata:
    envType: ["dev"]
```

### 文件夹结构 {#folder-structure}

名为`/config`或类似的文件夹应位于树顶部，并在其下方的树中放置一个或多个YAML文件。

例如：

```text
/config
  cdn.yaml
```

或者

```text
/config
  /dev
    cdn.yaml
```

`/config`下的文件夹名称和文件名是任意的。 但是，YAML文件必须包含有效的[`kind`属性值](#configurations)。

通常，配置会部署到所有环境。 如果每个环境的所有属性值都相同，则单个YAML文件就足够了。 但是，属性值在环境中不同是常见的现象，例如，在测试较低环境时。

以下各节说明了构造文件的一些策略。

### 适用于所有环境的单个配置文件 {#single-file}

文件结构类似于以下内容：

```text
/config
  cdn.yaml
  logForwarding.yaml
```

当相同的配置足以用于所有环境和所有类型的配置（CDN、日志转发等）时，请使用此结构。 在此方案中，`envTypes`数组属性将包含所有环境类型。

```yaml
   kind: "CDN"
   version: "1"
   metadata:
     envTypes: ["dev", "stage", "prod"]
```

使用密钥类型环境（或管道）变量，每个环境的[密钥属性](#secret-env-vars)可能会有所不同，如以下`${{SPLUNK_TOKEN}}`参考所示。

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

### 每种环境类型有一个单独的文件 {#file-per-env}

文件结构类似于以下内容：

```text
/config
  cdn-dev.yaml
  cdn-stage.yaml
  cdn-prod.yaml
  logForwarding-dev.yaml
  logForwarding-stage.yaml
  logForwarding-prod.yaml
```

当属性值可能存在差异时，请使用此结构。 在文件中，`envTypes`数组值应该与后缀相对应。 例如，值为`cdn-dev.yaml`的`logForwarding-dev.yaml`和`["dev"]`、值为`cdn-stage.yaml`的`logForwarding-stage.yaml`和`["stage"]`等。

### 每个环境的文件夹 {#folder-per-env}

在此策略中，每个环境有一个单独的`config`文件夹，并在Cloud Manager中为每个环境声明了一个单独的管道。

如果您有多个开发环境，并且每个环境都具有唯一的属性值，则此方法特别有用。

文件结构类似于以下内容：

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

## Edge Delivery Services {#yamls-for-eds}

Edge Delivery配置管道没有单独的开发、暂存和生产环境。 在发布交付环境中，通过开发、暂存和生产层更改进度。 相反，Edge Delivery配置管道将配置直接应用于Edge Delivery站点在Cloud Manager中注册的所有域映射。


因此，部署简单的文件结构，例如：

```text
/config
  cdn.yaml
  logForwarding.yaml
```

如果每个Edge Delivery站点上的规则需要不同，请使用语法&#x200B;*when*&#x200B;来区分这些规则。 例如，请注意域与以下代码片段中的dev.example.com匹配，该代码片段可与域`www.example.com`区分。

```
kind: "CDN"
version: "1"
data:
  trafficFilters:
    rules:
    # Block simple path
    - name: block-path
      when:
        allOf:
          - reqProperty: domain
            equals: "dev.example.com"
          - reqProperty: path
            equals: '/block/me'
      action: block
```

如果包含&#x200B;*envTypes*&#x200B;元数据字段，则只应使用值&#x200B;**prod**（省略envTypes元数据字段也是可以的）。 对于&#x200B;*层* reqProperty，只应使用值&#x200B;**publish**。

## 机密环境变量 {#secret-env-vars}

配置文件支持&#x200B;**secret**&#x200B;类型的Cloud Manager环境变量，因此无需将敏感信息存储在源代码管理中。 对于某些配置（包括日志转发），某些属性必须包含机密环境变量。

请注意，机密环境变量用于“发布投放”项目；请参阅Edge Delivery Services项目的“机密管道变量”部分。

以下代码片段是如何在配置中使用机密环境变量`${{SPLUNK_TOKEN}}`的示例。

```
kind: "LogForwarding"
version: "1"
data:
  splunk:
    default:
      enabled: true
      host: "splunk-host.example.com"
      token: "${{SPLUNK_TOKEN}}"
      index: "AEMaaCS"
```

有关如何使用环境变量的详细信息，请参阅[Cloud Manager环境变量](/help/implementing/cloud-manager/environment-variables.md)。

## 机密管道变量 {#secret-pipeline-vars}

对于Edge Delivery Services项目，请使用&#x200B;**密钥**&#x200B;类型的Cloud Manager管道变量，这样敏感信息就不需要存储在源代码管理中。 应用的&#x200B;*步骤*&#x200B;选择框应使用&#x200B;**部署**&#x200B;选项。

语法与上一节中显示的代码片段相同。

有关如何使用管道变量的详细信息，请参阅Cloud Manager中的[管道变量](/help/implementing/cloud-manager/configuring-pipelines/pipeline-variables.md)。
