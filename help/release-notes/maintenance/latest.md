---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 30b5d5838087a35a457939cdbaa13c5735df144e
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 49%

---


# 维护发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

## 版本 19823 {#19823}

以下总结了维护版本19823的持续改进，该版本于2025年3月4日公开发布。 上一个维护版本是版本 19687。

激活 2025.3.0 功能后会为此维护版本提供全套功能。有关更多信息，请参阅[ Experience Manager 发布路线图](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增强功能 {#enhancements-19823}

* Assets-46491：用于资源处理状态更改的OSGI事件处理程序。
* Assets-45613：删除或移动资源时发送取消发布事件。
* Assets-45131： Content Hub中的自定义标记属性支持。

### 修复的问题 {#fixed-issues-19823}

* Assets-20433：受密码保护的PDF存在Dynamic Media摄取问题。
* Assets-24675：对于仅样本图像配置文件，不显示图像处理选项。
* Assets-41257：资源版本比较会呈现宽高比不正确的资源。 资产版本在时间轴中的显示顺序不正确。
* Assets-44894： Assets视图书签可能无法单击。
* Assets-45015：如果找不到智能裁切资源句柄，则将智能裁切宽度和高度设置为零。
* Assets-45192：降低脉冲请求频率。
* Assets-45724：确保在未分配上载作业的情况下重试DM上载。
* Assets-46425： Adobe Stock集成搜索问题。
* Assets-27400：文件夹预览生成器可能会尝试打开原始文件夹。
* CQ-4358722：在Java 11和Java 17中处理不同的区域设置代码。
* SITES-29369：在激活/停用资产时触发的页面已发布/未发布事件。
* SITES-24074：修复Unified Shell下的键盘辅助功能。
* SITES-28058：Assets文件夹标题未转移到Live Copy。

### 已知问题 {#known-issues-19823}

无。

### 已弃用的功能和 API {#deprecated-19823}

AEM as a Cloud Service 中已弃用和删除的功能和 API 在[已弃用和删除的功能和 API](/help/release-notes/deprecated-removed-features.md) 文档中有详细说明。

### 安全修复 {#security-19823}

AEM as a Cloud Service 致力于优化您平台的安全性和性能。此维护版本解决了 6 个已发现的漏洞，增强了我们对强大系统保护的承诺。

### 嵌套的技术 {#embedded-tech-19823}

| 技术 | 版本 | 链接 |
|---|---|---|
| AEM Oak | 1.76.0 | [Oak API 1.76.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.76.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.26-1.4.0 | [HTML 模板语言规范](https://github.com/adobe/htl-spec) |
| AEM 核心组件 | 2.27.0 | [AEM WCM 核心组件](https://github.com/adobe/aem-core-wcm-components) |
