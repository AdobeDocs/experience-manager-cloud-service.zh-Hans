---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 6fa6fc9015624bec9113a198285531a3bdd7e29c
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 97%

---


# 维护发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

## 版本 18175 {#release-18175}

以下总结了维护版本18175的不断改进，该版本于2024年10月10日公开发布。 上一个维护版本是版本 17964。由于存在问题，版本 18099 已被设为专有。

激活 2024.10.0 功能后会为此维护版本提供全套功能。有关更多信息，请参阅[ Experience Manager 发布路线图](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增强 {#enhancements-18175}

* ASSETS-38322：为 AEM 启用 http 请求事件。
* ASSETS-41448：更新 auth.ims 捆绑包以支持 FI 到组映射。
* ASSETS-41684：添加 OOB OSGI 配置以定义 FI 到资产、基础、Sites 和 Forms 的组映射。
* ASSETS-43015：更新至最新的 auth.ims 捆绑包。
* CQ-4356633：在“仅限内容”工具提示中添加额外字符。
* GRANITE-50948：将存储库服务集成到 AEM 支持存储库服务中。
* GRANITE-52454：添加支持助手 0.1.2。
* GRANITE-52454：升级支持助手 GRANITE-52454 升级支持助手以使用 AEMaCS 的最新版本。
* GRANITE-53287：更新安全权限集成测试版本。
* GRANITE-53485：支持复制 Azure Blob 存储的服务主体身份验证。
* GRANITE-53514：Treeactivation 已更新至版本 1.0.26。
* GRANITE-53870：创建内部机制以跳过快速启动的最大 JVM 版本检查。
* GRANITE-53914：使用 Java 17 更新模块版本修复平台测试失败。
* GRANITE-53966：使用单独的线程池进行内容分发。
* GRANITE-54006：更新 Jackson 至 2.17.2。
* GRANITE-54038：将 Creative Cloud Enterprise IMS 客户端添加到 AEM IMS 客户端允许列表。
* GRANITE-54054：com.adobe.granite.repository.impl.SystemUserValidation 的环境变量 warnOnly。
* GRANITE-54266：生产 SDK 缺少搜索建议器服务。
* GRANITE-54274：接受 Firefly IMS 客户端。
* GRANITE-54300：将 Oak 更新至最新公开版本 (1.70.0)。
* GUIDES-19069：为 aem 指南插件添加 guidesPeerLinkIndex。
* SITES-23584：修复 Java 17 上 Foundation 组件的测试失败。
* SKYOPS-69768：SlingModels 不会反序列化 ResourceResolvers。
* SKYOPS-76378：提高 i18n 中 ResourceBundle 注册/注销的线程安全性。
* SKYOPS-79285：将 Sling XSS 更新至 2.4.2。
* SKYOPS-82383：在命令执行描述符中公开“helm-values”转换合并分析结果。
* SKYOPS-84810：在 RDE 启动时跳过“40-initialize-publish.sh”执行。
* SKYOPS-84951：修复可变内容校验和生成代码。
* SKYOPS-85335：将 org.apache.sling.jcr.repoinit 更新至 1.1.52。
* SKYOPS-85336：将 Sling Commons Threads 更新至 3.3.0。
* SKYOPS-86329：更新平台测试模块的版本以支持 Java 21 sdk。

### 修复的问题 {#fixed-issues-18175}

* CNTBF-298：从 CC 导出的包中删除 jcr:uuid。
* SKYOPS-83910：修复在 SKYOPS-82371 中发现的并发问题。
* GRANITE-52876：更新至 com.adobe.granite.ui.content 0.8.1448。
* GUIDES-14445：本机 PDF 生成失败，并出现与获取 Node.js 依赖项相关的错误。
* GUIDES-16961：带有  `<conref>`  的标题无法在 Web 编辑器的基线和翻译仪表板中解析。
* GUIDES-17283：选择 **使用在 topicmeta 中添加的元数据** 选项时，元数据属性不会传播到原生 PDF 输出的文档属性中。
* GUIDES-17793：在批量激活已发布内容期间，引用的 PDF 不会从 **批量发布仪表板** 激活。

如需了解有关新版本中新增功能、增强指南功能和已修复问题的更多信息，请查看 [Experience Manager Guides 发布路线图](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap)。

### 已知问题 {#known-issues-18175}

* FORMS - 15818：组件描述符条目 `OSGI-INF/com.adobe.aemfd.docmanager.impl.*.xml` 在服务器日志中未找到语句。这些是无害的日志语句。

### 已弃用的功能和 API {#deprecated-18175}

AEM as a Cloud Service 中已弃用和删除的功能和 API 在 [已弃用和删除的功能和 API](/help/release-notes/deprecated-removed-features.md) 文档中有详细说明。

以下是最近弃用的功能或正在弃用的功能的摘要。

#### JavaScript Use API {#javascript-use-api}

[由于用户在调试和维护利用 API 的代码时遇到困难，并且与 Java 替代方案相比存在性能限制，因此 JavaScript 使用 API](https://github.com/adobe/htl-spec/blob/master/SPECIFICATION.md#42-javascript-use-api) 已被正式弃用。

您应该转换到 [Java 使用 API，](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-htl/content/java-use-api) 它提供更好的性能、更容易的调试和更好的长期支持。

#### com.day.cq.wcm.api {#com-day-cq-wcm-api}

请注意，Adobe 正在更新 `com.day.cq.wcm.api`。它的一些方法和类在当前版本中已被标记为 `@Deprecated` 。这些将在未来的版本中删除。请考虑切换到他们建议的替代方案。

#### org.apache.jackrabbit.oak.plugins.blob。{#org.apache.jackrabbit.oak.plugins.blob}

* GRANITE-54165：在公共 API 中弃用 org.apache.jackrabbit.oak.plugins.blob。

### 安全修复 {#security-18175}

AEM as a Cloud Service 致力于优化您平台的安全性和性能。此维护版本解决了 2 个已发现的漏洞，增强了我们对强大系统保护的承诺。

### 嵌套的技术 {#embedded-tech-18175}

| 技术 | 版本 | 链接 |
|---|---|---|
| AEM Oak | 1.70.0 | [Oak API 1.70.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.70.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.24-1.4.0 | [HTML 模板语言规范](https://github.com/adobe/htl-spec) |
| AEM 核心组件 | 2.27.0 | [AEM WCM 核心组件](https://github.com/adobe/aem-core-wcm-components) |
