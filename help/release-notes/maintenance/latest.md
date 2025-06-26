---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 467e21aff1c2164be729598d03f30f6a9e90c8aa
workflow-type: tm+mt
source-wordcount: '1758'
ht-degree: 15%

---


# 维护发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

## 版本 21331 {#21331}

以下总结了维护版本21331的不断改进，该版本于2025年6月24日公开发布。 上一个维护版本是版本 21193。

激活 2025.7.0 功能后会为此维护版本提供全套功能。有关更多信息，请参阅[ Experience Manager 发布路线图](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增强功能 {#enhancements-21331}

* CQ-4356522： `WorkflowResourceStatusProvider`优化。
* Forms-16458：用于选择字体属性（字体）的UI。
* Forms-17707： AEP连接器不适用于AEP platform stage。
* Forms-19125：支持AF编辑器中的自动片段映射。
* Forms-19336：在AF编辑器的数据Source树中添加了搜索。
* Forms-19417：支持层次结构视图中的单选按钮。
* Forms-19603：在规则编辑器中支持母版页和设计页。
* SITES-5358：内容片段Rest API：复制具有子项的CF。
* SITES-10575：“MSM Blueprint Bloomfilter加载器”尝试加载的行数超过100000行。
* SITES-14542：重命名/移动Live Copy源页面应触发发布重命名的/移动的Live Copy页面（如果之前已发布）。
* SITES-19754：使用通用编辑器的Edge Delivery：在集成遇到问题时添加一条用户可读的错误消息。
* SITES-23499：带有通用编辑器的Edge Delivery：添加对要用于块选项的多个字段的支持。
* SITES-23518：带有通用编辑器的Edge Delivery：添加对特定于Edge Delivery的资源演绎版的支持。
* SITES-24436：内容片段Rest API：引入了本地缓存，以加快重复引用的检索。
* SITES-25155：内容片段Rest API：删除模型列表中已弃用的“enabledForFolder”查询参数。
* SITES-25913：内容片段Rest API：在启动发布工作流之前对资源进行时间分组验证。
* SITES-25976：MSM 转出后，体验片段中的链接未调整。
* SITES-26271：内容片段Rest API：切换到GET变体端点的BFS遍历。
* sites-27486：通用编辑器 — AEM集成。
* SITES-27775：优化了发布期间的引用搜索（元数据延迟加载）。
* SITES-27782：带有通用编辑器的Edge Delivery：添加特定的发布者 — 订阅者实施以将内容发布到Edge Delivery（提前访问）。
* SITES-27792：带有通用编辑器的Edge Delivery：添加专用的Edge Delivery服务配置模板。
* SITES-28557：内容片段Rest API：允许使用通过`references=direct`调用`/cf/fragments/{fragmentId}`检索到的ETags修补内容片段。
* sites-28683：允许MSM LiveRelationship搜索跳过高级状态。
* SITES-29601：内容片段Rest API：验证长文本字段的内容片段引用。
* SITES-29614：内容片段Rest API：使用`/cf/workflows/{workflowInstanceId}`端点检索工作流，其中workflowInstanceIda是发布请求返回的id。
* SITES-29615：内容片段Rest API：列出使用`GET /cf/batch`通过POST `/cf/batch`创建的所有批次请求。
* SITES-29874：内容片段Rest API：现在可检索内容片段的长文本字段中的引用并进行水合。
* SITES-29930：内容片段Rest API：为内容片段发布工作流添加量度。
* SITES-29986：内容片段Rest API：支持CF模型技术命名。
* SITES-30088：内容片段Rest API： CF发布 — 当filterReferencesByStatus为空时，跳过检索引用。
* SITES-30126：内容片段Rest API：CF发布性能改进：用最小的检查替换了资源是否为片段的检查。
* SITES-30328：带有通用编辑器的Edge Delivery：添加对从Sidekick预览的支持。
* SITES-30445：内容片段Rest API： CF模型UI架构：添加一个选项以控制可折叠的初始状态。
* SITES-30604：内容片段Rest API：支持在新UI中采用模型元数据架构。
* SITES-30885：优化了持久查询中的 JSON 处理。
* SITES-30886：内容片段Rest API：内容片段端点的GET工作流基于存储在工作流元数据中的片段uuid。
* SITES-31005：增强转出作业UI以显示进度。
* SITES-31020：增强创建Live Copy作业UI以显示进度。
* SITES-31111：内容片段Rest API：允许变量修补程序API接受内容片段启动项中的内容片段引用。
* SITES-31343：内容片段Rest API：按日期向列出批处理请求的端点添加筛选和分页。
* SITES-31472：删除启动项会导致存储库在启动项大量增加时暂停。
* SITES-31641：内容片段Rest API：将属性添加到模型字段，用于存储与扩展相关的动态映射。
* SITES-31677：自定义工作区支持将AEM内容片段导出到Target。
* SITES-31770：内容片段Rest API：PATCH性能改进。
* SITES-31782：内容片段Rest API：添加对本地资产的描述。
* SITES-32175：允许中间提交以用于Live Copy创建和MSM页面转出。

### 修复的问题 {#fixed-issues-21331}

* CQ-4359756：翻译规则现在包括组件级别的过滤器属性。
* CQ-4359826：解决内容片段引用面板中状态不一致的问题。
* CQ-4359866： LanguageUtils类现在支持单元测试，而不添加其他依赖关系。
* Forms-13990： Forms服务API：文档生成：选择后留空的数据字段在预期为400时提供200。
* Forms-14309： Forms服务API ：提取数据响应代码纠正。
* Forms-18526：复制条件中包含多个字段的规则时，固定字段不会更改。
* Forms-18977：记录文档服务未传递文档标题。
* Forms-19047：在SP22上的AEM Forms上发布自适应表单后缺少翻译。
* Forms-19234：无法在AEM表单中使用PDF的时间轴功能。
* Forms-19628：在自动生成的DOR中，排除嵌套面板标题也会隐藏根面板标题。
* Forms-19651：当单击的按钮在二进制条件中使用，并且在then语句中使用同一按钮时，修复规则。
* Forms-19808：FormsPortal — 启用延迟加载时，无法提取草稿。
* Forms-19887：Access属性在HTML5 Preview中不起作用。
* SITES-15452：发布时不应根据唯一 CF 元素的副本检查这些元素。
* SITES-24492：ARIA标签没有可访问的名称。
* SITES-24623：内容片段Rest API：修复同一CF的端点之间的ETag不匹配。
* SITES-24668：当缩放比例增加到400%时，引用边栏功能中断。
* SITES-24678：引用边栏状态消息不由屏幕阅读器通知。
* SITES-24697：屏幕阅读器不会声明图像模型的加载状态。
* SITES-24708：当缩放比例增加到400%时，过滤器边栏功能中断。
* SITES-25235：屏幕阅读器未公告筛选边栏内容加载消息。
* SITES-25254：当内容查看速度为320px时，水平滚动条会显示在轮盘模式中。
* SITES-25433：带有通用编辑器的Edge Delivery：修复了多语言站点结构的页面版本渲染问题。
* SITES-26064：内容片段Rest API：修复了在后端创建片段并获取`AccessDeniedException`时返回的状态代码。
* SITES-26890：使用键盘时，在管理发布页面中无法显示“表标题”键盘焦点范围。
* SITES-29075：Live Copy概述不适用于高流量网站。
* SITES-29514：使用通用编辑器的Edge Delivery：将GitHub/项目URL设为创建新站点时的必需项。
* SITES-29691：无法移动特定启动项相关案例中的页面。
* SITES-29745：内容片段Rest API：在BFS遍历中实施引用变体的水合。
* SITES-29748：更正渲染条件，以显示 CF 编辑器中的管理发布/快速发布操作。
* SITES-29789：复制的根页面上的组件链接更改问题。
* SITES-29987：内容片段重置API：创建和编辑内容片段模型不支持`previewUrlPattern`。
* SITES-30140：创建内容片段引用时出现双重窗口问题。
* SITES-30327：内容片段Rest API：发布没有权限的CF将为每个有效负载资源创建单独的工作流。
* SITES-30333：从 jcr 读取资产元数据，以避免 xmp 解析问题。
* SITES-30353：AEM 内容片段中“src”字段的 GraphQL DataFetchingExceptions。
* SITES-30377：使用通用编辑器的Edge Delivery：整理组织和站点名称。
* SITES-30386：使用通用编辑器的Edge Delivery：删除重复的旧版UE `cors.js`。
* SITES-30583：内容片段Rest API：查找并替换工具将所有字符更改为小写。
* SITES-30585：创建包含引用的CFM时未设置内容片段Rest API： `previewUrlPattern`。
* SITES-30634： RTE图像替换文本和对齐方式不一致。
* SITES-30660：自定义AEM组件存在ADA合规性问题。
* SITES-30695：使用通用编辑器的Edge Delivery：提高重写器管道的排名，以免干扰自定义代码。
* SITES-30727：无法在生产创作编辑器中拖放组件。
* SITES-30752：生成持久查询响应时不要使用 `If-modified-since`/`last-modified` 标头。
* SITES-30871：触发afteredit侦听器后，DOM更新。
* SITES-30877：子页面转出状态不正确。
* SITES-30899：转出“稍后”选项允许在未选择日期的情况下继续。
* SITES-30947：由于转出期间的Blueprint上缺少“行为”属性，出现空指针异常。
* SITES-31157：内容片段Rest API：修补程序失败是特定案例。
* SITES-31162：内容片段Rest API：修复了`ModelFieldMapper`中`DateTimeField`字段的强制转换问题。
* SITES-31174：内容片段Rest API：标记未与发布请求一起发布。
* SITES-31272：无法通过PageManager.copy创建Assets语言副本。
* SITES-31327：内容片段Rest API：删除GET片段请求中的ETag验证。
* SITES-31387：重新启用Ghost组件继承时，JavaScript出现“ns.ui.alert is not a function”错误。
* SITES-31454：内容片段Rest API：放松片段引用字段的模式，使其也接受UUID。
* SITES-31455：内容片段Rest API：修复相同内容片段模型的端点之间的ETag不匹配。
* SITES-31459：内容片段Rest API：当存在内容引用字段时，无法编辑CF Live Copy。
* SITES-31467：页面编辑器中contexthub.authoring-hook.js的js-errors。
* SITES-31487：内容片段Rest API：允许为根文件夹调用权限端点。
* SITES-31621：带有通用编辑器的Edge Delivery：从作为活动副本的电子表格中删除空行。
* SITES-31676：创作或删除组件会在页面底部留下空格。
* SITES-31822：经典UI复选框标签缺失并编码的HTML。
* SITES-31857：在具有单引号的文件夹中创建CF失败。
* SITES-31888：内容片段删除无法传播到预览。
* SITES-31922：内容片段Rest API：referencedBy端点不返回页面引用。
* SITES-31987：在将内容片段发布到预览时不会显示内容片段的previewURL。
* SITES-32095：在Live Copy中的afterchilddelete事件侦听器执行后自动刷新失败。
* SITES-32237：使用通用编辑器的Edge Delivery：修复了呈现空/格式错误的文本组件的问题。

### 已知问题 {#known-issues-21331}

无。

### 已弃用的功能和 API {#deprecated-21331}

AEM as a Cloud Service 中已弃用和删除的功能和 API 在[已弃用和删除的功能和 API](/help/release-notes/deprecated-removed-features.md) 文档中有详细说明。

### 安全修复 {#security-21331}

AEM as a Cloud Service 致力于优化您平台的安全性和性能。此维护版本解决了 21 个已发现的漏洞，增强了我们对强大系统保护的承诺。

### 嵌入的技术 {#embedded-tech-21331}

| 技术 | 版本 | 链接 |
|---|---|---|
| AEM Oak | 1.80.0 | [Oak API 1.80.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.80.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [HTML 模板语言规范](https://github.com/adobe/htl-spec) |
| AEM 核心组件 | 2.29.0 | [AEM WCM 核心组件](https://github.com/adobe/aem-core-wcm-components) |
