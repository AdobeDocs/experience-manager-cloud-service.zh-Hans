---
title: AEM as a Cloud Service 中的 CDN
description: AEM as a Cloud Service 中的 CDN
feature: Dispatcher
exl-id: a3f66d99-1b9a-4f74-90e5-2cad50dc345a
source-git-commit: 472a4311372ce9a01730f7ced6d4b26018aae4b9
workflow-type: tm+mt
source-wordcount: '993'
ht-degree: 8%

---

# AEM as a Cloud Service 中的 CDN {#cdn}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_cdn"
>title="AEM as a Cloud Service 中的 CDN"
>abstract="AEM asCloud Service随内置CDN一起提供。 其主要目的是通过从浏览器附近边缘的CDN节点交付可缓存的内容来减少延迟。 它经过全面的管理和配置，可提供最佳的 AEM 应用程序性能。"

AEM asCloud Service随内置CDN一起提供。 其主要目的是通过从浏览器附近的边缘 CDN 节点提供可缓存的内容来减少延迟。它经过全面的管理和配置，可提供最佳的 AEM 应用程序性能。

AEM托管的CDN将满足大多数客户的性能和安全要求。 对于发布层，客户可以选择从自己的CDN指向它，他们需要管理CDN。 将根据满足某些先决条件（包括但不限于客户与其CDN供应商进行旧版集成，而这些旧版集成很难放弃）的情况，逐个允许执行此操作。

另请观看以下视频 [Cloud 5 AEM CDN第1部分](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-5/cloud5-aem-cdn-part1.html) 和 [Cloud 5 AEM CDN第2部分](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-5/cloud5-aem-cdn-part2.html) 有关AEM as a Cloud Service中CDN的其他信息。

## AEM Managed CDN  {#aem-managed-cdn}

请按照以下部分，使用Cloud Manager自助服务UI，通过现成的CDN为内容交付做好准备：

1. [管理 SSL 证书](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md)
1. [管理自定义域名](/help/implementing/cloud-manager/custom-domain-names/introduction.md)

**限制流量**

默认情况下，对于AEM托管CDN设置，所有公共流量都可以进入生产环境和非生产（开发和暂存）环境的发布服务。 如果您希望限制给定环境的发布服务的流量（例如，限制按IP地址范围进行暂存），则可以通过Cloud Manager UI以自助方式执行此操作。

请参阅 [管理IP允许列表](/help/implementing/cloud-manager/ip-allow-lists/introduction.md) 以了解更多。

>[!CAUTION]
>
>只有来自允许IP的请求才会由AEM托管CDN提供。 如果您将自己的CDN指向AEM托管的CDN，请确保将CDN的IP包含在该允许列表中。

## 客户CDN指向AEM Managed CDN {#point-to-point-CDN}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_byocdn"
>title="客户CDN指向AEM Managed CDN"
>abstract="AEM as Cloud Service为客户提供了使用其现有CDN的选项。 对于发布层，客户可以选择从自己的CDN指向它，他们需要管理CDN。 将根据满足某些先决条件（包括但不限于客户与其CDN供应商进行旧版集成，而这些旧版集成很难放弃）的情况，逐个允许执行此操作。"

如果客户必须使用其现有的CDN，则他们可以管理CDN并将其指向AEM托管的CDN，从而满足以下要求：

* 客户必须拥有现有的CDN，这样的CDN更换将非常繁琐。
* 客户必须管理它。
* 客户必须能够配置CDN以使用AEMas a Cloud Service — 请参阅下面提供的配置说明。
* 客户必须有工程CDN专家随时待命，以防出现相关问题。
* 客户必须先执行并成功通过负载测试，然后才能转到生产环境。

>[!NOTE]
>
>AdobeCDN不是可选的。 客户自带CDN必须将其指向AEM Managed CDN。

配置说明：

1. 将您的CDN指向AdobeCDN的入口作为其源域。 例如， `publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com`.
1. SNI还必须设置为AdobeCDN的入口。
1. 将主机标头设置为源域。 例如：`Host:publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com`。
1. 设置 `X-Forwarded-Host` 标头，以便AEM可以确定主机标头。 例如：`X-Forwarded-Host:example.com`。
1. 套 `X-AEM-Edge-Key`. 值应来自Adobe。

   * 这是AdobeCDN验证请求源并传递 `X-Forwarded-*` 标头。 例如，`X-Forwarded-For` 用于确定客户端IP。 因此，它成为可信呼叫者（即客户管理的CDN）的责任，来确保 `X-Forwarded-*` 标题（请参阅下面的注释）。
   * 或者，当Adobe `X-AEM-Edge-Key` 不存在。 如果您需要直接访问AdobeCDN的入口（待阻止），请通知Adobe。

在接受实时流量之前，您应该通过Adobe的客户支持验证端到端流量路由是否正确运行。

获取 `X-AEM-Edge-Key`，则可以测试请求是否按如下方式正确路由。

在Linux中：

```
curl https://publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com -H "X-Forwarded-Host: example.com" -H "X-AEM-Edge-Key: <PROVIDED_EDGE_KEY>"
```

在Windows中：

```
curl https://publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com --header "X-Forwarded-Host: example.com" --header "X-AEM-Edge-Key: <PROVIDED_EDGE_KEY>"
```

请注意，使用您自己的CDN时，无需在Cloud Manager中安装域和证书。 AdobeCDN中的路由将使用默认域完成 `publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com`.

>[!NOTE]
>
>管理自己CDN的客户应确保发送到AEM CDN的标头的完整性。 例如，建议客户清除所有 `X-Forwarded-*` 标头，并将其设置为已知和受控值。 例如， `X-Forwarded-For` 应包含客户端的IP地址，而 `X-Forwarded-Host` 应包含网站的主机。

>[!NOTE]
>
>沙盒项目环境不支持客户提供的CDN。

由于额外的跳数，性能可能会受到较小的点击，不过从客户CDN到AEM托管CDN的跳数可能会非常有效。

请注意，发布层支持此客户CDN配置，但创作层不支持此配置。

## 地理位置标题 {#geo-headers}

AEM Managed CDN会通过以下方式向每个请求添加标头：

* 国家/地区代码： `x-aem-client-country`
* 大陆代码： `x-aem-client-continent`

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
