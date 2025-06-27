---
title: 了解 Cloud Service 内容请求
description: 如果您从Adobe购买了内容请求许可证，请了解Adobe Experience Cloud as a Service测量的内容请求类型以及与组织分析报告工具的差异。
exl-id: 3666328a-79a7-4dd7-b952-38bb60f0967d
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: fddd57877f2e4e98f0b89b496eedc25ce741d8f1
workflow-type: tm+mt
source-wordcount: '1574'
ht-degree: 3%

---

# 了解Cloud Service内容请求

## 简介 {#introduction}

内容请求包括发送到AEM Sites的请求。 这些请求可能会通过Edge Delivery Services或客户提供的缓存系统(例如Content Delivery Network (CDN))进行路由。 这些请求以HTML或JSON格式提供结构化数据，并支持页面视图（例如，页面和体验片段）或JSON以Headless方式通过API返回。

当用户使用HTML或JSON查看页面时，系统会计算内容请求数。 它会在第一个缓存系统收到请求的位置测量请求。 出于计数内容请求的目的，包含或排除某些HTTP请求。 查看HTTP [包含的内容请求](#included-content-requests)和[排除的内容请求](#excluded-content-request)的完整列表。

>[!NOTE]
>
>内容请求视图中显示的数据每24小时刷新一次。

## 关于Cloud Service内容请求 {#understanding-cloud-service-content-requests}

*页面请求*&#x200B;引用了HTTP请求，该请求可检索渲染主页面体验所需的核心结构化内容(例如，HTML或JSON)。 它不包括资源请求，例如图像或脚本。

对于使用现成CDN的客户，AEM as a Cloud Service会根据服务器端级别测量的内容请求数量来计数。 此测量自动进行，不依赖客户端分析跟踪。

AEM (Adobe Experience Manager) as a Cloud Service基于AEM实例生成并在CDN处接收的响应类型来标识内容请求。 具体而言，将计算返回HTML (`text/html`)或JSON (`application/json`)的请求。 这些格式通常为传统站点渲染或Headless投放投放投放提供主页面内容。

对静态资源(如JavaScript文件、CSS样式表和图像)的请求将不会计为内容请求。

>[!NOTE]
>如果API请求返回用作页面级内容的HTML或JSON（例如，在Headless投放中），则根据上下文，它仍可能会被视为内容请求。

测量内容请求，无论响应是从CDN缓存提供还是转发到源AEM环境。

<!-- REMOVED AS PER EMAIL REQUEST FROM SHWETA DUA, JULY 30, 2024 TO RICK BROUGH AND ALEXANDRU SARCHIZ   For customers employing their own CDN, client-side collection offers a more precise reflection of interactions, ensuring a reliable measure of website engagement via the [Real Use Monitoring](/help/sites-cloud/administering/real-use-monitoring-for-aem-as-a-cloud-service.md) service. This gives customers advanced insights into their page traffic and performance. While it is beneficial for all customers, it offers a representative reflection of user interactions, ensuring a reliable measure of website engagement by capturing the number of page views from the client side. 

For customers that bring their own CDN on top of AEM as a Cloud Service, server-side reporting results in numbers that cannot be used to compare with the licensed content requests. With the [Real Use Monitoring](/help/sites-cloud/administering/real-use-monitoring-for-aem-as-a-cloud-service.md), Adobe can reflect a reliable measure of website engagement. -->

### Cloud Service内容请求的差异 {#content-requests-variances}

内容请求在组织的分析报告工具中可能有差异，如下表所示。 通常，应避免使用依赖客户端工具来报告网站内容请求数量的分析工具。 这些工具经常会漏掉大部分流量，因为它们依赖于用户同意才能激活。 收集日志文件中的服务器端数据的Analytics工具，或供在AEM as a Cloud Service上添加其自己CDN的客户使用的CDN报告，可提供更好的计数。

| 差异原因 | 解释 |
|---|---|
| 最终用户同意 | 依赖客户端工具的Analytics工具通常取决于用户是否同意触发。 此工作流可能代表大多数未被跟踪的流量。 对于希望自行测量内容请求的客户，Adobe建议您依靠Analytics工具从服务器端或CDN报表中收集数据。 |
| 标记 | 作为Adobe Experience Manager内容请求跟踪的所有页面或API调用可能不会使用Analytics跟踪进行标记。 |
| Tag Management 规则 | Tag Management规则设置可能会导致页面上的各种数据收集配置，从而导致与内容请求跟踪的某些差异组合。 |
| 机器人 | AEM未预先识别和删除的未知机器人程序可能会导致跟踪不一致。 |
| 报告包 | 同一AEM实例中的页面可以向不同的Analytics报表包报告。 此过程可以将数据拆分到多个报表包，具体取决于配置。 |
| 第三方监控和安全工具 | 监控和安全扫描工具（例如，正常运行时间检查程序或漏洞扫描程序）可能会请求页面，从而生成分析报表中不显示的服务器端内容请求。 |
| API访问 | 通过API(例如，通过Adobe Experience Manager as a Headless CMS)对AEM页面或内容的请求仍会计为内容请求，但不会触发Analytics跟踪。 |
| 预获取请求 | 预获取（例如，使用Service Worker或Edge函数）可以通过提前请求页面来增加流量。 这些请求在服务器端计算，但不执行客户端分析代码。 |
| DDOS | Adobe使用过滤功能检测和阻止许多DDoS攻击。 但是，在应用过滤器之前，某些攻击请求可能仍会被计为内容请求。 |
| 流量拦截器 | 浏览器中的隐私功能或公司防火墙可能会阻止分析脚本的加载。 这些用户仍会生成服务器端内容请求。 |
| 防火墙 | 公司或区域防火墙可能会阻止分析调用抵达Adobe服务器，从而导致在服务器端计数保持不受影响时分析中出现报告不足。 |

请参阅[许可证仪表板](/help/implementing/cloud-manager/license-dashboard.md)，以了解有关查看和跟踪内容请求使用情况是否符合许可证限制的信息。

## 服务器端收集规则 {#serverside-collection}

AEM as a Cloud Service应用服务器端规则来计数内容请求。 这些规则包括用于排除已知机器人（如搜索引擎爬网程序）和非用户流量（如定期ping站点的监控服务）的逻辑。

下表列出了包含和排除的内容请求的类型，并针对每个类型进行了简要说明。

### 包含的内容请求的类型 {#included-content-requests}

>[!NOTE]
>如果API请求返回HTML响应，则可能会将其分类为内容请求，具体取决于其使用上下文。 通常会排除返回非UI数据的API请求。

| 请求类型 | 内容请求 | 描述 |
| --- | --- | --- |
| HTTP代码100-299 | 已包含 | 包含返回完整或部分HTML或JSON内容的成功请求。<br>HTTP代码206：这些请求仅交付完整内容的一部分。 例如，视频或大型图像。 部分内容请求在交付渲染页面内容中所使用的HTML或JSON响应的一部分时包含在内。 |
| 用于自动化的HTTP库 | 已包含 | 由检索页面内容的工具或库发出的请求。 示例包括： <br>· Amazon CloudFront<br>· Apache Http Client<br>· Asynchronous HTTP Client<br>· Axios<br>· Azureus<br>· Curl<br>· GitHub Node Fetch<br>· Guzzle<br>· Go-http-client<br>· Headless Chrome<br>· Java™ Client<br>· Jersey<br>· Node Oembed<br>· Oembed<br>· python请求<br>· Reactor Netty<br>· Wget<br>· WinHTTP<br>· Fast HTTP<br>· GitHub节点提取<br>· Reactor Netty |
| 监控和运行状况检查工具 | 已包含 | 用于监视页面运行状况或可用性的请求。<br>查看[排除的内容请求的类型](#excluded-content-request)。<br>示例包括以下内容：<br>· `Amazon-Route53-Health-Check-Service`<br>· EyeMonIT_bot_version_0.1_[(https://eyemonit.com/)](https://eyemonit.com/)<br>· Investis-Site24x7<br>· Mozilla/5.0+(兼容； UptimeRobot/2.0；[https://uptimerobot.com/](https://uptimerobot.com/))<br>· ThousandEyes-Dragonfly-x1<br>· OmtrBot/1.0<br>· WebMon/2.0.0 |
| `<link rel="prefetch">`个请求 | 已包含 | 当客户预载或预取内容（例如，使用`<link rel="prefetch">`）时，系统会计算这些服务器端请求。 请注意，此方法可能会增加流量，具体取决于预取的页面数量。 |
| 阻止Adobe Analytics或Google Analytics报表的流量 | 已包含 | 通常，网站访客会安装隐私软件（广告拦截器等），这会影响Google Analytics或Adobe Analytics的准确性。 AEM as a Cloud Service在进入Adobe运行的基础结构的第一个入口点而不是客户端计算请求。 |

另请参阅[许可证仪表板](/help/implementing/cloud-manager/license-dashboard.md)。

### 排除的内容请求的类型 {#excluded-content-request}

| 请求类型 | 内容请求 | 描述 |
| --- | --- | --- |
| HTTP代码500+ | 已排除 | 当AEM as a Cloud Service或客户自定义代码上出现问题时，会返回错误给访客。 |
| HTTP代码400-499 | 已排除 | 内容不存在(404)或存在其他内容或请求相关问题时返回给访客的错误。 |
| HTTP代码300-399 | 已排除 | 很好的请求：检查服务器上是否有某些内容发生更改，或将请求重定向到其他资源。 它们本身不包含内容，因此它们不可计费。 |
| 请求将转至`/libs/`* | 已排除 | AEM内部JSON请求，例如不可计费的CSRF令牌。 |
| 来自DDOS攻击的流量 | 已排除 | DDOS保护。 AEM会自动检测并阻止某些DDOS攻击。 检测到的DDOS攻击无法计费。 |
| AEM as a Cloud Service New Relic监控 | 已排除 | AEM as a Cloud Service全球监控。 |
| 客户用于监控其Cloud Service项目的URL | 已排除 | Adobe建议您使用URL从外部监视可用性或运行状况检查。<br><br>`/system/probes/health` |
| AEM as a Cloud Service Pod预热服务 | 已排除 |
| 座席： skyline-service-warmup/1.* |
| 著名的搜索引擎、社交网络和HTTP库（由Fastly标记） | 已排除 | 已知的服务定期访问网站以刷新其搜索索引或服务： <br><br>示例： <br>· AddSearchBot<br>· AhrefsBot<br>· Applebot<br>· Ask Jeeves Corporate Spider<br>· Bingbot<br>· BingPreview<br>· BLEXBot<br>· BuildWith<br>· Bytespider<br>· CrawlerKengo<br>· Facebookexternalhit<br>· Google AdsAds机器人<br>· Google AdsBot Mobile<br>· Googlebot<br>· Googlebot Mobile<br>· lmspider<br>· LucidWorks<br>· `MJ12bot`<br>· Pinterest<br>· SemrushBot<br>· SiteImprovement<br>· StatusCake<br>· YandexBot<br>· ContentKing<br>克劳德博特<br> |
| 排除Commerce integration framework调用 | 已排除 | 向AEM发出的请求将转发到Commerce integration framework（URL以`/api/graphql`开头）以避免重复计数，因此对于Cloud Service不计费。 |
| 排除`manifest.json` | 已排除 | 清单不是API调用。 本文件旨在提供有关如何在桌面或手机上安装网站的信息。 Adobe不应将对`/etc.clientlibs/*/manifest.json`的JSON请求计为 |
| 排除`favicon.ico` | 已排除 | 尽管返回的内容不应是HTML或JSON，但已观察到某些场景（如SAML身份验证流程）会以HTML的形式返回favicon。 因此，Favicon会明确从计数中排除。 |
| 体验片段(XF) — 相同域重用 | 已排除 | 从同一域上托管的页面（由与请求主机匹配的Referer标头标识）向XF路径（如`/content/experience-fragments/...`）发出请求。<br><br>示例： `aem.customer.com`上的主页从同一域提取横幅或卡片的XF。<br><br>· URL与/content/experience-fragments/...<br>· Referer域与&#x200B;`request_x_forwarded_host`<br><br>**匹配注意：**&#x200B;如果自定义体验片段路径（例如使用`/XFrags/...`或`/content/experience-fragments/`之外的任何路径），则不会排除请求并且可能会计入请求，即使它是同一域也是如此。 我们建议使用Adobe的标准XF路径结构，以确保正确应用排除逻辑。 |
