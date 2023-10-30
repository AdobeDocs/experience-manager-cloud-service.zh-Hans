---
title: 包含WAF规则的流量过滤器规则
description: 配置包括Web应用程序防火墙(WAF)规则的流量过滤规则
exl-id: 6a0248ad-1dee-4a3c-91e4-ddbabb28645c
source-git-commit: 8df8322eef7c74932d6feeeb4a7a6045935edd88
workflow-type: tm+mt
source-wordcount: '3473'
ht-degree: 45%

---


# 包含WAF规则的流量过滤器规则 {#traffic-filter-rules-including-waf-rules}

>[!NOTE]
>此功能现在可在开发环境中使用，并会在11月晚些时候逐步推出到暂存和生产环境。 您可以通过发送电子邮件来请求提前访问暂存和生产环境 **aemcs-waf-adopter@adobe.com**.

流量过滤器规则可用于在CDN层阻止或允许请求，这在以下情况下可能很有用：

* 在新网站正式启用之前，限制公司内部流量访问特定域
* 建立速率限制以减少受体积DoS攻击的影响
* 防止已知为恶意的IP地址定位您的页面

这些流量过滤器规则中的大多数适用于所有AEMas a Cloud ServiceSites和Forms客户。 它们主要对请求属性和请求标头进行操作，包括IP、主机名、路径和用户代理。

流量过滤器规则的子类别需要增强安全许可证或WAF-DDoS保护许可证，将在今年晚些时候提供。 这些功能强大的规则称为WAF （Web应用程序防火墙）流量过滤器规则（简称WAF规则），可访问 [WAF标志](#waf-flags-list) 本文后面部分将对此进行介绍。

流量过滤器规则可以通过Cloud Manager配置管道部署到生产（非沙盒）程序中的开发、暂存和生产环境类型。 未来将支持RDE。

[完成教程](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/security/traffic-filter-and-waf-rules/overview.html) 以快速建立关于此功能的具体专业知识。

## 本文的组织方式 {#how-organized}

本文分为以下部分：

* **流量保护概述：** 了解如何保护您免受恶意流量攻击。
* **配置规则的建议过程：** 阅读有关保护您网站的高级方法论。
* **设置：** 了解如何设置、配置和部署流量过滤器规则，包括高级WAF规则。
* **规则语法：** 在中阅读有关如何声明流量过滤器规则的信息 `cdn.yaml` 配置文件。 这包括适用于所有Sites和Forms客户的流量过滤器规则，以及许可此功能的WAF规则的子类别。
* **规则示例：** 请查看已声明规则的示例以帮助您顺利完成任务。
* **费率限制规则：** 了解如何使用速率限制规则保护您的网站免受高容量攻击。
* **CDN日志：** 查看哪些声明的规则和WAF标记与您的流量匹配。
* **功能板工具：** 分析您的CDN日志以提出新的流量过滤器规则。
* **推荐的入门规则：** 开始使用的一组规则。
* **教程：** 有关该功能的实用知识，包括如何使用仪表板工具声明正确的规则。

我们邀请您通过电子邮件发送反馈或询问有关流量过滤器规则的问题 **aemcs-waf-adopter@adobe.com**.

## 流量保护概述 {#traffic-protection-overview}

在当前数字环境中，恶意流量是一个始终存在的威胁。 我们认识到风险的严重性，并提供了几种方法来保护客户应用程序并在发生攻击时减少攻击。

在边缘，AdobeManaged CDN吸收网络层（第3层和第4层）的DoS攻击，包括泛洪和反射/放大攻击。

默认情况下，Adobe会采取措施防止由于突发的高流量超过特定阈值而导致性能下降。 如果发生影响站点可用性的DoS攻击，Adobe的操作团队将收到警报并采取措施缓解攻击。

客户可以通过在内容投放流的各个层配置规则来采取主动措施来缓解应用程序层攻击（第7层）。

例如，在Apache层，客户可以配置 [dispatcher模块](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#configuring-access-to-content-filter) 或 [修改安全性](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/modsecurity-crs-dos-attack-protection.html?lang=en) 以限制对特定内容的访问。

正如本文所述，可以使用Cloud Manager的配置管道将流量过滤器规则部署到Adobe托管的CDN。 除了基于IP地址、路径和标头等属性的流量过滤器规则或基于设置速率限制的规则之外，客户还可以许可一个称为WAF规则的强大流量过滤器子类别。

## 建议的流程 {#suggested-process}

以下是高级推荐的端到端流程，用于制定正确的流量过滤器规则：

1. 配置非生产和生产配置管道，如 [设置](#setup) 部分。
1. 已许可WAF流量过滤器规则的子类别的客户应在Cloud Manager中启用它们。
1. 阅读并尝试本教程，以具体了解如何使用流量过滤器规则，包括WAF规则（如果已授予许可）。 本教程将指导您完成以下操作：将规则部署到开发环境中、模拟恶意流量、下载 [CDN日志](#cdn-logs)，并在中分析它们 [仪表板工具](#dashboard-tooling).
1. 将推荐的入门规则复制到 `cdn.yaml` 并在日志模式下将配置部署到生产环境。
1. 收集了一些流量后，使用对结果进行分析 [仪表板工具](#dashboard-tooling) 看看有没有匹配。 查找误报并进行任何必要的调整，最终在块模式下启用启动程序规则。
1. 添加基于CDN日志分析的自定义规则，首先在开发环境中使用模拟流量进行测试，然后以日志模式部署到暂存和生产环境，最后再以块模式进行测试。
1. 持续监控流量，随着威胁形势的发展对规则进行更改。

## 设置 {#setup}

1. 首先，在Git中创建以下文件夹和文件结构（您的项目中的顶级文件夹）：

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

此 `kind` 参数应设置为 `CDN` 并且版本应设置为架构版本，当前为 `1`. 请参阅下面的示例。


<!-- Two properties -- `envType` and `envId` -- may be included to limit the scope of the rules. The envType property may have values "dev", "stage", or "prod", while the envId property is the environment (e.g., "53245"). This approach is useful if it is desired to have a single configuration pipeline, even if some environments have different rules. However, a different approach could be to have multiple configuration pipelines, each pointing to different repositories or git branches. -->

1. 如果WAF规则已获得许可，您应在Cloud Manager中启用该功能，如下面的新程序和现有程序方案所述。

   1. 要在新程序上配置WAF，请选中 **WAF-DDOS保护** 复选框 **安全性** 选项卡 [添加生产程序。](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)

   1. 要在现有程序上配置WAF， [编辑您的项目](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md) 在 **安全性** 制表符取消选中或选中 **WAF-DDOS** 选项。

1. 对于RDE以外的环境类型，请在Cloud Manager中创建目标部署配置管道。

   * [有关生产管道，请参阅此文档。](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md)
   * [请参阅本文档了解非生产管道。](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)

对于 RDE，将使用命令行，但目前不支持 RDE。

**注释**

* 您可以使用 `yq` 在本地验证配置文件的YAML格式(例如 `yq cdn.yaml`)。

## 流量过滤规则语法 {#rules-syntax}

您可以配置 `traffic filter rules` 以匹配 IPS、用户代理、请求标头、主机名、地理位置和 URL 等模式。

许可增强安全性或WAF-DDoS保护安全性产品的客户还可以配置一种名为的流量过滤器规则的特殊类别 `WAF traffic filter rules` （简称WAF规则）中引用了一个或多个 [WAF标志](#waf-flags-list).

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

中的流量过滤器规则的格式 `cdn.yaml` 文件如下所述。 查看一些 [其他示例](#examples) 在后面的部分中，以及关于 [费率限制规则](#rate-limit-rules).


| **属性** | **大多数流量过滤规则** | **WAF 流量过滤规则** | **类型** | **默认值** | **描述** |
|---|---|---|---|---|---|
| name | X | X | `string` | - | 规则名称（长度为 64 个字符，只能包含字母数字和 -） |
| when | X | X | `Condition` | - | 基本结构为：<br><br>`{ <getter>: <value>, <predicate>: <value> }`<br><br>[请参阅下面的条件结构语法，其中描述了 getter、谓词以及如何组合多个条件。](#condition-structure) |
| 动作 | X | X | `Action` | log | 日志、允许、阻止或操作对象。 默认为log |
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
| reqProperty | `string` | 请求属性。<br><br>其中之一：<br><ul><li>`path`：返回不含查询参数的URL的完整路径。</li><li>`queryString`：返回URL的查询部分</li><li>`method`：返回请求中使用的HTTP方法。</li><li>`tier`：返回一个 `author`， `preview` 或 `publish`.</li><li>`domain`：返回域属性(如 `Host` header)</li><li>`clientIp`：返回客户端IP。</li><li>`clientCountry`：返回两个字母的代码([https://en.wikipedia.org/wiki/Regional_indicator_symbol](https://en.wikipedia.org/wiki/Regional_indicator_symbol) 用于标识客户所在的国家/地区。</li></ul> |
| reqHeader | `string` | 返回具有指定名称的请求头 |
| queryParam | `string` | 返回具有指定名称的查询参数 |
| reqCookie | `string` | 返回具有指定名称的 Cookie |
| postParam | `string` | 从请求正文中返回具有指定名称的Post参数。 仅当正文为内容类型时才有效 `application/x-www-form-urlencoded` |

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

**注释**

* 请求属性 `clientIp` 只能与以下谓词一起使用： `equals`， `doesNotEqual`， `in`， `notIn`. `clientIp` 还可以在使用时与IP范围进行比较 `in` 和 `notIn` 谓词。 以下示例实施一个条件来评估客户端IP是否在192.168.0.0/24的IP范围内（从192.168.0.0到192.168.0.255）：

```
when:
  reqProperty: clientIp
  in: [ "192.168.0.0/24" ]
```

* 我们建议使用 [regex101](https://regex101.com/) 和 [飞天小提琴](https://fiddle.fastly.dev/) 使用正则表达式时。 您还可以在此了解有关Fastly如何处理正则表达式的更多信息 [文章](https://developer.fastly.com/reference/vcl/regex/#best-practices-and-common-mistakes).


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

此 `wafFlags` 属性（可在许可的WAF流量过滤器规则中使用）可以引用以下内容：

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

* Cloud Manager中定义的IP允许列表优先于流量过滤器规则。

* WAF规则匹配项仅显示在CDN未命中和传递的CDN日志中，而不显示在点击中。

## 规则示例 {#examples}

下面是一些规则示例。请参阅 [速率限制部分](#rules-with-rate-limits) 下面是费率限制规则的示例。

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

此规则阻止对路径的请求 `/block-me`，并阻止与 `SQLI` 或 `XSS` 模式。 此示例包含一个WAF流量过滤器规则，该规则引用 `SQLI` 和 `XSS` [WAF标志](#waf-flags-list)，因此需要单独的许可证。

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

## 费率限制规则 {#rate-limits-rules}

有时，如果流量超过传入请求的某个速率（可能基于特定条件），则需要阻止流量。 设置一个 `rateLimit` 属性值可限制那些符合规则条件的请求的速率。

费率限制规则不能引用WAF标志。 它们可供所有Sites和Forms客户使用。

速率限制是按CDN POP计算的。 例如，假设蒙特利尔、迈阿密和都柏林的POP每秒的流量率分别为80、90和120个请求，并且速率限制规则将设置为限制值100。 在这种情况下，只有前往都柏林的流量会受到限制。

### rateLimit 结构 {#ratelimit-structure}

| **属性** | **类型** | **默认** | **含义** |
|---|---|---|---|
| limit | 10 和 10000 之间的整数 | 必填 | 每秒触发规则的请求的请求率（每CDN POP）。 |
| window | 整数枚举：1、10 或 60 | 10 | 计算请求速率的采样时段（以秒为单位）。计数器的精度将取决于窗口的大小（窗口越大，精度越高）。 例如，1秒窗口可以达到50%的精度，60秒窗口可以达到90%的精度。 |
| penalty | 60 和 3600 之间的整数 | 300（5 分钟） | 匹配请求被阻止的时段（以秒为单位）（四舍五入到最接近的分钟）。 |
| groupBy | array[Getter] | 无 | 速率限制器计数器将由一组请求属性（例如 clientIp）聚合。 |


### 示例 {#ratelimiting-examples}

**示例 1**

此规则会在客户端在过去60秒内超过100请求/秒（每个CDN POP）时将其阻止5分钟：

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

当路径/critical/resource在过去60秒内超过100请求/秒（每个CDN POP）时，阻止对路径/critical/resource上的60s的请求：

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

AEMas a Cloud Service提供对CDN日志的访问，这些日志对于包括缓存命中率优化和配置流量过滤器规则在内的用例非常有用。 在选择创作和发布服务时，CDN 日志显示在 Cloud Manager 的&#x200B;**下载日志**&#x200B;对话框中。

请注意，CDN日志最多可能会延迟5分钟。

此 `rules` 属性描述匹配了哪些流量过滤器规则，其模式如下：

```
"rules": "match=<matching-customer-named-rules-that-are-matched>,waf=<matching-WAF-rules>,action=<action_type>"
```

例如：

```
"rules": "match=Block-Traffic-under-private-folder,Enable-SQL-injection-everywhere,waf="SQLI,SANS",action=block"
```

这些规则的行为方式如下：

* 任何匹配规则的客户声明的规则名称将列在 `match` 属性。
* 此 `action` 属性确定规则是否具有阻止、允许或记录的效果。
* 如果WAF已许可并启用，则 `waf` attribute将列出检测到的任何WAF标志（例如SQLI），而不管这些WAF标志是否列在任何规则中。 这是为了深入了解要声明的潜在新规则。
* 如果没有客户声明的规则匹配且没有waf规则匹配，则 `rules` 属性将为空。

如前所述，WAF规则匹配项仅显示在CDN缺失和传递的CDN日志中，而不显示在点击中。

以下示例显示了一个示例 `cdn.yaml` 和两个CDN日志条目：


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

## 功能板工具 {#dashboard-tooling}

Adobe提供一种机制，可以将功能板工具下载到计算机上，以摄取通过Cloud Manager下载的CDN日志。 借助此工具，您可以分析流量以帮助制定要声明的相应流量过滤器规则，包括WAF规则。

功能板工具可以直接从 [AEMCS-CDN-Log-Analysis-ELK-Tool](https://github.com/adobe/AEMCS-CDN-Log-Analysis-ELK-Tool) Github存储库。

[请参阅教程](#tutorial) 以获取有关如何使用仪表板工具的具体说明。

## 推荐的入门规则 {#recommended-starter-rules}

您可以将以下推荐的规则复制到 `cdn.yaml` 以开始使用。 在日志模式下启动，分析您的通信量，并在满意时更改为块模式。 您可能希望根据网站实时流量的独特特征来修改规则。

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

[完成教程](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/security/traffic-filter-and-waf-rules/overview.html) 获取有关流量过滤规则的实用知识和经验。

本教程将指导您完成：

* 设置Cloud Manager配置管道
* 使用工具模拟恶意流量
* 声明流量过滤器规则，包括WAF规则
* 使用仪表板工具分析结果
* 最佳实践
