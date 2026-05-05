---
title: 常见场景的CDN配置片段
description: 适用于Adobe管理的CDN和客户管理的CDN设置的复制就绪YAML模式，包括边缘身份验证、重定向、缓存变化、流量整形和速率限制。
feature: Dispatcher
role: Admin
source-git-commit: ab43facbd4c34c92878e303acf2fef9cc127e28a
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 0%

---


# 常见场景的CDN配置片段 {#cdn-configuration-snippets}

本文为AEM as a Cloud Service收集实用的`cdn.yaml`模式。 将它们与[CDN流量规则](/help/implementing/dispatcher/cdn-configuring-traffic.md)、[客户管理的CDN凭据](/help/implementing/dispatcher/cdn-credentials-authentication.md)和[流量过滤器规则（包括WAF](/help/security/traffic-filter-rules-including-waf.md)）的功能文档一起使用。 使用Cloud Manager [配置管道](/help/operations/config-pipeline.md)部署代码片段。

>[!NOTE]
>
>将主机名、路径、IP范围、密钥和阈值替换为与项目匹配的值。 在提升更改之前，先在非生产环境中测试这些更改。

## 客户管理的CDN {#customer-managed-cdn}

### 仅为某些域设置Edge密钥身份验证 {#edge-auth-selected-hosts}

问题：在[客户管理的CDN](/help/implementing/dispatcher/cdn.md#point-to-point-cdn)上，您必须对某些客户主机名强制实施身份验证，而其他可发布的主机名应保持可用而不使用该标头（例如，在转出期间或当您的CDN后面只有一个品牌域时）。

解决方案：仅当来自`X-Forwarded-Host`的第一个主机名等于您的目标主机名时（例如`example.com`），才需要`X-AEM-Edge-Key`身份验证。 规则使用`forwardedDomain`请求属性执行该匹配并对边缘身份验证器运行`authenticate`操作。 替换程序的主机名、验证者名称和密钥占位符。

```yaml
kind: "CDN"
version: "1"
data:
  authentication:
    authenticators:
      - name: edge-key-auth
        type: edge
        edgeKey1: ${{CDN_EDGEKEY_1}}
        edgeKey2: ${{CDN_EDGEKEY_2}}
    rules:
      - name: edge-key-auth-rule
        when: { reqProperty: forwardedDomain, equals: "example.com" }
        action:
          type: authenticate
          authenticator: edge-key-auth
```

### 为不来自VPN IP的请求设置Edge密钥身份验证 {#edge-auth-trusted-ips}

问题：为BYOCDN设置Edge Key身份验证，但只允许直接访问VPN IP的发布域

解决方案：仅当客户端IP不在VPN IP列表中时，才需要X-AEM-Edge-Key身份验证

```yaml
kind: "CDN"
version: "1"
data:
  authentication:
    authenticators:
      - name: edge-key-auth
        type: edge
        edgeKey1: ${{CDN_EDGEKEY_1}}
        edgeKey2: ${{CDN_EDGEKEY_2}}
    rules:
      - name: edge-key-auth-rule
        when: { reqProperty: clientIp, notIn: ["10.0.0.1", "11.0.0.0/24", "<other VPN IPs>"] }
        action:
          type: authenticate
          authenticator: edge-key-auth
```

## 重定向 {#redirects}

### 正在从APEX域重定向到www {#apex-to-www}

```yaml
kind: "CDN"
version: "1"
data:
 redirects:
   rules:
     - name: non-www-to-www-redirect
       when:
         reqProperty: domain
         doesNotMatch: '^www\.'
       action:
         type: redirect
         status: 301
         location:
           join:
             format: 'https://www.%s%s'
             args:
               - reqProperty: domain
               - reqProperty: url
```

### 修改缓存键 {#cache-key}

CDN不会公开单独的“缓存密钥”字段。 由于URL参与缓存，因此您可以通过更改URL来拆分缓存条目，例如，通过[请求转换](/help/implementing/dispatcher/cdn-configuring-traffic.md#request-transformations)添加查询参数。

```yaml
kind: "CDN"
version: "1"
data:
  requestTransformations:
    rules:
      - name: set-request-different-cache-curl
        when:
          allOf:
            - reqProperty: tier
              equals: publish
            - reqHeader: user-agent
              matches: curl
        actions:
          - type: set
            queryParam: cache
            value: 'curl'
```

### 重定向到规范化路径 {#trailing-slash}

当浏览器在发布时请求尾随斜杠（例如从`https://www.example.com/path/`到`https://www.example.com/path`）时，发送永久重定向。

```yaml
kind: "CDN"
version: "1"
data:
  redirects:
    rules:
      - name: remove-trailing-slash
        when:
          allOf:
            - reqProperty: tier
              equals: publish
            - reqProperty: domain
              equals: www.example.com
            - reqProperty: originalPath
              matches: ^/(.+)/$
        action:
          type: redirect
          status: 301
          location:
            reqProperty: originalPath
            transform:
              - op: replace
                match: ^/(.+)/$
                replacement: https://www.example.com/\1
```

### 从JSON Cookie提取信息 {#json-cookie}

```yaml
kind: "CDN"
version: "1"
data:
  requestTransformations:
    rules:
      - name: options-response
        when: { reqProperty: tier, equals: publish }
        actions:
        - type: set
          reqHeader: x-mycookie-info
          value:
            reqCookie: mycookie
            transform: 
            - 'base64decode'
            - { op: 'replace', match: '"info":\s*"([^"]*)"', replacement: '\1'} 
```

## 跨域设置 {#cross-origin}

### 从CDN提供OPTIONS请求 {#options-from-cdn}

```yaml
kind: "CDN"
version: "1"
data:
  requestTransformations:
    rules:
      - name: options-response
        when:
          allOf: 
            - { reqProperty: path, like: /mypathi*  }
            - { reqProperty: method, equals: "OPTIONS" }
            - { reqHeader: Origin, equals: "https://example.com" }
        actions:
          - type: respond
            status: 200
            reason: "OK"
            headers:
              content-type: 'text/plain'
              access-control-allow-origin: { reqHeader: Origin }
              access-control-allow-methods: "*"
              access-control-allow-headers: "*"
```

## 流量过滤器 {#traffic-filters}

### 速率限制ASN {#rate-limit-asn}

问题：每个IP的速率限制可能会丢失分布式拒绝服务(DDoS)模式：每个地址都保持在阈值以下，因此合法和滥用的流量在IP层看起来很相似。

解决方案：按自治系统名称(`clientAsName`)对请求进行计数，以便限制器聚合共享相同网络名称的主机。 该代码片段将`clientAsName`写入每个请求的日志属性，然后对按该值分组的作者和发布应用速率限制。 许多用户可以共享一个ASN（例如大型ISP或公司VPN出口），因此请仔细调整限制并监控CDN日志的误报。

```yaml
kind: "CDN"
version: "1"
data:
  requestTransformations:
    rules:
      - name: log-on-request
        when: "*"
        actions:
          - type: set
            logProperty: client_as_name
            value:
              reqProperty: clientAsName
  trafficFilters:
    rules:
    - name: limit-requests-client-as-name
      when:
        reqProperty: tier
        matches: "author|publish"
      rateLimit:
        limit: 60
        window: 10
        penalty: 300
        count: all
        groupBy:
          - reqProperty: clientAsName
      action: block
```
