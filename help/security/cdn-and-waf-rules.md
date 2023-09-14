---
title: 配置流量过滤器规则（使用WAF规则）
description: 使用流量过滤规则（带WAF规则）过滤流量
source-git-commit: b1b184b63ab6cdeb8a4e0019c31a34db59438a3d
workflow-type: tm+mt
source-wordcount: '2709'
ht-degree: 70%

---


# 配置流量过滤器规则（使用WAF规则）以过滤流量 {#configuring-cdn-and-waf-rules-to-filter-traffic}

>[!NOTE]
>
>此功能尚未普遍可用。要加入正在进行的早期采用者计划，请将电子邮件发送到 **aemcs-waf-adopter@adobe.com**，包括您的组织名称以及您对此功能感兴趣的上下文。

Adobe会尝试减少针对客户网站的攻击，但主动过滤匹配特定模式的流量可能会很有用，这样恶意流量就不会进入您的应用程序。 可能的方法包括：

* Apache 层模块，例如 `mod_security`
* 配置通过Cloud Manager的配置管道部署到CDN的流量过滤器规则

本文介绍了流量过滤器规则方法。 这些规则中的大多数都会根据请求属性和请求标头（包括IP、路径和用户代理）阻止或允许请求。 这些规则可由所有AEMas a Cloud Service的Sites和Forms客户配置。

许可WAF（Web应用程序防火墙）加载项的客户还可以配置另一类名为“WAF流量过滤器规则”（简称WAF规则）的规则。 这些WAF规则会阻止与已知与恶意通信相关的各种模式匹配的请求。 请联系您的Adobe客户团队，了解有关授权此即将推出的功能的详细信息。 请注意，早期采用者计划期间不需要额外的许可证。

流量过滤器规则可以部署到生产（非沙盒）程序中的所有云环境类型(RDE、dev、stage、prod)。

## 设置 {#setup}

1. 首先，在 git 中的顶层文件夹中创建以下文件夹和文件结构：

   ```
   config/
        cdn/
           cdn.yaml
   ```

1. `cdn.yaml` 应包含元数据以及流量过滤器规则和WAF规则的列表。

   ```
   kind: "CDN"
   version: "1"
   metadata:
     envTypes: ["dev"]
   data:
     trafficFilters:
       rules:
         ...
   ```

“kind”参数应设置为“CDN”，版本应设置为架构版本，当前为“1”。请参阅下面的示例。


<!-- Two properties -- `envType` and `envId` -- may be included to limit the scope of the rules. The envType property may have values "dev", "stage", or "prod", while the envId property is the environment (e.g., "53245"). This approach is useful if it is desired to have a single configuration pipeline, even if some environments have different rules. However, a different approach could be to have multiple configuration pipelines, each pointing to different repositories or git branches. -->

1. 要配置WAF规则，必须在Cloud Manager中启用WAF，如下面的新程序和现有程序方案所述。 请注意，必须为 WAF 购买单独的许可证。

   1. 要在新计划上配置 WAF，请选中&#x200B;**安全性**&#x200B;选项卡中的 **WAF-DDOS 保护**&#x200B;复选框，如下所示。继续执行[添加生产计划](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)中描述的步骤以创建计划

   1. 要在现有计划上配置 WAF，请执行[编辑计划](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md)文档中所述步骤来选择&#x200B;**编辑计划**&#x200B;选项。然后，在向导的&#x200B;**安全性**&#x200B;选项卡中，您可以随时取消选中或选中 WAF-DDOS 选项

1. 对于 RDE 以外的环境类型，请执行 Cloud Manager 配置管道，可按如下所述进行配置。

   1. 从 Cloud Manager 主页上的管道信息卡，选择&#x200B;**添加生产管道**&#x200B;或者&#x200B;**添加非生产管道**&#x200B;以启动添加管道向导
   1. 选择配置选项卡中的&#x200B;**部署管道**

      ![选择“部署管道”选项](/help/security/assets/deployment.png)

   1. 为管道命名并选择部署触发器，然后选择&#x200B;**继续**
   1. 在&#x200B;**源代码**&#x200B;选项卡中，选择&#x200B;**定向部署**，然后选择&#x200B;**配置**

      ![选择目标部署](/help/security/assets/target-deployment.png)

   1. 根据需要选择存储库和分支。如果所选环境存在配置管道，则会禁用此选择。

      ![配置管道概述](/help/security/assets/config-pipeline.png)

      >[!NOTE]
      >
      > 用户必须以部署管理员身份登录才能配置或运行这些管道。
      > 此外，每个环境只能配置和运行一个配置管道。

   1. 选择&#x200B;**保存**。您的新管道将显示在管道信息卡中，并且会在您就绪后运行。
   1. 对于RDE，将使用命令行，但目前不支持RDE。

## 流量过滤器规则语法 {#rules-syntax}

您可以配置 `traffic filter rules` 以匹配各种模式，如IP、用户代理、请求标头、主机名、地理位置和URL。

许可WAF产品的客户还可以配置一种名为的特殊流量过滤器规则类别 `WAF traffic filter rules` （简称WAF规则）引用了一个或多个WAF标志，这些标志在其自身的以下部分中列出。

下面是一组流量过滤器规则的示例，其中还包括WAF规则。

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
      - name: "path-rule"
        when: { reqProperty: path, equals: /block-me }
        action:
          type: block
      - name: "Enable-SQL-Injection-and-XSS-waf-rules-globally"
        when: { reqProperty: path, like: "*" }
        action:
          type: block
          wafFlags: [ SQLI, XSS]
```

cdn.yaml文件中流量过滤器规则的格式描述如下。 请参阅后面部分中的一些示例。


| **属性** | **大多数流量过滤器规则** | **WAF流量过滤器规则** | **类型** | **默认值** | **描述** |
|---|---|---|---|---|---|
| name | X | X | `string` | - | 规则名称（长度为 64 个字符，只能包含字母数字和 -） |
| when | X | X | `Condition` | - | 基本结构为：<br><br>`{ <getter>: <value>, <predicate>: <value> }`<br><br>请参阅下面的条件结构语法，其中描述了 getter、谓词以及如何组合多个条件。 |
| 动作 | X | X | `Action` | 日志 | log、allow、block、log或action对象默认为log |
| rateLimit | X |   | `RateLimit` | 未定义 | 速率限制配置。如果未定义，则禁用速率限制。<br><br>以下单独部分描述了 rateLimit 语法及示例。 |

### 条件结构 {#condition-structure}

条件可以是一个简单条件或一组条件。

**简单条件**

简单条件由一个 getter 和一个谓词组成。

```
{ <getter>: <value>, <predicate>: <value> }
```

**组条件**

一组条件由多个简单和/或组条件组成。

```
<allOf|anyOf>:
  - { <getter>: <value>, <predicate>: <value> }
  - { <getter>: <value>, <predicate>: <value> }
  - <allOf|anyOf>:
    - { <getter>: <value>, <predicate>: <value> }
```

| **属性** | **类型** | **含义** |
|---|---|---|
| **allOf** | `array[Condition]` | **and** 运算。如果所有列出的条件都返回 true，则为 true |
| **anyOf** | `array[Condition]` | **or** 运算。如果列出的任意条件返回 true，则为 true |

**Getter**

| **属性** | **类型** | **描述** |
|---|---|---|
| reqProperty | `string` | 请求属性。<br><br>下列项目之一：`path`、`queryString`、`method`、`tier`、`domain`、`clientIp`、`clientCountry`<br><br>域属性是请求的主机标头的小写转换。在字符串比较中，它很有用，可确保不会因区分大小写而错过匹配。<br><br>`clientCountry` 使用 [https://en.wikipedia.org/wiki/Regional_indicator_symbol](https://en.wikipedia.org/wiki/Regional_indicator_symbol) 上显示的两字母代码 |
| reqHeader | `string` | 返回具有指定名称的请求头 |
| queryParam | `string` | 返回具有指定名称的查询参数 |
| cookie | `string` | 返回具有指定名称的 Cookie |

**谓词**

| **属性** | **类型** | **含义** |
|---|---|---|
| **equals** | `string` | 如果 getter 结果等于提供的值，则为 true |
| **doesNotEqual** | `string` | 如果 getter 结果不等于提供的值，则为 true |
| **like** | `string` | 如果 getter 结果与提供的模式匹配，则为 true |
| **notLike** | `string` | 如果 getter 结果与提供的模式不匹配，则为 true |
| **matches** | `string` | 如果 getter 结果与提供的正则表达式匹配，则为 true |
| **doesNotMatch** | `string` | 如果 getter 结果与提供的正则表达式不匹配，则为 true |
| **in** | `array[string]` | 如果提供的列表包含 getter 结果，则为 true |
| **notIn** | `array[string]` | 如果提供的列表不包含 getter 结果，则为 true |

### 操作结构 {#action-structure}

指定者 `action` 字段，可以是指定操作类型（允许、阻止、日志）并假定所有其他选项的默认值的字符串，也可以是定义规则类型的对象，定义方式为 `type` 必填字段，以及适用于该类型的其他选项。

**操作类型**

下表中的操作根据其类型划分优先级，其排序反映了操作的执行顺序：

| **名称** | **允许的属性** | **含义** |
|---|---|---|
| **允许** | `wafFlags` （可选） | 如果wafFlags不存在，则停止进一步的规则处理并继续提供响应。 如果wafFlags存在，它将禁用指定的WAF保护并继续执行进一步的规则处理。 |
| **块** | `status, wafFlags` （可选且互斥） | 如果wafFlags不存在，则返回跳过所有其他属性的HTTP错误，错误代码由status属性定义或默认为406。 如果wafFlags存在，则它启用指定的WAF保护并继续进一步的规则处理。 |
| **日志** | `wafFlags` （可选） | 记录规则已触发的事实，否则不会影响处理。 wafFlags无效 |

### WAF标记列表 {#waf-flags-list}

此 `wafFlag` 资产可能包括：

| **标志ID** | **标志名称** | **描述** |
|---|---|---|
| SQLI | SQL 注入 | SQL 注入是指尝试通过执行任意数据库查询来获取应用程序的访问权限或特权信息。 |
| BACKDOOR | 后门 | 后门信号是指尝试确定系统上是否存在公共后门文件的请求。 |
| CMDEXE | 命令执行 | 命令执行是指尝试通过用户输入的任意系统命令来获得控制权限或损坏目标系统。 |
| XSS | 跨站点脚本 | 跨站点脚本是指尝试通过恶意 JavaScript 代码来劫持用户帐户或 Web 浏览会话。 |
| TRAVERSAL | 目录遍历 | 目录遍历是指尝试在整个系统中导航特权文件夹以获取敏感信息。 |
| USERAGENT | 攻击工具 | 攻击工具是指使用自动化软件来找出安全漏洞或尝试利用已发现的漏洞。 |
| LOG4J-JNDI | Log4J JNDI | Log4J JNDI 攻击尝试利用 2.16.0 版之前的 Log4J 版本中存在的 [Log4Shell 漏洞](https://en.wikipedia.org/wiki/Log4Shell) |
| AWS SSRF | AWS-SSRF | 服务器端请求伪造 (SSRF) 是一种请求，它尝试将 Web 应用程序发出的请求发送到目标内部系统。AWS SSRF 攻击使用 SSRF 获取 Amazon Web Services (AWS) 密钥并获取对 S3 存储桶及其数据的访问权限。 |
| BHH | 错误跳头 | 错误跳头是指尝试通过格式错误的 Transfer-Encoding (TE) 或 Content-Length (CL) 头或格式良好的 TE 和 CL 头进行 HTTP 走私 |
| ABNORMALPATH | 异常路径 | 异常路径表示原始路径与规范化路径不同（例如，`/foo/./bar` 标准化为 `/foo/bar`） |
| COMPRESSED | 检测到压缩 | POST 请求正文被压缩，无法检查。例如，如果指定了“Content-Encoding: gzip”请求头，并且 POST 正文不是纯文本。 |
| DOUBLEENCODING | 双重编码 | 双重编码检查双重编码 html 字符的规避技术 |
| FORCEFULBROWSING | 强制浏览 | 强制浏览是指尝试访问管理页面失败 |
| NOTUTF8 | 无效编码 | 无效编码可能会促使服务器将请求中的恶意字符转换为响应，从而导致拒绝服务或 XSS |
| JSON-ERROR | JSON 编码错误 | 指定为在“Content-Type”请求头中包含 JSON，但包含 JSON 解析错误的 POST、PUT 或 PATCH 请求正文。这通常与编程错误或自动或恶意请求有关。 |
| MALFORMED-DATA | 请求正文中的格式错误的数据 | 根据“Content-Type”请求头，格式错误的 POST、PUT 或 PATCH 请求正文。例如，如果指定了“Content-Type: application/x-www-form-urlencoded”请求头并包含 POST 正文 json。这通常是编程错误、自动或恶意请求。需要代理 3.2 版或更高版本。 |
| SANS | 恶意 IP 流量 | 已报告从事恶意活动的 IP 地址的 [SANS Internet Storm Center](https://isc.sans.edu/) 列表 |
| SIGSCI-IP | 网络效应 | 由 SignalSciences 标记的 IP：每当决策引擎因恶意信号而标记 IP 时，IP 将传播给所有客户。随后，记录来自这些 IP 地址的后续请求，其中包含标记持续时间的任何其他信号 |
| NO-CONTENT-TYPE | 缺少“Content-Type”请求头 | 不具有“Content-Type”请求头的 POST、PUT 或 PATCH 请求。在此示例中，默认情况下，应用程序服务器应假定“Content-Type: text/plain; charset=us-ascii”。许多自动和恶意请求可能缺少“内容类型”。 |
| NOUA | 无用户代理 | 许多自动和恶意请求使用虚假或缺失的用户代理，导致难以识别发出请求的设备类型。 |
| TORNODE | Tor 流量 | Tor 是可以隐藏用户身份的软件。Tor 流量尖峰可能表明攻击者正在试图掩盖其位置。 |
| DATACENTER | 数据中心流量 | 数据中心流量是源自确定的托管提供商的非自然流量。此类流量通常与实际最终用户无关。 |
| NULLBYTE | 空字节 | 空字节通常不会出现在请求中，并表明请求的格式错误且可能是恶意请求。 |
| IMPOSTOR | 搜索机器人伪装者 | 搜索机器人伪装者是指冒充 Google 或 Bing 搜索机器人且不合法的人员。请注意，它本身不依赖于响应，但必须先在云中解析，因此不应在预规则中使用它。 |
| PRIVATEFILE | 私有文件 | 私有文件通常是机密性的，例如 Apache `.htaccess` 文件或可能泄露敏感信息的配置文件 |
| SCANNER | 扫描程序 | 标识常用的扫描服务和工具 |
| RESPONSESPLIT | HTTP 响应拆分 | 标识何时将 CRLF 字符作为输入提交给应用程序以将标头注入 HTTP 响应 |
| XML-ERROR | XML 编码错误 | 指定为在“Content-Type”请求头中包含 XML，但包含 XML 解析错误的 POST、PUT 或 PATCH 请求正文。这通常与编程错误或自动或恶意请求有关。 |

## 注意事项 {#considerations}

* 在创建两个发生冲突的规则时，allow 规则将始终优先于 block 规则。例如，如果您创建一个规则来阻止特定路径，并创建一个规则来允许一个特定的 IP 地址，则来自被阻止路径的 IP 地址的请求将被允许。

* 如果规则匹配但被阻止，CDN 会提供 `406` 返回代码。

* 配置文件不应包含密钥，因为有权访问Git存储库的任何人都可以读取它们。

## 规则示例 {#examples}

下面是一些规则示例。请参阅[速率限制部分](#rules-with-rate-limits)以进一步了解速率限制示例。

**示例 1**

此规则阻止来自 IP 192.168.1.1 的请求：

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
     rules:
       - name: "block-request-from-ip"
         when: { reqProperty: clientIp, equals: "192.168.1.1" }
         action:
           type: block
```

**示例 2**

此规则阻止发布时带包含 Chrome 的 User-Agent 的路径`/helloworld` 的请求：

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
     rules:
       - name: "block-request-from-chrome-on-path-helloworld-for-publish-tier"
         when: { reqProperty: clientIp, equals: "192.168.1.1" }
           allOf:
            - { reqProperty: path, equals: /helloworld }
            - { reqProperty: tier, equals: publish }
            - { reqHeader: user-agent, matches: '.*Chrome.*'  }
           action:
             type: block
```

**示例 3**

此规则阻止包含查询参数 `foo` 的请求，但允许来自 IP 192.168.1.1 的每个请求：

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
      - name: "block-request-that-contains-query-parameter-foo"
        when: { queryParam: url-param, equals: foo }
        action:
          type: block
      - name: "allow-all-requests-from-ip"
        when: { reqProperty: clientIp, equals: 192.168.1.1 }
        action:
          type: allow
```

**示例 4**

此规则阻止对路径 /block-me 的请求，并阻止与 SQLI 或 XSS 模式匹配的每个请求：

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
      - name: "path-rule"
        when: { reqProperty: path, equals: /block-me }
        action:
          type: block
      - name: "Enable-SQL-Injection-and-XSS-waf-rules-globally"
        when: { reqProperty: path, like: "*" }
        action:
          type: block
          wafFlags: [ SQLI, XSS]
```

**示例 4**

此规则阻止对OFAC国家/地区的访问：

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
      - name: block-ofac-countries
        when:
          allOf:
            - { reqProperty: tier, equals: publish }
            - reqProperty: clientCountry
              in:
                - SY
                - BY
                - MM
                - KP
                - IQ
                - CD
                - SD
                - IR
                - LR
                - ZW
                - CU
                - CI
        action: block
```

## 具有速率限制的规则 {#rules-with-rate-limits}

有时，仅在匹配随时间推移超过特定速率时阻止与规则匹配的流量。设置一个 `rateLimit` 属性值可限制那些符合规则条件的请求的速率。

### rateLimit 结构 {#ratelimit-structure}

| **属性** | **类型** | **默认** | **含义** |
|---|---|---|---|
| limit | 10 和 10000 之间的整数 | 必填 | 触发规则的请求速率（以每秒请求数为单位）。 |
| window | 整数枚举：1、10 或 60 | 10 | 计算请求速率的采样时段（以秒为单位）。 |
| penalty | 60 和 3600 之间的整数 | 300（5 分钟） | 匹配请求被阻止的时段（以秒为单位）（四舍五入到最接近的分钟）。 |
| groupBy | 数组[Getter] | 无 | 速率限制器计数器将由一组请求属性（例如clientIp）聚合。 |

### 示例 {#ratelimiting-examples}

**示例 1**

该规则会在客户端在过去60秒内超过100请求/秒时将其阻止5分钟：

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    - name: limit-requests-client-ip
      when:
        reqProperty: path
        like: '*'
      rateLimit:
        limit: 60
        window: 10
        penalty: 300
        groupBy:
          - reqProperty: clientIp
      action: block
```

**示例 2**

当路径/critical/resource在过去60秒内超过100请求/秒时，阻止对60s的请求：

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
      - name: rate-limit-example
        when: { reqProperty: path, equals: /critical/resource }
        action:
          type: block
        rateLimit: { limit: 100, window: 60, penalty: 60 }
```

## CDN 日志 {#cdn-logs}

AEM as a Cloud Service 提供对 CDN 日志的访问权限，这对于包括缓存命中率优化以及配置 CDN 和 WAF 规则在内的用例非常有用。在选择创作和发布服务时，CDN 日志显示在 Cloud Manager 的&#x200B;**下载日志**&#x200B;对话框中。

“规则”属性描述匹配哪些流量过滤器规则，具有以下模式：

```
"rules": "match=<matching-customer-named-rules-that-are-matched>,waf=<matching-WAF-rules>,action=<action_type>"
```

例如：

```
"rules": "match=Block-Traffic-under-private-folder,Enable-SQL-injection-everywhere,waf="SQLI,SANS",action=block"
```

规则的行为方式如下：

* 任何匹配规则的客户声明的规则名称都将列在matches属性中。
* action属性详细说明规则是否具有阻止、允许或记录的效果。
* 如果WAF已许可并启用，则waf属性将列出检测到的任何waf规则（例如SQLI；请注意，这与客户声明的名称无关），无论配置中是否列出了waf规则。
* 如果没有客户声明的规则匹配且没有waf规则匹配，则rules属性将为空白。

通常，对CDN的所有请求都会在日志条目中显示匹配规则，无论这是CDN点击、通过还是未通过。 但是，WAF 规则仅显示在被视为 CDN 未命中或通过而非 CDN 命中的 CDN 请求的日志条目中。

以下示例显示了一个cdn.yaml示例和两个CDN日志条目：


```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
      - name: "path-rule"
        when: { reqProperty: path, equals: /block-me }
        action: block
      - name: "Enable-SQL-Injection-and-XSS-waf-rules-globally"
        when: { reqProperty: path, like: "*" }
        action:
          type: block
          wafFlags: [ SQLI, XSS ]
```

```
{
"timestamp": "2023-05-26T09:20:01+0000",
"ttfb": 19,
"cli_ip": "147.160.230.112",
"cli_country": "CH",
"rid": "974e67f6",
"req_ua": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/14.0.3 Safari/605.1.15",
"host": "example.com",
"url": "/block-me",
"method": "GET",
"res_ctype": "",
"cache": "PASS",
"status": 406,
"res_age": 0,
"pop": "PAR",
"rules": "match=path-rule,action=blocked"
}
```

```
{
"timestamp": "2023-05-26T09:20:01+0000",
"ttfb": 19,
"cli_ip": "147.160.230.112",
"cli_country": "CH",
"req_ua": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/14.0.3 Safari/605.1.15",
"rid": "974e67f6",
"host": "example.com",
"url": "/?sqli=%27%29%20UNION%20ALL%20SELECT%20NULL%2CNULL%2CNULL%2CNULL%2CNULL%2CNULL%2CNULL%2CNULL%2CNULL%2CNULL--%20fAPK",
"method": "GET",
"res_ctype": "image/png",
"cache": "PASS",
"status": 406,
"res_age": 0,
"pop": "PAR",
"rules": "match=Enable-SQL-Injection-and-XSS-waf-rules-globally,waf=SQLI,action=blocked"
}
```

### 日志格式 {#cdn-log-format}

以下是 CDN 日志中使用的字段名称列表以及简要说明。

| **字段名** | **描述** |
|---|---|
| *timestamp* | TLS 终止后请求开始的时间。 |
| *ttfb* | *首字节时间*&#x200B;的缩写。从请求开始到响应正文开始流式传输之前的时间间隔。 |
| *cli_ip* | 客户端 IP 地址。 |
| *cli_country* | 客户国家/地区的两字母 [ISO 3166-1](https://en.wikipedia.org/wiki/ISO_3166-1) alpha-2 国家/地区代码。 |
| *rid* | 用于唯一标识请求的请求头的值。 |
| *req_ua* | 负责发出给定 HTTP 请求的用户代理。 |
| *host* | 请求所针对的颁发机构。 |
| *url* | 完整路径，包括查询参数。 |
| *method* | 客户端发送的 HTTP 方法，例如“GET”或“POST”。 |
| *res_ctype* | 用于指示资源的原始媒体类型的 Content-Type。 |
| *cache* | 缓存的状态。可能的值为 HIT、MISS 或 PASS |
| *状态* | 整数值形式的 HTTP 状态代码。 |
| *res_age* | 响应已缓存（在所有节点中）的时间量（以秒为单位）。 |
| *pop* | CDN 缓存服务器的数据中心。 |
| *rules* | 任何匹配规则的名称。<br><br>还指示匹配是否产生块。<br><br>例如，“`match=Enable-SQL-Injection-and-XSS-waf-rules-globally,waf=SQLI,action=blocked`”<br><br>如果没有匹配的规则，则为空。 |
