---
title: OSGi 配置 API
description: AEMas a Cloud ServiceOSGi配置界面的描述
feature: Deploying
exl-id: 94d3df65-71d7-4442-8412-fe2cca7e79ff
source-git-commit: cba6648d7ef18f3cccbd9562f3a66d9c683ae852
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 3%

---

# OSGi 配置 API

以下两个列表反映了AEMas a Cloud Service的OSGi配置界面，描述了客户可以配置的内容。

1. 不能由客户代码配置的OSGi配置列表
1. OSGi配置的列表，虽然可以配置其属性，但必须遵循指示的验证规则。 这些规则包括是否要求属性声明、其类型以及在某些情况下其允许的值范围。

如果未列出OSGI配置，则可能由客户代码对其进行配置。

这些规则将在Cloud Manager构建过程中进行验证。 随着时间的推移，可能会添加其他规则，并且表中会注明预计的执行日期。 客户应在目标执行日期之前遵守这些规则。 在删除日期之后不遵守规则将在Cloud Manager构建过程中生成错误。 Maven项目应包括 [AEMas a Cloud ServiceSDK构建分析器Maven插件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html) 标记本地SDK开发期间的OSGI配置错误。

有关OSGI配置的其他信息，请访问 [此位置](/help/implementing/deploying/configuring-osgi.md).

## 无法修改的OSGi配置 {#osgi-configurations-that-cannot-be-modified}

* **`org.apache.felix.webconsole.internal.servlet.OsgiManager`** （公告日期：2021年4月30日，执行日期：2021年7月31日）
* **`com.day.cq.auth.impl.cug.CugSupportImpl`** （公告日期：2021年4月30日，执行日期：2021年7月31日）
* **`com.day.cq.jcrclustersupport.ClusterStartLevelController`** （公告日期：2021年4月30日，执行日期：2021年7月31日）
* **`org.apache.felix.http (Factory)`** （公告日期：2021年4月30日，执行日期：2021年7月31日）
* **`org.apache.sling.jcr.davex.impl.servlets.SlingDavExServlet`** （公告日期：2021年8月25日，执行日期：2021年11月26日）

## 受生成验证规则约束的OSGi配置 {#osgi-configurations-subject-to-build-validation-rules}

* **`org.apache.felix.eventadmin.impl.EventAdmin`** （公告日期：2021年4月30日，执行日期：2021年7月31日）
   * `org.apache.felix.eventadmin.ThreadPoolSize`
      * 类型：整数
      * 所需范围：2-100
   * `org.apache.felix.eventadmin.AsyncToSyncThreadRatio`
      * 类型：双精度
   * `org.apache.felix.eventadmin.Timeout`
      * 类型：整数
   * `org.apache.felix.eventadmin.RequireTopic`
      * 类型：布尔值
   * `org.apache.felix.eventadmin.IgnoreTimeout`
      * 必填
      * 类型：字符串数组
      * 所需范围：必须至少包含所有 `org.apache.felix*`， `org.apache.sling*`， `come.day*`， `com.adobe*`
   * `org.apache.felix.eventadmin.IgnoreTopic`
      * 类型：字符串数组
* **`org.apache.felix.http`** （公告日期：2021年4月30日，执行日期：2021年7月31日）
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
      * 类型：布尔值
   * `org.apache.felix.https.jetty.session.cookie.secure`
      * 类型：布尔值
   * `org.eclipse.jetty.servlet.SessionIdPathParameterName`
      * 类型：字符串
   * `org.eclipse.jetty.servlet.CheckingRemoteSessionIdEncoding`
      * 类型：布尔值
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
      * 类型：布尔值
   * `org.apache.felix.jetty.gzip.minGzipSize`
      * 类型：整数
   * `org.apache.felix.jetty.gzip.compressionLevel`
      * 类型：整数
   * `org.apache.felix.jetty.gzip.inflateBufferSize`
      * 类型：整数
   * `org.apache.felix.jetty.gzip.syncFlush`
      * 类型：布尔值
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
      * 类型：布尔值
   * `org.apache.felix.http.session.container.attribute`
      * 类型：字符串数组
   * `org.apache.felix.http.session.uniqueid`
      * 类型：布尔值
* **`org.apache.sling.scripting.cache`** （公告日期：2021年4月30日，执行日期：2021年7月31日）
   * `org.apache.sling.scripting.cache.size`
      * 类型：整数
      * 所需范围： >= 2048
   * `org.apache.sling.scripting.cache.additional_extensions`
      * 必填
      * 类型：字符串数组
      * 所需范围：必须包括js
* **`com.day.cq.mailer.DefaultMailService`** （公告日期：2021年4月30日，执行日期：2021年7月31日）
   * `smtp.host`
      * 类型：字符串
   * `smtp.port`
      * 类型：整数
      * 所需范围：465、587或25
   * `smtp.user`
      * 类型：字符串
   * `smtp.password`
      * 类型：字符串
   * `from.address`
      * 类型：字符串
   * `smtp.ssl`
      * 类型：字符串
   * `smtp.starttls`
      * 类型：布尔值
   * `smtp.requiretls`
      * 类型：布尔值
   * `debug.email`
      * 类型：布尔值
   * `oauth.flow`
      * 类型：布尔值
* **`org.apache.sling.commons.log.LogManager.factory.config`** （公告日期：2021年11月16日，执行日期：2021年2月16日）
   * `org.apache.sling.commons.log.level`
      * 类型：明细列表
      * 所需范围： INFO、DEBUG或TRACE
   * `org.apache.sling.commons.log.names`
      * 类型：字符串
   * `org.apache.sling.commons.log.file`
      * 类型：字符串
   * `org.apache.sling.commons.log.additiv`
      * 类型：布尔值