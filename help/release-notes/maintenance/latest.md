---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 6493c48797c09fa4598c2c0ff86c9cc1fafa758c
workflow-type: tm+mt
source-wordcount: '1448'
ht-degree: 14%

---


# 维护发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

## 版本 20783 {#20783}

以下总结了维护版本20783的持续改进，该版本于2025年5月13日公开发布。 上一个维护版本是版本 20626。

激活 2025.5.0 功能后会为此维护版本提供全套功能。有关更多信息，请参阅[ Experience Manager 发布路线图](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增强功能 {#enhancements-20783}

* Forms-19125：核心组件自适应表单编辑器已得到增强，可在数据源树中的相应部分放入表单画布中时支持自动映射可用的自适应表单片段。 这会将基础编辑器的关键工作效率功能引入核心组件。
* Forms-17107：AEM Forms现在提供增强的客户端自定义函数解析功能。 这包括支持现代JavaScript功能(ECMAScript ES10+)，例如可选链接，并引入了在自定义函数脚本中使用静态导入的功能。 这允许开发人员更好地组织代码，利用ESM模块，并移除在基于核心组件和Edge Delivery Services的自适应Forms中使用自定义函数时遇到的先前限制，特别是对于之前需要对这些功能采取变通办法的用户。
* SITES-27775：优化了发布期间的引用搜索。
* SITES-30885：优化了持久查询中的JSON处理。
* SITES-25433：带有通用编辑器的Edge Delivery：比较旧版本时支持完整页面渲染。
* SITES-27792：带有通用编辑器的Edge Delivery：为Edge Delivery服务配置添加特定模板
* SITES-19754：使用通用编辑器的Edge Delivery：当设置损坏时显示引人注目的错误消息。
* SITES-30328：带有通用编辑器的Edge Delivery：从Sidekick支持预览。
* SITES-23499：带有通用编辑器的Edge Delivery：允许将多个字段用于块选项。
* SITES-29987：在创建内容片段模型时添加用于设置`previewUrlPattern`的功能。
* sites-29874：在内容片段API中添加对LongTextField引用的支持。
* SITES-29601：为通过LongText字段引用的内容片段添加验证。
* SITES-24623：使GET和搜索片段API返回的ETags可用于修补。
* SITES-28557：PATCH内容片段中允许URL参数`references`。
* SITES-5358： [OpenAPI]复制具有子级的内容片段。
* SITES-29614： GET工作流端点。
* SITES-29615：列出批处理请求API端点。
* SITES-25130：将核心组件升级到2.28.0
* SITES-10575：“MSM Blueprint Bloomfilter加载器”尝试加载的行数大于100,000。
* SITES-26711： RTE文本字段的链接未更新为指向MSM转出时的Live Copy。
* SITES-25976：体验片段中的链接在MSM转出后不适用。

### 修复的问题 {#fixed-issues-20783}

* Assets-50994：传入流量在AemRequestEventFilter中被阻止。
* CQ-4358591：从具有“创建翻译项目”选项的站点引用面板创建语言副本时，缺少少数语言的项目。
* CQ-4359108：使用人工翻译导入/导出时，XLIFF 2.0格式失败。
* CQ-4358722：由于Java 11和Java 17中的区域设置代码不同，本地化不适用于旧版ISO代码。
* Forms-19808：保存包含已启用延迟加载的片段的大型表单时，用户无法提取草稿。
* Forms-19887：在HTML5中呈现表单时，XFA表单中的下拉字段（最初设置为只读访问）无法更改为打开/可编辑状态。 字段保持为只读状态并阻止用户交互，这与PDF渲染中它按预期工作的情况不同。
* Forms-19651：在规则编辑器中，如果在二进制条件中使用了按钮单击并且该规则的“then”语句中也使用了同一按钮，则规则将无法正常运行。
* Forms-19628：在基于核心组件的自适应Forms的自动生成的记录文档(DoR)中，如果根面板启用了“允许为标题使用富文本”选项，则从DoR中排除嵌套面板的标题也会错误地隐藏根面板的标题。
* Forms-18977：记录文档(DoR)服务生成的PDF缺少文档标题。 这可能会导致不符合PDF/UA和WCAG 2.1辅助功能标准，因为文档标题是辅助功能PDF的必需属性。
* Forms-18526：当在其条件中包含多个字段的规则从一个字段复制到另一个字段时，这些条件中的固定字段引用错误地保留其对原始源字段的引用，而不是更新到复制规则的新字段。
* Forms-19047：在AEM Forms上修改并重新发布自适应表单后（特别是6.5.22.0），某些表单元素（特别是文本框）的翻译可能缺失。
* Forms-19234： AEM Forms中PDF的时间轴功能允许用户查看有关PDF创建和版本控制的详细信息，当任何PDF上传到“Forms和文档”部分下后，该功能就会停止工作。
* Forms-18196：当XDP模板所需的可选字段数据在请求中留空时，`generatePrintedOutput`（或`generatePdfOutput`）同步HTTP API错误地返回200（成功）响应代码而不是预期的400（错误请求）错误代码。
* Forms-19336：在核心组件自适应表单编辑器（AF2编辑器）中，数据Source树中的搜索功能无法正常工作或按预期工作，阻止用户轻松查找特定数据元素。
* Forms-17707：AEP (Adobe Experience Platform)连接器在配置为连接到AEP平台“暂存”环境时无法正常工作。
* Forms-18526：复制具有基于多个字段的条件的规则时，在规则的条件或操作中引用的字段（不是触发规则的主字段）未更新以正确引用要将规则复制到的新字段。 而是继续引用从中复制规则的原始源字段。
* Forms-18474：规则旨在当表单上任何字段的更改错误地触发特定字段的值更改（例如，字段“A”）时，将焦点设置到特定面板或组件。 例如，如果字段“B”被修改，则焦点仍将被设置为指定的面板，即使该规则仅针对字段“A”的更改进行了配置。
* GRANITE-58276： OSGi依赖项循环导致HTL脚本引擎工厂无法正常工作。
* Oak-11673：由refreshLease导致的Oak-segment-azure v12 CPU增加。
* SITES-30752：生成持久查询响应时不使用`If-modified-since`/`last-modified`标头。
* SITES-30353： AEM内容片段中“src”字段的GraphQL DataFetchingExceptions。
* SITES-30333：从jcr中读取资产元数据以避免xmp解析问题。
* SITES-30140：创建内容片段引用时出现双窗口问题。
* SITES-29748：更正了renderconditions，以便在CF编辑器中显示managepublication/quickpublish操作。
* SITES-15452：不应根据启动项中的唯一CF元素副本对其进行检查。
* SITES-30386：带有通用编辑器的Edge Delivery：重复的UE cors.js导致UE在添加内容时产生重复部分。
* SITES-29745：修复了引用变体未水合的罕见问题。
* SITES-30585：在使用引用创建模型时无法设置“previewUrlPattern”。
* SITES-30327：发布没有权限的内容片段将为每个有效负载资源创建单独的工作流。
* SITES-29528：ETag不能用于发布实例上的缓存。
* SITES-30583：查找并替换工具将所有字符更改为小写。
* SITES-31157：由于ETag不一致，修补程序失败。
* SITES-31327： [OpenAPI]创作实例上的获取内容片段请求可以响应304。
* SITES-29691：尝试移动页面时出现NullPointerException。
* SITES-30728：在资产属性上配置时，OnTime/OffTime未按预期发布/取消发布。
* SITES-29789：AEM中已复制的根页面上的组件链接更改。
* SITES-29191：无法向产品列表组件添加超过20个SKU。
* SITES-30372：智能裁剪在AEM的图像(V2)核心组件上不起作用。
* SITES-28693：当标题为空时，Teaser组件呈现损坏的HTML。
* SITES-28668：无法使用 LaunchPromotionParameters 来推广发布。
* SITES-31005：增强转出作业UI以向客户显示进度。
* SITES-31020：增强创建Live Copy作业UI以向客户显示进度。
* SITES-29816：创建体验片段的实时副本时出现“未找到资源”错误。
* SITES-29363：重置实时复制按钮不可用于嵌套的实时复制内容层级。
* SKYOPS-106509：添加补充的加载打开标志，以支持Java 21上的GSON反射访问。

### 已知问题 {#known-issues-20783}

无。

### 已弃用的功能和 API {#deprecated-20783}

AEM as a Cloud Service 中已弃用和删除的功能和 API 在[已弃用和删除的功能和 API](/help/release-notes/deprecated-removed-features.md) 文档中有详细说明。

### 安全修复 {#security-20783}

AEM as a Cloud Service 致力于优化您平台的安全性和性能。此维护版本解决了 19 个已发现的漏洞，增强了我们对实现强大系统保护的承诺。

### 嵌入的技术 {#embedded-tech-20783}

| 技术 | 版本 | 链接 |
|---|---|---|
| AEM Oak | 1.78.1公吨20250429061757 | [Oak API 1.78.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.78.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.26-1.4.0 | [HTML 模板语言规范](https://github.com/adobe/htl-spec) |
| AEM 核心组件 | 2.29.0 | [AEM WCM 核心组件](https://github.com/adobe/aem-core-wcm-components) |
