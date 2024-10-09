---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: ea7e027b5247b64e78da1d14e4e602f39a37e4bd
workflow-type: tm+mt
source-wordcount: '836'
ht-degree: 27%

---


# 维护发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

## 版本 18099 {#release-18099}

以下总结了维护版本18099的不断改进，该版本于2024年10月9日公开发布。 上一个维护版本是版本 17964。

激活 2024.10.0 功能后会为此维护版本提供全套功能。有关更多信息，请参阅[ Experience Manager 发布路线图](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增强 {#enhancements-18099}

* Assets-43015：更新到最新的auth.ims包。
* Assets-41684：更新src/main/features/docker/ethos/base-ims-oauth.json。
* Assets-38322：启用AEM的http请求事件。
* Assets-41684：添加OOB OSGI配置以定义Assets、Foundation、Sites和Forms的FI到组映射。
* Assets-41448：更新auth.ims包以支持FI到组的映射。
* CQ-4356633：在“仅限内容”工具提示中添加额外的字符。
* SITES-23584：基础组件测试在Java 17上失败。
* GUIDES-19069：添加guidesPeerLinkIndex for aem guides插件。
* GRANITE-54300：将 Oak 更新至最新公开版本 (1.70.0)。
* GRANITE-54274：接受Firefly的IMS客户端。
* GRANITE-36205：将内部 oak 发行版更新到最新版本。
* GRANITE-45298：低权限用户可以通过不使用JS但使用XSS方式构建恶意表单来获取RCE。
* GRANITE-54266：生产SDK缺少搜索建议程序服务。
* GRANITE-50948 — 将存储库服务集成到AEM中为本地开发添加替代存储库服务。
* GRANITE-53966：对内容分发使用单独的线程池。
* GRANITE-53514：树激活1.0.26。
* GRANITE-54054：com.adobe.granite.repository.impl.SystemUserValidation warnOnly的环境变量。
* GRANITE-50948：将存储库服务集成到AEM Support for repository service中。
* GRANITE-52454：添加支持帮助程序0.1.2。
* GRANITE-53514：树激活1.0.26。
* GRANITE-54038：将Creative Cloud企业IMS客户端添加到AEM 列入允许列表 IMS客户端。
* GRANITE-36205：将内部 oak 发行版更新到最新版本。
* GRANITE-53485：复制Azure Blob存储的支持服务主体身份验证。
* GRANITE-54006：将Jackson更新为2.17.2。
* GRANITE-53287：正在更新安全权限集成测试版本。
* GRANITE-53914：使用Java 17更新模块版本的平台测试失败。
* GRANITE-53870：创建内部机制以跳过快速入门的最大JVM版本检查。
* GRANITE-52454：升级支持帮助程序GRANITE-52454升级支持帮助程序以使用AEMaaCS的最新版本。
* SKYOPS-85335：将org.apache.sling.jcr.repoinit更新为1.1.52。
* SKYOPS-85336：将Sling Commons Threads更新为3.3.0。
* SKYOPS-76378：提高i18n中ResourceBundle注册/注销的线程安全性。
* SKYOPS-84951：可变内容校验和生成代码不正确。
* SKYOPS-82383：在命令执行描述符中公开“helm-values”convert-merge-analyze结果。
* SKYOPS-86329：更新平台测试模块的版本以支持java 21 sdk。
* SKYOPS-69768： SlingModels不会反序列化ResourceResolvers。
* SKYOPS-84810：在RDE启动时跳过执行“40-initialize-publish.sh”。
* SKYOPS-79285：将Sling XSS更新为2.4.2

### 修复的问题 {#fixed-issues-18099}

* CNTBF-298：从CC导出的资源包中删除jcr：uuid。
* SKYOPS-83910：修复了SKYOPS-82371中发现的并发问题。
* GRANITE-52876：更新至com.adobe.granite.ui.content 0.8.1448。
* GRANITE-53088：由SITES-11992的修复引入的回归。
* GUIDES-14445：本机PDF生成失败，并出现与获取Node.js的依赖关系相关的错误。
* GUIDES-16961：带有`<conref>`的标题无法在Web编辑器的基线和翻译功能板中解析。
* GUIDES-17283：当选择在topicmeta **选项中添加的**&#x200B;使用PDF时，元数据属性不会在本机元数据输出的文档属性中传播。
* GUIDES-17793：在批量激活已发布的PDF期间，未从&#x200B;**批量Publish功能板**&#x200B;中激活引用的内容。

有关版本中新增和增强的Guides功能和问题的更多信息，请查看[Experience Manager Guides版本路线图](https://experienceleague.adobe.com/cn/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap)。

### 已知问题 {#known-issues-18099}

* FORMS - 15818：组件描述符条目 `OSGI-INF/com.adobe.aemfd.docmanager.impl.*.xml` 在服务器日志中未找到语句。这些是无害的日志语句。

### 已弃用的功能和 API {#deprecated-18099}

AEM as a Cloud Service 中已弃用和删除的功能和 API 在 [已弃用和删除的功能和 API](/help/release-notes/deprecated-removed-features.md) 文档中有详细说明。

以下是最近弃用的功能或正在弃用的功能的摘要。

#### JavaScript使用API {#javascript-use-api}

[JavaScript Use API](https://github.com/adobe/htl-spec/blob/master/SPECIFICATION.md#42-javascript-use-api)已正式弃用，因为用户调试和维护利用API的代码时遇到挑战，并且与Java替代方案相比，存在性能限制。

您应该转换到[Java Use API，](https://experienceleague.adobe.com/en/docs/experience-manager-htl/content/java-use-api)，它提供了更好的性能、更轻松的调试和更强大的长期支持。

#### com.day.cq.wcm.api {#com-day-cq-wcm-api}

请注意，Adobe正在更新`com.day.cq.wcm.api`。 其某些方法和类在当前版本中被标记为`@Deprecated`。 这些功能将在未来版本中删除。 请考虑改用他们建议的替代方案。

#### org.apache.jackrabbit.oak.plugins.blob {#org.apache.jackrabbit.oak.plugins.blob}

* GRANITE-54165：弃用公共API中的org.apache.jackrabbit.oak.plugins.blob。

### 安全修复 {#security-18099}

AEM as a Cloud Service 致力于优化您平台的安全性和性能。此维护版本解决了 2 个已发现的漏洞，增强了我们对强大系统保护的承诺。

### 嵌套的技术 {#embedded-tech-18099}

| 技术 | 版本 | 链接 |
|---|---|---|
| AEM Oak | 1.70.0 | [Oak API 1.70.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.70.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.24-1.4.0 | [HTML 模板语言规范](https://github.com/adobe/htl-spec) |
| AEM 核心组件 | 2.27.0 | [AEM WCM 核心组件](https://github.com/adobe/aem-core-wcm-components) |
