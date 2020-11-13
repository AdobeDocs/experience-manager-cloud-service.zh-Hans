---
title: 使用最佳实践分析器
description: 使用最佳实践分析器
translation-type: tm+mt
source-git-commit: ca6ee9c820c67b68c7498f2b0bad8c650b00562e
workflow-type: tm+mt
source-wordcount: '2207'
ht-degree: 47%

---


# 使用最佳实践分析器 {#using-best-practices-analyzer}

## 使用最佳实践分析器的重要注意事项 {#imp-considerations}

请按照以下部分了解运行最佳实践分析器(BPA)的重要注意事项：

* The BPA report is built using the output of the Adobe Experience Manager (AEM) [Pattern Detector](https://docs.adobe.com/content/help/zh-Hans/experience-manager-65/deploying/upgrading/pattern-detector.html). BPA使用的图案检测器版本包含在BPA安装包中。

* BPA may only be run by the **admin** user or a user in the **administrators** group.

* BPA在版本6.1及更高版本的AEM实例上受支持。

   >[!NOTE]
   > Please see [Installing on AEM 6.1](#installing-on-aem61) for special requirements for installing BPA on AEM 6.1.

* BPA can run on any environment, but it is preferred to have it run on a *Stage* environment.

   >[!NOTE]
   >In order to avoid an impact on business critical instances, it is recommended that you run BPA on an *Author* environment that is as close as possible to the *Production* environment in the areas of customizations, configurations, content and user applications. 或者，也可以在克隆的生产“创作”**&#x200B;环境中运行。

* 生成BPA报告内容可能需要花费大量时间，从几分钟到几小时。 具体所需的时间长短很大程度上取决于 AEM 存储库内容的大小和性质、AEM 版本以及其他因素。

* 由于生成报告内容可能需要花费大量时间，这些内容将由后台进程生成并保存在缓存中。查看和下载报告的速度应该相对较快，因为该操作会利用内容缓存，直到报告过期或报告被明确刷新为止。在生成报告内容的过程中，您可以关闭浏览器选项卡，稍后在内容保存到缓存中后，再返回查看报告。

## 可用性 {#availability}

最佳实践分析器可以从软件分发门户下载为zip文件。 您可以通过包管理器在源 Adobe Experience Manager (AEM) 实例上安装该包。

>[!NOTE]
>Download the Best Practices Analyzer from the [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html) portal.

## 查看最佳实践分析器报告 {#viewing-report}

### Adobe Experience Manager 6.3.0 和更高版本 {#aem-later-versions}

请按照本节学习如何视图最佳实践分析器报告：

1. Select Adobe Experience Manager and navigate to tools -> **Operations** -> **Best Practices Analyzer**.

   ![图像](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/BPA_pic1.png)

1. 单击“ **生成报告** ”以执行最佳实践分析器。

   ![图像](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/BPA_pic2.png)

1. 当BPA生成报表时，您可以在屏幕上看到该工具取得的进展。 它显示分析的项目数，还显示找到的查找结果数。

   ![图像](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/BPA_pic3.png)


1. 生成BPA报告后，它以表格格式显示摘要和结果数，其格式按查找类型和重要性级别进行组织。 要获取有关特定查找结果的更多详细信息，您可以单击表中与查找结果类型对应的编号。

   ![图像](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/BPA_pic4.png)

   上述操作将自动滚动到报告中该查找结果的位置。

   ![图像](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/BPA_pic5.png)

1. You have the option of downloading the report in a comma-separated values (CSV) format by clicking on **CSV**, as shown in the figure below.

   ![图像](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/BPA_pic6.png)

   >[!NOTE]
   >You may force the BPA to clear its cache and regenerate the report by clicking **Refresh Report**.

   ![图像](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/BPA_pic7.png)

   >[!NOTE]
   >在重新生成报表时，它按完成百分比显示进度，如下图所示。

   ![图像](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/BPA_pic8.png)


### Adobe Experience Manager 6.2 和 6.1 {#aem-specific-versions}

在Adobe Experience Manager6.2中，最佳实践分析器工具仅限于生成和下载CSV报告的链接。

在 Adobe Experience Manager 6.1 中，该工具无法正常运行，只能使用 HTTP 接口。

>[!NOTE]
>在所有版本中，包含的模式检测器可以独立运行。

## 解释最佳实践分析器报告 {#cra-report}

在AEM实例中运行最佳实践分析器工具时，报告将作为结果显示在工具窗口中。

报告的格式为：

* **报告概述**：有关报告本身的信息，包括以下内容：
   * **报告时间**：生成并首次提供报告内容的时间。
   * **过期时间**：报告内容缓存过期的时间。
   * **生成时间段**：报告内容生成过程所花费的时间。
   * **发现结果计数**：报告中包含的发现结果总数。
* **系统概述**:关于运行BPA的AEM系统的信息。
* **发现结果类别**：多个部分，每个部分提供同一类别的一个或多个发现结果。每个部分包括：类别名称、子类型、发现结果计数和重要性、摘要、指向类别文档的链接以及单个发现结果信息。

每个发现结果都分配有一个重要性级别，以指示粗略的操作优先级。

>[!NOTE]
>要进一步了解每个“查找”类别，请参 [阅“图案检测器”类别](https://experienceleague.adobe.com/docs/experience-manager-pattern-detection/table-of-contents/aso.html)。

请参阅下表，了解重要性级别：

| 重要性 | 描述 |
|--- |--- |
| 信息 | 此发现结果仅供参考。 |
| 建议 | 此发现结果可能是一个升级问题。建议进一步调查。 |
| 主要 | 此发现结果可能是一个应解决的升级问题。 |
| 关键 | 此发现结果极有可能是一个必须解决的升级问题，以防止功能或性能丢失。 |


## 解释最佳实践分析器CSV报告 {#cra-csv-report}

When you click the **CSV** option from your AEM instance, the CSV format of the Best Practices Analyzer report is built from the content cache and returned to your browser. 根据您的浏览器设置，此报告将自动下载为默认名称为 `results.csv` 的文件。

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

BPA提供HTTP接口，可用作AEM中用户界面的替代。 该接口支持 HEAD 和 GET 命令。它可用于生成BPA报表并以三种格式之一返回它：JSON、CSV和制表符分隔值(TSV)。

The following URLs are available for HTTP access, where `<host>` is the hostname, and port if necessary, of the server on which the BPA is installed:
* `http://<host>/apps/best-practices-analyzer/analysis/report.json`（对于 JSON 格式）
* `http://<host>/apps/best-practices-analyzer/analysis/report.csv`（对于 CSV 格式）
* `http://<host>/apps/best-practices-analyzer/analysis/report.tsv`（对于 TSV 格式）

### 执行 HTTP 请求 {#executing-http-request}

HTTP 接口可用于多种方法。

一种简单的方法是，在您已经以管理员身份登录 AEM 的同一浏览器中打开一个浏览器选项卡。您可以在该浏览器选项卡中输入 URL，并让浏览器显示或下载结果。

您还可以使用命令行工具，如 `curl` 或 `wget`，以及任何 HTTP 客户端应用程序。如果不将浏览器选项卡用于经过身份验证的会话，则必须在注释中提供管理用户名和密码。

以下是如何实现此操作的示例：
`curl -u admin:admin 'http://localhost:4502/apps/best-practices-analyzer/analysis/report.csv' > report.csv`。

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
`curl -u admin:admin 'http://localhost:4502/apps/best-practices-analyzer/analysis/report.json?max-age=0&respond-async=true'`。

发出请求后，客户端无需保持活动状态即可生成报告。报表生成可以由一个客户端使用HTTPGET请求启动，生成报表后，可使用另一个客户端或AEM用户界面中的BPA工具从缓存中查看。

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

默认的BPA缓存生命周期为24小时。 在AEM实例和HTTP接口中，使用刷新报告并重新生成缓存的选项，此默认值可能适用于大多数BPA的使用。 如果 AEM 实例的报告生成时间特别长，您可能希望调整缓存生命周期以最大限度地减少报告的重新生成。

缓存生命周期值作为 `maxCacheAge` 属性存储在以下存储库节点上：
`/apps/best-practices-analyzer/content/BestPracticesReport/jcr:content`

此属性的值便是缓存生命周期（以秒为单位）。管理员可以使用 CRX/DE Lite 调整缓存生命周期。

### 在 AEM 6.1 上安装 {#installing-on-aem61}

BPA utilizes a system service user account named `repository-reader-service` to execute the Pattern Detector. 此帐户在 AEM 6.2 和更高版本上可用。On AEM 6.1, this account must be created *prior to* installation of BPA by taking the following steps:

1. 按照[创建新服务用户](https://docs.adobe.com/content/help/zh-Hans/experience-manager-65/administering/security/security-service-users.html#creating-a-new-service-user)中的说明创建用户。将用户 ID 设置为 `repository-reader-service`，并将“中间路径”留空，然后单击绿色复选标记。

2. 按照[管理用户和组](https://docs.adobe.com/content/help/zh-Hans/experience-manager-65/administering/security/security.html#managing-users-and-groups)中的说明（特别是有关将用户添加到组的说明），将 `repository-reader-service` 用户添加到 `administrators` 组。

3. 在源AEM实例上通过包管理器安装BPA包。 （这将为 `repository-reader-service` 系统服务用户的 ServiceUserMapper 配置添加必要的配置修正。）
