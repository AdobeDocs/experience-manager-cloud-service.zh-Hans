---
title: 了解 Cloud Service 内容请求
description: 如果您从Adobe购买了内容请求许可证，请了解Adobe Experience Cloud as a Service测量的内容请求类型以及与组织分析报告工具的差异。
exl-id: 3666328a-79a7-4dd7-b952-38bb60f0967d
source-git-commit: 53a66eac5ca49183221a1d61b825401d4645859e
workflow-type: tm+mt
source-wordcount: '2688'
ht-degree: 5%

---

# Cloud Service内容请求

## 简介 {#introduction}

Cloud Service内容请求通过服务器端数据收集来测量。 收藏集可通过CDN日志分析启用。

>[!NOTE]
>此外，对于有限数量的 [率先采用者客户](/help/release-notes/release-notes-cloud/release-notes-current.md#sites-early-adopter)，客户端收集也将通过Real User Monitoring服务测量启用。 有关更多信息，请参阅中的文档。 [本文](#real-user-monitoring-for-aem-as-a-cloud-service).

## 了解 Cloud Service 内容请求 {#understaing-cloud-service-content-requests}

通过自动分析源自AEMas a Cloud ServiceCDN的日志文件，在Adobe Experience Manager as a Cloud Service边缘的服务器端自动收集内容请求。 这是通过隔离请求返回HTML来完成的 `(text/html)` 或JSON `(application /Json)` 来自CDN的内容以及基于下面详述的几个包含和排除规则。 内容请求独立于CDN缓存提供的返回内容或返回到CDN源的内容(AEM Dispatchers)。

Real User Monitoring服务作为客户端集合，提供了对用户交互的更精确反映，确保了对网站参与度的可靠衡量。 这可以让客户深入了解其页面流量和性能。 这对使用Adobe托管的CDN或非Adobe托管的CDN的客户都很有用。 此外，现在可以为使用非Adobe托管的CDN的客户启用自动流量报告，因此无需与Adobe共享任何流量报告。

对于在AEMas a Cloud Service之上自带CDN的客户，服务器端报表将导致无法使用数字与许可的内容请求进行比较。 这些数字必须由位于外部CDN边缘的客户测量。 对于这些客户、客户端报告和相关性能， [AdobeRUM数据服务](#real-user-monitoring-for-aem-as-a-cloud-service) 是Adobe推荐选项。 请参阅 [发行说明](/help/release-notes/release-notes-cloud/release-notes-current.md#sites-early-adopter) 以获取有关如何选择加入的信息。

## 服务器端收藏集 {#serverside-collection}

有规则可排除知名机器人，包括定期访问网站以刷新其搜索索引或服务的知名服务。

### Cloud Service内容请求的差异 {#content-requests-variances}

内容请求可能与组织的Analytics报告工具存在差异，如下表所示。 一般来说， *不要* 使用通过客户端工具收集数据的analytics工具来报告给定站点的内容请求数，原因很简单，它们通常依赖于要触发的用户同意，因此会错过流量的很大一部分。 在日志文件中收集数据服务器端的Analytics工具，或者为在AEMas a Cloud Service之上添加自己的CDN的客户提供的CDN报告，将提供更好的计数。 要报告页面查看及其相关性能，AdobeRUM数据服务是Adobe推荐选项。

| 差异原因 | 解释 |
|---|---|
| 最终用户同意 | 依赖客户端工具的Analytics工具通常取决于用户是否同意触发。 这可能表示大多数流量未被跟踪。 对于希望自行测量内容请求的客户，建议依赖分析工具来收集数据服务器端或CDN报告。 |
| 标记 | 作为Adobe Experience Manager (AEM)内容请求跟踪的所有页面或API调用可能不会使用Analytics跟踪进行标记。 |
| Tag Management 规则 | Tag Management规则设置可能会导致页面上的各种数据收集配置，从而导致与内容请求跟踪的某些差异组合。 |
| 机器人 | AEM 尚未预先识别和移除的未知机器人程序可能会导致跟踪不一致。 |
| 报告包 | 属于同一 AEM 实例和域的页面可能会将数据发送到不同的 Analytics 报告包。 |
| 第三方监控和安全工具 | 监控和安全扫描工具可能会为 AEM 生成 Analytics 报告中未跟踪的内容请求。 |
| API访问 | 以编程方式访问页面或Adobe Experience Manager API可能会为AEM生成未在Analytics报表中跟踪的内容请求。 |
| 预获取请求 | 使用预获取服务预加载页面来提高速度，可能会导致内容请求流量显著增加。 |
| DDOS | 虽然Adobe会尝试自动检测和过滤来自DDOS攻击的流量，但无法保证检测到所有可能的DDOS攻击。 |
| 流量拦截器 | 在浏览器中使用跟踪拦截器可能会选择不跟踪某些请求。 |
| 防火墙 | 防火墙可能会阻止分析跟踪。这种情况在公司防火墙中更为常见。 |

另请参阅 [许可证仪表板](/help/implementing/cloud-manager/license-dashboard.md).

### 包含的内容请求的类型 {#included-content-requests}

| 请求类型 | 内容请求 | 描述 |
| --- | --- | --- |
| HTTP代码100-299 | 已包含 | 这些是提交全部或部分内容的常规请求。 |
| 用于自动化的HTTP库 | 已包含 | 示例：<br>· Amazon CloudFront<br>· Apache Http客户端<br>·异步Http客户端<br>· Axios<br>·蔚蓝色<br>·卷曲<br>· GitHub节点获取<br>·居策尔<br>· Go-http-client<br>· Headless铬黄<br>· Java™客户端<br>·泽西岛<br>·节点Oembed<br>· okhttp<br>· Python请求<br>· Reactor Netty<br>·威吉特<br>· WinHTTP |
| 监控和运行状况检查工具 | 已包含 | 这些功能由客户设置，用于监控站点的某些方面。 例如，可用性或真实用户性能。 使用 `/system/probes/health` 端点，而不是网站中的实际HTML页面。<br>示例：<br>· Amazon-Route53-Health-Check-Service<br>· EyeMonIT_bot_version_0.1_[(https://www.eyemon.it/)](https://www.eyemon.it/)<br>·调查站点24x7<br>· Mozilla/5.0+(兼容；UptimeRobot/2.0； [https://uptimerobot.com/](https://uptimerobot.com/))<br>·千眼 — 蜻蜓 — x1<br>· OmtrBot/1.0<br>· WebMon/2.0.0 |
| `<link rel="prefetch">` 请求 | 已包含 | 为了提高下一页的加载速度，客户可以在用户单击链接之前让浏览器加载一组页面，以使这些页面已位于缓存中。 *注意：这会显着增加流量* — 取决于预取的页面数量。 |
| 阻止Adobe Analytics或Google Analytics报表的流量 | 已包含 | 通常，网站访客会安装隐私软件（广告拦截器等），这会影响Google Analytics或Adobe Analytics的准确性。 AEMas a Cloud Service在进入Adobe运行的基础结构的第一个入口点而不是客户端计算请求。 |

另请参阅 [许可证仪表板](/help/implementing/cloud-manager/license-dashboard.md).

### 排除的内容请求的类型 {#excluded-content-request}

| 请求类型 | 内容请求 | 描述 |
| --- | --- | --- |
| HTTP代码500+ | 已排除 | 当AEMas a Cloud Service或客户自定义代码出现问题时，会返回错误给访客。 |
| HTTP代码400-499 | 已排除 | 内容不存在(404)或存在其他内容或请求相关问题时返回给访客的错误。 |
| HTTP代码300-399 | 已排除 | 这些是很好的请求，可检查服务器上是否有某些内容发生更改，或将请求重定向到其他资源。 它们本身不包含内容，因此它们不可计费。 |
| 发送到/libs/*的请求 | 已排除 | AEM内部JSON请求，例如不可计费的CSRF令牌。 |
| 来自DDOS攻击的流量 | 已排除 | DDOS保护。 AEM会自动检测一些DDOS攻击并阻止它们。 检测到的DDOS攻击无法计费。 |
| AEMas a Cloud ServiceNewRelic监控 | 已排除 | AEMas a Cloud Service全局监控。 |
| 客户用于监控其Cloud Service计划的URL | 已排除 | 建议用于外部监控可用性的URL。<br><br>`/system/probes/health` |
| AEMas a Cloud ServicePod预热服务 | 已排除 | 用户代理： skyline-service-warmup/1.* |
| 著名的搜索引擎、社交网络和HTTP库（由Fastly标记） | 已排除 | 著名的服务会定期访问站点以刷新其搜索索引或服务：<br><br>示例：<br>· AddSearchBot<br>·AhrefsBot<br>· Applebot<br>·向Jeeves Corporate Spider咨询<br>·宾博特<br>·必应预览<br>·边界点<br>·内置于<br>·字节蜘蛛<br>·爬网工具引擎<br>· Facebookexternalhit<br>·Google AdsBot<br>· Google AdsBot Mobile<br>·谷歌机器人<br>· Google Bot Mobile<br>·爬虫程序<br>· LucidWorks<br>· MJ12bot<br>·平多姆<br>·Pinterest<br>· SemrushBot<br>·站点改进<br>·存储机器人<br>· StatusCake<br>· YandexBot |
| 排除Commerce integration framework调用 | 已排除 | 这些是向AEM发出的请求，将转发到Commerce integration framework，URL开头为 `/api/graphql` — 为了避免重复计数，它们不计费Cloud Service。 |
| 排除 `manifest.json` | 已排除 | 清单不是API调用，它旨在提供有关如何在桌面或手机上安装网站的信息。 Adobe不应将JSON请求计为 `/etc.clientlibs/*/manifest.json` |
| 排除 `favicon.ico` | 已排除 | 虽然返回的内容不应为HTML或JSON，但我们发现，在某些场景（如SAML身份验证流）中，favicon可能会作为HTML返回，因此会从计数中显式排除。 |

## 客户端收藏集 {#cliendside-collection}

### 适用于AEM的Real User Monitoring服务as a Cloud Service {#real-user-monitoring-service-for-aem-as-a-cloud-service}

>[!INFO]
>
>此功能仅适用于早期采用者计划。
>您需要使用AEM Cloud Service版本 **2023.11.14227** 以启用RUM数据服务。

### 概述 {#overview}

Real User Monitoring服务是一种性能监控技术，可实时捕获和分析网站或应用程序的数字用户体验。 它提供了Web应用程序实时性能的可视性，并提供了对最终用户体验的准确洞察。

Real User Monitoring服务可让您深入分析关键性能指标，从URL的启动一直到请求被反馈给浏览器为止，所有这些都有助于开发人员增强应用程序，使其易于最终用户使用。

### 谁能从真正的用户监控服务中受益？ {#who-can-benefit-from-rum-service}

RUM Data Service对于所有客户(无论是使用Adobe还是他们自己的CDN)都很有帮助。 它提供了对用户交互的更精确的反映，通过反映客户端的页面查看次数来确保对网站参与度的可靠衡量。

特别是，对于AdobeCDN用户，它可以准确地跟踪用户交互，以将客户端页面查看次数与服务器端CDN日志直接进行比较。

对于使用自己CDN的客户，他们可以受益于简化的流量报表，因为Adobe现在直接集成这些页面视图，而无需单独的报表。

此外，所有客户都可深入了解页面性能，从而有效优化其数字体验。

### 了解Real User监控服务的工作原理 {#understand-how-the-rum-service-works}

Adobe Experience Manager使用Real User Monitoring (RUM)帮助客户和Adobe了解、访客如何与Adobe Experience Manager支持的网站进行交互、诊断性能问题以及衡量实验的有效性。 RUM通过取样和明智地排除所有个人身份信息(PII)来保护访客的隐私（仅监控所有页面查看中的一小部分）。

### Real User Monitoring Service和Privacy {#rum-service-and-privacy}

Adobe Experience Manager中的Real User Monitoring服务旨在保护访客隐私并最大限度地减少数据收集。 作为访客，这意味着您访问的网站不会收集任何个人信息或不会提供Adobe使用。

作为站点操作员，这意味着通过此功能启用监视不需要其他选择加入。因此，最终用户将不需要接受额外的弹出窗口来启用RUM监视。

### Real User Monitoring Service数据采样 {#rum-service-data-sampling}

传统的Web分析解决方案会尝试收集每位访客的数据。 Adobe Experience Manager的Real User Monitoring服务仅从一小部分页面查看中捕获信息。 Real User Monitoring服务数据旨在进行采样和匿名处理，而不是取代分析。 默认情况下，页面的取样比例将为1:100。 截至今天，站点操作员无法将此数字配置为增加或减少采样速率。 为了准确估计总流量，我们每100次页面查看就收集一次的详细数据，从而为您提供整体流量的可靠近似值。”

由于是否按页面查看次数决定是否要收集数据，因此实际上不可能跟踪多个页面上的交互。 RUM没有访问次数、访客数或会话数的概念，而只是页面查看数的概念。 这是特意设计的。

### 正在收集哪些数据 {#what-data-is-being-collected}

Real User Monitoring服务旨在防止收集个人身份信息。 下面列出了Adobe Experience Manager的Real User Monitoring服务可以收集的全套信息：

* 被访问站点的主机名，例如： `experienceleague.adobe.com`
* 用于显示页面的广泛用户代理类型，例如：桌面或移动设备
* 数据收集的时间，例如： `2021-06-26 06:00:02.596000 UTC (in order to preserve privacy, we round all minutes to the previous hour, so that only seconds and milliseconds are tracked)`
* 所访问页面的URL，例如： `https://experienceleague.adobe.com/docs`
* 反向链接URL（链接到当前页面的页面的URL，如果用户点击链接）
* 随机生成的页面视图ID，格式类似于： `2Ac6`
* 采样率的加权或反比，例如： `100`. 这意味着只记录一百分之一的页面查看次数
* 检查点，或加载页面或作为访客与页面交互序列中特定事件的名称
* 用户与上述检查点交互的DOM元素的源或标识符。 例如，这可能是图像
* 针对上述检查点，与用户交互的外部页面或资源的目标或链接。 例如：`https://blog.adobe.com/jp/publish/2022/06/29/media_162fb947c7219d0537cce36adf22315d64fb86e94.png`
* 核心Web虚拟(CWV)性能指标、最大内容绘制(LCP)、首次输入延迟(FID)和累计布局偏移(CLS)，用于描述访客的体验质量。

### 如何设置Real User监控服务 {#how-to-set-up-the-rum-service}

* 如果您希望加入我们的率先采用者计划，请发送电子邮件至 `aemcs-rum-adopter@adobe.com`，以及与Adobe ID关联的电子邮件地址中的生产、暂存和开发环境的域名。 Adobe 的产品团队随后将为您启用真实用户监控 (RUM) 数据服务。
* 完成此操作后，Adobe的产品团队将创建一个客户协作渠道。
* Adobe的产品团队将与您联系，为您提供域密钥和数据仪表板URL，您可以在其中查看页面查看和 [核心Web虚拟(CWV)](https://web.dev/vitals/) 由客户端Real User Monitoring服务收集收集的量度。
* 然后，将指导您如何使用域密钥访问数据仪表板url并查看指标。

### 如何使用实际用户监控服务数据 {#how-rum-service-data-is-being-used}

RUM数据有利于以下目的：

* 确定并解决客户地点的性能瓶颈
* 简化的自动流量报表，包括使用自身CDN的客户的页面查看次数，这意味着他们不必与Adobe共享任何流量报表。
* 了解Adobe Experience Manager如何与同一页面上的其他脚本（例如Analytics、Targeting或外部库）进行交互以提高兼容性。

### 限制和了解页面查看次数和性能量度中的差异 {#limitations-and-understanding-variance-in-page-views-and-performance-metrics}

由于您将分析此数据，因此Real User Monitoring (RUM)报告的页面查看次数和其他性能量度可能存在也可能不存在差异。 这些差异可归因于实时客户端监控固有的几个因素。 以下是客户在解释RUM数据时要牢记的关键注意事项：

1. **跟踪器阻止程序**

   * 最终用户使用跟踪器阻止程序或隐私扩展可能会阻碍Real User Monitoring服务的数据收集，因为这些工具会限制跟踪脚本的执行。 此限制可能会导致页面查看次数和用户交互报告不足，从而造成实际网站活动与RUM捕获的数据之间存在差异。

1. **捕获API/JSON调用时的限制**

   * RUM数据服务侧重于客户端体验，目前不捕获后端API或JSON调用。 从Real User Monitoring服务数据中排除这些调用将会导致与CDN Analytics测量的内容请求产生差异。

### 常见问题解答 {#faq}

1. **如何配置要在监视中包含或排除的路径？**

   客户可以通过在Cloud Manager的配置中设置环境变量，来配置路径以包含或排除要监视的URL，具体方法是：使用这些变量： `AEM_WEBVITALS_EXCLUDE` 和 `AEM_WEBVITALS_INCLUDE_PATHS`

   请注意，默认情况下，“包含”设置配置为目标“/content”。 请务必记住，您需要在此处配置的路径是系统内的内容路径，而不是您在浏览器中看到的URL路径。 这一区别是准确设置和自定义您的配置以满足特定需求的关键。

1. **在交互到达客户管理的CDN之前或交互到达客户管理的CDN时，Adobe能否跟踪所有页面查看次数？**

   是的。

1. **客户能否将RUM数据服务脚本与Dynatrace等第三方系统集成？**

   是的。

1. **是否正在收集“交互到下一幅绘画”、“第一字节所用时间”和“首次内容绘画”Web虚拟量度？**

   收集到下一绘画的交互(INP)和到第一字节的时间(TTFB)。  此时不收集第一个内容绘制。
