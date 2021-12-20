---
title: 使用最佳实践分析器
description: 使用最佳实践分析器
source-git-commit: a6d225943c5d23ebd960fda0b0912a81f1f80014
workflow-type: tm+mt
source-wordcount: '2470'
ht-degree: 41%

---

# 使用最佳实践分析器 {#using-best-practices-analyzer}

>[!CONTEXTUALHELP]
>id="aemcloud_bpa_using"
>title="使用最佳实践分析器"
>abstract="查看有关使用最佳实践分析器（以前称为云就绪分析器）的文档和生成的报告。 最佳实践分析器报告用于深入了解一般升级就绪性。"
>additional-url="https://my.adobeconnect.com/pqgrfezoxghs?proto=true" text="[Webinar] Introducing Tools to Accelerate the Journey to Adobe Experience Manager as a Cloud Service"

## 使用最佳实践分析器的重要注意事项 {#imp-considerations}

请阅读以下章节，了解运行最佳实践分析器(BPA)的重要注意事项：

* BPA报告是使用Adobe Experience Manager(AEM)的输出生成的 [图案检测器](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/upgrading/pattern-detector.html). BPA使用的模式检测器版本包含在BPA安装包中。

* BPA只能由 **管理员** 用户或 **管理员** 群组。

* 版本6.1及更高版本的AEM实例支持BPA。

   >[!NOTE]
请参阅 [在AEM 6.1上安装](#installing-on-aem61) 在AEM 6.1上安装BPA的特殊要求。

* BPA可在任何环境中运行，但最好在 *阶段* 环境。

   >[!NOTE]
为避免对业务关键型实例产生影响，建议您在 *作者* 尽可能靠近的环境 *生产* 环境中的自定义、配置、内容和用户应用程序。 或者，也可以在克隆的生产“创作”**&#x200B;环境中运行。

* 生成BPA报告内容可能需要相当长的时间，从几分钟到几小时不等。 具体所需的时间长短很大程度上取决于 AEM 存储库内容的大小和性质、AEM 版本以及其他因素。

* 由于生成报告内容可能需要花费大量时间，这些内容将由后台进程生成并保存在缓存中。查看和下载报告的速度应该相对较快，因为该操作会利用内容缓存，直到报告过期或报告被明确刷新为止。在生成报告内容的过程中，您可以关闭浏览器选项卡，稍后在内容保存到缓存中后，再返回查看报告。

## 可用性 {#availability}

[!CONTEXTUALHELP]
id="aemcloud_bpa_download"
title="下载Best Practices Analyzer"
abstract="可以从软件分发门户以zip文件的形式下载最佳实践分析器。 您可以通过包管理器在源 Adobe Experience Manager (AEM) 实例上安装该包。"

可以从软件分发门户以zip文件的形式下载最佳实践分析器。 您可以通过 [包管理器](/help/implementing/developing/tools/package-manager.md) 在源Adobe Experience Manager(AEM)实例上。

>[!NOTE]
从下载最佳实践分析器 [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html) 门户。

## 查看最佳实践分析器报告 {#viewing-report}

### Adobe Experience Manager 6.3.0 和更高版本 {#aem-later-versions}

请阅读本节内容，了解如何查看“最佳实践分析器”报告：

1. 选择Adobe Experience Manager并导航到工具 — > **操作** -> **Best Practices Analyzer**.

   ![图像](/help/journey-migration/best-practices-analyzer/assets/BPA_pic1.png)

1. 单击 **生成报表** 以执行最佳实践分析器。

   ![图像](/help/journey-migration/best-practices-analyzer/assets/BPA_pic2.png)

1. 当BPA生成报表时，您可以在屏幕上看到该工具取得的进展。 它显示分析的项目数，还显示找到的发现结果数。

   ![图像](/help/journey-migration/best-practices-analyzer/assets/BPA_pic3.png)


1. 生成BPA报告后，它会以表格形式显示调查结果的摘要和数量，按调查结果类型和重要性级别进行组织。 要获取有关特定查找结果的更多详细信息，您可以单击表中与查找结果类型对应的编号。

   ![图像](/help/journey-migration/best-practices-analyzer/assets/BPA_pic4.png)

   上述操作将自动滚动到该发现结果在报表中的位置。

   ![图像](/help/journey-migration/best-practices-analyzer/assets/BPA_pic5.png)

1. 您可以通过单击 **导出到CSV**，如下图所示。

   ![图像](/help/journey-migration/best-practices-analyzer/assets/BPA_pic6.png)

   >[!NOTE]
您可以通过单击 **刷新报表**.

   ![图像](/help/journey-migration/best-practices-analyzer/assets/BPA_pic7.png)

   >[!NOTE]
在重新生成报告时，报告会以完成百分比显示进度，如下图所示。

   ![图像](/help/journey-migration/best-practices-analyzer/assets/BPA_pic8.png)



#### 在“最佳实践分析器”报告中使用过滤器 {#bpa-filters}

筛选与 [ACS Commons](https://adobe-consulting-services.github.io/acs-aem-commons/)，请执行以下步骤：

1. 单击页面左侧的左边栏图标。 这将显示 **ACS Commons过滤器**. 单击 **ACS Commons过滤器** 以显示交互式复选框，如下图所示。

   ![图像](/help/journey-migration/best-practices-analyzer/assets/report_filter_1.png)

   >[!NOTE]
仅当BPA检测到ACS Commons的使用情况时，才会显示左边栏图标。

1. 取消选中该框可筛选与ACS Commons相关的所有发现结果。 您应会看到 **筛选的发现结果计数** 如下图所示。 以逗号分隔值(CSV)格式导出报表时，该过滤器也会应用于报表。

   ![图像](/help/journey-migration/best-practices-analyzer/assets/report_filter_2.png)

   >[!NOTE]
不应忽视ACS Commons的调查结果。 请参阅 [文档](https://adobe-consulting-services.github.io/acs-aem-commons/pages/compatibility.html#aem-as-a-cloud-service-feature-incompatibility) 以确定与AEMas a Cloud Service的兼容性。


<!--
### Adobe Experience Manager 6.2 and 6.1 {#aem-specific-versions}
 
The Best Practices Analyzer tool is limited in Adobe Experience Manager 6.2 to a link that generates and downloads the CSV report.

For Adobe Experience Manager 6.1, the tool is not functional and only the HTTP interface may be used.

>[!NOTE]
>In all versions, the included Pattern Detector may run independently.
-->

## 解释最佳实践分析器报告 {#cra-report}

[!CONTEXTUALHELP]
id="aemcloud_bpa_interpreting"
title="解释最佳实践分析器报告"
abstract="查看BPA报表输出有两个选项：UI和CSV。 在AEM实例中运行“最佳实践分析器”工具时，UI报告将作为结果显示在工具窗口中。 CSV 格式的报告包括从模式检测器输出生成的信息，这些信息按类别类型、子类型和重要性级别进行排序和组织。"
additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-readiness-phase.html?lang=en#analysis-report" text="查看最佳实践分析报表"
additional-url="https://experienceleague.adobe.com/docs/experience-manager-pattern-detection/table-of-contents/aso.html?lang=en" text="了解最佳实践分析器报告类别"

在AEM实例中运行“最佳实践分析器”工具时，报告将作为结果显示在工具窗口中。

报告的格式为：

* **报告概述**：有关报告本身的信息，包括以下内容：
   * **报告时间**：生成并首次提供报告内容的时间。
   * **过期时间**：报告内容缓存过期的时间。
   * **生成时间段**：报告内容生成过程所花费的时间。
   * **发现结果计数**：报告中包含的发现结果总数。
* **系统概述**:有关运行BPA的AEM系统的信息。
* **发现结果类别**：多个部分，每个部分提供同一类别的一个或多个发现结果。每个部分包括：类别名称、子类型、发现结果计数和重要性、摘要、指向类别文档的链接以及单个发现结果信息。

每个发现结果都分配有一个重要性级别，以指示粗略的操作优先级。

>[!NOTE]
要详细了解每个“查找”类别，请参阅 [模式检测器类别](https://experienceleague.adobe.com/docs/experience-manager-pattern-detection/table-of-contents/aso.html).

请参阅下表，了解重要性级别：

| 重要性 | 描述 |
|--- |--- |
| 信息 | 此发现结果仅供参考。 |
| 建议 | 此发现结果可能是一个升级问题。建议进一步调查。 |
| 主要 | 此发现结果可能是一个应解决的升级问题。 |
| 关键 | 此发现结果极有可能是一个必须解决的升级问题，以防止功能或性能丢失。 |


## 解释最佳实践分析器CSV报告 {#cra-csv-report}

当您单击 **CSV** 选项，则“最佳实践分析器”报告的CSV格式将从内容缓存生成，并返回到您的浏览器。 根据您的浏览器设置，此报告将自动下载为默认名称为 `results.csv` 的文件。

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

BPA提供了HTTP接口，可用作AEM中用户界面的替代方法。 该接口支持 HEAD 和 GET 命令。它可用于生成BPA报告，并以三种格式之一返回：JSON、CSV和制表符分隔值(TSV)。

以下URL可用于HTTP访问，其中 `<host>` 是安装BPA的服务器的主机名和端口（如果需要）：
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

* `Cache-Control: max-age=<seconds>`:以秒为单位指定缓存刷新生命周期。 （请参阅 [RFC 7234](https://tools.ietf.org/html/rfc7234#section-5.2.2.8)。）
* `Prefer: respond-async`:指定服务器应异步响应。 （请参阅 [RFC 7240](https://tools.ietf.org/html/rfc7240#section-4.1)。）
* `Prefer: return=minimal`:指定服务器应返回最小响应。 （请参阅 [RFC 7240](https://tools.ietf.org/html/rfc7240#section-4.2)。）

当不能轻松使用 HTTP 标头时，可以方便地使用以下 HTTP 查询参数：

* `max-age` （数字，可选）：以秒为单位指定缓存刷新生命周期。 此数字必须为 0 或更大。默认的刷新生命周期为86400秒。 如果没有此参数或相应的标头，则新的缓存将用于在24小时内为请求提供服务，此时必须重新生成缓存。 使用 `max-age=0` 将使用新生成的缓存之前的非零刷新生命周期，强制清除缓存并开始重新生成报告。
* `respond-async` （布尔，可选）：指定应异步提供响应。 使用 `respond-async=true` 当缓存失效时，将导致服务器返回 `202 Accepted` 无需等待缓存刷新和报告生成。 如果缓存是新的，则此参数不起作用。默认值为 `false`.如果没有此参数或相应的标头，服务器将同步响应，这可能需要大量时间，并且需要调整HTTP客户端的最大响应时间。
* `may-refresh-cache` （布尔，可选）：指定当前缓存为空、失效或即将失效时，服务器可以响应请求刷新缓存。 如果 `may-refresh-cache=true`或者，如果未指定，则服务器可以启动后台任务，该任务将调用模式检测器并刷新缓存。 如果 `may-refresh-cache=false` 那么，服务器将不会启动任何刷新任务，否则，如果缓存为空或失效，则会执行该任务，在这种情况下，报表将为空。 任何已在处理中的刷新任务将不会受到此参数的影响。
* `return-minimal` （布尔，可选）：指定来自服务器的响应应仅包含包含JSON格式进度指示和缓存状态的状态。 如果 `return-minimal=true`，则响应主体将限制为状态对象。 如果 `return-minimal=false`，或者如果未指定，则将提供完整响应。
* `log-findings` （布尔，可选）：指定服务器应在首次构建或刷新缓存时记录缓存的内容。 缓存中的每个发现结果都将记录为JSON字符串。 仅当 `log-findings=true` 并且该请求会生成一个新缓存。

当同时存在 HTTP 标头和相应的查询参数时，将优先采用查询参数。

通过 HTTP 接口开始生成报告的简单方法是使用以下命令：
`curl -u admin:admin 'http://localhost:4502/apps/best-practices-analyzer/analysis/report.json?max-age=0&respond-async=true'`。

发出请求后，客户端无需保持活动状态即可生成报告。可以使用HTTPGET请求在一个客户端中启动报告生成，生成报告后，可以使用另一个客户端或AEM用户界面中的BPA工具从缓存中查看报告生成。

### 响应 {#http-responses}

可以使用以下响应值：

* `200 OK`:指示响应包含来自模式检测器的发现结果，这些发现结果在缓存的刷新生命周期内生成。
* `202 Accepted`:用于指示缓存已失效。 When `respond-async=true` 和 `may-refresh-cache=true` 此响应表示正在执行刷新任务。 When `may-refresh-cache=false` 此响应仅表示缓存已失效。
* `400 Bad Request`：指示请求出错。以“问题详细信息”格式显示的消息(请参阅 [RFC 7807](https://tools.ietf.org/html/rfc7807))提供更多详细信息。
* `401 Unauthorized`:表示请求未获得授权。
* `500 Internal Server Error`：指示发生内部服务器错误。以“问题详细信息”格式显示的消息提供了更多详细信息。
* `503 Service Unavailable`：指示服务器正忙于其他响应，无法及时为此请求提供服务。仅当发出同步请求时，才可能出现此响应。以“问题详细信息”格式显示的消息提供了更多详细信息。

## 管理员信息

### 缓存生命周期调整 {#cache-adjustment}

默认的BPA缓存生命周期为24小时。 在AEM实例和HTTP接口中都具有用于刷新报告和重新生成缓存的选项，此默认值可能适用于BPA的大多数使用。 如果 AEM 实例的报告生成时间特别长，您可能希望调整缓存生命周期以最大限度地减少报告的重新生成。

缓存生命周期值作为 `maxCacheAge` 属性存储在以下存储库节点上：
`/apps/best-practices-analyzer/content/BestPracticesReport/jcr:content`

此属性的值便是缓存生命周期（以秒为单位）。管理员可以使用 CRX/DE Lite 调整缓存生命周期。

### 在 AEM 6.1 上安装 {#installing-on-aem61}

BPA利用名为的系统服务用户帐户 `repository-reader-service` 以执行模式检测器。 此帐户在 AEM 6.2 和更高版本上可用。在AEM 6.1上，必须创建此帐户 *之前* 安装BPA，方法如下：

1. 按照[创建新服务用户](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security-service-users.html#creating-a-new-service-user)中的说明创建用户。将用户 ID 设置为 `repository-reader-service`，并将“中间路径”留空，然后单击绿色复选标记。

2. 按照[管理用户和组](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security.html#managing-users-and-groups)中的说明（特别是有关将用户添加到组的说明），将 `repository-reader-service` 用户添加到 `administrators` 组。

3. 通过包管理器在源AEM实例上安装BPA包。 （这将为 `repository-reader-service` 系统服务用户的 ServiceUserMapper 配置添加必要的配置修正。）
