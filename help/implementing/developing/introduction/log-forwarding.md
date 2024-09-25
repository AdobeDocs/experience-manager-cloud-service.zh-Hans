---
title: AEM as a Cloud Service的日志转发
description: 了解如何在AEM as a Cloud Service中将日志转发给Splunk和其他日志记录供应商
exl-id: 27cdf2e7-192d-4cb2-be7f-8991a72f606d
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 17d195f18055ebd3a1c4a8dfe1f9f6bc35ebaf37
workflow-type: tm+mt
source-wordcount: '1362'
ht-degree: 0%

---

# 日志转发 {#log-forwarding}

>[!NOTE]
>
>此功能尚未发布，并且在发布时，某些日志记录目标可能不可用。 同时，您可以打开支持票证以将日志转发到&#x200B;**Splunk**，如[AEM as a Cloud Service日志记录](/help/implementing/developing/introduction/logging.md)中所述。

拥有日志记录供应商许可证或托管日志记录产品的客户可以将AEM日志(包括Apache/Dispatcher)和CDN日志转发到关联的日志记录目标。 AEM as a Cloud Service支持以下日志记录目标：

* Azure Blob存储
* Datacog
* Elasticsearch或OpenSearch
* HTTPS
* Splunk

以自助方式配置日志转发，方法是在Git中声明一个配置，并通过Cloud Manager Configuration Pipeline将其部署到生产（非沙盒）程序中的开发、暂存和生产环境类型。

AEM和Apache/Dispatcher日志可以选择通过AEM的高级网络基础架构（如专用出口IP）进行路由。

请注意，与发送到日志记录目的地的日志相关联的网络带宽被视为您组织的网络I/O使用的一部分。


## 本文的结构 {#how-organized}

本文按以下方式组织：

* 设置 — 适用于所有日志记录目标
* 记录目标配置 — 每个目标的格式略有不同
* 日志条目格式 — 有关日志条目格式的信息
* 高级联网 — 通过专用出口或VPN发送AEM和Apache/Dispatcher日志


## 设置 {#setup}

1. 创建名为`logForwarding.yaml`的文件。 它应包含元数据，如[配置管道项目](/help/operations/config-pipeline.md#common-syntax)中所述（**kind**&#x200B;应设置为`LogForwarding`，版本应设置为“1”），其配置类似于以下内容（我们使用Splunk作为示例）。

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

1. 将文件放置在名为&#x200B;*config*&#x200B;或类似的顶级文件夹下，如[使用配置管道](/help/operations/config-pipeline.md#folder-structure)中所述。

1. 对于RDE以外的环境类型（当前不支持），在Cloud Manager中创建目标部署配置管道，如[此部分](/help/operations/config-pipeline.md#creating-and-managing)所引用；请注意，全栈管道和Web层管道不部署配置文件。

1. 部署配置。

配置中的令牌（如`${{SPLUNK_TOKEN}}`）表示不应存储在Git中的密钥。 请将其声明为Cloud Manager [机密环境变量](/help/operations/config-pipeline.md#secret-env-vars)。 确保选择&#x200B;**全部**&#x200B;作为“已应用服务”字段的下拉列表值，以便可以将日志转发到作者、发布和预览层。

通过在&#x200B;**default**&#x200B;块后添加额外的&#x200B;**cdn**&#x200B;和/或&#x200B;**aem**&#x200B;块，可以设置CDN日志和AEM日志(包括Apache/Dispatcher)之间的不同值，其中的属性可以覆盖&#x200B;**default**&#x200B;块中定义的属性；只需要启用的属性。 一个可能的用例可能是对CDN日志使用不同的Splunk索引，如下面的示例所示。

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

另一种方法是禁用CDN日志或AEM日志(包括Apache/Dispatcher)的转发。 例如，要仅转发CDN日志，可以配置以下内容：

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

* 允许的服务：必须选择Blob。
* 允许的资源：必须选择对象。
* 允许的权限：必须选择“写入”、“添加”、“创建”。
* 有效的开始和到期日期/时间。

以下是SAS令牌配置示例屏幕截图：

![Azure Blob SAS令牌配置](/help/implementing/developing/introduction/assets/azureblob-sas-token-config.png)

#### Azure Blob存储CDN日志 {#azureblob-cdn}

每个全局分布式日志服务器每隔几秒会在`aemcdn`文件夹下生成一个新文件。 创建后，该文件将不再附加到。 文件名格式为YYYY-MM-DDThh:mm:ss.sss-uniqueid.log。 例如，2024-03-04T10:00:00.000-WnFWYN9BpOUs2aOVn4ee.log。

例如，在某个时间点：

```
aemcdn/
   2024-03-04T10:00:00.000-abc.log
   2024-03-04T10:00:00.000-def.log
```

30秒后：

```
aemcdn/
   2024-03-04T10:00:00.000-abc.log
   2024-03-04T10:00:00.000-def.log
   2024-03-04T10:00:30.000-ghi.log
   2024-03-04T10:00:30.000-jkl.log
   2024-03-04T10:00:30.000-mno.log
```

每个文件都包含多个json日志条目，每个条目位于一行中。 日志条目格式在[AEM as a Cloud Service日志记录](/help/implementing/developing/introduction/logging.md)下描述，每个日志条目还包括以下[日志条目格式](#log-format)部分中提到的其他属性。

#### Azure Blob Storage AEM日志 {#azureblob-aem}

AEM日志(包括Apache/Dispatcher)显示在具有以下命名约定的文件夹下方：

* aemaccess
* aemerror
* aemrequest
* aemdispatcher
* aemhttpdaccess
* aemhttpderror

在每个文件夹下，将创建一个文件并将其附加到。 客户负责处理和管理此文件，以免它变得太大。

请参阅AEM as a Cloud Service的[日志记录](/help/implementing/developing/introduction/logging.md)下的日志条目格式。 日志条目还将包括以下[日志条目格式](#log-formats)部分中提到的其他属性。


### Datadog {#datadog}

```
kind: "LogForwarding"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  datadog:
    default:
      enabled: true       
      host: "http-intake.logs.datadoghq.eu"
      token: "${{DATADOG_API_KEY}}"
      tags:
         tag1: value1
         tag2: value2
      
```

注意事项：

* 创建API密钥，而不与特定的云提供商进行任何集成。
* tags属性是可选的
* 对于AEM日志，Datadog源标记设置为`aemaccess`、`aemerror`、`aemrequest`、`aemdispatcher`、`aemhttpdaccess`或`aemhttpderror`之一
* 对于CDN日志，Datadog源标记设置为`aemcdn`
* Datadog服务标记设置为`adobeaemcloud`，但您可以在标记部分中覆盖它


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
      pipeline: "ingest pipeline name"
```

注意事项：

* 默认情况下，端口为443。 可以选择使用名为`port`的属性覆盖它
* 对于凭据，请确保使用部署凭据，而不是帐户凭据。 这些是在屏幕中生成的凭据，可能与以下图像类似：

![弹性部署凭据](/help/implementing/developing/introduction/assets/ec-creds.png)

* 对于AEM日志，`index`设置为`aemaccess`、`aemerror`、`aemrequest`、`aemdispatcher`、`aemhttpdaccess`或`aemhttpderror`之一
* optional pipeline属性应设置为Elasticsearch或OpenSearch引入管道的名称，可以将其配置为将日志条目路由到相应的索引。 管道的处理器类型必须设置为&#x200B;*script*，脚本语言应设置为&#x200B;*无痛苦*。 以下是将日志条目路由到索引（如aemaccess_dev_26_06_2024）的脚本片段示例：

```
def envType = ctx.aem_env_type != null ? ctx.aem_env_type : 'unknown';
def sourceType = ctx._index;
def date = new SimpleDateFormat('dd_MM_yyyy').format(new Date());
ctx._index = sourceType + "_" + envType + "_" + date;
```

### HTTPS {#https}

```
kind: "LogForwarding"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  https:
    default:
      enabled: true
      url: "https://example.com/aem_logs/aem"
      authHeaderName: "X-AEMaaCS-Log-Forwarding-Token"
      authHeaderValue: "${{HTTPS_LOG_FORWARDING_TOKEN}}"
```

注意事项：

* URL字符串必须包含&#x200B;**https://**，否则验证将失败。
* URL可能包含端口。 例如，`https://example.com:8443/aem_logs/aem`。如果url字符串中未包含任何端口，则采用端口443（默认的HTTPS端口）。

#### HTTPS CDN日志 {#https-cdn}

Web请求(POST)将使用json有效负载连续发送，该有效负载是一个日志条目数组，日志条目格式在[AEM as a Cloud Service日志记录](/help/implementing/developing/introduction/logging.md#cdn-log)下描述。 下面的[日志条目格式](#log-formats)部分中提及了其他属性。

还有一个名为`sourcetype`的属性，该属性设置为值`aemcdn`。

>[!NOTE]
>
> 在发送第一个CDN日志条目之前，您的HTTP服务器必须成功完成一次性质询：发送到路径``/.well-known/fastly/logging/challenge``的请求在正文中必须以星号``*``和200状态代码响应。

#### HTTPS AEM日志 {#https-aem}

对于AEM日志（包括apache/dispacher），将连续发送Web请求(POST)，JSON有效负载为日志条目数组，其日志条目格式多种多样，如[AEM as a Cloud Service日志记录](/help/implementing/developing/introduction/logging.md)中所述。 下面的[日志条目格式](#log-format)部分中提及了其他属性。

还有一个名为`Source-Type`的属性，该属性设置为以下值之一：

* aemaccess
* aemerror
* aemrequest
* aemdispatcher
* aemhttpdaccess
* aemhttpderror

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
      index: "aemaacs"
```

注意事项：

* 默认情况下，端口为443。 可以选择使用名为`port`的属性覆盖它。


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

## 日志条目格式 {#log-formats}

有关每种日志类型(CDN日志和包括Apache/Dispatcher的AEM日志)的格式，请参阅[AEM as a Cloud Service日志记录](/help/implementing/developing/introduction/logging.md)。

由于来自多个程序和环境的日志可能会转发到同一日志记录目标，因此除了日志记录文章中所述的输出之外，每个日志条目中还将包含以下属性：

* aem_env_id
* aem_env_type
* aem_program_id
* aem_tier

例如，属性可能具有以下值：

```
aem_env_id: 1242
aem_env_type: dev
aem_program_id: 12314
aem_tier: author
```

## 高级网络 {#advanced-networking}

某些组织选择限制日志记录目标可以接收的流量。

对于CDN日志，您可以将IP地址添加到允许列表，如[fastly文档 — 公共IP列表](https://www.fastly.com/documentation/reference/api/utils/public-ip-list/)中所述。 如果共享IP地址列表过大，请考虑将流量发送到https服务器或(非Adobe)Azure Blob存储区，其中可以写入逻辑以将已知IP的日志发送到其最终目标。

对于AEM日志(包括Apache/Dispatcher)，如果您已配置[高级网络](/help/security/configuring-advanced-networking.md)，则可以使用advancedNetworking属性从专用出口IP地址或通过VPN转发它们。

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
      port: 443
      token: "${{SPLUNK_TOKEN}}"
      index: "aemaacs"
    aem:
      advancedNetworking: true
```

