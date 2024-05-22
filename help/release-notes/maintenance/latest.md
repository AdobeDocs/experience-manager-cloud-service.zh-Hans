---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: b6fe2a58bb16c70cef48426ec49dda474195c023
workflow-type: tm+mt
source-wordcount: '1612'
ht-degree: 9%

---

# 维护发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

## 版本 16357 {#release-16357}

以下总结了维护版本16357的持续改进，该版本于2024年5月22日公开发布。 上一个维护版本是版本 16145。

2024.5.0 功能激活将会为此维护版本提供全套功能。有关更多信息，请参阅[ Experience Manager 发布路线图](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增强 {#enhancements-16357}

* SITES-19579：用于将内容片段从一个模型迁移到另一个模型的Java API。
* SITES-19698： [打开API] 创建读取操作以管理OpenAPI定义中每个模型的UI架构。
* SITES-19834：Adobe I/O事件缺少用于发布/取消发布的ID。
* SITES-20146：为移动的页面启用预览版本/比较。
* SITES-19973：CFM搜索API实施。
* SITES-20333：改进创建内容片段时的验证。
* SITES-20334：改进编辑内容片段模型时的验证。
* SITES-20585：增强内容片段搜索API，以按区域设置进行过滤。
* SITES-20594：返回创建/修改/复制资源的用户的全名。
* SITES-20601： [OpenAPI] 更新CF Search API以允许仅提取直接子内容片段。
* SITES-20656： [BE] 提供替换字符串时匹配大小写的选项。
* SITES-20405： [Xwalk] 支持字段折叠的mimeType。
* SITES-17854：支持UUID以用于CF和资产引用(Pfizer MVP)。
* SITES-19555：适用于UI架构的简单模型API。
* SITES-19611： [打开API] 在OpenAPI定义中为每个模型创建用于管理UI架构的写入/更新操作。
* SITES-19614： [Xwalk] 电子表格分页/无限滚动。
* SITES-20005：创作管道应具有可配置的事件延迟。
* SITES-20121：允许枚举字段使用defaultValue。
* SITES-20342： [后端] 在文件夹级别发布 — 将过滤器添加到仅发布CF。
* SITES-20355：删除内容片段模型和权限API Servlet。
* SITES-20387：导航tagadmin将始终计算标记使用情况。
* SITES-20495： [BE] 能够获得在文件夹级别发布的权限。
* SITES-20653： [Xwalk] 添加experiment-start-date和 — end-date。
* SITES-20666： [Xwalk] 默认情况下，创作时应关闭试验。
* SITES-20752： [cq-wcm-core] 适用于CF的Apple启动项。
* SITES-20946：将etag添加为LIST模型端点中的属性。
* SITES-20947： [persistence] 按内容片段id获取子任务。
* SITES-21012：将模型元数据架构合并到产品。
* SITES-21769：对按ID检索的资源使用/jcr：id/路径前缀。
* ASSETS-30379：DRM许可证检查会展示正在下载的整个资源树。
* ASSETS-35535： [DaaS适配器错误] v1事件需要忽略空资源下载。
* SITES-21550： [Xwalk] 自定义元数据：数字、日期、日期时间、时间字段。
* SITES-20149： RTC： [cq-wcm-launches-core] 为CF的启动项导出新的API。
* SITES-20150： RTC： [cq-command] 向现有API添加新方法。
* SITES-20451：将sidecar插件添加到wcm-commons。
* SITES-20499： [MSM][Async] 将代码从AsyncOperationServlet提取到实用程序类。
* SITES-20763：更新站点集成中的投放API端点。
* SITES-20583：将etag作为属性添加到中 `LIST`/search fragments.
* CQ-4356445：事件生成器和架构实施。
* CQ-4356625：改进languagecopyrendercondition.jsp中的授权检查。
* CQ-4356629：改进isWorkflowUser rendercondition中的授权检查。
* CQ-4356934：在使用ResponseEntities时简化RequestProcessor API。
* CQ-4357214：请求处理器不得依赖于servlet逻辑。
* SITES-16392：失败的启动项创建不应留下垃圾内容。
* SITES-20238： [RTC] Pfizer MVP — 添加CF API以将CF路径解析为ID，反之亦然。
* SITES-21043： [CF][launches] Cloud Service的侧端口性能改进。
* SITES-21044： [CF][launches] 将侧端口异步编辑有效负载实现用于Cloud Service。
* Forms-9606：以前，在自适应Forms编辑器中，只有字段值可以映射到调用服务的响应。 现在，作者能够将字段的任何属性映射到调用服务响应。
* Forms-7483： AEM Forms JSON架构解析器现在支持JSON架构(2020-12)。
* Forms-13209：包含一个处理程序，用于覆盖自适应Forms默认提交成功和提交失败处理程序。 您可以通过自适应Forms规则编辑器配置这些处理程序。
* Forms-13612：屏幕阅读器现在可阅读基于核心组件的自适应Forms中的错误消息、简短描述和长篇描述。 此外，还增加了支持功能，可在表单包含错误且无法提交时使自适应表单输入失效。
* Forms-12052：表单作者现在可以应用自定义函数在提交之前预处理数据。
* Forms-11295：增加了对SHA256和AEM Forms数字签名的ECDSA算法的支持。
* Forms-9432：向数据源云配置中添加了其他内容类型（REST端点）。 它允许以键值对的形式将数据提交到经过身份验证的端点。

### 修复的问题 {#fixed-issues-16357}

* SITES-20608：在模板中包含时启用了个性化的体验片段会导致无限循环。
* SITES-19554： [Xwalk] 电子表格编辑器：不能清空单元格。
* SITES-19971：修补包含选项卡的CFM会更改字段的顺序。
* SITES-20168：内容片段模型 `locked` 字段未正确更新。
* SITES-20522：损坏的内容片段中断/adobe/sites/cf/fragments端点。
* SITES-20816： CF OpenAPI — 输出与引用片段的缺少模型不一致。
* SITES-21239：删除ContentFragmentSearchService循环依赖关系。
* SITES-20582：搜索和列出内容片段应允许深度0。
* SITES-20559： [MSM][XF][Lufthansa] 将体验片段从母版/语言转出到国家/语言时，不会更新引用。
* SITES-17772：AEM：具有管理员组的用户无法解锁其他用户锁定的页面。
* SITES-20401： [Xwalk] 节元数据不支持多值属性。
* SITES-21391： [OpenAPI事件] 修改内容片段模型的标题或标记（属性）时不会触发任何事件。
* SKYOPS-73234：AEM Assets全局DAM程序升级到AEM版本15553和PR ID 35362时，错误日志失败增加。
* SKYOPS-75341：分布交叉通路捆绑包中的NoSuchMethodError。
* SCRNS-3945： Skyline：屏幕中的未本地化“已计划”字符串。
* SITES-20586：模板“已发布”时间戳未更新。
* SITES-16674：继承转出配置复选框不适用于Live Copy属性。
* SITES-18680：无法提取graphql查询(Apple)中的引用变量。
* SITES-21233： [CoreCmp] 升级到15860后，GS1美国的可折叠项已损坏。
* SITES-20367：在AEM中删除启动项时出现问题。
* CQ-4357161：AEM 收件箱负载屏幕返回 404。
* SITES-20214：保存时出现AEM转出配置序列问题。
* SITES-20364： 302重定向不适用于URL中的选择器。
* SITES-20547：AEMas a Cloud Service上Live Copy排除的路径列表中的路径被截断。
* SITES-20691：体验片段模板限制不遵循cq：allowedTemplates。
* SITES-21122：带有内容片段的AEM CS Live Copy缺陷。
* ASSETS-38723：在初始化this.readRules之前调用getReadRulesForMetadataChildNodes()时，MetadataRulesProviderImpl引发的NPE。
* SITES-11727： [GQL] 内容片段引用的完全水合缺少数据。
* SITES-19462：资产搜索在AEM Cloud中无法正常工作。
* SITES-19994：用户尝试关闭内容片段时，关闭按钮会计时。
* SITES-20029：内容片段版本在关闭后立即创建，而不更改内容。
* SITES-21316：片段预览：由于代码从SITES-11727更改，预览失败。
* SITES-20023：文件上传不适用于多字段中的远程（新一代资产）资产。
* ASSETS-37611：为未发布的资产触发“请求完成移动操作”工作流。
* CQ-4357278：如果getRequestBodyType返回空值，则DispatcherServlet会引发NPE。
* CQ-4357279：当请求没有pathInfo时，请求处理失败。
* SITES-20496： [Xwalk] 在网站管理员中选择电子表格时没有属性选项。
* Forms-13827：在自适应Forms规则编辑器中，WHEN操作当前不支持带日期选取器的不同类型字段。
* Forms-13786：在自适应Forms规则编辑器中，拖放功能不适用于自定义函数。
* Forms-13587：在自适应Forms编辑器中，基于核心组件的自适应Forms的设备模拟器功能无法正常运行。
* Forms-14376当用户按下“重置”按钮时，如果静态文本标记为未绑定，则会导致控制台错误。
* Forms-13801：即使禁用了条款和条件组件，对应的复选框也会保持启用状态。
* Forms-11952：提交表单时，表单生成的提交URL以/content/开头，而不是/portale/，这会错误路由请求。 这样可防止请求到达预期服务器。
* Forms-13616：日期选取器将当前日期显示为晚一天，这可能是由于时区问题，并且由于这种不一致性和额外的显示模式问题，难以设置正确的日期格式。
* Forms-13829：清除并重新选择某个选择后，由模拟单选按钮功能规则控制的下拉菜单无法正确填充。 所需的行为是让单个复选框充当单选按钮，一次只允许一个选项，并允许取消选择所有选项。
* Forms-14244：在基于XDP的自适应表单中，复选框上嵌入了脚本，此类复选框之后的元素不会执行脚本。
* Forms-14267：用户在开发、暂存和生产环境中发送API请求时，遇到一致的超时错误。 这些请求与生成PDF相关，有时使用数据绑定预填充数据。 该问题会导致挂起的进程，该进程最终会超时，但在出错后重试时会成功。
* Forms-11589：对于仅具有AEM Forms解决方案（没有任何其他解决方案）的用户，前端管道无法正常工作。
* Forms-13896：在DoR（记录文档）输出中，日期和数字以阿拉伯语显示，无论输入数据是否使用公历数字合并。

### 已知问题 {#known-issues-16357}

无。

### 已弃用的功能和 API {#deprecated-16357}

若要了解 AEM as a Cloud Service 中已弃用或移除的功能，请参阅[已弃用和已移除的功能和 API。](/help/release-notes/deprecated-removed-features.md)

### 嵌套的技术 {#embedded-tech-16357}

| 技术 | 版本 | 链接 |
|---|---|---|
| AEM Oak | 1.62.0 | [Oak API 1.62.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.62.0/index.html) |
| AEM SLING API | 2.27.2 | [Apache Sling API 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.22-1.4.0 | [HTML 模板语言规范](https://github.com/adobe/htl-spec) |
| AEM 核心组件 | 2.25.4 | [AEM WCM 核心组件](https://github.com/adobe/aem-core-wcm-components) |
