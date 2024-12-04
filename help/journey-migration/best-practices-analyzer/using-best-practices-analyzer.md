---
title: 使用 Best Practices Analyzer
description: 了解如何使用Best Practices Analyzer了解升级准备情况。
exl-id: e8498e17-f55a-4600-87d7-60584d947897
feature: Migration
role: Admin
source-git-commit: 3a0576e62518240b89290a75752386128b1ab082
workflow-type: tm+mt
source-wordcount: '2724'
ht-degree: 38%

---

# 使用 Best Practices Analyzer {#using-best-practices-analyzer}

>[!CONTEXTUALHELP]
>id="aemcloud_bpa_using"
>title="使用最佳实践分析器"
>abstract="查看使用最佳实践分析器（以前称为云就绪分析器）的文档和生成的报告。最佳实践分析器报告可用于概要了解一般升级就绪性。"
>additional-url="https://my.adobeconnect.com/pqgrfezoxghs?proto=true" text="[网络研讨会] 介绍加速 Adobe Experience Manager as a Cloud Service 历程的工具"

## 使用Best Practices Analyzer的重要注意事项 {#imp-considerations}

请阅读以下章节，以了解运行最佳实践分析器(BPA)时的重要注意事项：

* BPA报告是使用Adobe Experience Manager (AEM) [模式检测器](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/upgrading/pattern-detector.html)的输出生成的。 BPA使用的模式检测器版本包含在BPA安装包中。

* BPA只能由&#x200B;**管理员**&#x200B;用户或&#x200B;**管理员**&#x200B;组中的用户运行。

* 版本6.1及更高版本的AEM实例支持BPA。

  >[!NOTE]
  >有关在AEM 6.1上安装BPA的特殊要求，请参阅[在AEM 6.1上安装](#installing-on-aem61)。

* BPA可以在任何环境中运行，但最好在&#x200B;*暂存*&#x200B;环境中运行它。

  >[!NOTE]
  >为避免对业务关键型实例产生影响，建议您在自定义、配置、内容和用户应用程序方面尽可能接近&#x200B;*生产*&#x200B;环境的&#x200B;*暂存*&#x200B;环境中运行BPA。 或者，也可以在克隆的生产“创作”**&#x200B;环境中运行。

* 生成BPA报告内容可能需要相当长的时间，从几分钟到几小时不等。 具体所需的时间长短很大程度上取决于 AEM 存储库内容的大小和性质、AEM 版本以及其他因素。

* 由于生成报告内容可能需要花费大量时间，这些内容将由后台进程生成并保存在缓存中。查看和下载报告的速度应该相对较快，因为该操作会利用内容缓存，直到报告过期或报告被明确刷新为止。在生成报告内容的过程中，您可以关闭浏览器选项卡，稍后在内容保存到缓存中后，再返回查看报告。

## 可用性 {#availability}

>[!CONTEXTUALHELP]
>id="aemcloud_bpa_download"
>title="下载最佳实践分析器"
>abstract="最佳实践分析器可以从软件分发门户以 zip 文件的形式下载。您可以通过包管理器在源 Adobe Experience Manager (AEM) 实例上安装该包。"

最佳实践分析器可以从软件分发门户以 zip 文件的形式下载。您可以在源Adobe Experience Manager (AEM)实例上通过[包管理器](/help/implementing/developing/tools/package-manager.md)安装包。

>[!NOTE]
>从[软件分发](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)门户下载最佳实践分析器。

## Source环境连接 {#source-environment-connectivity}

源AEM实例可能正在防火墙后面运行，在该防火墙中，它只能访问已添加到允许列表的特定主机。 要将BPA生成的报告自动成功上传到Cloud Acceleration Manager，需要从运行AEM的实例访问以下端点：

* Azure Blob存储服务： `casstorageprod.blob.core.windows.net`


## 查看Best Practices Analyzer报告 {#viewing-report}

### Adobe Experience Manager 6.3.0 和更高版本 {#aem-later-versions}

>[!CONTEXTUALHELP]
>id="aemcloud_cam_bpa_upload_setup"
>title="自动将最佳实践分析器报告上传至 CAM"
>abstract="提供 BPA 上传密钥，以将生成的 BPA 报告自动上传到 Cloud Acceleration Manager（CAM）。"

请参阅此部分，了解如何查看Best Practices Analyzer报告：

1. 选择Adobe Experience Manager并导航到工具> **操作** > **最佳实践分析器**。

   ![最佳实践分析器](/help/journey-migration/best-practices-analyzer/assets/BPA_pic1.png)

1. 单击&#x200B;**生成报告**&#x200B;以执行最佳实践分析器。

   ![生成报告](/help/journey-migration/best-practices-analyzer/assets/BPA_pic2.png)

1. 提供BPA上传密钥，以自动将生成的BPA报告上传到[Cloud Acceleration Manager (CAM)](/help/journey-migration/cloud-acceleration-manager/introduction/benefits-cam.md)。 要获取上传密钥，请导航到CAM中的[最佳实践分析](/help/journey-migration/cloud-acceleration-manager/using-cam/cam-readiness-phase.md#best-practices-analysis)

   ![设置BPA上传密钥](/help/journey-migration/best-practices-analyzer/assets/BPA_upload_key.png)

>[!NOTE]
>您可以通过选择&#x200B;**跳过报告自动上载到CAM**&#x200B;来选择跳过自动上载到CAM。 如果您选择跳过，则需要手动下载BPA报告作为逗号分隔值文件，然后在CAM中上传该文件。 建议使用上传密钥选项，因为它可简化操作。

>[!IMPORTANT]
>当手动上载到CAM时，报表大小限制为大约200MB。 对于较大的报告，您将需要利用自动上传。

1. 提供有效密钥后，**生成**&#x200B;按钮将变为活动状态。 单击&#x200B;**生成**&#x200B;以启动报告生成。

   ![生成报告](/help/journey-migration/best-practices-analyzer/assets/BPA_upload_key1.png)

1. 在BPA生成报告时，您可以在屏幕上看到该工具取得的进展。 它按完成百分比显示进度。 它还会显示分析的项目数以及找到的结果数。

   ![正在生成报告](/help/journey-migration/best-practices-analyzer/assets/BPA_generate_upload.png)

>[!NOTE]
>BPA上传密钥到期时间戳显示在右上角。 您应在BPA上传密钥即将到期时续订该密钥。 若要续订密钥，您可以单击&#x200B;**续订**&#x200B;以导航到CAM来续订密钥。

1. 生成BPA报告后，它以表格形式显示调查结果的摘要和数量，按调查结果类型和重要性级别进行整理。 要获取有关特定发现结果的更多详细信息，您可以单击与表中发现结果类型对应的数字。

   ![报告概述](/help/journey-migration/best-practices-analyzer/assets/BPA_report_upload.png)

1. 您可以通过单击&#x200B;**导出到CSV**，选择下载逗号分隔值(CSV)格式的报表。 您还可以通过单击&#x200B;**转到CAM**&#x200B;在CAM中查看报告。 这将带您进入CAM中的[最佳实践分析](/help/journey-migration/cloud-acceleration-manager/using-cam/cam-readiness-phase.md#best-practices-analysis)页面。

您可以通过单击&#x200B;**刷新报告**，强制BPA清除其缓存并重新生成报告。

![刷新报告](/help/journey-migration/best-practices-analyzer/assets/BPA_report_upload.png)

1. 如果缓存过期，您可以选择在CAM中查看上次生成的报告，方法是单击&#x200B;**在CAM中查看上次生成的报告**，或者单击&#x200B;**生成新报告**&#x200B;启动新的报告生成。

![无报告](/help/journey-migration/best-practices-analyzer/assets/BPA_regeneratereport.png)


#### 在最佳实践分析器报告中使用过滤器 {#bpa-filters}

要筛选出与[ACS Commons](https://adobe-consulting-services.github.io/acs-aem-commons/)相关的发现，请执行以下步骤：

1. 单击页面左侧的左边栏图标。 这将显示&#x200B;**ACS Commons筛选器**。 单击&#x200B;**ACS Commons Filter**&#x200B;以显示交互式复选框，如下图所示。

   ![ACS Commons筛选器](/help/journey-migration/best-practices-analyzer/assets/report_filter_1.png)

   >[!NOTE]
   >仅当BPA检测到使用了ACS Commons时，才会显示左边栏图标。

1. 取消选中该框可筛选掉所有与ACS Commons相关的发现。 您应该会在报表中看到&#x200B;**已过滤的发现结果计数**，如下图所示。 当以逗号分隔值(CSV)格式导出时，也会将该过滤器应用于报表。

   ![已过滤的发现结果计数](/help/journey-migration/best-practices-analyzer/assets/report_filter_2.png)

   >[!NOTE]
   >不应忽略ACS Commons调查结果。 请参阅[文档](https://adobe-consulting-services.github.io/acs-aem-commons/pages/compatibility.html#aem-as-a-cloud-service-feature-incompatibility)以确定与AEM as a Cloud Service的兼容性。

<!--
### Adobe Experience Manager 6.2 and 6.1 {#aem-specific-versions}
 
The Best Practices Analyzer tool is limited in Adobe Experience Manager 6.2 to a link that generates and downloads the CSV report.

For Adobe Experience Manager 6.1, the tool is not functional and only the HTTP interface may be used.

>[!NOTE]
>In all versions, the included Pattern Detector may run independently.
-->

## 解读最佳实践分析器报告 {#cra-report}

>[!CONTEXTUALHELP]
>id="aemcloud_bpa_interpreting"
>title="解读最佳实践分析器报告"
>abstract="在查看 BPA 报告输出时有两个选项：UI 和 CSV。在 AEM 实例中运行最佳实践分析器工具后，UI 报告将作为结果显示在工具窗口中。CSV 格式的报告包括从模式检测器输出生成的信息，这些信息按类别类型、子类型和重要性级别进行排序和组织。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-readiness-phase.html#analysis-report" text="审核最佳实践分析报告"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-pattern-detection/table-of-contents/aso.html" text="了解最佳实践分析器报告类别"

在AEM实例中运行最佳实践分析器工具时，报告将作为结果显示在工具窗口中。

报告的格式为：

* **报告概述**：有关报告本身的信息，包括以下内容：
   * **报告时间**：生成并首次提供报告内容的时间。
   * **过期时间**：报告内容缓存过期的时间。
   * **生成时间段**：报告内容生成过程所花费的时间。
   * **发现结果计数**：报告中包含的发现结果总数。
* **系统概述**：有关运行BPA的AEM系统的信息。
* **发现结果类别**：多个部分，每个部分提供同一类别的一个或多个发现结果。每个部分包括：类别名称、子类型、发现结果计数和重要性、摘要、指向类别文档的链接以及单个发现结果信息。

每个发现结果都分配有一个重要性级别，以指示粗略的操作优先级。

>[!NOTE]
>要了解有关每个发现结果类别的更多信息，请参阅[模式检测器类别](https://experienceleague.adobe.com/docs/experience-manager-pattern-detection/table-of-contents/aso.html)。

请参阅下表，了解重要性级别：

| 重要性 | 描述 |
|--- |--- |
| 信息 | 此发现结果仅供参考。 |
| 建议 | 此发现结果可能是一个升级问题。建议进一步调查。 |
| 主要 | 此发现结果可能是一个应解决的升级问题。 |
| 关键 | 此发现结果极有可能是一个必须解决的升级问题，以防止功能或性能丢失。 |

## 解释最佳实践分析器CSV报告 {#cra-csv-report}

当您从AEM实例单击&#x200B;**CSV**&#x200B;选项时，将从内容缓存生成CSV格式的最佳实践分析器报告，并将该报告返回到您的浏览器。 根据您的浏览器设置，此报表将自动下载为默认名称为`results.csv`的文件。

如果缓存已过期，则在生成并下载CSV文件之前会重新生成报表。

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

## HTTP接口 {#http-interface}

BPA提供了一个HTTP接口，可用作其AEM用户界面的替代方法。 该接口支持 HEAD 和 GET 命令。它可用于生成BPA报告，并以三种格式之一返回报告：JSON、CSV和制表符分隔值(TSV)。

以下URL可用于HTTP访问，其中`<host>`是安装BPA的服务器的主机名和端口（如果需要）：
* `http://<host>/apps/best-practices-analyzer/analysis/report.json`（对于 JSON 格式）
* `http://<host>/apps/best-practices-analyzer/analysis/report.csv`（对于 CSV 格式）
* `http://<host>/apps/best-practices-analyzer/analysis/report.tsv`（对于 TSV 格式）

### 执行HTTP请求 {#executing-http-request}

HTTP 接口可用于多种方法。

一种简单的方法是，在您已经以管理员身份登录 AEM 的同一浏览器中打开一个浏览器选项卡。您可以在该浏览器选项卡中输入 URL，并让浏览器显示或下载结果。

您还可以使用命令行工具，如`curl`或`wget`以及任何HTTP客户端应用程序。 如果不将浏览器选项卡用于经过身份验证的会话，则必须在注释中提供管理用户名和密码。

以下是如何实现此操作的示例：
`curl -u admin:admin 'http://localhost:4502/apps/best-practices-analyzer/analysis/report.csv' > report.csv`。

### 标题和参数 {#http-headers-and-parameters}

此接口使用以下 HTTP 标头：

* `Cache-Control: max-age=<seconds>`：指定缓存刷新生命周期（以秒为单位）。 （请参阅 [RFC 7234](https://tools.ietf.org/html/rfc7234#section-5.2.2.8)。）
* `Prefer: respond-async`：指定服务器应异步响应。 （请参阅 [RFC 7240](https://tools.ietf.org/html/rfc7240#section-4.1)。）
* `Prefer: return=minimal`：指定服务器应返回最小响应。 （请参阅 [RFC 7240](https://tools.ietf.org/html/rfc7240#section-4.2)。）

当不能轻松使用 HTTP 标头时，可以方便地使用以下 HTTP 查询参数：

* `max-age` （数字，可选）：以秒为单位指定缓存刷新生命周期。 此数字必须为 0 或更大。默认的刷新生命周期为86400秒。 如果没有此参数或相应的标头，新的缓存将用于服务24小时的请求，此时必须重新生成缓存。 使用`max-age=0`将强制清除缓存，并使用新生成的缓存的先前非零刷新生命周期开始重新生成报告。
* `respond-async` （布尔值，可选）：指定应异步提供响应。 在缓存失效时使用`respond-async=true`将导致服务器返回`202 Accepted`的响应，而无需等待缓存刷新和生成报告。 如果缓存是新的，则此参数不起作用。默认值为`false`。 如果没有此参数或相应的标头，服务器将同步响应，这可能需要大量时间，并且需要调整HTTP客户端的最大响应时间。
* `may-refresh-cache` （布尔值，可选）：指定如果当前缓存为空、已失效或即将失效，服务器可以刷新缓存以响应请求。 如果`may-refresh-cache=true`或未指定，则服务器可能会启动后台任务，该任务将调用模式检测器并刷新缓存。 如果`may-refresh-cache=false`，则服务器将不会启动任何刷新任务，否则如果缓存为空或过时（在此情况下报表为空）就会完成这些刷新任务。 此参数不会影响任何已在处理的刷新任务。
* `return-minimal` （布尔值，可选）：指定来自服务器的响应应仅包含包含进度指示的状态和采用JSON格式的缓存状态。 如果为`return-minimal=true`，则响应正文仅限于状态对象。 如果`return-minimal=false`或未指定，则会提供完整的响应。
* `log-findings` （布尔值，可选）：指定服务器在首次生成或刷新缓存时应记录缓存的内容。 缓存中的每个发现结果都记录为JSON字符串。 只有在`log-findings=true`且请求生成新缓存时，才会进行此日志记录。

当同时存在 HTTP 标头和相应的查询参数时，将优先采用查询参数。

通过 HTTP 接口开始生成报告的简单方法是使用以下命令：
`curl -u admin:admin 'http://localhost:4502/apps/best-practices-analyzer/analysis/report.json?max-age=0&respond-async=true'`。

发出请求后，客户端无需保持活动状态即可生成报告。可以在一个客户端中使用HTTPGET请求启动报告生成操作；生成报告后，可在缓存中使用另一个客户端或AEM用户界面中的BPA工具进行查看。

### 响应 {#http-responses}

可以使用以下响应值：

* `200 OK`：指示响应包含来自模式检测器的发现结果，这些发现结果在缓存的刷新生命周期内生成。
* `202 Accepted`：用于指示缓存已过时。 当`respond-async=true`和`may-refresh-cache=true`时，此响应表示正在执行刷新任务。 当`may-refresh-cache=false`时，此响应仅指示缓存已过时。
* `400 Bad Request`：指示请求出错。以“问题详细信息”格式显示的消息（请参阅[RFC 7807](https://tools.ietf.org/html/rfc7807)）提供了更多详细信息。
* `401 Unauthorized`：表示请求未获得授权。
* `500 Internal Server Error`：指示发生内部服务器错误。以“问题详细信息”格式显示的消息提供了更多详细信息。
* `503 Service Unavailable`：指示服务器正忙于其他响应，无法及时为此请求提供服务。仅当发出同步请求时，才可能出现此响应。以“问题详细信息”格式显示的消息提供了更多详细信息。

## 管理员信息

### 缓存生命周期调整 {#cache-adjustment}

默认的BPA缓存生命周期为24小时。 在AEM实例和HTTP接口中都有用于刷新报告和重新生成缓存的选项，此默认值可能适用于BPA的大多数使用情况。 如果AEM实例的报告生成时间特别长，则可能需要调整缓存生命周期以最大限度地减少报告的重新生成。

缓存生命周期值作为 `maxCacheAge` 属性存储在以下存储库节点上：
`/apps/best-practices-analyzer/content/BestPracticesReport/jcr:content`

此属性的值便是缓存生命周期（以秒为单位）。管理员可以使用 CRX/DE Lite 调整缓存生命周期。

### 在AEM 6.1上安装 {#installing-on-aem61}

BPA利用名为`repository-reader-service`的系统服务用户帐户来执行模式检测器。 此帐户在 AEM 6.2 和更高版本上可用。在AEM 6.1上，必须在安装BPA *之前*&#x200B;通过执行以下步骤来创建此帐户：

1. 按照[创建新服务用户](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security-service-users.html#creating-a-new-service-user)中的说明创建用户。将用户 ID 设置为 `repository-reader-service`，并将“中间路径”留空，然后单击绿色复选标记。

2. 按照[管理用户和组](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security.html#managing-users-and-groups)中的说明（特别是有关将用户添加到组的说明），将 `repository-reader-service` 用户添加到 `administrators` 组。

3. 通过包管理器在源AEM实例上安装BPA包。 （这将为 `repository-reader-service` 系统服务用户的 ServiceUserMapper 配置添加必要的配置修正。）
