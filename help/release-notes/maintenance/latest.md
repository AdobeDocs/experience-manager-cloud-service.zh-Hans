---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 68444ac15513bad7c1eaee97c474e21d36992d49
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 39%

---


# 维护发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

## 发行版本 23482 {#23482}

以下总结了于2025年12月3日公开发布的维护版本23482的持续改进。 上一个维护版本是版本 23385。

激活 2025.12.0 功能后会为此维护版本提供全套功能。有关更多信息，请参阅[&#x200B; Experience Manager 发布路线图](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。


### 增强功能 {#enhancements-23482}

* Assets-49770：为恶意软件扫描结果添加隔离通知。
* Assets-54079：为隔离文件夹应用自定义元数据。
* Assets-54083：创建计划的隔离清理机制。
* Assets-54278：从资源中删除`dam:avScanTime`属性。
* Assets-57284：将文件上传限制到隔离文件夹（禁用拖放）。
* Assets-57428：在Assets视图UI中隐藏隔离文件夹。
* Assets-57626：改进异步资源作业的重试行为。
* Assets-57879：为异步移动/复制资源作业添加合并选项。
* Assets-58099：添加配置以禁用整个环境的增强型智能标记。
* Assets-58136：在Search OpenAPI中实施分页反馈。
* Assets-59402：为文件夹删除API添加异步作业端点：将包导出到内部区域。
* Assets-59966：将Malware Administrators组重命名为Quarantine Administrators。
* Assets-60166：使用VideoViewer.js而不是基于iframe的URL。
* GRANITE-61378：权限调试工具 — ListPrincipals API。
* GRANITE-63235：查询以使用`cq:conf`属性标识站点，支持检测旧页面/版本。
* SITES-30452：带ASO的内容API — 标题和描述建议、XWalk支持、JSON修补程序操作、IMS服务主体绑定。

### 修复的问题 {#fixed-issues-23482}

* Assets-57430：修复Assets视图上传跳过预处理：导出`repoapi.preprocessing`包，将RAPI更新为最新版本。
* Assets-58190：减少收藏集UI中不必要的过高猜测总数。
* Assets-58866：修复了OpenAPI响应中返回的资产标题/描述/ID。
* Assets-58868：当资源上缺少排序字段时修复分页。
* Assets-58920：修复批量资源导入，跳过预处理。
* Assets-59168：修复扫描开始/结束时间显示错误时区的问题。
* Assets-59702：将资源状态设置为无状态时修复事件排序。
* Assets-59830：在终止面板期间停止了对异步作业重新排队。
* Assets-49757：修复了恶意软件检测扫描事件。
* GRANITE-61019：重新启动AEM后首次运行时未通知修补程序`gcMonitor`。
* GRANITE-62717：修复了处理包含非ASCII字符的`JSafe`密码。
* SITES-34331：修复了非管理员用户(`cqLiveSyncCancelled index`)加载转出覆盖时出现503超时的问题。

### 已知问题 {#known-issues-23482}

无。

### 已弃用的功能和 API {#deprecated-23482}

AEM as a Cloud Service 中已弃用和删除的功能和 API 在[已弃用和删除的功能和 API](/help/release-notes/deprecated-removed-features.md) 文档中有详细说明。

### 安全修复 {#security-23482}

AEM as a Cloud Service 致力于优化您平台的安全性和性能。此维护版本解决了 4 个已发现的漏洞，增强了我们对强大系统保护的承诺。

### 嵌入的技术 {#embedded-tech-23482}

| 技术 | 版本 | 链接 |
|---|---|---|
| AEM Oak | 1.88.0 | [Oak 1.88.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.88/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [HTML 模板语言规范](https://github.com/adobe/htl-spec) |
| Apache HTTP 服务器 | 2.4.65 | [Apache Httpd 2.4.65](https://apache.googlesource.com/httpd/+/refs/tags/2.4.65/CHANGES) |
| AEM 核心组件 | 2.30.2 | [AEM WCM 核心组件](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14（默认） | [受支持的 Node.js 版本](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |

