---
title: 流量过滤规则，包括 WAF 规则
description: 配置流量过滤规则，包括 Web 应用程序防火墙 (WAF) 规则
exl-id: 6a0248ad-1dee-4a3c-91e4-ddbabb28645c
source-git-commit: a129c188e9ec6871c86245acb5f0bf0333fdc340
workflow-type: tm+mt
source-wordcount: '3441'
ht-degree: 97%

---


# 流量过滤规则，包括 WAF 规则 {#traffic-filter-rules-including-waf-rules}

流量过滤规则可用于在 CDN 层阻止或允许请求，这在以下场景中可能很有用：

* 在新网站上线之前，将对特定域的访问限制为公司内部流量
* 建立速率限制，以减少受到批量 DoS 攻击的影响
* 防止已知的恶意 IP 地址以您的页面为目标

大多数此类流量过滤器规则可供所有 AEM as a Cloud Service 站点和表单客户使用。它们主要会对请求属性和请求标头进行操作，包括 IP、主机名、路径和用户代理。

流量过滤规则的子类别需要增强安全许可证或 WAF-DDoS 保护许可证，这些会于今年晚些时候推出。这些强大的规则被称为 WAF（Web 应用程序防火墙）流量过滤规则（或简称 WAF 规则），可以访问本文后面描述的 [WAF 标志。](#waf-flags-list)

流量过滤规则可以通过 Cloud Manager 配置管道部署到生产（非沙盒）程序中的开发、阶段和生产环境类型。对 RDE 的支持将在未来推出。

[完成教程](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/security/traffic-filter-and-waf-rules/overview.html) 以快速建立关于此功能的具体专业知识。

## 本文的结构 {#how-organized}

本文分为以下几节：

* **流量保护概述：**&#x200B;了解如何保护您免受恶意流量的侵害。
* **配置规则的建议流程：**&#x200B;了解保护您网站的高级方法。
* **设置：**&#x200B;了解如何设置、配置和部署流量过滤规则，包括高级 WAF 规则。
* **规则语法：**&#x200B;了解如何在 `cdn.yaml` 配置文件中声明流量过滤规则。这包括可供所有 Sites 和 Forms 客户使用的流量过滤规则，以及为获得该功能许可的人提供的 WAF 规则的子类别。
* **规则示例：**&#x200B;查看已声明规则的示例，增进了解。
* **速率限制规则：**&#x200B;了解如何使用速率限制规则来保护您的网站免受大量攻击。
* **CDN 日志：**&#x200B;查看哪些声明的规则和 WAF 标志与您的流量相匹配。
* **仪表板工具：**&#x200B;分析您的 CDN 日志以提出新的流量过滤规则。
* **推荐的入门规则：**&#x200B;一组入门规则。
* **教程：**&#x200B;有关该功能的实用知识，包括如何使用仪表板工具来声明正确的规则。

我们邀请您通过发送电子邮件至 **aemcs-waf-adopter@adobe.com** 提供反馈或询问有关流量过滤规则的问题。

## 流量保护概述 {#traffic-protection-overview}

在当前的数字环境中，恶意流量是一种始终存在的威胁。我们认识到该风险的严重性，并提供多种方法来保护客户应用程序并在发生攻击时减轻其影响。

在边缘，Adobe Managed CDN 吸收了网络层（第 3 层和第 4 层）的 DoS 攻击，其中包括洪水和反射/放大攻击。

默认情况下，Adobe 会采取措施防止由于突发的意外高流量超出特定阈值而导致性能下降。如果发生影响站点可用性的 DoS 攻击，Adobe 的运营团队会收到警报并采取措施进行缓解。

客户可以通过在内容交付流的各个层面配置规则来采取主动措施来减轻应用程序层受到的攻击（第 7 层）。

例如，在 Apache 层，客户可以配置[ Dispatcher 模块](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#configuring-access-to-content-filter)或者[ ModSecurity ](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/modsecurity-crs-dos-attack-protection.html?lang=en)限制对某些内容的访问。

正如本文所述，可以使用 Cloud Manager 的配置管道将流量过滤器规则部署到 Adobe Managed CDN。除了基于 IP 地址、路径和标头等属性的流量过滤规则或基于设置速率限制的规则之外，客户还可以许可称为 WAF 规则的强大流量过滤规则子类别。

## 建议流程 {#suggested-process}

以下是制定正确流量过滤规则时推荐使用的端到端高级流程：

1. 配置非生产和生产配置管道，如[设置](#setup)部分中所述。
1. 已获得 WAF 流量过滤规则子类别许可的客户应在 Cloud Manager 中启用它们。
1. 阅读并尝试本教程，具体了解如何使用流量过滤规则，其中包括 WAF 规则（如果已获得许可）。本教程会引导您完成将规则部署到开发环境、模拟恶意流量、下载 [CDN 日志](#cdn-logs)，并分析其[仪表板工具。](#dashboard-tooling)
1. 将推荐的启动规则复制到 `cdn.yaml`，并以日志模式将该配置部署到生产环境。
1. 收集一些流量后，使用[仪表板工具](#dashboard-tooling)分析结果，查看是否有任何匹配项。留意误报，并进行任何必要的调整，最终在阻止模式下启用启动规则。
1. 根据 CDN 日志分析添加自定义规则，首先在开发环境中使用模拟流量进行测试，然后以日志模式部署到阶段和生产环境，然后以阻止模式部署。
1. 持续监控流量，根据威胁形势的发展而更改规则。

## 设置 {#setup}

1. 首先，在 Git 中项目的顶层文件夹中创建以下文件夹和文件结构：

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

`kind` 参数应设置为 `CDN`，版本应设置为架构版本，当前为 `1`。请参阅下面的示例。


<!-- Two properties -- `envType` and `envId` -- may be included to limit the scope of the rules. The envType property may have values "dev", "stage", or "prod", while the envId property is the environment (e.g., "53245"). This approach is useful if it is desired to have a single configuration pipeline, even if some environments have different rules. However, a different approach could be to have multiple configuration pipelines, each pointing to different repositories or git branches. -->

1. 如果 WAF 规则已获得许可，您应在 Cloud Manager 中为新的和现有的程序场景启用该功能，如下所述。

   1. 要在新程序上配置 WAF，请在[添加生产程序](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)时，选中&#x200B;**安全**&#x200B;选项卡上的 **WAF-DDOS 保护**&#x200B;复选框。

   1. 要在现有程序上配置 WAF，[编辑程序](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md)并随时在&#x200B;**安全**&#x200B;选项卡上取消选中或选中 **WAF-DDOS** 选项。

1. 对于 RDE 以外的环境类型，请在 Cloud Manager 中创建目标部署配置管道。

   * [请参阅本文档了解生产管道。](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md)
   * [请参阅本文档了解非生产管道。](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)

对于 RDE，将使用命令行，但目前不支持 RDE。

**注释**

* 您可以使用 `yq` 在本地验证配置文件（例如 `yq cdn.yaml`）的 YAML 格式。

## 流量过滤规则语法 {#rules-syntax}

您可以配置 `traffic filter rules` 以匹配 IPS、用户代理、请求标头、主机名、地理位置和 URL 等模式。

许可增强安全或 WAF-DDoS 防护安全产品的客户还可以配置一种特殊类别的流量过滤器规则，这些规则称为 `WAF traffic filter rules`（简称 WAF 规则），它们会引用一个或多个[ WAF 标志。](#waf-flags-list)

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

`cdn.yaml` 文件中的流量过滤规则格式如下所述。请参阅后面章节中的一些[其他示例](#examples)，以及有关[速率限制规则](#rate-limit-rules)的单独章节。


| **属性** | **大多数流量过滤规则** | **WAF 流量过滤规则** | **类型** | **默认值** | **描述** |
|---|---|---|---|---|---|
| name | X | X | `string` | - | 规则名称（长度为 64 个字符，只能包含字母数字和 -） |
| when | X | X | `Condition` | - | 基本结构为：<br><br>`{ <getter>: <value>, <predicate>: <value> }`<br><br>[请参阅下面的条件结构语法，其中描述了 getter、谓词以及如何组合多个条件。](#condition-structure) |
| 动作 | X | X | `Action` | log | 记录、允许、阻止或操作对象。默认为日志。 |
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
| reqProperty | `string` | 请求属性。<br><br>其中之一：<br><ul><li>`path`：返回不带查询参数的 URL 的完整路径。</li><li>`queryString`：返回 URL 的查询部分</li><li>`method`：返回请求中使用的 HTTP 方法。</li><li>`tier`：返回 `author` , `preview` 或者 `publish` 其中之一。</li><li>`domain`：以小写形式返回域属性（如 `Host` 标头中定义的）</li><li>`clientIp`：返回客户端 IP。</li><li>`clientCountry`：返回可用于识别客户位于哪个国家的两个字母的代码 ([https://en.wikipedia.org/wiki/Regional_indicator_symbol](https://en.wikipedia.org/wiki/Regional_indicator_symbol))。</li></ul> |
| reqHeader | `string` | 返回具有指定名称的请求头 |
| queryParam | `string` | 返回具有指定名称的查询参数 |
| reqCookie | `string` | 返回具有指定名称的 Cookie |
| postParam | `string` | 从请求正文中返回具有指定名称的 Post 参数。仅当正文为内容类型为 `application/x-www-form-urlencoded` 时才有效  |

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
| **存在** | `boolean` | 当设置为 true 且属性存在或当设置为 false 且属性不存在时，为 true |

**注释**

* 请求属性 `clientIp` 只能与以下谓词一起使用：`equals`, `doesNotEqual`, `in`, `notIn`。当使用 `in` 和 `notIn` 谓词时，也可以将 `clientIp` 与 IP 范围进行比较。以下示例会实施一个条件来评估客户端 IP 是否在 192.168.0.0/24 的 IP 范围内（即从 192.168.0.0 到 192.168.0.255）：

```
when:
  reqProperty: clientIp
  in: [ "192.168.0.0/24" ]
```

* 我们建议在使用正则表达式时使用 [regex101](https://regex101.com/) 和 [Fastly Fiddle。](https://fiddle.fastly.dev/)您还可以通过此[文章](https://developer.fastly.com/reference/vcl/regex/#best-practices-and-common-mistakes)了解有关 Fastly 如何处理正则表达式的更多信息。


### 操作结构 {#action-structure}

An `action` 可以是指定操作（允许、阻止或日志）的字符串，也可以是由操作类型（允许、阻止或日志）和wafFlags和/或状态等选项组成的对象。

**操作类型**

根据下表中的操作类型设定操作的优先级，优先级将进行排序以反映操作的执行顺序：

| **名称** | **允许的属性** | **含义** |
|---|---|---|
| **allow** | `wafFlags`（可选） | 如果 wafFlags 不存在，则停止进一步的规则处理并继续提供响应。如果 wafFlags 存在，则禁用指定的 WAF 保护并继续执行进一步的规则处理。 |
| **block** | `status, wafFlags`（可选且互斥） | 如果 wafFlags 不存在，则绕过所有其他属性来返回 HTTP 错误，错误代码由状态属性定义或默认为 406。如果 wafFlags 存在，则启用指定的 WAF 保护并继续执行进一步的规则处理。 |
| **log** | `wafFlags`（可选） | 记录规则已触发这一事实，否则对处理不起作用。wafFlags 不起作用 |

### WAF 标志列表 {#waf-flags-list}

可在可获许可的 WAF 流量过滤规则中使用的 `wafFlags` 属性可能会引用以下内容：

| **标志 ID** | **标志名称** | **描述** |
|---|---|---|
| SQLI | SQL 注入 | SQL 注入是指尝试通过执行任意数据库查询来获取应用程序的访问权限或特权信息。 |
| BACKDOOR | 后门 | 后门信号是指尝试确定系统上是否存在公共后门文件的请求。 |
| CMDEXE | 命令执行 | 命令执行是指尝试通过用户输入的任意系统命令来获得控制权限或损坏目标系统。 |
| XSS | 跨站点脚本 | 跨站点脚本是指尝试通过恶意 JavaScript 代码来劫持用户帐户或 Web 浏览会话。 |
| TRAVERSAL | 目录遍历 | 目录遍历是指尝试在整个系统中导航特权文件夹以获取敏感信息。 |
| USERAGENT | 攻击工具 | 攻击工具是指使用自动化软件来找出安全漏洞或尝试利用已发现的漏洞。 |
| LOG4J-JNDI | Log4J JNDI | Log4J JNDI 攻击尝试利用 2.16.0 版之前的 Log4J 版本中存在的 [Log4Shell 漏洞](https://en.wikipedia.org/wiki/Log4Shell) |
| BHH | 错误跳头 | 错误跳头是指尝试通过格式错误的 Transfer-Encoding (TE) 或 Content-Length (CL) 头或格式良好的 TE 和 CL 头进行 HTTP 走私 |
| ABNORMALPATH | 异常路径 | 异常路径表示原始路径与规范化路径不同（例如，`/foo/./bar` 标准化为 `/foo/bar`） |
| DOUBLEENCODING | 双重编码 | 双重编码检查双重编码 html 字符的规避技术 |
| NOTUTF8 | 无效编码 | 无效编码可能会促使服务器将请求中的恶意字符转换为响应，从而导致拒绝服务或 XSS |
| JSON-ERROR | JSON 编码错误 | 指定为在“Content-Type”请求头中包含 JSON，但包含 JSON 解析错误的 POST、PUT 或 PATCH 请求正文。这通常与编程错误或自动或恶意请求有关。 |
| MALFORMED-DATA | 请求正文中的格式错误的数据 | 根据“Content-Type”请求头，格式错误的 POST、PUT 或 PATCH 请求正文。例如，如果指定了“Content-Type: application/x-www-form-urlencoded”请求头并包含 POST 正文 json。这通常是编程错误、自动或恶意请求。需要代理 3.2 版或更高版本。 |
| SANS | 恶意 IP 流量 | 已报告从事恶意活动的 IP 地址的 [SANS Internet Storm Center](https://isc.sans.edu/) 列表 |
| SIGSCI-IP | 网络效应 | 由 SignalSciences 标记的 IP：每当决策引擎因恶意信号而标记 IP 时，IP 将传播给所有客户。随后，记录来自这些 IP 地址的后续请求，其中包含标记持续时间的任何其他信号 |
| NO-CONTENT-TYPE | 缺少“Content-Type”请求头 | 不具有“Content-Type”请求头的 POST、PUT 或 PATCH 请求。在此示例中，默认情况下，应用程序服务器应假定“Content-Type: text/plain; charset=us-ascii”。许多自动和恶意请求可能缺少“内容类型”。 |
| NOUA | 无用户代理 | 许多自动和恶意请求使用虚假或缺失的用户代理，导致难以识别发出请求的设备类型。 |
| TORNODE | Tor 流量 | Tor 是可以隐藏用户身份的软件。Tor 流量尖峰可能表明攻击者正在试图掩盖其位置。 |
| NULLBYTE | 空字节 | 空字节通常不会出现在请求中，并表明请求的格式错误且可能是恶意请求。 |
| PRIVATEFILE | 私有文件 | 私有文件通常是机密性的，例如 Apache `.htaccess` 文件或可能泄露敏感信息的配置文件 |
| SCANNER | 扫描程序 | 标识常用的扫描服务和工具 |
| RESPONSESPLIT | HTTP 响应拆分 | 标识何时将 CRLF 字符作为输入提交给应用程序以将标头注入 HTTP 响应 |
| XML-ERROR | XML 编码错误 | 指定为在“Content-Type”请求头中包含 XML，但包含 XML 解析错误的 POST、PUT 或 PATCH 请求正文。这通常与编程错误或自动或恶意请求有关。 |

## 注意事项 {#considerations}

* 在创建两个发生冲突的规则时，allow 规则将始终优先于 block 规则。例如，如果您创建一个规则来阻止特定路径，并创建一个规则来允许一个特定的 IP 地址，则来自被阻止路径的 IP 地址的请求将被允许。

* 如果规则匹配但被阻止，CDN 会提供 `406` 返回代码。

* 配置文件不应包含机密信息，因为任何有权访问 Git 存储库的人员都能读取这些文件。

* Cloud Manager 中定义的 IP 允许列表优先于流量过滤器规则。

* WAF规则匹配项仅显示在CDN未命中和传递的CDN日志中，而不显示在点击中。

## 规则示例 {#examples}

下面是一些规则示例。请参阅[速率限制部分](#rules-with-rate-limits)以进一步了解速率限制规则示例。

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

此规则阻止对路径 `/block-me` 的请求，并阻止与 `SQLI` 或 `XSS` 模式匹配的每个请求：此示例包含 WAF 流量过滤规则，该规则引用了 `SQLI` 和 `XSS`[WAF 标志](#waf-flags-list)，因此需要单独的许可证。

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

## 速率限制规则 {#rate-limits-rules}

有时，如果流量超过传入请求的特定速率（可能基于特定条件），则需要阻止流量。设置一个 `rateLimit` 属性值可限制那些符合规则条件的请求的速率。

速率限制规则不能引用 WAF 标志。它们可供所有 Sites 和 Forms 客户使用。

速率限制是根据 CDN POP 计算的。例如，假设蒙特利尔、迈阿密和都柏林的 POP 的流量速率分别为每秒 80、90 和 120 个请求，并且速率限制规则设置为限制 100。在这种情况下，只有到都柏林的流量会受到速率限制。

### rateLimit 结构 {#ratelimit-structure}

| **属性** | **类型** | **默认** | **含义** |
|---|---|---|---|
| limit | 10 和 10000 之间的整数 | 必填 | 触发规则的请求速率（每个 CDN POP），以每秒请求数为单位。 |
| window | 整数枚举：1、10 或 60 | 10 | 计算请求速率的采样时段（以秒为单位）。计数器的精度取决于 window 的大小（window 越大，精度越高）。例如，1 秒 window 口的准确度预计为 50%，而 60 秒 window 的准确度预计为 90%。 |
| penalty | 60 和 3600 之间的整数 | 300（5 分钟） | 匹配请求被阻止的时段（以秒为单位）（四舍五入到最接近的分钟）。 |
| groupBy | array[Getter] | 无 | 速率限制器计数器将由一组请求属性（例如 clientIp）聚合。 |


### 示例 {#ratelimiting-examples}

**示例 1**

当客户端在过去 60 秒内超过 100 个请求/秒（每个 CDN POP）时，此规则将阻止客户端 5 分钟：

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

当过去 60 秒内超过 100 个请求/秒（每个 CDN POP）时，阻止路径 /critical/resource 上的请求 60 秒：

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

AEM as a Cloud Service 提供对 CDN 日志的访问权限，这对于包括缓存命中率优化以及配置流量过滤规则在内的用例非常有用。在选择创作和发布服务时，CDN 日志显示在 Cloud Manager 的&#x200B;**下载日志**&#x200B;对话框中。

请注意，CDN 日志可能会延迟最多 5 分钟。

`rules` 属性描述了匹配的流量过滤规则，并具有以下模式：

```
"rules": "match=<matching-customer-named-rules-that-are-matched>,waf=<matching-WAF-rules>,action=<action_type>"
```

例如：

```
"rules": "match=Block-Traffic-under-private-folder,Enable-SQL-injection-everywhere,waf="SQLI,SANS",action=block"
```

这些规则的行为方式如下：

* 任何匹配规则的客户声明的规则名称都将在 `match` 属性中列出。
* `action` 属性确定规则是否起到了阻止、允许或记录作用。
* 如果 WAF 已获得许可并启用，`waf` 属性将会列出检测到的所有 WAF 标志（例如 SQLI），无论 WAF 标志是否在任何规则中列出。这是为了深入了解需要宣布的潜在新规则。
* 如果没有客户声明的规则匹配并且没有 waf 规则匹配，则 `rules` 属性将为空。

如前所述，WAF规则匹配项仅显示在CDN缺失和传递的CDN日志中，而不显示在点击中。

下面的示例显示了一个示例 `cdn.yaml` 和两个 CDN 日志条目：


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

## 仪表板工具 {#dashboard-tooling}

Adobe 提供了一种将仪表板工具下载到您的计算机上的机制，以获取通过 Cloud Manager 下载的 CDN 日志。使用此工具，您可以分析流量，以帮助制定要声明的适当的流量过滤器规则，包括 WAF 规则。

仪表板工具可以直接从 [AEMCS-CDN-Log-Analysis-ELK-Tool](https://github.com/adobe/AEMCS-CDN-Log-Analysis-ELK-Tool) Github 存储库中复制。

[请参阅该教程](#tutorial)，了解有关如何使用仪表板工具的具体说明。

## 推荐的入门规则 {#recommended-starter-rules}

您可以将以下推荐规则复制到您的 `cdn.yaml`，以开始使用。从日志模式开始，分析您的流量，如果满意，则更改为阻止模式。建议您根据网站实时流量的独特特征修改规则。

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev", "stage", "prod"]
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
    # Enable recommended WAF protections (only works if WAF is licensed enabled for your environment)
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
    # Disable protection against CMDEXE on /bin (only works if WAF is licensed enabled for your environment)
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

## 教程 {#tutorial}

[查看教程](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/security/traffic-filter-and-waf-rules/overview.html)，获得有关流量过滤规则的实用知识和经验。

本教程将引导您完成：

* 设置 Cloud Manager 配置管道
* 使用工具模拟恶意流量
* 声明流量过滤规则，包括 WAF 规则
* 使用仪表板工具分析结果
* 最佳实践
