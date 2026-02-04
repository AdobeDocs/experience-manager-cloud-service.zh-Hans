---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: f01a98604e045c48ab7167122aee3b2468db6d52
workflow-type: tm+mt
source-wordcount: '988'
ht-degree: 23%

---


# 维护发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

## 发行版本 24288 {#24288}

以下总结了维护版本24288的持续改进，该版本于2026年2月4日公开发布。 上一个维护版本是版本 23963。

2026.2.0 功能激活将会为此维护版本提供全套功能。有关更多信息，请参阅[ Experience Manager 发布路线图](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

>[!NOTE]
>
>发行说24222已设为私有。

### 增强功能 {#enhancements-24288}

* CNTBF-604：创建新的contentbackflow包版本。
* CQ-4361592：为项目创建和更新添加TypeHint支持。
* CQ-4362198：最新的AEM和Granite包翻译。
* GRANITE-36205：将内部 Oak 发行版更新到最新版本。
* GRANITE-59211：OPTEL：添加了Nonce支持和自助服务配置。
* GRANITE-62166：更新迁移包以重用迁移工具中的迁移状态。
* GRANITE-62598：删除从内容包过滤器排除的冗余属性。
* GRANITE-62684：通过skyline-ops配置客户端套接字超时。
* GRANITE-62702：将sling发现替换为用于在线迁移的独立实施。
* GRANITE-62763：根据ASSETS旋转图标更新Guava弃用例外列表。
* GRANITE-62771：引入新的已弃用的Commons-Lang依赖项后，快速启动构建失败。
* GRANITE-62987：将Felix Webconsole更新到版本5.0.18。
* GRANITE-63339：改进Azure迁移状态Blob的租用机制。
* GRANITE-63343：在workflow.core中添加对最新版本Sling API包的支持。
* GRANITE-63799：凹凸OIDC身份验证包版本。
* GRANITE-63821：将Quickstart更新到Filevault版本，以修复JCRVLT-831/JCRVLT-839。
* GRANITE-63827：将快速入门更新到Oak的最新公共版本(1.90.0)。
* GRANITE-63888：将Quickstart更新为Jackrabbit 2.22.3。
* GRANITE-64030：将关键字和模式添加到表达式语言验证器的允许列表中。
* GRANITE-64050：允许隐藏的conf文件夹隐藏外部产品功能。
* SITES-30452：带ASO的内容API — 标题和描述建议。
* SITES-38099：更新`testing-model.txt`以使用更高版本的健全性检查。
* SKYOPS-43616：将Jenkins凭据迁移到Dispatcher存储库中的保险库。
* SKYOPS-108584：从0.6.0到0.6.10的凹凸事实工具。
* SKYOPS-115691：升级CORS过滤器捆绑包以在预检请求中添加Vary Origin标头。
* SKYOPS-123094：在快速入门中更新Apache HTTP组件。
* SKYOPS-123236：复制包中包含`rep:cugPolicy`。
* SKYOPS-123240：在快速入门中更新CRXDE依赖项。
* SKYOPS-123247：在快速入门中更新Sling XSS捆绑包。
* SKYOPS-123250：在快速入门中更新Sling安全包。
* SKYOPS-123327：AEM-CS SDK需要Java 21。
* SKYOPS-125574：更新快速入门中的netcentric AC工具包。
* SKYOPS-126150：改进线程转储生成器脚本的top命令。

### 修复的问题 {#fixed-issues-24288}

* Forms-23687：修复在没有默认值的条件下使用“包含规则”时的SSV验证失败。
* GRANITE-48472：在“编辑用户设置”选项卡中更改密码时出现本地化错误。
* GRANITE-50286：修复了“用户管理”模式的“状态”列中的布局问题。
* GRANITE-52301：本地化无法将更改提交到安全组中的会话字符串。
* GRANITE-52920：在“安全”“创建新用户”中创建用户时出现本地化错误。
* GRANITE-54654：在安全Adobe IMS配置检查对话框中本地化字符串。
* GRANITE-56371：修复安全信任存储区中数据格式不正确的问题。
* GRANITE-62717：升级加密密钥库，以便处理包含非ASCII字符的JSafe密码。
* GRANITE-62789：更新消息传递客户端以支持内容分发的不重试模式。
* GRANITE-62824：访问用户编辑器中的“组”选项卡时修复`NullPointerException`。
* GRANITE-63080：使`org.slf4j.spi`的导入与`slf4j 2.x`兼容。
* GRANITE-63210：更新分发核心以修复发布启动时调度程序失效的问题。
* GRANITE-63293：修复首次创作后必填路径字段丢失所需星号的问题。
* GRANITE-63360：修复了在选择多个路径时显示的错误信息。
* SITES-36242：缩小GraphQL执行正则表达式范围以修复绕过Dispatcher过滤器的问题。
* SITES-40122：修复了Edge Delivery与内容分发ImsService的集成。
* SKYOPS-84379：使用最新的FACT工具以便RDE进行正确的功能切换选取。
* SKYOPS-121216：恢复对Jackson 2.20.0库的更新。

#### AEM Guides {#guides-24288}

* GUIDES-38198 ：使用上下文菜单中的编辑MathML选项更新内联MathML公式时，在刷新页面之前，不会反映更新的值。
* GUIDES-38276：无法从Assets UI的“版本历史记录”面板中移除“版本”标签。
* GUIDES-36641：生成AEM Sites输出时，发布的输出中不包含包含关键字和主题标题以及`<ph>`元素的映射标题。
* GUIDES-37837：尝试保存主题或映射时，操作可能会间歇性地失败，并出现“无法保存文件”错误，尤其是在后台运行密集型资源处理任务或翻译工作流期间。
* GUIDES-27774： Broken list报告错误地包含外部链接、有效的`keyrefs`以及在当前映射范围内正确解析的关键字。

如需了解有关新版本中新增功能、增强功能和已修复问题的更多信息，请查看 [Experience Manager Guides 发布路线图](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap)。

### 已知问题 {#known-issues-24288}

无。

### 已弃用的功能和 API {#deprecated-24288}

* AEMSRE-2896：修复自定义的logmanager配置处理。
* GRANITE-62802：从`commons-lang`中删除已弃用的`granite.auth.saml`依赖项。
* GRANITE-62805：从`commons-lang`中删除已弃用的`granite.httpcache.core`依赖项。
* GRANITE-62864：从`commons-lang`中删除已弃用的`granite.jobs.async`依赖项。
* GRANITE-62865：从`commons-lang`中删除已弃用的`granite.replication.core`依赖项。
* GRANITE-62868：从`commons-lang`中删除已弃用的`granite.rest.api`依赖项。
* GRANITE-62895：从`commons-lang`中删除已弃用的`translation.connector.msft.core`依赖项。
* granite-63069：弃用`com.adobe.granite.httpcache.core`。
* GRANITE-63179：从`commons-lang`中删除已弃用的`cq-workflow-impl`依赖项。
* GRANITE-63180：从`commons.lang`包中删除已弃用的`cq-mailer`导出。
* SKYOPS-123329：删除对AEM Ethos部署的Java 11支持并更新`commons-lang3`。
* SKYOPS-124983：从AEM启动脚本中删除已弃用的`nashorn.args`。

AEM as a Cloud Service 中已弃用和删除的功能和 API 在[已弃用和删除的功能和 API](/help/release-notes/deprecated-removed-features.md) 文档中有详细说明。

### 安全修复 {#security-24288}

AEM as a Cloud Service 致力于优化您平台的安全性和性能。此维护版本解决了 10 个已发现的漏洞，增强了我们对强大系统保护的承诺。

### 嵌入的技术 {#embedded-tech-24288}

| 技术 | 版本 | 链接 |
|---|---|---|
| AEM Oak | 1.90.0 | [Oak 1.90.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.90.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [HTML 模板语言规范](https://github.com/adobe/htl-spec) |
| Apache HTTP 服务器 | 2.4.65 | [Apache Httpd 2.4.65](https://apache.googlesource.com/httpd/+/refs/tags/2.4.65/CHANGES) |
| AEM 核心组件 | 2.30.2 | [AEM WCM 核心组件](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14（默认） | [受支持的 Node.js 版本](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |
