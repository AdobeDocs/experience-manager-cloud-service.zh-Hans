---
title: AEM as a Cloud Service 中的 CDN
description: AEM as a Cloud Service 中的 CDN
feature: Dispatcher
exl-id: a3f66d99-1b9a-4f74-90e5-2cad50dc345a
source-git-commit: 98eff568686c72c626d2bf77d82e8c3f224eda42
workflow-type: tm+mt
source-wordcount: '1023'
ht-degree: 15%

---

# AEM as a Cloud Service 中的 CDN {#cdn}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_cdn"
>title="AEM as a Cloud Service 中的 CDN"
>abstract="AEM as a Cloud Service 随附一个内置 CDN。其主要目的是通过从浏览器附近的边缘 CDN 节点提供可缓存的内容来减少延迟。它经过全面的管理和配置，可提供最佳的 AEM 应用程序性能。"

AEM as a Cloud Service 随附一个内置 CDN。其主要目的是通过从浏览器附近的边缘 CDN 节点提供可缓存的内容来减少延迟。它经过全面的管理和配置，可提供最佳的 AEM 应用程序性能。

AEM管理的CDN可满足大多数客户的性能和安全要求。 对于发布层，客户可以选择从自己的CDN指向它，他们必须管理CDN。 根据满足某些先决条件（包括但不限于客户与其CDN供应商的旧版集成很难放弃）的情况，允许逐个执行此方案。

<!-- ERROR: NEITHER URL IS FOUND (HTTP ERROR 404) Also, see the following videos [Cloud 5 AEM CDN Part 1](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-5/cloud5-aem-cdn-part1.html) and [Cloud 5 AEM CDN Part 2](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-5/cloud5-aem-cdn-part2.html) for additional information about CDN in AEM as a Cloud Service. -->

## AEM-managed CDN  {#aem-managed-cdn}

请按照以下部分，使用Cloud Manager自助服务UI，通过现成的CDN为内容交付做好准备：

1. [管理 SSL 证书](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md)
1. [管理自定义域名](/help/implementing/cloud-manager/custom-domain-names/introduction.md)

**限制流量**

默认情况下，对于AEM管理的CDN设置，所有公共流量都可以进入生产环境和非生产（开发和暂存）环境的发布服务。 您可以通过Cloud Manager用户界面限制给定环境的发布服务的流量（例如，限制IP地址范围的暂存）。

请参阅[管理 IP 允许列表](/help/implementing/cloud-manager/ip-allow-lists/introduction.md)了解详情。

>[!CAUTION]
>
>只有来自允许IP的请求才由AEM托管CDN提供。 如果您将自己的CDN指向AEM管理的CDN，请确保将CDN的IP包含在允许列表该中。

## 客户CDN指向AEM-Managed CDN {#point-to-point-CDN}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_byocdn"
>title="客户 CDN 指向 AEM 托管 CDN"
>abstract="AEM as a Cloud Service 为客户提供了使用现有 CDN 的选项。对于发布层，客户可以选择从自己的CDN指向它，他们必须管理CDN。 根据满足某些先决条件（包括但不限于客户与其CDN供应商的旧版集成很难放弃）的情况，允许逐个执行此方案。"

如果客户必须使用其现有的CDN，则他们可以管理CDN并将其指向AEM管理的CDN，从而满足以下要求：

* 客户必须拥有现有的CDN，这样的CDN更换将非常繁琐。
* 客户必须管理它。
* 客户必须能够配置CDN以使用AEMas a Cloud Service — 请参阅下面提供的配置说明。
* 客户必须有工程CDN专家随时待命，以防出现与案例相关的问题。
* 客户必须先执行并成功通过负载测试，然后才能转到生产环境。

配置说明：

1. 将您的CDN指向AdobeCDN的入口作为其源域。 例如：`publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com`。
1. 将SNI设置为AdobeCDN的入口。
1. 将主机标头设置为源域。 例如：`Host:publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com`。
1. 设置 `X-Forwarded-Host` 标头，以便AEM可以确定主机标头。 例如：`X-Forwarded-Host:example.com`。
1. 套 `X-AEM-Edge-Key`. 值应来自Adobe。

   * 需要，以便AdobeCDN能够验证请求源并传递 `X-Forwarded-*` 标头。 例如，`X-Forwarded-For` 用于确定客户端IP。 因此，它成为可信呼叫者（即客户管理的CDN）的责任，来确保 `X-Forwarded-*` 标题（请参阅下面的注释）。
   * 或者，当Adobe `X-AEM-Edge-Key` 不存在。 如果您需要直接访问AdobeCDN的入口（待阻止），请通知Adobe。

请参阅 [示例CDN供应商配置](#sample-configurations) 部分，以了解领先CDN供应商的配置示例。

在接受实时流量之前，您应该通过Adobe的客户支持验证端到端流量路由是否正确运行。

获取 `X-AEM-Edge-Key`，则可以测试请求是否按如下方式正确路由。

在Linux®中：

```
curl https://publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com -H "X-Forwarded-Host: example.com" -H "X-AEM-Edge-Key: <PROVIDED_EDGE_KEY>"
```

在Windows中：

```
curl https://publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com --header "X-Forwarded-Host: example.com" --header "X-AEM-Edge-Key: <PROVIDED_EDGE_KEY>"
```

>[!NOTE]
>
>使用您自己的CDN时，无需在Cloud Manager中安装域和证书。 AdobeCDN中的路由是使用默认域完成的 `publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com` 应在请求中发送 `Host` 标题。 覆盖请求 `Host` 具有自定义域名的标头可能会导致AdobeCDN错误地路由请求。


>[!NOTE]
>
>管理自己CDN的客户应确保发送到AEM CDN的标头的完整性。 例如，建议客户清除所有 `X-Forwarded-*` 标头，并将其设置为已知和受控值。 例如， `X-Forwarded-For` 应包含客户端的IP地址，而 `X-Forwarded-Host` 应包含网站的主机。

>[!NOTE]
>
>沙盒项目环境不支持客户提供的CDN。

仅当存在缓存缺失时，才需要在客户CDN和AEM CDN之间额外跳转。 通过使用本文中描述的缓存优化策略，添加客户CDN只会引入可忽略的延迟。

发布层支持此客户CDN配置，但创作层不支持此配置。

### 示例CDN供应商配置 {#sample-configurations}

以下是一些领先CDN供应商提供的几个配置示例。

**Akamai**

![Akamai1](assets/akamai1.png "Akamai")
![Akamai2](assets/akamai2.png "Akamai")

**Amazon CloudFront**

![CloudFront1](assets/cloudfront1.png "Amazon CloudFront")
![CloudFront2](assets/cloudfront2.png "Amazon CloudFront")

**Cloudflare**

![Cloudflare1](assets/cloudflare1.png "Cloudflare")
![Cloudflare2](assets/cloudflare2.png "Cloudflare")

## 地理位置标题 {#geo-headers}

AEM-managed CDN会通过以下方式向每个请求添加标头：

* 国家/地区代码： `x-aem-client-country`
* 大陆代码： `x-aem-client-continent`

>[!NOTE]
>
>如果存在由客户管理的CDN，则这些标头将反映客户CDN代理服务器的位置，而不是实际的客户端。 因此，对于客户管理的CDN，地理位置标头应由客户CDN管理。

国家/地区代码的值是所述的Alpha-2代码 [此处](https://en.wikipedia.org/wiki/ISO_3166-1).

大陆代码的值包括：

* 非洲联盟
* 南极洲
* AS亚洲
* 欧盟
* 北美洲
* 大洋州奥克
* 南美洲

此信息可能对以下用例有用：根据请求的来源（国家/地区）重定向到其他url。 使用Vary标头来缓存依赖于地理信息的响应。 例如，重定向到特定国家/地区登录页面时应始终包含 `Vary: x-aem-client-country`. 如果需要，您可以使用 `Cache-Control: private` 以防止缓存。 另请参阅 [缓存](/help/implementing/dispatcher/caching.md#html-text).
