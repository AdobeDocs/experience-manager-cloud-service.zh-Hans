---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 3fbdb150a9a1c133b4910603682e37f1c5d885d2
workflow-type: tm+mt
source-wordcount: '414'
ht-degree: 35%

---

# 维护发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

## 版本 13804 {#release-13804}

以下总结了维护版本13804的不断改进，该版本于2023年10月10日公开发布。 此维护版本是对上一个维护版本 13665 的更新。

2023.10.0 功能激活将为此维护版本提供全套功能。有关更多信息，请参阅[ Experience Manager 发布路线图](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html)。

### 增强 {#enhancements-13804}

* GRANITE-47238：审核日志维护 — 清除cronjob以使用客户配置。
* GRANITE-47123：发布(Sling) — 默认情况下，通过异步初始化虚路径缓存来缩短启动时间。
* GRANITE-46618：发布（复制） — 通过复制状态消息批量处理来提高发布启动速度。
* GRANITE-47136：索引（下载） — 提高新并行索引下载程序的下载速度（通过禁用校验和验证）。
* GRANITE-47211：发布(Infra) — 改进发布层部署的分离（通过存储和获取区段存储修订名称）。
* GRANITE-47267：更新至Apache Felix Http Jetty 4.2.18(包括对请求参数处理([FELIX-6625](https://issues.apache.org/jira/browse/FELIX-6625))，提高了本地和RDE开发的性能)。
* GRANITE-47247：更新至Sling Servlet Resolver 2.9.14，提高了Servlet解析度的性能。

### 修复的问题 {#fixed-issues-13804}

* GRANITE-47376：创作(Infra) — 修复了滚动重新启动后出现的DiscoveryTopologyUndefined错误。
* CQ-4353436： AEM Web Console (Sling) - ServiceUserMapperImpl验证器（主体/用户）中的空配置中断AEM实例([SLING-11912](https://issues.apache.org/jira/browse/SLING-11912))。
* SKYOPS-63925：转换作业 — 避免出现JDK 11的TransformJob失败 — ZipException：无效的CEN标头错误（带有disableZip64ExtraFieldValidation JVM标志）。
* SKYOPS-63361：转换作业（日志记录）通过转换作业（CUSTOMER_EXTRACT子步骤）改进了日志记录。
* SKYOPS-64103： FACT工具（日志记录） — 减少或截断Clientlib编译错误和警告消息。
* SKYOPS-65109： FACT工具（错误处理） — 具有未解析依赖关系的内容包会导致正确报告的错误。
* SKYOPS-65368： FACT工具（错误处理） — 工具陷入无休止的包含循环，最终在Clientlibs的循环嵌入上超时。
* SKYOPS-64031： RDE — 由于ResourceResolverFactory注册重复([SLING-12019](https://issues.apache.org/jira/browse/SLING-12019))。
* ASSETS-29105： RDE - RDE功能模型中SecurityProviderRegistration requiredServicePids中缺少限制提供程序。
* GRANITE-44674： CoralUI — 日期选取器必填字段功能不正确。

### 已知问题 {#known-issues-13804}

无。

### 嵌套的技术 {#embedded-tech-13804}

| 技术 | 版本 | 链接 |
|---|---|---|
| AEM OAK | 1.56-T20230927085643-189caed | [Oak API 1.56.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.56.0/index.html) |
| AEM SLING API | 2.27.2 版 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 版本 1.4.20-1.4.0 | [HTML 模板语言规范](https://github.com/adobe/htl-spec) |
| AEM 核心组件 | 2.23.4 版 | [AEM WCM 核心组件](https://github.com/adobe/aem-core-wcm-components) |
