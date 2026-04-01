---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: e035c1c27f652af231034588eb1359354182dcb0
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 57%

---


# 维护发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

## 发行版本 25194 {#25194}

以下总结了维护版本25194的持续改进，该版本于2026年4月1日公开发布。 上一个维护版本是版本 24678。

2026.4.0 功能激活提供此维护版本的全套功能。有关更多信息，请参阅[&#x200B; Experience Manager 发布路线图](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

>[!NOTE]
>
>发行说24893已设为私有。

### 增强功能 {#enhancements-25194}

* Assets-65127：事件自定义元数据：改进了元数据名称的处理。
* Assets-63313：根据C2PA清单为导出的资源和父项自动创建相关链接。
* Assets-10995：限制下载zip文件中的资源数。

### 修复的问题 {#fixed-issues-25194}

* Assets-62882：管理员视图：上传多个无效文件名时信息工具提示中断。
* Assets-63642：共享链接无法在某些开发环境中呈现资产(SLA3)。
* Assets-59267：为投放有效负载加载应用程序元数据时出现NPE。
* Assets-59227：元数据导出：由于正则表达式匹配，不再包含未选择的属性。
* Assets-65187：列数据包含转义逗号时，在云中进行CSV预览。
* Assets-63441：确保所有用户都有权读取Assets Omnisearch配置。
* SITES-40095：元数据编辑器：本地内容片段引用超过10个条目。

### 已知问题 {#known-issues-25194}

无。

### 已弃用的功能和 API {#deprecated-25194}

AEM as a Cloud Service 中已弃用和删除的功能和 API 在[已弃用和删除的功能和 API](/help/release-notes/deprecated-removed-features.md) 文档中有详细说明。

### 安全修复 {#security-25194}

AEM as a Cloud Service 致力于优化您平台的安全性和性能。此维护版本解决了 9 个已发现的漏洞，增强了我们对强大系统保护的承诺。

### 嵌入的技术 {#embedded-tech-25194}

| 技术 | 版本 | 链接 |
|---|---|---|
| AEM Oak | 1.90.0 | [Oak 1.90.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.90.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [HTML 模板语言规范](https://github.com/adobe/htl-spec) |
| Apache HTTP 服务器 | 2.4.65 | [Apache Httpd 2.4.65](https://apache.googlesource.com/httpd/+/refs/tags/2.4.65/CHANGES) |
| AEM 核心组件 | 2.30.4 | [AEM WCM 核心组件](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14（默认） | [受支持的 Node.js 版本](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |
