---
title: AEM as a Cloud Service 中的 CDN
description: AEM as a Cloud Service 中的 CDN
feature: Dispatcher
exl-id: a3f66d99-1b9a-4f74-90e5-2cad50dc345a
translation-type: tm+mt
source-git-commit: f6c700f82bc5a1a3edf05911a29a6e4d32dd3f72
workflow-type: tm+mt
source-wordcount: '808'
ht-degree: 9%

---

# AEM as a Cloud Service 中的 CDN {#cdn}


>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_cdn"
>title="AEM as a Cloud Service 中的 CDN"
>abstract="AEM as Cloud Service随内置CDN提供。 其主要目的是通过从位于浏览器边缘的CDN节点传送可缓存内容来减少延迟。 它经过全面的管理和配置，可提供最佳的 AEM 应用程序性能。"

AEM as Cloud Service随内置CDN提供。 其主要目的是通过从浏览器附近的边缘 CDN 节点提供可缓存的内容来减少延迟。它经过全面的管理和配置，可提供最佳的 AEM 应用程序性能。


AEM托管CDN将满足大多数客户的性能和安全要求。 对于发布层，客户可以选择从自己的CDN指向它，他们需要管理它。 这将基于满足某些先决条件（包括但不限于客户与其CDN供应商的旧版集成很难放弃）而允许，逐个案例进行。

## AEM Managed CDN {#aem-managed-cdn}

请按照以下部分使用Cloud Manager自助服务UI，准备使用AEM现成的CDN进行内容投放:

1. [管理SSL证书](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md)
1. [管理自定义域名](/help/implementing/cloud-manager/custom-domain-names/introduction.md)

**限制流量**

默认情况下，对于AEM托管CDN设置，所有公共流量都可用于生产和非生产（开发和阶段）环境的发布服务。 如果您希望限制特定环境的发布服务通信量（例如，按IP地址范围限制暂存），则可以通过Cloud Manager UI以自助方式执行此操作。

请参阅[管理IP允许列表](/help/implementing/cloud-manager/ip-allow-lists/introduction.md)以了解更多信息。

>[!CAUTION]
>
>只有来自允许IP的请求才能由AEM托管CDN提供。 如果将您自己的CDN指向AEM托管的CDN，则确保您的CDN的IP包含在允许列表中。

## 客户CDN指向AEM Managed CDN {#point-to-point-CDN}

如果客户必须使用其现有CDN，他们可以管理CDN并将其指向AEM托管CDN，只要满足以下条件：

* 客户必须拥有一个需要更换的现有CDN。
* 客户必须管理它。
* 客户必须能够配置CDN以将AEM作为Cloud Service使用 — 请参阅下面的配置说明。
* 客户必须拥有随时待命的工程CDN专家，以防出现相关问题。
* 客户必须执行并成功通过负载测试，然后才能投产。

配置说明：

1. 使用域名设置`X-Forwarded-Host`头。 例如：`X-Forwarded-Host:example.com`。
1. 将主机头设置为来源域，即AEM CDN的入口。 例如：`Host:publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com`。
1. 将SNI头发送到来源。 与主机头一样， SNI头必须是来源域。
1. 设置`X-Edge-Key`或`X-AEM-Edge-Key`（如果CDN去除`X-Edge-*`）。 值应来自Adobe。
   * 这是为了使Adobe CDN能够验证请求源并将`X-Forwarded-*`标头传递到AEM应用程序而必需的。 例如，AEM使用`X-Forwarded-Host`确定主机头，使用`X-Forwarded-For`确定客户端IP。 因此，由受信任的呼叫者（即客户管理的CDN）负责确保`X-Forwarded-*`标头的正确性（请参阅下面的说明）。
   * 或者，当`X-Edge-Key`不存在时，可以阻止访问Adobe CDN的入口。 如果您需要直接访问Adobe CDN的入口（要阻止），请通知Adobe。

在接受实时流量之前，您应向Adobe的客户支持确认端到端流量路由是否正常运行。

>[!NOTE]
>
>管理自己的CDN的客户应确保发送到AEM CDN的头的完整性。 例如，建议客户清除所有`X-Forwarded-*`标头，并将其设置为已知和受控值。 例如，`X-Forwarded-For`应包含客户端的IP地址，而`X-Forwarded-Host`应包含站点的主机。

由于额外的跃点，性能可能会受到很小的影响，但从客户CDN到AEM托管CDN的跃点可能会很高效。

请注意，发布层支持此客户CDN配置，但创作层不支持。

## 地理位置标头{#geo-headers}

AEM托管CDN可通过以下方式将标头添加到每个请求：

* 国家/地区代码：`x-aem-client-country`
* 大陆代码：`x-aem-client-continent`

国家代码的值是[此处](https://en.wikipedia.org/wiki/ISO_3166-1)描述的Alpha-2代码。

大陆代码的值为：

* AF非洲
* 南极洲
* AS亚洲
* 欧盟
* 北美
* 大洋洲
* SA南美洲

此信息对于根据请求的来源（国家）重定向到其他url等用例可能很有用。 使用Vary头缓存取决于地理信息的响应。 例如，重定向到特定国家/地区的登陆页应始终包含`Vary: x-aem-client-country`。 如果需要，您可以使用`Cache-Control: private`来阻止缓存。 另请参阅[缓存](/help/implementing/dispatcher/caching.md#html-text)。
