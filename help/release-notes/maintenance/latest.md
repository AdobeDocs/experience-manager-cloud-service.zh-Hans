---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 67b9a5f73f1f8c599e902a0ac0d8efbc614c7f75
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 32%

---


# 维护发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

## 版本X {#X}

以下总结了维护版本X的持续改进，该版本于2025年4月1日公开发布。 上一个维护版本是版本 19823。

激活 2025.4.0 功能后会为此维护版本提供全套功能。有关更多信息，请参阅[ Experience Manager 发布路线图](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增强功能 {#enhancements-X}

Forms-19068：在AEP Manager API中添加了对Forms Connector提交操作的支持，以增强表单数据集成功能。

Forms-18513：在AEP Connector中实施数据树转换支持，以增强向导功能和数据处理功能。

Forms-18432：实施特定于表单（基于正则表达式）的客户端预填充配置，以便在没有OSGI级别更改的情况下启用选择性预填充功能。

Forms-17551：添加了对SharePoint列表集成的记录文档(DoR)支持。

### 修复的问题 {#fixed-issues-X}

Forms-19028：客户端预填充功能中断了表单事件处理，导致值提交和DOMContentLoaded事件在表单加载时无法正确触发。

Forms-18360：在SharePoint文档管理中增强了团队网站的Forms列表范围管理，以改进数据组织和访问控制。

Forms-18325：添加了Adobe Experience Platform (AEP)云配置，以增强表单数据集成和处理功能。

Forms-18213：实施了从记录文档(DoR)隐藏/排除已禁用字段的功能，以提高文档清晰度和用户体验。

Forms-18189：修改了自定义函数处理，以防止为空客户端库记录错误，并改进UI中的错误显示。

Forms-18426：当列表名称包含特殊字符（例如，“ — ”）时，SharePoint列表查找功能失败，这会影响表单与SharePoint列表的集成。

Forms-18375：如果未选择特定的配置容器，则基于基础组件的表单从`conf/global`文件夹中错误地选择recaptcha配置。

Forms-18304：由于设备相关的颜色错误，在Acrobat和LiveCycle ES4中通过验证的PDF/A-1b文档在AEM 6.5 Forms中被错误地标记为不合规的。

Forms-18271： Forms主题编辑器显示未本地化的错误消息，影响表单配置和主题自定义中的用户体验。

Forms-18068：单选按钮和复选框组使用富文本字段的记录文档(DoR)中存在粗体文本渲染问题。

Forms-7016：表单编辑器中的键盘焦点顺序不遵循逻辑导航。

Forms-6950：向文件系统navigator treeview组件添加了所需的ARIA角色和属性，以提高屏幕阅读器可访问性，并符合WCAG 4.1.2名称、角色、值（级别A）标准。

### 已知问题 {#known-issues-X}

无。

### 已弃用的功能和 API {#deprecated-X}

AEM as a Cloud Service 中已弃用和删除的功能和 API 在[已弃用和删除的功能和 API](/help/release-notes/deprecated-removed-features.md) 文档中有详细说明。

### 安全修复 {#security-X}

AEM as a Cloud Service 致力于优化您平台的安全性和性能。此维护版本解决了X发现的漏洞，强化了我们对强大系统保护的承诺。

### 嵌套的技术 {#embedded-tech-X}

| 技术 | 版本 | 链接 |
|---|---|---|
| AEM Oak | 1.76.0 | [Oak API 1.76.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.76.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.26-1.4.0 | [HTML 模板语言规范](https://github.com/adobe/htl-spec) |
| AEM 核心组件 | 2.27.0 | [AEM WCM 核心组件](https://github.com/adobe/aem-core-wcm-components) |
