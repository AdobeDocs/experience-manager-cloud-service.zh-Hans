---
title: 内容转移工具的先决条件
description: 内容转移工具的先决条件
exl-id: 41a9cff1-4d89-480c-b9fc-5e8efc2a0705
source-git-commit: eb633db8fe64a62661c094b88f0ce8d9950ed6d7
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 15%

---

# 内容转移工具的先决条件 {#prerequisites}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_prereqs"
>title="有关使用内容转移工具的重要注意事项"
>abstract="查看有关使用内容转移工具的重要注意事项，包括 Java 和 AEM 版本、支持的数据存储类型、用户组注意事项等。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html#pre-reqs" text="使用内容传输工具的重要注意事项"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html#best-practices" text="最佳实践和准则"

下表總結使用「內容轉移工具」的先決條件。

請檢閱下列所有考量事項：

| 注意事项 | 目前支援的內容 |
|---------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| AEM 版本 | 「內容轉移工具」只能在AEM 6.3或更新版本上執行。 |
| 區段存放區的大小 | 現有的存放庫，具有少於5,500萬個JCR節點和最多250GB （線上壓縮大小） *作者* 和50 GB以上 *發佈* 目前支援。 與Adobe客戶服務建立支援票證，以討論超過這些限制的區段存放區大小選項。 |
| 內容存放庫的總大小 <br>*（區段存放區+資料存放區）* | 「內容轉移工具」的設計目的，是針對檔案資料存放區型別的資料存放區，轉移最高20 TB的內容。 目前不支援任何大於20 TB的內容。 與Adobe客戶服務建立支援票證，以討論大於20 TB內容的選項。 <br>若要大幅加快大型存放庫的內容轉移流程，可選擇使用 [預先複製](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html#setting-up-pre-copy-step) 步驟可以使用。 這適用於檔案資料存放區、Amazon S3和Azure資料存放區型別的資料存放區。 Amazon S3和Azure資料存放區支援大於20TB的存放庫大小。 |
| Lucene索引大小總計 | Lucene索引大小總計上限25GB，不包括 `/oak:index/lucene` 和 `/oak:index/damAssetLucene` 目前支援。 與Adobe客戶服務建立支援票證，以討論超過此限制的索引大小選項。 |
| 節點名稱長度 | 當節點父路徑>= （等於或大於） 350位元組時，節點名稱的長度必須等於或少於150位元組。 這些節點名稱必須縮短為&lt;= 150個位元組，才能受到AEMas a Cloud Service的Document節點存放區支援。 如果未修正這些長節點名稱，內嵌將會失敗。 |
| 不可變路徑中的內容 | 「內容轉移工具」無法用於移轉不可變路徑中的內容。 轉移內容來源： `/etc` 僅限特定 `/etc` 允許選取路徑，但僅支援 [AEM Forms至AEM Formsas a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/migrate-to-forms-as-a-cloud-service.html#paths-of-various-aem-forms-specific-assets). 如需所有其他使用案例，請參閱 [通用存放庫重組](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/restructuring/all-repository-restructuring-in-aem-6-5.html) 以進一步瞭解存放庫重組。 |
| MongoDB中的節點屬性值 | 儲存在MongoDB中的節點屬性值不能超過16MB。 這會由MongoDB強制執行。 如果屬性值大於此限制，擷取將失敗。 在執行擷取之前，請執行此作業 [oak-run](https://repo1.maven.org/maven2/org/apache/jackrabbit/oak-run/1.38.0/oak-run-1.38.0.jar) 指令碼。 檢閱所有大型屬性值，並驗證是否需要它們。 超過16MB的則需要轉換為二進位值。 |

## 后续内容 {#whats-next}

在檢閱了先決條件並確定您能否在移轉專案中使用內容轉移工具後，請參閱 [使用內容轉移工具的准則和最佳實務](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html).
