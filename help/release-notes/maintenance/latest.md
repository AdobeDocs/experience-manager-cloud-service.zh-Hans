---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 22ed74b307b9eb4c6c2f72ac2a34e2ab6d30a85c
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 50%

---

# 维护发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

## 发行版本 13239 {#release-13239}

下面总结了维护版本 13239 的持续改进，该版本已于 2023 年 8 月 29 日公开发布。此维护版本取代了发行说13206。

激活 2023.9.0 功能后可为此次维护版本提供完整的功能集。有关更多信息，请参阅[ Experience Manager 发布路线图](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html)。

### 增强 {#enhancements-13239}

- GRANITE-46784：添加用于禁用BearerAuthenticationHandler的选项
- GRANITE-36205：将内部Oak发行版本更新到最新版本
- GRANITE-47059：删除Granite Jetty SSL包
- ASSETS-26713：触屏UI外部链接到新的Experience UI功能板 — 已升级unified-shell集成和ui-touch-optimized
- SKYOPS-63302：将com.adobe.granite：com.adobe.granite.auth.saml升级到v1.0.54
- GRANITE-46634：升级到事件客户端1.4.0
- GRANITE-46788：更新Apache Commons库
- GRANITE-29211：将工具更新为Sling功能模型2.0
- GRANITE-46705：更新至Apache Felix Http Jetty 4.1.14
- GRANITE-46631：将Jackrabbit版本更新为2.20.11
- SKYOPS-61895：更新至Jackrabbit Filevault 3.7.0

### 修复的问题 {#fixed-issues-13239}

- SKYOPS-63290：修复了存储桶的不正确演化
- SKYOPS-54607：速率限制符服务器负载计算对失败的请求不正确
- ASSETS-27648： ContentModelIT无法从其他包中读取排除文件
- GRANITE-43744：如果身份验证要求和虚路径配置错误，则Sling Authenticator无法正常工作
- GRANITE-46419：AEM与Auth0 Idp的集成问题
- GRANITE-46292：AEM Cloud更新后，Okta SAML配置不起作用

### 已知问题 {#known-issues-13239}

无。

### 嵌套的技术 {#embedded-tech-13239}

| 技术 | 版本 | 链接 |
|---|---|---|
| AEM OAK | 1.54-T20230817132355-3800a65 | [Oak API 1.54.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.54.0/index.html) |
| AEM SLING API | 2.27.2 版 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 版本 1.4.20-1.4.0 | [HTML 模板语言规范](https://github.com/adobe/htl-spec) |
| AEM 核心组件 | 2.23.2 版 | [AEM WCM 核心组件](https://github.com/adobe/aem-core-wcm-components) |
