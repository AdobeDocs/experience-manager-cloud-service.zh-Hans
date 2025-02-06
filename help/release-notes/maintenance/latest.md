---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: f7aa50d8a2fa80489c56571caa9a75bc50715368
workflow-type: tm+mt
source-wordcount: '919'
ht-degree: 20%

---


# 维护发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

## 版本 19352 {#19352}

以下总结了维护版本19352的持续改进，该版本于2025年2月5日公开发布。 上一个维护版本是版本 19149。

激活 2025.2.0 功能后会为此维护版本提供全套功能。有关更多信息，请参阅[ Experience Manager 发布路线图](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增强功能 {#enhancements-19352}

* Forms-13998：添加折叠组件。
* Forms-17913：为单选按钮组添加卡片变体。
* Forms-17333：在AEM表单提交中启用HTML电子邮件模板。
* Forms-17702：允许在输出同步API中生成的PDF上传到Azure Blob Storage。
* SITES-28282：带有通用编辑器的Edge Delivery：提供基本路径、站点名称和组织，作为任何页面的页面信息。
* SITES-27055：带有通用编辑器的Edge Delivery：支持反向代理servlet中的查询参数。
* SITES-26796：带有通用编辑器的Edge Delivery：支持分类电子表格的自定义列。
* SITES-26087：带有通用编辑器的Edge Delivery：支持对电子表格进行CSV导出。
* SITES-26265：带有通用编辑器的Edge Delivery：在配置UI中显示要与Edge Delivery集成的TA帐户。
* SITES-20372：带有通用编辑器的Edge Delivery：为电子表格启用基本的MSM用例。
* SITES-26681：带有通用编辑器的Edge Delivery：支持对作者上的分类电子表格使用？sheet=参数。
* SITES-26479： [架构]内容片段模型计划发布状态终结点。
* SITES-25944： [Livecopy概述]添加状态“继承受限的Live Copy为最新版本”。
* SITES-28713： [V2]为内容刮刀添加结构化数据支持。
* SITES-27896：在通知时自动打开CommentsTab。
* SITES-26720：不应允许用户从资产选择器中选择整个收藏集。
* SITES-27875：默认情况下，将容器中的任何可编辑内容设为可移动。
* SITES-28340：深条通用编辑器服务插件。
* SITES-26098：可避免在发布内容片段时发布引用的页面。
* SITES-27789：支持DOM中的数据属性data-aue-component。
* SITES-25997：增强变体以支持修改日期。
* SITES-28023：用于远程资源引用（存储库+资源ID）的GraphQL输出。
* SITES-26058：内容片段模型计划发布状态端点。
* SITES-25108：用于UUID引用的模型迁移。
* SITES-26630：多个内容片段的内容片段计划发布状态端点。
* SITES-23432：改进删除引用功能。
* SITES-25797：支持外部资源引用 — GraphQL。
* SITES-17514：删除端点增强以取消发布内容片段。
* SITES-14633：验证内容片段模型，在安装之前创建负载 — 试运行。

### 修复的问题 {#fixed-issues-19352}

* SITES-28415：带有通用编辑器的Edge Delivery：修复电子表格的“打开属性”按钮。
* SITES-26669：使用通用编辑器的Edge Delivery：修复了在上传以UTF-8编码并以电子表格形式使用BOM的CSV文件时的问题。
* SITES-26543：使用通用编辑器的Edge Delivery：修复没有模型渲染错误标记的空块。
* SITES-26857：使用通用编辑器的Edge Delivery：修复了在基于文件的配置用户界面中可见的站点身份验证令牌。
* SITES-26662：使用通用编辑器的Edge Delivery：修复区分大小写的批量元数据的问题。
* SITES-28133：将Publish设为“预览”会导致内容在生产环境中可用。
* SITES-27187：计划页面/资产激活，包括未发布引用的引用（实验性）。
* SITES-27264： 2与Content-Fragment-LiveCopy-Creation相关的Selenium测试在主服务器上始终失败。
* SITES-26559：将内容片段模型的查询固定到cqPageLucene索引。
* SITES-24469：交互式元素无法通过键盘访问。
* SITES-24518：“父引用”表格中的“名称”和“模型”按钮不可使用键盘。
* SITES-27937：更新模型后，UISchema约束设置为null。
* SITES-27852：模型UISchema缺少分类。
* SITES-27904：完整投影的列表/搜索内容片段模型中缺少MetadataSchema。
* SITES-26827：列出片段最终会陷入无限循环。
* SITES-27678： [性能]防止不必要地获取_references。
* SITES-27589：具有多个内容/片段引用字段的内容片段模型的UUID升级失败。
* SITES-26679：取消发布内容片段模型应仅验证已发布的引用。
* SITES-26666：referencesTree和引用端点返回不同的结果。
* SITES-26499：标记字段的值在GET片段中的顺序错误，PATCH会随机排列这些顺序。
* SITES-26585：修复架构中的小描述错误。
* SITES-26647：对非管理员用户而言，删除端点和UnpublishFragments引用验证可能会失败。
* SITES-26458： [搜索内容片段模型]按复制状态修复筛选。
* SITES-23513： [内容片段模型编辑器]对“片段引用” — “允许的内容片段模型”属性验证失败。
* SITES-26575：从预览中取消发布片段应更新previewStatus。
* SITES-26571：启用FT_SITES-12435时，无法保存页面引用。
* SITES-26660：当@ContentType为“字符串”类型时，内容片段版本比较可能会中断。
* SITES-26626：数字和布尔字段上缺少customErrorMessage。
* SITES-26268：如果在创建片段时引用无效，则返回错误状态代码。
* Forms-18098、FORMS-17954：在Microsoft Edge浏览器的Internet Explorer模式下加载自适应Forms失败。
* Forms-17162：发布资源会导致运行OOTB查询，从而降低发布性能。

### 已知问题 {#known-issues-19352}

无。

### 已弃用的功能和 API {#deprecated-19352}

AEM as a Cloud Service 中已弃用和删除的功能和 API 在[已弃用和删除的功能和 API](/help/release-notes/deprecated-removed-features.md) 文档中有详细说明。

### 安全修复 {#security-19352}

AEM as a Cloud Service 致力于优化您平台的安全性和性能。此维护版本解决了 36 个已发现的漏洞，增强了我们对强大系统保护的承诺。

### 嵌套的技术 {#embedded-tech-19352}

| 技术 | 版本 | 链接 |
|---|---|---|
| AEM Oak | 1.72.0 | [Oak API 1.72.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.72.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.24-1.4.0 | [HTML 模板语言规范](https://github.com/adobe/htl-spec) |
| AEM 核心组件 | 2.27.0 | [AEM WCM 核心组件](https://github.com/adobe/aem-core-wcm-components) |
