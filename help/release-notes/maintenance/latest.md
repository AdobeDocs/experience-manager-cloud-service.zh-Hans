---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 1a1eeb3b9aec839677baadf9bea67993a22f9519
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 43%

---


# 维护发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

## 发行版本 22943 {#22943}

以下总结了维护版本22943的持续改进，该版本于2025年10月14日公开发布。 上一个维护版本是版本 22758。

激活 2025.10.0 功能后会为此维护版本提供全套功能。有关更多信息，请参阅[&#x200B; Experience Manager 发布路线图](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增强功能 {#enhancements-22943}

* Assets-57809：damAssetLucene-13的索引定义更新。
* Assets-36521：改进了DM重新上传工作流程，以确保一致的后处理。
* Assets-56400：为具有透明度的资源添加了新的OOTB缩放PNG演绎版。
* Assets-55326：通过HTTP事件启用AI元数据文件夹配置视图。
* Assets-56905：支持通过代理连接到Indesign。
* Assets-48286：将CAI资产添加到GenStudio的Algolia。
* Assets-48653：在预处理阶段应用不可见水印。
* Assets-55874：将图像预设从scene7迁移到DMWithOpenapi。
* SITES-30452：对/content/definition端点上ASO的内容API进行了改进。

### 修复的问题 {#fixed-issues-22943}

* Assets-56301：修复了选择性元数据导出以在CSV中包含预测标记。
* Assets-55543：将异步处理逻辑重构为可重用的捆绑包。
* Assets-54789：在启用DM ACL时，修复了ACLPermissionsValidator中的NPE。
* Assets-55888：修复了出现在UI呈现面板中的恶意软件呈现版本。
* GRANITE-62236：修复了智能收藏集的保存搜索中的关键词本地化问题。
* GRANITE-61875：修复了阻止保存内容片段和资产下载的“表达式评估无效”修补程序问题。
* SITES-24074：修复了在键盘选项卡导航期间接收焦点的隐藏移动导航。
* SITES-33611：修复了大流量市场的Live Copy概述问题。

#### AEM Guides {#guides-22943}

* GUIDES-31421：当打开多个DITA映射或主题并且其中一个主题关闭时，显示所有打开的选项卡的&#x200B;**>>**&#x200B;按钮与选项卡栏上其余打开的选项卡重叠。
* GUIDES-33229：在生成PDF时，如果任何属性名称包含句点，则会忽略DITAVAL文件中的筛选规则。
* GUIDES-33720：在翻译UI屏幕中缩放时，发送以供翻译按钮移动到省略号下方，并且变为启用状态，即使未选择任何资产也是如此。
* GUIDES-33590：当审阅人完成审阅任务或发起人更新审阅任务而未输入注释时，发送的通知电子邮件将显示最近的上一注释。

如需了解有关新版本中新增功能、增强功能和已修复问题的更多信息，请查看 [Experience Manager Guides 发布路线图](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap)。

### 已弃用的功能和 API {#deprecated-22943}

AEM as a Cloud Service 中已弃用和删除的功能和 API 在[已弃用和删除的功能和 API](/help/release-notes/deprecated-removed-features.md) 文档中有详细说明。

### 安全修复 {#security-22943}

AEM as a Cloud Service 致力于优化您平台的安全性和性能。此维护版本解决了 14 个已发现的漏洞，增强了我们对实现强大系统保护的承诺。

### 更改通知

* 此版本包含以下新的产品索引版本：
* **damAssetLucene-13**

### 嵌入的技术 {#embedded-tech-22943}

| 技术 | 版本 | 链接 |
|---|---|---|
| AEM Oak | 1.86.0 | [Oak 1.86.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.86/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [HTML 模板语言规范](https://github.com/adobe/htl-spec) |
| Apache HTTP 服务器 | 2.4.65 | [Apache Httpd 2.4.65](https://apache.googlesource.com/httpd/+/refs/tags/2.4.65/CHANGES) |
| AEM 核心组件 | 2.30.2 | [AEM WCM 核心组件](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14（默认） | [受支持的 Node.js 版本](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |
