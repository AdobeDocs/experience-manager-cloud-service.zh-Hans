---
title: 内容投放
description: '内容投放 '
translation-type: tm+mt
source-git-commit: a07de761dd9aedb3469f256e08ecf05b2102889d
workflow-type: tm+mt
source-wordcount: '2268'
ht-degree: 1%

---


# AEM 云服务中的内容交付 {#content-delivery}

当前页面详细信息将AEM中的服务内容投放作为云服务发布。 发布服务内容投放包括：

* CDN（通常由Adobe管理）
* AEM调度程序
* AEM发布

数据流如下：

1. URL将添加到浏览器中
1. 向DNS中映射到该域的CDN发出请求
1. 如果内容已在CDN上完全缓存，CDN会将其提供给浏览器
1. 如果内容未完全缓存，CDN将向调度程序发出（反向代理）调用
1. 如果内容已完全缓存在调度程序上，调度程序会将其提供给CDN
1. 如果内容未完全缓存，调度程序将调用（反向代理）AEM发布
1. 内容由浏览器呈现，浏览器也可缓存它，具体取决于标题

内容类型HTML/文本设置为在调度程序层300秒（5分钟）后过期，该阈值与调度程序缓存和CDN均相关。 在发布服务的重新部署期间，将清除调度程序缓存，然后在新发布节点接受通信之前预热。

以下各节提供有关内容投放（包括CDN配置和缓存）的更详细信息。

有关从作者服务复制到发布服务的信息，请在此 [处获取](/help/operations/replication.md)。

## CDN {#cdn}

AEM as Cloud Service随内置CDN提供。 其主要目的是通过从位于边缘、靠近浏览器的CDN节点传送可缓存内容来减少延迟。 它经过全面的管理和配置，可提供最佳的 AEM 应用程序性能。

总而言之，AEM优惠了两个选项：

1. AEM Managed CDN - AEM现成的CDN。 它是一个紧密集成的选项，在支持CDN与AEM集成方面不需要客户大量投资。
1. 客户管理的CDN指向AEM Managed CDN —— 客户将自己的CDN指向AEM现成的CDN。 客户仍需要管理自己的CDN，但与AEM集成的投资相当有限。

第一个选项应满足大多数客户性能和安全性要求。 此外，它还需要最少的客户工作。

第二个选项将逐个允许。 此决定基于满足某些先决条件，包括但不限于客户与其CDN供应商进行难以放弃的旧式集成。

下面是比较两个选项的决策矩阵。 有关更多详细信息，请参阅后面的部分。

| 详细信息 | AEM Managed CDN | 客户管理的CDN指向AEM CDN |
|---|---|---|
| **客户工作** | 没有，完全集成。 只需将CNAME指向AEM Managed CDN。 | 适中的客户投资。 客户必须管理自己的CDN。 |
| **先决条件** | 无 | 现有的CDN需要更换。 上线前必须演示成功的负载测试。 |
| **CDN专业知识** | 无 | 至少需要一个兼职的工程资源，具备能够配置客户CDN的详细CDN知识。 |
| **安全** | 由 Adobe 管理. | 由Adobe（或由客户在自己的CDN进行管理）管理。 |
| **演出** | 由Adobe优化。 | 将从某些AEM CDN功能中受益，但由于额外的跳数，性能可能会受到较小的影响。 **注意**: 从客户CDN到Adobe开箱即用CDN的跃进可能非常有效)。 |
| **缓存** | 支持在调度程序上应用的缓存头。 | 支持在调度程序上应用的缓存头。 |
| **图像和视频压缩功能** | 可以与Adobe Dynamic Media一起使用。 | 可以与Adobe Dynamic Media或客户管理的CDN图像／视频解决方案配合使用。 |

### AEM Managed CDN  {#aem-managed-cdn}

使用Adobe现成的CDN准备内容投放很简单，如下所述：

1. 您将通过共享指向包含此信息的安全表单的链接，向Adobe提供已签名的SSL证书和密钥。 请在此任务与客户支持协作。
   **注意：** Aem作为云服务不支持域验证(DV)证书。
1. 您应通知客户支持：
   * 哪个自定义域应与给定环境关联，如项目id和环境id所定义。
   * 如果需要任何IP白名单来限制到给定环境的通信。
1. 然后，客户支持将与您协调CNAME DNS记录的时间，并将其FQDN指向 `cdn.adobeaemcloud.com`。
1. 当SSL证书过期时，将通知您，这样您就可以重新提交新的SSL证书。

**限制流量**

默认情况下，对于Adobe Managed CDN设置，所有公共流量都可用于生产和非生产（开发和阶段）环境的发布服务。 如果希望限制特定环境发布服务的通信量（例如，限制按IP地址范围进行分阶段），应与客户支持合作配置这些限制。

### 客户CDN指向AEM Managed CDN {#point-to-point-CDN}

如果您希望使用现有CDN，但无法满足客户管理的CDN的要求，则支持此功能。 在这种情况下，您可以管理自己的CDN，但可以指向Adobe的托管CDN。

请注意：

1. 您必须拥有现有CDN。
1. 你必须管理它。
1. 您必须能够配置CDN以将Aem作为云服务使用——请参阅下面的配置说明。
1. 如果出现相关问题，您必须有随时待命的工程CDN专家。
1. 必须先执行并成功通过负载测试，然后才能投入生产。

配置说明：

1. 使用 `X-Forwarded-Host` 域名设置头。
1. 将主机头与来源域（即Adobe CDN的入口）一起设置。 价值应来自Adobe。
1. 将SNI头发送到来源。 与主机头一样， sni头必须是来源域。
1. 设置 `X-Edge-Key`将流量正确路由到AEM服务器所需的流量。 价值应来自Adobe。

在接受实时流量之前，您应向Adobe客户支持确认端对端流量路由是否工作正常。

## 缓存 {#caching}

可以使用调度程序规则配置CDN上的缓存。 请注意，如果在调度程序配置中启用，调度程序 `enableTTL` 还会考虑生成的缓存过期标头，这意味着即使在重新发布的内容之外，它也会刷新特定内容。

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

* 请注意，其他方法( [包括dispatcher-ttl AEM ACS Commons项目](https://adobe-consulting-services.github.io/acs-aem-commons/features/dispatcher-ttl/))将无法成功覆盖值。

### 客户端库(js、css) {#client-side-libraries}

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

## Dispatcher {#disp}

流量通过apache Web服务器，它支持包括调度程序的模块。 调度程序主要用作缓存，以限制对发布节点的处理，以提高性能。

如CDN的缓存部分所述，可以将规则应用于调度程序配置以修改任何默认缓存过期设置。

本节的其余部分介绍了与调度程序缓存失效相关的注意事项。 对于大多数客户而言，不必使调度程序缓存失效，而是依赖调度程序在内容被重新发布时刷新其缓存，以及与缓存过期头相关的CDN。

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

clientlibs框架提供自动版本管理，这意味着开发人员可以通过源代码控制检入对JS库的更改，并且当客户推送其版本时，将提供最新版本。 如果没有这一功能，开发人员将需要手动更改引用了新版本库的HTML，如果许多HTML模板共享同一库，这将特别困难。

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
