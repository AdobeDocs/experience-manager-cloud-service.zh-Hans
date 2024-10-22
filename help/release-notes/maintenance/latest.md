---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 9278ec9bb5bccd7b40cd65a120f296faba454b9c
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 35%

---


# 维护发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

## 版本 18311 {#18311}

以下总结了维护版本18311的持续改进，该版本于2024年10月22日公开发布。 上一个维护版本是版本 18175。

激活 2024.10.0 功能后会为此维护版本提供全套功能。有关更多信息，请参阅[ Experience Manager 发布路线图](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增强 {#enhancements-18311}

* Assets-41820 ：改进了处理监视程序的索引编制。
* Assets-43720 ：改进了处理监视程序的功能。
* Assets-42554 ：改进了大型文件夹的性能。
* SKYOPS-77603 ：按业务用户管理重定向。

### 修复的问题 {#fixed-issues-18311}

* Assets-37534 ：搜索发生了更改，不会公开用于批准目标的资产。
* Assets-38322 ：移除发布标准提供程序配置移除发布事件功能。
* Assets-40482 ：Scene7视频播放器的播放/暂停和静音/取消静音按钮中存在辅助功能问题。
* Assets-40593 ：单击“Assets”>“文件”中的“属性”按钮后出现错误页面。
* Assets-40598 ：将未同步的资源移动到启用同步的文件夹时，同步智能裁剪。
* Assets-40743 ：当文件名中存在某些字符时，触发替换资源对话框时出现问题。
* Assets-40825 ：Assets搜索Facet在编辑搜索表单后消失。
* Assets-41007 ：在AEM上删除有时会留下投放孤立的Assets。
* Assets-41172 ：Dynamic Media模板中不允许在名称中使用特殊字符。
* Assets-41896 ：不应将文件夹上cq：discarded属性中提到的Assets发布到Brand Portal。
* Assets-42067 ：Dynamic Media模板 — 下载时出错。
* Assets-42070 ：Dynamic Media模板 — 非管理员用户应具有模板创建/编辑权限。
* Assets-42344 ：连接的Assets同步已断开连接 — 重新连接并提供给客户的建议。
* Assets-42620 ：资源版本的预览选项问题 — 打开资源时显示空白预览。
* Assets-42701 ：Web优化图像投放和裁切问题。
* Assets-42966 ：如果多个作业共享同一路径，则异步阻止可能会出错而解锁。
* Assets-43072 ：Dynamic Media模板 — 模板引用查找中断了无效的引用。
* Assets-43212 ：元数据架构编辑器中存在国际化问题。
* Assets-43202 ：修复了从时间轴中选择要打印的注释的问题。
* Assets-43502 ：编辑页面上不显示AEM CS现有图像预设名称。
* Assets-43538 ：异步复制资源作业对源路径使用不正确的属性。
* Assets-43798 ：在复制资源之前，首先检查目标路径。
* Assets-43945 ：将异步资源作业队列的重试延迟增加到20分钟。
* Assets-44025 ：当选择单个资源时，异步删除资源作业失败。
* SITES-26128 ：CreateLiveCopyStep中出现类转换异常。
* SCRNS-4551 ： [SG池]包含视频组件的Screens渠道在浏览器预览和播放器上显示“一般页面错误”

### 已知问题 {#known-issues-18311}

* FORMS - 15818：组件描述符条目 `OSGI-INF/com.adobe.aemfd.docmanager.impl.*.xml` 在服务器日志中未找到语句。这些是无害的日志语句。

### 已弃用的功能和 API {#deprecated-18311}

AEM as a Cloud Service 中已弃用和删除的功能和 API 在 [已弃用和删除的功能和 API](/help/release-notes/deprecated-removed-features.md) 文档中有详细说明。

### 安全修复 {#security-18311}

AEM as a Cloud Service 致力于优化您平台的安全性和性能。此维护版本解决了 3 个已发现的漏洞，增强了我们对强大系统保护的承诺。

### 嵌套的技术 {#embedded-tech-18311}

| 技术 | 版本 | 链接 |
|---|---|---|
| AEM Oak | 1.70.0 | [Oak API 1.70.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.70.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.24-1.4.0 | [HTML 模板语言规范](https://github.com/adobe/htl-spec) |
| AEM 核心组件 | 2.27.0 | [AEM WCM 核心组件](https://github.com/adobe/aem-core-wcm-components) |
