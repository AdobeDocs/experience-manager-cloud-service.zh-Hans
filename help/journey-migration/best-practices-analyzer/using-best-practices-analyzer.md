---
title: 使用 Best Practices Analyzer
description: 使用 Best Practices Analyzer
exl-id: e8498e17-f55a-4600-87d7-60584d947897
source-git-commit: df1fdbe0f3590708e1da44864b6e08075a521b51
workflow-type: tm+mt
source-wordcount: '2490'
ht-degree: 49%

---

# 使用 Best Practices Analyzer {#using-best-practices-analyzer}

>[!CONTEXTUALHELP]
>id="aemcloud_bpa_using"
>title="使用最佳实践分析器"
>abstract="查看使用最佳实践分析器（以前称为云就绪分析器）的文档和生成的报告。最佳实践分析器报告可用于概要了解一般升级就绪性。"
>additional-url="https://my.adobeconnect.com/pqgrfezoxghs?proto=true" text="[网络研讨会] 介绍加速 Adobe Experience Manager as a Cloud Service 历程的工具"

## 使用Best Practices Analyzer的重要考量 {#imp-considerations}

請依照以下章節瞭解執行Best Practices Analyzer (BPA)的重要考量：

* BPA報告是使用Adobe Experience Manager (AEM)的輸出所建置 [模式偵測器](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/upgrading/pattern-detector.html). BPA使用的模式偵測器版本包含在BPA安裝套件中。

* BPA只能由 **管理員** 使用者或使用者 **管理員** 群組。

* 6.1版及更新版本的AEM執行個體支援BPA。

   >[!NOTE]
   >請參閱 [在AEM 6.1上安裝](#installing-on-aem61) 針對AEM 6.1上安裝BPA的特殊需求。

* BPA可以在任何環境中執行，但最好執行於 *階段* 環境。

   >[!NOTE]
   >為避免對業務關鍵執行個體造成影響，建議您對 *作者* 儘可能靠近 *生產* 自訂、設定、內容和使用者應用程式領域的環境。 或者，也可以在克隆的生产“创作”**&#x200B;环境中运行。

* 產生BPA報告內容可能需要相當長的時間，從幾分鐘到幾小時不等。 具体所需的时间长短很大程度上取决于 AEM 存储库内容的大小和性质、AEM 版本以及其他因素。

* 由于生成报告内容可能需要花费大量时间，这些内容将由后台进程生成并保存在缓存中。查看和下载报告的速度应该相对较快，因为该操作会利用内容缓存，直到报告过期或报告被明确刷新为止。在生成报告内容的过程中，您可以关闭浏览器选项卡，稍后在内容保存到缓存中后，再返回查看报告。

## 可用性 {#availability}

>[!CONTEXTUALHELP]
>id="aemcloud_bpa_download"
>title="下载最佳实践分析器"
>abstract="最佳实践分析器可以从软件分发门户以 zip 文件的形式下载。您可以通过包管理器在源 Adobe Experience Manager (AEM) 实例上安装该包。"

最佳实践分析器可以从软件分发门户以 zip 文件的形式下载。您可以透過以下方式安裝套件 [封裝管理員](/help/implementing/developing/tools/package-manager.md) 在您的來源Adobe Experience Manager (AEM)例項上。

>[!NOTE]
>從下載Best Practices Analyzer [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html) 入口網站。

## 檢視Best Practices Analyzer報表 {#viewing-report}

### Adobe Experience Manager 6.3.0 和更高版本 {#aem-later-versions}

請詳閱本節，瞭解如何檢視Best Practices Analyzer報告：

1. 選取Adobe Experience Manager並導覽至工具 — > **作業** -> **Best Practices Analyzer**.

   ![图像](/help/journey-migration/best-practices-analyzer/assets/BPA_pic1.png)

1. 按一下 **產生報表** 以執行Best Practices Analyzer。

   ![图像](/help/journey-migration/best-practices-analyzer/assets/BPA_pic2.png)

1. 在BPA產生報表時，您可以在畫面上看到工具執行的進度。 它會顯示已分析的專案數，也會顯示找到的結果數。

   ![图像](/help/journey-migration/best-practices-analyzer/assets/BPA_pic3.png)

1. 產生BPA報告後，它會以表格格式顯示結果的摘要和數目，並依結果型別和重要性層級加以整理。 若要取得特定發現專案的詳細資訊，您可以按一下與表格中的發現專案型別相對應的數字。

   ![图像](/help/journey-migration/best-practices-analyzer/assets/BPA_pic4.png)

   上述動作會自動捲動至該結果在報表中的位置。

   ![图像](/help/journey-migration/best-practices-analyzer/assets/BPA_pic5.png)

1. 您可以按一下「 」，選擇下載逗點分隔值(CSV)格式的報表 **匯出至CSV**，如下圖所示。

   ![图像](/help/journey-migration/best-practices-analyzer/assets/BPA_pic6.png)

   >[!NOTE]
   >您可以按一下「 」，強制BPA清除其快取並重新產生報表 **重新整理報告**.

   ![图像](/help/journey-migration/best-practices-analyzer/assets/BPA_pic7.png)

   >[!NOTE]
   >報表在重新產生期間，會以完成百分比顯示進度，如下圖所示。

   ![图像](/help/journey-migration/best-practices-analyzer/assets/BPA_pic8.png)

#### 在Best Practices Analyzer報告中使用篩選器 {#bpa-filters}

若要篩選掉與下列專案相關的發現 [ACS Commons](https://adobe-consulting-services.github.io/acs-aem-commons/)，請遵循下列步驟：

1. 按一下頁面左側的左側邊欄圖示。 這會顯示 **ACS Commons篩選器**. 按一下 **ACS Commons篩選器** 以顯示「互動式」核取方塊，如下圖所示。

   ![图像](/help/journey-migration/best-practices-analyzer/assets/report_filter_1.png)

   >[!NOTE]
   >只有在BPA偵測到ACS Commons的使用時，左側邊欄圖示才會出現。

1. 取消選取此方塊，以篩選掉與ACS Commons相關的所有發現。 您應會看到 **篩選結果計數** 在報表上，如下圖所示。 當篩選器匯出為逗號分隔值(CSV)格式時，也會套用至報表。

   ![图像](/help/journey-migration/best-practices-analyzer/assets/report_filter_2.png)

   >[!NOTE]
   >不應忽略ACS Commons的發現。 請參閱 [檔案](https://adobe-consulting-services.github.io/acs-aem-commons/pages/compatibility.html#aem-as-a-cloud-service-feature-incompatibility) 以判斷與AEMas a Cloud Service的相容性。

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
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-readiness-phase.html?lang=zh-Hans#analysis-report" text="审核最佳实践分析报告"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-pattern-detection/table-of-contents/aso.html?lang=zh-Hans" text="了解最佳实践分析器报告类别"

在 AEM 实例中运行最佳实践分析器工具后， 报告将作为结果显示在工具窗口中。

报告的格式为：

* **报告概述**：有关报告本身的信息，包括以下内容：
   * **报告时间**：生成并首次提供报告内容的时间。
   * **过期时间**：报告内容缓存过期的时间。
   * **生成时间段**：报告内容生成过程所花费的时间。
   * **发现结果计数**：报告中包含的发现结果总数。
* **系統概觀**：有關執行BPA的AEM系統的資訊。
* **发现结果类别**：多个部分，每个部分提供同一类别的一个或多个发现结果。每个部分包括：类别名称、子类型、发现结果计数和重要性、摘要、指向类别文档的链接以及单个发现结果信息。

每个发现结果都分配有一个重要性级别，以指示粗略的操作优先级。

>[!NOTE]
>若要進一步瞭解每個結果類別，請參閱 [模式偵測器類別](https://experienceleague.adobe.com/docs/experience-manager-pattern-detection/table-of-contents/aso.html).

请参阅下表，了解重要性级别：

| 重要性 | 描述 |
|--- |--- |
| 信息 | 此发现结果仅供参考。 |
| 建议 | 此发现结果可能是一个升级问题。建议进一步调查。 |
| 主要 | 此发现结果可能是一个应解决的升级问题。 |
| 关键 | 此发现结果极有可能是一个必须解决的升级问题，以防止功能或性能丢失。 |

## 解譯Best Practices Analyzer CSV報表 {#cra-csv-report}

當您按一下 **CSV** 選項從AEM執行個體中，從內容快取建置CSV格式的Best Practices Analyzer報告並傳回至您的瀏覽器。 根据您的浏览器设置，此报告将自动下载为默认名称为 `results.csv` 的文件。

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

BPA提供HTTP介面，可作為AEM使用者介面的替代介面。 该接口支持 HEAD 和 GET 命令。它可用來產生BPA報表，並以三種格式之一傳回：JSON、CSV和定位字元分隔值(TSV)。

以下URL可用於HTTP存取，其中 `<host>` 是安裝BPA之伺服器的主機名稱及連線埠（如有需要）：
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

* `Cache-Control: max-age=<seconds>`：指定快取時效性存留期（以秒為單位）。 （请参阅 [RFC 7234](https://tools.ietf.org/html/rfc7234#section-5.2.2.8)。）
* `Prefer: respond-async`：指定伺服器應以非同步方式回應。 （请参阅 [RFC 7240](https://tools.ietf.org/html/rfc7240#section-4.1)。）
* `Prefer: return=minimal`：指定伺服器應傳回最小回應。 （请参阅 [RFC 7240](https://tools.ietf.org/html/rfc7240#section-4.2)。）

当不能轻松使用 HTTP 标头时，可以方便地使用以下 HTTP 查询参数：

* `max-age` （數字，選用）：指定快取時效性存留期（以秒為單位）。 此数字必须为 0 或更大。預設的時效性存留期為86400秒。 如果沒有此引數或對應的標頭，新的快取將在24小時內用來處理請求，屆時必須重新產生快取。 使用 `max-age=0` 會強制清除快取，並使用新產生之快取的先前非零時效性存留期，開始重新產生報表。
* `respond-async` （布林值，選用）：指定應以非同步方式提供回應。 使用 `respond-async=true` 當快取過期時，將導致伺服器傳回 `202 Accepted` 而不等待快取重新整理及報表產生。 如果缓存是新的，则此参数不起作用。預設值為 `false`.若沒有此引數或對應的標頭，伺服器將會同步回應，而這可能需要相當長的時間，且需要調整HTTP使用者端的最大回應時間。
* `may-refresh-cache` （布林值，選用）：指定如果目前快取是空的、過時或即將過時，伺服器可能會重新整理快取以回應要求。 若 `may-refresh-cache=true`，或未指定時，伺服器可能會起始背景工作，並叫用模式偵測器並重新整理快取。 若 `may-refresh-cache=false` 之後，伺服器將不會起始任何重新整理工作，否則如果快取為空白或過時（此時報表將是空的）就會完成這項工作。 任何已在處理的重新整理任務都不會受到此引數的影響。
* `return-minimal` （布林值，選用）：指定伺服器的回應應僅包含包含進度指示的狀態，以及JSON格式的快取狀態。 若 `return-minimal=true`，則回應內文將限製為狀態物件。 若 `return-minimal=false`，或若未指定，則會提供完整的回應。
* `log-findings` （布林值，選用）：指定第一次建立或重新整理快取時，伺服器應該記錄快取的內容。 快取中的每個結果都會記錄為JSON字串。 此記錄只會在 `log-findings=true` 而且請求會產生新快取。

当同时存在 HTTP 标头和相应的查询参数时，将优先采用查询参数。

通过 HTTP 接口开始生成报告的简单方法是使用以下命令：
`curl -u admin:admin 'http://localhost:4502/apps/best-practices-analyzer/analysis/report.json?max-age=0&respond-async=true'`。

发出请求后，客户端无需保持活动状态即可生成报告。報表產生作業可以由一個使用者端使用HTTPGET要求來起始，且報表產生後，可由另一個使用者端從快取中檢視，或由AEM使用者介面中的BPA工具檢視。

### 响应 {#http-responses}

可以使用以下响应值：

* `200 OK`：指出此回應包含「模式偵測器」在快取的時效性存留期內產生的結果。
* `202 Accepted`：用於表示快取已過時。 時間 `respond-async=true` 和 `may-refresh-cache=true` 此回應表示重新整理任務正在進行中。 時間 `may-refresh-cache=false` 此回應僅表示快取已過時。
* `400 Bad Request`：指示请求出错。「問題詳細資料」格式的訊息(請參閱 [RFC 7807](https://tools.ietf.org/html/rfc7807))提供詳細資訊。
* `401 Unauthorized`：指出要求未獲授權。
* `500 Internal Server Error`：指示发生内部服务器错误。以“问题详细信息”格式显示的消息提供了更多详细信息。
* `503 Service Unavailable`：指示服务器正忙于其他响应，无法及时为此请求提供服务。仅当发出同步请求时，才可能出现此响应。以“问题详细信息”格式显示的消息提供了更多详细信息。

## 管理员信息

### 缓存生命周期调整 {#cache-adjustment}

預設的BPA快取存留期為24小時。 在AEM執行個體和HTTP介面中，都有重新整理報表和重新產生快取的選項，此預設值可能適合大部分的BPA使用。 如果 AEM 实例的报告生成时间特别长，您可能希望调整缓存生命周期以最大限度地减少报告的重新生成。

缓存生命周期值作为 `maxCacheAge` 属性存储在以下存储库节点上：
`/apps/best-practices-analyzer/content/BestPracticesReport/jcr:content`

此属性的值便是缓存生命周期（以秒为单位）。管理员可以使用 CRX/DE Lite 调整缓存生命周期。

### 在 AEM 6.1 上安装 {#installing-on-aem61}

BPA會使用名為的系統服務使用者帳戶 `repository-reader-service` 執行模式偵測器。 此帐户在 AEM 6.2 和更高版本上可用。在AEM 6.1上，必須建立此帳戶 *早於* 請依照下列步驟安裝BPA：

1. 按照[创建新服务用户](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security-service-users.html#creating-a-new-service-user)中的说明创建用户。将用户 ID 设置为 `repository-reader-service`，并将“中间路径”留空，然后单击绿色复选标记。

2. 按照[管理用户和组](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security.html#managing-users-and-groups)中的说明（特别是有关将用户添加到组的说明），将 `repository-reader-service` 用户添加到 `administrators` 组。

3. 透過封裝管理程式，在您的來源AEM執行個體上安裝BPA封裝。 （这将为 `repository-reader-service` 系统服务用户的 ServiceUserMapper 配置添加必要的配置修正。）
