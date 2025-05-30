---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 6884e33a922a7147e3a6a3f3ddb3dd3b2da85fbf
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 49%

---


# 维护发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

## 版本 21005 {#21005}

以下总结了维护版本21005的持续改进，该版本于2025年5月27日公开发布。 上一个维护版本是版本 20626。

激活 2025.5.0 功能后会为此维护版本提供全套功能。有关更多信息，请参阅[ Experience Manager 发布路线图](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增强功能 {#enhancements-21005}

* GRANITE-58927：改进了语义搜索切换功能。
* GRANITE-58800：将Apache Commons集合更新至版本4.5.0。
* GRANITE-58866：将Oak更新为1.80.0。
* SKYOPS-106509：通过Java 21中的反射式访问增强了GSON兼容性。
* SKYOPS-107761：将Sling模型Jackson导出程序更新为1.1.6。
* SKYOPS-107813：更新至 Sling ResourceResolver 1.12.8。

### 修复的问题 {#fixed-issues-21005}

* CNTBF-443：修复了SearchSlingJob `EVENT_JOB_TOPIC`属性。
* GRANITE-57853：修复了UI中的下拉列表对齐问题。
* GRANITE-58107：通过在OAuth处理程序中禁用基于用户的面板亲和度，修复了Publish上的404错误。
* GRANITE-58276、SLING-12755：修复了OSGi依赖项循环，这些循环可能会阻止HTL脚本引擎工厂正确启动，从而导致间歇性的服务器端渲染错误。
* SKYOPS-105151：修复了访问包列表时的NPE。
* SKYOPS-83910、SKYOPS-82371 — 修复了JSP编译并发问题。

#### AEM 指南 {#guides}

* GUIDES-26919 ：在启用Unified Shell的情况下打开DITA映射时，编辑器会间歇性地刷新。
* GUIDES-26282：更新或创建主题时无法关闭JCR会话连接，从而导致内存泄漏和服务停机。
* GUIDES-26434：如果DITA内容具有Weblink但没有作用域为`external`，则本机PDF发布将无限期继续。
* GUIDES-26516：当内容中出现错误时，原生PDF和AEM站点的发布会停止并排队等候。

如需了解有关新版本中新增功能、增强功能和已修复问题的更多信息，请查看 [Experience Manager Guides 发布路线图](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap)。

### 已知问题 {#known-issues-21005}

无。

### 已弃用的功能和 API {#deprecated-21005}

* GRANITE-54164：从公共API中删除了`org.apache.jackrabbit.oak.plugins.blob`。
* GRANITE-54280：从公共API中删除了`org.apache.jackrabbit.oak.cache`。
* GRANITE-58332：在公共API中弃用`org.apache.jackrabbit.oak.plugins.memory`。
* 已弃用适用于javascript的YUI压缩程序。
* 已弃用[Experience Cloud安装程序自动化](/help/sites-cloud/integrating/adobe-analytics-exc-setup-automation.md)功能。

AEM as a Cloud Service 中已弃用和删除的功能和 API 在[已弃用和删除的功能和 API](/help/release-notes/deprecated-removed-features.md) 文档中有详细说明。

### 安全修复 {#security-21005}

AEM as a Cloud Service 致力于优化您平台的安全性和性能。此维护版本解决了 5 个已发现的漏洞，增强了我们对实现强大系统保护的承诺。

### 更改通知 {#change-notice-21005}

* 此版本包含以下新的产品索引版本：
   * **damAssetLucene-12**

先前索引版本的自定义版本将自动与新产品索引版本合并。请对合并版本应用进一步的自定义更新。

#### 更新aem-cloud-testing-clients {#update-aem-cloud-testing-clients-21005}

即将进行的更改需要将在自定义功能测试中使用的库[aem-cloud-testing-clients](https://github.com/adobe/aem-testing-clients)至少更新为版本&#x200B;**1.2.1**（推荐：最新版本1.2.9）

确保您在 `it.tests/pom.xml` 中的依赖项已经升级。

```xml
<dependency>
   <groupId>com.adobe.cq</groupId>
   <artifactId>aem-cloud-testing-clients</artifactId>
   <version>1.2.9</version>
</dependency>
```

此更改需要在2025年6月15日之前执行。
如果未更新依赖项库，则会导致“自定义功能测试”步骤中的管道失败。

### 嵌入的技术 {#embedded-tech-21005}

| 技术 | 版本 | 链接 |
|---|---|---|
| AEM Oak | 1.80.0 | [Oak API 1.80.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.80.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [HTML 模板语言规范](https://github.com/adobe/htl-spec) |
| AEM 核心组件 | 2.29.0 | [AEM WCM 核心组件](https://github.com/adobe/aem-core-wcm-components) |
