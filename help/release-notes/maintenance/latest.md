---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 3884f53d56a8fc5bb71b736dd0b1368906c05623
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 35%

---


# 维护发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

## 版本 21994 {#21994}

以下总结了维护版本21994的不断改进，该版本于2025年8月19日公开发布。 上一个维护版本是版本 21772。

激活 2025.8.0 功能后会为此维护版本提供全套功能。有关更多信息，请参阅 [Experience Manager 发布路线图](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 新增功能  {#new-features-21994}

无。

### 增强功能 {#enhancements-21994}

* GRANITE-53488：改进deleteconf.json端点错误处理。
* GRANITE-59968：允许配置REPLICATION_FORCE_READY_MILLIES。
* GRANITE-60183：Apache commons-fileupload 1.6.0。
* GRANITE-60306：Apache Commons-lang到3.18.0。
* GRANITE-60637：将Apache Commons-codec设置为1.19.0。
* GRANITE-60645：Apache commons-io 2.20.0。
* GRANITE-60663：Apache Commons-text 1.14.0。
* GRANITE-60714：Mongo Java驱动程序5.2。
* GRANITE-60778：Filevault 4.0.0。
* GRANITE-60823：Jackrabbit 2.22.2。
* GRANITE-60967：创建用于跟踪clientlib编译时间的量度。
* SKYOPS-105469：在autofix api中添加对acsredirectMgr的支持。
* SKYOPS-113929：为复制就绪检查添加量度。
* SKYOPS-84821：Sling引擎2.16.6。
* SKYOPS-114322：将关闭编译语言的级别提升到`ECMASCRIPT_2018`。

### 修复的问题 {#fixed-issues-21994}

* GRANITE-60167： Skyline中的异步索引更新不支持CSV数据。
* GRANITE-60532：不选取值切换的修改。
* SITES-34277：修复了页面的翻译工作流中的阻止错误。
* SKYOPS-105471：支持aso自动修复的dambaseredirect修复。
* SKYOPS-109532：在切换开关后添加功能已删除链接作为评论。

#### AEM Guides {#guides-21994}

* GUIDES-26688：本机PDF模板中的CSS和页面布局文件表现出不一致的文件锁定行为，即使文件被锁定也允许进行编辑。
* GUIDES-30900：从Assets UI复制具有大量资源的文件夹会导致API超时。 该操作将继续在后端运行并在一定时间后完成，但UI中未显示任何成功或失败消息或通知。
* GUIDES-29090：在本机PDF输出中，索引列表(LOI)以非字母顺序显示，并且嵌套的索引词未正确分组，导致索引难以导航。
* GUIDES-11227：从Assets UI复制DITA映射还会将其附加的基线复制到新映射。
* GUIDES-31506：当“最近使用的文件”小部件中列出的某个文件所基于的模板的源模板不包含缩略图时，主页变为空白。

如需了解有关新版本中新增功能、增强功能和已修复问题的更多信息，请查看 [Experience Manager Guides 发布路线图](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap)。

### 已知问题 {#known-issues-21994}

* 由于作为安全修复的一部分实施的新限制，Apache HTTPD版本2.4.65引入的更改可能会影响某些配置。 这些修复通过确保用于修改Content-Type标头的`RequestHeader set`、`edit`和`edit_r`等指令现在正确限制为请求标头来解决漏洞。 此更改可防止对响应标头（尤其是静态内容）进行意外修改。
* 在使用ProxyRemote连接时，Apache HTTPD版本2.4.65引入了mod_proxy中的更改。 如果您遇到问题，请将disablereuse标志设置为On。
  ```ProxyPass "/example" "http://backend.example.com" disablereuse=on```

### 已弃用的功能和 API {#deprecated-21994}

AEM as a Cloud Service 中已弃用和删除的功能和 API 在[已弃用和删除的功能和 API](/help/release-notes/deprecated-removed-features.md) 文档中有详细说明。

### 安全修复 {#security-21994}

AEM as a Cloud Service 致力于优化您平台的安全性和性能。此维护版本解决了 2 个已发现的漏洞，增强了我们对强大系统保护的承诺。

### 嵌入的技术 {#embedded-tech-21994}

| 技术 | 版本 | 链接 |
|---|---|---|
| AEM Oak | 1.84.0 | [Oak API 1.84.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.84/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [HTML 模板语言规范](https://github.com/adobe/htl-spec) |
| Apache HTTP 服务器 | 2.4.65 | [Apache Httpd 2.4.65](https://apache.googlesource.com/httpd/+/refs/tags/2.4.65/CHANGES) |
| AEM 核心组件 | 2.29.0 | [AEM WCM 核心组件](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14（默认） | [受支持的 Node.js 版本](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |
