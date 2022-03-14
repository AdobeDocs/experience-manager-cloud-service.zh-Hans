---
title: OSGi 配置 API
description: AEMas a Cloud ServiceOSGi配置曲面的描述
feature: Deploying
exl-id: 94d3df65-71d7-4442-8412-fe2cca7e79ff
source-git-commit: cba6648d7ef18f3cccbd9562f3a66d9c683ae852
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 1%

---

# OSGi 配置 API

以下两个列表反映了AEMas a Cloud ServiceOSGi配置界面，描述了客户可以配置的内容。

1. 不能由客户代码配置的OSGi配置列表
1. 可以配置其属性的OSGi配置列表，但必须遵守指示的验证规则。 这些规则包括是否需要声明资产、其类型，以及在某些情况下是否允许的值范围。

如果OSGi配置未列出，则可以按客户代码进行配置。

这些规则将在Cloud Manager构建过程中验证。 随着时间推移，可能会添加其他规则，并且表中会说明预期的执行日期。 客户应在目标实施日期之前遵守这些规则。 在删除日期后不遵守规则将在Cloud Manager构建过程中生成错误。 Maven项目应包含 [AEMas a Cloud ServiceSDK Build Analyzer Maven插件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html) 用于在本地SDK开发期间标记OSGI配置错误。

有关OSGI配置的其他信息，请访问 [此位置](/help/implementing/deploying/configuring-osgi.md).

## 无法修改的OSGi配置 {#osgi-configurations-that-cannot-be-modified}

* **`org.apache.felix.webconsole.internal.servlet.OsgiManager`** (公告日期：4/30/2021，执行日期：7/31/2021)
* **`com.day.cq.auth.impl.cug.CugSupportImpl`** (公告日期：4/30/2021，执行日期：7/31/2021)
* **`com.day.cq.jcrclustersupport.ClusterStartLevelController`** (公告日期：4/30/2021，执行日期：7/31/2021)
* **`org.apache.felix.http (Factory)`** (公告日期：4/30/2021，执行日期：7/31/2021)
* **`org.apache.sling.jcr.davex.impl.servlets.SlingDavExServlet`** (公告日期：8/25/2021，执行日期：11/26/2021)

## 受构建验证规则约束的OSGi配置 {#osgi-configurations-subject-to-build-validation-rules}

* **`org.apache.felix.eventadmin.impl.EventAdmin`** (公告日期：4/30/2021，执行日期：7/31/2021)
   * `org.apache.felix.eventadmin.ThreadPoolSize`
      * 类型：整数
      * 必需范围：2-100
   * `org.apache.felix.eventadmin.AsyncToSyncThreadRatio`
      * 类型：多次
   * `org.apache.felix.eventadmin.Timeout`
      * 类型：整数
   * `org.apache.felix.eventadmin.RequireTopic`
      * 类型：布尔
   * `org.apache.felix.eventadmin.IgnoreTimeout`
      * 必填
      * 类型：字符串数组
      * 必需范围：必须至少包括 `org.apache.felix*`, `org.apache.sling*`, `come.day*`, `com.adobe*`
   * `org.apache.felix.eventadmin.IgnoreTopic`
      * 类型：字符串数组
* **`org.apache.felix.http`** (公告日期：4/30/2021，执行日期：7/31/2021)
   * `org.apache.felix.http.timeout`
      * 类型：整数
   * `org.apache.felix.http.session.timeout`
      * 类型：整数
   * `org.apache.felix.http.jetty.threadpool.max`
      * 类型：整数
   * `org.apache.felix.http.jetty.headerBufferSize`
      * 类型：整数
   * `org.apache.felix.http.jetty.requestBufferSize`
      * 类型：整数
   * `org.apache.felix.http.jetty.responseBufferSize`
      * 类型：整数
   * `org.apache.felix.http.jetty.maxFormSize`
      * 类型：整数
   * `org.apache.felix.https.jetty.session.cookie.httpOnly`
      * 类型：布尔
   * `org.apache.felix.https.jetty.session.cookie.secure`
      * 类型：布尔
   * `org.eclipse.jetty.servlet.SessionIdPathParameterName`
      * 类型：字符串
   * `org.eclipse.jetty.servlet.CheckingRemoteSessionIdEncoding`
      * 类型：布尔
   * `org.eclipse.jetty.servlet.SessionCookie`
      * 类型：字符串
   * `org.eclipse.jetty.servlet.SessionDomain`
      * 类型：字符串
   * `org.eclipse.jetty.servlet.SessionPath`
      * 类型：字符串
   * `org.eclipse.jetty.servlet.MaxAge`
      * 类型：整数
   * `org.eclipse.jetty.servlet.SessionScavengingInterval`
      * 类型：整数
   * `org.apache.felix.jetty.gziphandler.enable`
      * 类型：布尔
   * `org.apache.felix.jetty.gzip.minGzipSize`
      * 类型：整数
   * `org.apache.felix.jetty.gzip.compressionLevel`
      * 类型：整数
   * `org.apache.felix.jetty.gzip.inflateBufferSize`
      * 类型：整数
   * `org.apache.felix.jetty.gzip.syncFlush`
      * 类型：布尔
   * `org.apache.felix.jetty.gzip.excludedUserAgents`
      * 类型：字符串
   * `org.apache.felix.jetty.gzip.includedMethods`
      * 类型：字符串数组
   * `org.apache.felix.jetty.gzip.excludedMethods`
      * 类型：字符串数组
   * `org.apache.felix.jetty.gzip.includedPaths`
      * 类型：字符串数组
   * `org.apache.felix.jetty.gzip.excludedPaths`
      * 类型：字符串数组
   * `org.apache.felix.jetty.gzip.includedMimeTypes`
      * 类型：字符串数组
   * `org.apache.felix.jetty.gzip.excludedMimeTypes`
      * 类型：字符串数组
   * `org.apache.felix.http.session.invalidate`
      * 类型：布尔
   * `org.apache.felix.http.session.container.attribute`
      * 类型：字符串数组
   * `org.apache.felix.http.session.uniqueid`
      * 类型：布尔
* **`org.apache.sling.scripting.cache`** (公告日期：4/30/2021，执行日期：7/31/2021)
   * `org.apache.sling.scripting.cache.size`
      * 类型：整数
      * 必需范围：>= 2048
   * `org.apache.sling.scripting.cache.additional_extensions`
      * 必填
      * 类型：字符串数组
      * 必需范围：必须包含js
* **`com.day.cq.mailer.DefaultMailService`** (公告日期：4/30/2021，执行日期：7/31/2021)
   * `smtp.host`
      * 类型：字符串
   * `smtp.port`
      * 类型：整数
      * 必需范围：465、587或25
   * `smtp.user`
      * 类型：字符串
   * `smtp.password`
      * 类型：字符串
   * `from.address`
      * 类型：字符串
   * `smtp.ssl`
      * 类型：字符串
   * `smtp.starttls`
      * 类型：布尔
   * `smtp.requiretls`
      * 类型：布尔
   * `debug.email`
      * 类型：布尔
   * `oauth.flow`
      * 类型：布尔
* **`org.apache.sling.commons.log.LogManager.factory.config`** (公告日期：11/16/21，执行日期：2/16/21)
   * `org.apache.sling.commons.log.level`
      * 类型：明细列表
      * 必需范围：信息、调试或TRACE
   * `org.apache.sling.commons.log.names`
      * 类型：字符串
   * `org.apache.sling.commons.log.file`
      * 类型：字符串
   * `org.apache.sling.commons.log.additiv`
      * 类型：布尔