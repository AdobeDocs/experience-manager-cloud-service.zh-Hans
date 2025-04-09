---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的当前维护发行说明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: c8d7f23ef89de97ed656157ba628fd33206b4588
workflow-type: tm+mt
source-wordcount: '1577'
ht-degree: 95%

---


# 维护发行说明 {#maintenance-release-notes}

以下部分概述 Experience Manager as a Cloud Service 的当前维护版本的技术发行说明。

## 版本 20133 {#20133}

下面总结了维护版本 20133 的持续改进，该版本已于 2025 年 4 月 1 日公开发布。上一个维护版本是版本 19823。

激活 2025.4.0 功能后会为此维护版本提供全套功能。有关更多信息，请参阅[ Experience Manager 发布路线图](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增强功能 {#enhancements-20133}

* ASSETS-47850：如果 AEM CS 启用了 ES，则限制添加 Scene7 配置。
* CQ-4359547：从 git 存储库中完全移除 Guava。
* FORMS-17551：添加了对 SharePoint 列表集成的记录文档 (DoR) 支持。
* FORMS-18432：实现了特定于表单的（基于正则表达式）客户端预填充配置，从而无需进行 OSGI 级别的更改即可实现选择性预填充功能。
* FORMS-18513：在 AEP 连接器中实现了数据树转换支持，以增强向导功能和数据处理能力。
* FORMS-19068：在表单管理器 API 中添加了对 AEP 连接器提交操作的支持，以增强表单的数据集成功能。
* GRANITE-57717：在 AEM 中更新客户端包。
* SITES-10469：AdapterFactory 应该始终返回相同的 PageManager 实例。
* SITES - 25130：发布核心组件 2.28.0 版本。
* SITES-25433：比较旧版本时支持整页渲染。
* SITES-25923：当不再存储任何 URL 时，LinkInfoStorageImpl 可能会阻塞。
* SITES-26208：通过工作流删除内容片段时，现在允许通过移除新删除的片段来更新引用资源。
* SITES-26500：添加通过工作流移动内容片段的选项——`move-fragments`。
* SITES-26711：转出触发器——链接无法更新。
* SITES-27583：体验片段在移动后会丢失版本历史记录。
* SITES-27618：在页面中搜索某个片段的引用时不会返回所有结果。
* SITES-27781：实现了内容片段引用的模型级验证，允许根据模型约束和所需标记验证引用的片段。
* SITES-27784：更新 SQL 查询生成，以使用 PATH 函数而不是 `jcr:path`。
* SITES-28040：Adobe Target ExperienceFragmentsReplicationListener 已损坏。
* SITES-28051：获取当前用户对内容片段的权限：GET /cf/fragments/{fragmentId}/permissions。
* SITES-28190：预览集成测试的设置。
* SITES-28227：当将资产添加为某个片段的引用时，我们会验证该资产是否存在。
* SITES-28248：根据 OSGI 配置切换 Sites 事件。
* SITES-28255：所有 3 个审核属性（创建、修改、发布）均缺少全名。
* SITES-28390：PageImpl: 优化 hasContent()。
* SITES-28404：在作者端删除页面应从预览服务中取消发布。
* SITES-28446：在响应中新增了 2 个之前不可见的字段——NumberModelField 中的占位符和 LongTextModelField 中允许的模型。
* SITES-28536：为内容片段创建 `RENAME` 端点。
* SITES-28537：添加通过工作流重命名内容片段的选项——`rename-fragments`。
* SITES-28538：为确保作者和发布内容持续有效，必须重新发布参考。
* SITES-28549：创建 `/cf/domains` 以根据 AEM 层返回域 ID。
* SITES-29026：添加了一个可选参数，用于使用语言和国家/地区代码指定内容片段的区域设置。
* SITES-29031：改进了 PATCH 片段的逻辑，从而提供更好的性能。
* SITES-29169：如果状态为“已发布”的资源引用了已被移动、重命名或删除的资源，则这些资源将会被重新发布。
* SITES-29376：在已发布资源删除验证中添加代码切换功能。
* SITES-29417：将 `/libs/cq/Page/proxy.jsp` 更新为请求转发至 jcr:content 节点，而不是包含该节点。
* SITES-2947：创建/修改 kibana 可视化，以比较发布 rasp。
* SITES-29733：通过使用内容片段标记，提高了模型搜索的性能。
* SITES-8316：内容策略：缓存 ContentPolicyManager。
* SITES-24906：带有通用编辑器的 Edge Delivery：支持作者创建的无映射电子表格（早期访问）。
* SITES-24907：带有通用编辑器的 Edge Delivery：支持将资产发布到多个站点以满足 MSM 用例的要求（早期访问）。
* SITES-27956：带有通用编辑器的 Edge Delivery：提高发布吞吐量（早期访问）。
* SITES-27956：带有通用编辑器的 Edge Delivery：改进向 Edge Delivery 服务发布时的错误处理（早期访问）。
* SITES-29602：CIF：删除了core-cif-components-core中的Guava用法。
* SITES-25785： CIF：为CIF产品引用数据类型添加产品变体选择。
* SITES-26392： CIF[实验性]：PDP中CIF核心组件的JSON+LD。
* SITES-21278： CIF[实验性]： CIF清除缓存的功能。

### 修复的问题 {#fixed-issues-20133}

* CQ-4358378：处理翻译执行中的许可证错误。
* CQ-4359263：作业完成时对话框中不会显示任何消息。
* CQ-4359386：无法将 i18n 词典添加到 AEMaaCS 中的翻译项目。
* FORMS-18068：在使用富文本字段的单选按钮和复选框组中，记录文档 (DoR) 中的粗体文本呈现存在问题。
* FORMS-18189：修改了自定义函数处理方式，以防止对空客户端库进行错误记录，并改进用户界面中的错误显示。
* FORMS-18213：实现了从记录文档 (DoR) 中隐藏/排除禁用字段的功能，以提高文档清晰度和用户体验。
* FORMS-18271：Forms 主题编辑器显示未本地化的错误消息，影响表单配置和主题自定义的用户体验。
* FORMS-18304：由于设备相关的颜色错误，在 Acrobat 和 LiveCycle ES4 中通过验证的 PDF/A-1b 文档在 AEM 6.5 Forms 中被错误地标记为不合规。
* FORMS-18325：添加了 Adobe Experience Platform (AEP) 云配置以增强表单数据集成和处理能力。
* FORMS-18360：增强 Forms 文档管理中团队站点的 SharePoint 列表范围管理，以改善数据组织和访问控制。
* FORMS-18375：当未选择特定配置容器时，基于 Foundation Components 的表单会错误地从 `conf/global` 文件夹中选择 recaptcha 配置。
* FORMS-18426：当列表名称包含特殊字符（例如“-”）时，SharePoint 列表查找功能会失败，从而影响与 SharePoint 列表的表单集成。
* FORMS-19028：客户端预填充功能会打断表单事件处理，导致在表单加载时无法正确触发 Value commit 和 DOMContentLoaded 事件。
* FORMS-6950：向文件系统导航器树视图组件添加了所需的 ARIA 角色和属性，以提高屏幕阅读器的可访问性并符合 WCAG 4.1.2 名称、角色、值（级别 A）标准。
* FORMS-7016：表单编辑器中的键盘焦点顺序不符合逻辑导航。
* SITES-1960：改进了内容片段编辑器的 JSON 预览操作的性能。
* SITES-24308：当内容大小调整为 400% 时会出现水平滚动条。
* SITES-24493：交互元素不具备所需的角色。
* SITES-24669：参考轨道窗口分割器无法通过键盘访问。
* SITES-26881：AEMaaCS 可访问性错误——评论输入字段旁边的“三个点”图标所对应的角色不正确。
* SITES-26956：跟进 SITES-24920，无法在生产环境中移动页面。
* SITES-27707：内容查找器资产列表因资产名称问题而失败（6.5 SP22 回归问题）。
* SITES-27757：带有通用编辑器的 Edge Delivery：根据 helix-html-pipeline 语义重写图标。
* SITES-27780：在 SP22 上，RTE 中出现带有纯文本DefaultPasteMode 的意外 &lt;br> 标记。
* SITES-27958：Linkchecker 抛出“此会话已关闭”错误。
* SITES-28149：XF 导出到 Target 期间未触发自定义 ExperienceFragmentLinkRewriterProvider。
* SITES-28449：工作流小组件 UI 错误——包括子项未在 AEM 中显示所有子页面。
* SITES-28456：如果在 GraphiQL Explorer 中保存了不正确的持久查询，用户界面上会缺少通知（跟进——SITES-28313）。
* SITES-28464：更新片段查询以使用以毫秒为单位的格式化日期。
* SITES-28486：新内容片段编辑器中的就地编辑不会重定向到旧编辑器。
* SITES-28570：内容片段的 GraphQL 可以正确处理缺失的资产元数据。
* SITES-28580：升级到 SP22 后，经典图像资产查找器损坏。
* SITES-28600：发布——内容重复。
* SITES-28668：无法使用 LaunchPromotionParameters 来推广发布。
* SITES-28820：在基于重写创建的新变体中添加了两次发布前缀。
* SITES-28877：当未定义本地外部器端点时，UE URL 服务抛出异常。
* SITES-28956：如果内容片段引用了标记，则标记删除操作会显示警告。
* SITES-29208：当引用字段包含无效路径时，可以正确返回引用和变体。
* SITES-29363：重置实时复制按钮不适用于嵌套的实时复制内容层级。
* SITES-29369：AIO 中的资产事件问题 | 错误触发页面已发布/未发布事件。
* SITES-29972：删除和重命名操作有时会产生不真实的工作流程注释。
* SITES-24631：CIF：产品字段存在搜索问题。
* SITES-24902： CIF：产品URL格式无法按预期用于#variant_sku。
* SITES-29191： CIF：无法向产品列表组件添加超过20个SKU。

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

关于此次弃用的更多详情，请参阅文档 [SPA 编辑器弃用。](/help/implementing/developing/hybrid/spa-editor-deprecation.md)

### 安全修复 {#security-20133}

AEM as a Cloud Service 致力于优化您平台的安全性和性能。此维护版本解决了 34 个已发现的漏洞，增强了我们对实现强大系统保护的承诺。

### 嵌套的技术 {#embedded-tech-20133}

| 技术 | 版本 | 链接 |
|---|---|---|
| AEM Oak | 1.76.0 | [Oak API 1.76.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.76.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.26-1.4.0 | [HTML 模板语言规范](https://github.com/adobe/htl-spec) |
| AEM 核心组件 | 2.28.0 | [AEM WCM 核心组件](https://github.com/adobe/aem-core-wcm-components) |
