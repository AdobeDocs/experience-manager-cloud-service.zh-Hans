---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: c1e175128ab6e4b483e3940d9bd86a06540ef40f
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 25%

---


# 维护发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

## 发行版本 24464 {#release-24464}

以下总结了维护版本24464的持续改进，该版本于2026年2月18日公开发布。 上一个维护版本是版本 24288。

2026.2.0 功能激活提供此维护版本的全套功能。有关更多信息，请参阅[&#x200B; Experience Manager 发布路线图](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增强功能 {#enhancements-24464}

* AEMANCH-264：添加对基于RequestEntity验证条件请求的支持。
* AEMARCH-269：为OpenAPI实施公开JavaEE验证API。
* AEMANCH-276：通过RequestEntity提供i18n支持。
* Assets-10995：设置下载zip文件中资源数量的限制。
* Assets-50788：更新搜索API以使用资源元数据GET API。
* Assets-50946：将使用元数据GET API的请求正文映射到JCR元数据。
* Assets-55866：在前面的处理完成之前，请避免提交对同一资源的新请求。
* Assets-60300：提供API以检索异步作业上下文和结果。
* Assets-60574：添加对最新版本的Sling API包的支持。
* Assets-61049：继续元数据管理器包开发。
* Assets-61692：默认情况下，在“搜索开放API”中执行语义搜索。
* Assets-61696：资源视图上的BAM路由和MFE包装器。
* Assets-61854：在激活/停用消息中发送GenStudio解决方案。
* Assets-61973：在AEM中创建API以管理提示。
* Assets-62182：适用于c2pa-manifest呈现的Asset Compute事件处理程序。
* Assets-62311：搜索回归问题。
* Assets-62413：在JSON的每个层中添加对customModifier字段的支持。
* Assets-62432：合并文件夹删除API PR。
* Assets-62540：在快速入门中增加用户界面触控优化版本。
* Assets-62622：在MatchQuery中处理搜索模式。
* Assets-62671：修复MatchQuery startsWith运算符。
* Assets-62780：为文件夹API添加功能切换。
* Assets-62988：隐藏c2pa清单演绎版，使其不显示在“演绎版”选项卡中。
* Assets-63336：仅应针对DAM命名空间元数据执行从AEM到DM的模板同步。
* Assets-63375：将资源上传实验OpenAPI置于功能切换之后。
* Assets-63453：确保所有用户都可以读取omnisearch配置。
* GRANITE-63744：允许将异步作业连接到sling作业。
* GRANITE-64567：自动禁用SKU搜索的语义搜索。
* GUIDES-41187：添加标头以便Guides使用。
* SITES-30452：带ASO的内容API — 标题和描述建议。
* SITES-33116：修复路径验证。
* SITES-34234：页面编辑器：保留内容树状态。

### 修复的问题 {#fixed-issues-24464}

* Assets-43198：资源过期通知电子邮件不遵循用户语言偏好设置。
* Assets-51840：改进了资源处理。
* Assets-52061：选择保存的搜索后无法导航回来。
* Assets-53155：改进了资源内容。
* Assets-53745：Dynamic Media下载流要求在选择Web预设之前取消选择原始资源。
* Assets-54260：资源内容修复。
* Assets-54787：改进了资源内容。
* Assets-57391：资源内容更新。
* Assets-59213： cq-dynamicmedia-core依赖于已弃用的commons-lang库。
* Assets-59214： cq-scene7-imaging依赖于已弃用的commons-lang库。
* Assets-59546： cq-remotedam-client-core依赖于已弃用的commons-lang库。
* Assets-59703： cq-dam-core依赖于已弃用的commons-lang库。
* Assets-59705： cq-dam-handler依赖于已弃用的commons-lang库。
* Assets-59707： cq-dam-indesign依赖于已弃用的commons-lang库。
* Assets-59709： cq-scene7-core依赖于已弃用的commons-lang库。
* Assets-59929：当字段具有新行字符时，元数据导出中的CSV将中断。
* Assets-60241：重命名文件夹时，异步移动作业失败。
* Assets-61134：从pom文件中删除comparisonVersion标记。
* Assets-61309：内容片段移动/复制不再更新内部引用。
* Assets-61730：重定向到“直接二进制访问”应遵循资源编码。
* Assets-62358： Assets报表CSV在内容路径中显示损坏的值。
* Assets-62610：在Assets UI中禁用了“Adobe Stock许可证”按钮。
* Assets-62613： `downloadasset`/`saveas`中的NPE。
* Assets-62656：对于非Assets搜索，OmnisearchAI 搜索指示器显示不正确。
* GRANITE-55387：更正用引号括起来的单词会删除整个单词。
* GRANITE-61240：通过存储在lazycontainer.js中的XSS实现RCE。
* GRANITE-64101：重新启动时，转换为ES的OOTB索引恢复为Lucene。
* SITES-24530：搜索模式中关闭/删除按钮的触控目标不够大。
* SITES-31425：启动工作流中存在未本地化的错误消息。

### 已知问题 {#known-issues-24464}

无。

### 已弃用的功能和 API {#deprecated-24464}

AEM as a Cloud Service 中已弃用和删除的功能和 API 在[已弃用和删除的功能和 API](/help/release-notes/deprecated-removed-features.md) 文档中有详细说明。

### 安全修复 {#security-24464}

AEM as a Cloud Service 致力于优化您平台的安全性和性能。此维护版本解决了 14 个已发现的漏洞，增强了我们对实现强大系统保护的承诺。

### 嵌入的技术 {#embedded-tech-24464}

| 技术 | 版本 | 链接 |
|---|---|---|
| AEM Oak | 1.90.0 | [Oak 1.90.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.90.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [HTML 模板语言规范](https://github.com/adobe/htl-spec) |
| Apache HTTP 服务器 | 2.4.65 | [Apache Httpd 2.4.65](https://apache.googlesource.com/httpd/+/refs/tags/2.4.65/CHANGES) |
| AEM 核心组件 | 2.30.4 | [AEM WCM 核心组件](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14（默认） | [受支持的 Node.js 版本](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |

