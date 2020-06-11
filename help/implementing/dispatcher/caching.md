---
title: 在AEM中缓存为云服务
description: '在AEM中缓存为云服务 '
translation-type: tm+mt
source-git-commit: 18c2f70acd33c83a0d98ccb658d3e9be18b34c8b
workflow-type: tm+mt
source-wordcount: '1358'
ht-degree: 0%

---


# 简介 {#intro}

流量通过CDN传递到apache Web服务器层，该层支持包括调度程序的模块。 为了提高性能，调度程序主要用作缓存以限制发布节点上的处理。
规则可应用于调度程序配置以修改任何默认缓存过期设置，从而在CDN上缓存。 请注意，如果在调度程序配置中启用，调 `enableTTL` 度程序还会考虑生成的缓存过期标头，这意味着即使在重新发布的内容之外，它也会刷新特定内容。

本页还描述了调度程序缓存失效的方式，以及在浏览器级别上对客户端库的缓存工作方式。

## 缓存 {#caching}

### HTML/文本 {#html-text}

* 默认情况下，根据apache层发出的cache-control头，由浏览器缓存五分钟。 CDN还尊重此价值。
* 通过在将AEM用作云服务SDK调度程序工 `EXPIRATION_TIME` 具中 `global.vars` 定义变量，可覆盖所有HTML/文本内容。
* 可以由以下apache mod_headers指令在更细的粒度级别上覆盖：

```
<LocationMatch "\.(html)$">
        Header set Cache-Control "max-age=200"
</LocationMatch>
```

必须确保文件下 `src/conf.dispatcher.d/cache` 有以下规则（默认配置中）:

```
/0000
{ /glob "*" /type "allow" }
```

* 要阻止对特定内容进行缓存，请将Cache-Control头设置为“private”。 例如，以下操作将阻止缓存名为“myfolder”的目录下的html内容：

```
<LocationMatch "\/myfolder\/.*\.(html)$">.  // replace with the right regex
    Header set Cache-Control “private”
</LocationMatch>
```

* 请注意，其他方法( [包括dispatcher-ttl AEM ACS Commons项目](https://adobe-consulting-services.github.io/acs-aem-commons/features/dispatcher-ttl/))将无法成功覆盖值。

### 客户端库(js,css) {#client-side-libraries}

* 通过使用AEM的客户端库框架，JavaScript和CSS代码的生成方式使浏览器能够无限地缓存它，因为任何更改都以具有唯一路径的新文件的形式显示出来。  换言之，将根据需要生成引用客户端库的HTML，以便客户在发布新内容时体验新内容。 对于不尊重“不可变”值的旧版浏览器，缓存控件设置为“不可变”或30天。
* 有关更多详 [细信息，请参阅客户端库和版本一致性](#content-consistency) 一节。

### 图像和任何大到足以存储在blob存储中的内容 {#images}

* 默认情况下，未缓存
* 可以通过以下apache指令在更细的粒度级别 `mod_headers` 上设置：

```
<LocationMatch "^.*.jpeg$">
    Header set Cache-Control "max-age=222"
</LocationMatch>
```

必须确保src/conf.dispatcher.d/cache下的文件具有以下规则（默认配置中）:

```
/0000
{ /glob "*" /type "allow" }
```

确保要保持私有而非缓存的资源不是LocationMatch指令过滤器的一部分。

* 请注意，其他方法( [包括dispatcher-ttl AEM ACS Commons项目](https://adobe-consulting-services.github.io/acs-aem-commons/features/dispatcher-ttl/))将无法成功覆盖值。

### 节点存储中的其他内容文件类型 {#other-content}

* 无默认缓存
* 默认值不能用用于html/ `EXPIRATION_TIME` 文本文件类型的变量设置
* 通过指定适当的正则表达式，可使用html/text部分中描述的相同LocationMatch策略设置缓存过期

## 调度程序缓存失效 {#disp}

通常，不必使调度程序缓存失效。 相反，当内容重新发布时，您应依赖调度程序刷新其缓存，而CDN则依赖于缓存过期标头。

### 激活/取消激活期间调度程序缓存失效 {#cache-activation-deactivation}

与先前版本的AEM一样，发布或取消发布页面将从调度程序缓存中清除内容。 如果怀疑存在缓存问题，客户应重新发布相关页面。

当发布实例从作者处收到页面或资产的新版本时，它使用刷新代理使其调度程序上的适当路径失效。 更新的路径将从调度程序缓存及其父缓存中删除，最高可达一个级别(您可以使用statfiles级别配 [置它](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#invalidating-files-by-folder-level)。

### 显式调度程序缓存失效 {#explicit-invalidation}

通常，不必手动使调度程序中的内容失效，但如果需要，可以这样做，如下所述。

在将AEM作为云服务之前，有两种方法可以使调度程序缓存失效。

1. 调用复制代理，指定发布调度程序刷新代理
2. 直接调 `invalidate.cache` 用API(例如 `POST /dispatcher/invalidate.cache`)

不再支持调 `invalidate.cache` 度程序的API方法，因为它只针对特定的调度程序节点。 AEM作为云服务在服务级别运行，而不是在单个节点级别运行，因此“从AEM中取消 [验证缓存页面](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/page-invalidate.html) ”页面中的失效说明对AEM作为云服务不再有效。
而应使用复制刷新代理。 这可以使用复制API完成。 此处提供复制API文 [档](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/replication/Replicator.html) ，有关刷新缓存的示例，请参见API示例页 [，具体是](https://helpx.adobe.com/experience-manager/using/aem64_replication_api.html)`CustomStep` 向所有可用代理发出ACTIVATE类型复制操作的示例。 刷新代理端点不可配置，但已预配置为指向调度程序，与运行刷新代理的发布服务匹配。 刷新代理通常可由OSGi事件或工作流触发。

下图说明了这一点。

![](assets/cdnd.png "CDNCDN")

如果担心调度程序缓存未清除，请联系客户支 [持人员](https://helpx.adobe.com/support.ec.html) ，如有必要，可以刷新调度程序缓存。

由Adobe管理的CDN尊重TTL，因此无需刷新它。 如果怀疑存在问题，请 [联系可以根据需要](https://helpx.adobe.com/support.ec.html) 刷新Adobe管理的CDN缓存的客户支持支持人员。

## 客户端库和版本一致性 {#content-consistency}

页面由HTML、Javascript、CSS和图像组成。 鼓励客户利用客户端库(clientlibs)框架将Javascript和CSS资源导入HTML页面，同时考虑JS库之间的相关性。

clientlibs框架提供自动版本管理，这意味着开发人员可以通过源代码控制检入对JS库的更改，并且当客户推送其版本时，将提供最新版本。 如果没有这一功能，开发人员需要手动更改引用了新版本库的HTML，如果许多HTML模板共享同一库，这尤其困难。

将新版库发布到生产版时，引用HTML页面会更新，其中包含指向这些已更新库版本的新链接。 在给定HTML页面的浏览器缓存过期后，不会担心旧库将从浏览器缓存中加载，因为现在保证刷新的页面（从AEM）引用新版本的库。 换言之，刷新的HTML页面将包括所有最新的库版本。

其机制是序列化哈希，附加到客户端库链接，确保浏览器有一个唯一的版本化URL来缓存CSS/JS。 序列化哈希仅在客户端库的内容发生更改时更新。 这意味着，即使在新部署时也会发生不相关的更新（即对客户端库的基础css/js没有更改），引用将保持不变，确保减少对浏览器缓存的中断。

### 启用客户端库的长缓存版本- AEM作为云服务SDK快速启动 {#enabling-longcache}

HTML页面上的默认clientlib如下所示：

```
<link rel="stylesheet" href="/etc.clientlibs/wkndapp/clientlibs/clientlib-base.css" type="text/css">
```

启用严格clientlib版本控制后，会将长期哈希键作为选择器添加到客户端库。 因此，clientlib引用如下所示：

```
<link rel="stylesheet" href="/etc.clientlibs/wkndapp/clientlibs/clientlib-base.lc-7c8c5d228445ff48ab49a8e3c865c562-lc.css" type="text/css">
```

在所有AEM中，默认情况下，严格clientlib版本控制都作为云服务环境启用。

要在本地SDK快速启动中启用严格的clientlib版本控制，请执行以下操作：

1. 导航到OSGi Configuration Manager `<host>/system/console/configMgr`
1. 查找Adobe Granite HTML Library Manager的OSGi配置：
   * 选中此复选框可启用严格版本控制
   * 在标记为“长期客户端缓存密钥”的字段中，输入值/。*；哈希
1. 保存更改。请注意，无需将此配置保存在源代码管理中，因为AEM将作为云服务自动在开发、暂存和生产环境中启用此配置。
1. 只要客户端库的内容发生更改，就会生成新的哈希键，并更新HTML引用。
