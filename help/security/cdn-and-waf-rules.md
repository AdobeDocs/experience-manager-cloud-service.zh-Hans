---
title: 配置CDN和WAF规则以过滤流量
description: 使用CDN和Web应用程序防火墙规则过滤恶意通信
source-git-commit: 579f2842a72c7da1c9d24772bdae354a943de40c
workflow-type: tm+mt
source-wordcount: '2360'
ht-degree: 2%

---


# 配置CDN和WAF规则以过滤流量 {#configuring-cdn-and-waf-rules-to-filter-traffic}

>[!NOTE]
>
>此功能尚未普遍可用。要加入正在实施的早期采用者计划，请发送电子邮件至 **aemcs-waf-adopter@adobe.com**，包括贵组织的名称以及有关您对该功能感兴趣的上下文。

Adobe会尝试减少针对客户网站的攻击，但主动筛选匹配特定模式的请求可能会有用，这样恶意流量就不会到达您的应用程序。 可能的方法包括：

* Apache层模块，例如 `mod_security`
* 配置通过Cloud Manager的配置管道部署到CDN的规则。

本文介绍了后一种方法，它提供了两类规则：

1. **CDN规则**：根据请求属性和请求标头（包括IP、路径和用户代理）阻止或允许请求。 这些规则可以由所有AEMas a Cloud Service客户配置
1. **WAF** （Web应用程序防火墙）规则：阻止与已知与恶意通信相关的各种模式匹配的请求。 这些规则可由许可WAF加载项的客户配置；请联系您的Adobe客户团队以了解详细信息。 请注意，在早期采用者计划期间不需要额外的许可证。

这些规则可以部署到开发、暂存和生产云环境类型，用于生产（非沙盒）程序。 未来将支持RDE环境。

## 设置 {#setup}

1. 首先，在Git中创建以下文件夹和文件结构顶级文件夹：

   ```
   config/
        cdn/
           cdn.yaml
           _config.yaml
   ```

1. `_config.yaml` 描述有关配置的一些元数据。 “kind”参数应设置为“CDN”，版本应设置为架构版本，当前版本为“1”。 请参阅以下代码片段：

   ```
   kind: "CDN"
   version: "1"
   ```

   <!-- Two properties -- `envType` and `envId` -- may be included to limit the scope of the rules. The envType property may have values "dev", "stage", or "prod", while the envId property is the environment (e.g., "53245"). This approach is useful if it is desired to have a single configuration pipeline, even if some environments have different rules. However, a different approach could be to have multiple configuration pipelines, each pointing to different repositories or git branches. -->

1. `cdn.yaml` 应包括CDN规则和WAF规则的列表，如下节所述
1. 要匹配WAF规则，必须在Cloud Manager中启用WAF，如下面的针对新程序和现有程序方案所述。 请注意，必须为WAF购买单独的许可证。

   1. 要在新程序上配置WAF，请选中 **WAF-DDOS保护** 复选框 **安全性** 选项卡，如下所示。 按照中所述的步骤继续操作 [添加生产程序](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md) 以创建您的项目

   1. 要在现有程序上配置WAF，请选择 **编辑项目** 选项，具体步骤见 [编辑程序](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md) 文档。 然后，在 **安全性** 选项卡中，您可以随时取消选中或选中WAF-DDOS选项

1. 对于RDE以外的环境类型，执行Cloud Manager配置管道，可以按照以下所述进行配置。

   1. 从Cloud Manager主页中的管道信息卡中，选择 **添加生产管道** 或 **添加非生产管道** 启动添加管道向导
   1. 选择 **部署管道** 在“配置”选项卡中

      ![选择部署管道选项](/help/security/assets/deployment.png)

   1. 为管道命名，然后选择部署触发器，然后选择 **继续**
   1. 在 **源代码** 选项卡，选择 **目标部署**，然后选择 **配置**

      ![选择目标部署](/help/security/assets/target-deployment.png)

   1. 根据需要选择存储库和分支。 如果所选环境存在配置管道，则此选择被禁用。

      ![配置管道概述](/help/security/assets/config-pipeline.png)

      >[!NOTE]
      >
      >每个环境只能配置和运行一个配置管道。

   1. 选择&#x200B;**保存**。您的新管道将显示在管道信息卡中，并可在您准备就绪后运行。
   1. 对于RDE，将使用命令行，但当前不支持RDE。

## 规则语法 {#rules-syntax}

下面介绍了规则的格式，后面一节中提供了一些示例。

| **属性** | **CDN规则** | **WAF规则** | **类型** | **默认值** | **描述** |
|---|---|---|---|---|---|
| name | X | X | `string` | - | 规则名称（64个字符长，只能包含字母数字和 — ） |
| 时间 | X | X | `Condition` | - | 其基本结构为：<br><br>`{ <getter>: <value>, <predicate>: <value> }`<br><br>请参阅下面的条件结构语法，其中介绍了获取器、谓词以及如何组合多个条件。 |
| 动作 | X | X | `Enum` | 日志（CDN规则） | 对于CDN规则：允许、阻止、日志。 默认值为log。<br><br>对于WAF规则： `enableWafRules`， `disableWafRules`，日志。 无默认值。 |
| rateLimit | X |   | `RateLimit` | 未定义 | 速率限制配置。 如果未定义，将禁用速率限制。<br><br>下面有一个单独的部分进一步描述了rateLimit语法以及示例。 |
| wafRules |   | X | `array[Enum]` | - | 应启用或禁用的WAF规则列表。<br><br>示例包括SQLI和XSS。 有关完整列表，请参阅下面的waf规则列表。 |

### 条件结构 {#condition-structure}

条件可以是一个简单的条件，也可以是一组条件。

**简单条件**

简单条件由getter和谓词组成。

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

| **属性** | **类型** | **描述** |
|---|---|---|
| **allOf** | `array[Condition]` | **和** 操作。 如果列出的所有条件都返回true，则为true |
| **anyOf** | `array[Condition]` | **或** 操作。 如果列出的任一条件返回true，则为true |

**Getter**

| **属性** | **类型** | **描述** |
|---|---|---|
| reqProperty | `string` | 请求属性。<br><br>其中之一： `path` ， `queryString`， `method`， `tier`， `domain`， `clientIp`， `clientCountry`<br><br>domain属性是请求主机标头的小写转换。 此变量对于字符串比较很有用，因此匹配项不会因区分大小写而丢失。<br><br>此 `clientCountry` 使用以下位置显示的两个字母代码： [https://en.wikipedia.org/wiki/Regional_indicator_symbol](https://en.wikipedia.org/wiki/Regional_indicator_symbol) |
| reqHeader | `string` | 返回具有指定名称的请求标头 |
| queryParam | `string` | 返回具有指定名称的查询参数 |
| Cookie | `string` | 返回具有指定名称的Cookie |

**谓词**

| **属性** | **类型** | **描述** |
|---|---|---|
| **等于** | `string` | 如果getter结果等于提供的值，则为true |
| **doesNotEqual** | `string` | 如果getter结果不等于提供的值，则为true |
| **赞** | `string` | 如果getter结果与提供的模式匹配，则为true |
| **notLike** | `string` | 如果getter结果与提供的模式不匹配，则为true |
| **matches** | `string` | 如果getter结果与提供的regex匹配，则为true |
| **doesNotMatch** | `string` | 如果getter结果不匹配提供的regex，则为true |
| **中的** | `array[string]` | 如果提供的列表包含getter结果，则为true |
| **notIn** | `array[string]` | 如果提供的列表不包含getter结果，则为true |

**wafRules列表**

此 `wafRules` 资产可能包括以下规则：

| **规则编号** | **规则名称** | **描述** |
|---|---|---|
| SQLI | SQL注入 | SQL注入是指通过执行任意数据库查询来获取对应用程序的访问权限或获取特权信息的尝试。 |
| 后门 | 后门 | 后门信号是尝试确定系统上是否存在公共后门文件的请求。 |
| CMDEXE | 命令执行 | 命令执行是指通过用户输入任意系统命令，试图控制或破坏目标系统。 |
| XSS | 跨站点脚本 | 跨站点脚本是指试图通过恶意JavaScript代码劫持用户帐户或Web浏览会话。 |
| 遍历 | 目录遍历 | 目录遍历是指在整个系统中浏览特权文件夹以获取敏感信息的尝试。 |
| USERAGENT | 攻击工具 | 攻击工具使用自动化软件来识别安全漏洞或尝试利用发现的漏洞。 |
| LOG4J-JNDI | Log4J JNDI | Log4J JNDI攻击试图利用 [Log4Shell漏洞](https://en.wikipedia.org/wiki/Log4Shell) 在2.16.0之前的Log4J版本中存在 |
| AWS SSRF | AWS-SSRF | 服务器端请求伪造(SSRF)是一种试图将Web应用程序发出的请求发送到目标内部系统的请求。 AWS SSRF攻击使用SSRF获取Amazon Web Services (AWS)密钥，并获取对S3存储桶及其数据的访问权限。 |
| BHH | 错误的跃点标头 | 错误跃点标头表示通过格式错误的Transfer-Encoding (TE)或Content-Length (CL)标头或者格式正确的TE和CL标头进行HTTP走私尝试 |
| 异常路径 | 异常路径 | 异常路径表示原始路径与规范化路径不同(例如， `/foo/./bar` 已标准化为 `/foo/bar`) |
| 已压缩 | 检测到压缩 | POST请求正文已压缩，无法检查。 例如，如果指定了“Content-Encoding： gzip”POST标头，且请求正文不是纯文本。 |
| DOUBLE编码 | 双重编码 | 双重编码检查双重编码html字符的规避技术 |
| FORCEFULBROWSING | 强制浏览 | 强制浏览是访问管理页面的尝试失败 |
| NOTUTF8 | 编码无效 | 无效编码会导致服务器将请求中的恶意字符转换为响应，从而造成拒绝服务或XSS |
| JSON-ERROR | JSON编码错误 | POST、PUT或PATCH请求正文，指定为在“Content-Type”请求标头中包含JSON，但包含JSON解析错误。 这通常与编程错误、自动请求或恶意请求有关。 |
| 格式不正确的数据 | 请求正文中的数据格式不正确 | 根据“Content-Type”请求标头格式错误的POST、PUT或PATCH请求正文。 例如，如果指定了“Content-Type： application/x-www-form-urlencoded”POST标头并包含名为json的请求正文。 这通常是编程错误，自动请求或恶意请求。 需要代理3.2或更高版本。 |
| SANS | 恶意IP流量 | [SANS Internet Storm Center](https://isc.sans.edu/) 已报告参与恶意活动的IP地址列表 |
| SIGSCI-IP | 网络效果 | 由SignalSciences标记的IP：每当决策引擎通过恶意信号标记某个IP时，该IP就会传播给所有客户。 随后记录来自这些IP地址的后续请求，这些请求包含标志持续时间内任何附加信号 |
| NO-CONTENT-TYPE | 缺少“Content-Type”请求标头 | 无“Content-Type”POST标头的PUT、请求或PATCH请求。 在这种情况下，应用程序服务器默认应采用“Content-Type： text/plain； charset=us-ascii”。 许多自动化和恶意请求可能缺少“内容类型”。 |
| 努阿 | 无用户代理 | 许多自动化和恶意请求会使用虚假或缺失的用户代理，从而难以识别发出请求的设备类型。 |
| TORNODE | Tor流量 | Tor是隐藏用户身份的软件。 Tor流量尖峰可能表示攻击者试图掩盖其位置。 |
| 数据中心 | 数据中心流量 | 数据中心流量是指源自已识别托管提供商的非自然流量。 此类流量通常不与真实的最终用户相关联。 |
| NULLBYTE | 空字节 | Null字节通常不会出现在请求中，并指示该请求的格式不正确且可能是恶意的。 |
| 冒名顶替 | SearchBot冒名 | 搜索机器人冒名顶替者伪装成Google或Bing搜索机器人，但其身份不合法。 请注意，不依赖于响应本身，而是必须首先在云中解析，因此不应在预规则中使用它。 |
| PRIVATEFILE | 专用文件 | 私有文件通常具有保密性质，例如Apache `.htaccess` 文件，或可能泄露敏感信息的配置文件 |
| 扫描仪 | 扫描仪 | 识别流行的扫描服务和工具 |
| RESPONSESPLIT | http响应拆分 | 标识何时将CRLF字符作为输入内容提交到应用程序，以将标头插入HTTP响应 |
| XML错误 | XML编码错误 | POST、PUT或PATCH请求正文，指定为包含“Content-Type”请求标头中的XML，但包含XML解析错误。 这通常与编程错误、自动请求或恶意请求有关。 |

## 注意事项 {#considerations}

* 如果创建了两个冲突规则，则允许规则将始终优先于块规则。 例如，如果您创建规则来阻止特定路径，创建规则来允许一个特定IP地址，则将允许来自被阻止路径上的该IP地址的请求。

* 如果规则已匹配并阻止，则CDN将做出响应 `406` 返回代码。

## 示例 {#examples}

下面是一些规则示例。 请参阅 [速率限制部分](#rules-with-rate-limits) 下面是速率限制示例。

**示例1**

此规则阻止来自IP 192.168.1.1的请求：

```
data:
  rules:
    - name: "block-request-from-ip"
      when: { reqProperty: clientIp, equals: "192.168.1.1" }
      action: block
```

**示例2**

此规则阻止路径上的请求 `/helloworld` 在使用包含Chrome的User-Agent发布时：

```
data:
  rules:
    - name: "block-request-from-chrome-on-path-helloworld-for-publish-tier"
      when:
        allOf:
          - { reqProperty: path, equals: /helloworld }
          - { reqProperty: tier, equals: publish }
          - { reqHeader: user-agent, matches: '.*Chrome.*'  }
      action: block
```

**示例3**

此规则阻止包含查询参数的请求 `foo`，但允许来自IP 192.168.1.1的每个请求：

```
data:
  rules:
    - name: "block-request-that-contains-query-parameter-foo"
      when: { queryParam: url-param, equals: foo }
      action: block
    - name: "allow-all-requests-from-ip"
      when: { reqProperty: clientIp, equals: 192.168.1.1 }
      action: allow
```

**示例4**

此规则阻止对/block-me路径的请求，并阻止每个匹配SQLI或XSS模式的请求：

```
data:
  rules:
    - name: "path-rule"
      when: { reqProperty: path, equals: /block-me }
      action: block

    - name: "Enable-SQL-Injection-and-XSS-waf-rules-globally"
      when: { reqProperty: path, like: "*" }
      action: enableWafRules
      wafRules:
        - SQLI
        - XSS
```

## 具有速率限制的规则 {#rules-with-rate-limits}

有时，仅当匹配项在一段时间内超过特定速率时，才需要阻止匹配规则的流量。 设置值 `rateLimit` 属性限制与规则条件匹配的请求的速率。

### rateLimit结构 {#ratelimit-structure}

| **属性** | **类型** | **默认值** | **描述** |
|---|---|---|---|
| 限制 | 10到10000之间的整数 | 必需 | 触发规则的请求速率（以每秒请求数为单位） |
| 窗口 | 整数枚举：1、10或60 | 10 | 计算请求速率的采样窗口（以秒为单位） |
| 惩罚 | 从60到3600的整数 | 300（5分钟） | 阻止匹配请求的时段（以秒为单位）（四舍五入到最接近的分钟） |

### 示例 {#ratelimiting-examples}

示例1：当请求速率在最近60秒内超过每秒100个请求时，阻止 `/critical/resource` 持续60秒

```
- name: rate-limit-example
  when: { reqProperty: /critical/resource }
  action: block
  rateLimit: { limit: 100, window: 60, penalty: 60 }
```

示例2：当请求速率在10秒内超过每秒10个请求时，将资源阻止300秒：

```
- name: rate-limit-using-defaults
  when: { reqProperty: /critical/resource }
  action: block
  rateLimit:
    limit: 10
```

## CDN日志 {#cdn-logs}

AEMas a Cloud Service提供对CDN日志的访问，这些日志对于用例非常有用，包括缓存命中率优化以及配置CDN和WAF规则。 cdn日志显示在Cloud Manager中 **下载日志** 对话框，在选择作者或发布服务时。

如果请求与规则匹配，则规则的名称会显示在rules属性中，即使操作为“allow”也是如此，因此不会阻止流量。

无论是否为CDN点击、通过或未命中，对CDN的所有请求都会在日志条目中显示匹配的CDN规则。 但是，WAF规则仅显示在对CDN的请求中，这些请求被视为CDN未命中或传递，而不是CDN点击。

以下示例显示了一个示例 `cdn.yaml` 以及两个CDN日志条目，由于分别匹配CDN规则和WAF规则的阻止请求，这些日志条目在rules属性中具有非空值。


```
data:
  rules:
    - name: "path-rule"
      when: { reqProperty: path, equals: /block-me }
      action: block

    - name: "Enable-SQL-Injection-and-XSS-waf-rules-globally"
      when: { reqProperty: path, like: "*" }
      action: enableWafRules
      wafRules:
        - SQLI
        - XSS
```

```
{
"timestamp": "2023-05-26T09:20:01+0000",
"ttfb": 19,
"cip": "147.160.230.112",
"rid": "974e67f6",
"host": "example.com",
"url": "/block-me",
"req_mthd": "GET",
"res_type": "",
"cache": "PASS",
"res_status": 406,
"res_bsize": 3362,
"server": "PAR",
"rules": "cdn=path-rule;waf=;action=blocked"
}
```

```
{
"timestamp": "2023-05-26T09:20:01+0000",
"ttfb": 19,
"cip": "147.160.230.112",
"rid": "974e67f6",
"host": "example.com",
"url": "/?sqli=%27%29%20UNION%20ALL%20SELECT%20NULL%2CNULL%2CNULL%2CNULL%2CNULL%2CNULL%2CNULL%2CNULL%2CNULL%2CNULL--%20fAPK",
"req_mthd": "GET",
"res_type": "",
"cache": "PASS",
"res_status": 406,
"res_bsize": 3362,
"server": "PAR",
"rules": "cdn=;waf=SQLI;action=blocked"
}
```

### 日志格式 {#cdn-log-format}

以下是CDN日志中使用的字段名称列表，以及简短描述。

| **字段名** | **描述** |
|---|---|
| *时间戳* | TLS终止后请求开始的时间 |
| *ttfb* | 缩写 *到第一个字节的时间*. 从请求开始到响应正文开始进行流式处理之前的时间间隔。 |
| *cip* | 客户端IP地址。 |
| *rid* | 用于唯一标识请求的请求标头的值。 |
| *主机* | 请求所针对的权限。 |
| *url* | 完整路径，包括查询参数。 |
| *req_mthd* | 客户端发送的HTTP方法，如“GET”或“POST”。 |
| *res_type* | 用于指示资源的原始媒体类型的内容类型 |
| *cache* | 缓存的状态。 可能的值包括“点击”、“未命中”或“通过” |
| *res_status* | 整数值形式的HTTP状态代码。 |
| *res_bsize* | 在响应中发送到客户端的正文字节。 |
| *服务器* | cdn缓存服务器的数据中心。 |
| *规则* | CDN规则和waf规则的任何匹配规则的名称。<br><br>无论是否为CDN点击、通过或未命中，对CDN的所有请求都会在日志条目中显示匹配的CDN规则。<br><br>还指示匹配是否导致块。 <br><br>例如，“`cdn=;waf=SQLI;action=blocked`”<br><br>如果没有匹配的规则，则为空。 |
