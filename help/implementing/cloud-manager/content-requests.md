---
title: 了解 Cloud Service 内容请求
description: 如果您从Adobe购买了内容请求许可证，请了解Adobe Experience Cloud as a Service测量的内容请求类型以及与组织分析报告工具的差异。
exl-id: 3666328a-79a7-4dd7-b952-38bb60f0967d
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: f24b2672431ecf7b7b0ed11b6dc9b09344946239
workflow-type: tm+mt
source-wordcount: '1276'
ht-degree: 9%

---

# 了解Cloud Service内容请求

## 简介 {#introduction}

内容请求是指向AEM Sites发出的请求，包括那些与Edge Delivery Services或客户提供的缓存系统（如Content Delivery Network）相关的请求。 这些请求通过页面视图(例如，页面和HTML片段)以JSON格式以Headless方式通过API调用以Experience格式交付内容或数据。 内容请求被计为一次页面查看或五次API调用，并在第一个接收内容请求的缓存系统的入口测量。 出于计数内容请求的目的，包含或排除某些HTTP请求。 文档中提供了此类已包含和已排除的HTTP请求的完整列表及其技术定义。

## 关于Cloud Service内容请求 {#understanding-cloud-service-content-requests}

对于使用现成CDN的客户，Cloud Service内容请求通过服务器端数据收集来测量。 此收藏集将通过CDN日志分析启用。 AEM (Adobe Experience Manager) as a Cloud Service会自动在边缘位置收集服务器端内容请求。 它分析AEM as a Cloud Service CDN生成的日志文件。 此过程通过从CDN隔离返回HTML`(text/html)`或JSON `(application/json)`内容的请求来完成，并且基于下面详述的几个包含和排除规则。 无论内容是从CDN缓存中提供，还是返回到CDN源位置(AEM调度程序)，都会发生内容请求。

<!-- REMOVED AS PER EMAIL REQUEST FROM SHWETA DUA, JULY 30, 2024 TO RICK BROUGH AND ALEXANDRU SARCHIZ   For customers employing their own CDN, client-side collection offers a more precise reflection of interactions, ensuring a reliable measure of website engagement via the [Real Use Monitoring](/help/sites-cloud/administering/real-use-monitoring-for-aem-as-a-cloud-service.md) service. This gives customers advanced insights into their page traffic and performance. While it is beneficial for all customers, it offers a representative reflection of user interactions, ensuring a reliable measure of website engagement by capturing the number of page views from the client side. 

For customers that bring their own CDN on top of AEM as a Cloud Service, server-side reporting results in numbers that cannot be used to compare with the licensed content requests. With the [Real Use Monitoring](/help/sites-cloud/administering/real-use-monitoring-for-aem-as-a-cloud-service.md), Adobe can reflect a reliable measure of website engagement. -->

### Cloud Service内容请求的差异 {#content-requests-variances}

内容请求在组织的Analytics报告工具中可能有差异，如下表所示。 通常，应避免使用依赖客户端工具来报告网站内容请求数量的分析工具。 这些工具经常会漏掉大部分流量，因为它们依赖于用户同意才能激活。 收集日志文件中的服务器端数据的Analytics工具，或供在AEM as a Cloud Service上添加其自己CDN的客户使用的CDN报告，可提供更好的计数。

| 差异原因 | 解释 |
|---|---|
| 最终用户同意 | 依赖客户端工具的Analytics工具通常取决于用户是否同意触发。 此工作流可能代表大多数未被跟踪的流量。 对于希望自行测量内容请求的客户，建议依赖分析工具来收集数据服务器端或CDN报告。 |
| 标记 | 作为Adobe Experience Manager内容请求跟踪的所有页面或API调用可能不会使用Analytics跟踪进行标记。 |
| Tag Management 规则 | Tag Management规则设置可能会导致页面上的各种数据收集配置，从而导致与内容请求跟踪的某些差异组合。 |
| 机器人 | AEM未预先识别和删除的未知机器人程序可能会导致跟踪不一致。 |
| 报告包 | 属于同一 AEM 实例和域的页面可能会将数据发送到不同的 Analytics 报告包。 |
| 第三方监控和安全工具 | 监控和安全扫描工具可能会为 AEM 生成 Analytics 报告中未跟踪的内容请求。 |
| API访问 | 以编程方式访问页面或Adobe Experience Manager API可能会为AEM生成未在Analytics报表中跟踪的内容请求。 |
| 预获取请求 | 使用预获取服务预加载页面来提高速度，可能会导致内容请求流量显著增加。 |
| DDOS | 虽然Adobe会尝试自动检测和过滤来自DDOS攻击的流量，但无法保证检测到所有可能的DDOS攻击。 |
| 流量拦截器 | 在浏览器中使用跟踪拦截器可能会选择不跟踪某些请求。 |
| 防火墙 | 防火墙可能会阻止分析跟踪。这种情况在公司防火墙中更为常见。 |

另请参阅[许可证仪表板](/help/implementing/cloud-manager/license-dashboard.md)。

## 服务器端收集规则 {#serverside-collection}

有规则可排除知名机器人，包括定期访问网站以刷新其搜索索引或服务的知名服务。

### 包含的内容请求的类型 {#included-content-requests}

| 请求类型 | 内容请求 | 描述 |
| --- | --- | --- |
| HTTP代码100-299 | 已包含 | 提供全部或部分内容的常规请求。 |
| 用于自动化的HTTP库 | 已包含 | 示例：<br>· Amazon CloudFront<br>· Apache Http Client<br>· Asynchronous HTTP Client<br>· Axios<br>· Azureus<br>· Curl<br>· GitHub Node Fetch<br>· Guzzle<br>· Go-http-client<br>· Headless Chrome<br>· Java™ Client<br>· Jersey<br>· Node Oembed<br>· okhttp<br>· <br>· Reactor Netty<br>· Wget<br>· WinHTTP<br>· Fast HTTP<br>· GitHub Node Fetch<br>· Reactor Netty |
| 监控和运行状况检查工具 | 已包含 | 由客户设置，用于监控站点的某些方面。 例如，可用性或真实用户性能。 如果它们针对特定端点（如`/system/probes/health`）进行运行状况检查，Adobe建议您使用`/system/probes/health`端点，而不是网站中的实际HTML页面。 [查看以下](#excluded-content-request)<br>示例：<br>· `Amazon-Route53-Health-Check-Service`<br>· EyeMonIT_bot_version_0.1_[(https://eyemonit.com/)](https://eyemonit.com/)<br>· Investis-Site24x7<br>· Mozilla/5.0+(兼容； UptimeRobot/2.0；[https://uptimerobot.com/](https://uptimerobot.com/))<br>· ThoudedEyes-Dragonfly-x1<br>· OmtrBot/1.0<br>· WebMon/2.0.0 |
| `<link rel="prefetch">`个请求 | 已包含 | 为了提高下一页的加载速度，客户可以在用户单击链接之前让浏览器加载一组页面，以使这些页面已位于缓存中。 *请注意：此方法会显着增加流量*，具体取决于预取的页面数量。 |
| 阻止Adobe Analytics或Google Analytics报表的流量 | 已包含 | 通常，网站访客会安装隐私软件（广告拦截器等），这会影响Google Analytics或Adobe Analytics的准确性。 AEM as a Cloud Service在进入Adobe运行的基础结构的第一个入口点而不是客户端计算请求。 |

另请参阅[许可证仪表板](/help/implementing/cloud-manager/license-dashboard.md)。

### 排除的内容请求的类型 {#excluded-content-request}

| 请求类型 | 内容请求 | 描述 |
| --- | --- | --- |
| HTTP代码500+ | 已排除 | 当AEM as a Cloud Service或客户自定义代码上出现问题时，会返回错误给访客。 |
| HTTP代码400-499 | 已排除 | 内容不存在(404)或存在其他内容或请求相关问题时返回给访客的错误。 |
| HTTP代码300-399 | 已排除 | 很好的请求：检查服务器上是否有某些内容发生更改，或将请求重定向到其他资源。 它们本身不包含内容，因此它们不可计费。 |
| 发送到/libs/*的请求 | 已排除 | AEM内部JSON请求，例如不可计费的CSRF令牌。 |
| 来自DDOS攻击的流量 | 已排除 | DDOS保护。 AEM会自动检测一些DDOS攻击并阻止它们。 检测到的DDOS攻击无法计费。 |
| AEM as a Cloud Service New Relic监控 | 已排除 | AEM as a Cloud Service全球监控。 |
| 客户用于监控其Cloud Service计划的URL | 已排除 | Adobe建议您使用URL从外部监视可用性或运行状况检查。<br><br>`/system/probes/health` |
| AEM as a Cloud Service Pod预热服务 | 已排除 |
| 座席： skyline-service-warmup/1.* |
| 著名的搜索引擎、社交网络和HTTP库（由Fastly标记） | 已排除 | 已知的服务定期访问网站以刷新其搜索索引或服务： <br><br>示例： <br>· AddSearchBot<br>· AhrefsBot<br>· Applebot<br>· Ask Jeeves Corporate Spider<br>· Bingbot<br>· BingPreview<br>· BLEXBot<br>· BuildWith<br>· Bytespider<br>· CrawlerKengo<br>· Facebookexternalhit<br>· Google AdsBotBot <br>· Google AdsBot Mobile<br>· Googlebot<br>· Googlebot Mobile<br>· lmspider<br>· LucidWorks<br>· `MJ12bot`<br>· Pinterest<br>· SemrushBot<br>· SiteImprove<br>· StashBot<br>· StatusCake<br>· YandexBot<br>· Claudebot |
| 排除Commerce integration framework调用 | 已排除 | 向AEM发出的请求将转发到Commerce integration framework（URL以`/api/graphql`开头）以避免重复计数，因此不计费Cloud Service。 |
| 排除`manifest.json` | 已排除 | 清单不是API调用。 本文件旨在提供有关如何在桌面或手机上安装网站的信息。 Adobe不应计为`/etc.clientlibs/*/manifest.json`的JSON请求 |
| 排除`favicon.ico` | 已排除 | 尽管返回的内容不应为HTML或JSON，但已观察到某些场景（如SAML身份验证流）会返回favicon作为HTML。 因此，Favicon会明确从计数中排除。 |
| 到其他后端的CDN代理 | 已排除 | 排除使用[CDN源选择器](/help/implementing/dispatcher/cdn-configuring-traffic.md#origin-selectors)技术路由到其他非AEM后端的请求，因为它们未命中AEM。 |
