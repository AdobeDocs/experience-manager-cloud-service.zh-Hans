---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: f12e60cdfce24dd2f6c1400157180d16b1b98653
workflow-type: tm+mt
source-wordcount: '998'
ht-degree: 18%

---


# 维护发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

## 版本 17393 {#release-17393}

以下总结了维护版本17393的持续改进，该版本于2024年8月13日公开发布。 上一个维护版本是版本 17258。

2024.8.0 功能激活将会为此维护版本提供全套功能。有关更多信息，请参阅[ Experience Manager 发布路线图](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增强 {#enhancements-17393}

* Forms-15436 — 在Adobe Sign状态计划程序中正常处理异常。
* Forms-15362 — 在aemds中为forms-foundation添加配置以启用登录。
* Forms-15261 - SPA不会在Forms编辑器中渲染。
* Forms-15138 — 处理由于sling commons json升级而导致的双重数据向后兼容性。
* Forms-15113 — 将密钥名称从vistorId更改为sid，以便进行RUM跟踪。
* Forms-15103 — 表单中附加的Assets未在Edge交付中发布。
* Forms-15082 — 要映射到自定义自适应表单组件的JSON架构。
* Forms-15002 - v1片段的模板类型注册。
* Forms-14845 — 通过Forms Manager支持核心组件库表单中的xdpRef。
* Forms-14840 - Forms预填充服务错误。
* Forms-14836 — 改进表单管理器UI，以列出AF1片段模板。
* Forms-14834 — 模板支持AF1中的片段。
* Forms-14275 — 在嵌入容器中覆盖感谢页面和感谢消息。
* Forms-13623 — 为V2启用基于时间的自动保存功能。
* Forms-8651 — 有关更改表单属性页面上的数据模型配置的警告对话框。
* SITES-23310 — 内容片段REST API：防止内容片段的嵌套引用中出现循环依赖关系。
* SITES-23285 — 内容片段REST API：创建端点以列出所有可用语言。
* SITES-22857 — 内容片段REST API：复选框枚举字段不应允许将多个属性设置为false。
* SITES-22813 — 内容片段REST API：定义枚举字段的最小值/最大值属性。
* SITES-22031 — 内容片段REST API：获取片段文件夹的允许内容片段模型。
* SITES-17640 — 内容片段REST API：内容片段Publish操作验证。
* SITES-22677 — 内容片段REST API：检索后代引用的简单列表
* SITES-22207 — 创建内容片段时重复的模型。
* SITES-23093 — 事件：将标记添加到内容片段模型事件的负载。
* SITES-23092 — 事件：将标记添加到内容片段事件的负载。
* SITES-22447 — 将体验片段属性继承支持添加到基本属性选项卡。
* SITES-12209 — 通过将cq：policy添加到索引来提高策略编辑器的性能。

### 修复的问题 {#fixed-issues-17393}

* CQ-4358028 — 如果上传了缩略图，则无法创建项目。
* CQ-4357891 — 导出的XLIFF的序列问题。
* CQ-4357059 — 翻译作业需要几个小时才能完成，导致AEMaaCS中出现503超时。
* Forms-15320 — 基于核心组件的表单中无法提交电子邮件。
* Forms-15272 - AEM Forms — 复选框组仅发送1个值。
* Forms-15269 — 维护版本16461行后面临产品相关问题。
* Forms-15174 - JsonSchemaParser isValid问题。
* Forms-15095 — 多行文本框可以拉长到AEM Forms中包含的面板之外。
* Forms-15057 — 对于提交> 999，FDM Sharepoint列表抛出附件错误。
* Forms-15011 — 在编辑器中打开表单时，核心编辑器导致控制台错误。
* Forms-14809 — 未在共享的临时目录中自动创建SDK文件夹。
* Forms-14327 - Forms服务API ：提取数据： — 当输入中提供非交互式pdf时，会提供500个响应代码。
* Forms-7475 — 排序功能在自适应表单创建页面上不起作用。
* Forms-3309 — 如果在提交表单时选择了多个选项，则在生成的DoR中只显示一个选项。
* SITES-23646 — 对于使用OpenAPI创建的模型，如果字段包含唯一值，则GraphQL模型端点失败。
* SITES-23637 — 内容片段REST API： OpenAPI没有为枚举使用正确的值类型。
* SITES-23573 — 内容片段REST API：未按uuid遵循GET内容片段的实时关系。
* SITES-23535 — 内容片段REST API：内容片段模型枚举多个字段具有空值。
* SITES-23534 — 内容片段REST API：内容片段验证ClassCastException。
* SITES-23524 — 调整GraphQL BFF模型端点以支持多字段枚举字段。
* SITES-23467 — 内容片段REST API：由于光标问题，搜索模型失败。
* SITES-23327 - AuditLogTimelineEventProvider中的ArrayIndexOutOfBoundsException在时间线事件处理说明期间发生。
* SITES-23277 — 内容片段REST API：应仅对活动副本执行内容片段字段实时关系检查。
* SITES-23232 — 自定义验证在新的CF编辑器UI中不起作用。
* SITES-23090 — 内容片段REST API：无法更新锁定的内容片段的标题。
* SITES-22981 — 不发布提升不深的嵌套启动项。
* SITES-22870 - PathAttributesHandler.processSrcAttr ArrayIndexOutOfBoundsException。
* SITES-22814 — 内容片段REST API：复选框枚举片段字段值应按照模型中定义的键排序。
* SITES-22716 - OOTB组件实时使用列表问题。
* SITES-22457 — 提升非深层启动项不会更新源内容。
* SITES-22449 — 在AEM P20升级后，无法保存内容片段中的更改。
* SITES-22279 — 内容片段REST API：内容片段缺少枚举类型的唯一属性。
* SITES-22203 — 内容片段REST API：调整管理API以针对同一情况做出相同的响应。
* SITES-21973 — 内容片段REST API：模型缺少枚举类型的唯一属性。
* SITES-20364 - 302重定向不适用于URL中的选择器。
* SITES-21198 - VersionPreviewServlet：清理在所有群集节点上并行运行，从而导致合并冲突和块提交
* GRANITE-53094 — 使用相对路径时，无法找到基于存储库的JS使用对象。

### 已知问题 {#known-issues-17393}

无。

### 更改通知 {#change-notice-17393}

* 从 2024 年 9 月开始，AEM as a Cloud Service 将会通过 Sling Model Exporter 框架禁用资源解析器的序列化。请参阅[该文档](/help/implementing/developing/hybrid/disallow-the-serialization-of-resourceresolvers-via-sling-model-exporter.md)了解更多详情。

### 已弃用的功能和 API {#deprecated-17393}

AEM as a Cloud Service 中已弃用和删除的功能和 API 在 [已弃用和删除的功能和 API](/help/release-notes/deprecated-removed-features.md) 文档中有详细说明。

### 嵌套的技术 {#embedded-tech-17393}

| 技术 | 版本 | 链接 |
|---|---|---|
| AEM Oak | 1.66.0 | [Oak API 1.66.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.66.0/index.html) |
| AEM SLING API | 2.27.2 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.24-1.4.0 | [HTML 模板语言规范](https://github.com/adobe/htl-spec) |
| AEM 核心组件 | 2.25.4 | [AEM WCM 核心组件](https://github.com/adobe/aem-core-wcm-components) |
