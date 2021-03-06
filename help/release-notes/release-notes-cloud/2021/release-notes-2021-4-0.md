---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2021.4.0 版的发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2021.4.0 版的发行说明。'
exl-id: 775332b5-24ce-430e-97a2-6eeb80877c64
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '1535'
ht-degree: 29%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 的最新发行说明 {#release-notes}

以下部分概述了当前（最新）版本的 [!DNL Experience Manager] as a Cloud Service 的一般发行说明。

>[!NOTE]
>从此处，您可以导航到以前版本的发行说明；例如，2020年、2021年等年份的客户。

>[!NOTE]
>
>有关未与版本直接相关的文档更新的详细信息，请参阅[最新文档更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=zh-Hans)。

## 发布日期 {#release-date}

的发行日期 [!DNL Adobe Experience Manager] as a Cloud Service2021.4.0是2021年5月6日。
以下版本(2021.5.0)将于2021年5月27日发布。

## AEMas a Cloud Service基础{#aem-as-a-cloud-service-foundation}

### 新增功能 {#what-is-new-foundation}

* [发布内容树工作流](/help/operations/replication.md#publish-content-tree-workflow)  — 新的工作流模型和步骤在发布内容的深层层次结构时提高了性能。

## [!DNL Adobe Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### [!DNL Sites] 的新增功能 {#what-is-new-sites}

* GraphQL端点 — 现在，可以为各个AEM Sites配置启用AEM GraphQL API，并通过使用新的GraphQL控制台UI为这些配置创建自定义GraphQL端点。 UI还允许管理GraphQL端点。

* 内容模型、增强的日期和时间数据类型 — 现在可以配置日期和时间日期类型，以仅允许创作日期、时间或日期和时间信息。

* 内容模型、增强的标记数据类型 — 现在可以配置标记数据类型，以允许创作单个或多个标记。

* 内容模型、新的制表符占位符数据类型 — 新的制表符占位符数据类型允许将数据类型分组到将在内容片段编辑器的选项卡下呈现的部分中。

### [!DNL Sites] 中的错误修复 {#bug-fixes-sites}

* 内容片段 — 移动内容片段或文件夹现在会更新片段内的嵌套引用(CQ-4320815)

* GraphQL — 持久化查询现在支持特定于AEM Sites配置的用户定义的端点(CQ-4315928)

## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets] 的新增功能 {#what-is-new-assets}

* [!DNL Experience Manager] 在下载原始文件的位置不会存档单个资产下载。 此增强功能可加快下载速度。

* 当通过链接共享选项下载资产时，您现在可以选择下载或不下载演绎版。 以前，会下载所有资产演绎版。

* 管理员可以配置 [!DNL Experience Manager] ，以在批量摄取资产后删除资产源。 请参阅 [批量资产摄取](/help/assets/add-assets.md#asset-bulk-ingestor).

* 现在，在执行运行状况检查以批量导入资产时，Experience Manager会提供失败的更多信息原因。 请参阅 [批量资产摄取](/help/assets/add-assets.md#asset-bulk-ingestor).

* 现在，使用批量导入工具导入资产时，管理员可以选择在导入成功后删除源文件。 请参阅 [批量资产摄取](/help/assets/add-assets.md#asset-bulk-ingestor).

* 在编辑元数据架构时，新的根路径选择器字段允许管理员快速轻松地进行选择，从而缩短配置时间。

* 编辑元数据架构时，会添加一种数据类型，该数据类型在元数据编辑器中提供自由格式文本区域。 用户可以使用此文本区域输入自由格式文本作为资产的元数据。 请参阅 [元数据架构编辑器](/help/assets/metadata-schemas.md).

* 许多资产的元数据可以使用CSV文件批量导入，并可以导出到CSV文件。 默认日期格式现在为 `yyyy-MM-dd'T'HH:mm:ss.SSSXXX`. 用户可以通过更新列标题来使用其他格式。 例如，添加 `Date: DateFormat: yyyy-MM-dd'T'HH:mm:ssXXX` 作为列标题，而不是单词 `Date`.

* 在列视图中浏览资产时，可视指示器会显示每个资产的已批准或已拒绝状态。

* 在列视图中浏览资产时，会为过期的资产显示一个可视指示器。

### [!DNL Assets] 中的错误修复 {#bug-fixes-assets}

* 尝试移动多个资产或文件夹时，控制台中会记录一个错误，并且移动操作未能完成。 如果标题无法更新，则移动操作会失败。 (CQ-4322080)

* 可以根据规则隐藏元数据字段，以便在满足预定义条件时，不必强制使用元数据。 但是，此类隐藏的元数据字段会显示为必填字段。 (CQ-4321285)

* 由于日期格式不正确，批量元数据导入失败。 (CQ-4319014)

* 当在“属性”页面中选择更新元数据时，当架构提供了多个选项时，界面响应速度会很慢。 (CQ-4318538)

* 在单行文本字段中更新和保存元数据值时，下拉菜单中的值会被删除，即使在下拉菜单中禁用了编辑也是如此。 (CQ-4317077)

* 您可以使用省略号作为注释来查看资产。 使用小椭圆时，椭圆与打印版本中的注释数重叠。 (CQ-4316792)

* 在搜索后从搜索结果中选择资产时，不会显示快速发布选项。 (CQ-4317748)

## [!DNL Adobe Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] 的新增功能 {#what-is-new-forms}

* **在支持 Adobe Sign 的自适应表单中使用 Government ID 身份验证方法**

   通过先进的机器学习算法，Adobe Sign 的 Government ID 流程让世界各地的公司均可确保高质量地验证其收件人的身份。现在，您可以在支持 Adobe Sign 的自适应表单中使用 Government ID 身份验证方法。

   Government ID 是一种高级的身份验证方法，它指示收件人[上传政府颁发的身份证明文件（驾照、身份证、护照）的图像](https://helpx.adobe.com/in/sign/using/adobesign-authentication-government-id.html)，然后评估该证明文件以确保真实有效。

* **支持对异步提交自适应表单使用表单内签名体验**

   现在，您可以使用表单内签名体验来异步提交自适应表单。还可将自适应表单嵌入到 [!DNL Experience Manager Sites] 页面中，并使用表单内签名体验提交自适应表单。

* **支持在为“分配任务”步骤预先填充自适应表单时使用变量指定附件**

   在为“分配任务”步骤预先填充自适应表单时，现在可使用文档类型变量为该自适应表单选择输入附件。

* **支持使用字面选项设置 JSON 类型变量的值**

   可在 AEM Workflow 的“设置变量”步骤中使用字面选项设置 JSON 类型变量的值。通过字面选项，可按字符串的形式指定 JSON。

* **使用本地开发环境创建记录文档 (DoR)**

   可在 Cloud Service 实例和 AEM Forms as a Cloud Service SDK（本地开发环境）上使用 XDP 作为文档记录模板。以前仅限 Cloud Service 实例支持这样做。

### [!DNL Forms] 中的错误修复 {#bug-fixes-forms}

* 将配置为不生成记录文档的自适应表单提交到配置为生成记录文档的 AEM Workflow 时，不会显示任何错误消息，但任务无法提交。

### 其他更新 {#misc-2021-04-0-forms}

* 为了更便于识别内容，该服务现在为XDP、动态PDF和架构文件生成实时缩略图。
* 添加了将PDF文件移动到AEM Forms UI中放置文件夹的功能。

## Adobe Experience Manager商务as a Cloud Service {#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* 支持类别UID — 这会为对类别ID使用字符串的系统解锁第三方商务集成

* AEM的PWA Studio扩展，包括 示例集成

* 新的CIF导航核心组件，可扩展WCM导航核心组件

* AEM storefront中暂存目录数据的可视指示器

* 商务端点现在可通过Cloud Manager UI进行配置

### 错误修复 {#bug-fixes-commerce}

* 类别页面的页面属性的商务选项卡下未显示根类别字段

## Cloud Manager {#cloud-manager}

此部分概述了 AEM as a Cloud Service 2021.4.0 中的 Cloud Manager 的发行说明。

### 发布日期 {#release-date-cm-april}

AEM 2021.4.0版中Cloud Manager的发布日期是2021年4月8日。
下一版本计划于2021年5月6日发布。

### 新增功能 {#what-is-new-april}

* 更新了添加和编辑程序工作流的UI，使其更加直观。

* 现在，具有必需权限的用户可以通过UI提交商务端点。

* 现在，环境变量的范围可以是特定服务（创作或发布）。 需要AEM版本 `2021.03.5104.20210328T185548Z` 或更高版本。

* 的 **管理Git** 按钮，即使尚未配置管道，该按钮也会显示在管道卡上。

* Cloud Manager使用的AEM项目原型版本已更新至版本27。

* 在Adobe I/O开发人员控制台中，由Cloud Manager创建的项目不能再被无意中编辑或删除。

* 当用户添加新环境时，他们将被告知，一旦创建了环境，便无法将其移动到其他区域。

* 现在，环境变量的范围可以是特定服务（创作或发布）。 需要AEM版本2021.03.5104.20210328T185548Z或更高版本。

* 澄清了在删除环境时启动管道时的错误消息。

* 现在，Eclipse项目提供的OSGi包已从规则中排除 `CQBP-84--dependencies`.

### 错误修复 {#bug-fixes-cm-april}

* 编辑管道的体验审核页面时，输入路径以斜杠开头 `( / )` 将不再导致步骤卡在“待定”状态中。

* 创建新生产管道时，如果用户未添加内容审核覆盖，则不会审核默认主页。

* 的问题 `CloudServiceIncompatibleWorkflowProcess` 的可下载问题CSV文件中的严重性不正确。

* 的 `Runmode` 检查在非文件夹节点上产生误报。

## Best Practices Analyzer {#best-practices-analyzer}

### 发布日期 {#release-date-bpa}

Best Practices Analyzer v2.1.12的发布日期是2021年4月12日。

### 错误修复 {#bug-fixes-bpa-april}

* 报告的BPA中发现重复的行。 此问题已得到修复。
* AEM版本6.4.2上的BPA UI会引发一个JS错误，该错误会禁用“生成报表”按钮。 此问题已修复
