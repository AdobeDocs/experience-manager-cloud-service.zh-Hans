---
title: OSGi 配置 API
description: AEMas a Cloud ServiceOSGi設定表面的說明
feature: Deploying
exl-id: 94d3df65-71d7-4442-8412-fe2cca7e79ff
source-git-commit: cba6648d7ef18f3cccbd9562f3a66d9c683ae852
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 3%

---

# OSGi 配置 API

以下兩個清單反映了AEMas a Cloud ServiceOSGi設定介面，說明客戶可以設定的內容。

1. 不得由客戶程式碼設定的OSGi設定清單
1. 其屬性可設定，但必須符合指示的驗證規則的OSGi設定清單。 這些規則包括是否需要屬性的宣告、其型別，以及在某些情況下其允許的值範圍。

如果未列出OSGI設定，則可能由客戶程式碼設定。

這些規則會在Cloud Manager建置流程中驗證。 可隨著時間新增其他規則，預計的執行日期會記在表格中。 客戶應在目標執行日期之前遵守這些規則。 在移除日期之後不遵守規則將會在Cloud Manager建置過程中產生錯誤。 Maven專案應包含 [AEMas a Cloud ServiceSDK建置分析器Maven外掛程式](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html) 在本機SDK開發期間標籤OSGI設定錯誤。

有關OSGI設定的其他資訊，請參閱 [此位置](/help/implementing/deploying/configuring-osgi.md).

## 無法修改的OSGi設定 {#osgi-configurations-that-cannot-be-modified}

* **`org.apache.felix.webconsole.internal.servlet.OsgiManager`** （公告日期：二零二一年四月三十日，執行日期：二零二一年七月三十一日）
* **`com.day.cq.auth.impl.cug.CugSupportImpl`** （公告日期：二零二一年四月三十日，執行日期：二零二一年七月三十一日）
* **`com.day.cq.jcrclustersupport.ClusterStartLevelController`** （公告日期：二零二一年四月三十日，執行日期：二零二一年七月三十一日）
* **`org.apache.felix.http (Factory)`** （公告日期：二零二一年四月三十日，執行日期：二零二一年七月三十一日）
* **`org.apache.sling.jcr.davex.impl.servlets.SlingDavExServlet`** （公告日期：2021年8月25日，執行日期：2021年11月26日）

## 受組建驗證規則約束的OSGi設定 {#osgi-configurations-subject-to-build-validation-rules}

* **`org.apache.felix.eventadmin.impl.EventAdmin`** （公告日期：二零二一年四月三十日，執行日期：二零二一年七月三十一日）
   * `org.apache.felix.eventadmin.ThreadPoolSize`
      * 型別：整數
      * 所需範圍： 2-100
   * `org.apache.felix.eventadmin.AsyncToSyncThreadRatio`
      * 型別：兩次
   * `org.apache.felix.eventadmin.Timeout`
      * 型別：整數
   * `org.apache.felix.eventadmin.RequireTopic`
      * 型別：布林值
   * `org.apache.felix.eventadmin.IgnoreTimeout`
      * 必填
      * 型別：字串陣列
      * 必要範圍：至少必須包含所有 `org.apache.felix*`， `org.apache.sling*`， `come.day*`， `com.adobe*`
   * `org.apache.felix.eventadmin.IgnoreTopic`
      * 型別：字串陣列
* **`org.apache.felix.http`** （公告日期：二零二一年四月三十日，執行日期：二零二一年七月三十一日）
   * `org.apache.felix.http.timeout`
      * 型別：整數
   * `org.apache.felix.http.session.timeout`
      * 型別：整數
   * `org.apache.felix.http.jetty.threadpool.max`
      * 型別：整數
   * `org.apache.felix.http.jetty.headerBufferSize`
      * 型別：整數
   * `org.apache.felix.http.jetty.requestBufferSize`
      * 型別：整數
   * `org.apache.felix.http.jetty.responseBufferSize`
      * 型別：整數
   * `org.apache.felix.http.jetty.maxFormSize`
      * 型別：整數
   * `org.apache.felix.https.jetty.session.cookie.httpOnly`
      * 型別：布林值
   * `org.apache.felix.https.jetty.session.cookie.secure`
      * 型別：布林值
   * `org.eclipse.jetty.servlet.SessionIdPathParameterName`
      * 型別：字串
   * `org.eclipse.jetty.servlet.CheckingRemoteSessionIdEncoding`
      * 型別：布林值
   * `org.eclipse.jetty.servlet.SessionCookie`
      * 型別：字串
   * `org.eclipse.jetty.servlet.SessionDomain`
      * 型別：字串
   * `org.eclipse.jetty.servlet.SessionPath`
      * 型別：字串
   * `org.eclipse.jetty.servlet.MaxAge`
      * 型別：整數
   * `org.eclipse.jetty.servlet.SessionScavengingInterval`
      * 型別：整數
   * `org.apache.felix.jetty.gziphandler.enable`
      * 型別：布林值
   * `org.apache.felix.jetty.gzip.minGzipSize`
      * 型別：整數
   * `org.apache.felix.jetty.gzip.compressionLevel`
      * 型別：整數
   * `org.apache.felix.jetty.gzip.inflateBufferSize`
      * 型別：整數
   * `org.apache.felix.jetty.gzip.syncFlush`
      * 型別：布林值
   * `org.apache.felix.jetty.gzip.excludedUserAgents`
      * 型別：字串
   * `org.apache.felix.jetty.gzip.includedMethods`
      * 型別：字串陣列
   * `org.apache.felix.jetty.gzip.excludedMethods`
      * 型別：字串陣列
   * `org.apache.felix.jetty.gzip.includedPaths`
      * 型別：字串陣列
   * `org.apache.felix.jetty.gzip.excludedPaths`
      * 型別：字串陣列
   * `org.apache.felix.jetty.gzip.includedMimeTypes`
      * 型別：字串陣列
   * `org.apache.felix.jetty.gzip.excludedMimeTypes`
      * 型別：字串陣列
   * `org.apache.felix.http.session.invalidate`
      * 型別：布林值
   * `org.apache.felix.http.session.container.attribute`
      * 型別：字串陣列
   * `org.apache.felix.http.session.uniqueid`
      * 型別：布林值
* **`org.apache.sling.scripting.cache`** （公告日期：二零二一年四月三十日，執行日期：二零二一年七月三十一日）
   * `org.apache.sling.scripting.cache.size`
      * 型別：整數
      * 所需範圍： >= 2048
   * `org.apache.sling.scripting.cache.additional_extensions`
      * 必填
      * 型別：字串陣列
      * 必要範圍：必須包含js
* **`com.day.cq.mailer.DefaultMailService`** （公告日期：二零二一年四月三十日，執行日期：二零二一年七月三十一日）
   * `smtp.host`
      * 型別：字串
   * `smtp.port`
      * 型別：整數
      * 所需範圍：465、587或25
   * `smtp.user`
      * 型別：字串
   * `smtp.password`
      * 型別：字串
   * `from.address`
      * 型別：字串
   * `smtp.ssl`
      * 型別：字串
   * `smtp.starttls`
      * 型別：布林值
   * `smtp.requiretls`
      * 型別：布林值
   * `debug.email`
      * 型別：布林值
   * `oauth.flow`
      * 型別：布林值
* **`org.apache.sling.commons.log.LogManager.factory.config`** （公告日期：2021年11月16日，執行日期：2021年2月16日）
   * `org.apache.sling.commons.log.level`
      * 型別：分項清單
      * 必要範圍： INFO、DEBUG或TRACE
   * `org.apache.sling.commons.log.names`
      * 型別：字串
   * `org.apache.sling.commons.log.file`
      * 型別：字串
   * `org.apache.sling.commons.log.additiv`
      * 型別：布林值