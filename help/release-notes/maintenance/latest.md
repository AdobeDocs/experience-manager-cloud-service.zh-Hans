---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 96084c84c45af54b1f152e22b8331f85dc6b583f
workflow-type: tm+mt
source-wordcount: '1501'
ht-degree: 20%

---


# 维护发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

## 版本 20133 {#20133}

以下总结了维护版本20133的持续改进，该版本于2025年4月1日公开发布。 上一个维护版本是版本 19823。

激活 2025.4.0 功能后会为此维护版本提供全套功能。有关更多信息，请参阅[ Experience Manager 发布路线图](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增强功能 {#enhancements-20133}

* Assets-47850：如果启用AEM CS ES，则限制添加Scene7配置。
* CQ-4359547：从Git存储库中完全删除Guava。
* Forms-17551：添加了对SharePoint列表集成的记录文档(DoR)支持。
* Forms-18432：实施特定于表单（基于正则表达式）的客户端预填充配置，以便在没有OSGI级别更改的情况下启用选择性预填充功能。
* Forms-18513：在AEP Connector中实施数据树转换支持，以增强向导功能和数据处理功能。
* Forms-19068：在AEP Manager API中添加了对Forms Connector提交操作的支持，以增强表单数据集成功能。
* GRANITE-57717：更新AEM中的客户端包。
* SITES-10469： AdapterFactory应始终返回相同的PageManager实例。
* SITES-25130：发行核心组件2.28.0。
* SITES-25433：比较旧版本时支持完整页面渲染。
* SITES-25923：当不再存储任何url时，LinkInfoStorageImpl可能会阻止。
* SITES-26208：通过工作流删除内容片段现在允许选项通过删除新删除的片段来更新引用资源。
* SITES-26500：添加通过工作流移动内容片段的选项 — `move-fragments`。
* SITES-26711：转出触发器 — 链接未更新。
* SITES-27583：体验片段在移动后会丢失版本历史记录。
* SITES-27618：搜索页面中片段的引用不会返回所有结果。
* SITES-27781：为内容片段引用实施了模型级验证，允许根据引用的片段的模型约束和所需标记验证这些片段。
* SITES-27784：更新SQL查询生成以使用PATH函数而不是`jcr:path`。
* SITES-28040： Adobe Target ExperienceFragmentsReplicationListener已损坏。
* SITES-28051：获取当前用户对内容片段的权限： GET /cf/fragments/{fragmentId}/permissions。
* SITES-28190：设置预览集成测试。
* SITES-28227：在将资产作为引用添加到片段时，我们会验证资产是否存在。
* SITES-28248：根据OSGI配置切换站点事件。
* SITES-28255：所有3个审核属性中缺少全名：已创建、已修改和已发布。
* sites-28390： PageImpl：优化hasContent()。
* SITES-28404：删除创作实例上的页面应会将其从预览服务中取消发布。
* SITES-28446：添加了2个在响应中不可见的新字段 — NumberModelField中的占位符和LongTextModelField中允许的模型。
* SITES-28536：为内容片段创建`RENAME`端点。
* SITES-28537：添加通过工作流重命名内容片段的选项 — `rename-fragments`。
* SITES-28538：必须重新发布引用，才能在创作和发布时保留有效内容。
* SITES-28549：创建`/cf/domains`以根据AEM层返回域ID。
* SITES-29026：添加了一个可选参数，该参数使用语言和国家/地区代码指定内容片段的区域设置。
* SITES-29031：改进了PATCH生成片段的逻辑，从而提供了更好的性能。
* SITES-29169：如果状态为PUBLISHED的资源引用的资源被移动、重命名或删除，则将重新发布这些资源。
* SITES-29376：将添加代码切换为验证已发布的资源删除。
* SITES-29417：更新`/libs/cq/Page/proxy.jsp`以将请求转发到jcr：content节点而不是include。
* SITES-2947：创建/修改Kibana可视化图表以比较发布rasp。
* SITES-29733：提高了按内容片段标记进行模型搜索的性能。
* SITES-8316：内容策略：缓存ContentPolicyManager。
* SITES-24906：带有通用编辑器的Edge Delivery：支持作者创建的不带映射的电子表格（提前访问）。
* SITES-24907：带有通用编辑器的Edge Delivery：支持将Assets发布到多个站点，以便进行MSM用例（提前访问）。
* SITES-27956：使用通用编辑器的Edge Delivery：提高发布吞吐量（提前访问）。
* SITES-27956：带有通用编辑器的Edge Delivery：改进发布到Edge Delivery Services的错误处理（提前访问）。

### 修复的问题 {#fixed-issues-20133}

* cq-4358378：处理翻译执行中的许可证错误。
* CQ-4359263：作业完成时，对话框中未显示消息。
* CQ-4359386：无法将i18n词典添加到AEMaaCS中的翻译项目。
* Forms-18068：单选按钮和复选框组使用富文本字段的记录文档(DoR)中存在粗体文本渲染问题。
* Forms-18189：修改了自定义函数处理，以防止为空客户端库记录错误，并改进UI中的错误显示。
* Forms-18213：实施了从记录文档(DoR)隐藏/排除已禁用字段的功能，以提高文档清晰度和用户体验。
* Forms-18271： Forms主题编辑器显示未本地化的错误消息，影响表单配置和主题自定义中的用户体验。
* Forms-18304：由于设备相关的颜色错误，在Acrobat和LiveCycle ES4中通过验证的PDF/A-1b文档在AEM 6.5 Forms中被错误地标记为不合规的。
* Forms-18325：添加了Adobe Experience Platform (AEP)云配置，以增强表单数据集成和处理功能。
* Forms-18360：在SharePoint文档管理中增强了团队网站的Forms列表范围管理，以改进数据组织和访问控制。
* Forms-18375：如果未选择特定的配置容器，则基于基础组件的表单从`conf/global`文件夹中错误地选择recaptcha配置。
* Forms-18426：当列表名称包含特殊字符（例如，“ — ”）时，SharePoint列表查找功能失败，这会影响表单与SharePoint列表的集成。
* Forms-19028：客户端预填充功能中断了表单事件处理，导致值提交和DOMContentLoaded事件在表单加载时无法正确触发。
* Forms-6950：向文件系统navigator treeview组件添加了所需的ARIA角色和属性，以提高屏幕阅读器可访问性，并符合WCAG 4.1.2名称、角色、值（级别A）标准。
* Forms-7016：表单编辑器中的键盘焦点顺序不遵循逻辑导航。
* SITES-1960：改进了内容片段编辑器JSON预览操作的性能。
* SITES-24308：当内容大小调整为400%时，将显示水平滚动条。
* SITES-24493：交互式元素没有所需的角色。
* SITES-24669：无法通过键盘访问引用边栏窗口拆分器。
* SITES-26881： AEMaaCS可访问性错误 — 注释输入字段旁边的“三点”图标提供的角色不正确。
* SITES-26956：对SITES进行跟踪 — 24920无法在生产环境中移动页面。
* SITES-27707：由于资产名称问题（6.5 SP22回归），内容查找器资产列表失败。
* SITES-27757：使用通用编辑器的Edge Delivery：根据helix-html-pipeline语义重写图标。
* SITES-27780：在SP22上具有纯文本DefaultPasteMode的RTE中显示意外的&lt;br>标记。
* SITES-27958： Linkchecker引发“此会话已关闭”错误。
* SITES-28149：在XF导出到Target期间未触发自定义ExperienceFragmentLinkRewriterProvider。
* SITES-28449：工作流小组件UI错误 — 包括未在AEM中显示所有子页面的子页面。
* SITES-28456：在GraphiQL资源管理器中保存不正确的持久查询时，在UI上缺少通知(跟进 — SITES-28313)。
* SITES-28464：更新片段查询以使用带毫秒格式的日期。
* SITES-28486：在新内容片段编辑器中就地编辑不会重定向到旧编辑器。
* SITES-28570：缺少的资源元数据由内容片段的GraphQL正确处理。
* SITES-28580：经典映像资产查找器在SP22升级后损坏。
* SITES-28600：启动项 — 内容重复。
* SITES-28668：无法使用LaunchPromotionParameters提升启动项。
* SITES-28820：在rebase上创建的新变体中添加了Launch前缀两次。
* SITES-28877：未定义本地外部化器终结点时，UE URL服务引发异常。
* SITES-28956：如果标记由内容片段引用，则标记删除操作将显示警告。
* SITES-29208：在引用字段包含无效路径的情况下，正确返回引用和变量。
* SITES-29363：重置Live Copy按钮不适用于嵌套式Live Copy内容层次结构。
* SITES-29369：AIO中的Assets事件问题 | 错误地触发页面已发布/未发布事件。
* SITES-29972：“删除”和“重命名”操作有时会产生不真实的工作流注释。

### 已知问题 {#known-issues-20133}

无。

### 已弃用的功能和 API {#deprecated-20133}

AEM as a Cloud Service 中已弃用和删除的功能和 API 在[已弃用和删除的功能和 API](/help/release-notes/deprecated-removed-features.md) 文档中有详细说明。

#### 用户组和产品轮廓同步变更 {#changes-user-groups}

在使用 Adobe Admin Console 进行权限管理时，不得使用以下群组，因为它们将不再与 AEM 同步：
* 以 _GROUP_NAME_SUFFIX 结尾的 AEM 组。
* 来自其他环境、程序或产品的产品轮廓。

更多详细信息请查看[用户组和产品轮廓同步变更](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/security/changes-in-user-group-and-product-profile-synchronization)。

#### SPA 编辑器弃用 {#deprecate-spa-editor}

从版本 2025.4.0 开始，[SPA 编辑器](/help/implementing/developing/hybrid/introduction.md)已在新项目中弃用。SPA 编辑器仍支持现有项目，但不应在新项目中使用。

管理 AEM 中的 Headless 内容时首选以下编辑器：

* [通用编辑器](/help/edge/wysiwyg-authoring/authoring.md)，用于可视化编辑。
* [内容片段编辑器](/help/assets/content-fragments/content-fragments-managing.md)，用于以基于表单的方法编辑。

有关此弃用的详细信息，请参阅文档[SPA Editor弃用。](/help/implementing/developing/hybrid/spa-editor-deprecation.md)

### 安全修复 {#security-20133}

AEM as a Cloud Service 致力于优化您平台的安全性和性能。此维护版本解决了 34 个已发现的漏洞，增强了我们对强大系统保护的承诺。

### 嵌套的技术 {#embedded-tech-20133}

| 技术 | 版本 | 链接 |
|---|---|---|
| AEM Oak | 1.76.0 | [Oak API 1.76.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.76.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.26-1.4.0 | [HTML 模板语言规范](https://github.com/adobe/htl-spec) |
| AEM 核心组件 | 2.28.0 | [AEM WCM 核心组件](https://github.com/adobe/aem-core-wcm-components) |
