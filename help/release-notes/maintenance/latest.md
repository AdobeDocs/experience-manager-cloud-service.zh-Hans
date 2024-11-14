---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护版本发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护版本发行说明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 9a653fbe13b29fa60af7410fff178cbac6ca554d
workflow-type: tm+mt
source-wordcount: '842'
ht-degree: 73%

---


# 维护版本发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

## 版本 18598 {#18598}

以下总结了维护版本18598的不断改进，该版本于2024年11月13日公开发布。 上一个维护版本是版本 18311。由于存在问题，版本 18459 已被设为专有。

激活 2024.11.0 功能后会为此维护版本提供全套功能。有关更多信息，请参阅[ Experience Manager 发布路线图](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增强 {#enhancements-18598}

* CQ-4357471：在 AEMaaCS 中添加对 i18n 词典翻译的支持。
* Forms-11646：为AEM Forms相关页面设置globalContext变量。
* Forms-14833：AEM Forms现在能够在最终记录文档(DoR)中包含自适应表单片段。
* Forms-14255：用户现在可以从自动保存功能中受益，该功能会自动将部分完成的表单另存为草稿。 他们可以稍后返回，在同一台或其他设备上完成填写。
* SITES-23591：内容片段：内容片段升级以支持 UUID。
* SITES-25440：内容片段：CFM 搜索 API 以显示复制状态。
* SITES-24369：内容片段：OpenAPI 文档改进。
* SITES-25478：内容片段：添加对外部资产引用的后端支持。
* SITES-26119：内容片段：在引用类型中添加对外部资产引用的支持。
* SITES-21199：带有通用编辑器的 Edge Delivery：添加对从页面创建的模板的支持。
* SITES-20311：带有通用编辑器的 Edge Delivery：添加将 CSV 导入电子表格的支持。
* SITES-24821：带有通用编辑器的 Edge Delivery：将 aem.page / aem.live 设为与 Edge Delivery 集成的默认设置。

### 修复的问题 {#fixed-issues-18598}

* CQ-4358730：当超过 10 个键需要翻译时，CQPagePreviewGenerator 将显示失败。
* CQ-4358028：当仅具有project-administrators组的用户在项目创建页面上上传新缩略图时，AEM项目创建失败。
* FORMS-14978：为主题编辑器基于核心组件的表单启用页面加载。
* Forms-15682：该问题涉及AEM Forms和Dynamics FDM集成。 当用户提交表单时，记录文档(DOR)未作为PDF附件发送到指定的实体字段。
* Forms-15799： Adobe Sign GovCloud签名页面不会在iframe中渲染注释。
* Forms-16113：当作为Adobe Sign帐户管理员的用户尝试访问由其他用户（也是管理员）发送的文档时，获取协议API可能会返回与创建协议时最初生成的协议ID不同的协议ID。
* FORMS-16596：可访问性问题：屏幕阅读器无法识别禁用按钮。
* GRANITE-53907：无法将服务用户标识为工作流超级用户。
* SKYOPS-90560：最新Sling模型版本影响Sling模型导出的性能。
* SITES-10575：MSM：Blueprint Bloomfilter Loader 尝试加载 >100,000 行。
* SITES-20755：内容片段：刷新 UUID 的资产引用不显示缩略图。
* SITES-26253：内容片段：UUID 迁移：将 sling 作业主题更改为通用。
* SITES-21338：内容片段：referencedBy 端点没有返回正确的页面引用。
* SITES-24421：内容片段：编辑 CF 端点对通过 GET CF 检索的 CF 无效。
* SITES-25461：内容片段：按模型筛选搜索 CF 时应不区分大小写。
* SITES-25471：内容片段：修复 ModelValidatorServlet 中全局模型的验证。
* SITES-25795：内容片段：当未设置 cq 日期时，CF 模型 API 将显示失败。
* SITES-25817：内容片段：增强 promoteLaunch：更新 CF Launches 的最后一次促销。
* SITES-26030：内容片段：端点 /referencesTree 没有返回所需的标头。
* SITES-26031：内容片段：CFM 搜索端点未返回复制状态。
* SITES-26213：内容片段：取消发布的内容片段应该仅验证已发布的引用。
* SITES-26226：内容片段：当给定的路径均不可用时，启动工作流问题。
* SITES-26238：内容片段：API 返回的资产引用顺序与 JCR 的顺序不同。
* SITES-25456：事件：移动页面时，除了页面移动事件之外，还会生成页面删除事件。
* SITES-25658：事件：页面内容状态事件中未填充层和 sourceUrl。
* SITES-6497：启动：启动时创建页面不起作用。
* SITES-25938：启动：意外删除翻译帖子项目。
* SITES-25393：带有通用编辑器的 Edge Delivery：渲染带有单个段落的格式化富文本时文本节点丢失。
* SITES-24643：带有通用编辑器的 Edge Delivery：OpenGraph 和 Twitter 元数据属性在页面元数据模型中不起作用。
* SITES-25401：体验片段：XF引用更新缓慢。

### 已知问题 {#known-issues-18598}

无。

### 已弃用的功能和 API {#deprecated-18598}

AEM as a Cloud Service 中已弃用和删除的功能和 API 在 [已弃用和删除的功能和 API](/help/release-notes/deprecated-removed-features.md) 文档中有详细说明。

### 安全修复 {#security-18598}

AEM as a Cloud Service 致力于优化您平台的安全性和性能。此维护版本解决了 21 个已发现的漏洞，增强了我们对强大系统保护的承诺。

### 嵌套的技术 {#embedded-tech-18598}

| 技术 | 版本 | 链接 |
|---|---|---|
| AEM Oak | 1.70.0 | [Oak API 1.70.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.70.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.24-1.4.0 | [HTML 模板语言规范](https://github.com/adobe/htl-spec) |
| AEM 核心组件 | 2.27.0 | [AEM WCM 核心组件](https://github.com/adobe/aem-core-wcm-components) |
