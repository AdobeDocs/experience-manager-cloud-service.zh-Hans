---
title: 在 CDN 上配置流量
description: 了解如何通过在配置文件中声明规则和过滤器并使用Cloud Manager配置管道将它们部署到CDN来配置CDN流量。
feature: Dispatcher
exl-id: e0b3dc34-170a-47ec-8607-d3b351a8658e
role: Admin
source-git-commit: e5e0606c83f144f92f9ae57e5380a30389e8df1b
workflow-type: tm+mt
source-wordcount: '1351'
ht-degree: 1%

---


# 在 CDN 上配置流量 {#cdn-configuring-cloud}

AEM as a Cloud Service提供可在[Adobe管理的CDN](/help/implementing/dispatcher/cdn.md#aem-managed-cdn)层配置的功能集合，这些功能可修改传入请求或传出响应的性质。 可以声明以下规则（在本页中有详细描述）以实现以下行为：

* [请求转换](#request-transformations) — 修改传入请求的各个方面，包括标头、路径和参数。
* [响应转换](#response-transformations) — 修改返回客户端的标头（例如，Web浏览器）。
* [客户端重定向](#client-side-redirectors) — 触发浏览器重定向。
* [源选择器](#origin-selectors) — 代理到其他源后端。

在CDN上还可配置的还有流量过滤器规则(包括WAF)，这些规则控制CDN允许或拒绝的流量。 此功能已发布，您可以在[流量筛选器规则(包括WAF规则)](/help/security/traffic-filter-rules-including-waf.md)页面中了解更多相关信息。

此外，如果CDN无法联系其源，则可以编写引用自托管自定义错误页面（随后将渲染）的规则。 请阅读[配置CDN错误页面](/help/implementing/dispatcher/cdn-error-pages.md)文章，以了解有关此内容的更多信息。

所有这些在源代码管理的配置文件中声明的规则，均使用Cloud Manager [config管道进行部署。](/help/operations/config-pipeline.md)请注意，配置文件（包括流量过滤器规则）的累积大小不能超过100 KB。

## 评估顺序 {#order-of-evaluation}

在功能上，前面提到的各种功能将按照以下顺序进行评估：

![评估顺序](/help/implementing/dispatcher/assets/order.png)

## 设置 {#initial-setup}

在CDN上配置流量之前，您需要执行以下操作：

1. 创建名为`cdn.yaml`或类似的文件，并引用以下部分中的各种配置片段。

   所有代码片段都具有这些通用属性，在[配置管道](/help/operations/config-pipeline.md#common-syntax)中对其进行了说明。 `kind`属性值应为&#x200B;*CDN*，`version`属性应设置为&#x200B;*1*。

   ```
   kind: "CDN"
   version: "1"
   metadata:
     envTypes: ["dev"]
   ```

1. 将文件放置在名为&#x200B;*config*&#x200B;或类似的顶级文件夹下，如[配置管道](/help/operations/config-pipeline.md#folder-structure)中所述。

1. 在Cloud Manager中创建配置管道，如[配置管道](/help/operations/config-pipeline.md#managing-in-cloud-manager)中所述。

1. 部署配置。

## 规则语法 {#configuration-syntax}

以下部分中的规则类型具有相同的语法。

规则由名称、条件“when子句”和操作引用。

when子句根据属性（包括域、路径、查询字符串、标头和Cookie）确定是否评估规则。 各种规则类型的语法相同；有关详细信息，请参阅“流量过滤规则”文章中的[条件结构部分](/help/security/traffic-filter-rules-including-waf.md#condition-structure)。

“操作”节点的详细信息因规则类型而异，并在以下各个部分中进行了概述。

## 请求转换 {#request-transformations}

请求转换规则允许您修改传入请求。 这些规则支持根据各种匹配条件（包括正则表达式）设置、取消设置和更改路径、查询参数和标头（包括Cookie）。 您还可以设置变量，之后可在评估序列中引用这些变量。

用例多种多样，包括URL重写以简化应用程序或映射旧版URL。

如前所述，配置文件存在大小限制，因此具有更高要求的组织应在`apache/dispatcher`层定义规则。

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
      - name: set-header-with-reqproperty-rule
        when:
          reqProperty: path
          like: /set-header
        actions:
          - type: set
            reqHeader: x-some-header
            value: {reqProperty: path}
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
| **设置** | （reqProperty、reqHeader、queryParam或reqCookie），值 | 将指定的请求参数（仅支持“path”属性）或请求标头、查询参数或Cookie设置为给定值，该值可以是字符串文字或请求参数。 |
|     | 变量，值 | 将指定的请求属性设置为给定值。 |
| **取消设置** | reqProperty | 将指定的请求参数（仅支持“path”属性），或请求标头、查询参数或Cookie删除到给定值，该值可以是字符串文字或请求参数。 |
|         | 变量 | 删除指定的变量。 |
|         | queryParamMatch | 删除与指定正则表达式匹配的所有查询参数。 |
| **转换** | op：replace， （reqProperty或reqHeader、queryParam或reqCookie或var），匹配，替换 | 将部分请求参数（仅支持“path”属性）、请求标头、查询参数、Cookie或变量替换为新值。 |
|              | op：tolower， （reqProperty或reqHeader、queryParam或reqCookie或var） | 将请求参数（仅支持“path”属性）、请求标头、查询参数、Cookie或变量设置为其小写值。 |

替换操作支持捕获组，如下图所示：

```
      - name: extract-country-code-from-path
        when:
          reqProperty: path
          matches: ^/([a-zA-Z]{2})(/.*|$)
        actions:
          - type: set
            var: country-code
            value:
              reqProperty: path
          - type: transform
            var: country-code
            op: replace
            match: ^/([a-zA-Z]{2})(/.*|$)
            replacement: \1
      - name: replace-jpg-with-jpeg
        when:
          reqProperty: path
          like: /mypath
        actions:
          - type: transform
            reqProperty: path
            op: replace
            match: (.*)(\.jpg)$
            replacement: "\1\.jpeg"
```

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

您可以在请求转换期间设置变量，然后稍后在评估序列中引用它们。 有关更多详细信息，请参阅[评估顺序](#order-of-evaluation)图表。

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
| **取消设置** | 响应标头 | 从响应中删除指定的标头。 |

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
        when: { reqProperty: path, like: /proxy* }
        action:
          type: selectOrigin
          originName: example-com
          # skipCache: true
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
|     | skipCache （可选，默认为false） | 标记是否将缓存用于与此规则匹配的请求。 默认情况下，将根据响应缓存标头（例如，Cache-Control或Expires）缓存响应 |

**源**

与原端的连接仅使用SSL并使用端口443。

| 属性 | 含义 |
|------------------|--------------------------------------|
| **名称** | 可由“action.originName”引用的名称。 |
| **域** | 用于连接到自定义后端的域名。 它还用于SSL SNI和验证。 |
| **ip**（可选，支持的iv4和ipv6） | 如果提供，则将其用于连接到后端，而不是“域”。 仍使用“域”进行SSL SNI和验证。 |
| **forwardHost** （可选，默认为false） | 如果设置为true，则客户端请求中的“主机”标头将传递到后端，否则“域”值将传递到“主机”标头。 |
| **forwardCookie**（可选，默认为false） | 如果设置为true，则会将客户端请求中的“Cookie”标头传递到后端，否则将删除Cookie标头。 |
| **forwardAuthorization**（可选，默认为false） | 如果设置为true ，则客户端请求中的“Authorization”标头将传递到后端，否则删除Authorization标头。 |
| **timeout**（可选，以秒为单位，默认为60） | CDN应等待后端服务器传递HTTP响应主体的第一个字节的秒数。 此值还用作后端服务器的字节超时之间的值。 |

### 代理到Edge Delivery Services {#proxying-to-edge-delivery}

在某些情况下，可以使用源选择器将流量通过AEM Publish路由到AEMEdge Delivery Services：

* 某些内容由AEM Publish管理的域交付，而来自同一域的其他内容由Edge Delivery Services交付
* Edge Delivery Services交付的内容将受益于通过配置管道部署的规则，包括流量过滤器规则或请求/响应转换

以下是可以实现此目标的原点选择器规则的示例：

```
kind: CDN
version: '1'
data:
  originSelectors:
    rules:
      - name: select-edge-delivery-services-origin
        when:
          allOf:
            - reqProperty: tier
              equals: publish
            - reqProperty: domain
              equals: <Production Host>
            - reqProperty: path
              matches: "^(/scripts/.*|/styles/.*|/fonts/.*|/blocks/.*|/icons/.*|.*/media_.*|/favicon.ico)"
        action:
          type: selectOrigin
          originName: aem-live
    origins:
      - name: aem-live
        domain: main--repo--owner.aem.live
```

>[!NOTE]
> 由于使用了Adobe托管CDN，请确保按照Edge Delivery Services[安装程序推送失效文档](https://www.aem.live/docs/byo-dns#setup-push-invalidation)在&#x200B;**托管**&#x200B;模式下配置推送失效。


## 客户端重定向 {#client-side-redirectors}

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
  redirects:
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

重定向的位置可以是字符串文字(例如https://www.example.com/page)，也可以是可选地使用以下语法进行转换的属性（例如path）的结果：

```
experimental_redirects:
  rules:
    - name: country-code-redirect
      when: { reqProperty: path, like: "/" }
      action:
        type: redirect
        location:
          reqProperty: clientCountry
          transform:
            - op: replace
              match: '^(.*)$'
              replacement: 'https://www.example.com/\1/home'
            - op: tolower
    - name: www-redirect
      when: { reqProperty: domain, equals: "example.com" }
      action:
        type: redirect
        location:
          reqProperty: path
          transform:
            - op: replace
              match: '^/(.*)$'
              replacement: 'https://www.example.com/\1'
```
