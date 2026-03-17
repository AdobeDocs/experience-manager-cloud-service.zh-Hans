---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 2a7b83b99547637e02ec7cef9c92c5dd794a9adc
workflow-type: tm+mt
source-wordcount: '636'
ht-degree: 34%

---


# 维护发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

## 发行版本 24893 {#release-24893}

以下总结了维护版本24893的持续改进，该版本于2026年3月17日公开发布。 上一个维护版本是版本 24678。

2026.3.0 功能激活将会为此维护版本提供全套功能。有关更多信息，请参阅[&#x200B; Experience Manager 发布路线图](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增强功能 {#enhancements-24893}

* CNTBF-613：修复访问被拒绝(JCR-101) — 无法注册节点类型。
* GRANITE-53957：将Azure SDK V8升级到V12，以用于oak-blob-azure。
* GRANITE-57035：使用Bouncy Castle作为默认安全提供程序。
* GRANITE-59249：避免在JVM中注册安全提供程序。
* GRANITE-61564： `/security/users.html`上的视图设置无法为管理员打开。
* GRANITE-64748：OIDC：可配置的sling.oauth-request-key Cookie到期。
* SITES-39767：通过请求属性(CSP)支持nonce值。
* SKYOPS-129301：将API jar javadoc合规性级别设置为17。
* GRANITE-64962：将Apache Jackrabbit Oak更新至1.92.0。
* GRANITE-64963：将Apache Jackrabbit Filevault更新为4.2.0。
* GRANITE-64764：将Apache Commons文本更新到版本1.15.0。
* SKYOPS-131412：将Apache Commons Exec更新为1.6.0。
* SKYOPS-131432：将Felix SCR更新为2.2.14。
* SKYOPS-131907：将Sling API区域更新为1.1.10。
* SKYOPS-131938：将GSON更新为2.13.2。
* SKYOPS-132173：将Apache Commons编解码器更新为1.21.0。
* SKYOPS-132182：将Sling租户更新为1.1.8。
* SKYOPS-132267：将org.osgi.service.component更新为1.5.1。
* SKYOPS-132272：将Sling功能模型更新为2.0.4。
* SKYOPS-133689：更新Dispatcher以使用Apache httpd 2.4.66。

### 修复的问题 {#fixed-issues-24893}

* GRANITE-64443： `workflow.core`删除`log4j`的已弃用导出。
* GRANITE-64543：权限限制响应应与API合同匹配。

#### AEM Guides {#guides-24893}

* GUIDES-38412 ：在编辑Schematron `(*.sch)`文件并使用查找和替换功能时，“查找和替换”面板在底部部分显示在屏幕外，阻止访问其输入字段和控件。
* GUIDES-37806：如果在具有不同条件预设的多个映射中重用同一主题，则发布最新映射到Salesforce时会覆盖主题内容，从而导致向以前发布映射的用户显示的数据不正确。
* GUIDES-39394：在将最初作为具有特定版本（例如，在`/en/`下）的语言特定资产管理的图像移动到全局文件夹并执行更新版本基线导出时，新基线将继续引用该图像的过时语言特定版本，从而导致基线导出失败。
* GUIDES-39054：创建动态基线时，编辑器有时会因多个并发API请求而变得无响应，导致所有其他操作暂停。
* GUIDES-37781：将用户分配给审核任务时，下拉列表会列出所有用户，而非仅列出与所选项目关联的用户，从而导致用户选项无效。
* GUIDES-39385：打开地图的报表时，“筛选器”面板的加载存在延迟。

如需了解有关新版本中新增功能、增强功能和已修复问题的更多信息，请查看 [Experience Manager Guides 发布路线图](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap)。

### 已知问题 {#known-issues-24893}

无。

### 已弃用的功能和 API {#deprecated-24893}

AEM as a Cloud Service 中已弃用和删除的功能和 API 在[已弃用和删除的功能和 API](/help/release-notes/deprecated-removed-features.md) 文档中有详细说明。

### 安全修复 {#security-24893}

AEM as a Cloud Service 致力于优化您平台的安全性和性能。此维护版本解决了 9 个已发现的漏洞，增强了我们对强大系统保护的承诺。

### 嵌入的技术 {#embedded-tech-24893}

| 技术 | 版本 | 链接 |
|---|---|---|
| AEM Oak | 1.92.0 | [Oak 1.92.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.92.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [HTML 模板语言规范](https://github.com/adobe/htl-spec) |
| Apache HTTP 服务器 | 2.4.66 | [Apache Httpd 2.4.66](https://apache.googlesource.com/httpd/+/refs/tags/2.4.66/CHANGES) |
| AEM 核心组件 | 2.30.4 | [AEM WCM 核心组件](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14（默认） | [受支持的 Node.js 版本](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |
