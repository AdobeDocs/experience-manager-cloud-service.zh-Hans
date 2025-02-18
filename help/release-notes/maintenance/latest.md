---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 1d6a54f87d55179c11c7ccc7766eeeb475674f05
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 45%

---


# 维护发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

## 版本 19567 {#19567}

以下总结了维护版本19567的持续改进，该版本于2025年2月18日公开发布。 上一个维护版本是版本 19352。

激活 2025.2.0 功能后会为此维护版本提供全套功能。有关更多信息，请参阅[ Experience Manager 发布路线图](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增强功能 {#enhancements-19567}

* GRANITE-56650：内容分发应仅在重试几次后指示阻塞的队列
* SKYOPS-89616：允许在Adobe Developer Console中创建最多40个技术帐户

### 修复的问题 {#fixed-issues-19567}

* CNTBF-232：深层包nt：file节点，包含强制的jcr：content子级
* CQ-4358930：在加载具有多个字段的页面属性期间出现性能问题
* GRANITE-55960：AEM as Cloud Service上的Coral Select字段存在性能问题
* GRANITE-56197：新的TreeActivation工作流步骤不会批处理大型平面文件夹结构中的资产

#### AEM 指南 {#guides}

* GUIDES-23526：从文件夹配置文件更新条件时，所有条件组都将丢失，条件会扁平化。
* GUIDES-22574：如果外部链接包含UUID，则它会进行后期处理，并将外部链接转换为UUID链接，从而断开编辑器和发布站点上的链接。
* GUIDES-24983：从任何外部产品（例如，MS PowerPoint）复制图像并将其粘贴到Guides中时，动态上传资产以用于文件的功能会中断。
* GUIDES-21772：对于将&#x200B;**区块属性**&#x200B;设置为&#x200B;**to-content**&#x200B;的内容，本机PDF生成失败。
* GUIDES-23964：选择&#x200B;**编辑属性**&#x200B;时，基线对话框不显示以前保存的动态基线标准。
* GUIDES-19067：复制任何文件夹配置文件时，其管理员用户列表也会从原始文件夹配置文件中复制

如需了解有关新版本中新增功能、增强功能和已修复问题的更多信息，请查看 [Experience Manager Guides 发布路线图](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap)。

### 已知问题 {#known-issues-19567}

无。

### 已弃用的功能和 API {#deprecated-19567}

AEM as a Cloud Service 中已弃用和删除的功能和 API 在[已弃用和删除的功能和 API](/help/release-notes/deprecated-removed-features.md) 文档中有详细说明。

### 安全修复 {#security-19567}

AEM as a Cloud Service 致力于优化您平台的安全性和性能。此维护版本解决了 21 个已发现的漏洞，增强了我们对强大系统保护的承诺。

### 嵌套的技术 {#embedded-tech-19567}

| 技术 | 版本 | 链接 |
|---|--------------|-------------------------------------------------------------------------------------------------------------------|
| AEM Oak | 1.76.0 | [Oak API 1.76.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.76.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.26-1.4.0 | [HTML 模板语言规范](https://github.com/adobe/htl-spec) |
| AEM 核心组件 | 2.27.0 | [AEM WCM 核心组件](https://github.com/adobe/aem-core-wcm-components) |
