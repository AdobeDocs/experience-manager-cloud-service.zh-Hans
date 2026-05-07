---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: d00af3aee8c2a42233bfc0f914a4e24abe921e08
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 30%

---


# 维护发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

## 发行说25892 {#release-25892}

以下总结了维护版本25892的持续改进，该版本于2026年5月7日公开发布。 以前的维护版本是25520版。

2026.5.0功能激活将提供此维护版本的完整功能集。 有关更多信息，请参阅[&#x200B; Experience Manager 发布路线图](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

>[!NOTE]
>
>发行说25821已设为私有。

### 增强功能 {#enhancements-25892}

* CQ-4362304：前端创建准则并更新LLM配置UI。
* GRANITE-39546：将Apache Tika升级到3.x。
* GRANITE-53957：将Azure SDK V8升级到V12，以用于oak-blob-azure。
* GRANITE-61245：删除所有commons-lang用法（替换为commons-lang3）。
* GRANITE-64748：颠覆OIDC身份验证处理程序。
* GRANITE-64764：将Apache Commons文本更新为1.15.0。
* GRANITE-64963：将Filevault更新为4.2.0。
* GRANITE-66197：为M365租户添加Microsoft Graph API电子邮件支持。
* GRANITE-66449：更新用于Java 17 API支持的Maven插件。
* GRANITE-66473：将咖啡因缓存库添加到base-granite。
* GRANITE-66836：将快速入门更新到Oak 2.0.0。
* SKYOPS-129301：将APIs jar Javadoc合规性级别设置为Java 17。
* SKYOPS-129351：更新反应流和反应栈，以实现MCP SDK兼容性。
* SKYOPS-131412：将Apache Commons Exec更新到最新版本。
* SKYOPS-131432：将Felix SCR更新为2.2.14。
* SKYOPS-131907：将Sling API区域更新为1.1.10。
* SKYOPS-131938：将GSON更新到最新版本。
* SKYOPS-132173：将Apache Commons编解码器更新到最新版本。
* SKYOPS-132182：更新Sling租户包。
* SKYOPS-132267：更新`org.osgi.service.component`注释。
* SKYOPS-132272：更新Sling功能模型包。
* SKYOPS-132525：添加快速入门分析器以防止新的API被删除。
* SKYOPS-134408：将`com.adobe.granite.asset.core`更新为2.2.82。
* SKYOPS-137750：将`com.adobe.granite.comments`更新为1.0.40。
* SKYOPS-137759：将`com.adobe.granite.jobs.async.ui.commons`更新为3.2.4。
* SKYOPS-138356：将`com.adobe.granite.oauth.server`更新为1.1.36。
* SKYOPS-138739：将SnakeYAML更新为2.6。

### 修复的问题 {#fixed-issues-25892}

* Assets-59546：删除对已弃用的commons-lang库的依赖项。
* Assets-64831： AssetProcessorProcess重置处理尝试计数导致资产卡住。
* Assets-66683：由uploadBlob失败导致的审批循环。
* CNTBF-613：注册节点类型时修复访问被拒绝(JCR-101)。
* GRANITE-44537：“国家/地区”中的字符串未在AEM中本地化。
* GRANITE-61760：修复了激活AdminUserInitializer失败的问题。
* GRANITE-64543：权限限制响应不遵循API结构。
* GRANITE-66692：内部类加载程序对包刷新不敏感。
* GRANITE-66732：对启动级别1捆绑包使用激活器而不是服务组件。
* GRANITE-66846： AEM权限API不显示`rep:ntNames`限制。
* SITES-39267：恢复关系链条目中的pagePath。
* SITES-43715：权限验证无法读取资源状态。

#### AEM Guides {#guides-25892}

* GUIDES-45110：使用&#x200B;**选择文件**&#x200B;对话框在编辑器中选择图像时，只显示光栅格式（如JPG、PNG和GIF）。 矢量文件（如`.ai`和`.eps`）未显示，因此无法选择。
* GUIDES-41938：在名称中包含空格的文件夹中创建主题时，会错误地创建一个重复的文件夹，其中空格被连字符替换，并且主题会保存在该文件夹中而不是原始文件夹中。
* GUIDES-38377：将文件夹配置文件中对输出预设的更改应用于现有映射时，将重置AEM Sites预设的已保存&#x200B;**发布上下文**。
* GUIDES-43547：打开大型主题或地图时，创作实例无响应，在某些情况下需要重新启动。
* GUIDES-32520：对元素使用Backspace时，无论光标位置如何，编辑器都会滚动到主题的顶部（编辑器2.0）。

如需了解有关新版本中新增功能、增强功能和已修复问题的更多信息，请查看 [Experience Manager Guides 发布路线图](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap)。

### 已知问题 {#known-issues-25892}

无。

### 已弃用的功能和 API {#deprecated-25892}

AEM as a Cloud Service 中已弃用和删除的功能和 API 在[已弃用和删除的功能和 API](/help/release-notes/deprecated-removed-features.md) 文档中有详细说明。

### 安全修复 {#security-25892}

AEM as a Cloud Service 致力于优化您平台的安全性和性能。 此维护版本解决了19个已识别的漏洞，强化了我们对强大系统保护的承诺。

### 嵌入的技术 {#embedded-tech-25892}

| 技术 | 版本 | 链接 |
|---|---|---|
| AEM Oak | 2.0.0 | [Oak 2.0.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/2.0.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [HTML 模板语言规范](https://github.com/adobe/htl-spec) |
| Apache HTTP 服务器 | 2.4.65 | [Apache Httpd 2.4.65](https://apache.googlesource.com/httpd/+/refs/tags/2.4.65/CHANGES) |
| AEM 核心组件 | 2.30.4 | [AEM WCM 核心组件](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14（默认） | [受支持的 Node.js 版本](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |
