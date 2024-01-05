---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 4fc676bd975e44234b478ba57f12cbf0f4f5ba45
workflow-type: ht
source-wordcount: '371'
ht-degree: 100%

---

# 维护发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

## 版本 14697 {#release-14697}

下方总结了维护版本 14697（于 2023 年 12 月 18 日公开发布该版本）的持续改进。它取代了出现问题的 14538。上一个维护版本是版本 14227。

2023.12.0 功能激活提供此维护版本的全套功能。有关更多信息，请参阅[ Experience Manager 发布路线图](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html)。

### 增强 {#enhancements-14697}

* GRANITE-46723：用户同步 - SAML 从默认同步迁移到基于 IDP 的同步。
* OAK-10311：复制 - 优化 blob 比较以减少 AEM 中大批量资产的复制时间。
* OAK-10511：复制 - 减少网络往返次数以减少 AEM 中大型资产的复制时间。
* GRANITE-48334：发布者 - RUM 缺少收藏集脚本。

### 修复的问题 {#fixed-issues-14697}

* CQ-4354867：ToggleCondition 引用在 InstanceActionServlet 中指代不存在的字段。
* CQ-4349948：“工具”→“安全”→“用户”下的“编辑用户设置”中“配置文件属性”字符串的本地化。
* GRANITE-44541：“工具”→“安全”→“用户”下的“编辑用户”>“密钥库”的添加“私钥文件”屏幕上的错误对话框的本地化。
* GRANITE-45341：在“工具”→“安全”→“用户”下激活/停用用户操作的成功/失败字符串的本地化。
* GRANITE-46650：错误消息“用户 ID/密码不匹配”的本地化。“工具”→“安全”→“用户创建对话框”下的字符串。
* GRANITE-47764：对 Sling 模型的更新 API 1.5.0：注入 Sling 模型中的静态变量会导致编译错误 (SLING-11507)。
* GRANITE-48452：发送状态代码为 200 的空 clientlib。
* GRANITE-48410：ResourceResolver 未关闭。
* ASSETS-31297：防止从 Dynamic Media 中删除复制的资源。
* ASSETS-30811：Blocktag 服务绑定的参考更新。
* GRANITE-46418：更新 AEM 中的 Sling 事件：GaugeSupport 在 registerWithSuffix 中具有无限递归 (SLING-11918)。
* GRANITE-48937：修复了维护版本 14538 中 Omnisearch 在 aem/start.html 页面上不起作用的回归问题。

### 已知问题 {#known-issues-14697}

无。

### 嵌套的技术 {#embedded-tech-14697}

| 技术 | 版本 | 链接 |
|---|---|---|
| AEM OAK | 1.58-T20231123092841-619e1bd | [Oak API 1.58.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.58.0/index.html) |
| AEM SLING API | 2.27.2 版 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 版本 1.4.20-1.4.0 | [HTML 模板语言规范](https://github.com/adobe/htl-spec) |
| AEM 核心组件 | 2.23.4 版 | [AEM WCM 核心组件](https://github.com/adobe/aem-core-wcm-components) |
