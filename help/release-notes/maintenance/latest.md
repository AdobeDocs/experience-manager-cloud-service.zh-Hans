---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 33468de99a3e77539f4bdc9435324c9f52a45d9f
workflow-type: ht
source-wordcount: '350'
ht-degree: 100%

---


# 维护发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

## 发行版本 22171 {#22171}

下面总结了对 2025 年 9 月 2 日公开发布的维护版本 22171 的持续改进。上一个维护版本是版本 21994。

激活 2025.9.0 功能后会为此维护版本提供全套功能。有关更多信息，请参阅 [Experience Manager 发布路线图](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 新增功能  {#new-features-22171}

* ASSETS-53136：具有 OpenAPI 功能的 Dynamic Media 支持虚域 ID。

### 增强 {#enhancements-22171}

无。

### 修复的问题 {#fixed-issues-22171}

* ASSETS-52510：对于包含 Unicode `U+202F` 的文件名，对重复文件名的检测失败。
* ASSETS-53489：从资产视图 UI 中删除文件夹不会取消批准其包含的所有资产。
* ASSETS-54821：资产链接中偶尔出现“服务器错误”。
* ASSETS-55024：AEM Assets 的“通过电子邮件下载”模板中图像显示不正确。
* ASSETS-55325：资产重命名后，Dynamic Media 静态 URL 漏掉了文件扩展名。
* ASSETS-55334：链接共享对话框会短暂闪烁然后消失，或者完全不显示。
* ASSETS-55382：重新启动异步资产作业后，会创建重复的目标文件夹。
* ASSETS-55472：管理发布选项“仅包含已发布的页面”被忽略。
* SITES-31600：Contexthub js 错误中断个性化。

如需了解有关新版本中新增功能、增强功能和已修复问题的更多信息，请查看 [Experience Manager Guides 发布路线图](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap)。

### 已知问题 {#known-issues-22171}

无。

### 已弃用的功能和 API {#deprecated-22171}

AEM as a Cloud Service 中已弃用和删除的功能和 API 在[已弃用和删除的功能和 API](/help/release-notes/deprecated-removed-features.md) 文档中有详细说明。

### 安全修复 {#security-22171}

AEM as a Cloud Service 致力于优化您平台的安全性和性能。此维护版本解决了 7 个已发现的漏洞，增强了我们对强大系统保护的承诺。

### 嵌入的技术 {#embedded-tech-22171}

| 技术 | 版本 | 链接 |
|---|---|---|
| AEM Oak | 1.84.0 | [Oak API 1.84.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.84/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [HTML 模板语言规范](https://github.com/adobe/htl-spec) |
| Apache HTTP 服务器 | 2.4.65 | [Apache Httpd 2.4.65](https://apache.googlesource.com/httpd/+/refs/tags/2.4.65/CHANGES) |
| AEM 核心组件 | 2.29.0 | [AEM WCM 核心组件](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14（默认） | [受支持的 Node.js 版本](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |
