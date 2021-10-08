---
title: AEM as a Cloud Service 中的缓存
description: 'AEM as a Cloud Service 中的缓存 '
feature: Dispatcher
exl-id: 4206abd1-d669-4f7d-8ff4-8980d12be9d6
source-git-commit: c08e442e58a4ff36e89a213aa7b297b538ae3bab
workflow-type: tm+mt
source-wordcount: '1572'
ht-degree: 1%

---

# 简介 {#intro}

流量会通过CDN传递到Apache Web服务器层，该层支持包括调度程序在内的模块。 为了提高性能，调度程序主要用作缓存以限制发布节点上的处理。
可以将规则应用于调度程序配置以修改任何默认的缓存过期设置，从而导致在CDN上缓存。 请注意，如果调度程序配置中启用了`enableTTL`，则调度程序还会遵循生成的缓存过期标头，这意味着即使在重新发布的内容之外，它也会刷新特定内容。

本页还介绍调度程序缓存如何失效，以及缓存在浏览器级别与客户端库有关的工作方式。

## 缓存 {#caching}

### HTML/文本 {#html-text}

* 默认情况下，会根据apache层发出的`cache-control`标头，由浏览器缓存五分钟。 CDN还尊重此价值。
* 可通过在`global.vars`中定义`DISABLE_DEFAULT_CACHING`变量来禁用默认HTML/文本缓存设置：

```
Define DISABLE_DEFAULT_CACHING
```

例如，当您的业务逻辑需要微调页面标题（其值基于日历日）时，这非常有用，因为默认情况下，页面标题设置为0。 也就是说，在关闭默认缓存时，请务必谨慎。****

* 可以通过使用AEMas a Cloud ServiceSDK Dispatcher工具在`global.vars`中定义`EXPIRATION_TIME`变量来覆盖所有HTML/文本内容。
* 可以由以下apache mod_headers指令在更细粒度级别上覆盖：

   ```
   <LocationMatch "^/content/.*\.(html)$">
        Header set Cache-Control "max-age=200"
        Header set Age 0
   </LocationMatch>
   ```

   在设置全局缓存控制标头或与宽正则表达式匹配的标头时，请务必谨慎，以便这些标头不会应用于您可能打算保留为私有的内容。 请考虑使用多个指令，以确保以细粒度方式应用规则。 根据上述说明，如果AEM as a Cloud Service检测到已将缓存标头应用于Dispatcher检测到的不可执行的内容，则它将删除该缓存标头，如Dispatcher文档中所述。 为了强制AEM始终应用缓存标头，可以添加&#x200B;**always**&#x200B;选项，如下所示：

   ```
   <LocationMatch "^/content/.*\.(html)$">
        Header unset Cache-Control
        Header unset Expires
        Header always set Cache-Control "max-age=200"
        Header set Age 0
   </LocationMatch>
   ```

   必须确保`src/conf.dispatcher.d/cache`下的文件具有以下规则（默认配置中为）：

   ```
   /0000
   { /glob "*" /type "allow" }
   ```

* 要防止特定内容在CDN **上缓存**，请将Cache-Control标头设置为&#x200B;*private*。 例如，以下内容会阻止将名为&#x200B;**secure**&#x200B;的目录下的html内容缓存到CDN中：

   ```
      <LocationMatch "/content/secure/.*\.(html)$">.  // replace with the right regex
      Header unset Cache-Control
      Header unset Expires
      Header always set Cache-Control “private”
     </LocationMatch>
   ```

   >[!NOTE]
   >其他方法(包括[dispatcher-ttl AEM ACS Commons项目](https://adobe-consulting-services.github.io/acs-aem-commons/features/dispatcher-ttl/))将无法成功覆盖值。

   >[!NOTE]
   >请注意，调度程序可能仍会根据其自己的[缓存规则](https://helpx.adobe.com/experience-manager/kb/find-out-which-requests-does-aem-dispatcher-cache.html)来缓存内容。 要使内容真正私有，您应确保dispatcher不会缓存该内容。

### 客户端库(js，css) {#client-side-libraries}

* 通过使用AEM客户端库框架，可以生成JavaScript和CSS代码，以便浏览器可以无限期地缓存它，因为任何更改都将显示为具有唯一路径的新文件。  换言之，将根据需要生成引用客户端库的HTML，以便客户在发布新内容时能够体验到新内容。 对于不遵循“不可变”值的旧版浏览器，缓存控制将设置为“不可变”或30天。
* 有关更多详细信息，请参阅[客户端库和版本一致性](#content-consistency)部分。

### 图像和任何存储在blob存储中且足够大的内容 {#images}

* 默认情况下，未缓存
* 可以通过以下apache `mod_headers`指令在更细粒度级别进行设置：

   ```
      <LocationMatch "^/content/.*\.(jpeg|jpg)$">
        Header set Cache-Control "max-age=222"
        Header set Age 0
      </LocationMatch>
   ```

   请参阅上面html/文本部分中的讨论，以了解如何谨慎避免缓存过于广泛，以及如何强制AEM始终使用“始终”选项应用缓存。

   必须确保`src/conf.dispatcher.d/`cache下的文件具有以下规则（默认配置中为）：

   ```
   /0000
   { /glob "*" /type "allow" }
   ```

   确保要保留为私有而非缓存的资产未包含在LocationMatch指令筛选器中。

   >[!NOTE]
   >其他方法(包括[dispatcher-ttl AEM ACS Commons项目](https://adobe-consulting-services.github.io/acs-aem-commons/features/dispatcher-ttl/))将无法成功覆盖值。

### 节点存储中的其他内容文件类型 {#other-content}

* 无默认缓存
* 默认值不能使用用于html/文本文件类型的`EXPIRATION_TIME`变量进行设置
* 可通过指定适当的正则表达式，使用html/text部分中描述的相同LocationMatch策略来设置缓存过期

## 调度程序缓存失效 {#disp}

通常，不必使调度程序缓存失效。 相反，在重新发布内容时，您应该依赖调度程序刷新其缓存，并依赖CDN遵守缓存过期标头。

### 在激活/停用期间使调度程序缓存失效 {#cache-activation-deactivation}

与AEM的先前版本一样，发布或取消发布页面将从调度程序缓存中清除内容。 如果怀疑存在缓存问题，客户应重新发布相关页面。

当发布实例收到作者提供的页面或资产的新版本时，它会使用刷新代理使其调度程序上的相应路径失效。 更新的路径会从调度程序缓存及其父缓存中删除，最高级别为（您可以使用[statfileslevel](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#invalidating-files-by-folder-level)配置此路径）。

### 显式调度程序缓存失效 {#explicit-invalidation}

通常，不需要手动使调度程序中的内容失效，但如果需要，可以执行此操作，如下所述。

在AEMas a Cloud Service之前，有两种方法可使调度程序缓存失效。

1. 调用复制代理，指定发布调度程序刷新代理
2. 直接调用`invalidate.cache` API（例如`POST /dispatcher/invalidate.cache`）

不再支持调度程序的`invalidate.cache` API方法，因为它只处理特定的调度程序节点。 AEMas a Cloud Service在服务级别运行，而不是在单个节点级别运行，因此[从AEM](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/page-invalidate.html)页中使缓存页面失效的失效说明对AEMas a Cloud Service不再有效。
而应使用复制刷新代理。 可以使用复制API完成此操作。 [此处](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/replication/Replicator.html)提供了复制API文档，有关刷新缓存的示例，请参阅[ API示例页面](https://helpx.adobe.com/experience-manager/using/aem64_replication_api.html)，具体是`CustomStep`向所有可用代理发布类型为ACTIVATE的复制操作示例。 无法配置刷新代理端点，但已预配置为指向与运行刷新代理的发布服务匹配的调度程序。 刷新代理通常可以由OSGi事件或工作流触发。

下图说明了这一点。

![](assets/cdnd.png "CDNCDN")

如果担心调度程序缓存未清除，请联系[客户支持](https://helpx.adobe.com/support.ec.html)，如有必要，可以刷新调度程序缓存。

Adobe管理的CDN遵循TTL，因此无需刷新。 如果怀疑存在问题，请[联系可根据需要刷新Adobe管理的CDN缓存的客户支持](https://helpx.adobe.com/support.ec.html)支持人员。

## 客户端库和版本一致性 {#content-consistency}

页面由HTML、Javascript、CSS和图像组成。 我们鼓励客户利用[客户端库(clientlibs)框架](/help/implementing/developing/introduction/clientlibs.md)将Javascript和CSS资源导入HTML页面，同时考虑JS库之间的依赖关系。

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

1. 导航到OSGi配置管理器`<host>/system/console/configMgr`
1. 找到AdobeGraniteHTML库管理器的OSGi配置：
   * 选中此复选框可启用严格版本控制
   * 在标记为长期客户端缓存键的字段中，输入值/。*；哈希
1. 保存更改。请注意，无需在源代码管理中保存此配置，因为AEMas a Cloud Service将在开发、暂存和生产环境中自动启用此配置。
1. 每当客户端库的内容发生更改时，都会生成一个新的哈希键，并且HTML引用将会更新。
