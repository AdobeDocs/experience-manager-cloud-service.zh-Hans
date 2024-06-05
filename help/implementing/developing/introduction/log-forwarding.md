---
title: AEM的日志转发as a Cloud Service
description: 了解如何在AEMas a Cloud Service中将日志转发给Splunk和其他日志记录供应商
exl-id: 27cdf2e7-192d-4cb2-be7f-8991a72f606d
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 3%

---

# 日志转发 {#log-forwarding}

>[!NOTE]
>
>此功能尚未发布，并且在发布时，某些日志记录目标可能不可用。 同时，您可以打开支持工单以将日志转发到 **Splunk**，如中所述 [日志文章](/help/implementing/developing/introduction/logging.md).

拥有日志记录供应商许可证或托管日志记录产品的客户可以将AEM、Apache/Dispatcher和CDN日志转发到关联的日志记录目标。 AEMas a Cloud Service支持以下日志记录目标：

* Azure Blob存储
* Datacog
* Elasticsearch或OpenSearch
* HTTPS
* Splunk

以自助方式配置日志转发，方法是在Git中声明一个配置，并通过Cloud Manager配置管道将其部署到生产（非沙盒）程序中的开发、暂存和生产环境类型。

请注意，与发送到日志记录目的地的日志相关联的网络带宽被视为您组织的网络I/O使用的一部分。


## 本文的结构 {#how-organized}

本文按以下方式组织：

* 设置 — 适用于所有日志记录目标
* 记录目标配置 — 每个目标的格式略有不同
* 高级联网 — 通过专用出口或VPN发送AEM和Apache/Dispatcher日志


## 设置 {#setup}

1. 在Git的项目顶级文件夹中创建以下文件夹和文件结构：

   ```
   config/
        logForwarding.yaml
   ```

1. logForwarding.yaml应包含元数据和类似于以下格式的配置（我们使用Splunk作为示例）。

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

   此 **种类** 参数应设置为LogForwarding版本应设置为架构版本，即1。

   配置中的令牌(如 `${{SPLUNK_TOKEN}}`)表示不应存储在Git中的密钥。 相反，将它们声明为Cloud Manager  [环境变量](/help/implementing/cloud-manager/environment-variables.md) 类型 **密码**. 确保选择 **全部** 作为“已应用服务”字段的下拉值，因此可以将日志转发到创作层、发布层和预览层。

   通过添加其他( AEM和apache日志)，可以在cdn日志和其他所有日志（和apache日志）之间设置不同的值 **cdn** 和/或 **aem** 之后阻止 **默认** 块，其中属性可以覆盖中定义的属性。 **默认** 块；仅需要已启用的属性。 一个可能的用例可能是对CDN日志使用不同的Splunk索引，如下面的示例所示。

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
          cdn:
            enabled: true
            token: "${{SPLUNK_TOKEN_CDN}}"
            index: "AEMaaCS_CDN"   
   ```

   另一种方案是禁用CDN日志的转发或其他所有内容(AEM和apache日志)。 例如，要仅转发CDN日志，可以配置以下内容：

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
          aem:
            enabled: false
   ```

1. 对于RDE以外的环境类型（当前不支持），请在Cloud Manager中创建目标部署配置管道。

   * [请参阅配置生产管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md)。
   * [请参阅配置非生产管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)。

## 记录目标配置 {#logging-destinations}

下面列出了受支持的日志记录目标的配置以及任何特定注意事项。

### Azure Blob存储 {#azureblob}

```
kind: "LogForwarding"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  azureBlob:
    default:
      enabled: true       
      storageAccountName: "example_acc"
      container: "aem_logs"
      sasToken: "${{AZURE_BLOB_SAS_TOKEN}}
      
```

SAS令牌应该用于身份验证。 它应该从共享访问签名页面而不是共享访问令牌页面创建，并且应该使用以下设置进行配置：

* 允许的服务：必须选择Blob
* 允许的资源：必须选择对象
* 允许的权限：必须选择“写入”、“添加”、“创建”
* 有效的开始和到期日期/时间。

以下是SAS令牌配置示例屏幕截图：

![Azure Blob SAS令牌配置](/help/implementing/developing/introduction/assets/azureblob-sas-token-config.png)


### Datadog {#datadog}

```
kind: "LogForwarding"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  dataDog:
    default:
      enabled: true       
      host: "http-intake.logs.datadoghq.eu"
      token: "${{DATADOG_API_KEY}}"
      
```

注意事项：

* 创建API密钥，而不与特定的云提供商进行任何集成。


### Elasticsearch和OpenSearch {#elastic}

```
kind: "LogForwarding"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  elasticsearch:
    default:
      enabled: true
      host: "example.com"
      user: "${{ELASTICSEARCH_USER}}"
      password: "${{ELASTICSEARCH_PASSWORD}}"
```

注意事项：

* 对于凭据，请确保使用部署凭据，而不是帐户凭据。 这些是在屏幕中生成的凭据，可能与以下图像类似：

![弹性部署凭据](/help/implementing/developing/introduction/assets/ec-creds.png)

### HTTPS {#https}

```
kind: "LogForwarding"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  https:
    default:
      url: "https://example.com/aem_logs/aem"
      authHeaderName: "X-AEMaaCS-Log-Forwarding-Token"
      authHeaderValue: "${{HTTPS_LOG_FORWARDING_TOKEN}}"
```

### Splunk {#splunk}

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

<!--
### Sumo Logic {#sumologic}

   ```
   kind: "LogForwarding"
   version: "1"
   metadata:
     envTypes: ["dev"]
   data:
     splunk:
       default:
         enabled: true
         host: "https://collectors.de.sumologic.com"
         uri: "/receiver/v1/http"
         privateKey: "${{SomeOtherToken}}"
   
   ```   
-->

## 高级网络 {#advanced-networking}

如果您有组织要求将流量锁定到日志记录目标，则可以配置日志转发以通过 [高级联网](/help/security/configuring-advanced-networking.md). 请参阅以下三种高级联网类型的模式，它们使用可选 `port` 参数，以及 `host` 参数。

### 灵活端口出口 {#flex-port}

如果日志通信流转到的端口不是443（例如，下面的8443），请配置高级联网，如下所示：

```
{
    "portForwards": [
        {
            "name": "mylogging.service.logger.com",
            "portDest": 8443, # something other than 443
            "portOrig": 30443
        }    
    ]
}
```

并配置yaml文件，如下所示：

```
kind: "LogForwarding"
version: "1"
data:
  splunk:
    default:
      host: "proxy.tunnel"
      token: "${{SomeToken}}"
      port: 30443
      index: "index_name"
```

### 专用出口IP {#dedicated-egress}

如果日志流量需要从专用出口IP发出，请配置高级网络，如下所示：

```
{
    "portForwards": [
        {
            "name": "mylogging.service.com",
            "portDest": 443, # something other than 443
            "portOrig": 30443
        }    
    ]
}
```

并配置yaml文件，如下所示：

```
kind: "LogForwarding"
version: "1"
data:
  splunk:
    default:
      host: "proxy.tunnel"
      token: "${{SomeToken}}"
      port: 30443
      index: "index_name"
```

### VPN {#vpn}

如果日志流量需要通过VPN，请配置高级网络，如下所示：

```
{
    "portForwards": [
        {
            "name": "mylogging.service.com",
            "portDest": 443, # something other than 443
            "portOrig": 30443
        }    
    ]
}
```

并配置yaml文件，如下所示：

```
kind: "LogForwarding"
version: "1"
data:
  splunk:
    default:
      host: "mylogging.service.com"
      token: "${{SomeToken}}"
      port: 30443
      index: "index_name"
```
