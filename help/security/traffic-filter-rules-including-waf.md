---
title: 流量过滤规则（包括 WAF 规则）
description: 配置流量过滤规则（包括 Web 应用程序防火墙 (WAF) 规则）。
exl-id: 6a0248ad-1dee-4a3c-91e4-ddbabb28645c
feature: Security
role: Admin
source-git-commit: cf9e1b3c290d142095912c794de58547913faece
workflow-type: tm+mt
source-wordcount: '4012'
ht-degree: 97%

---


# 流量过滤规则（包括 WAF 规则） {#traffic-filter-rules-including-waf-rules}

流量过滤规则可用于在 CDN 层阻止或允许请求，这在以下场景中可能很有用：

* 在新网站上线之前，仅限公司内部流量访问特定的域
* 制定速率限制以降低受到大规模 DoS 攻击影响的程度
* 防止已知有恶意的 IP 地址将您的页面作为目标

所有 AEM as a Cloud Service Sites 和 Forms 客户均可使用大多数此类流量过滤器规则。这些规则主要作用于请求属性和请求标头，包括 IP、主机名、路径和用户代理。

流量过滤规则的子类别需要“增强安全性”许可证或“WAF-DDoS 保护”许可证。这些强有力的规则称为 WAF（Web 应用程序防火墙）流量过滤规则（或简称为 WAF 规则），它们可访问本文稍后所述的 [WAF 标志](#waf-flags-list)。

可通过 Cloud Manager 配置管道将流量过滤规则部署到生产（非沙盒）程序中的开发、暂存和生产环境类型。未来还将支持 RDE。

[按照教程进行操作，](#tutorial)快速建立有关此功能的具体专业知识。

>[!NOTE]
>有关在 CDN 上配置流量的其他选项，包括编辑请求/响应、声明重定向以及代理到非 AEM 来源，请参阅[在 CDN 上配置流量](/help/implementing/dispatcher/cdn-configuring-traffic.md)文章。


## 本文的结构 {#how-organized}

本文分为以下几个部分：

* **流量保护概述：**&#x200B;了解如何保护您抵御恶意流量。
* **配置规则的建议流程：**&#x200B;大致了解保护您的网站的方法。
* **设置：**&#x200B;了解如何设置、配置和部署流量过滤规则（包括高级 WAF 规则）。
* **规则语法：**&#x200B;了解如何在 `cdn.yaml` 配置文件中声明流量过滤规则。其中包括所有 Sites 和 Forms 客户均可使用的流量过滤规则以及 WAF 规则子类别（对于许可该功能的人）。
* **规则示例：**&#x200B;查看已声明的规则的示例以增进了解。
* **速率限制规则：**&#x200B;了解如何使用速率限制规则保护您的网站抵御大规模攻击。
* **流量过滤规则警报：**&#x200B;配置警报，以便在触发规则时收到通知。
* **默认源流量尖峰警报：**&#x200B;当源流量激增，表明可能发生了 DDoS 攻击时，您将收到通知。
* **CDN 日志：**&#x200B;查看哪些声明的规则和 WAF 标志与您的流量相匹配。
* **仪表板工具：**&#x200B;分析您的 CDN 日志以提出新的流量过滤规则。
* **推荐的入门规则：**&#x200B;一组入门规则。
* **教程：**&#x200B;有关该功能的实用知识，包括如何使用仪表板工具声明正确的规则。

Adobe 邀请您通过发送电子邮件至 **aemcs-waf-adopter@adobe.com** 提供反馈或询问有关流量过滤规则的问题。

## 流量保护概述 {#traffic-protection-overview}

在当前的数字环境中，恶意流量是一种始终存在的威胁。Adobe 意识到此类风险的危害性，因此提供若干方法以保护客户应用程序并在发生攻击时减轻其影响。

在边缘，AdobeManaged CDN吸收网络层（第3层和第4层）的DoS攻击，包括泛洪和反射/放大攻击。

Adobe 默认采取措施，以防因规模超预期的突发流量超出特定阈值而导致性能下降。如果 DoS 攻击影响站点可用性，则提醒 Adobe 的运营团队采取措施以减轻影响。

客户可采取主动措施以通过在内容投放流的各层配置规则而减轻应用层（第 7 层）受到的攻击。

例如，客户可在 Apache 层配置[ Dispatcher 模块](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration#configuring-access-to-content-filter)或 [ModSecurity](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-learn/foundation/security/modsecurity-crs-dos-attack-protection) 以限制访问某些内容。

正如本文所述，还可使用 Cloud Manager 的[配置管道将流量过滤器规则部署到 Adobe Managed CDN。](/help/operations/config-pipeline.md)除了基于 IP 地址、路径和标头等属性的流量过滤规则或基于设置速率限制的规则之外，客户还可许可过滤规则的一个强有力的子类别，称为 WAF 规则。

## 建议流程 {#suggested-process}

以下大致介绍推荐用于提出正确的流量过滤规则的整个流程：

1. 配置非生产和生产配置管道，如[设置](#setup)部分中所述。
1. 已许可 WAF 流量过滤规则子类别的客户应在 Cloud Manager 中启用这些规则。
1. 阅读并尝试本教程以切实地了解如何使用流量过滤规则，包括 WAF 规则（如果已许可这些规则）。本教程带领您完成将规则部署到开发环境、模拟恶意流量、下载 [CDN 日志](#cdn-logs)并在[仪表板工具](#dashboard-tooling)中分析这些日志的全过程。
1. 将推荐的入门规则复制到 `cdn.yaml`，并在日志模式下将配置部署到生产环境。
1. 收集一些流量后，使用[仪表板工具](#dashboard-tooling)分析结果以查看是否有任何匹配。留意误报并作出任何必要的调整，最终在阻止模式下启用这些入门规则。
1. 根据对 CDN 日志的分析结果添加自定义规则，首先在开发环境上用模拟流量测试这些规则，然后先后在日志模式和阻止模式下将其部署到暂存和生产环境。
1. 持续监控流量，根据威胁形势的发展而更改规则。

## 设置 {#setup}

1. 创建一个文件 `cdn.yaml`，其中包含一组流量过滤规则，包括 WAF 规则。

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

   请参阅 [使用配置管道](/help/operations/config-pipeline.md#common-syntax)，了解 `data` 节点上方属性的描述。`kind` 属性值应设置为 *CDN* ，版本应设置为 `1`。


1. 如果许可了 WAF 规则，则应在 Cloud Manager 中为新的和现有的程序场景启用它，如下所述。

   1. 要在新程序上配置 WAF，请在[添加生产程序](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)时，选中&#x200B;**安全性**&#x200B;选项卡上的 **WAF-DDOS 保护**&#x200B;复选框。

   1. 要在现有程序上配置 WAF，可在任何时候[编辑您的程序](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md)，并在&#x200B;**安全性**&#x200B;选项卡上取消选中或选中 **WAF-DDOS** 选项。

1. 按照 [配置管道文章中的说明，在 Cloud Manager 中创建配置管道。](/help/operations/config-pipeline.md#managing-in-cloud-manager) 管道将引用顶层 `config` 文件夹，`cdn.yaml` 文件放置在其下方的某处，参见 [使用配置管道](/help/operations/config-pipeline.md#folder-structure)。

## 流量过滤规则语法 {#rules-syntax}

您可以配置 *流量过滤规则* 以匹配 IPS、用户代理、请求标头、主机名、地理位置和 URL 等模式。

许可“增强安全性”或“WAF-DDoS 保护”安全产品的客户还可配置一种特殊类别的流量过滤器规则，称为 *WAF 流量过滤器规则*（或简称为 WAF 规则），它们引用一个或多个 [WAF 标志](#waf-flags-list)。

下面是一组流量过滤规则（其中还包括 WAF 规则）的示例。

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
      - name: "path-rule"
        when:
          allOf:
            - { reqProperty: path, equals: /block-me }
            - { reqProperty: tier, equals: publish }
        action:
          type: block
      - name: "Enable-SQL-Injection-and-XSS-waf-rules-globally"
        when: { reqProperty: path, like: "*" }
        action:
          type: block
          wafFlags: [ SQLI, XSS]
```

`cdn.yaml` 文件中的流量过滤规则的格式如下所述。请参阅后面章节中的一些[其他示例](#examples)，以及有关[速率限制规则](#rate-limit-rules)的单独章节。


| **属性** | **大多数流量过滤规则** | **WAF 流量过滤规则** | **类型** | **默认值** | **描述** |
|---|---|---|---|---|---|
| name | X | X | `string` | - | 规则名称（长度为 64 个字符，只能包含字母数字和 -） |
| when | X | X | `Condition` | - | 基本结构为：<br><br>`{ <getter>: <value>, <predicate>: <value> }`<br><br>[请在下方参阅条件结构语法](#condition-structure)，其中描述 getter、谓词以及如何组合多个条件。 |
| action | X | X | `Action` | log | log、allow、block 或 Action 对象。默认为 log。 |
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
| reqProperty | `string` | 请求属性。<br><br>以下各项之一：<br><ul><li>`path`：返回不带查询参数的 URL 的完整路径。</li><li>`queryString`：返回 URL 的查询部分</li><li>`method`：返回在请求中使用的 HTTP 方法。</li><li>`tier`：返回 `author`、`preview` 或 `publish` 之一。</li><li>`domain`：以小写形式返回域属性（如 `Host` 标头中所定义）</li><li>`clientIp`：返回客户端 IP。</li><li>`clientCountry`：返回标识客户端位于哪个国家/地区的二字母代码（[区域指标符号](https://zh.wikipedia.org/wiki/cn/Regional_indicator_symbol)）。</li></ul> |
| reqHeader | `string` | 返回具有指定名称的请求头 |
| queryParam | `string` | 返回具有指定名称的查询参数 |
| reqCookie | `string` | 返回具有指定名称的 Cookie |
| postParam | `string` | 从请求正文返回具有指定名称的 Post 参数。只有正文的内容类型为 `application/x-www-form-urlencoded` 才能发挥作用 |

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
| **exists** | `boolean` | 当设置为 true 且属性存在或当设置为 false 且属性不存在时为 true |

**注释**

* 请求属性 `clientIp` 只能与以下谓词一起使用：`equals`、`doesNotEqual`、`in`、`notIn`。当使用 `in` 和 `notIn` 谓词时，还可比较 `clientIp` 与 IP 范围。以下示例实现一个条件以评估客户端 IP 是否在 192.168.0.0/24 的 IP 范围内（即从 192.168.0.0 到 192.168.0.255）：

```
when:
  reqProperty: clientIp
  in: [ "192.168.0.0/24" ]
```

* Adobe 建议在使用正则表达式时采用 [regex101](https://regex101.com/) 和 [Fastly Fiddle](https://fiddle.fastly.dev/)。您还可以从 [fastly 文档 - Fastly VCL 中的正则表达式中了解更多有关 Fastly 如何处理正则表达式的信息](https://www.fastly.com/documentation/reference/vcl/regex/#best-practices-and-common-mistakes)。


### 操作结构 {#action-structure}

`action` 可以是指定操作（允许、阻止或日志）的字符串，也可以是由操作类型（允许、阻止或日志）和 wafFlags 和/或状态等选项组成的对象。

**操作类型**

根据下表中的操作类型设定操作的优先级，优先级将进行排序以反映操作的执行顺序：

| **名称** | **允许的属性** | **含义** |
|---|---|---|
| **allow** | `wafFlags`（可选），`alert`（可选） | 如果 wafFlags 不存在，则停止进一步的规则处理并继续提供响应。如果 wafFlags 存在，则禁用指定的 WAF 保护并继续执行进一步的规则处理。<br>如果指定了警报，则当规则在 5 分钟内触发 10 次时，将会发送“操作中心”通知。一旦针对特定规则触发警报，它将不会再次触发，直到第二天（UTC）。 |
| **block** | `status, wafFlags`（可选且互斥），`alert`（可选） | 如果 wafFlags 不存在，则绕过所有其他属性来返回 HTTP 错误，错误代码由状态属性定义或默认为 406。如果 wafFlags 存在，则启用指定的 WAF 保护并继续执行进一步的规则处理。<br>如果指定了警报，则当规则在 5 分钟内触发 10 次时，将会发送“操作中心”通知。一旦针对特定规则触发警报，它将不会再次触发，直到第二天（UTC）。 |
| **log** | `wafFlags`（可选），`alert`（可选） | 记录规则已触发这一事实，否则对处理不起作用。wafFlags 不起作用。<br>如果指定了警报，则当规则在 5 分钟内触发 10 次时，将会发送“操作中心”通知。一旦针对特定规则触发警报，它将不会再次触发，直到第二天（UTC）。 |

### WAF 标志列表 {#waf-flags-list}

`wafFlags` 属性可用在可许可的 WAF 流量过滤规则中，该属性可能会引用以下各项：

| **标志 ID** | **标志名称** | **描述** |
|---|---|---|
| SQLI | SQL 注入 | SQL 注入是指尝试通过执行任意数据库查询来获取应用程序的访问权限或特权信息。 |
| BACKDOOR | 后门 | 后门信号是指尝试确定系统上是否存在公共后门文件的请求。 |
| CMDEXE | 命令执行 | 命令执行是指尝试通过用户输入的任意系统命令来获得控制权限或损坏目标系统。 |
| CMDEXE-NO-BIN | 除 `/bin/` 上的命令执行 | 由于 AEM 架构，提供与 `CMDEXE` 相同级别的保护，同时禁用 `/bin` 上的误报。 |
| XSS | 跨站点脚本 | 跨站点脚本是指尝试通过恶意 JavaScript 代码来劫持用户帐户或 Web 浏览会话。 |
| TRAVERSAL | 目录遍历 | 目录遍历是指尝试在整个系统中导航特权文件夹以获取敏感信息。 |
| USERAGENT | 攻击工具 | 攻击工具是指使用自动化软件来找出安全漏洞或尝试利用已发现的漏洞。 |
| LOG4J-JNDI | Log4J JNDI | Log4J JNDI 攻击尝试利用 2.16.0 版之前的 Log4J 版本中存在的 [Log4Shell 漏洞](https://zh.wikipedia.org/wiki/cn/Log4Shell) |
| BHH | 错误跳头 | 错误跳头是指尝试通过格式错误的 Transfer-Encoding (TE) 或 Content-Length (CL) 头或格式良好的 TE 和 CL 头进行 HTTP 走私 |
| CODEINJECTION | 代码注入 | 代码注入是指尝试通过用户输入的任意应用程序代码命令来获得控制权限或损坏目标系统。 |
| ABNORMALPATH | 异常路径 | 异常路径表示原始路径与规范化路径不同（例如，`/foo/./bar` 标准化为 `/foo/bar`） |
| DOUBLEENCODING | 双重编码 | 双重编码检查双重编码 html 字符的规避技术 |
| NOTUTF8 | 无效编码 | 无效编码可能会促使服务器将请求中的恶意字符转换为响应，从而导致拒绝服务或 XSS |
| JSON-ERROR | JSON 编码错误 | 指定为在“Content-Type”请求头中包含 JSON，但包含 JSON 解析错误的 POST、PUT 或 PATCH 请求正文。这通常与编程错误或自动或恶意请求有关。 |
| MALFORMED-DATA | 请求正文中的格式错误的数据 | 根据“Content-Type”请求头，格式错误的 POST、PUT 或 PATCH 请求正文。例如，如果指定了“Content-Type: application/x-www-form-urlencoded”请求头并包含 POST 正文 json。这通常是编程错误、自动或恶意请求。需要代理 3.2 版或更高版本。 |
| SANS | 恶意 IP 流量 | 已报告从事恶意活动的 IP 地址的 [SANS Internet Storm Center](https://isc.sans.edu/) 列表。 |
| NO-CONTENT-TYPE | 缺少“Content-Type”请求头 | 不具有“Content-Type”请求头的 POST、PUT 或 PATCH 请求。在此示例中，默认情况下，应用程序服务器应假定“Content-Type: text/plain; charset=us-ascii”。许多自动和恶意请求可能缺少“内容类型”。 |
| NOUA | 无用户代理 | 表示请求不包含“User-Agent”标头或未设置标头值。 |
| TORNODE | Tor 流量 | Tor 是可以隐藏用户身份的软件。Tor 流量尖峰可能表明攻击者正在试图掩盖其位置。 |
| NULLBYTE | 空字节 | 空字节通常不会出现在请求中，并表明请求的格式错误且可能是恶意请求。 |
| PRIVATEFILE | 私有文件 | 私有文件是具有机密性的，例如 Apache `.htaccess` 文件或可能泄露敏感信息的配置文件 |
| SCANNER | 扫描程序 | 标识常用的扫描服务和工具 |
| RESPONSESPLIT | HTTP 响应拆分 | 标识何时将 CRLF 字符作为输入提交给应用程序以将标头注入 HTTP 响应 |
| XML-ERROR | XML 编码错误 | 指定为在“Content-Type”请求头中包含 XML，但包含 XML 解析错误的 POST、PUT 或 PATCH 请求正文。这通常与编程错误或自动或恶意请求有关。 |
| DATACENTER | 数据中心 | 标识请求来自已知托管服务提供商。此类流量通常与实际最终用户无关。 |


## 注意事项 {#considerations}

* 在创建两个发生冲突的规则时，允许的规则将始终优先于阻止规则。例如，如果您创建一个规则来阻止特定路径，并创建一个规则来允许一个特定的 IP 地址，则来自被阻止路径的 IP 地址的请求将被允许。

* 如果规则匹配但被阻止，CDN 会提供 `406` 返回代码。

* 配置文件不应包含机密信息，因为任何有权访问 Git 存储库的人员都能读取这些文件。

* 在 Cloud Manager 中定义的 IP 允许列表优先于流量过滤器规则。

* WAF 规则匹配只显示在 CDN 未命中和通过（而非命中）的 CDN 日志中。

## 规则示例 {#examples}

下面是一些规则示例。请参阅[速率限制](#rate-limit-rules)部分以找到速率限制规则的更多示例。

**示例 1**

此规则阻止来自 **IP 192.168.1.1** 的请求：

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

此规则会阻止包含查询参数 `foo` 的发布请求，但允许来自 IP 192.168.1.1 的每个请求：

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
      - name: "block-request-that-contains-query-parameter-foo"
        when:
          allOf:
            - { queryParam: url-param, equals: foo }
            - { reqProperty: tier, equals: publish }
        action:
          type: block
      - name: "allow-all-requests-from-ip"
        when: { reqProperty: clientIp, equals: 192.168.1.1 }
        action:
          type: allow
```

**示例 4**

此规则在发布时会阻止对路径 `/block-me` 的请求，并阻止每个匹配 `SQLI` 或 `XSS` 模式的请求。此示例包括 WAF 流量过滤规则，它引用 `SQLI` 和 `XSS`[WAF 标志](#waf-flags-list)，因此需要一个单独的许可证。

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
      - name: "path-rule"
        when:
          allOf:
            - { reqProperty: path, equals: /block-me }
            - { reqProperty: tier, equals: publish }
        action:
          type: block
      - name: "Enable-SQL-Injection-and-XSS-waf-rules-globally"
        when: { reqProperty: path, like: "*" }
        action:
          type: block
          wafFlags: [ SQLI, XSS]
```

**示例 5**

此规则阻止访问 OFAC 国家/地区：

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

## 速率限制规则

如果流量超过传入请求的特定速率，有时最好根据某个具体的条件阻止流量。为 `rateLimit` 属性设置一个值可限制符合规则条件的那些请求的速率。

速率限制规则不能引用 WAF 标志。所有 Sites 和 Forms 客户均可使用它们。

根据每个 CDN POP 计算得出速率限制。举例来说，假设蒙特利尔、迈阿密和都柏林的 POP 的流量速率分别为每秒 80、90 和 120 个请求。并且，速率限制规则设置为 100 的限制。在该情况下，仅对通往都柏林的流量进行速率限制。

速率限制根据到达边缘的流量、到达来源的流量或错误的数量进行评估。

### rateLimit 结构 {#ratelimit-structure}

| **属性** | **类型** | **默认** | **含义** |
|---|---|---|---|
| limit | 10 和 10000 之间的整数 | 必填 | 为其触发规则的请求速率（每个 CDN POP），以每秒请求数为单位。 |
| window | 整数枚举：1、10 或 60 | 10 | 计算请求速率的采样时段（以秒为单位）。计数器的准确性取决于时段的大小（时段越大越准确）。例如，1 秒时段的准确性预计为 50%，而 60 秒时段的准确性预计为 90%。 |
| penalty | 60 和 3600 之间的整数 | 300（5 分钟） | 匹配请求被阻止的时段（以秒为单位）（四舍五入到最接近的分钟） |
| 计数 | 全部，获取，错误 | 全部 | 根据边缘流量（全部）、来源流量（获取）或错误数量（错误）进行评估。 |
| groupBy | array[Getter] | 无 | 速率限制器计数器将由一组请求属性（例如 clientIp）聚合。 |

### 示例 {#ratelimiting-examples}

**示例 1**

当客户端在过去 10 秒内超过平均 60 请求/秒（每个 CDN POP）时，此规则会阻止该客户端 5 毫秒：

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
        count: all
        groupBy:
          - reqProperty: clientIp
      action: block
```

**示例 2**

当 10 秒时间窗口内每秒对来源的平均请求数量（每个 CDN POP）超过 100 个时，将会阻止路径 /重要/资源上的请求 60 秒：

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
      - name: rate-limit-example
        when:
          allOf:
            - { reqProperty: path, equals: /critical/resource }
            - { reqProperty: tier, equals: publish }
        action:
          type: block
        rateLimit: { limit: 100, window: 10, penalty: 60, count: fetches }
```

## CVE规则 {#cve-rules}

如果WAF获得许可，Adobe会自动应用阻止规则来抵御许多已知CVE（常见漏洞和暴露），并且新的CVE可能会在发现后不久添加。 客户不应也不需要自己配置CVE规则。

如果流量请求与CVE匹配，它将显示在相应的CDN日志条目中。

如果对某个CVE存在疑问，或者您的组织希望禁用某个特定CVE规则，请联系Adobe支持部门。

## 流量筛选规则警报 {#traffic-filter-rules-alerts}

可以配置一条规则，如果在 5 分钟内触发十次，则发送“操作中心”通知。当某些流量模式出现时，此类规则会向您发出警报，以便您采取必要的措施。一旦针对特定规则触发警报，它将不会再次触发，直到第二天（UTC）。

详细了解[操作中心](/help/operations/actions-center.md)，包括如何设置接收电子邮件所需的通知配置文件。

![行动中心通知](/help/security/assets/traffic-filter-rules-actions-center-alert.png)


警报属性可应用于所有操作类型（允许、阻止、日志）的操作节点。

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
      - name: "path-rule"
        when:
          allOf:
            - { reqProperty: path, equals: /block-me }
            - { reqProperty: tier, equals: publish }
        action:
          type: block
          alert: true
```

## 默认源流量尖峰警报 {#traffic-spike-at-origin-alert}

当有大量流量发送到源时，如果来自同一 IP 地址的请求达到高阈值，则会发送[操作中心](/help/operations/actions-center.md)电子邮件通知，这表明可能存在 DDoS 攻击。

如果达到此阈值，Adobe 将阻止来自该 IP 地址的流量，但建议采取额外措施保护您的源，包括配置速率限制流量过滤规则以在较低阈值下阻止流量激增。请参阅[使用流量规则阻止 DoS 和 DDoS 攻击教程](#tutorial-blocking-DDoS-with-rules)，获取逐步指导。

此警报默认启用，但可以通过将 *defaultTrafficAlerts* 属性设置为 false 来禁用。一旦触发警报，它将不会再次触发，直到第二天（UTC）。

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
   defaultTrafficAlerts: false
```

## CDN 日志 {#cdn-logs}

通过 AEM as a Cloud Service 可访问 CDN 日志，这些日志对于包括缓存命中率优化以及配置流量筛选规则在内的诸多用例都很有用。在选择创作和发布服务时，CDN 日志显示在 Cloud Manager 的&#x200B;**下载日志**&#x200B;对话框中。

CDN 日志可能会延迟最多五分钟。

`rules` 属性描述与什么流量过滤规则匹配，并具有以下模式：

```
"rules": "match=<matching-customer-named-rules-that-are-matched>,waf=<matching-WAF-rules>,action=<action_type>"
```

例如：

```
"rules": "match=Block-Traffic-under-private-folder,Enable-SQL-injection-everywhere,waf="SQLI,SANS",action=block"
```

这些规则的行为方式如下：

* 任何匹配规则的客户声明规则名称都列在 `match` 属性中。
* `action` 属性决定规则是否阻止、允许或记录。
* 如果 WAF 已获得许可并启用，则 `waf` 属性会列出检测到的任何 WAF 标志（例如，SQLI）。无论任何规则中是否列出了 WAF 标志，情况都是如此。这样做是为了深入展示可能要声明的新规则。
* 如果没有客户声明的规则匹配并且没有 waf 规则匹配，则 `rules` 属性为空。

如前所述，WAF 规则匹配只会显示在 CDN 未命中和通过（而非命中）的 CDN 日志中。

下面的示例展示一个示例 `cdn.yaml` 和两个 CDN 日志条目：


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
| *cli_country* | 客户国家/地区的两字母 [ISO 3166-1](https://zh.wikipedia.org/wiki/cn/ISO_3166-1) alpha-2 国家/地区代码。 |
| *rid* | 用于唯一标识请求的请求头的值。 |
| *req_ua* | 负责发出给定 HTTP 请求的用户代理。 |
| *host* | 请求所针对的颁发机构。 |
| *url* | 完整路径，包括查询参数。 |
| *method* | 客户端发送的 HTTP 方法，例如“GET”或“POST”。 |
| *res_ctype* | 用于指示资源的原始媒体类型的 Content-Type。 |
| *cache* | 缓存的状态。可能的值为 HIT、MISS 或 PASS |
| *status* | 整数值形式的 HTTP 状态代码。 |
| *res_age* | 响应已缓存（在所有节点中）的时间量（以秒为单位）。 |
| *pop* | CDN 缓存服务器的数据中心。 |
| *rules* | 任何匹配的规则的名称。<br><br>还指示匹配是否产生块。<br><br>例如，“`match=Enable-SQL-Injection-and-XSS-waf-rules-globally,waf=SQLI,action=blocked`”<br><br>如果没有匹配的规则，则为空。 |

## 仪表板工具 {#dashboard-tooling}

Adobe 提供一种机制，它将仪表板工具下载到您的计算机上以摄取通过 Cloud Manager 下载的 CDN 日志。使用此工具，您可分析您的流量以帮助提出要声明的相应流量过滤器规则，包括 WAF 规则。

可直接从 [AEMCS-CDN-Log-Analysis-Tooling](https://github.com/adobe/AEMCS-CDN-Log-Analysis-Tooling) GitHub 存储库克隆仪表板工具。

[教程](#tutorial)提供了有关如何使用仪表板工具的具体说明。

## 推荐的入门规则 {#recommended-starter-rules}

可将以下推荐的规则复制到您的 `cdn.yaml` 中以快速入门。首先进入日志模式，分析您的流量，感到满意时改为阻止模式。您可能要根据您网站的实时流量的独有特征修改规则。

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev", "stage", "prod"]
data:
  trafficFilters:
    rules:
    #  Block client for 5m when it exceeds an average of 100 req/sec to origin on a time window of 10sec
    - name: limit-origin-requests-client-ip
      when:
        reqProperty: tier
        equals: 'publish'
      rateLimit:
        limit: 100
        window: 10
        count: fetches
        penalty: 300
        groupBy:
          - reqProperty: clientIp
      action: log
    #  Block client for 5m when it exceeds an average of 500 req/sec on a time window of 10sec
    - name: limit-requests-client-ip
      when:
        reqProperty: tier
        equals: 'publish'
      rateLimit:
        limit: 500
        window: 10
        count: all
        penalty: 300
        groupBy:
          - reqProperty: clientIp
      action: log
    # Block requests coming from OFAC countries
    - name: block-ofac-countries
      when:
        allOf:
          - { reqProperty: tier, in: ["author", "publish"] }
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
        in: ["author", "publish"]
      action:
        type: log
        wafFlags:
          - TRAVERSAL
          - CMDEXE-NO-BIN
          - XSS
          - LOG4J-JNDI
          - BACKDOOR
          - USERAGENT
          - SQLI
          - SANS
          - TORNODE
          - NOUA
          - SCANNER
          - PRIVATEFILE
          - NULLBYTE
```

## 教程 {#tutorial}

提供以下两个教程。

### 使用流量过滤规则（包括 WAF 规则）保护网站 {#tutorial-protecting-websites}

[观看教程](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-learn/cloud-service/security/traffic-filter-and-waf-rules/overview)，获得有关流量过滤规则（包括 WAF 规则）的总体实用知识和经验。

本教程带领您完成以下操作：

* 设置 Cloud Manager 配置管道
* 使用工具模拟恶意流量
* 声明流量过滤规则，包括 WAF 规则
* 用仪表板工具分析结果
* 最佳实践

### 使用流量过滤规则阻止 DoS 和 DDoS 攻击 {#tutorial-blocking-DDoS-with-rules}

[深入研究如何使用速率限制流量过滤规则和其他策略来阻止](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-learn/cloud-service/security/blocking-dos-attack-using-traffic-filter-rules)拒绝服务 (DoS) 和分布式拒绝服务 (DDoS) 攻击。

本教程带领您完成以下操作：

* 理解保护
* 超出速率限制时接收警报
* 使用仪表板工具分析流量模式，为速率限制流量过滤规则配置阈值



