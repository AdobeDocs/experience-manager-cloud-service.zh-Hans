---
title: AEM as a Cloud Service 中的缓存
description: 了解AEM as a Cloud Service中的缓存基础知识
feature: Dispatcher
exl-id: 4206abd1-d669-4f7d-8ff4-8980d12be9d6
role: Admin
source-git-commit: 0e328d013f3c5b9b965010e4e410b6fda2de042e
workflow-type: tm+mt
source-wordcount: '2894'
ht-degree: 1%

---

# 简介 {#intro}

流量通过CDN传输到Apache Web服务器层，该层支持包括Dispatcher在内的模块。 为了提高性能，Dispatcher主要用作缓存以限制发布节点上的处理。
可以将规则应用于Dispatcher配置以修改任何默认的缓存过期设置，从而在CDN上生成缓存。 如果在Dispatcher配置中启用了`enableTTL`，则Dispatcher还遵循生成的缓存过期标头，这意味着它刷新特定内容，即使这些内容不在要重新发布的内容之列。

本页还介绍了Dispatcher缓存如何失效以及缓存如何在浏览器级别使用客户端库。

## 缓存 {#caching}

### HTML/文本 {#html-text}

* 默认情况下，根据Apache层发出的`cache-control`标头，浏览器将缓存五分钟。 CDN也遵循此值。
* 可以通过在`global.vars`中定义`DISABLE_DEFAULT_CACHING`变量来禁用默认HTML/文本缓存设置：

```
Define DISABLE_DEFAULT_CACHING
```

例如，当您的业务逻辑需要微调页面标头（具有基于日历天的值）时，此方法非常有用，因为默认情况下，页面标头设置为0。 也就是说，**在关闭默认缓存时要小心。**

* 可以通过使用AEM as a Cloud Service SDK Dispatcher工具在`global.vars`中定义`EXPIRATION_TIME`变量来覆盖所有HTML/文本内容。
* 可以使用以下Apache `mod_headers`指令在更细粒度级别覆盖，包括独立控制CDN和浏览器缓存：

  ```
  <LocationMatch "^/content/.*\.(html)$">
       Header set Cache-Control "max-age=200"
       Header set Surrogate-Control "max-age=3600"
       Header set Age 0
  </LocationMatch>
  ```

  >[!NOTE]
  >Surrogate-Control标头适用于Adobe托管的CDN。 如果使用[客户管理的CDN](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn.html#point-to-point-CDN)，则根据您的CDN提供商，可能需要不同的标头。

  在设置与宽正则表达式匹配的全局缓存控制标头或类似缓存标头时，请务必谨慎，以免将它们应用于必须保持私密的内容。 请考虑使用多个指令，以确保以细粒度应用规则。 这样一来，如果AEM as a Cloud Service检测到缓存标头已应用于它检测到无法由Dispatcher缓存的内容，则会删除该缓存标头，如Dispatcher文档中所述。 要强制AEM始终应用缓存标头，可以按如下方式添加&#x200B;**`always`**&#x200B;选项：

  ```
  <LocationMatch "^/content/.*\.(html)$">
       Header unset Cache-Control
       Header unset Expires
       Header always set Cache-Control "max-age=200"
       Header set Age 0
  </LocationMatch>
  ```

  确保`src/conf.dispatcher.d/cache`下的文件具有以下规则（默认配置中的规则）：

  ```
  /0000
  { /glob "*" /type "allow" }
  ```

* 若要防止在CDN **处缓存**&#x200B;特定内容，请将Cache-Control标头设置为&#x200B;*private*。 例如，以下内容将阻止在CDN上缓存名为&#x200B;**secure**&#x200B;的目录下的html内容：

  ```
     <LocationMatch "/content/secure/.*\.(html)$">.  // replace with the right regex
     Header unset Cache-Control
     Header unset Expires
     Header always set Cache-Control "private"
    </LocationMatch>
  ```

* 虽然未在CDN中缓存设置为私有的HTML内容，但如果配置了[权限敏感型缓存](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/permissions-cache.html?lang=zh-Hans)，则可以在Dispatcher中缓存该内容，从而确保仅授权用户提供该内容。

  >[!NOTE]
  >其他方法(包括[Dispatcher-ttl AEM ACS Commons项目](https://adobe-consulting-services.github.io/acs-aem-commons/features/dispatcher-ttl/))未成功覆盖值。

  >[!NOTE]
  >Dispatcher可能仍会根据自己的[缓存规则](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17497.html)来缓存内容。 要使内容真正为私有，请确保Dispatcher不缓存该内容。

### 客户端库(js，css) {#client-side-libraries}

* 使用AEM的客户端库框架时，生成JavaScript和CSS代码的方式使得浏览器可以无限期地缓存它，因为任何更改都会显示为具有唯一路径的新文件。 换句话说，会根据需要生成引用客户端库的HTML，以便客户可以在发布新内容时体验这些内容。 对于不遵循“不可变”值的旧版浏览器，缓存控制设置为“不可变”，或者为30天。
* 有关其他详细信息，请参阅[客户端库和版本一致性](#content-consistency)部分。

### 足够大的图像及任何内容可存储在Blob存储中 {#images}

2022年5月中旬之后创建的程序(特别是高于65000的程序ID)的默认行为是默认缓存，同时还要考虑请求的身份验证上下文。 默认情况下，旧版程序(程序ID等于或小于65000)不会缓存Blob内容。

在这两种情况下，可以使用Apache `mod_headers`指令在Apache/Dispatcher层的更细粒度级别覆盖缓存标头，例如：

```
   <LocationMatch "^/content/.*\.(jpeg|jpg)$">
     Header set Cache-Control "max-age=222"
     Header set Age 0
   </LocationMatch>
```

在Dispatcher层修改缓存标头时，请务必小心不要缓存太广。 请参阅以上](#html-text)的HTML/文本部分[中的讨论。 此外，请确保应该保持私有（而不是缓存）的资产不属于`LocationMatch`指令过滤器的一部分。

AEM通常将存储在Blob存储中的JCR资源（大于16KB）用作302重定向。 截获这些重定向后，CDN将跟随，内容将直接从blob存储中交付。 只能对这些响应自定义有限的一组标头。 例如，要自定义`Content-Disposition`，您应按如下方式使用Dispatcher指令：

```
<LocationMatch "\.(?i:pdf)$">
  ForceType application/pdf
  Header set Content-Disposition inline
  </LocationMatch>
```

可以在Blob响应中自定义的标头列表包括：

```
content-security-policy
x-frame-options
x-xss-protection
x-content-type-options
x-robots-tag
access-control-allow-origin
content-disposition
permissions-policy
referrer-policy
x-vhost
content-disposition
cache-control
vary
```

#### 新的默认缓存行为 {#new-caching-behavior}

AEM层根据是否已设置缓存标头和请求类型的值来设置缓存标头。 如果未设置缓存控制标头，则会缓存公共内容，并且经过身份验证的流量会设置为private。 如果设置了缓存控制标头，则缓存标头保持不变。

| 是否存在缓存控制标头？ | 请求类型 | AEM将缓存标头设置为 |
|------------------------------|---------------|------------------------------------------------|
| 否 | 公共 | Cache-Control： public， max-age=600，不可变 |
| 否 | 已验证 | Cache-Control： private， max-age=600，不可变 |
| 是 | 任何 | 未更改 |

虽然不建议这样做，但可以通过将Cloud Manager环境变量`AEM_BLOB_ENABLE_CACHING_HEADERS`设置为false，将新的默认行为更改为遵循旧行为(程序id等于或小于65000)。

#### 较旧的默认缓存行为 {#old-caching-behavior}

默认情况下，AEM层不缓存blob内容。

>[!NOTE]
>通过将Cloud Manager环境变量AEM_BLOB_ENABLE_CACHING_HEADERS设置为true，更改旧的默认行为以便与新行为(高于65000的程序ID)一致。 如果项目已经上线，请确保您验证在更改后，内容是否按预期运行。

现在，无法使用[权限敏感型缓存](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/permissions-cache.html?lang=zh-Hans)在Dispatcher中缓存标记为“私有”的Blob存储中的图像。 始终会从AEM源请求图像，并在用户获得授权时提供图像。

>[!NOTE]
>其他方法(包括[dispatcher-ttl AEM ACS Commons项目](https://adobe-consulting-services.github.io/acs-aem-commons/features/dispatcher-ttl/))无法成功覆盖这些值。

### 节点存储中的其他内容文件类型 {#other-content}

* 无默认缓存
* 无法使用用于html/文本文件类型的`EXPIRATION_TIME`变量设置默认值
* 通过指定适当的正则表达式，可以使用html/text部分中描述的相同LocationMatch策略设置缓存过期时间

### 进一步优化 {#further-optimizations}

* 避免使用`User-Agent`作为`Vary`标头的一部分。 旧版默认Dispatcher设置（在原型版本28之前）包含该变量，Adobe建议您使用以下步骤将其删除。
   * 在`<Project Root>/dispatcher/src/conf.d/available_vhosts/*.vhost`中找到vhost文件
   * 从所有vhost文件中删除或注释掉行： `Header append Vary User-Agent env=!dont-vary`，但default.vhost除外，其为只读
* 使用`Surrogate-Control`标头独立于浏览器缓存控制CDN缓存
* 请考虑应用[`stale-while-revalidate`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cache-Control#stale-while-revalidate)和[`stale-if-error`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cache-Control#stale-if-error)指令以允许后台刷新并避免缓存丢失，从而为用户保持内容的快速刷新。
   * 可以使用多种方法应用这些指令，但将30分钟的`stale-while-revalidate`添加到所有缓存控制标头是一个很好的起点。
* 下面是各种内容类型的示例，在设置自己的缓存规则时，可参考这些示例。 请仔细考虑并测试您的特定设置和要求：

   * 缓存可变的客户端库资源达12小时，12小时后进行后台刷新。

     ```
     <LocationMatch "^/etc\.clientlibs/.*\.(?i:json|png|gif|webp|jpe?g|svg)$">
        Header set Cache-Control "max-age=43200,stale-while-revalidate=43200,stale-if-error=43200,public" "expr=%{REQUEST_STATUS} < 400"
        Header set Age 0
     </LocationMatch>
     ```

   * 通过后台刷新缓存不可变的客户端库资源长期（30天）以避免丢失。

     ```
     <LocationMatch "^/etc\.clientlibs/.*\.(?i:js|css|ttf|woff2)$">
        Header set Cache-Control "max-age=2592000,stale-while-revalidate=43200,stale-if-error=43200,public,immutable" "expr=%{REQUEST_STATUS} < 400"
        Header set Age 0
     </LocationMatch>
     ```

   * 在浏览器上缓存5分钟HTML页，后台刷新一小时，在CDN上缓存12小时。 将始终添加Cache-Control标头，因此请务必确保在/content/*下与html页面匹配的页面是公共的。 如果不能，请考虑使用更具体的正则表达式。

     ```
     <LocationMatch "^/content/.*\.html$">
        Header unset Cache-Control
        Header always set Cache-Control "max-age=300,stale-while-revalidate=3600" "expr=%{REQUEST_STATUS} < 400"
        Header always set Surrogate-Control "stale-while-revalidate=43200,stale-if-error=43200" "expr=%{REQUEST_STATUS} < 400"
        Header set Age 0
     </LocationMatch>
     ```

   * 将内容服务/Sling模型导出程序json响应缓存五分钟，在浏览器上后台刷新一小时，在CDN上后台刷新十二小时。

     ```
     <LocationMatch "^/content/.*\.model\.json$">
        Header set Cache-Control "max-age=300,stale-while-revalidate=3600" "expr=%{REQUEST_STATUS} < 400"
        Header set Surrogate-Control "stale-while-revalidate=43200,stale-if-error=43200" "expr=%{REQUEST_STATUS} < 400"
        Header set Age 0
     </LocationMatch>
     ```

   * 通过后台刷新来缓存核心图像组件中的不可变URL，以使其保持长期（30天）不变，从而避免MISS。

     ```
     <LocationMatch "^/content/.*\.coreimg.*\.(?i:jpe?g|png|gif|svg)$">
        Header set Cache-Control "max-age=2592000,stale-while-revalidate=43200,stale-if-error=43200,public,immutable" "expr=%{REQUEST_STATUS} < 400"
        Header set Age 0
     </LocationMatch>
     ```

   * 将来自DAM的可变资源（如图像和视频）缓存24小时，并在12小时后进行后台刷新以避免遗漏。

     ```
     <LocationMatch "^/content/dam/.*\.(?i:jpe?g|gif|js|mov|mp4|png|svg|txt|zip|ico|webp|pdf)$">
        Header set Cache-Control "max-age=43200,stale-while-revalidate=43200,stale-if-error=43200" "expr=%{REQUEST_STATUS} < 400"
        Header set Age 0
     </LocationMatch>
     ```

### 分析CDN缓存命中率 {#analyze-chr}

有关使用仪表板下载CDN日志和分析网站缓存命中率的信息，请参阅[缓存命中率分析教程](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/caching/cdn-cache-hit-ratio-analysis.html)。

### HEAD请求行为 {#request-behavior}

在AdobeCDN上收到&#x200B;**未**&#x200B;缓存的资源的HEAD请求时，该请求将进行转换并作为GET请求由Dispatcher和/或AEM实例接收。 如果响应可缓存，则从CDN提供后续HEAD请求。 如果响应不可缓存，则后续HEAD请求将传递到Dispatcher或AEM实例，或同时传递到两者，时间取决于`Cache-Control` TTL。

### 营销活动参数 {#marketing-parameters}

网站URL通常包括用于跟踪营销活动成功的营销活动参数。

对于在2023年10月或之后创建的环境，为了更好地缓存请求，CDN将删除与营销相关的常见查询参数，特别是与以下正则表达式模式匹配的参数：

```
^(utm_.*|gclid|gdftrk|_ga|mc_.*|trk_.*|dm_i|_ke|sc_.*|fbclid)$
```

如果您希望禁用此行为，请提交支持票证。

对于2023年10月之前创建的环境，建议将Dispatcher配置的`ignoreUrlParams`属性配置为此处记录的[](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#ignoring-url-parameters)。

忽略营销参数有两种可能性。 （其中首选方法是通过查询参数忽略缓存无效）：

1. 忽略所有参数并选择性地允许使用的参数。
在以下示例中，仅`page`和`product`参数不会被忽略，请求将被转发到发布者。

```
/ignoreUrlParams {
   /0001 { /glob "*" /type "allow" }
   /0002 { /glob "page" /type "deny" }
   /0003 { /glob "product" /type "deny" }
}
```

1. 允许除营销参数之外的所有参数。 文件[marketing_query_parameters.any](https://github.com/adobe/aem-project-archetype/blob/develop/src/main/archetype/dispatcher.cloud/src/conf.dispatcher.d/cache/marketing_query_parameters.any)定义了将被忽略的常用营销参数的列表。 Adobe不会更新此文件。 用户可以对其进行扩展，具体取决于其营销提供商。

```
/ignoreUrlParams {
   /0001 { /glob "*" /type "deny" }
   $include "../cache/marketing_query_parameters.any"
}
```


## Dispatcher缓存失效 {#disp}

通常，无需使Dispatcher缓存失效。 实际上，您应该依赖Dispatcher在重新发布内容时刷新其缓存，以及CDN遵循缓存过期标头。

### 在激活/停用期间Dispatcher缓存失效 {#cache-activation-deactivation}

与以前版本的AEM一样，发布或取消发布页面会从Dispatcher缓存中清除内容。 如果怀疑存在缓存问题，应重新发布有问题的页面，并确保可用的虚拟主机与Dispatcher缓存失效所需的`ServerAlias`本地主机匹配。

>[!NOTE]
>为使Dispatcher正确失效，请确保来自“127.0.0.1”、“localhost”、“\*.local”、“\*.adobeaemcloud.com”和“\*.adobeaemcloud.net”的请求均匹配，并由vhost配置进行处理，以便提供该请求。 在执行此任务时，可以按照引用[AEM原型](https://github.com/adobe/aem-project-archetype/blob/develop/src/main/archetype/dispatcher.cloud/src/conf.d/available_vhosts/default.vhost)中的模式，在捕获所有vhost配置中全局匹配“*”。 或者，您可以确保上述列表由其中一台主机捕获。

当发布实例从作者那里收到新版本的页面或资源时，它使用刷新代理使其Dispatcher上的相应路径失效。 更新的路径及其父项会从Dispatcher缓存中删除，最多可删除一个级别（您可以使用[statfileslevel](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#invalidating-files-by-folder-level)配置此级别）。

## 明确使Dispatcher缓存失效 {#explicit-invalidation}

Adobe建议您依赖标准缓存标头来控制内容交付生命周期。 但是，如果需要，可以直接使Dispatcher中的内容失效。

以下列表包含可能想要显式使缓存失效的情况（同时可以选择侦听失效的完成）：

* 发布体验片段或内容片段等内容后，使引用这些元素的已发布和缓存的内容失效。
* 在引用的页面成功失效时通知外部系统。

有两种方法可明确使缓存失效：

* 首选方法是使用Author的Sling内容分发(SCD)。
* 另一种方法是使用复制API调用发布Dispatcher Flush复制代理。

这些方法在层可用性、消除重复事件的能力和事件处理保障方面有所不同。 下表总结了这些选项：

<table style="table-layout:auto">
 <tbody>
  <tr>
    <th>不适用</th>
    <th>层可用性</th>
    <th>删除重复项 </th>
    <th>保证 </th>
    <th>操作 </th>
    <th>影响 </th>
    <th>描述 </th>
  </tr>  
  <tr>
    <td>Sling内容分发(SCD) API</td>
    <td>创作</td>
    <td>可能使用发现API或启用<a href="https://github.com/apache/sling-org-apache-sling-distribution-journal/blob/e18f2bd36e8b43814520e87bd4999d3ca77ce8ca/src/main/java/org/apache/sling/distribution/journal/impl/publisher/DistributedEventNotifierManager.java#L146-L149">重复数据删除模式</a>。</td>
    <td>至少一次。</td>
    <td>
     <ol>
       <li>添加</li>
       <li>删除</li>
       <li>失效</li>
     </ol>
     </td>
    <td>
     <ol>
       <li>分层/统计级别</li>
       <li>分层/统计级别</li>
       <li>仅级别资源</li>
     </ol>
     </td>
    <td>
     <ol>
       <li>发布内容并使缓存失效。</li>
       <li>删除内容并使缓存失效。</li>
       <li>使内容失效而不发布内容。</li>
     </ol>
     </td>
  </tr>
  <tr>
    <td>复制 API</td>
    <td>发布</td>
    <td>不可能，将在每个发布实例上引发事件。</td>
    <td>尽力而为。</td>
    <td>
     <ol>
       <li>激活</li>
       <li>取消激活</li>
       <li>删除</li>
     </ol>
     </td>
    <td>
     <ol>
       <li>分层/统计级别</li>
       <li>分层/统计级别</li>
       <li>分层/统计级别</li>
     </ol>
     </td>
    <td>
     <ol>
       <li>发布内容并使缓存失效。</li>
       <li>从创作/Publish层 — 删除内容并使缓存失效。</li>
       <li><p><strong>从创作层</strong> — 删除内容并使缓存无效(如果从Publish代理上的AEM创作层触发)。</p>
           <p><strong>从Publish层</strong> — 仅使缓存失效(如果是从刷新代理或仅用于资源的刷新代理上的AEM Publish层触发的)。</p>
       </li>
     </ol>
     </td>
  </tr>
  </tbody>
</table>

与缓存失效直接相关的两个操作是Sling内容分发(SCD) API失效和复制API停用。

此外，从表中可以看到：

* 当必须保证每个事件时（例如，与需要准确知识的外部系统同步），需要SCD API。 如果在失效调用时存在发布层升级事件，则当每个新发布处理失效时，将引发一个额外事件。

* 使用复制API不是常见用例，但可用于以下情况：使缓存失效的触发器来自发布层，而不是创作层。 如果配置了Dispatcher TTL，此方法可能很有用。

最后，如果您要使Dispatcher缓存失效，建议的选项是使用来自创作实例的SCD API失效操作。 此外，您还可以监听事件，以便随后触发后续操作。

### Sling内容分发(SCD) {#sling-distribution}

>[!NOTE]
>使用下面提供的说明时，请在AEM Cloud Service开发环境中测试自定义代码，而不是在本地测试。

使用来自创作实例的SCD操作时，实施模式如下所示：

1. 在Author中，编写自定义代码以调用Sling内容分发[API](https://sling.apache.org/documentation/bundles/content-distribution.html)，通过路径列表传递失效操作：

```
@Reference
private Distributor distributor;

ResourceResolver resolver = ...; // the resource resolver used for authorizing the request
String agentName = "publish";    // the name of the agent used to distribute the request

String pathToInvalidate = "/content/to/invalidate";
DistributionRequest distributionRequest = new SimpleDistributionRequest(DistributionRequestType.INVALIDATE, false, pathToInvalidate);
distributor.distribute(agentName, resolver, distributionRequest);
```

* （可选）侦听一个事件，该事件反映所有Dispatcher实例中的资源都将失效：


```
package org.apache.sling.distribution.journal.shared;

import org.apache.sling.discovery.DiscoveryService;
import org.apache.sling.distribution.journal.impl.event.DistributionEvent;
import org.osgi.service.component.annotations.Component;
import org.osgi.service.component.annotations.Reference;
import org.osgi.service.event.Event;
import org.osgi.service.event.EventHandler;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import static org.apache.sling.distribution.DistributionRequestType.INVALIDATE;
import static org.apache.sling.distribution.event.DistributionEventProperties.DISTRIBUTION_PATHS;
import static org.apache.sling.distribution.event.DistributionEventProperties.DISTRIBUTION_TYPE;
import static org.apache.sling.distribution.event.DistributionEventTopics.AGENT_PACKAGE_DISTRIBUTED;
import static org.osgi.service.event.EventConstants.EVENT_TOPIC;

@Component(immediate = true, service = EventHandler.class, property = {
        EVENT_TOPIC + "=" + AGENT_PACKAGE_DISTRIBUTED
})
public class InvalidatedHandler implements EventHandler {
    private static final Logger LOG = LoggerFactory.getLogger(InvalidatedHandler.class);

    @Reference
    private DiscoveryService discoveryService;

    @Override
    public void handleEvent(Event event) {

        String distributionType = (String) event.getProperty(DISTRIBUTION_TYPE);

        if (INVALIDATE.name().equals(distributionType)) {
            boolean isLeader = discoveryService.getTopology().getLocalInstance().isLeader();
            // process the OSGi event on the leader author instance
            if (isLeader) {
                String[] paths = (String[]) event.getProperty(DISTRIBUTION_PATHS);
                String packageId = (String) event.getProperty(DistributionEvent.PACKAGE_ID);
                invalidated(paths, packageId);
            }
        }
    }

    private void invalidated(String[] paths, String packageId) {
        // custom logic
        LOG.info("Successfully applied package with id {}, paths {}", packageId, paths);
    }
}
```

<!-- Optionally, instead of using the isLeader approach, one could add an OSGi configuration for the PID org.apache.sling.distribution.journal.impl.publisher.DistributedEventNotifierManager and property deduplicateEvent=true. But we'll stick with just one strategy and not mention it (double-check this).**review this**-->

* （可选）在上述`invalidated(String[] paths, String packageId)`方法中执行业务逻辑。

>[!NOTE]
>
>Dispatcher失效时，不会刷新AdobeCDN。 Adobe管理的CDN遵循TTL，因此无需刷新TTL。

### 复制 API {#replication-api}

下面显示了使用复制API停用操作时的实施模式：

1. 在发布层上，调用复制API以触发发布Dispatcher Flush复制代理。

刷新代理端点不可配置，而是预配置为指向Dispatcher，与随刷新代理运行的发布服务匹配。

刷新代理通常可以由基于OSGi事件或工作流的自定义代码触发。

```
String[] paths = …
ReplicationOptions options = new ReplicationOptions();
options.setSynchronous(true);
options.setFilter( new AgentFilter {
  public boolean isIncluded (Agent agent) {
   return agent.getId().equals("flush");
  }
});

Replicator.replicate (session,ReplicationActionType.DELETE,paths, options);
```

<!-- In general, it will not be necessary to manually invalidate content in the dispatcher, but it is possible if needed.

>[!NOTE]
>Prior to AEM as a Cloud Service, there were two ways of invalidating the dispatcher cache.
>
>1. Invoke the replication agent, specifying the publish dispatcher flush agent
>2. Directly calling the `invalidate.cache` API (for example, `POST /dispatcher/invalidate.cache`)
>
>The dispatcher's `invalidate.cache` API approach will no longer be supported since it addresses only a specific dispatcher node. AEM as a Cloud Service operates at the service level, not the individual node level and so the invalidation instructions in the [Invalidating Cached Pages From AEM](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/page-invalidate.html) page are not longer valid for AEM as a Cloud Service.

The replication flush agent should be used. This can be done using the [Replication API](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/replication/Replicator.html). The flush agent endpoint is not configurable but pre-configured to point to the dispatcher, matched with the publish service running the flush agent. The flush agent can typically be triggered by OSGi events or workflows.

<!-- Need to find a new link and/or example -->
<!-- 
and for an example of flushing the cache, see the [API example page](https://helpx.adobe.com/experience-manager/using/aem64_replication_api.html) (specifically the `CustomStep` example issuing a replication action of type ACTIVATE to all available agents). 

The diagram presented below illustrates this.

![CDN](assets/cdnd.png "CDN")

If there is a concern that the dispatcher cache is not clearing, contact [customer support](https://helpx.adobe.com/support.ec.html) who can flush the dispatcher cache if necessary.

The Adobe-managed CDN respects TTLs and thus there is no need fo it to be flushed. If an issue is suspected, [contact customer support](https://helpx.adobe.com/support.ec.html) support who can flush an Adobe-managed CDN cache as necessary. -->

## 客户端库和版本一致性 {#content-consistency}

页面由HTML、JavaScript、CSS和图像组成。 建议客户使用[客户端库(clientlibs)框架](/help/implementing/developing/introduction/clientlibs.md)将JavaScript和CSS资源导入HTML页，并考虑JS库之间的依赖关系。

clientlibs框架提供自动版本管理。 这意味着开发人员可以在源代码管理中检查对JS库的更改，并且在客户推送其版本时提供最新版本。 如果没有此工作流，开发人员必须手动更改引用库新版本的HTML，如果同一库共享许多HTML模板，则更改操作会非常繁重。

将库的新版本发布到生产环境后，将会更新引用HTML页面，并包含指向这些已更新库版本的新链接。 在给定HTML页面的浏览器缓存过期后，无需担心旧库会从浏览器缓存中加载。 原因是现在，刷新页面(来自AEM)必定会引用库的新版本。 即，刷新的HTML页面包含所有最新库版本。

这种能力背后的机制是序列化哈希，该哈希会附加到客户端库链接中。 它确保浏览器拥有唯一的版本化URL来缓存CSS/JS。 仅当客户端库的内容更改时，才会更新序列化哈希。 这意味着即使进行了新部署，如果发生不相关的更新（即不更改客户端库的基础css/js），引用将保持不变。 反过来，它可以确保减少浏览器缓存的中断。

### 启用客户端库的Longcache版本 — AEM as a Cloud Service SDK快速入门 {#enabling-longcache}

HTML页面上默认的clientlib include类似于以下示例：

```
<link rel="stylesheet" href="/etc.clientlibs/wkndapp/clientlibs/clientlib-base.css" type="text/css">
```

启用严格的clientlib版本控制后，会向客户端库添加一个长期哈希键作为选择器。 因此，clientlib引用如下所示：

```
<link rel="stylesheet" href="/etc.clientlibs/wkndapp/clientlibs/clientlib-base.lc-7c8c5d228445ff48ab49a8e3c865c562-lc.css" type="text/css">
```

默认情况下，所有AEM as a Cloud Service环境中都启用严格的clientlib版本控制。

要在本地SDK快速入门中启用严格的clientlib版本控制，请执行以下操作：

1. 导航到OSGi配置管理器`<host>/system/console/configMgr`
1. 查找AdobeGraniteHTML库管理器的OSGi配置：
   * 选中复选框，以便启用严格版本控制
   * 在标记为&#x200B;**长期客户端缓存密钥**&#x200B;的字段中，输入/的值。*；哈希
1. 保存更改。 无需在源代码管理中保存此配置，因为AEM as a Cloud Service会自动在开发、暂存和生产环境中启用此配置。
1. 无论何时改变客户端库的内容，都生成新的散列密钥并更新HTML引用。
