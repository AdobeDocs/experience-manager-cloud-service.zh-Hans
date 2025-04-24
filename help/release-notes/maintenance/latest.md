---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: c5152543550b5f81bf0b79741f288b0c16648584
workflow-type: ht
source-wordcount: '452'
ht-degree: 100%

---


# 维护发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

## 版本 20476 {#20476}

下面总结了维护版本 20476 的持续改进，该版本已于 2025 年 4 月 15 日公开发布。上一个维护版本是版本 20133。

激活 2025.4.0 功能后会为此维护版本提供全套功能。有关更多信息，请参阅[ Experience Manager 发布路线图](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增强功能 {#enhancements-20476}

* CNTBF-411：增加删除吊索作业的可能性，以防 JCR 丢弃。
* CQ-4359813：AEM 翻译套件：3 月 20 日。
* CQ-4359811：花岗岩翻译套件：3 月 20 日。
* GRANITE-57863：将 Filevault 更新到 3.8.4。
* GRANITE-56154：在 oak-segment-azure 中配置指数重试。
* GRANITE-55999：提高 UserPropertiesService 的性能。
* GRANITE-55781：避免对用户成员资格进行冗余重新配置。
* GRANITE-53956：将 oak-segment-azure 的 Azure SDK V8 升级到 V12。
* GRANITE-50654：在主体权限选项卡上，删除前端默认的“所有人”负载。
* SKYOPS-103444：更新至 Sling ResourceResolver 1.12.6。
* SKYOPS-101147：更新 caconfig 实现。
* SKYOPS-97124：为 SPIFly 捆绑包的过时版本添加分析器警告。
* SKYOPS-95826：将运行时 Java 版本更新至 11.0.26 和 21.0.6。
* SKYOPS-53671：在 (RDE) AEM 重新启动时使用来自功能模型的客户安装的工件。

### 修复的问题 {#fixed-issues-20476}

* ASSETS-49027：[回归] AemRequestEventFilter 中断了对 OSGI 网页控制台的 POST 请求。
* ASSETS-44956：无法选择任何动态媒体演绎版 - 脚本标签应加载到顶级组件中。
* CNTBF-410：ContentCopy 捆绑包中的 CheckJob getId 空指针。
* CNTBF-341：ContentCopy 导出索引超出范围。
* CQ-4355411：工具提示仍然显示在“用户首选项”对话框中。
* GRANITE-57265：下拉选择值未被选中。
* GRANITE-57067 - UI 上缺少有效策略。
* SITES-30727：AEM 编辑器中的子组件拖放操作可能会失败。
* SKYOPS-90607：Sling Jobs 在非活动部署/可变内容中执行。
* SKYOPS-95722：从 AEM-SDK 中的快速启动标志中移除 `MaxPermSize` 的大小。
* SKYOPS-103569：某些图像无法使用 Java 21：`javax.imageio.IIOException: Cannot create Sun JPEGImageReader backend`加载。

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
