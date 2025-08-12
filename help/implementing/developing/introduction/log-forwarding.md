---
title: AEM as a Cloud Service的日志转发
description: 了解如何在AEM as a Cloud Service中将日志转发到日志记录供应商
exl-id: 27cdf2e7-192d-4cb2-be7f-8991a72f606d
feature: Developing
role: Admin, Architect, Developer
source-git-commit: bf35f847f6f00d21915dfedb10cf38ea74344988
workflow-type: tm+mt
source-wordcount: '2409'
ht-degree: 3%

---

# 日志转发 {#log-forwarding}

>[!NOTE]
>
>现在，日志转发是以自助方式配置的，不同于传统方法，后者需要提交Adobe支持票证。 如果您的日志转发是由Adobe设置的，请参阅[正在迁移](#legacy-migration)部分。

如果客户拥有带日志记录供应商的许可证或托管日志记录产品，则可以将AEM日志(包括Apache/Dispatcher)和CDN日志转发到关联的日志记录目标。 AEM as a Cloud Service支持以下日志记录目标：

<table>
  <tbody>
    <tr>
      <th>日志技术</th>
      <th>Private Beta*</th>
      <th>AEM</th>
      <th>Dispatcher</th>
      <th>CDN</th>
    </tr>
    <tr>
      <td>Amazon S3</td>
      <td style="background-color: #ffb3b3;">是</td>
      <td>是</td>
      <td>是</td>
      <td style="background-color: #ffb3b3;">否</td>
    </tr>
    <tr>
      <td>Azure Blob存储</td>
      <td>否</td>
      <td>是</td>
      <td>是</td>
      <td>是</td>
    </tr>
    <tr>
      <td>Datacog</td>
      <td>否</td>
      <td>是</td>
      <td>是</td>
      <td>是</td>
    </tr>
    <tr>
      <td>Dynatrace</td>
      <td style="background-color: #ffb3b3;">是</td>
      <td>是</td>
      <td>是</td>
      <td style="background-color: #ffb3b3;">否</td>
    </tr>
    <tr>
      <td>Elasticsearch<br>OpenSearch</td>
      <td>否</td>
      <td>是</td>
      <td>是</td>
      <td>是</td>
    </tr>
    <tr>
      <td>HTTPS</td>
      <td>否</td>
      <td>是</td>
      <td>是</td>
      <td>是</td>
    </tr>
    <tr>
      <td>New Relic</td>
      <td style="background-color: #ffb3b3;">是</td>
      <td>是</td>
      <td>是</td>
      <td style="background-color: #ffb3b3;">否</td>
    </tr>
    <tr>
      <td>Splunk</td>
      <td>否</td>
      <td>是</td>
      <td>是</td>
      <td>是</td>
    </tr>
    <tr>
      <td>Sumo逻辑</td>
      <td style="background-color: #ffb3b3;">是</td>
      <td>是</td>
      <td>是</td>
      <td style="background-color: #ffb3b3;">否</td>
    </tr>
  </tbody>
</table>

>[!NOTE]
>
> 对于Private Beta中的技术，请发送电子邮件至[aemcs-logforwarding-beta@adobe.com](mailto:aemcs-logforwarding-beta@adobe.com)以请求获取访问权限。

日志转发以自助方式配置，方法是在Git中声明配置，并且可以通过Cloud Manager配置管道部署到开发、暂存和生产环境类型。 可以使用调用命令行工具将配置文件部署到快速开发环境（RDE）。

AEM和Apache/Dispatcher日志可以选择通过AEM的高级网络基础架构（如专用出口IP）进行路由。

请注意，与发送到日志记录目的地的日志相关联的网络带宽被视为您组织的网络I/O使用的一部分。

## 本文的结构 {#how-organized}

本文按以下方式组织：

* 设置 — 适用于所有日志记录目标
* 传输和高级网络 — 在创建日志记录配置之前，应考虑网络设置
* 记录目标配置 — 每个目标的格式略有不同
* 日志条目格式 — 有关日志条目格式的信息
* 从旧版日志转发迁移 — 如何从Adobe之前设置的日志转发迁移到自助方法

## 设置 {#setup}

1. 创建名为`logForwarding.yaml`的文件。 它应包含元数据，如[配置管道](/help/operations/config-pipeline.md#common-syntax)文章中所述（**kind**&#x200B;应设置为`LogForwarding`，版本应设置为“1”），其配置类似于以下内容（我们使用Splunk作为示例）。

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

1. 将文件放置在名为&#x200B;*config*&#x200B;或类似的顶级文件夹下，如[使用配置管道](/help/operations/config-pipeline.md#folder-structure)中所述。

1. 对于RDE（使用命令行工具）以外的环境类型，在Cloud Manager中创建目标部署配置管道，如[此部分](/help/operations/config-pipeline.md#creating-and-managing)所引用；请注意，全栈管道和Web层管道不部署配置文件。

1. 部署配置。

配置中的令牌（如`${{SPLUNK_TOKEN}}`）表示不应存储在Git中的密钥。 请将其声明为Cloud Manager [机密环境变量](/help/operations/config-pipeline.md#secret-env-vars)。 确保选择&#x200B;**全部**&#x200B;作为“已应用服务”字段的下拉列表值，以便可以将日志转发到作者、发布和预览层。

通过在&#x200B;**default**&#x200B;块后添加额外的&#x200B;**cdn**&#x200B;和/或&#x200B;**aem**&#x200B;块，可以设置CDN日志和AEM日志(包括Apache/Dispatcher)之间的不同值，其中属性可以覆盖&#x200B;**default**&#x200B;块中定义的属性；只需要启用的属性。 一个可能的用例可能是对CDN日志使用不同的Splunk索引，如下面的示例所示。

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
       cdn:
         enabled: true
         token: "${{SPLUNK_TOKEN_CDN}}"
         index: "AEMaaCS_CDN"   
```

另一种方法是禁用CDN日志或AEM日志(包括Apache/Dispatcher)的转发。 例如，要仅转发CDN日志，可以配置以下内容：

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
       aem:
         enabled: false
```

## 传输和高级网络 {#transport-advancednetworking}

有些组织选择限制日志记录目标可以接收哪些流量，而有些组织则可能需要使用HTTPS (443)以外的端口。  如果是，则在部署日志转发配置之前，需要配置[高级网络](/help/security/configuring-advanced-networking.md)。

根据您是否使用端口443以及是否需要从固定IP地址显示日志，使用下表查看高级联网和日志配置的要求。

<table>
  <tbody>
    <tr>
      <th>目标端口</th>
      <th>需要从固定IP显示日志？</th>
      <th>需要高级联网</th>
      <th>需要LogForwarding.yaml端口定义</th>
    </tr>
    <tr>
      <td rowspan="2" ro>HTTPS (443)</td>
      <td>否</td>
      <td>否</td>
      <td>否</td>
    </tr>
    <tr>
      <td>是</td>
      <td>是，<a href="/help/security/configuring-advanced-networking.md#dedicated-egress-ip-address-dedicated-egress-ip-address">专用出口</a></td>
      <td>否</td>
    <tr>
    <tr>
      <td rowspan="2">非标准端口（如8088）</td>
      <td>否</td>
      <td>是，<a href="/help/security/configuring-advanced-networking.md#flexible-port-egress-flexible-port-egress">灵活出口</a></td>
      <td>是</td>
    </tr>
    <tr>
      <td>是</td>
      <td>是，<a href="/help/security/configuring-advanced-networking.md#dedicated-egress-ip-address-dedicated-egress-ip-address">专用出口</a></td>
      <td>是</td>
  </tbody>
</table>

>[!NOTE]
>是否从单个IP地址显示日志取决于您选择的高级联网配置。  必须使用专用出口实现此目的。
>
> 高级网络配置是[两步流程](/help/security/configuring-advanced-networking.md#configuring-and-enabling-advanced-networking-configuring-enabling)，需要在程序和环境级别启用。

对于AEM日志(包括Apache/Dispatcher)，如果您已配置[高级网络](/help/security/configuring-advanced-networking.md)，则可以使用`aem.advancedNetworking`属性从专用出口IP地址或通过VPN转发它们。

以下示例说明如何使用高级联网在标准HTTPS端口上配置日志记录。

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
      port: 443
      token: "${{SPLUNK_TOKEN}}"
      index: "aemaacs"
    aem:
      advancedNetworking: true
```

对于CDN日志，您可以将IP地址添加到允许列表，如[Fastly文档 — 公共IP列表](https://www.fastly.com/documentation/reference/api/utils/public-ip-list/)中所述。 如果共享IP地址列表过大，请考虑将流量发送到https服务器或(非Adobe)Azure Blob Store，其中可以写入逻辑，以将已知IP的日志发送到其最终目标。

>[!NOTE]
>
>CDN日志不可能显示自AEM日志显示来源的IP地址，这是因为日志是直接从Fastly而不是AEM Cloud Service发送的。

## 记录目标配置 {#logging-destinations}

下面列出了受支持的日志记录目标的配置以及任何特定注意事项。

### Amazon S3 {#amazons3}

日志转发到Amazon S3支持AEM和Dispatcher日志，尚不支持CDN日志。

>[!NOTE]
>
>定期写入S3的日志，每种日志文件类型每10分钟写入一次。  这可能会导致切换功能后将日志写入S3的初始延迟。  [有关此行为的详细信息](https://docs.fluentbit.io/manual/pipeline/outputs/s3#differences-between-s3-and-other-fluent-bit-outputs)。

```yaml
kind: "LogForwarding"
version: "1.0"
metadata:
  envTypes: ["dev"]
data:
  awsS3:
    default:
      enabled: true
      region: "your-bucket-region"
      bucket: "your_bucket_name"
      accessKey: "${{AWS_S3_ACCESS_KEY}}"
      secretAccessKey: "${{AWS_S3_SECRET_ACCESS_KEY}}"
```

要使用S3日志转发器，您需要为AWS IAM用户预配置用于访问S3存储段的适当策略。  有关如何创建IAM用户凭据的信息，请参阅[AWS IAM用户文档](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html)。

IAM策略应允许用户使用`s3:putObject`。  例如：

```json
 {
    "Version": "2012-10-17",
    "Statement": [{
        "Effect": "Allow",
        "Action": [
            "s3:PutObject"
        ],
        "Resource": "arn:aws:s3:::your_bucket_name/*"
    }]
}
```

有关如何实施的更多信息，请参阅[AWS存储段策略文档](https://docs.aws.amazon.com/AmazonS3/latest/userguide/bucket-policies.html)。

### Azure Blob存储 {#azureblob}

```yaml
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

如果日志在之前正常工作后停止传递，请检查您配置的SAS令牌是否仍然有效，因为它可能已过期。

#### Azure Blob存储CDN日志 {#azureblob-cdn}

每个全局分布式日志服务器每隔几秒会在`aemcdn`文件夹下生成一个新文件。 创建后，该文件将不再附加到。 文件名格式为YYYY-MM-DDThh:mm:ss.sss-uniqueid.log。 例如，2024-03-04T10:00:00.000-WnFWYN9BpOUs2aOVn4ee.log。

例如，在某个时间点：

```text
aemcdn/
   2024-03-04T10:00:00.000-abc.log
   2024-03-04T10:00:00.000-def.log
```

30秒后：

```text
aemcdn/
   2024-03-04T10:00:00.000-abc.log
   2024-03-04T10:00:00.000-def.log
   2024-03-04T10:00:30.000-ghi.log
   2024-03-04T10:00:30.000-jkl.log
   2024-03-04T10:00:30.000-mno.log
```

每个文件都包含多个json日志条目，每个条目位于一行中。 日志条目格式在[AEM as a Cloud Service日志记录](/help/implementing/developing/introduction/logging.md)下描述，每个日志条目还包括以下[日志条目格式](#log-formats)部分中提到的其他属性。

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

```yaml
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

#### 注意事项

* 创建API密钥，而不与特定的云提供商进行任何集成。
* 标记属性是可选的
* 对于AEM日志，Datadog源标记设置为`aemaccess`、`aemerror`、`aemrequest`、`aemdispatcher`、`aemhttpdaccess`或`aemhttpderror`之一
* 对于CDN日志，Datadog源标记设置为`aemcdn`
* Datadog服务标记设置为`adobeaemcloud`，但您可以在标记部分中覆盖它
* 如果您的摄取管道使用Datadog标记确定转发日志的适当索引，请验证这些标记在日志转发YAML文件中是否正确配置。 如果管道依赖于缺少标记，则可能会阻止成功的日志摄取。

### Elasticsearch和OpenSearch {#elastic}

```yaml
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

#### 注意事项

* 默认情况下，端口为443。 可以选择使用名为`port`的属性覆盖它
* 对于凭据，请确保使用部署凭据，而不是帐户凭据。 这些是在屏幕中生成的凭据，可能与以下图像类似：

![弹性部署凭据](/help/implementing/developing/introduction/assets/ec-creds.png)

* 对于AEM日志，`index`设置为`aemaccess`、`aemerror`、`aemrequest`、`aemdispatcher`、`aemhttpdaccess`或`aemhttpderror`之一
* 可选的pipeline属性应设置为Elasticsearch或OpenSearch摄取管道的名称，可以将其配置为将日志条目路由到相应的索引。 管道的处理器类型必须设置为&#x200B;*script*，脚本语言应设置为&#x200B;*无痛苦*。 以下是将日志条目路由到索引（如aemaccess_dev_26_06_2024）的脚本片段示例：

```text
def envType = ctx.aem_env_type != null ? ctx.aem_env_type : 'unknown';
def sourceType = ctx._index;
def date = new SimpleDateFormat('dd_MM_yyyy').format(new Date());
ctx._index = sourceType + "_" + envType + "_" + date;
```

### HTTPS {#https}

```yaml
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

#### 注意事项

* URL字符串必须包含&#x200B;**https://**，否则验证将失败。
* URL可能包含端口。 例如，`https://example.com:8443/aem_logs/aem`。如果url字符串中未包含任何端口，则采用端口443（默认的HTTPS端口）。

#### HTTPS CDN日志 {#https-cdn}

Web请求(POST)将使用json有效负载连续发送，该有效负载是一个日志条目数组，日志条目格式在[AEM as a Cloud Service日志记录](/help/implementing/developing/introduction/logging.md#cdn-log)下描述。 下面的[日志条目格式](#log-formats)部分中提及了其他属性。

还有一个名为`sourcetype`的属性，该属性设置为值`aemcdn`。

>[!NOTE]
>
> 在发送第一个CDN日志条目之前，您的HTTP服务器必须成功完成一次性质询：发送到路径``/.well-known/fastly/logging/challenge``的请求在正文中必须以星号``*``和200状态代码响应。

#### HTTPS AEM日志 {#https-aem}

对于AEM日志（包括apache/dispacher），将连续发送Web请求(POST)，JSON有效负载为日志条目数组，其日志条目格式多种多样，如[AEM as a Cloud Service日志记录](/help/implementing/developing/introduction/logging.md)中所述。 下面的[日志条目格式](#log-formats)部分中提及了其他属性。

还有一个名为`Source-Type`的属性，该属性设置为以下值之一：

* aemaccess
* aemerror
* aemrequest
* aemdispatcher
* aemhttpdaccess
* aemhttpderror

### New Relic日志API {#newrelic-https}

将日志转发到New Relic会利用New Relic HTTPS API进行摄取。  目前，它仅支持来自AEM和Dispatcher的日志；尚不支持CDN日志。

```yaml
  kind: "LogForwarding"
  version: "1"
  metadata:
    envTypes: ["dev"]
  data:
    newRelic:
      default:
        enabled: true
        uri: "https://log-api.newrelic.com/log/v1"
        apiKey: "${{NR_API_KEY}}"
```

>[!NOTE]
>
>日志转发到New Relic仅适用于客户拥有的New Relic帐户。
>
>向[aemcs-logforwarding-beta@adobe.com](mailto:aemcs-logforwarding-beta@adobe.com)发送电子邮件以请求访问权限。
>
>New Relic根据您的New Relic帐户配置位置提供特定于区域的端点。  有关详细信息，请参阅[New Relic文档](https://docs.newrelic.com/docs/logs/log-api/introduction-log-api/#endpoint)。

### Dynatrace日志API {#dynatrace-https}

将日志转发到Dynatrace会利用Dynatrace HTTPS API进行摄取。  目前，它仅支持来自AEM和Dispatcher的日志；尚不支持CDN日志。

令牌需要“摄取日志”范围属性。

```yaml
  kind: "LogForwarding"
  version: "1"
  metadata:
    envTypes: ["dev"]
  data:
    dynatrace:
      default:
        enabled: true
        environmentId: "${{DYNATRACE_ENVID}}"
        token: "${{DYNATRACE_TOKEN}}"  
```

>[!NOTE]
>
> 向[aemcs-logforwarding-beta@adobe.com](mailto:aemcs-logforwarding-beta@adobe.com)发送电子邮件以请求访问权限。

### Splunk {#splunk}

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
      index: "aemaacs"
```

#### 注意事项

* 默认情况下，端口为443。 可以选择使用名为`port`的属性覆盖它。
* 根据特定日志，sourcetype字段将具有以下值之一： *aemaccess*，*aemerror*，
  *aemrequest*，*aemdispatcher*，*aemhttpdaccess*，*aemhttpderror*，*aemcdn*
* 如果所需的IP已列入允许列表并且日志仍未交付，请验证是否没有实施Splunk令牌验证的防火墙规则。 Fastly执行初始验证步骤，其中有意发送无效的Splunk令牌。 如果防火墙设置为终止使用无效Splunk令牌的连接，则验证过程将失败，从而阻止Fastly将日志投放到您的Splunk实例。

>[!NOTE]
>
> [如果将](#legacy-migration)从旧版日志转发迁移到此自助模型，则发送到您的Splunk索引的`sourcetype`字段的值可能已更改，因此请进行相应调整。

### Sumo逻辑 {#sumologic}

日志转发到Sumo Logic支持AEM和Dispatcher日志；尚不支持CDN日志。

在配置Sumo Logic进行数据摄取时，您会看到“HTTP Source地址”，该地址在单个字符串中提供主机、接收者URI和私钥。  例如：

`https://collectors.de.sumologic.com/receiver/v1/http/ZaVnC...`

您需要复制URL的最后一个部分（前面没有`/`）并将其添加为[CloudManager机密环境变量](/help/operations/config-pipeline.md#secret-env-vars)，如上面[设置](#setup)部分中所述，然后在您的配置中引用该变量。  下面提供了一个示例。

```yaml
kind: "LogForwarding"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  sumologic:
    default:
      enabled: true
      collectorURL: "https://collectors.de.sumologic.com/receiver/v1/http"
      privateKey: "${{SUMOLOGIC_PRIVATE_KEY}}"
      index: "aem-logs"
```

>[!NOTE]
> 您需要订购Sumo Logic Enterprise才能使用“索引”字段功能。  非企业订阅的日志将作为标准路由到`sumologic_default`分区。  有关详细信息，请参阅[Sumo逻辑分区文档](https://help.sumologic.com/docs/search/optimize-search-partitions/)。

## 日志条目格式 {#log-formats}

有关每种日志类型(CDN日志和包括Apache/Dispatcher的AEM as a Cloud ServiceAEM日志)的格式，请参阅[日志记录](/help/implementing/developing/introduction/logging.md)。

由于来自多个程序和环境的日志可能会转发到同一日志记录目标，因此除了日志记录文章中所述的输出之外，每个日志条目中还将包含以下属性：

* aem_env_id
* aem_env_type
* aem_program_id
* aem_tier

例如，属性可能具有以下值：

```text
aem_env_id: 1242
aem_env_type: dev
aem_program_id: 12314
aem_tier: author
```

## 从旧版日志转发迁移 {#legacy-migration}

在通过自助模型实现日志转发配置之前，已请求客户打开支持工单，Adobe将在其中启动集成。

欢迎已由Adobe以这种方式设置的客户在方便时改用自助模式。 进行此过渡有几个原因：

* 已配置新环境（例如，新的开发环境或RDE）。
* 更改您现有的Splunk端点或凭据。
* Adobe已在CDN日志可用之前设置日志转发，您想要接收CDN日志。
* 有意识地决定主动适应自助服务模式，使您的组织甚至在对时间敏感的更改之前就拥有了知识。

准备迁移时，只需按照前几节所述配置YAML文件即可。 使用Cloud Manager配置管道部署到应应用配置的每个环境。

建议将配置部署到所有环境，以便所有环境都处于自助控制状态，但不是必需的。 如果没有，您可能会忘记哪些环境已由Adobe配置，哪些是自助式配置的。

>[!NOTE]
>
>发送到Splunk索引的`sourcetype`字段的值可能已更改，因此请进行相应调整。
>
>在将日志转发部署到之前由Adobe支持配置的环境时，您最多可能会收到几个小时的重复日志。 这将最终自动解决。
