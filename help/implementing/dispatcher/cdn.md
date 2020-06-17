---
title: AEM中的CDN作为Cloud Service
description: AEM中的CDN作为Cloud Service
translation-type: tm+mt
source-git-commit: dd32e9357bfbd8a9b23db1167cecc4e713cccd99
workflow-type: tm+mt
source-wordcount: '646'
ht-degree: 1%

---


# AEM中的CDN作为Cloud Service {#cdn}

AEM作为Cloud Service随内置CDN提供。 其主要目的是通过从位于边缘、靠近浏览器的CDN节点传送可缓存内容来减少延迟。 它经过全面的管理和配置，可提供最佳的 AEM 应用程序性能。

AEM托管的CDN将满足大多数客户的性能和安全要求。 客户可以选择从自己的CDN指向它，他们需要管理它。 根据满足某些先决条件（包括但不限于客户与其CDN供应商进行难以放弃的旧式集成），将允许按个例执行此操作。

## AEM Managed CDN  {#aem-managed-cdn}

按照以下步骤，使用Adobe现成的CDN准备内容投放:

1. 通过共享指向包含此信息的安全表单的链接，向Adobe提供已签名的SSL证书和密钥。 请在此任务与客户支持协作。
   **注意：** Aem作为Cloud Service不支持域验证(DV)证书。
1. 通知客户支持：
   * 哪个自定义域应与给定环境关联，如项目id和环境id所定义。 请注意，作者端不支持自定义域。
   * 如果需要任何IP允许列表来限制给定环境的通信。
1. 与客户支持协作，确定对DNS记录进行必要更改的时间。 根据是否需要顶点记录，说明有所不同：
   * 如果不需要apex记录，客户应将CNAME DNS记录设置为将其FQDN指向 `cdn.adobeaemcloud.com`。
   * 如果需要apex记录，请创建指向以下IP的A记录： 151.101.3.10、151.101.67.10、151.101.131.10、151.101.195.10。如果所需的FQDN与DNS匹配，客户需要一个顶点记录。 可以使用Unix dig命令测试此值，以查看输出的SOA值是否与域匹配。 例如，该命令 `dig anything.dev.adobeaemcloud.com` 返回SOA(权限开始，即区域), `dev.adobeaemcloud.com` 因此它不是APEX记录，而 `dig dev.adobeaemcloud.com` 返回SOA, `dev.adobeaemcloud.com` 因此它是顶点记录。
1. 当SSL证书过期时，将通知您，这样您就可以重新提交新的SSL证书。

**限制流量**

默认情况下，对于Adobe Managed CDN设置，所有公共流量都可用于生产和非生产（开发和阶段）环境的发布服务。 如果希望限制特定环境发布服务的通信量（例如，限制按IP地址范围进行分阶段），应与客户支持合作配置这些限制。

## 客户CDN指向AEM Managed CDN {#point-to-point-CDN}

如果客户必须使用其现有CDN，他们可以管理CDN并将其指向Adobe的托管CDN，只要满足以下条件：

* 客户必须拥有一个需要更换的现有CDN。
* 客户必须管理它。
* 客户必须能够配置CDN以将AEM作为Cloud Service使用——请参阅下面的配置说明。
* 客户必须拥有随时待命的工程CDN专家，以防出现相关问题。
* 客户必须执行并成功通过负载测试，然后才能投入生产。

配置说明：

1. 使用 `X-Forwarded-Host` 域名设置头。
1. 将主机头与来源域（即Adobe CDN的入口）一起设置。 价值应来自Adobe。
1. 将SNI头发送到来源。 与主机头一样， sni头必须是来源域。
1. 设置 `X-Edge-Key`将流量正确路由到AEM服务器所需的流量。 价值应来自Adobe。

在接受实时流量之前，您应向Adobe客户支持确认端对端流量路由是否工作正常。

请注意，额外的跳数可能会对性能造成很小影响，但从客户CDN到Adobe托管CDN的跳数可能会很有效。
