---
title: 了解Cloud Service内容请求
description: 如果您从Adobe购买了内容请求许可证，请了解Adobe Experience Cloud as a Service测量的内容请求类型以及与组织分析报告工具的差异。
source-git-commit: e34b21194e35b2f56dd1e7df2165c3fa5c0cb7da
workflow-type: tm+mt
source-wordcount: '1171'
ht-degree: 12%

---


# Cloud Service内容请求

## Cloud Service内容请求的差异{#content-requests-variances}

内容请求可能与组织的Analytics报告工具存在差异，如下表所示。 通常，Analytics工具通过客户端工具收集数据 <b>不应使用</b> 报告给定站点的内容请求数，原因很简单，它们通常依赖于最终用户同意触发，因此会错过流量的很大一部分。 在日志文件中收集数据服务器端的Analytics工具，或者为在AEMas a Cloud Service之上添加自己的CDN的客户提供的CDN报告，将提供更好的计数。 要报告页面查看次数及其相关性能，AdobeRUM数据服务是Adobe推荐的选项。

| 差异原因 | 解释 |
|---|---|
| 最终用户同意 | 依赖客户端工具的Analytics工具通常取决于最终用户同意触发。 这可能表示大多数流量未被跟踪。 对于希望自行测量内容请求的客户，建议依赖分析工具来收集数据服务器端或CDN报告。 |
| 标记 | 作为Adobe Experience Manager (AEM)内容请求跟踪的所有页面或API调用可能不会使用Analytics跟踪进行标记。 |
| Tag Management 规则 | Tag Management规则设置可能会导致页面上的各种数据收集配置，从而导致与内容请求跟踪的某些差异组合。 |
| 机器人 | AEM 尚未预先识别和移除的未知机器人程序可能会导致跟踪不一致。 |
| 报告包 | 属于同一 AEM 实例和域的页面可能会将数据发送到不同的 Analytics 报告包。 |
| 第三方监控和安全工具 | 监控和安全扫描工具可能会为 AEM 生成 Analytics 报告中未跟踪的内容请求。 |
| API访问 | 以编程方式访问页面或Adobe Experience Manager API可能会为AEM生成未在Analytics报表中跟踪的内容请求。 |
| 预获取请求 | 使用预获取服务预加载页面来提高速度，可能会导致内容请求流量显著增加。 |
| DDOS | 虽然 Adobe 竭尽全力自动检测和过滤 DDOS 攻击的流量，但无法保证检测到所有可能的 DDOS 攻击 |
| 流量拦截器 | 在浏览器中使用跟踪拦截器可能会选择不跟踪某些请求。 |
| 防火墙 | 防火墙可能会阻止分析跟踪。这种情况在公司防火墙中更为常见。 |

另请参阅 [许可证仪表板](/help/implementing/cloud-manager/license-dashboard.md).

## 了解Cloud Service内容请求 {#about-content-request}

通过自动分析源自Adobe Experience Manager (AEM)as a Cloud ServiceCDN的日志文件，从CDN中分离返回HTML（文本/html）或JSON （应用程序/json）内容的请求，并根据下面详述的若干包含和排除规则，在AEM ()as a Cloud Service的边缘自动跟踪内容请求。 内容请求与从CDN缓存提供或返回到CDN源位置(AEM Dispatchers)的返回内容无关。

对于在AEMas a Cloud Service之上自带CDN的客户，此跟踪将导致无法使用数字与许可的内容请求进行比较，这些数字将由位于外部CDN边缘的客户测量。

有规则可排除知名机器人，包括定期访问网站以刷新其搜索索引或服务的知名服务。

### 包含的内容请求的类型{#included-content-requests}

| 请求类型 | 内容请求 | 描述 |
| --- | --- | --- |
| HTTP代码100-299 | 已包含 | 这些是提交全部或部分内容的常规请求。 |
| 用于自动化的HTTP库 | 已包含 | 示例：<br>· Amazon CloudFront<br>· Apache Http客户端<br>·异步Http客户端<br>· Axios<br>·蔚蓝色<br>·卷曲<br>· GitHub节点获取<br>·居策尔<br>· Go-http-client<br>· Headless铬黄<br>· Java™客户端<br>·泽西岛<br>·节点Oembed<br>· okhttp<br>· Python请求<br>· Reactor Netty<br>·威吉特<br>· WinHTTP |
| 监控和运行状况检查工具 | 已包含 | 这些功能由客户设置，用于监控站点的某些方面。 例如，可用性或真实用户性能。 使用 `/system/probes/health` 端点，而不是网站中的实际HTML页面。<br>示例：<br>· Amazon-Route53-Health-Check-Service<br>· EyeMonIT_bot_version_0.1_[(https://www.eyemon.it/)](https://www.eyemon.it/)<br>·调查站点24x7<br>· Mozilla/5.0+(兼容；UptimeRobot/2.0； [https://uptimerobot.com/](https://uptimerobot.com/))<br>·千眼 — 蜻蜓 — x1<br>· OmtrBot/1.0<br>· WebMon/2.0.0 |
| `<link rel="prefetch">` 请求 | 已包含 | 为了提高下一页的加载速度，客户可以在用户单击链接之前让浏览器加载一组页面，以使这些页面已位于缓存中。 *注意：这会显着增加流量* — 取决于预取的页面数量。 |
| 阻止Adobe Analytics或Google Analytics报表的流量 | 已包含 | 通常，网站访客会安装隐私软件（广告拦截器等），这会影响Google Analytics或Adobe Analytics的准确性。 AEMas a Cloud Service在进入Adobe运行的基础结构的第一个入口点而不是客户端计算请求。 |

另请参阅 [许可证仪表板](/help/implementing/cloud-manager/license-dashboard.md).

### 排除的内容请求的类型{#excluded-content-request}

| 请求类型 | 内容请求 | 描述 |
| --- | --- | --- |
| HTTP代码500+ | 已排除 | 当AEMas a Cloud Service或客户自定义代码出现问题时，会返回错误给访客。 |
| HTTP代码400-499 | 已排除 | 内容不存在(404)或存在其他内容或请求相关问题时返回给访客的错误。 |
| HTTP代码300-399 | 已排除 | 这些是很好的请求，可检查服务器上是否有某些内容发生更改，或将请求重定向到其他资源。 它们本身不包含内容，因此它们不可计费。 |
| 发送到/libs/*的请求 | 已排除 | AEM内部JSON请求，例如不可计费的CSRF令牌。 |
| 来自DDOS攻击的流量 | 已排除 | DDOS保护。 AEM会自动检测一些DDOS攻击并阻止它们。 检测到的DDOS攻击无法计费。<br><br>自动检测到的DDOS类型：<br>· DDOSBlockedCiphersSHA<br>· DDOSBlockedPattern<br>· DDOSSuspiciousRequest |
| AEMas a Cloud ServiceNewRelic监控 | 已排除 | AEMas a Cloud Service全局监控。 |
| 客户用于监控其Cloud Service计划的URL | 已排除 | 建议用于外部监控可用性的URL。<br><br>`/system/probes/health` |
| AEMas a Cloud ServicePod预热服务 | 已排除 | 用户代理： skyline-service-warmup/1.* |
| 著名的搜索引擎、社交网络和HTTP库（由Fastly标记） | 已排除 | 著名的服务会定期访问站点以刷新其搜索索引或服务：<br><br>示例：<br>· AddSearchBot<br>·AhrefsBot<br>· Applebot<br>·向Jeeves Corporate Spider咨询<br>·宾博特<br>·必应预览<br>·边界点<br>·内置于<br>·字节蜘蛛<br>·爬网工具引擎<br>· Facebookexternalhit<br>·Google AdsBot<br>· Google AdsBot Mobile<br>·谷歌机器人<br>· Google Bot Mobile<br>·爬虫程序<br>· LucidWorks<br>· MJ12bot<br>·平多姆<br>·Pinterest<br>· SemrushBot<br>·站点改进<br>·存储机器人<br>· StatusCake<br>· YandexBot |
| 排除Commerce integration framework调用 | 已排除 | 这些是向AEM发出的请求，将转发到Commerce integration framework，URL开头为 `/api/graphql` — 为了避免重复计数，它们不计费Cloud Service。 |
| 不包括 `manifest.json` | 已排除 | 清单不是API调用，它旨在提供有关如何在桌面或手机上安装网站的信息。 Adobe不应将JSON请求计为 `/etc.clientlibs/*/manifest.json` |
| 不包括 `favicon.ico` | 已排除 | 虽然返回的内容不应为HTML或JSON，但我们发现，在某些场景（如SAML身份验证流）中，favicon可能会作为HTML返回，因此会从计数中显式排除。 |


