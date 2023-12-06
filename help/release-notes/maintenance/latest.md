---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 2677e8fbdf6b21ce2d1d848000401c826bc5f289
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 37%

---

# 维护发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

## 版本 14538 {#release-14538}

以下总结了于2023年12月6日公开发布的维护版本14538的持续改进。 此维护版本是对上一个维护版本 14227 的更新。

2023.12.0 功能激活将为此维护版本提供全套功能。有关更多信息，请参阅[ Experience Manager 发布路线图](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html)。

### 增强 {#enhancements-14538}

* GRANITE-46723：用户同步 — SAML从默认同步迁移到基于IDP的同步。
* OAK-10311：复制 — 优化Blob比较，以缩短AEM中大量资产的复制时间。
* OAK-10511：复制 — 减少网络往返次数，以缩短AEM中大型资源的复制时间。
* GRANITE-48334：发布者 — RUM缺少收藏集脚本。

### 修复的问题 {#fixed-issues-14538}

* CQ-4354867： ToggleCondition引用了InstanceActionServlet中不存在的字段。
* CQ-4349948：对工具→安全→用户下的编辑用户设置中的“配置文件属性”字符串进行本地化。
* GRANITE-44541：错误对话框的本地化：在“工具”→“安全→用户”下的“编辑用户”>“密钥库”屏幕中，添加私钥文件时出现。
* GRANITE-45341：在“工具”→“安全性”→“用户”下，本地化激活/取消激活用户操作的成功/失败字符串。
* GRANITE-46650：本地化错误消息“UserId/Password不匹配”。 “工具→安全→用户创建”对话框下的字符串。
* GRANITE-47764：更新到Sling模型API 1.5.0：注入到Sling模型中的静态变量将导致编译错误(SLING-11507)。
* GRANITE-48452：发送状态代码为200的空clientlibs。
* GRANITE-48410： ResourceResolver未关闭。
* ASSETS-31297：阻止从Dynamic Media中删除复制的资产。
* ASSETS-30811：引用Blocktag Service绑定的更新。
* GRANITE-46418：更新AEM中的Sling事件： GaugeSupport在registerWithSuffix中具有无限递归(SLING-11918)。

### 已知问题 {#known-issues-14538}

无。

### 嵌套的技术 {#embedded-tech-14538}

| 技术 | 版本 | 链接 |
|---|---|---|
| AEM OAK | 1.58-T20231123092841-619e1bd | [Oak API 1.58.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.58.0/index.html) |
| AEM SLING API | 2.27.2 版 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 版本 1.4.20-1.4.0 | [HTML 模板语言规范](https://github.com/adobe/htl-spec) |
| AEM 核心组件 | 2.23.4 版 | [AEM WCM 核心组件](https://github.com/adobe/aem-core-wcm-components) |
