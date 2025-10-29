---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 9d081b468e42306c56238bee6117d92c6afd48d4
workflow-type: tm+mt
source-wordcount: '863'
ht-degree: 23%

---


# 维护发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

## 发行版本 23122 {#23122}

以下总结了维护版本23122的不断改进，该版本于2025年10月29日公开发布。 上一个维护版本是版本 22943。

激活 2025.11.0 功能后会为此维护版本提供全套功能。有关更多信息，请参阅[&#x200B; Experience Manager 发布路线图](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增强功能 {#enhancements-23122}

* Forms-21594：为内容作者启用交互式通信模板内容和布局锁定功能。
* Forms-20385：支持在交互式通信编辑器中进行XDP编辑。
* Forms-10883：支持在DoR生成中使用XHTML命名空间标记的JSON，以确保准确呈现通过API提交的富文本数据。
* Forms-21751：画布功能 — 文本溢出，用于分页的UI。
* Forms-22049：交互式通信编辑器 — 迁移到频谱2。
* Forms-22050：支持交互式通信编辑器中的动态页码。
* Forms-21606：用于交互式通信的公共OSGi渲染SPI。
* Forms-21613：渲染交互式通信SPI的事务报告和性能日志记录。
* SITES-35092：内容片段 — 用于语义搜索的新mixin和升级过程。
* SITES-32319：投放OpenAPI — 支持页面引用。
* SITES-20123： GraphQL：支持JSON响应中的上标元素。
* SITES-34744：内容片段响应中新增的“卡片”属性，该属性包含可用于呈现缩略图的数据。
* SITES-34571：允许枚举字段为空。
* SITES-34812：使用值为“none”的“references”参数，新增了在没有引用的情况下检索内容片段的功能。
* SITES-35176：现在，通过触屏UI签出内容片段会阻止其他用户在新编辑器中编辑内容片段。
* SITES-30371：增加了对基于uuid的引用字段的支持。
* SITES-19309：在打开移动页面向导时，最多检索150个引用。
* SITES-32515：带有通用编辑器的Edge Delivery — 添加对多字段和复合多字段的支持（提前访问）。
* SITES-33784：带有通用编辑器的Edge Delivery — 在页面元数据中添加对ld-json的支持。
* SITES-34832：带有通用编辑器的Edge Delivery — 将页面的公共路径添加到页面信息servlet响应。
* SITES-25893：带有通用编辑器的Edge Delivery — 添加对强功能的支持，并强调以块形式呈现文本。
* SITES-26158：带有通用编辑器的Edge Delivery — 添加对块和列中的表标记的支持（抢先访问）。
* SITES-27949：带有通用编辑器的Edge Delivery — 将路径映射设为可选。

### 修复的问题 {#fixed-issues-23122}

* CQ-4361144：修复了从翻译作业中跳过内容片段的问题。
* CQ-4355446：修复了取消翻译作业对话框上翻译项目中未本地化的字符串。
* SITES-34555： GraphQL — 部署后出现QueryValidationError。
* SITES-35077：内容片段 — 由于URL编码不正确，对带有圆括号的片段取消发布失败。
* SITES-35374：内容片段 — 编辑的内容片段在导航回之后消失。
* SITES-36130： `EditorRestrictionsStatusImpl`中的NPE。
* SITES-35810： Launches中的NullPointerException块publishEdgeDeliverySubscriber队列。
* SITES-34368： AEM CIF生成12个GraphQL别名 — 超过Magento 2.4.6-P12中10个别名限制。
* SITES-36193：CCS连接器修复。
* SITES-35169：解决了当搜索返回无效片段资源时，会导致分页错误的问题。
* SITES-34574：修复了在某些情况下内容片段搜索API不会返回游标的问题。
* SITES-35520：修复了在尝试发布内容时导致ClassCastException或超时的问题。
* SITES-35210：修复了在尝试发布具有空引用过滤器的损坏片段时可能出现的NullPointerException。
* SITES-35933：修复了在发布内容片段后导致触发空“请求激活”工作流的错误。
* SITES-35925：修复了与修补内容片段模型相关的错误，该错误会导致从模型中删除“可翻译”和“showThumbnail”属性。
* SITES-35409：修复了在移动页面时阻止重新发布已调整片段的错误。
* SITES-15757：修复了在移动页面时阻止重新发布已调整页面的错误。
* SITES-34638：修复了在创建新版本时不会包含父级页面中的属性的错误。
* SITES-35071：当omnisearch使用带引号的短语时，CSV导出会返回未过滤的结果。
* SITES-32182：使用通用编辑器的Edge Delivery — 修复包含已编码请求参数的URL的编码问题。
* SITES-34324：带有通用编辑器的Edge Delivery — 修复了使用tel：协议呈现链接的问题。
* SITES-35333：使用通用编辑器的Edge Delivery — 修复页面元数据中图像的资源演绎版选择。
* SITES-35549：使用通用编辑器的Edge Delivery — 修复页面元数据中双重编码的html实体。

### 已知问题 {#known-issues-23122}

无。

### 已弃用的功能和 API {#deprecated-23122}

AEM as a Cloud Service 中已弃用和删除的功能和 API 在[已弃用和删除的功能和 API](/help/release-notes/deprecated-removed-features.md) 文档中有详细说明。

### 安全修复 {#security-23122}

AEM as a Cloud Service 致力于优化您平台的安全性和性能。此维护版本解决了 18 个已发现的漏洞，增强了我们对实现强大系统保护的承诺。

### 嵌入的技术 {#embedded-tech-23122}

| 技术 | 版本 | 链接 |
|---|---|---|
| AEM Oak | 1.86.0 | [Oak 1.86.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.86/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [HTML 模板语言规范](https://github.com/adobe/htl-spec) |
| Apache HTTP 服务器 | 2.4.65 | [Apache Httpd 2.4.65](https://apache.googlesource.com/httpd/+/refs/tags/2.4.65/CHANGES) |
| AEM 核心组件 | 2.30.2 | [AEM WCM 核心组件](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14（默认） | [受支持的 Node.js 版本](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |
