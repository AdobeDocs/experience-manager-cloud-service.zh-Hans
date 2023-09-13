---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 8a1ed1e44db0154854af73a96339d8e416afd3b4
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 45%

---

# 维护发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

## 版本 13420 {#release-13420}

以下总结了维护版本13420的不断改进，该版本于2023年9月12日公开发布。 此维护版本取代了发行说13323。

激活 2023.9.0 功能后可为此次维护版本提供完整的功能集。有关更多信息，请参阅[ Experience Manager 发布路线图](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html)。

### 增强 {#enhancements-13420}

- ASSETS-19544：资产上次修改者属性现在设置为请求处理的用户。

### 修复的问题 {#fixed-issues-13420}

- ASSETS-27628：在自定义资产搜索面板时创建了错误的“渠道”节点
- ASSETS-27539：上载限制正则表达式匹配。
- ASSETS-26530： Unified Shell不会将用户返回到原始页面。
- ASSETS-22719：智能裁切断点命名中的括号会破坏智能裁切编辑功能。
- ASSETS-27726： linkshare.html不应由Google编制索引。
- ASSETS-27791：仅对第一个字段进行元数据架构验证。
- ASSETS-25544：修复了已禁用的CDN缓存失效按钮。
- ASSETS-26575：创建图像集时修复了名称截断问题。
- ASSETS-26705：修复了对非DM文件夹资源和内容片段进行的不必要处理。
- ASSETS-25740：固定屏幕阅读器不提供使用向下箭头键在“编辑智能裁切”页面上编辑/裁切控件的名称和角色的旁白。
- CQ-4354266：无法打开收件箱项目。
- CQ-4354347：更新了AEM翻译。
- DISP-1009：作为非第一个标头的User-Agent会裁切X-Forwarded-Host。
- 各种与辅助功能和安全相关的修复。

### 已知问题 {#known-issues-13420}

无。

### 嵌套的技术 {#embedded-tech-13420}

| 技术 | 版本 | 链接 |
|---|---|---|
| AEM OAK | 1.54-T20230817132355-3800a65 | [Oak API 1.54.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.54.0/index.html) |
| AEM SLING API | 2.27.2 版 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 版本 1.4.20-1.4.0 | [HTML 模板语言规范](https://github.com/adobe/htl-spec) |
| AEM 核心组件 | 2.23.2 版 | [AEM WCM 核心组件](https://github.com/adobe/aem-core-wcm-components) |
