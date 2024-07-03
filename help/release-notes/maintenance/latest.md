---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 9303ecadea38d83bd71ed0d440067bae5c419940
workflow-type: tm+mt
source-wordcount: '944'
ht-degree: 19%

---

# 维护发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

## 版本 16971 {#release-16971}

以下总结了维护版本16971的不断改进，该版本于2024年7月3日公开发布。 上一个维护版本是版本 16799。

2024.7.0 功能激活将会为此维护版本提供全套功能。有关更多信息，请参阅[ Experience Manager 发布路线图](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增强 {#enhancements-16971}

* SITES-22948：删除AEM CS的基础内容中的商业引用。
* SITES-22141： [内容片段] OnRC之后CFM ModelChangeRepositoryImpl中的SegmentNotFoundException。
* SITES-21893：创作实例上的图像裁切问题。
* SITES-21788： [内容片段] 为模型启用uiSchema时，在CF和CF模型编辑器中显示NOTE。
* SITES-21688： MSM转出不会更新Live Copy页面上的体验片段(XF)路径。
* SITES-21659：返回创建/修改/复制模型资源的用户的全名。
* SITES-21609：用于将内容片段从一个模型迁移到另一个模型的OpenAPI端点。
* SITES-21598： [打开API] 创建CFM — 如果给定的配置路径不存在，则返回错误。
* SITES-21491： [打开API] CFPATCH端点应遵循字段级别的实时关系。
* SITES-21434： [打开API] CFGET端点应遵循字段级别的实时关系。
* SITES-21415：CF编辑器 — 支持UUID引用。
* SITES-21326： [打开API] 提供有关存在对内容片段的引用的信息。
* SITES-21310： [打开API] 在翻译API响应中添加内容片段的ID。
* SITES-20859： CF打开API — 按路径检索片段时返回引用。
* SITES-20687： [打开API] 用于批处理状态检索的端点。
* SITES-20657： [打开API] 使用以下方式替换字符串时，为match提供全字选项 `FindAndReplace` 端点。
* SITES-20587： [打开API] 创建 `COPY` 内容片段的端点。
* SITES-20584： [打开API] 优化引用检索。
* SITES-20308： [打开API] 在API上启用批量处理。
* SITES-19976： [打开API] 条件字段的通用UI架构。
* SITES-19556： [内容片段] 如果编辑模型时存在uiSchema，则更新它。
* SITES-18056： [打开API] 将内容片段发布到预览时，包括引用。
* SITES-16898： [架构] 用于将内容片段从一个模型迁移到另一个模型的OpenAPI端点。
* SITES-16609：列出启动项端点。
* SITES-16606：创建启动项端点。
* SITES-21617： [Xwalk] 使页面属性/元数据在UE中可编辑。
* SITES-19614： [Xwalk] 电子表格编辑器分页和无限滚动。
* SITES-22163： [Xwalk] 改进了对从Edge Delivery Sites的发布层提供的内容的支持。
* SITES-22109： [Xwalk] 改进了富文本标记后处理的处理。
* SITES-22035： [Xwalk] 改进了MSM和启动项的处理。
* SITES-21839： [Xwalk] 改进了Edge Delivery不提供服务的内容的路径映射和清理。

### 修复的问题 {#fixed-issues-16971}

* CQ-4356898： [翻译] 包含异常多的链接的CF出现outOfMemory错误。
* CQ-4357055： [翻译] 使用Rest API时，自动翻译不起作用。
* CQ-4353931： [翻译] 在翻译源页面/xf/asset（如果缺少）中添加jcr：uuid。
* CQ-4357591： [翻译] 修改“关联JCR：UUID”工作流以适用于页面/XF。
* Forms-14844：尽管失败reCAPTCHA验证，自适应Forms仍允许提交表单。
* Forms-14984：如果提交的数据中不存在“submitMetaData”，则带CAPTCHA的Forms将跳过验证。
* Forms-14477：规则编辑器中的“Is After”和“Is Before”选项在日期选取器验证中无法正常工作。
* Forms-14019：规则编辑器的“调用服务”功能在通用编辑器中不起作用。
* Forms-14336：未选择表单字段时，编辑器应会打开，并重点关注整个表单元素。
* Forms-15061：在规则编辑器中使用调用服务选项时，加载器循环将无限期地持续存在。
* SITES-22457：提升非深层启动项不会更新源内容。
* SITES-22748： [内容片段] 增强内容片段更新作业的错误处理
* SITES-22349： [内容片段] 无法更改空的多行cf元素的ContentType。
* SITES-22343： [内容片段] 语义类型“明细列表”已损坏。
* SITES-22194：设置重定向后，model.json不再可用。
* SITES-21953： [打开API] Etag将根据validationStatus的顺序进行更改。
* SITES-21894： [打开API] 创建CF时增强父级路径验证。
* SITES-21887： [打开API] POST变体端点返回的ETag无效。
* SITES-21657： [打开API] 改进对CF搜索路径属性的验证。
* SITES-21949：搜索API的无效光标返回500。
* SITES-20927：当查询缺失时，搜索API返回500。
* SITES-20544： [打开API] 更改发布包名称的生成，以避免Oak冲突。
* SITES-19710： CVE-2022-47937 — 从页面编辑器中删除org.apache.sling.commons.json的所有用法。
* SITES-11992： [辅助功能] 注释样本选择器按钮缺少可访问的名称。
* SITES-10979： [辅助功能] 标签不是永久性的。
* SITES-10962： [辅助功能] 按钮：按钮没有角色。
* SITES-10905： [辅助功能] 活动组件的状态缺少3到1的对比度。
* SITES-2974：  [辅助功能]  — 宽度为320像素的水平滚动。
* sites-22026：无法在AEM中的文件夹之间移动体验片段
* SITES-22106：新内容片段编辑器中的语言切换功能问题
* SITES-21980：对基于UUID的引用类型的处理不一致。
* SITES-7257：ThumbnailServlet中出现NPE。

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
