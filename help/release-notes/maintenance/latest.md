---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 0f16c31a5fea1fc538fbeabe6db182ad3a30560d
workflow-type: tm+mt
source-wordcount: '1619'
ht-degree: 12%

---


# 维护发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

## 版本 21772 {#21772}

以下总结了维护版本21772的持续改进，该版本于2025年8月6日公开发布。 上一个维护版本是版本 21706。

激活 2025.8.0 功能后会为此维护版本提供全套功能。有关更多信息，请参阅 [Experience Manager 发布路线图](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 新增功能  {#new-features-21772}

* SITES-30049：添加了新端点，用于通过内容片段的UUID检索内容片段的语言副本。

### 增强功能 {#enhancements-21772}

* CQ-4358722 ：解决了Java 11和Java 17之间因区域设置代码不同导致的本地化问题。
* Forms-19624：启用交互式通信(IC)。 它通过将结构化模板与动态数据相结合，使组织能够提供个性化的按需通信（如报表、发票和信件）。 借助基于Web的模板设计、可重用的内容片段、规则驱动的变化以及无缝数据集成等功能，IC支持跨渠道进行一致且可伸缩的客户通信。
* Forms-19587、FORMS-17107、FORMS-19591、FORMS-19582、FORMS-20129、FORMS-20002、FORMS-19593、FORMS-20655、FORMS-19583、FORMS-18024、FORMS-19581：对自适应Forms规则编辑器进行了以下增强：
   * 函数列表中的`validate`方法现在可以验证面板、字段和表单。
   * 改进了客户端自定义函数解析，以支持ES10+功能和静态导入。
   * 在规则编辑器中添加了现成(OOTB)“下载记录文档(DoR)”按钮。
   * 在规则中添加了对动态变量的支持。
   * 启用基于自定义事件的规则创建。
   * 可重复面板的规则现在在正确的上下文中执行，而不是仅在最后一个面板实例上执行。
   * 现在可以根据查询参数、UTM参数和浏览器参数触发规则。
   * 在EDS (Experience Data Store)中添加了对特定于表单的自定义函数脚本的支持。
   * 添加了对在规则编辑器的成功处理程序的“导航到”操作中使用`EVENT_PAYLOAD`的支持。
   * 在规则编辑器的输入参数中支持的函数调用，如果函数调用中缺少任何所需的参数，则不会保存已确认的规则。
   * 在规则编辑器UI中突出显示了损坏的规则。
* Forms-18450：reCAPTCHA V2（包括不可见的reCAPTCHA）现在更容易在自适应Forms中设置和使用。 配置现在集中在一个位置进行管理，使您能够更轻松地在表单中启用垃圾邮件保护。
* Forms-18385：通过Output服务增加了对XDP的AFP生成和AEM Forms中的数据的支持。
* Forms-17789：在规则编辑器中添加了一个现成按钮以下载记录文档(DoR)。
* Forms-20313、FORMS-2896：添加了对`dorExclude`属性的支持，以禁用基于核心组件的表单中的特定功能。
* Forms-20262：在客户端处理无效的文件附件（0字节）。
* Forms-18347：针对缺少表单容器代理组件改进了自适应Forms编辑器日志记录。
* Forms-16205：从基于核心组件的表单中的记录文档(DoR)中排除已禁用的组件。
* Forms-10836：将记录文档(DoR)中母版页属性的方向更改为从右到左。
* SITES-33025：通过ID而不是路径打开新的CF编辑器。
* SITES-32741：异步触发内容片段页面引用的更新。
* SITES-32087： GraphQL：在StringArray中添加对`_ignoreCase`的支持。
* SITES-12211：提高了模板编辑器中的性能
* SITES-32861：通过分块处理提高Live Copy创建的性能。
* SITES-21383：优化了内容片段启动删除操作的性能。
* SITES-31165：通过将转出操作拆分为可管理的块来提高性能。
* SITES-21353：使用数据库索引提高了内容片段启动项的查询性能。
* SITES-30495：增强了内容片段启动项中支持基于UUID的片段引用的功能。
* SITES-32151：增强了容器属性功能的API。
* SITES-26849：在移动或删除内容片段变体时调整反向引用。
* SITES-31846：添加用于复制/粘贴根片段和引用的选项，以便执行复制树操作。
* SITES-30241：移动、重命名或删除片段时，调整位于长文本字段中的引用。
* SITES-32684：增强了UI架构中同步选项卡更改的机制。
* SITES-33308：添加重试机制，以便在编辑模型时将更改同步到UI架构。
* SITES-32247：“文本和Personalization”组件中缺少对话框Personalization和UI不一致。
* SITES-32261：体验片段i18n未应用于字段。
* SITES-32666：模板谓词包含`\n`导致HTML查找失败。
* SITES-32674：尽管有`cq:showOnCreate`，特色图像字段图像选取器仍不适用于页面创建向导。
* SITES-32014：带有通用编辑器的Edge Delivery：为localhost、aem.page和aem.live添加自动配置CORS策略
* SITES-26532：带有通用编辑器的Edge Delivery：添加对本地化URL的支持（提前访问）。
* SITES-30887：添加存储在工作流元数据中的内容片段uuid。

### 修复的问题 {#fixed-issues-21772}

* CQ-4360190：修复了在尝试使用添加操作时发生的不支持该操作的keySet的`UnsupportedOperationException`。
* CQ-4360421：解决了Microsoft Translator订阅密钥加密的问题，以提高安全性和兼容性。
* Forms-20980：修复了自适应Forms中带自定义显示格式的日期选取器上的键盘辅助功能问题。
* Forms-20498：在OdataResponse中添加了对空指针异常的检查，以防止出现运行时错误。
* Forms-20947：解决了多个辅助功能问题，包括屏幕阅读器违规和文本截断/重叠问题。
* Forms-21030、FORMS-20630：解决了为自适应表单中的多个选择配置的下拉字段存在的问题。 生成的PDF现在正确包含所有选定值。
* Forms-19579：修复了重新保存时“调用服务”规则无法自动更正的问题。
* Forms-20734：更正了输出服务为基于XFAF的输入PDF模板生成的PDF文档中签名字段的重复。
* Forms-20934：修复了AEM Forms创作UI中的“自动填写属性”下拉列表，可删除重复条目并包括所有标准HTML自动完成令牌。
* Forms-20700：解决了在AEM Forms中进行初始加载时下拉帮助文本闪烁的问题。
* Forms-20307：修复了嵌入到网站页面上的表单未使用4字符区域设置进行翻译的问题。
* Forms-20493：解决了在获取数据时表单会自动刷新，进而给用户带来不便的问题。
* Forms-18455：增强了核心组件的自适应Forms编辑器，以显示数据源树中已用数据对象的圆点。
* Forms-19373：防止未配置任何复制代理的发布环境的复制错误。
* Forms-20042：修复了启用HTML配置的Apache Sling GET Servlet配置导致属性视图中断的问题。
* Forms-20036、FORMS-19978：解决了PDF/A-1b合规性和验证问题。
* Forms-19166：将pagedatasource.jsp移动到servlet以提高错误栈栈跟踪的清晰度，并添加了更多护栏和日志记录。
* Forms-16466：修复了可重复面板在AEM Forms中无法正确填充的问题。
* Forms-19629：解决了客户JSON架构解析的问题，提供了无效结果。
* LC-3923083：解决了XDP模板中边界项的“路径对象未标记”错误。
* SITES-33177：使用通用编辑器的Edge Delivery：修复作为逗号分隔字符串存储时损坏的节样式。
* SITES-33262：带有通用编辑器的Edge Delivery：修复没有名称的块（属性中断）页面呈现和发布。
* SITES-33309：使用通用编辑器的Edge Delivery：在写入电子表格时修复`IllegalArgumentException`，该电子表格在列中带有斜杠。
* SITES-33408：使用通用编辑器的Edge Delivery：修复电子表格在进行更改后不会显示为已修改。
* SITES-31992：GraphQL：修复包启动期间模型扫描中偶尔出现的错误。
* SITES-29967： GraphiQL：长查询名称被切断。
* SITES-26266：不会从BE响应(Java API)返回不以`/`开头的内容引用。
* SITES-17874： GraphQL持久查询：修复内容类型application/graphql-response+json的编码。
* SITES-24506：根据搜索结果通知屏幕阅读器。
* SITES-25268：改进了批注的屏幕阅读器。
* SITES-32366：拼写检查结果隐藏在RTE对话框中。
* SITES-32829：改进了MediaQuery模拟器以解析媒体查询级别3和级别4。
* SITES-32278：已修复标记字段以正确使用字段标签。
* SITES-25244：图像模式中不再显示水平条。
* SITES-33395：修复了内容片段Live Copy同步的转出按钮功能。
* SITES-33147：修复了影响实时关系功能的服务绑定问题。
* SITES-33528：修复了启动项提升期间的时间戳保留问题。
* SITES-33014：修复了从LaunchesAdapterFactory生成过多警告日志的问题。
* SITES-32305：修复了布局更改后的Live Copy继承中断功能。
* SITES-32268：为内容片段搜索禁用URL编码。
* SITES-32772：启用SITES-31455中的增强功能时，变量字段中锁定的属性始终为false — 这与统一etag值有关。
* SITES-32696：修复了继承中断的内容片段Live Copy字段无法再编辑的问题。
* SITES-31712：对生产作者进行全搜索时查询速度较慢。
* SITES-33039：页面事件未正确触发。
* SITES-31192：体验片段在移动后会丢失版本历史记录。
* SITES-33529：将ACS活动模板与AEM页面链接时出错。
* SITES-33678：为SITES-33529添加切换开关。
* SITES-33468： AEMaaCS无法连接到ACS。

### 更改功能 {#altered-functionality-21772}

* SITES-26344：在端点之间统一验证`fragmentId`/`modelId` — 这些ID现在已验证，如果无效，将返回400状态代码。
* SITES-29598：验证在更新内容片段模型时添加到片段引用字段中的内容片段引用。

### 已知问题 {#known-issues-21772}

* SITES-31791：内容片段GraphQL — 查询失败，显示“超出最大字段计数”。 请参阅[知识库文章](https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-27231)。

### 已弃用的功能和 API {#deprecated-21772}

AEM as a Cloud Service 中已弃用和删除的功能和 API 在[已弃用和删除的功能和 API](/help/release-notes/deprecated-removed-features.md) 文档中有详细说明。

### 安全修复 {#security-21772}

AEM as a Cloud Service 致力于优化您平台的安全性和性能。此维护版本解决了 35 个已发现的漏洞，增强了我们对实现强大系统保护的承诺。


### 嵌入的技术 {#embedded-tech-21772}

| 技术 | 版本 | 链接 |
|---|---|---|
| AEM Oak | 1.80.0 | [Oak API 1.80.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.80/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [HTML 模板语言规范](https://github.com/adobe/htl-spec) |
| Apache HTTP 服务器 | 2.4.63 | [Apache Httpd 2.4.63](https://github.com/apache/httpd/blob/2.4.63/CHANGES) |
| AEM 核心组件 | 2.29.0 | [AEM WCM 核心组件](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14（默认） | [支持的Node.js版本](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |

