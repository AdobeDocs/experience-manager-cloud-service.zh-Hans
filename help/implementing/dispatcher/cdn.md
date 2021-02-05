---
title: AEM as a Cloud Service 中的 CDN
description: AEM as a Cloud Service 中的 CDN
translation-type: tm+mt
source-git-commit: b6ae5cab872a3cca4eb41259f6c242b1fbeb98bb
workflow-type: tm+mt
source-wordcount: '604'
ht-degree: 5%

---


# AEM as a Cloud Service 中的 CDN {#cdn}

AEM asCloud Service随内置CDN一起提供。 其主要目的是通过从位于边缘、靠近浏览器的CDN节点传送可缓存内容来减少延迟。 它经过全面的管理和配置，可提供最佳的 AEM 应用程序性能。

AEM托管CDN将满足大多数客户的性能和安全要求。 对于发布层，客户可以选择从自己的CDN指向它，他们需要管理它。 根据满足某些先决条件（包括但不限于客户与其CDN供应商进行难以放弃的旧式集成），将允许按个例执行此操作。

## AEM Managed CDN {#aem-managed-cdn}

请按照以下部分使用Cloud Manager自助UI，使用Adobe现成的CDN准备内容投放:

1. [管理SSL证书](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md)
1. [管理自定义域名](/help/implementing/cloud-manager/custom-domain-names/introduction.md)

**限制流量**

默认情况下，对于Adobe管理的CDN设置，所有公共流量都可用于生产和非生产（开发和阶段）环境的发布服务。 如果您希望限制特定环境发布服务的流量（例如，按IP地址范围限制暂存），则可以通过云管理器UI以自助方式执行此操作。

请参阅[管理IP允许列表](/help/implementing/cloud-manager/ip-allow-lists/introduction.md)以了解更多信息。

>[!CAUTION]
>
>只有AEM的托管CDN提供来自允许IP的请求。 如果将您自己的CDN指向AEM托管的CDN，则确保您的CDN的IP包含在允许列表中。

## 客户CDN指向AEM Managed CDN {#point-to-point-CDN}

如果客户必须使用其现有CDN，则可以管理它并将其指向Adobe的托管CDN，只要满足以下条件：

* 客户必须拥有一个需要更换的现有CDN。
* 客户必须管理它。
* 客户必须能够配置CDN以将AEM作为Cloud Service使用——请参阅下面的配置说明。
* 客户必须拥有随时待命的工程CDN专家，以防出现相关问题。
* 客户必须执行并成功通过负载测试，然后才能投入生产。

配置说明：

1. 使用域名设置`X-Forwarded-Host`头。
1. 将主机头与来源域(即Adobe的CDN入口)一起设置。 值应来自Adobe。
1. 将SNI头发送到来源。 与主机头一样， sni头必须是来源域。
1. 设置`X-Edge-Key` ，它是将流量正确路由到AEM服务器所需的。 值应来自Adobe。

在接受实时流量之前，您应向Adobe客户支持确认端对端流量路由是否正常运行。

由于额外的跳数，可能会对性能造成很小的影响，但从客户CDN到Adobe托管CDN的跳数可能会很高效。

请注意，发布层支持此客户CDN配置，但创作层不支持此客户CDN配置。

## 地理位置标头{#geo-headers}

Adobe管理的CDN将通过以下方式向每个请求添加头：

* 国家／地区代码：`x-aem-client-country`
* 大陆代码：`x-aem-client-continent`

国家代码的值是[此处](https://en.wikipedia.org/wiki/ISO_3166-1)描述的Alpha-2代码。

大陆代码的值为：

* AF非洲
* 南极洲
* AS亚洲
* 欧盟
* 北美
* 大洋洲OC
* SA南美洲

此信息对于根据请求的来源（国家）重定向到其他url等用例可能非常有用。 但是，在此特定用例中，不应缓存重定向，因为它会有所不同。 如果需要，可以使用`Cache-Control: private`阻止缓存。 另请参阅[缓存](/help/implementing/dispatcher/caching.md#html-text)。
