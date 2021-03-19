---
title: AEM as a Cloud Service 中的缓存
description: 'AEM as a Cloud Service 中的缓存 '
feature: Dispatcher
translation-type: tm+mt
source-git-commit: 69c865dbc87ca021443e53b61440faca8fa3c4d4
workflow-type: tm+mt
source-wordcount: '1534'
ht-degree: 1%

---


# 简介 {#intro}

流量通过CDN传递到apache Web服务器层，该层支持包括调度程序的模块。 为了提高性能，调度程序主要用作缓存以限制发布节点上的处理。
规则可应用于调度程序配置以修改任何默认缓存过期设置，从而在CDN上缓存。 请注意，如果在调度程序配置中启用`enableTTL`，则调度程序还会考虑生成的缓存过期标头，这意味着即使在重新发布的内容之外，它也会刷新特定内容。

本页还描述了如何使调度程序缓存失效，以及在浏览器级别上缓存在客户端库方面的工作方式。

## 缓存{#caching}

### HTML/文本{#html-text}

* 默认情况下，根据apache图层发出的`cache-control`标头，由浏览器缓存五分钟。 CDN也尊重此价值。
* 通过在`global.vars`中定义`DISABLE_DEFAULT_CACHING`变量，可以禁用默认的HTML/文本缓存设置：

```
Define DISABLE_DEFAULT_CACHING
```

例如，当您的业务逻辑需要微调页面标题（其值基于日历日期）时，这可能很有用，因为默认情况下，页面标题设置为0。 也就是说，**在关闭默认缓存时请务必小心。**

* 可以通过在`global.vars`中定义`EXPIRATION_TIME`变量来覆盖所有HTML/Text内容，将AEM用作Cloud Service SDK Dispatcher工具。
* 可以由以下apache mod_headers指令在更细的粒度级别上覆盖：

   ```
   <LocationMatch "^/content/.*\.(html)$">
        Header set Cache-Control "max-age=200"
        Header set Age 0
   </LocationMatch>
   ```

   在设置全局缓存控制标头或与宽正则表达式匹配的标头时，请务必小心，以便它们不会应用于您可能打算保持私有的内容。 请考虑使用多个指令来确保以细粒度方式应用规则。 如上所述，如调度程序文档中所述，AEM作为Cloud Service将删除缓存头，前提是它检测到缓存头已应用于它检测到的调度程序不可执行的功能。 为了强制AEM始终应用缓存，可以添加“always”选项，如下所示：

   ```
   <LocationMatch "^/content/.*\.(html)$">
        Header always set Cache-Control "max-age=200"
        Header set Age 0
   </LocationMatch>
   ```

   必须确保`src/conf.dispatcher.d/cache`下的文件具有以下规则（默认配置中）：

   ```
   /0000
   { /glob "*" /type "allow" }
   ```

* 要防止对特定内容进行缓存，请将Cache-Control头设置为&#x200B;*private*。 例如，以下内容会阻止缓存名为&#x200B;**myfolder**&#x200B;的目录下的html内容：

   ```
      <LocationMatch "/content/myfolder/.*\.(html)$">.  // replace with the right regex
      Header set Cache-Control “private”
     </LocationMatch>
   ```

   >[!NOTE]
   >其他方法(包括[dispatcher-ttl AEM ACS Commons项目](https://adobe-consulting-services.github.io/acs-aem-commons/features/dispatcher-ttl/))将无法成功覆盖值。

### 客户端库(js，css){#client-side-libraries}

* 通过使用AEM客户端库框架，JavaScript和CSS代码的生成方式使浏览器可以无限地缓存它，因为任何更改都以具有唯一路径的新文件形式显示。  换句话说，将根据需要生成引用客户端库的HTML，以便客户能够在发布新内容时体验新内容。 对于不尊重“不可变”值的旧版浏览器，缓存控制设置为“不可变”或30天。
* 有关更多详细信息，请参阅[客户端库和版本一致性](#content-consistency)部分。

### 图像和任何足够大的内容存储在blob存储{#images}中

* 默认情况下，未缓存
* 可以通过以下apache `mod_headers`指令在更细的粒度级别上设置：

   ```
      <LocationMatch "^/content/.*\.(jpeg|jpg)$">
        Header set Cache-Control "max-age=222"
        Header set Age 0
      </LocationMatch>
   ```

   请参阅上面html/text部分中的讨论，以了解如何小心不要过度缓存，以及如何强制AEM始终使用“always”选项应用缓存。

   必须确保`src/conf.dispatcher.d/`缓存下的文件具有以下规则（默认配置中）：

   ```
   /0000
   { /glob "*" /type "allow" }
   ```

   确保要保持私有而不是缓存的资源不是LocationMatch指令过滤器的一部分。

   >[!NOTE]
   >其他方法(包括[dispatcher-ttl AEM ACS Commons项目](https://adobe-consulting-services.github.io/acs-aem-commons/features/dispatcher-ttl/))将无法成功覆盖值。

### 节点存储{#other-content}中的其他内容文件类型

* 无默认缓存
* 不能使用用于html/text文件类型的`EXPIRATION_TIME`变量设置default
* 可通过指定适当的正则表达式，使用html/text部分中描述的相同LocationMatch策略设置缓存过期

## 调度程序缓存失效{#disp}

通常，调度程序缓存无需失效。 相反，当内容重新发布时，应依赖调度程序刷新其缓存，并依赖有缓存过期标头的CDN。

### 激活/取消激活{#cache-activation-deactivation}期间调度程序缓存失效

与先前版本的AEM一样，发布或取消发布页面将从调度程序缓存中清除内容。 如果怀疑存在缓存问题，客户应重新发布相关页面。

当发布实例从作者处收到页面或资产的新版本时，它使用刷新代理使其调度程序上的适当路径失效。 更新的路径将从调度程序缓存及其父缓存中删除，最高可达一个级别（您可以使用[statfilelevel](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#invalidating-files-by-folder-level)配置该级别）。

### 显式调度程序缓存失效{#explicit-invalidation}

通常，不必手动使调度程序中的内容失效，但如果需要，可以这样做，如下所述。

在AEM作为Cloud Service之前，有两种方法会使调度程序缓存失效。

1. 调用复制代理，指定发布调度程序刷新代理
2. 直接调用`invalidate.cache` API（例如`POST /dispatcher/invalidate.cache`）

不再支持调度程序的`invalidate.cache` API方法，因为它只针对特定的调度程序节点。 AEM作为Cloud Service在服务级别运行，而不是单个节点级别运行，因此，对于AEM作为Cloud Service,[“从AEM](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/page-invalidate.html)中取消缓存页面的失效说明不再有效。
而应使用复制刷新代理。 这可以使用复制API完成。 复制API文档可在[此处](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/replication/Replicator.html)找到，有关刷新缓存的示例，请参见[ API示例页](https://helpx.adobe.com/experience-manager/using/aem64_replication_api.html)，具体是向所有可用代理发出类型为ACTIVATE的复制操作的`CustomStep`示例。 无法配置刷新代理端点，但已预先配置为指向调度程序，与运行刷新代理的发布服务匹配。 刷新代理通常可以由OSGi事件或工作流触发。

下图说明了这一点。

![](assets/cdnd.png "CDNCDN")

如果担心调度程序缓存未清除，请联系[客户支持](https://helpx.adobe.com/support.ec.html)，如有必要，可以刷新调度程序缓存。

由Adobe管理的CDN会遵守TTL，因此无需刷新它。 如果怀疑存在问题，请[联系可根据需要刷新Adobe管理的CDN缓存的客户支持](https://helpx.adobe.com/support.ec.html)支持人员。

## 客户端库和版本一致性{#content-consistency}

页面由HTML、Javascript、CSS和图像组成。 鼓励客户利用[客户端库(clientlibs)框架](/help/implementing/developing/introduction/clientlibs.md)将Javascript和CSS资源导入HTML页面，同时考虑到JS库之间的依赖关系。

clientlibs框架提供自动版本管理，这意味着开发人员可以通过源代码控制签入对JS库的更改，并且当客户推送其版本时，将提供最新版本。 如果没有此选项，开发人员需要手动更改引用了新版本库的HTML，如果许多HTML模板共享同一库，这尤其繁琐。

将新版本的库发布到生产版本后，引用HTML页面会更新，其中包含指向那些已更新库版本的新链接。 在给定HTML页的浏览器缓存过期后，不会担心旧库会从浏览器缓存中加载，因为现在(从AEM)刷新的页面可以引用新版本的库。 换言之，刷新的HTML页面将包含所有最新的库版本。

这种机制是序列化哈希，附加到客户端库链接，确保浏览器有一个唯一的版本化URL来缓存CSS/JS。 序列化哈希仅在客户端库的内容发生更改时更新。 这意味着，即使在新部署时也会发生不相关的更新（即对客户端库的基础css/js没有更改），引用也保持不变，确保减少对浏览器缓存的中断。

### 启用客户端库的长缓存版本 — AEM作为Cloud ServiceSDK快速启动{#enabling-longcache}

HTML页面上的默认clientlib如下例所示：

```
<link rel="stylesheet" href="/etc.clientlibs/wkndapp/clientlibs/clientlib-base.css" type="text/css">
```

启用严格clientlib版本控制后，会将长期哈希键作为选择器添加到客户端库。 因此，clientlib引用如下所示：

```
<link rel="stylesheet" href="/etc.clientlibs/wkndapp/clientlibs/clientlib-base.lc-7c8c5d228445ff48ab49a8e3c865c562-lc.css" type="text/css">
```

默认情况下，所有AEM中都启用严格的clientlib版本控制作为Cloud Service环境。

要在本地SDK快速启动中启用严格的clientlib版本控制，请执行以下操作：

1. 导航到OSGi Configuration Manager `<host>/system/console/configMgr`
1. 查找Adobe Granite HTML库管理器的OSGi配置：
   * 选中此复选框可启用严格版本控制
   * 在标记为“长期客户端缓存键”的字段中，输入值/。*
1. 保存更改。请注意，不必在源代码管理中保存此配置，因为AEM作为Cloud Service将在开发、舞台和生产环境中自动启用此配置。
1. 每当客户端库的内容发生更改时，都会生成新的哈希键，并更新HTML引用。
