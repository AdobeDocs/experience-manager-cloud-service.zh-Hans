---
title: AEM as a Cloud Service 中的缓存
description: 'AEM as a Cloud Service 中的缓存 '
feature: Dispatcher
exl-id: 4206abd1-d669-4f7d-8ff4-8980d12be9d6
source-git-commit: 91a88cb02192defdd651ecb6d108d4540186d06e
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# 简介 {#intro}

流量会通过CDN传递到Apache Web服务器层，该层支持包括调度程序在内的模块。 为了提高性能，调度程序主要用作缓存以限制发布节点上的处理。
可以将规则应用于调度程序配置以修改任何默认的缓存过期设置，从而导致在CDN上缓存。 请注意，如果 `enableTTL` 在dispatcher配置中启用，这意味着即使在重新发布的内容之外，它也将刷新特定内容。

本页还介绍调度程序缓存如何失效，以及缓存在浏览器级别与客户端库有关的工作方式。

## 缓存 {#caching}

### HTML/文本 {#html-text}

* 默认情况下，会根据 `cache-control` apache层发出的标头。 CDN还尊重此价值。
* 通过定义 `DISABLE_DEFAULT_CACHING` 变量 `global.vars`:

```
Define DISABLE_DEFAULT_CACHING
```

例如，当您的业务逻辑需要微调页面标题（其值基于日历日）时，这非常有用，因为默认情况下，页面标题设置为0。 话虽如此， **关闭默认缓存时请务必谨慎。**

* 可以通过定义 `EXPIRATION_TIME` 变量 `global.vars` 使用AEMas a Cloud ServiceSDK Dispatcher工具。
* 可以在更精细的粒度级别上覆盖，包括通过以下apache mod_headers指令独立控制CDN和浏览器缓存：

   ```
   <LocationMatch "^/content/.*\.(html)$">
        Header set Cache-Control "max-age=200"
        Header set Surrogate-Control "max-age=3600"
        Header set Age 0
   </LocationMatch>
   ```

   >[!NOTE]
   >代理控制标头适用于Adobe管理的CDN。 如果使用 [客户管理的CDN](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn.html?lang=en#point-to-point-CDN)，则可能需要不同的标头，具体取决于您的CDN提供商。

   在设置全局缓存控制标头或与宽正则表达式匹配的标头时，请务必谨慎，以便这些标头不会应用于您可能打算保留为私有的内容。 请考虑使用多个指令，以确保以细粒度方式应用规则。 根据上述说明，如果AEM as a Cloud Service检测到已将缓存标头应用于Dispatcher检测到的不可执行的内容，则它将删除该缓存标头，如Dispatcher文档中所述。 为了强制AEM始终应用缓存标头，您可以添加 **always** 选项：

   ```
   <LocationMatch "^/content/.*\.(html)$">
        Header unset Cache-Control
        Header unset Expires
        Header always set Cache-Control "max-age=200"
        Header set Age 0
   </LocationMatch>
   ```

   您必须确保 `src/conf.dispatcher.d/cache` 具有以下规则（默认配置中）：

   ```
   /0000
   { /glob "*" /type "allow" }
   ```

* 阻止缓存特定内容 **在CDN**，请将Cache-Control标头设置为 *私人*. 例如，下面会阻止名为 **安全** 从缓存到CDN :

   ```
      <LocationMatch "/content/secure/.*\.(html)$">.  // replace with the right regex
      Header unset Cache-Control
      Header unset Expires
      Header always set Cache-Control “private”
     </LocationMatch>
   ```

   >[!NOTE]
   >其他方法，包括 [dispatcher-ttl AEM ACS Commons项目](https://adobe-consulting-services.github.io/acs-aem-commons/features/dispatcher-ttl/)，则无法成功覆盖值。

   >[!NOTE]
   >请注意，调度程序可能仍会根据其自己的内容来缓存内容 [缓存规则](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17497.html). 要使内容真正私有，您应确保dispatcher不会缓存该内容。

### 客户端库(js，css) {#client-side-libraries}

* 通过使用AEM客户端库框架，可以生成JavaScript和CSS代码，以便浏览器可以无限期地缓存它，因为任何更改都将显示为具有唯一路径的新文件。  换言之，将根据需要生成引用客户端库的HTML，以便客户在发布新内容时能够体验到新内容。 对于不遵循“不可变”值的旧版浏览器，缓存控制将设置为“不可变”或30天。
* 请参阅部分 [客户端库和版本一致性](#content-consistency) 以了解更多详细信息。

### 图像和任何足够大且可存储到blob存储中的内容 {#images}

2022年5月中旬之后创建的程序(特别是高于65000的程序ID)的默认行为是默认缓存，同时尊重请求的身份验证上下文。 默认情况下，旧程序(程序ID等于或低于65000)不会缓存Blob内容。

在这两种情况下，可以使用Apache在Apache/Dispatcher层以更细粒度级别覆盖缓存标头 `mod_headers` 指令，例如：

```
   <LocationMatch "^/content/.*\.(jpeg|jpg)$">
     Header set Cache-Control "max-age=222"
     Header set Age 0
   </LocationMatch>
```

修改调度程序层的缓存标头时，请小心不要缓存得太广，请参阅HTML/文本部分中的讨论 [以上](#html-text). 此外，请确保要保持私有（而不是缓存）的资产不属于 `LocationMatch` 指令筛选器。

#### 新的默认缓存行为 {#new-caching-behavior}

AEM层将根据是否已设置缓存标头和请求类型的值来设置缓存标头。 请注意，如果未设置缓存控制标头，则会缓存公共内容，并将经过身份验证的流量设置为私有。 如果已设置缓存控制标头，则缓存标头将不受影响。

| 是否存在缓存控制标头？ | 请求类型 | AEM将缓存标头设置为 |
|------------------------------|---------------|------------------------------------------------|
| 否 | 公共 | Cache-Control:public， max-age=600，不可变 |
| 否 | 已验证 | Cache-Control:private，max-age=600，不可变 |
| 是 | 任何 | 未更改 |

虽然不推荐，但可以通过设置Cloud Manager环境变量来更改新的默认行为，以遵循旧行为(程序ID等于或小于65000) `AEM_BLOB_ENABLE_CACHING_HEADERS` 为false。

#### 旧的默认缓存行为 {#old-caching-behavior}

默认情况下，AEM层不会缓存Blob内容。

>[!NOTE]
>建议通过将Cloud Manager环境变量AEM_BLOB_ENABLE_CACHING_HEADERS设置为true，将旧的默认行为更改为与新行为(程序ID大于65000)一致。 如果程序已处于实时状态，请确保您确认在进行更改后，内容会按预期运行。

>[!NOTE]
>其他方法，包括 [dispatcher-ttl AEM ACS Commons项目](https://adobe-consulting-services.github.io/acs-aem-commons/features/dispatcher-ttl/)，则无法成功覆盖值。

### 节点存储中的其他内容文件类型 {#other-content}

* 无默认缓存
* 默认值不能设置为 `EXPIRATION_TIME` 用于html/文本文件类型的变量
* 可通过指定适当的正则表达式，使用html/text部分中描述的相同LocationMatch策略来设置缓存过期

### 进一步优化 {#further-optimizations}

* 避免使用 `User-Agent` 作为 `Vary` 标题。 旧版默认Dispatcher设置（在原型版本28之前）包含此内容，我们建议您使用以下步骤删除该设置。
   * 在 `<Project Root>/dispatcher/src/conf.d/available_vhosts/*.vhost`
   * 删除或注释掉行： `Header append Vary User-Agent env=!dont-vary` 从所有vhost文件中删除，但default.vhost除外，它为只读
* 使用 `Surrogate-Control` 用于独立于浏览器缓存控制CDN缓存的标头
* 考虑应用 [`stale-while-revalidate`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cache-Control#stale-while-revalidate) 和 [`stale-if-error`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cache-Control#stale-if-error) 指令，以允许后台刷新并避免缓存缺失，从而让用户快速、新鲜地查看内容。
   * 有多种方法可以应用这些指令，但需要添加30分钟 `stale-while-revalidate` 对所有缓存控制标头都是一个很好的起点。
* 下面是各种内容类型的一些示例，在设置您自己的缓存规则时，这些内容可用作指南。 请仔细考虑并测试您的具体设置和要求：

   * 缓存12h的可变客户端库资源，12h后进行后台刷新。

      ```
      <LocationMatch "^/etc\.clientlibs/.*\.(?i:json|png|gif|webp|jpe?g|svg)$">
         Header set Cache-Control "max-age=43200,stale-while-revalidate=43200,stale-if-error=43200,public" "expr=%{REQUEST_STATUS} < 400"
         Header set Age 0
      </LocationMatch>
      ```

   * 通过后台刷新，长期（30天）缓存不可变的客户端库资源，以避免MISS。

      ```
      <LocationMatch "^/etc\.clientlibs/.*\.(?i:js|css|ttf|woff2)$">
         Header set Cache-Control "max-age=2592000,stale-while-revalidate=43200,stale-if-error=43200,public,immutable" "expr=%{REQUEST_STATUS} < 400"
         Header set Age 0
      </LocationMatch>
      ```

   * 在浏览器上缓存HTML页面5分钟，后台刷新1小时，在CDN上缓存12小时。 将始终添加Cache-Control标头，因此务必要确保/content/*下匹配的html页面是公共的。 如果没有，请考虑使用更具体的正则表达式。

      ```
      <LocationMatch "^/content/.*\.html$">
         Header unset Cache-Control
         Header always set Cache-Control "max-age=300,stale-while-revalidate=3600" "expr=%{REQUEST_STATUS} < 400"
         Header always set Surrogate-Control "stale-while-revalidate=43200,stale-if-error=43200" "expr=%{REQUEST_STATUS} < 400"
         Header set Age 0
      </LocationMatch>
      ```

   * 将内容服务/Sling模型导出程序json响应缓存5分钟，在浏览器上刷新1小时，在CDN上刷新12小时。

      ```
      <LocationMatch "^/content/.*\.model\.json$">
         Header set Cache-Control "max-age=300,stale-while-revalidate=3600" "expr=%{REQUEST_STATUS} < 400"
         Header set Surrogate-Control "stale-while-revalidate=43200,stale-if-error=43200" "expr=%{REQUEST_STATUS} < 400"
         Header set Age 0
      </LocationMatch>
      ```

   * 长期（30天）通过后台刷新缓存核心图像组件中的不可变URL，以避免发生遗漏。

      ```
      <LocationMatch "^/content/.*\.coreimg.*\.(?i:jpe?g|png|gif|svg)$">
         Header set Cache-Control "max-age=2592000,stale-while-revalidate=43200,stale-if-error=43200,public,immutable" "expr=%{REQUEST_STATUS} < 400"
         Header set Age 0
      </LocationMatch>
      ```

   * 缓存DAM中可变资源（如图像和视频）24小时，并在12小时后进行后台刷新，以避免发生错误

      ```
      <LocationMatch "^/content/dam/.*\.(?i:jpe?g|gif|js|mov|mp4|png|svg|txt|zip|ico|webp|pdf)$">
         Header set Cache-Control "max-age=43200,stale-while-revalidate=43200,stale-if-error=43200" "expr=%{REQUEST_STATUS} < 400"
         Header set Age 0
      </LocationMatch>
      ```

### HEAD请求行为 {#request-behavior}

在AdobeCDN中接收HEAD请求时， **not** 缓存后，调度程序和/或AEM实例将该请求转换并作为GET请求接收。 如果响应可缓存，则随后将从CDN提供HEAD请求。 如果响应不可缓存，则后续HEAD请求将在一段时间内(取决于 `Cache-Control` TTL。

## 调度程序缓存失效 {#disp}

通常，不必使调度程序缓存失效。 相反，在重新发布内容时，您应该依赖调度程序刷新其缓存，并依赖CDN遵守缓存过期标头。

### 在激活/停用期间使调度程序缓存失效 {#cache-activation-deactivation}

与AEM的先前版本一样，发布或取消发布页面将从调度程序缓存中清除内容。 如果怀疑存在缓存问题，客户应重新发布相关页面，并确保虚拟主机与ServerAlias localhost匹配，Dispatcher缓存失效需要该ServerAlias localhost。


当发布实例收到作者提供的页面或资产的新版本时，它会使用刷新代理使其调度程序上的相应路径失效。 更新的路径将从调度程序缓存及其父缓存中删除，最高级别为(您可以使用 [stafileslevel](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#invalidating-files-by-folder-level))。

### 显式调度程序缓存失效 {#explicit-invalidation}

通常，无需手动使调度程序中的内容失效，但如果需要，可以这样做。

>[!NOTE]
>在AEMas a Cloud Service之前，有两种方法可使调度程序缓存失效。
>
>1. 调用复制代理，指定发布调度程序刷新代理
>2. 直接调用 `invalidate.cache` API(例如， `POST /dispatcher/invalidate.cache`)

>
>调度程序的 `invalidate.cache` 不再支持API方法，因为它只处理特定的调度程序节点。 AEMas a Cloud Service在服务级别运行，而不是在单个节点级别运行，因此 [使从AEM中缓存的页面失效](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/page-invalidate.html) 页面对AEMas a Cloud Service无效。

应使用复制刷新代理。 可以使用 [复制API](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/replication/Replicator.html). 无法配置刷新代理端点，但已预配置为指向与运行刷新代理的发布服务匹配的调度程序。 刷新代理通常可以由OSGi事件或工作流触发。

<!-- Need to find a new link and/or example -->
<!-- 
and for an example of flushing the cache, see the [API example page](https://helpx.adobe.com/experience-manager/using/aem64_replication_api.html) (specifically the `CustomStep` example issuing a replication action of type ACTIVATE to all available agents). 
-->

下图说明了这一点。

![CDN](assets/cdnd.png "CDN")

如果担心调度程序缓存未清除，请联系 [客户支持](https://helpx.adobe.com/support.ec.html) 可以刷新调度程序缓存的用户。

Adobe管理的CDN遵循TTL，因此无需刷新。 如果怀疑存在问题， [联系客户支持](https://helpx.adobe.com/support.ec.html) 支持谁可以根据需要刷新Adobe管理的CDN缓存。

## 客户端库和版本一致性 {#content-consistency}

页面由HTML、Javascript、CSS和图像组成。 我们鼓励客户利用 [客户端库(clientlibs)框架](/help/implementing/developing/introduction/clientlibs.md) 将Javascript和CSS资源导入HTML页面，同时考虑JS库之间的依赖关系。

clientlibs框架提供了自动版本管理，这意味着开发人员可以在源代码管理中签入对JS库的更改，并且当客户推送其版本时，将提供最新版本。 如果没有这些权限，开发人员将需要手动更改引用新版库的HTML，如果许多HTML模板共享同一库，则更加繁琐。

将库的新版本发布到生产环境后，将更新引用的HTML页面，其中包含指向这些更新库版本的新链接。 给定HTML页面的浏览器缓存过期后，无论从浏览器缓存中加载旧库，因为现在保证(从AEM中)刷新的页面会引用库的新版本。 换言之，刷新的HTML页面将包含所有最新的库版本。

其机制是序列化哈希，将附加到客户端库链接中，以确保浏览器有一个唯一的版本化URL来缓存CSS/JS。 仅当客户端库的内容发生更改时，才会更新序列化的哈希。 这意味着，即使在新部署中，如果发生不相关的更新（即对客户端库的基础css/js没有更改），则引用将保持不变，从而确保减少对浏览器缓存的中断。

### 启用客户端库的长缓存版本 — AEMas a Cloud ServiceSDK快速启动 {#enabling-longcache}

HTML页面上的默认clientlib包含如下示例所示：

```
<link rel="stylesheet" href="/etc.clientlibs/wkndapp/clientlibs/clientlib-base.css" type="text/css">
```

启用严格clientlib版本控制后，会将长期哈希键作为选择器添加到客户端库。 因此，clientlib引用如下所示：

```
<link rel="stylesheet" href="/etc.clientlibs/wkndapp/clientlibs/clientlib-base.lc-7c8c5d228445ff48ab49a8e3c865c562-lc.css" type="text/css">
```

默认情况下，所有AEMas a Cloud Service环境中都启用了严格clientlib版本控制。

要在本地SDK快速启动中启用严格的clientlib版本控制，请执行以下操作：

1. 导航到OSGi配置管理器 `<host>/system/console/configMgr`
1. 找到AdobeGraniteHTML库管理器的OSGi配置：
   * 选中此复选框可启用严格版本控制
   * 在标记为长期客户端缓存键的字段中，输入值/。*；哈希
1. 保存更改。请注意，无需在源代码管理中保存此配置，因为AEMas a Cloud Service将在开发、暂存和生产环境中自动启用此配置。
1. 每当客户端库的内容发生更改时，都会生成一个新的哈希键，并且HTML引用将会更新。
