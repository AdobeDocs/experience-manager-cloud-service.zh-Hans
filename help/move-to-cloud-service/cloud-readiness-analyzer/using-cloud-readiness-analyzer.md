---
title: 使用云就绪性分析器
description: 使用云就绪性分析器
translation-type: tm+mt
source-git-commit: d72f02f76f9be61ef4c3eefd790ff8abbb23a3d8
workflow-type: tm+mt
source-wordcount: '1812'
ht-degree: 0%

---


# 使用云就绪性分析器 {#using-cloud-readiness-analyzer}

## 使用云就绪性分析器的重要注意事项 {#imp-considerations}

请按照以下部分了解运行云就绪性分析器(CRA)时的重要注意事项：

* CRA报告是使用Adobe Experience Manager(AEM)Pattern Detector的输出 [构建的](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/upgrading/pattern-detector.html)。 CRA使用的图案检测器版本包含在CRA安装包中。

* CRA只能由用户或组 `admin` 中的用户运 `Administrators` 行。

* 版本6.1及更高版本的AEM实例支持CRA。

* CRA可以在任何环境上运行，但它更喜欢在舞台 *环境运行* 。

   >[!NOTE]
   >为避免对业务关键型实例产生影响，建议在自定义、配置、内容和用户应用程 *序方面* ，在与生产环境尽可能接近的创作阶段环境上运行CRA。 或者，也可以在生产作者环境的克隆上 *运行* 。

* CRA报告的生成可能需要相当长的时间，从几分钟到几小时。 所需的时间量高度取决于AEM存储库内容的大小和性质、AEM版本以及其他因素。

* 由于生成报告所需的时间很长，因此结果会保留在缓存中，并可供后续查看和下载，直到缓存过期或显式刷新报告为止。

## 可用性 {#availability}

Cloud Readiness Analyzer可从软件分发门户以zip文件的形式下载。 您可以通过源Adobe Experience Manager(AEM)实例上的包管理器安装该包。

>[!NOTE]
>正在从软件分发门户下载云就绪性分析 *器*。

## 运行云就绪性分析器 {#running-tool}

请按照本节学习如何运行云就绪性分析器：

1. 选择Adobe Experience Manager并导航到工具->操 **作** -> **云就绪性分析器**。

   ![图像](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/cra-1.png)

1. 单击“云就绪 **性分析器**”后，生成报告的工具开始在几分钟后AEM实例中会显示摘要报告。

   >[!NOTE]
   >您必须向下滚动页面以视图完整报告。

   ![图像](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/cra-2.png)

### AEM 6.3及更高版本 {#aem-older-version}

对于AEM 6.3及更高版本，运行云就绪性分析器的主要方式是：

1. 使用Adobe Experience Manager用户界面导航到工具->操 **作** -> **云就绪性分析器**。

   >[!NOTE]
   >CRA将在工具打开后立即开始生成报告的后台过程。 它显示一个指示，表示报表生成在报表准备就绪之前正在进行。 您可以关闭浏览器选项卡，稍后返回以在报告完成时视图报告。

生成并显示CRA报告后，您可以选择通过单击工具页面右上角的CSV按钮，以逗号分隔值( **CSV** )格式下载报告。

您可以单击左上角的“刷新报告”按钮，强制CRA清除其缓存并重新生成报告。

### AEM 6.2和6.1 {#aem-specific-versions}

AEM 6.2中的CRA用户界面仅限于生成和下载CSV报告的链接。 对于AEM 6.1，用户界面无法正常工作，只能使用HTTP界面。

在所有版本中，包含的图案检测器可以独立运行。

## CRA摘要报告 {#cra-summary-report}

在AEM用户界面中运行CRA时，报告将作为结果显示在工具窗口中。 报告的格式为：

* 报告概述： 有关报告本身的信息，包括报告的生成时间。
* 系统概述： 关于运行CRA的AEM系统的信息。
* 查找类别: 多个部分，每个部分都处理同一类别的一个或多个发现。 每个部分包括： 类别名称、子类型、查找计数和重要性、摘要、指向类别文档的链接以及单个查找信息。

每个查找结果都分配一个重要性级别，以指示粗略的操作优先级。 使用的重要性级别如下：

| 重要性 | 描述 |
|--- |--- |
| 信息 | 此查找结果仅供参考。 |
| 建议 | 此发现可能是升级问题。 建议进一步调查。 |
| MAJOR | 这一发现可能是一个应解决的升级问题。 |
| 关键 | 这一发现很可能是一个必须解决的升级问题，以防止功能或性能丢失。 |

## CRA CSV报告 {#crs-csv-report}

按下“CSV”按钮后，将从结果缓存中构建CRA报表的CSV格式并返回到您的浏览器。 根据您的浏览器设置，此报告将自动下载为默认名称为的文件 `results.csv`。 如果缓存已过期，则在构建和下载CSV文件之前将重新生成报告。

请按照以下步骤从AEM实例生成摘要报告的CSV格式：

1. 
   1. 选择Adobe Experience Manager并导航到工具->操 **作** -> **云就绪性分析器**。

1. 报告可用后，单击 **CSV** ，以逗号分隔值(CSV)格式下载完整的摘要报告，如下图所示。

   ![图像](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/cra-3.png)

报告的CSV格式包括从“模式检测器”输出生成的信息，这些信息按类别类型、子类型和重要性级别进行排序和组织。 其格式适合在Microsoft Excel等应用程序中查看和编辑。 它旨在以可重复的格式提供所有查找信息，在比较报告以衡量进度时，这些信息会很有帮助。

CSV格式报告的列有：

* **代码**: 类别
* **类型**: 类别名
* **子类型**: 类别子类型
* **重要性**: 重要性级别
* **标识符**: 查找结果的主要标识符
* **其他**: 有关查找结果的其他信息
* **消息**: 为查找结果提供的消息
* **moreInfo**: 可用于访问有关类别的联机帮助的链接
* **上下文**: 查找数据的JSON字符串

单个查找结果的列中的值“\N”表示未提供任何数据。

## HTTP接口 {#http-interface}

CRA提供HTTP界面，可用作AEM用户界面的替代界面。 该接口支持HEAD和GET命令。 它可用于生成CRA报告并以三种格式之一返回： JSON、CSV和制表符分隔值(TSV)。

以下URL可用于HTTP访问，其 `<host>` 中是安装CRA的服务器的主机名和端口（如果需要）:
* `http://<host>/apps/readiness-analyzer/analysis/result.json` for JSON format
* `http://<host>/apps/readiness-analyzer/analysis/result.csv` 格式
* `http://<host>/apps/readiness-analyzer/analysis/result.tsv` for TSV format

### 执行HTTP请求 {#executing-http-request}

HTTP接口可用于多种方法。

一种简单的方法是在您以管理员身份登录AEM的同一浏览器中打开浏览器选项卡。 您可以在浏览器选项卡中输入URL，并让浏览器显示或下载结果。

您还可以使用命令行工具，如 `curl` 或 `wget` 任何HTTP客户端应用程序。 当不在经过身份验证的会话中使用浏览器选项卡时，必须在评论中提供管理用户名和密码。 以下是如何实现此操作的示例：
`curl -u admin:admin 'http://localhost:4502/apps/readiness-analyzer/analysis/result.csv' > result.csv`

### 标题和参数 {#http-headers-and-parameters}

此接口使用以下HTTP头：

* `Cache-Control: max-age=<seconds>`: 以秒为单位指定缓存刷新时间。 (请参 [阅RFC 7234](https://tools.ietf.org/html/rfc7234#section-5.2.2.8)。)
* `Prefer: respond-async`: 指示服务器应异步响应。 (请参 [阅RFC 7240](https://tools.ietf.org/html/rfc7240#section-4.1)。)

当可能不能轻松使用HTTP头时，以下HTTP查询参数可用：

* `max-age` （数字，可选）: 以秒为单位指定缓存刷新时间。 此数字必须为0或更大。 默认的新鲜度生命周期为86400秒，这意味着如果没有此参数或相应的标头，将使用新缓存在必须重新生成报告之前24小时内为请求提供服务。 使用 `max-age=0` 将强制清除缓存并启动报告的重新生成。 在此请求后，新鲜期将立即重置为上一个非零值。
* `respond-async` （布尔、可选）: 指定应异步提供响应。 当缓 `respond-async=true` 存失效时，使用将导致服务器返回响应，而 `202 Accepted, processing cache` 无需等待生成报告和刷新缓存。 如果缓存是新的，则此参数无效。 默认值是， `false`这意味着如果没有此参数或相应的头，服务器将同步响应，这可能需要大量时间，并且需要调整HTTP客户端的最大响应时间。

当同时存在HTTP头和相应的查询参数时，查询参数优先。

通过HTTP接口启动生成报告的简单方法是使用以下命令：
`curl -u admin:admin 'http://localhost:4502/apps/readiness-analyzer/analysis/result.json?max-age=0&respond-async=true'`

发出请求后，客户端无需保持活动状态即可生成报告。 可以使用HTTP GET请求由一个客户端启动报表生成，生成报表后，可通过另一个客户端的缓存或AEM用户界面中的CSV工具查看。

### 响应(#http-responses)

可以使用以下响应值：

* `200 OK`: 该响应包含来自模式检测器的发现，这些发现在高速缓存的新鲜度寿命内产生。
* `202 Accepted, processing cache`: 为异步响应提供，以指示缓存已过时且正在刷新。
* `400 Bad Request`: 指示请求出错。 “问题详细信息”格式的消息( [请参阅RFC 7807](https://tools.ietf.org/html/rfc7807))提供了更多详细信息。
* `401 Unauthorized`: 请求未获得授权。
* `500 Internal Server Error`: 指示发生内部服务器错误。 “问题详细信息”格式的消息提供更多详细信息。
* `503 Service Unavailable`: 表示服务器正忙于其他响应，无法及时为此请求提供服务。 这只适用于发出同步请求时。 “问题详细信息”格式的消息提供更多详细信息。

## 缓存生命周期调整 {#cache-adjustment}

默认的CRA缓存生命周期为24小时。 在用户界面和HTTP界面中，使用刷新报告和重新生成缓存的选项，此默认值可能适用于大多数CRA使用。 如果AEM实例的报表生成时间特别长，您可能希望调整缓存生命周期以最大限度地减少报表的再生。

缓存生命周期值作为以下存储库 `maxCacheAge` 节点上的属性进行存储：
`/apps/readiness-analyzer/content/CloudReadinessReport/jcr:content`

此属性的值是缓存生命周期（以秒为单位）。 管理员可以使用CRX/DE Lite到AEM的界面调整缓存生命周期。

## 在AEM 6.1实例中查看报表 {#aem-instances-report}

请按照以下步骤下载Adobe Experience Manager(AEM)6.1的CSV报告：

1.使用导 **航到Adobe Experience Manager Web Console配置**`https://serveraddress:serverport/system/console/configMgr`。

1. 选择 **状态** 选项卡，并从下 **拉列表中** 搜索模式检测器，如下图所示。

   ![图像](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/cra-4.png)

1. 您可以以zip文件夹或JSON格式下载摘要报告。


