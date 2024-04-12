---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 1dd2eae9201c86d2cdac78ff99634eff8ca57a05
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 88%

---

# 维护发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

## 版本 15860 {#release-15860}

以下总结了维护版本15860的不断改进，该版本于2024年4月10日公开发布。 上一个维护版本是版本 15787。

2024.3.0 功能激活将会为此维护版本提供全套功能。有关更多信息，请参阅[ Experience Manager 发布路线图](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=zh-Hans)。

### 增强 {#enhancements-15860}

无。

### 修复的问题 {#fixed-issues-15860}

* 修复了在启动项引用已删除或移动的页面时显示启动项控制台的回归。

### 已知问题 {#known-issues-15860}

无。

### 已弃用的功能和 API {#deprecated-15860}

* [在 Adobe Developer Console 中弃用 JWT 凭据](/help/security/jwt-credentials-deprecation-in-adobe-developer-console.md)

查看[已弃用和已移除的功能和 API](/help/release-notes/deprecated-removed-features.md)，了解 AEM as a Cloud Service 中已弃用或移除的功能。

### 更改通知 {#change-notice-15860}

**必需执行的操作**

#### 将 CM Java 版本设置为 11 {#set-java-version-11}

新版本的 aem-sdk-api 包含使用 Java 11 目标编译的类，该目标与 Cloud Manager 生成环境默认 JDK 版本 1.8 不兼容。此更新要求使用 JDK 11 执行 Maven。

建议客户将 `.cloudmanager/java-version` 文件添加到其 git 存储库的根目录中，其中的内容为：`11`。请参阅[生成环境/设置 Maven JDK 版本](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#alternate-maven-jdk-version)。


### 嵌套的技术 {#embedded-tech-15860}

| 技术 | 版本 | 链接 |
|---|---|---|
| AEM OAK | 1.60-T20240131102219-0cde853 | [Oak API 1.60.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.60.0/index.html) |
| AEM SLING API | 2.27.2 版 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 版本 1.4.20-1.4.0 | [HTML 模板语言规范](https://github.com/adobe/htl-spec) |
| AEM 核心组件 | 2.24.4 版 | [AEM WCM 核心组件](https://github.com/adobe/aem-core-wcm-components) |
