---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: c8a798e1f1b7234f91682b6e5ef7072e024df022
workflow-type: tm+mt
source-wordcount: '693'
ht-degree: 33%

---


# 维护发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

## 版本 18751 {#18751}

以下总结了于2024年12月11日公开发布的维护版本18751的持续改进。 上一个维护版本是版本 18598。

激活 2025.1.0 功能后会为此维护版本提供全套功能。有关更多信息，请参阅[ Experience Manager 发布路线图](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增强功能 {#enhancements-18751}

* SKYOPS-88509：对AEM SDK的Java 21支持。

### 修复的问题 {#fixed-issues-18751}

* Assets-42802： MFE上的“返回”按钮始终不起作用，并显示额外的对话框。
* Assets-44148：AEM中的固定NODE_MOVED事件可能会导致NPE。
* Assets-44418：未在Skyline上配置“修复的正确环境”。
* Assets-44821：修复了更新事件过滤器，以包含用于上传事件的表单URL编码数据。
* CNTBF-298：固定内容复制因UUID冲突而失败。
* CNTBF-331： [content-copy-bundle]版本2.0.14。
* Forms-16572：删除Java 21 SDK内部版本的工作流测试失败。
* GRANITE-36205：QS中的内部Oak版本的自动更新。
* GRANITE-53704：重新评估存储库服务上的Sling发现。
* GRANITE-54300：将 Oak 更新至最新公开版本 (1.70.0)。
* GRANITE-54416：将 Filevault 更新到 3.8.2。
* GRANITE-54462：将SubscriberAgent配置为使用“systemready”的hc.tags。
* GRANITE-54542：将commons-io依赖关系更新为2.17.0。
* GRANITE-54658：为QS中的fullGC添加delayFactor和批量大小OSGi配置。
* GRANITE-54696：扩大Jackrabbit API的导入范围。
* GRANITE-54803：当imsauth处于活动状态时，在AEM中禁用ClusterAtExchange。
* GRANITE-55095：将 Oak 更新至最新公开版本 (1.72.0)。
* GUIDES-20006：在保存新版本之前，标记为“完成”的文档状态将还原为“草稿”，从而导致“完成”状态不会在任何文档版本中持续存在。
* GUIDES-21840：在本机PDF输出中，目录中的章节标题缺失，导致层次结构不正确。
* GUIDES-19558：如果基线具有大量主题或映射，则在1分钟后编辑基线并将其保存到云设置中将会超时。
* GUIDES-19733：使用基线的映射翻译变得缓慢，最终无法加载所有关联主题和映射文件的列表。
* SITES-26798：“启动项自动促销”未更新促销状态（促销日期）。
* SITES-27137：从MSM核心中删除Sling Commons量度依赖关系。
* SKYOPS-75446：修复的AEM有时返回404或页面缺少内容。
* SKYOPS-76366：AEM发行说15977和更高版本中没有Jetty Threadpool量度。
* SKYOPS-82371： java.io.IOException： classFile.delete()失败。
* SKYOPS-83369：如果转换作业执行不生成捆绑包，则AEM部署无法启动。
* SKYOPS-83910：修复了SKYOPS-82371中的并发问题。
* SKYOPS-84821：将Sling主Servlet的sling.include.checkcontenttype配置设置为true。
* SKYOPS-85798：固定转换作业生成空索引定义。
* SKYOPS-86251：升级到AEM Analyzer核心1.5.6，并在转换作业中启用产品包导入分析器。
* SKYOPS-86710：删除Java 21 sdk内部版本的最小测试失败。
* SKYOPS-86745：更新至Sling ResourceResolver 1.12.2。
* SKYOPS-89616：修复了无法在Adobe Developer Console中创建技术帐户的问题。
* SKYOPS-89691：修复了用于ASM警告的不正确工件ID。
* SKYOPS-89699：Groovy控制台的“orbinson”风格中嵌入的旧Groovy版本缺少警告。
* SKYOPS-88664：记录并防止下载的映射文件行超过1024限制的情况。
* SKYOPS-89734：发布Dispatcher图像2.0.235。

有关 Experience Manager Guides 中的新增功能、增强功能和已修复问题的更多信息，请查看 [Experience Manager Guides 发布路线图](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap)。

### 已知问题 {#known-issues-18751}

无。

### 已弃用的功能和 API {#deprecated-18751}

AEM as a Cloud Service 中已弃用和删除的功能和 API 在[已弃用和删除的功能和 API](/help/release-notes/deprecated-removed-features.md) 文档中有详细说明。

### 安全修复 {#security-18751}

AEM as a Cloud Service 致力于优化您平台的安全性和性能。此维护版本解决了 3 个已发现的漏洞，增强了我们对强大系统保护的承诺。

### 嵌套的技术 {#embedded-tech-18751}

| 技术 | 版本 | 链接 |
|---|---|---|
| AEM Oak | 1.72.0 | [Oak API 1.72.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.72.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.24-1.4.0 | [HTML 模板语言规范](https://github.com/adobe/htl-spec) |
| AEM 核心组件 | 2.27.0 | [AEM WCM 核心组件](https://github.com/adobe/aem-core-wcm-components) |
