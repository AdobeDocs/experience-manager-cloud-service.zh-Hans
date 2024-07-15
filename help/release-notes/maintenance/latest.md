---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 9303ecadea38d83bd71ed0d440067bae5c419940
workflow-type: tm+mt
source-wordcount: '944'
ht-degree: 100%

---

# 维护发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

## 版本 16971 {#release-16971}

下面总结了维护版本 16971 的持续改进，该版本已于 2024 年 7 月 3 日公开发行。上一个维护版本是版本 16799。

2024.7.0 功能激活将会为此维护版本提供全套功能。有关更多信息，请参阅[ Experience Manager 发布路线图](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增强 {#enhancements-16971}

* SITES-22948：删除 AEM CS 基础内容中的商业引用。
* SITES-22141：[内容片段] OnRC 之后，CFM ModelChangeRepositoryImpl 出现 SegmentNotFoundException。
* SITES-21893：作者实例上的图像裁切问题。
* SITES-21788：[内容片段] 当为模型启用 uiSchema 时，在 CF 和 CF 模型编辑器中显示注释。
* SITES-21688：MSM 转出不会更新实时副本页面上的体验片段 (XF) 路径。
* SITES-21659：返回创建/修改/复制模型资源用户的全名。
* SITES-21609：OpenAPI 端点用于将一个模型的内容片段迁移到另一个模型。
* SITES-21598：[Open API] 创建 CFM：如果给定的配置路径不存在则返回错误。
* SITES-21491：[Open API] CF PATCH 端点应尊重字段级别的实时关系。
* SITES-21434：[Open API] CF GET 端点应尊重字段级别的实时关系。
* SITES-21415：CF 编辑器，支持 UUID 引用。
* SITES-21326：[Open API] 提供有关内容片段参考存在的信息。
* SITES-21310：[Open API] 在翻译 API 响应中添加内容片段的 id。
* SITES-20859：CF Open API，通过路径检索片段时返回引用。
* SITES-20687：[Open API] 进行批处理状态检索的端点。
* SITES-20657： [Open API] 提供使用 `FindAndReplace` 端点替换字符串时匹配整个单词的选项。
* SITES-20587：[Open API] 为内容片段创建 `COPY` 端点。
* SITES-20584：[Open API] 优化参考检索。
* SITES-20308：[Open API] 对 API 启用批处理。
* SITES-19976：[Open API] 条件字段的通用 UI 架构。
* SITES-19556：[内容片段] 编辑模型时，如果 uiSchema 存在，则更新它。
* SITES-18056：[Open API] 将内容片段发布到预览时，包含参考资料。
* SITES-16898：[架构] OpenAPI 端点用于将一个模型的内容片段迁移到另一个模型。
* SITES-16609：列出启动端点。
* SITES-16606：创建启动端点。
* SITES-21617：[Xwalk] 使页面属性/元数据在 UE 内可编辑。
* SITES-19614：[Xwalk] 电子表格编辑器分页和无限滚动。
* SITES-22163：[Xwalk] 改进了对从 Edge Delivery Sites 的发布层提供的内容的支持。
* SITES-22109：[Xwalk] 改进了富文本标记后期处理。
* SITES-22035：[Xwalk] 改进了 MSM 和启动的处理。
* SITES-21839：[Xwalk] 改进了 Edge Delivery 未提供的内容的路径映射和清理。

### 修复的问题 {#fixed-issues-16971}

* CQ-4356898：[翻译] CF 发生内存不足错误，其中包含大量链接。
* CQ-4357055：[翻译] 使用 Rest API 自动翻译不起作用。
* CQ-4353931：[翻译] 若缺少 jcr:uuid，则在翻译源页面/xf/资源中添加。
* CQ-4357591：[翻译] 修改“关联 JCR:UUID”工作流程以适用于页面/XF。
* FORMS-14844：尽管 reCAPTCHA 验证失败，自适应表单仍允许提交表单。
* FORMS-14984：如果提交的数据中缺少“submitMetaData”，则带有 CAPTCHA 的表单会跳过验证。
* FORMS-14477：规则编辑器中的“在之后”和“在之前”选项在日期选择器验证中出现故障。
* FORMS-14019：规则编辑器的“调用服务”功能在通用编辑器中不起作用。
* FORMS-14336：当未选择任何表单字段时，编辑器应打开并聚焦于整个表单元素。
* FORMS-15061：使用规则编辑器中的调用服务选项时，加载器循环会无限期地持续存在。
* SITES-22457：推广不够深入的发布不会更新源内容。
* SITES-22748：[内容片段] 增强内容片段更新作业的错误处理
* SITES-22349：[内容片段] 空的多行 cf 元素的 ContentType 无法更改。
* SITES-22343：[内容片段] 语义类型“枚举”已损坏。
* SITES-22194：设置重定向后，model.json 不再起作用。
* SITES-21953：[打开 API] Etag 会根据 validationStatus 的顺序进行更改。
* SITES-21894：[打开 API] 创建 CF 时增强父路径验证。
* SITES-21887：[打开 API] POST 变体端点返回的 ETag 无效。
* SITES-21657：[Open API] 改进 CF 搜索路径属性的验证。
* SITES-21949：搜索 API 无效光标会返回 500。
* SITES-20927：当查询缺失时，搜索 API 将返回 500。
* SITES-20544：[Open API] 更改发布包名称的生成以避免 oak 冲突。
* SITES-19710：CVE-2022-47937 - 从页面编辑器中删除 org.apache.sling.commons.json 的所有用法。
* SITES-11992：[辅助功能] 注释样本选择器按钮缺少可访问的名称。
* SITES-10979：[辅助功能] 标签不是持久的。
* SITES-10962：[辅助功能] 按钮：按钮没有作用。
* SITES-10905：[辅助功能] 活动组件的状态缺少 3 比 1 的对比度。
* SITES-2974：[辅助功能]，水平滚动宽度为 320px。
* SITES-22026：无法在 AEM 中的文件夹之间移动体验片段
* SITES-22106：新内容片段编辑器中的语言切换功能问题
* SITES-21980：基于 UUID 的参考类型的处理不一致。
* SITES-7257：ThumbnailServlet 中存在 NPE。

### 已知问题 {#known-issues-16971}

无。

### 更改通知 {#change-notice-16971}

* 从 2024 年 9 月开始，AEM as a Cloud Service 将会通过 Sling Model Exporter 框架禁用资源解析器的序列化。请参阅[该文档](/help/implementing/developing/hybrid/disallow-the-serialization-of-resourceresolvers-via-sling-model-exporter.md)了解更多详情。

### 已弃用的功能和 API {#deprecated-16971}

若要了解 AEM as a Cloud Service 中已弃用或移除的功能，请参阅[已弃用和已移除的功能和 API。](/help/release-notes/deprecated-removed-features.md)

### 嵌套的技术 {#embedded-tech-16971}

| 技术 | 版本 | 链接 |
|---|---|---|
| AEM Oak | 1.64.0 | [Oak API 1.64.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.64.0/index.html) |
| AEM SLING API | 2.27.2 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.22-1.4.0 | [HTML 模板语言规范](https://github.com/adobe/htl-spec) |
| AEM 核心组件 | 2.25.4 | [AEM WCM 核心组件](https://github.com/adobe/aem-core-wcm-components) |
