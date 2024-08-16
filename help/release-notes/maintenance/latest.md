---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 80edd0255b38beee93b3f9c779ae0f364500b4a5
workflow-type: tm+mt
source-wordcount: '1176'
ht-degree: 79%

---


# 维护发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

## 版本 17465 {#release-17465}

以下总结了维护版本17465的持续改进，该版本于2024年8月14日公开发布。 上一个维护版本是版本 17258。

2024.8.0 功能激活将会为此维护版本提供全套功能。有关更多信息，请参阅[ Experience Manager 发布路线图](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增强 {#enhancements-17465}

* FORMS-15436 - 妥善处理 Adobe Sign 状态调度程序中的异常。
* FORMS-15362 - 在 aemds 中添加 forms-foundation 的配置以启用登录。
* FORMS-15261 - SPA 未在表单编辑器中呈现。
* FORMS-15138 - 由于 sling commons json 升级而导致的双重数据向后兼容性处理。
* FORMS-15113 - 将密钥名称从 vistorId 更改为 sid，以进行 RUM 跟踪。
* FORMS-15103 - 表单中附加的资产未在边缘交付中发布。
* FORMS-15082 - 用于映射到自定义自适应表单组件的 JSON 模式
* FORMS-15002 – v1 片段的模板类型注册。
* FORMS-14845 - 通过表单管理器支持核心组件库中的 xdpRef。
* FORMS-14840 – 表单预填服务错误。
* FORMS-14836 - 改进表单管理器 UI，列出 AF1 片段模板。
* FORMS-14834 - AF1 中对片段的模板支持。
* FORMS-14275 - 覆盖嵌入容器中的感谢页面和感谢信息。
* FORMS-13623 - 为 V2 启用基于自动保存时间的功能。
* FORMS-8651 - 在表单属性页面上更改数据模型配置时出现警告对话框。
* SITES-23310 - 内容片段 REST API：防止内容片段的嵌套引用中的循环依赖。
* SITES-23285 - 内容片段 REST API：创建端点以列出所有可用的语言。
* SITES-22857 - 内容片段 REST API：复选框枚举字段不应允许将多个属性设置为 false。
* SITES-22813 - 内容片段 REST API：为枚举字段定义最小/最大属性。
* SITES-22031 - 内容片段 REST API：获取片段文件夹允许的内容片段模型。
* SITES-17640 - 内容片段 REST API：内容片段发布操作验证。
* SITES-22677 — 内容片段REST API：检索后代引用的简单列表。
* SITES-22207 - 内容片段创建时模型重复。
* SITES-23093 - 事件：为内容片段模型事件的有效负载添加标记。
* SITES-23092 - 事件：为内容片段事件的有效负载添加标记。
* SITES-22447 - 在基本属性选项卡中添加体验片段属性继承支持。
* SITES-12209 - 通过将 cq:policy 添加到索引来提高策略编辑器的性能。

### 修复的问题 {#fixed-issues-17465}

* CQ-4358028 - 如果上传了缩略图，则无法创建项目。
* CQ-4357891 - 导出的 XLIFF 的序列问题。
* CQ-4357059 - 翻译工作需要数小时才能完成，导致 AEMaaCS 出现 503 超时。
* FORMS-15320 - 在基于核心组件的表单中，电子邮件提交不起作用。
* FORMS-15272 - AEM Forms - 复选框组仅发送 1 个值。
* FORMS-15269 - 维护版本 16461 后面临与产品相关的问题。
* FORMS-15174 - JsonSchemaParser isValid 问题。
* FORMS-15095 - 多行文本框可以延伸至 AEM Forms 中包含的面板之外。
* FORMS-15057 - FDM Sharepoint 列表抛出提交附件错误 > 999。
* FORMS-15011 - 在编辑器中打开表单时核心编辑器导致控制台错误。
* FORMS-14809 - 共享临时目录中未自动创建 SDK 文件夹。
* FORMS-14327 - 表单服务 API：提取数据：- 当输入中提供非交互式 pdf 时提供 500 响应代码。
* FORMS-7475 - 自适应表单创建页面上的排序不起作用。
* FORMS-3309 - 如果在提交表单时选择了多个选项，则在生成的 DoR 中只会显示一个选项。
* SITES-23646 - 如果字段包含唯一值，则使用 OpenAPI 创建的模型的 GraphQL 模型端点会失败。
* SITES-23637 - 内容片段 REST API：OpenAPI 没有使用正确的枚举值类型。
* SITES-23573 - 内容片段 REST API：通过 uuid 获取内容片段时不尊重实时关系。
* SITES-23535 - 内容片段 REST API：内容片段模型枚举多字段具有空值。
* SITES-23534 - 内容片段 REST API：内容片段验证 ClassCastException。
* SITES-23524 - 调整 GraphQL BFF 模型端点以支持多字段枚举字段。
* SITES-23467 - 内容片段 REST API：由于光标问题，搜索模型失败。
* SITES-23327 - 时间线事件处理期间 AuditLogTimelineEventProvider 中出现 ArrayIndexOutOfBoundsException 描述。
* SITES-23277 - 内容片段 REST API：内容片段字段实时关系检查仅应针对实时副本进行。
* SITES-23232 - 自定义验证在新 CF 编辑器 UI 中不起作用。
* SITES-23090 - 内容片段 REST API：无法更新已锁定的内容片段的标题。
* SITES-22981 - 推广不深入的嵌套发布不会发布。
* SITES-22870 - PathAttributesHandler.processSrcAttr ArrayIndexOutOfBoundsException。
* SITES-22814 - 内容片段 REST API：复选框枚举片段字段值应按模型中定义的键排序。
* SITES-22716 - OOTB 组件实时使用列表存在问题。
* SITES-22457 - 推广不够深入的发布不会更新源内容。
* SITES-22449 - AEM P20 升级后无法保存内容片段中的更改。
* SITES-22279 - 内容片段 REST API：内容片段缺少枚举类型的唯一属性。
* SITES-22203 - 内容片段 REST API：调整管理 API 以对相同情况做出相同响应。
* SITES-21973 - 内容片段 REST API：模型缺少枚举类型的唯一属性。
* SITES-20364 - 302 重定向无法与 URL 中的选择器一起使用。
* SITES-21198 - VersionPreviewServlet：清理在所有群集节点上并行运行，从而导致合并冲突和块提交。

### 已知问题 {#known-issues-17465}

* Assets-40875 - AssetDeleteHandler类侦听资源删除事件，并根据删除DELETE类型(PRE_event或POST_event)执行特定DELETE。 在某些情况下，POST的DELETE类型会导致NullPointerException。
* Forms-14340 — 实例化FormsAndDocumentOmniSearchHandler和CloudStorageSubmitActionInserter时出错。 这些是无害的log语句。
* Forms-15818 — 组件描述符条目“OSGI-INF/com.adobe.aemfd.docmanager.impl”。在服务器日志中找不到*.xml&#39;语句。 这些是无害的log语句。
* 
   * SITES-23662 — 无法从服务器日志中的JCR日志语句中提取触发发布的用户。 这是针对正在开发的功能，该功能可能会在日志中导致“在批次OSGI事件中找不到有效用户ID”的间歇性且无害的错误。

### 更改通知 {#change-notice-17465}

* 从 2024 年 9 月开始，AEM as a Cloud Service 将会通过 Sling Model Exporter 框架禁用资源解析器的序列化。请参阅[该文档](/help/implementing/developing/hybrid/disallow-the-serialization-of-resourceresolvers-via-sling-model-exporter.md)了解更多详情。

### 已弃用的功能和 API {#deprecated-17465}

请注意，我们正在更新`com.day.cq.wcm.api`，并且在当前版本中，我们已将它的几个方法和类标记为`@Deprecated`。 这些功能将在未来版本中删除，因此，如果您使用任何这些功能，请考虑改用其建议的替代功能。

AEM as a Cloud Service 中已弃用和删除的功能和 API 在 [已弃用和删除的功能和 API](/help/release-notes/deprecated-removed-features.md) 文档中有详细说明。

### 安全修复 {#security-17465}

AEM as a Cloud Service致力于优化平台的安全性和性能。 此维护版本解决了7个已识别的漏洞，强化了我们对强大系统保护的承诺。

### 嵌套的技术 {#embedded-tech-17465}

| 技术 | 版本 | 链接 |
|---|---|---|
| AEM Oak | 1.66.0 | [Oak API 1.66.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.66.0/index.html) |
| AEM SLING API | 2.27.2 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.24-1.4.0 | [HTML 模板语言规范](https://github.com/adobe/htl-spec) |
| AEM 核心组件 | 2.25.4 | [AEM WCM 核心组件](https://github.com/adobe/aem-core-wcm-components) |
