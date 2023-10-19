---
title: 配置流量过滤规则与 WAF 规则
description: 结合使用流量过滤规则和 WAF 规则来过滤流量
exl-id: 6a0248ad-1dee-4a3c-91e4-ddbabb28645c
source-git-commit: 550ef9a969dc184fccbfd3b79716744cd80ce463
workflow-type: tm+mt
source-wordcount: '3826'
ht-degree: 70%

---

# 配置流量过滤规则与 WAF 规则来过滤流量 {#configuring-cdn-and-waf-rules-to-filter-traffic}

>[!NOTE]
>
>此功能尚未普遍可用。要加入正在进行的早期采用者计划，请将电子邮件发送到 **aemcs-waf-adopter@adobe.com**，包括您的组织名称以及您对此功能感兴趣的上下文。

Adobe 尝试缓解对客户网站发起的攻击，而主动过滤与某些模式匹配的流量，从而使恶意流量无法到达您的应用程序可能会有帮助。可能的方法包括：

* Apache 层模块，例如 `mod_security`
* 配置通过 Cloud Manager 的配置管道部署到 CDN 的流量过滤规则。

本文介绍流量过滤规则方法。此类规则中的大多数规则会根据请求属性和请求标头（包括 IP、路径和用户代理）阻止或允许请求。所有 AEM as a Cloud Service Sites 和 Forms 客户都可以配置这些规则。

许可 WAF（Web 应用程序防火墙）加载项的客户还可以配置称为“WAF 流量过滤规则”（简称 WAF 规则）的附加类别的规则。这些 WAF 规则阻止已知与恶意流量相关的各种模式相匹配的请求。请联系您的 Adobe 帐户团队，了解有关许可这项即将推出的功能的详细信息。请注意，早期采用者计划期间不需要额外的许可证。

流量过滤规则可部署到所有用于生产（非沙盒）项目的云环境类型（RDE、开发、暂存和生产）。

## 设置 {#setup}

1. 首先，在 git 中的顶层文件夹中创建以下文件夹和文件结构：

   ```
   config/
        cdn.yaml
   ```

1. `cdn.yaml` 应包含元数据以及流量过滤器规则和 WAF 规则的列表。

   ```
   kind: "CDN"
   version: "1"
   metadata:
     envTypes: ["dev"]
   data:
     trafficFilters:
       rules:
       # Block simple path
       - name: block-path
         when:
           allOf:
             - reqProperty: tier
               matches: "author|publish"
             - reqProperty: path
               equals: '/block/me'
         action: block
   ```

“kind”参数应设置为“CDN”，版本应设置为架构版本，当前为“1”。请参阅下面的示例。


<!-- Two properties -- `envType` and `envId` -- may be included to limit the scope of the rules. The envType property may have values "dev", "stage", or "prod", while the envId property is the environment (e.g., "53245"). This approach is useful if it is desired to have a single configuration pipeline, even if some environments have different rules. However, a different approach could be to have multiple configuration pipelines, each pointing to different repositories or git branches. -->

1. 要配置 WAF 规则，必须在 Cloud Manager 中为新的和现有的项目场景启用 WAF，如下所述。请注意，必须为 WAF 购买单独的许可证。

   1. 要在新计划上配置 WAF，请选中&#x200B;**安全性**&#x200B;选项卡中的 **WAF-DDOS 保护**&#x200B;复选框，如下所示。继续执行[添加生产计划](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)中描述的步骤以创建计划

   1. 要在现有计划上配置 WAF，请执行[编辑计划](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md)文档中所述步骤来选择&#x200B;**编辑计划**&#x200B;选项。然后，在向导的&#x200B;**安全性**&#x200B;选项卡中，您可以随时取消选中或选中 WAF-DDOS 选项

1. 对于 RDE 以外的环境类型，请执行 Cloud Manager 配置管道，可按如下所述进行配置。

   1. 从 Cloud Manager 主页上的管道信息卡，选择&#x200B;**添加生产管道**&#x200B;或者&#x200B;**添加非生产管道**&#x200B;以启动添加管道向导
   1. 选择配置选项卡中的&#x200B;**部署管道**

      ![选择“部署管道”选项](/help/security/assets/deployment.png)

   1. 为管道命名并选择部署触发器，然后选择&#x200B;**继续**
   1. 在&#x200B;**源代码**&#x200B;选项卡中，选择&#x200B;**定向部署**，然后选择&#x200B;**配置**

      ![选择定向部署](/help/security/assets/target-deployment.png)

   1. 根据需要选择存储库和分支。如果所选环境存在配置管道，则会禁用此选择。

      ![配置管道概述](/help/security/assets/config-pipeline.png)

      >[!NOTE]
      >
      > 用户必须以部署管理员身份登录，才能配置或运行这些管道。
      > 此外，您只能为每个环境配置和运行一个配置管道。

   1. 将代码位置设置为存储根配置的位置（例如/config）。
   1. 选择&#x200B;**保存**。您的新管道将显示在管道信息卡中，并且会在您就绪后运行。
   1. 对于 RDE，将使用命令行，但目前不支持 RDE。

## 流量过滤规则语法 {#rules-syntax}

您可以配置 `traffic filter rules` 以匹配 IPS、用户代理、请求标头、主机名、地理位置和 URL 等模式。

许可 WAF 产品的客户还可以配置一种特殊类别的流量过滤器规则，这些规则称为 `WAF traffic filter rules`（简称 WAF 规则），它们引用下面的单独部分中列出的一个或多个 WAF 标志。

下面是一组流量过滤规则示例，其中还包括 WAF 规则。

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

cdn.yaml 文件中的流量过滤规则格式如下所述。请参阅后面部分中的一些示例。


| **属性** | **大多数流量过滤规则** | **WAF 流量过滤规则** | **类型** | **默认值** | **描述** |
|---|---|---|---|---|---|
| name | X | X | `string` | - | 规则名称（长度为 64 个字符，只能包含字母数字和 -） |
| when | X | X | `Condition` | - | 基本结构为：<br><br>`{ <getter>: <value>, <predicate>: <value> }`<br><br>请参阅下面的条件结构语法，其中描述了 getter、谓词以及如何组合多个条件。 |
| 动作 | X | X | `Action` | log | log、allow、block、log 或 action 对象，默认值为 log |
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
| reqCookie | `string` | 返回具有指定名称的 Cookie |

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
| **存在** | `boolean` | 设置为true且属性存在或设置为false且属性不存在时为true |

### 操作结构 {#action-structure}

由 `action` 字段指定，它可以是指定操作类型（allow、block、log）并为所有其他选项代入默认值的字符串，也可以是一个对象，在其中通过 `type` 必填字段以及适用于规则类型的其他选项来定义规则类型。

**操作类型**

根据下表中的操作类型设定操作的优先级，优先级将进行排序以反映操作的执行顺序：

| **名称** | **允许的属性** | **含义** |
|---|---|---|
| **allow** | `wafFlags`（可选） | 如果 wafFlags 不存在，则停止进一步的规则处理并继续提供响应。如果 wafFlags 存在，则禁用指定的 WAF 保护并继续执行进一步的规则处理。 |
| **block** | `status, wafFlags`（可选且互斥） | 如果 wafFlags 不存在，则绕过所有其他属性来返回 HTTP 错误，错误代码由状态属性定义或默认为 406。如果 wafFlags 存在，则启用指定的 WAF 保护并继续执行进一步的规则处理。 |
| **log** | `wafFlags`（可选） | 记录规则已触发这一事实，否则对处理不起作用。wafFlags 不起作用 |

### WAF 标志列表 {#waf-flags-list}

`wafFlags` 属性可能包含：

| **标志 ID** | **标志名称** | **描述** |
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

* 配置文件不应包含机密信息，因为任何有权访问 Git 存储库的人员都能读取这些文件。

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
        when:
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

**示例 5**

此规则阻止对 OFAC 国家/地区的访问：

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
            - reqProperty: tier
              matches: "author|publish"
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
| groupBy | array[Getter] | 无 | 速率限制器计数器将由一组请求属性（例如 clientIp）聚合。 |

### 示例 {#ratelimiting-examples}

**示例 1**

当客户端在过去 60 秒内超过 100 个请求/秒时，此规则将阻止客户端 5 分钟：

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
    - name: limit-requests-client-ip
      when:
        reqProperty: tier
        matches: "author|publish"
      rateLimit:
        limit: 60
        window: 10
        penalty: 300
        groupBy:
          - reqProperty: clientIp
      action: block
```

**示例 2**

当过去 60 秒内超过 100 个请求/秒时，阻止路径 /critical/resource 上的请求 60 秒：

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

“rules”属性描述了匹配的流量过滤规则，并具有以下模式：

```
"rules": "match=<matching-customer-named-rules-that-are-matched>,waf=<matching-WAF-rules>,action=<action_type>"
```

例如：

```
"rules": "match=Block-Traffic-under-private-folder,Enable-SQL-injection-everywhere,waf="SQLI,SANS",action=block"
```

这些规则的行为方式如下：

* 任何匹配规则的客户声明的规则名称都将在 matches 属性中列出。
* action 属性详细说明了规则是否起到了阻止、允许或记录作用。
* 如果已许可并启用 WAF，则 waf 属性将列出检测到的所有 waf 规则（例如 SQLI；请注意，这与客户声明的名称无关），无论配置中是否列出了 waf 规则。
* 如果没有客户声明的规则匹配并且没有 waf 规则匹配，则 rules 属性将为空。

一般来说，匹配的规则会显示在针对 CDN 的所有请求的日志条目中，无论它是 CDN 命中、通过还是未命中。但是，WAF 规则仅显示在被视为 CDN 未命中或通过而非 CDN 命中的 CDN 请求的日志条目中。

下面的示例显示了一个示例 cdn.yaml 和两个 CDN 日志条目：


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
| *rules* | 任何匹配的规则的名称。<br><br>还指示匹配是否产生块。<br><br>例如，“`match=Enable-SQL-Injection-and-XSS-waf-rules-globally,waf=SQLI,action=blocked`”<br><br>如果没有匹配的规则，则为空。 |

## 仪表板工具教程  {#dashboard-tooling}

Adobe提供一种机制，可以将功能板工具下载到计算机上，以摄取通过Cloud Manager下载的CDN日志。 借助此工具，您可以分析流量以帮助制定要声明的相应流量过滤器规则，包括WAF规则。 本节首先提供了熟悉开发环境中的仪表板工具的一些说明，然后提供了有关如何利用该知识在生产环境中创建规则的指南。

流量过滤器规则早期采用者客户应请求压缩功能板工具，其中包括一个描述如何加载Docker容器和摄取CDN日志的自述文件。


### 熟悉功能板工具 {#dashboard-getting-familiar}

1. 创建与开发环境关联的Cloud Manager非生产配置管道。 首先选择部署管道选项。 然后选择目标部署、配置、存储库、Git分支，并将代码位置设置为/config。

   ![添加非生产管道选择部署](/help/security/assets/waf-select-pipeline1.png)

   ![添加非生产管道选择目标](/help/security/assets/waf-select-pipeline2.png)


1. 在您的工作区中，在根级别创建一个文件夹配置并添加一个名为cdn.yaml的文件，您将在该文件中声明一个简单的规则，并将其设置为日志模式而不是阻止模式。

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
    # Log request on simple path
    - name: log-rule-example
      when:
        allOf:
          - reqProperty: tier
            matches: "author|publish"
          - reqProperty: path
            equals: '/log/me'
      action: log
```

1. 提交和推送更改，并使用配置管道部署配置。

   ![运行配置管道](/help/security/assets/waf-run-pipeline.png)

1. 部署配置后，请尝试使用Web浏览器或以下curl命令访问https://publish-pXXXXX-eYYYYYY.adobeaemcloud.com/log/me 。 系统应显示404错误页面，因为该页面不存在。

   ```
   curl -svo /dev/null https://publish-pXXXXX-eYYYYYY.adobeaemcloud.com/log/me
   ```

1. 从Cloud Manager下载CDN日志，并验证规则是否按预期匹配，以及规则属性是否与规则名称匹配：

   ```
   "rules": "match=log-rule-example"
   ```

   ![选择下载日志](/help/security/assets/waf-download-logs1.png)

   ![下载日志](/help/security/assets/waf-download-logs2.png)

1. 使用功能板工具加载Docker图像，然后按照自述文件摄取CDN日志。 如以下屏幕截图所示，选择正确的时间段、正确的环境和正确的过滤器。

   ![从仪表板选择时间](/help/security/assets/dashboard-select-time.png)

   ![从功能板选择环境](/help/security/assets/dashboard-select-env.png)

1. 应用正确的过滤器后，您应该能够看到加载了预期数据的功能板。 在下面的屏幕截图中，规则log-rule-example在过去2小时内由位于爱尔兰的同一IP使用Web浏览器和curl触发了3次。

   ![查看开发仪表板数据](/help/security/assets/dashboard-see-data-logmode.png)
   ![查看开发仪表板数据构件](/help/security/assets/dashboard-see-data-logmode2.png)

1. 现在，更改cdn.yaml以将规则置于阻止模式，以确保页面按预期被阻止。 然后像之前那样提交、推送并触发配置管道。

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
    # Log request on simple path
    - name: log-rule-example
      when:
        allOf:
          - reqProperty: tier
            matches: "author|publish"
          - reqProperty: path
            equals: '/log/me'
      action: block
```

1. 部署配置后，请尝试使用Web浏览器或以下curl命令访问https://publish-pXXXXX-eYYYYYY.adobeaemcloud.com/log/me 。 系统应显示406错误页面，指示请求被阻止。

   ```
   curl -svo /dev/null https://publish-pXXXXX-eYYYYYY.adobeaemcloud.com/log/me
   ```

1. 请再次在Cloud Manager中下载CDN日志（注意：新请求可能需要5分钟时间才能在CDN日志中公开），并将其导入功能板工具中，就像我们之前所做的那样。 完成后，刷新您的仪表板。 如以下屏幕快照所示，对/log/me的请求被我们的规则阻止。

   ![查看生产仪表板数据](/help/security/assets/dashboard-see-data-blockmode.png)
   ![查看生产仪表板数据](/help/security/assets/dashboard-see-data-blockmode2.png)

1. 如果已启用WAF流量过滤器（此功能为GA后，将需要额外的许可证），请在日志模式下重复使用WAF流量过滤器规则，然后部署这些规则。

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
      - name: log-waf-flags
        when:
          reqProperty: tier
          matches: "author|publish"
        action:
          type: log
          wafFlags:
              - SANS
              - SIGSCI-IP
              - TORNODE
              - NOUA
              - SCANNER
              - USERAGENT
              - PRIVATEFILE
              - ABNORMALPATH
              - TRAVERSAL
              - NULLBYTE
              - BACKDOOR
              - LOG4J-JNDI
              - SQLI
              - XSS
              - CODEINJECTION
              - CMDEXE
              - NO-CONTENT-TYPE
              - UTF8
```

1. 使用工具，如 [nikto](https://github.com/sullo/nikto/tree/master) 以生成匹配请求。 以下命令将在1分钟内发送约550个恶意请求。

   ```
   ./nikto.pl -useragent "MyAgent (Demo/1.0)" -D V -Tuning 9 -ssl -h https://publish-pXXXXX-eYYYYY.adobeaemcloud.com
   ```

1. 从Cloud Manager下载CDN日志（请记住，这些日志最多可能需要5分钟才能显示）并验证是否同时显示匹配的已声明规则和WAF标记。

   如您所见， WAF将Nikto生成的多个请求标记为恶意。 我们可以看到Nikto试图利用CMDEXE、SQLI和NULLBYTE漏洞。 如果您现在将操作从日志更改为阻止，并使用Nikto重新触发扫描，则之前标记的所有请求都将遭到阻止。

   ![查看WAF数据](/help/security/assets/dashboard-see-data-waf.png)


   请注意，每当请求与任何WAF标记匹配时，这些WAF标记都会出现，即使它们不是已声明的规则的一部分也是如此；因此，您始终能够识别潜在的新恶意流量，您尚未为它们声明匹配规则。 例如：

   ```
   "rules": "match=log-waf-flags,waf=SQLI,action=blocked"
   ```

1. 在日志模式下，重复使用使用使用速率限制的规则。 与以往一样，提交、推送并触发配置管道以应用您的配置。

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
      - name: limit-requests-client-ip
        when:
          reqProperty: tier
          matches: "author|publish"
        rateLimit:
          limit: 10
          window: 1
          penalty: 60
          groupBy:
            - reqProperty: clientIp
        action: log
```

1. 使用工具，如 [韦盖塔](https://github.com/tsenart/vegeta) 以生成流量。

   ```
   echo "GET https://publish-pXXXXX-eYYYYYY.adobeaemcloud.com" | vegeta attack -duration=5s | tee results.bin | vegeta report
   ```

1. 运行该工具后，您可以下载CDN日志并将其摄取到功能板中，以验证是否已触发速率限制器规则

   ![查看WAF数据](/help/security/assets/waf-dashboard-ratelimiter-1.png)

   ![查看WAF数据](/help/security/assets/waf-dashboard-ratelimiter-2.png)

   如您所见，我们的规则 *limit-requests-client-ip* 已触发。

   现在您已经熟悉了流量过滤器规则的工作方式，您可以移至生产环境。

### 将规则部署到生产环境 {#dashboard-prod-env}

请确保最初在日志模式下声明规则，以验证没有误报，这意味着将错误阻止的合法流量。

1. 创建与生产环境关联的生产配置管道。

1. 将以下推荐的规则复制到您的cdn.yaml中。 您可能希望根据网站实时流量的独特特征来修改规则。 提交、推送和触发您的配置管道。 确保规则处于日志模式。

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
    #  Block client for 5m when it exceeds 100 req/sec on a time window of 1sec
    - name: limit-requests-client-ip
      when:
        reqProperty: path
        like: '*'
      rateLimit:
        limit: 100
        window: 1
        penalty: 300
        groupBy:
          - reqProperty: clientIp
      action: log
    # Block requests coming from OFAC countries
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
      action: log
    # Enable recommended WAF protections (only works if WAF is enabled for your environment)
    - name: block-waf-flags-globally
      when:
        reqProperty: tier
        matches: "author|publish"
      action:
        type: log
        wafFlags:
          - SANS
          - SIGSCI-IP
          - TORNODE
          - NOUA
          - SCANNER
          - USERAGENT
          - PRIVATEFILE
          - ABNORMALPATH
          - TRAVERSAL
          - NULLBYTE
          - BACKDOOR
          - LOG4J-JNDI
          - SQLI
          - XSS
          - CODEINJECTION
          - CMDEXE
          - NO-CONTENT-TYPE
          - UTF8
    # Disable protection against CMDEXE on /bin
    - name: allow-cdmexe-on-root-bin
      when:
        allOf:
          - reqProperty: tier
            matches: "author|publish"
          - reqProperty: path
            matches: "^/bin/.*"
      action:
        type: log
        wafFlags:
          - CMDEXE
```

1. 添加任何其他规则以阻止您可能察觉到的恶意流量。 例如，某些IP一直在攻击您的站点。

1. 几分钟、几小时或几天后（具体取决于您网站的流量），从Cloud Manager下载CDN日志并使用仪表板分析这些日志。

1. 以下是一些注意事项：
   1. 流量匹配声明的规则会显示在图表和请求日志中，以便您轻松检查是否触发了声明的规则。
   1. 流量匹配的WAF标记会显示在图表和请求日志中，即使您未在规则中记录也是如此。 因此，您始终能够了解潜在的新恶意流量，并且可以根据需要创建新规则。 查看未反映在声明的规则中的WAF标记，并考虑声明它们。
   1. 对于匹配规则，检查请求日志中的误报，并查看是否可以从规则中过滤出误报。 例如，可能只对某些路径误报。

1. 将相应的规则设置为块模式，并考虑添加其他规则。 当您进一步分析并显示更多流量时，其中一些规则可能仍会保留在日志模式中。

1. 重新部署配置

1. 迭代，频繁地分析仪表板。

