---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 13124956fcce105ad42767f67b700284c8250012
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 31%

---


# 维护发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

## 版本 21644 {#21644}

以下总结了维护版本21644的持续改进，该版本于2025年7月22日公开发布。 上一个维护版本是版本 21570。

激活 2025.7.0 功能后会为此维护版本提供全套功能。有关更多信息，请参阅[ Experience Manager 发布路线图](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增强功能 {#enhancements-21644}

* Assets-39377：在Assets批量导入程序中改进对远程存储429的处理。
* Assets-46026：元数据导出器的可配置最大深度。
* Assets-49172： Dynamic Media模板资源应继承文件夹中的元数据。
* Assets-50209：支持DM模板中的子字符串。
* Assets-52326： AEM Assets配置页面可设置Assets的标题显示首选项。
* Assets-52805：为批量操作作业添加CSV输出/下载支持。
* Assets-52873：在文件夹属性中添加新配置以禁用该文件夹的AI处理。
* Assets-53535：改进了YouTube视频上传性能。
* Assets-53612：控制Assets Omnisearch中的混合搜索。
* GRANITE-60183：将commons-fileupload依赖项更新为1.6.0。
* GRANITE-60287：将QS更新为Jackrabbit 2.22.1。
* SITES-30452：带ASO的内容API — 标题和描述建议。
* SITES-31677：自定义工作区现已支持将 AEM 内容片段导出至 Target。
* SKYOPS-112741：从AEM-CS SDK中删除`com.adobe.granite.product.support`捆绑包。

### 修复的问题 {#fixed-issues-21644}

* Assets-12882：打开查看器预设后，UI对齐出现问题。
* Assets-48958：资产同步更改站点本地AEM中的已发布状态的问题。
* Assets-50856： completeUpload未重置`dam:processingAttempts`。
* Assets-51604：链接共享报表CSV缺少“共享对象”数据。
* Assets-51783：如果使用搜索查询未找到配置，则回退到`/conf/global`下的DM配置。
* Assets-51857：资源表项目不可重新排序。
* Assets-52169：新的BAT计算机演绎版错误地包含在资源下载中。
* Assets-52229：AEM as a Cloud Service中缺少资产报表的收件箱通知。
* Assets-52399： com.day.cq.dam.api中的版本提升可能会破坏客户代码。
* Assets-52780：即使未启用切换，也可以将资源标记为预览。
* Assets-52866：在禁用DM同步的情况下，迁移的DM视频在文件夹下保持处理状态。
* Assets-53237：“图像预设”编辑器中的“颜色配置文件”下拉列表为空。
* Assets-53240：资源报表 — 从Dynamic Media获取资源演绎版大小时，“磁盘使用情况”失败。
* Assets-53446：由于NPE，YouTube身份验证令牌间歇性刷新失败。
* Assets-53827： ACL验证阻止保存混合媒体集。
* Assets-5403：发布实例上使用的Dynamicmedia clientlibs应具有`allowProxy=true`。
* Assets-54261：元数据导入会泄漏连接，如果文件下载失败，则会被阻止。
* CQ-4359863：内容片段编辑器/资产编辑器中关键字的标记搜索顺序不正确。
* CQ-4359958：使openapi-support与AEM 6.5.22.0及更高版本兼容。
* CQ-4360256：在通过`/adobe` servlet上下文处理的HTTP请求的请求路径中包含servlet上下文路径。
* CQ-4360317：添加用于在构建响应时设置失效日期标头的方法。
* GRANITE-60311： AEM SDK Quickstart - “OSGi Installer Configuration Printer”上的NPE。
* GS-15285：用户显示为已停用。

### 已知问题 {#known-issues-21644}

无。

### 已弃用的功能和 API {#deprecated-21644}

AEM as a Cloud Service 中已弃用和删除的功能和 API 在[已弃用和删除的功能和 API](/help/release-notes/deprecated-removed-features.md) 文档中有详细说明。

### 安全修复 {#security-21644}

AEM as a Cloud Service 致力于优化您平台的安全性和性能。此维护版本解决了 4 个已发现的漏洞，增强了我们对强大系统保护的承诺。

### 嵌入的技术 {#embedded-tech-21644}

| 技术 | 版本 | 链接 |
|---|---|---|
| AEM Oak | 1.80.0 | [Oak API 1.80.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.80.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [HTML 模板语言规范](https://github.com/adobe/htl-spec) |
| Apache HTTP Server | 2.4.63 | [Apache Httpd 2.4.63](https://github.com/apache/httpd/blob/2.4.63/CHANGES) |
| AEM 核心组件 | 2.29.0 | [AEM WCM 核心组件](https://github.com/adobe/aem-core-wcm-components) |
