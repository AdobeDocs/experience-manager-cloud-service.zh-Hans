---
title: 边缘侧包括
description: Adobe托管的CDN现在支持Edge Side Include (ESI)，这是一种用于边缘级动态Web内容汇编的标记语言。
feature: Dispatcher
source-git-commit: 8f9173e45dd802ecced21531dfa161890e4a8af1
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 2%

---

# 边缘侧包括 {#edge-side-includes}

>[!NOTE]
>此功能尚未普遍可用。要加入率先采用者计划，请发送电子邮件至 `aemcs-cdn-config-adopter@adobe.com` 并描述您的用例。

内容交付速度得益于积极缓存页面，通过设置具有高生存时间(TTL)值的缓存标头来实现。 当页面包含动态内容时，这可能具有挑战性，动态内容需要经常刷新或可能根本无法缓存。 幸运的是，有些策略可以使用高的TTL来缓存包含的HTML页面，从而将获取更多动态内容片段的过程推迟到以后（通过客户端Javascript或CDN）。 后一种方法是名为Edge Side Include (ESI)的标准，使用AEM发布呈现的网站支持此标准。 该HTML包括ESI标记，指示CDN将页面的服务延迟到浏览器评估这些标记之前，从源检索额外的更动态（更低的TTL）内容（如果其TTL未过期，则为CDN缓存）。

Edge Side Include的一些用例可能很有用：

* 显示最终用户的名称或最终用户特有的其他信息。
* 显示最近信息的列表，如新闻文章或股价。

## ESI语法 {#esi-syntax}

如果父页面，则ESI语法如下所示 `/content/page.html` 包含一个代码片段 `content/snippets/mysnippet.html`.

```
<html>
  <head>
      <title>My Site</title>
  </head>
  <body>
    <div id="content">
      <esi:include src="/content/snippets/mysnippet.html" />
    </div>
  </body>
</html>
```

请参阅 [ESI规范](https://www.w3.org/TR/esi-lang/) 以了解详细信息。

### 注意事项 {#esi-syntax-considerations}

* 支持以下ESI标记： include、comment、remove。
* ESI标记在CDN中按顺序处理而不是同时处理，因此，具有低TTL的页面上的许多ESI标记可能会增加最终用户体验的延迟。
* ESI：包含处理的最大深度为5。
* 最大ESI：包括处理片段数为256。


## Apache配置 {#esi-apache}

如果您的页面具有ESI标记，则应当在Apache配置中声明以下属性：

```
<LocationMatch "/parent-pages/*content/page.html">
   # disable dispatcher compression
   SetEnv no-gzip 1
   # enable esi processing 
   Header set x-aem-esi "on"
   # enable edgeCDN compression
   Header set x-aem-compress "on"

   # typically the main page is cached at the CDN
   Header always set Cache-Control "max-age=300"
 </LocationMatch>


<LocationMatch "/content/snippets/mysnippet.html">
  SetEnv no-gzip 1

  # typically the included page is either set to a lower TTL than the parent page, or not cached at all, as these 2 commented declarations show, respectively:
  #Header always set Cache-Control "no-cache"
  #Header always set Cache-Control "max-age=50"
 </LocationMatch> 
```

配置的属性具有以下行为：

| 属性 | 行为 |
|-----------|--------------------------|
| **no-gzip** | 如果设置为1，则会将HTML页面从Apache未压缩地传输到CDN。 这对于ESI是必需的，因为内容必须未压缩地发送到CDN，以便CDN可以查看和评估ESI标记。<br/><br/>父页面和包含的片段都应将no-gzip设置为1。<br/><br/>根据请求的 `Accept-Encoding` 值。 |
| **x-aem-esi** | 如果设置为“开”，CDN将评估父HTML页面的ESI标记。  默认情况下，未设置标头。 |
| **x-aem-compress** | 如果设置为“开”，则CDN会将内容从CDN压缩到浏览器。 由于从Apache到CDN的父页面传输必须解压缩，ESI才能正常工作(`no-gzip` 设置为1)，这将减少延迟。<br/><br/>如果未设置此标头，则当CDN从未压缩的原始服务器中检索内容时，它也会向未压缩的客户端提供内容。 因此，如果符合以下条件，则必须设置此标头 `no-gzip` 设置为1（ESI必需），并且需要向浏览器提供从CDN压缩的内容。 |

## Sling Dynamic 包括 {#esi-sdi}

虽然不需要， [Sling Dynamic包括](https://sling.apache.org/documentation/bundles/dynamic-includes.html) (SDI)可用于生成在CDN上解释的ESI片段。
