---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: c5152543550b5f81bf0b79741f288b0c16648584
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 46%

---


# 维护发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

## 版本 20476 {#20476}

以下总结了维护版本20476的持续改进，该版本于2025年4月15日公开发布。 上一个维护版本是版本 20133。

激活 2025.4.0 功能后会为此维护版本提供全套功能。有关更多信息，请参阅[ Experience Manager 发布路线图](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增强功能 {#enhancements-20476}

* CNTBF-411：添加删除sling作业的可能性，以防JCR丢弃。
* CQ-4359813：AEM翻译包：3月20日。
* CQ-4359811：Granite翻译包：3月20日。
* GRANITE-57863：将 Filevault 更新到 3.8.4。
* GRANITE-56154：在oak-segment-azure中配置指数重试。
* GRANITE-55999：提高UserPropertiesService的性能。
* GRANITE-55781：避免对用户成员资格进行冗余重新配置。
* GRANITE-53956：将Azure SDK V8升级到V12，以便使用oak-segment-azure。
* GRANITE-50654：在“主体权限”选项卡上，默认删除前端上的“所有人”加载。
* SKYOPS-103444：更新至 Sling ResourceResolver 1.12.6。
* SKYOPS-101147：更新caconfig实施。
* SKYOPS-97124：为SPIFly捆绑包的过时版本添加分析器警告。
* SKYOPS-95826：将运行时Java版本更新为11.0.26和21.0.6。
* SKYOPS-53671：在(RDE) AEM重新启动时，使用功能模型中的客户安装的工件。

### 修复的问题 {#fixed-issues-20476}

* Assets-49027： [回归] AemRequestEventFilter中断对OSGI Web控制台的POST请求。
* Assets-44956：无法选择任何Dynamic Media呈现版本 — 脚本标记应加载到顶级组件中。
* CNTBF-410： ContentCopy包中的CheckJob getId空指针。
* CNTBF-341： ContentCopy导出索引超出边界。
* CQ-4355411：工具提示仍显示在“用户首选项”对话框中。
* GRANITE-57265：未选择下拉列表选择值。
* GRANITE-57067 - UI上缺少有效策略。
* SITES-30727：AEM 编辑器中的子组件拖放操作可能会失败。
* SKYOPS-90607：在非活动部署/可变内容中执行Sling作业。
* SKYOPS-95722：从AEM-SDK中的快速入门标记中删除`MaxPermSize`大小。
* SKYOPS-103569：某些图像不能使用Java 21加载： `javax.imageio.IIOException: Cannot create Sun JPEGImageReader backend`。

### 已知问题 {#known-issues-20476}

无。

### 已弃用的功能和 API {#deprecated-20476}

AEM as a Cloud Service 中已弃用和删除的功能和 API 在[已弃用和删除的功能和 API](/help/release-notes/deprecated-removed-features.md) 文档中有详细说明。

### 安全修复 {#security-20476}

AEM as a Cloud Service 致力于优化您平台的安全性和性能。此维护版本解决了 5 个已发现的漏洞，增强了我们对实现强大系统保护的承诺。

### 嵌套的技术 {#embedded-tech-20476}

| 技术 | 版本 | 链接 |
|---|---|---|
| AEM Oak | 1.78.0 | [Oak API 1.78.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.78.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.26-1.4.0 | [HTML 模板语言规范](https://github.com/adobe/htl-spec) |
| AEM 核心组件 | 2.28.0 | [AEM WCM 核心组件](https://github.com/adobe/aem-core-wcm-components) |
