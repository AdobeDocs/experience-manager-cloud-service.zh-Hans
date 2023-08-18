---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: cf8b5d8b11452268b2839053c1e05cc2ec107a91
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 63%

---

# 维护发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

## 发行版本 13173 {#release-13173}

以下总结了维护版本13173的不断改进，该版本于2023年8月18日公开发布。 此维护版本是对上一个维护版本 13099 的更新。

激活 2023.8.0 功能后可为此次维护版本提供完整的功能集。有关更多信息，请参阅[ Experience Manager 发布路线图](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html)。

### 增强 {#enhancements-13173}

无。

### 修复的问题 {#fixed-issues-13173}

- sites-15463：站点模板 — 无法发布模板。

### 已知问题 {#known-issues-13173}

- SITES-15359：内容片段 — 变量名称模式无法正确匹配具有以下特征的变量 ```'_'``` 在资源名称中。
- Forms-10444：自适应Forms模板 — 无法发布模板（解决方法：使用分发控制台）。
- CQ-4354191：工作流 — 由于nt：unstructured节点上存在复制元数据，自定义启动器可能会触发许多次（解决方法：更新启动器以排除复制元数据属性以避免重叠）。

### 嵌套的技术 {#embedded-tech-13173}

| 技术 | 版本 | 链接 |
|---|---|---|
| AEM OAK | 1.52-T20230629133256-25c01b8 | [Oak API 1.52.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.52.0/index.html) |
| AEM SLING API | 2.27.2 版 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 版本 1.4.20-1.4.0 | [HTML 模板语言规范](https://github.com/adobe/htl-spec) |
| AEM 核心组件 | 2.23.2 版 | [AEM WCM 核心组件](https://github.com/adobe/aem-core-wcm-components) |
