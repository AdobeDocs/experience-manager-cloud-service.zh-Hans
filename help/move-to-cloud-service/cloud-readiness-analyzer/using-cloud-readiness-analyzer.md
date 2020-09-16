---
title: 使用云就绪分析器
description: 使用云就绪分析器
translation-type: tm+mt
source-git-commit: ba2105d389617fe0c7e26642799b3a7dd3adb8a1
workflow-type: tm+mt
source-wordcount: '2091'
ht-degree: 77%

---


# 使用云就绪分析器 {#using-cloud-readiness-analyzer}

## 使用云就绪分析器的重要注意事项 {#imp-considerations}

请参阅以下部分，了解运行云就绪分析器 (CRA) 的重要注意事项：

* CRA 报告是使用 Adobe Experience Manager (AEM) [模式检测器](https://docs.adobe.com/content/help/zh-Hans/experience-manager-65/deploying/upgrading/pattern-detector.html)的输出生成的。CRA 使用的模式检测器版本包含在 CRA 安装包中。

* CRA 只能由&#x200B;**管理员**&#x200B;用户或&#x200B;**管理员**&#x200B;组中的用户运行。

* 版本 6.1 及更高版本的 AEM 实例支持 CRA。

   >[!NOTE]
   > 有关在 AEM 6.1 上安装 CRA 的特殊要求，请参阅[在 AEM 6.1 上安装](#installing-on-aem61)。

* CRA 可以在任何环境中运行，但最好在“暂存”**&#x200B;环境中运行它。

   >[!NOTE]
   >为避免对业务关键型实例产生影响，建议您在自定义、配置、内容和用户应用程序方面尽可能接近“生产”**&#x200B;环境的“创作”**&#x200B;环境中运行 CRA。或者，也可以在克隆的生产“创作”**&#x200B;环境中运行。

* 生成 CRA 报告内容可能需要相当长的时间，从几分钟到几小时不等。具体所需的时间长短很大程度上取决于 AEM 存储库内容的大小和性质、AEM 版本以及其他因素。

* 由于生成报告内容可能需要花费大量时间，这些内容将由后台进程生成并保存在缓存中。查看和下载报告的速度应该相对较快，因为该操作会利用内容缓存，直到报告过期或报告被明确刷新为止。在生成报告内容的过程中，您可以关闭浏览器选项卡，稍后在内容保存到缓存中后，再返回查看报告。

## 可用性 {#availability}

可以从软件分发门户以 zip 文件的形式下载云就绪分析器。您可以通过包管理器在源 Adobe Experience Manager (AEM) 实例上安装该包。

>[!NOTE]
>从[软件分发](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)门户下载云就绪分析器。

## 查看云就绪分析器报告 {#viewing-report}

### Adobe Experience Manager 6.3.0 和更高版本 {#aem-later-versions}

请参阅此部分，了解如何查看云就绪分析器报告：

1. 选择 Adobe Experience Manager 并导航到“工具”-> **操作** -> **云就绪分析器**。

   ![图像](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/cra-1.png)

1. 单击&#x200B;**云就绪分析器**&#x200B;后，该工具将开始生成报告并在报告可用时显示报告。

   >[!NOTE]
   >您必须向下滚动页面才能查看完整报告。

   ![图像](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/cra-tool-1.png)

1. 生成并显示 CRA 报告后，您可以通过单击 **CSV**，选择下载逗号分隔值 (CSV) 格式的报告，如下图所示。

   ![图像](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/cra-tool-2.png)

   >[!NOTE]
   >您可以通过单击&#x200B;**刷新报告**，强制 CRA 清除其缓存并重新生成报告。

### Adobe Experience Manager 6.2 和 6.1 {#aem-specific-versions}

云就绪分析器工具在 Adobe Experience Manager 6.2 中仅限于生成和下载 CSV 报告的链接。

在 Adobe Experience Manager 6.1 中，该工具无法正常运行，只能使用 HTTP 接口。

>[!NOTE]
>在所有版本中，包含的模式检测器可以独立运行。

## 解释云就绪分析器报告 {#cra-report}

在 AEM 实例中运行云就绪分析器工具后，报告将作为结果显示在工具窗口中。

报告的格式为：

* **报告概述**：有关报告本身的信息，包括以下内容：
   * **报告时间**：生成并首次提供报告内容的时间。
   * **过期时间**：报告内容缓存过期的时间。
   * **生成时间段**：报告内容生成过程所花费的时间。
   * **发现结果计数**：报告中包含的发现结果总数。
* **系统概述**：关于运行 CRA 的 AEM 系统的信息。
* **发现结果类别**：多个部分，每个部分提供同一类别的一个或多个发现结果。每个部分包括：类别名称、子类型、发现结果计数和重要性、摘要、指向类别文档的链接以及单个发现结果信息。

每个发现结果都分配有一个重要性级别，以指示粗略的操作优先级。

请参阅下表，了解重要性级别：

| 重要性 | 描述 |
|--- |--- |
| 信息 | 此发现结果仅供参考。 |
| 建议 | 此发现结果可能是一个升级问题。建议进一步调查。 |
| 主要 | 此发现结果可能是一个应解决的升级问题。 |
| 关键 | 此发现结果极有可能是一个必须解决的升级问题，以防止功能或性能丢失。 |


## 解释云就绪分析器 CSV 报告 {#cra-csv-report}

当您从 AEM 实例单击 **CSV** 选项时，将从内容缓存生成 CSV 格式的云就绪分析器报告，并将该报告返回到您的浏览器。根据您的浏览器设置，此报告将自动下载为默认名称为 `results.csv` 的文件。

如果缓存已过期，则将重新生成报告，然后再生成并下载 CSV 文件。

CSV 格式的报告包括从模式检测器输出生成的信息，这些信息按类别类型、子类型和重要性级别进行排序和组织。其格式适合在 Microsoft Excel 等应用程序中查看和编辑。它旨在以可重复的格式提供所有发现结果信息，在比较不同时间的报告以衡量进度时，这些信息很有用。

CSV 格式的报告包含以下列：

* **代码**：类别代码
* **类型**：类别名称
* **子类型**：类别子类型
* **重要性**：重要性级别
* **标识符**：发现结果的主要标识符
* **其他**：有关发现结果的其他信息
* **消息**：为发现结果提供的消息
* **更多信息**：可用于访问有关类别的在线帮助的链接
* **上下文**：发现结果数据的 JSON 字符串

单个发现结果的列中的值“\N”表示未提供任何数据。

## HTTP 接口 {#http-interface}

CRA 提供了 HTTP 接口，可用作 AEM 中的用户界面的替代方式。该接口支持 HEAD 和 GET 命令。它可用于生成 CRA 报告，并以三种格式（JSON、CSV 和制表符分隔值 (TSV)）之一返回报告。

以下 URL 可用于 HTTP 访问，其中 `<host>` 是安装 CRA 的服务器的主机名和端口（如果需要）：
* `http://<host>/apps/readiness-analyzer/analysis/result.json`（对于 JSON 格式）
* `http://<host>/apps/readiness-analyzer/analysis/result.csv`（对于 CSV 格式）
* `http://<host>/apps/readiness-analyzer/analysis/result.tsv`（对于 TSV 格式）

### 执行 HTTP 请求 {#executing-http-request}

HTTP 接口可用于多种方法。

一种简单的方法是，在您已经以管理员身份登录 AEM 的同一浏览器中打开一个浏览器选项卡。您可以在该浏览器选项卡中输入 URL，并让浏览器显示或下载结果。

您还可以使用命令行工具，如 `curl` 或 `wget`，以及任何 HTTP 客户端应用程序。如果不将浏览器选项卡用于经过身份验证的会话，则必须在注释中提供管理用户名和密码。

以下是如何实现此操作的示例：
`curl -u admin:admin 'http://localhost:4502/apps/readiness-analyzer/analysis/result.csv' > result.csv`。

### 标头和参数 {#http-headers-and-parameters}

此接口使用以下 HTTP 标头：

* `Cache-Control: max-age=<seconds>`:以秒为单位指定缓存刷新时间。 （请参阅 [RFC 7234](https://tools.ietf.org/html/rfc7234#section-5.2.2.8)。）
* `Prefer: respond-async`:指定服务器应异步响应。 （请参阅 [RFC 7240](https://tools.ietf.org/html/rfc7240#section-4.1)。）
* `Prefer: return=minimal`:指定服务器应返回最小响应。 （请参阅 [RFC 7240](https://tools.ietf.org/html/rfc7240#section-4.2)。）

当不能轻松使用 HTTP 标头时，可以方便地使用以下 HTTP 查询参数：

* `max-age` （数字，可选）:以秒为单位指定缓存刷新时间。 此数字必须为 0 或更大。默认新鲜度寿命为86400秒。 如果没有此参数或相应的标头，将使用新缓存在24小时内服务请求，此时必须重新生成缓存。 使用 `max-age=0` 将强制清除缓存并启动报表的重新生成，同时使用新生成的缓存以前的非零新鲜寿命。
* `respond-async` （布尔、可选）:指定应异步提供响应。 Using `respond-async=true` when the cache is stale will cause the server to return a response of `202 Accepted` without waiting for the cache to be refreshed and for the report to be generated. 如果缓存是新的，则此参数不起作用。The default value is `false`. Without this parameter or the corresponding header the server will respond synchronously, which may require a significant amount of time and require an adjustment to the maximum response time for the HTTP client.
* `may-refresh-cache` （布尔、可选）:指定当当前缓存为空、过时或即将过时时，服务器可以响应请求刷新缓存。 如 `may-refresh-cache=true`果或未指定，则服务器可启动背景任务，该后台将调用模式检测器并刷新缓存。 如 `may-refresh-cache=false` 果缓存为空或过时，服务器将不启动任何刷新任务，否则，如果缓存为空或过期，则报表将为空。 任何已处理的刷新任务都不会受此参数影响。
* `return-minimal` （布尔、可选）:指定来自服务器的响应应仅包含JSON格式的进度指示和缓存状态的状态。 如 `return-minimal=true`果是，则响应主体将限于状态对象。 如 `return-minimal=false`果或未指定，则将提供完整的响应。
* `log-findings` （布尔、可选）:指定服务器在首次构建或刷新缓存时应记录其内容。 缓存中的每个查找结果都将记录为JSON字符串。 仅当请求生成新缓 `log-findings=true` 存时，才会发生此记录。

当同时存在 HTTP 标头和相应的查询参数时，将优先采用查询参数。

通过 HTTP 接口开始生成报告的简单方法是使用以下命令：
`curl -u admin:admin 'http://localhost:4502/apps/readiness-analyzer/analysis/result.json?max-age=0&respond-async=true'`。

发出请求后，客户端无需保持活动状态即可生成报告。报表生成可以由一个客户端使用HTTPGET请求启动，生成报表后，可以使用另一个客户端或AEM用户界面中的CRA工具从缓存中查看。

### 响应 {#http-responses}

可以使用以下响应值：

* `200 OK`:指示响应包含来自模式检测器的发现，这些发现是在高速缓存的新鲜寿命内生成的。
* `202 Accepted`:用于指示缓存过时。 当和 `respond-async=true` 此 `may-refresh-cache=true` 响应指示正在进行刷新任务。 当此 `may-refresh-cache=false` 响应仅指示缓存过时。
* `400 Bad Request`：指示请求出错。A message in Problem Details format (see [RFC 7807](https://tools.ietf.org/html/rfc7807)) provides more details.
* `401 Unauthorized`:表示请求未获得授权。
* `500 Internal Server Error`：指示发生内部服务器错误。以“问题详细信息”格式显示的消息提供了更多详细信息。
* `503 Service Unavailable`：指示服务器正忙于其他响应，无法及时为此请求提供服务。仅当发出同步请求时，才可能出现此响应。以“问题详细信息”格式显示的消息提供了更多详细信息。

## 管理员信息

### 缓存生命周期调整 {#cache-adjustment}

默认的 CRA 缓存生命周期为 24 小时。在 AEM 实例和 HTTP 接口中都有用于刷新报告和重新生成缓存的选项，此默认值可能适用于 CRA 的大多数使用情况。如果 AEM 实例的报告生成时间特别长，您可能希望调整缓存生命周期以最大限度地减少报告的重新生成。

缓存生命周期值作为 `maxCacheAge` 属性存储在以下存储库节点上：
`/apps/readiness-analyzer/content/CloudReadinessReport/jcr:content`

此属性的值便是缓存生命周期（以秒为单位）。管理员可以使用 CRX/DE Lite 调整缓存生命周期。

### 在 AEM 6.1 上安装 {#installing-on-aem61}

CRA 利用名为 `repository-reader-service` 的系统服务用户帐户来执行模式检测器。此帐户在 AEM 6.2 和更高版本上可用。在 AEM 6.1 上安装 CRA *之前*，必须先通过执行以下步骤来创建此帐户：

1. 按照[创建新服务用户](https://docs.adobe.com/content/help/zh-Hans/experience-manager-65/administering/security/security-service-users.html#creating-a-new-service-user)中的说明创建用户。将用户 ID 设置为 `repository-reader-service`，并将“中间路径”留空，然后单击绿色复选标记。

2. 按照[管理用户和组](https://docs.adobe.com/content/help/zh-Hans/experience-manager-65/administering/security/security.html#managing-users-and-groups)中的说明（特别是有关将用户添加到组的说明），将 `repository-reader-service` 用户添加到 `administrators` 组。

3. 通过包管理器在源 AEM 实例上安装 CRA 包。（这将为 `repository-reader-service` 系统服务用户的 ServiceUserMapper 配置添加必要的配置修正。）
