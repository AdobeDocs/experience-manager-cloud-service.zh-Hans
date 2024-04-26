---
title: 在 CDN 上配置流量
description: 了解如何通过在配置文件中声明规则和过滤器并使用Cloud Manager配置管道将它们部署到CDN来配置CDN流量。
feature: Dispatcher
exl-id: e0b3dc34-170a-47ec-8607-d3b351a8658e
source-git-commit: f9eeafbf128b4581c983e19bcd5ad2294a5e3a9a
workflow-type: tm+mt
source-wordcount: '1199'
ht-degree: 4%

---

# 在 CDN 上配置流量 {#cdn-configuring-cloud}

AEMas a Cloud Service提供了一系列功能，可在 [Adobe管理的CDN](/help/implementing/dispatcher/cdn.md#aem-managed-cdn) 修改传入请求或传出响应的性质的层。 可以声明以下规则（在本页中有详细描述）以实现以下行为：

* [请求转换](#request-transformations)  — 修改传入请求的各个方面，包括标头、路径和参数。
* [响应转换](#response-transformations)  — 修改返回客户端的标头（例如，Web浏览器）。
* [客户端重定向](#client-side-redirectors)  — 触发浏览器重定向。 此功能尚未正式发布，但可供早期采用者使用。
* [源选择器](#origin-selectors)  — 代理到其他源后端。

在CDN上还可以配置流量过滤器规则（包括WAF），它控制CDN允许或拒绝的流量。 此功能已发布，您可以在 [包含WAF规则的流量过滤器规则](/help/security/traffic-filter-rules-including-waf.md) 页面。

此外，如果CDN无法联系其源，则可以编写引用自托管自定义错误页面（随后将渲染）的规则。 要了解有关此内容的更多信息，请参阅 [配置CDN错误页面](/help/implementing/dispatcher/cdn-error-pages.md) 文章。

所有这些在源代码管理的配置文件中声明的规则，都通过使用进行部署 [Cloud Manager的配置管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#config-deployment-pipeline). 请注意，配置文件（包括流量过滤器规则）的累积大小不能超过100 KB。

## 评估顺序 {#order-of-evaluation}

在功能上，前面提到的各种功能将按照以下顺序进行评估：

![图像](/help/implementing/dispatcher/assets/order.png)

## 设置 {#initial-setup}

在CDN上配置流量之前，您需要执行以下操作：

* 在Git项目的顶级文件夹中创建此文件夹和文件结构：

```
config/
     cdn.yaml
```

* 此 `cdn.yaml` 配置文件应包含元数据和以下示例中描述的规则。 此 `kind` 参数应设置为 `CDN` 并且版本应设置为架构版本，当前为 `1`.

* 在Cloud Manager中创建目标部署配置管道。 请参阅 [配置生产管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) 和 [配置非生产管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md).

**注释**

* RDE当前不支持配置管道。
* 您可以使用 `yq` 在本地验证配置文件（例如 `yq cdn.yaml`）的 YAML 格式。

## 语法 {#configuration-syntax}

以下部分中的规则类型具有相同的语法。

规则由名称、条件“when子句”和操作引用。

when子句根据属性（包括域、路径、查询字符串、标头和Cookie）确定是否评估规则。 各种规则类型的语法相同；有关详细信息，请参阅 [“条件结构”部分](/help/security/traffic-filter-rules-including-waf.md#condition-structure) 在流量过滤器规则文章中。

“操作”节点的详细信息因规则类型而异，并在以下各个部分中进行了概述。

## 请求转换 {#request-transformations}

请求转换规则允许您修改传入请求。 这些规则支持根据各种匹配条件（包括正则表达式）设置、取消设置和更改路径、查询参数和标头（包括Cookie）。 您还可以设置变量，之后可在评估序列中引用这些变量。

用例多种多样，包括URL重写以简化应用程序或映射旧版URL。

如前所述，配置文件有大小限制，因此具有更高要求的组织应在 `apache/dispatcher` 图层。

配置示例：

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev", "stage", "prod"]
data:  
  requestTransformations:
    removeMarketingParams: true
    rules:
      - name: set-header-rule
        when:
          reqProperty: path
          like: /set-header
        actions:
          - type: set
            reqHeader: x-some-header
            value: some value
            
      - name: unset-header-rule
        when:
          reqProperty: path
          like: /unset-header
        actions:
          - type: unset
            reqHeader: x-some-header
            
      - name: unset-matching-query-params-rule
        when:
          reqProperty: path
          equals: /unset-matching-query-params
        actions:
          - type: unset
            queryParamMatch: ^removeMe_.*$
            
      - name: unset-all-query-params-except-exact-two-rule
        when:
          reqProperty: path
          equals: /unset-all-query-params-except-exact-two
        actions:
          - type: unset
            queryParamMatch: ^(?!leaveMe$|leaveMeToo$).*$
            
      - name: multi-action
        when:
          reqProperty: path
          like: /multi-action
        actions:
          - type: set
            reqHeader: x-header1
            value: body set by transformation rule
          - type: set
            reqHeader: x-header2
            value: '201'
            
      - name: replace-html
        when:
          reqProperty: path
          like: /mypath
        actions:
          - type: transform
           reqProperty: path
           op: replace
           match: \.html$
           replacement: ""
```

**操作**

下表说明了可用的操作。

| 名称 | 属性 | 含义 |
|-----------|--------------------------|-------------|
| **设置** | （reqProperty、reqHeader、queryParam或reqCookie），值 | 将指定的请求参数（仅支持“path”属性）或请求标头、查询参数或Cookie设置为给定值。 |
|     | 变量，值 | 将指定的请求属性设置为给定值。 |
| **未设置** | reqProperty | 将指定的请求参数（仅支持“path”属性），或请求标头、查询参数或Cookie删除到给定值。 |
|         | 变量 | 删除指定的变量。 |
|         | queryParamMatch | 删除与指定正则表达式匹配的所有查询参数。 |
| **转换** | op：replace， （reqProperty或reqHeader、queryParam或reqCookie），匹配，替换 | 将部分请求参数（仅支持“path”属性）、请求标头、查询参数或Cookie替换为新的值。 |
|              | op：tolower， （reqProperty、reqHeader、queryParam或reqCookie） | 将请求参数（仅支持“path”属性），或请求标头、查询参数或Cookie设置为其小写值。 |

操作可以链接在一起。 例如：

```
actions:
    - type: transform
      reqProperty: path
      op: replace
      match: \.html$
      replacement: ""
    - type: transform
      reqProperty: path
      op: tolower
```

### 变量 {#variables}

您可以在请求转换期间设置变量，然后稍后在评估序列中引用它们。 请参阅 [评估顺序](#order-of-evaluation) 图表以了解更多详细信息。

配置示例：

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["prod", "dev"]
data:   
  requestTransformations:
    rules:
      - name: set-variable-rule
        when:
          reqProperty: path
          equals: /set-variable
        actions:
          - type: set
            var: some_var_name
            value: some_value
 
  responseTransformations:
    rules:
      - name: set-response-header-while-variable
        when:
          var: some_var_name
          equals: some_value
        actions:
          - type: set
            respHeader: x-some-header
            value: some header value
```

## 响应转换 {#response-transformations}

响应转换规则允许您设置和取消设置CDN传出响应的标头。 另请参阅上述示例，以引用之前在请求转换规则中设置的变量。

配置示例：

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["prod", "dev"]
data:
  responseTransformations:
    rules:
      - name: set-response-header-rule
        when:
          reqProperty: path
          like: /set-response-header
        actions:
          - type: set
            value: value-set-by-resp-rule
            respHeader: x-resp-header
 
      - name: unset-response-header-rule
        when:
          reqProperty: path
          like: /unset-response-header
        actions:
          - type: unset
            respHeader: x-header1
 
      # Example: Multi-action on response header
      - name: multi-action-response-header-rule
        when:
          reqProperty: path
          like: /multi-action-response-header
        actions:
          - type: set
            respHeader: x-resp-header-1
            value: value-set-by-resp-rule-1
          - type: set
            respHeader: x-resp-header-2
            value: value-set-by-resp-rule-2
```

**操作**

下表说明了可用的操作。

| 名称 | 属性 | 含义 |
|-----------|--------------------------|-------------|
| **设置** | reqHeader，值 | 将指定的标头设置为响应中的给定值。 |
| **未设置** | 响应标头 | 从响应中删除指定的标头。 |

## 源选择器 {#origin-selectors}

您可以利用AEM CDN将流量路由到不同的后端，包括非Adobe应用程序（可能基于每路径或子域）。

配置示例：

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  originSelectors:
    rules:
      - name: example-com
        when: { reqProperty: path, like: /proxy-me* }
        action:
          type: selectOrigin
          originName: example-com
          # useCache: false
    origins:
      - name: example-com
        domain: www.example.com
        # ip: '1.1.1.1'
        # forwardHost: true
        # forwardCookie: true 
        # forwardAuthorization: true
        # timeout: 20
```

**操作**

下表说明了可用的操作。

| 名称 | 属性 | 含义 |
|-----------|--------------------------|-------------|
| **selectOrigin** | originName | 其中一个已定义源的名称。 |
|     | useCache （可选，默认值为true） | 标记是否将缓存用于与此规则匹配的请求。 |

**来源**

与原端的连接仅使用SSL并使用端口443。

| 属性 | 含义 |
|------------------|--------------------------------------|
| **name** | 可由“action.originName”引用的名称。 |
| **域** | 用于连接到自定义后端的域名。 它还用于SSL SNI和验证。 |
| **ip** （可选，支持iv4和ipv6） | 如果提供，则将其用于连接到后端，而不是“域”。 仍使用“域”进行SSL SNI和验证。 |
| **forwardHost** （可选，默认值为false） | 如果设置为true，则客户端请求中的“主机”标头将传递到后端，否则“域”值将传递到“主机”标头。 |
| **forwardCookie** （可选，默认值为false） | 如果设置为true，则会将客户端请求中的“Cookie”标头传递到后端，否则将删除Cookie标头。 |
| **forwardAuthorization** （可选，默认值为false） | 如果设置为true ，则客户端请求中的“Authorization”标头将传递到后端，否则删除Authorization标头。 |
| **timeout** （可选，以秒为单位，默认值为60） | CDN应等待后端服务器传递HTTP响应主体的第一个字节的秒数。 此值还用作后端服务器的字节超时之间的值。 |

## 客户端重定向 {#client-side-redirectors}

>[!NOTE]
>此功能尚未普遍可用。要加入率先采用者计划，请发送电子邮件至 `aemcs-cdn-config-adopter@adobe.com` 并描述您的用例。

对于301、302和类似的客户端重定向，您可以使用客户端重定向规则。 如果规则匹配，CDN会使用包含状态代码和消息（例如，HTTP/1.1 301 Moved Permanently）以及位置标头集的状态行进行响应。

允许使用具有固定值的绝对位置和相对位置。

请注意，配置文件（包括流量过滤器规则）的累积大小不能超过100 KB。

配置示例：

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  experimental_redirects:
    rules:
      - name: redirect-absolute
        when: { reqProperty: path, equals: "/page.html" }
        action:
          type: redirect
          status: 301
          location: https://example.com/page
      - name: redirect-relative
        when: { reqProperty: path, equals: "/anotherpage.html" }
        action:
          type: redirect
          location: /anotherpage
```

| 名称 | 属性 | 含义 |
|-----------|--------------------------|-------------|
| **重定向** | 位置 | “Location”标头的值。 |
|     | 状态（可选，默认为301） | 重定向消息中使用的HTTP状态，默认为301，允许值为：301、302、303、307、308。 |
