---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 82be9b2b328343e827b90bd8266d93127757f477
workflow-type: tm+mt
source-wordcount: '675'
ht-degree: 39%

---


# 维护发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

## 版本 17569 {#release-17569}

以下总结了维护版本17569的持续改进，该版本于2024年8月27日公开发布。 上一个维护版本是版本 17465。

2024.9.0 功能激活将会为此维护版本提供全套功能。有关更多信息，请参阅[ Experience Manager 发布路线图](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增强 {#enhancements-17569}

* CQ-4353778：翻译流程事件。
* CQ-4354583：通过Adobe管道发送翻译流程事件。
* CQ-4356479：仅允许Adobe代码使用/adobe servlet上下文。
* CQ-4358133：优化Jenkins工作程序的使用。
* CQ-4358226：保存翻译关键词功能不适用于特定字符串格式。
* CQ-4358270：AEM翻译包：2008年8月。
* CQ-4358310：将oak-compat-query-spi-1.2添加到快速入门中。
* GRANITE-36205：QS中的内部Oak版本的自动更新。
* GRANITE-49833：对事件发送者和代理的批量处理支持。
* GRANITE-52053：删除Commons Collections的使用情况3： Platform其他。
* GRANITE-52492：在PIT还原的情况下进行弹性异步追溯。
* GRANITE-53086：在AEMaaCS中将jacoco插件版本更新为0.8.12。
* GRANITE-53099：更新到 Apache Felix Http Jetty 5.1.24。
* GRANITE-53125：向CloudEvent添加分类。
* GRANITE-53328：将Filevault更新为3.8.0-T20240726111512-3cc11d50，并包含存储日志记录改进功能。
* GRANITE-53340：AEM660:660 CQ/Platform的正确版本控制和分支。
* GRANITE-53341：对使用ACS Commons 6不发出警告。
* GRANITE-53453：将commons-lang更新为3.15.0。
* GRANITE-53473：取消弃用Sling设置。
* GRANITE-53478：将Filevault更新到版本3.8.0。
* GRANITE-53505：将QS更新为commons-collections-3.2.2-adobe-2。
* GRANITE-53528：更新平台工件的版本。
* GRANITE-53547：提供替代API，避免使用Apache Commons Lang 2。
* GRANITE-53575：在CS中使用BSAFE 6.2.5。
* GRANITE-53608：将Oak更新到最新公共版本(1.68.0)。
* SITES-23583：Sites Evergreen测试在Java 17上失败。
* SKYOPS-79535：更新至rum脚本v2。
* SKYOPS-79816：在FACT工具中为服务用户映射启用Sling功能分析器任务。
* SKYOPS-81179：AEM构建包切换测试。
* SKYOPS-81866：报告已知与Java 21不兼容的捆绑包的警告。
* SKYOPS-82660：将Sling API更新为2.27.6。
* SKYOPS-82961：更新至Sling ResourceResolver 1.12.0-T20240723153354-a0270a0。
* SKYOPS-83356：创建全局功能板，以跟踪AEM部署中使用的JVM版本。
* SKYOPS-83436：Java Runtime 21转出会中断自适应表单AEM Forms的创建。
* SKYOPS-84272：记录在aem启动器启动中使用的Java版本。

### 修复的问题 {#fixed-issues-17569}

* CMGR-60225：验证AEM发行说17486的更新时，在AEM Sites CS客户上发现管道执行失败。
* GRANITE-45919：编辑用户设置中的“国家/地区”列表中已禁运的国家/地区。
* GRANITE-51715：选取器有时不会在文本字段中输入选定内容。
* GRANITE-53290：在解析XSS检查中的URL时，正确检查协议。
* GRANITE-53576：OSGi配置中的服务排名定义错误。
* SKYOPS-82129：Sling模型中的内存泄漏。

### 已知问题 {#known-issues-17569}

无。

### 更改通知 {#change-notice-17569}

* 从 2024 年 9 月开始，AEM as a Cloud Service 将会通过 Sling Model Exporter 框架禁用资源解析器的序列化。请参阅[该文档](/help/implementing/developing/hybrid/disallow-the-serialization-of-resourceresolvers-via-sling-model-exporter.md)了解更多详情。

### 已弃用的功能和 API {#deprecated-17569}

请注意，我们正在更新 `com.day.cq.wcm.api`，并且在当前版本中，我们已将其中的一些方法和类标记为 `@Deprecated`。这些将在未来的版本中删除，所以如果您正在使用其中任何一个，请考虑切换到其建议的替代方案。

AEM as a Cloud Service 中已弃用和删除的功能和 API 在 [已弃用和删除的功能和 API](/help/release-notes/deprecated-removed-features.md) 文档中有详细说明。

### 安全修复 {#security-17569}

AEM as a Cloud Service 致力于优化您平台的安全性和性能。此维护版本解决了 4 个已发现的漏洞，增强了我们对强大系统保护的承诺。

### 嵌套的技术 {#embedded-tech-17569}

| 技术 | 版本 | 链接 |
|---|---|---|
| AEM Oak | 1.68.0 | [Oak API 1.68.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.68.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.24-1.4.0 | [HTML 模板语言规范](https://github.com/adobe/htl-spec) |
| AEM 核心组件 | 2.26.0 | [AEM WCM 核心组件](https://github.com/adobe/aem-core-wcm-components) |
