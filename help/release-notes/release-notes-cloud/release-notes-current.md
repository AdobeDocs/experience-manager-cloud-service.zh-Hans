---
title: ' [!DNL Adobe Experience Manager] 作为Cloud Service的最新发行说明。'
description: ' [!DNL Adobe Experience Manager] 作为Cloud Service的最新发行说明。'
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
source-git-commit: 6c1320d43b551247e63962dd52ada58d463fb92e
workflow-type: tm+mt
source-wordcount: '1996'
ht-degree: 2%

---


# [!DNL Adobe Experience Manager]作为Cloud Service{#release-notes}的最新发行说明

以下部分概述了作为Cloud Service的[!DNL Experience Manager]当前（最新）版本的常规发行说明。

>[!NOTE]
>从此处，您可以导航到以前版本的发行说明；例如，2020年、2021年等年份的客户。

>[!NOTE]
>
>请参阅[近期文档更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html) ，以了解有关与版本不直接相关的文档更新的详细信息。

## 发布日期 {#release-date}

[!DNL Adobe Experience Manager]作为Cloud Service2021.4.0的发布日期是2021年5月6日。
以下版本(2021.5.0)将于2021年5月27日发布。

## AEM as a A Foundation{#aem-as-a-cloud-service-foundation}

### 新增功能 {#what-is-new-foundation}

* [发布内容树工作流](/help/operations/replication.md#publish-content-tree-workflow)  — 发布内容的深层层次结构时，新的工作流模型和步骤可提高性能。

## [!DNL Adobe Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### [!DNL Sites] {#what-is-new-sites}的新增功能

* GraphQL端点 — 现在，可以为各个AEM Sites配置启用AEM GraphQL API，并通过使用新的GraphQL控制台UI为这些配置创建自定义GraphQL端点。 UI还允许管理GraphQL端点。

* 内容模型、增强的日期和时间数据类型 — 现在可以配置日期和时间日期类型，以仅允许创作日期、时间或日期和时间信息。

* 内容模型、增强的标记数据类型 — 现在可以配置标记数据类型，以允许创作单个或多个标记。

* 内容模型、新的制表符占位符数据类型 — 新的制表符占位符数据类型允许将数据类型分组到将在内容片段编辑器的选项卡下呈现的部分中。

### [!DNL Sites] {#bug-fixes-sites}中的错误修复

* 内容片段 — 移动内容片段或文件夹现在会更新片段内的嵌套引用(CQ-4320815)

* GraphQL — 持久化查询现在支持特定于AEM Sites配置的用户定义的端点(CQ-4315928)

## [!DNL Adobe Experience Manager Assets] as a  [!DNL Cloud Service] {#assets}

### [!DNL Assets] {#what-is-new-assets}的新增功能

* [!DNL Experience Manager] 在下载原始文件的位置不会存档单个资产下载。此增强功能可加快下载速度。 请参阅[下载资产](/help/assets/download-assets-from-aem.md)。

* 现在，当您通过链接共享选项下载资产时，可以选择下载或不下载演绎版。 以前，会下载所有资产演绎版。 请参阅[下载选项](/help/assets/download-assets-from-aem.md)。

* 现在，在执行运行状况检查以批量导入资产时，Experience Manager会提供失败的更多信息原因。 请参阅[批量资产摄取](/help/assets/add-assets.md#asset-bulk-ingestor)。

* 现在，使用批量导入工具导入资产时，管理员可以选择在导入成功后删除源文件。 请参阅[批量资产摄取](/help/assets/add-assets.md#asset-bulk-ingestor)。

* 在编辑元数据架构时，新的根路径选择器字段允许管理员快速轻松地进行选择。 此增强功能有助于缩短元数据配置时间。

* 许多资产的元数据可以使用CSV文件批量导入，并可以导出到CSV文件。 默认日期格式现在为`yyyy-MM-dd'T'HH:mm:ss.SSSXXX`。 用户可以通过更新列标题来使用其他格式。 例如，将`Date: DateFormat: yyyy-MM-dd'T'HH:mm:ssXXX`添加为CSV文件中的列标题，而不是单词`Date`。 请参阅[导入元数据](/help/assets/metadata-import-export.md)。

* 在列视图中浏览资产时，可视指示器会显示每个资产的已批准或已拒绝状态。

* 在列视图中浏览资产时，会为过期的资产显示一个可视指示器。

* 在[!DNL Assets]元数据编辑器中提供了文本区域数据类型。 您可以使用此选项让用户在自由格式文本字段中输入元数据。

### [!DNL Assets] {#bug-fixes-assets}中的错误修复

* 尝试移动多个资产或文件夹时，控制台中会记录一个错误，并且移动操作未能完成。 如果标题无法更新，则移动操作会失败。 (CQ-4322080)

* 可以根据规则隐藏元数据字段，以便在满足预定义条件时，不必强制使用元数据。 但是，此类隐藏的元数据字段会显示为必填字段。 (CQ-4321285)

* 由于日期格式不正确，批量元数据导入失败。 (CQ-4319014)

* 当在“属性”页面中选择更新元数据时，当架构提供了多个选项时，界面响应速度会很慢。 (CQ-4318538)

* 在单行文本字段中更新和保存元数据值时，下拉菜单中的值会被删除，即使在下拉菜单中禁用了编辑也是如此。 (CQ-4317077)

* 您可以使用省略号作为注释来查看资产。 使用小椭圆时，椭圆与打印版本中注释的数量重叠。 (CQ-4316792)

## [!DNL Adobe Experience Manager Forms] as a  [!DNL Cloud Service] {#forms}

### [!DNL Forms] {#what-is-new-forms}的新增功能

您可以使用[AEM Forms作为Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/home.html)创建数字表单，将表单连接到现有数据源，将表单与Adobe Sign集成以向表单添加电子签名，生成记录文档(DoR)以将提交的表单存档为PDF文件。 该服务还可以将您现有的PDF forms转换为数字表单。 除了标准的AEM Forms功能外，该服务还提供若干云原生功能，如自动扩展、升级无停机以及云原生开发环境。 请阅读[此博客文章](https://blog.adobe.com/en/publish/2021/03/11/experience-manager-forms-as-a-cloud-service.html) ，了解AEM Forms作为Cloud Service的功能和特性。

* **在启用了Adobe Sign的自适应Forms中使用政府ID身份验证方法**

   Adobe Sign的政府ID流程由先进的机器学习算法提供支持，使全球的公司能够确保对其收件人身份的高质量身份验证。 现在，您可以在启用了Adobe Sign的自适应Forms中使用政府ID身份验证方法。

   政府ID是一种高级身份验证方法，它指示收件人[上传政府颁发的身份文档（驾照、国家ID、护照）](https://helpx.adobe.com/in/sign/using/adobesign-authentication-government-id.html)的图像，然后对该文档进行评估以确保其真实性。

* **支持将表单内签名体验用于异步自适应表单提交**

   现在，您可以将表单内签名体验用于异步自适应表单提交。 您还可以在[!DNL Experience Manager Sites]页面中嵌入自适应表单，并使用表单内签名体验来提交自适应表单。

* **支持在为分配任务步骤预填充自适应表单时使用变量指定附件**

   在为“分配任务”步骤预填充自适应表单时，您现在可以使用文档类型变量为自适应表单选择输入附件。

* **支持使用文字选项为JSON类型变量设置值**

   您可以使用文字选项在AEM工作流的设置变量步骤中为JSON类型变量设置值。 利用文本选项，可以指定字符串形式的JSON。

* **使用本地开发环境创建记录文档(DoR)**

   您可以在Cloud Service实例中将XDP用作记录文档模板，将AEM Forms用作Cloud ServiceSDK（本地开发环境）。 以前，支持仅限于Cloud Service实例。

### [!DNL Forms] {#bug-fixes-forms}中的错误修复

* 将配置为未生成记录文档的自适应表单提交到配置为生成记录文档的AEM工作流后，不会显示错误消息，并且任务无法提交。

### 其他更新{#misc-2021-04-0-forms}

* 为了更便于识别内容，该服务现在为XDP、动态PDF和架构文件生成实时缩略图。
* 添加了将PDF文件移动到AEM Forms UI中文件夹的功能。

## Adobe Experience Manager Commerce as aCloud Service{#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* 支持类别UID — 这会为对类别ID使用字符串的系统解锁第三方商务集成

* AEM的PWA Studio扩展，包括 示例集成

* 新的CIF导航核心组件，可扩展WCM导航核心组件

* AEM storefront中暂存目录数据的可视指示器

* 商务端点现在可通过Cloud Manager UI进行配置

### 错误修复 {#bug-fixes-commerce}

* 类别页面的页面属性的商务选项卡下未显示根类别字段


## Cloud Manager {#cloud-manager}

本部分概述了AEM as a 2021.5.0和2021.4.0Cloud Service中Cloud Manager的发行说明。

### 发布日期 {#release-date-cm-may}

AEM as a Cloud Service2021.5.0中的Cloud Manager的发布日期是2021年5月6日。
下一版本计划于2021年6月3日发布。

### 新增功能 {#what-is-new-may}

* PackageOverlaps质量规则现在会检测在同一部署的包集中多次部署同一包的情况，即在多个嵌入位置中部署同一包的情况。

* 现在，公共API中的存储库端点包含Git URL。

* Cloud Manager用户下载的部署日志将更有洞察力，现在将包含有关失败和成功方案的详细信息。

* 现在，已解决将代码推送到AdobeGit时遇到的间歇性故障。

* 现在，可以在编辑项目工作流期间将商务加载项应用于沙盒项目。

* 编辑程序体验已刷新。

* “环境详细信息”页面中的“域名”表将通过分页显示多达250个域名。

* 添加程序和编辑程序工作流中的解决方案选项卡将显示解决方案，即使该程序只有一个解决方案可用。

* 生成步骤日志中未生成任何已部署的内容包时的错误消息不明确。

### 错误修复 {#bug-fixes-cm-may}

* 有时，即使未部署该配置，用户也可能会在IP允许列表旁边看到绿色的“活动”状态。

* 管道变量API不会删除“已删除”变量，而是仅以状态&#x200B;**DELETED**&#x200B;标记它们。

* 某些代码气味类型的质量问题错误地影响了可靠性评级。

* 由于不支持通配符域，因此UI将禁止用户提交通配符域。

* 当从午夜UTC到凌晨1点之间开始管道执行时，Cloud Manager生成的对象版本不保证大于前一天创建的版本。

* 在沙盒项目设置过程中，成功创建包含示例代码的项目后，“概述”页面中的“管理Git”将显示为主页卡中的链接。

### 发布日期 {#release-date-cm-april}

AEM as a Cloud ManagerCloud Service2021.4.0的发布日期是2021年4月8日。

### 新增功能 {#what-is-new-april}

* 更新了添加和编辑程序工作流的UI，使其更加直观。

* 现在，具有必需权限的用户可以通过UI提交商务端点。

* 现在，环境变量的范围可以是特定服务（创作或发布）。 需要AEM版本`2021.03.5104.20210328T185548Z`或更高版本。

* 即使未配置管道，**管理Git**&#x200B;按钮也会显示在Pipelines卡上。

* Cloud Manager使用的AEM项目原型版本已更新至版本27。

* 在Adobe I/O开发人员控制台中，由Cloud Manager创建的项目不能再被无意中编辑或删除。

* 当用户添加新环境时，他们将被告知，一旦创建了环境，便无法将其移动到其他区域。

* 现在，环境变量的范围可以是特定服务（创作或发布）。 需要AEM版本2021.03.5104.20210328T185548Z或更高版本。

* 澄清了在删除环境时启动管道时的错误消息。

* 现在，由Eclipse项目提供的OSGi包已从规则`CQBP-84--dependencies`中排除。

### 错误修复 {#bug-fixes-cm-april}

* 编辑管道的体验审核页面时，以斜杠`( / )`开头的输入路径将不再导致该步骤卡在待处理状态中。

* 创建新生产管道时，如果用户未添加内容审核覆盖，则不会审核默认主页。

* `CloudServiceIncompatibleWorkflowProcess`的问题在可下载的问题CSV文件中的严重性不正确。

* `Runmode`检查对非文件夹节点产生误报。

## 内容传输工具 {#content-transfer-tool}

### 发布日期 {#release-date-ctt}

内容传输工具v1.4.0的发布日期是2021年5月11日。

### 新增功能 {#what-is-new-ctt-may}

* 此版本的内容传输工具会为要迁移到Cloud Service的资产创建文本演绎版。 需要文本演绎版才能支持对摄取的资产进行全文搜索。
* 用户可以创建的内容传输工具迁移集的最大数量已从4个增加到10个。

### 错误修复 {#bug-fixes-ctt-may}

* 修复了与内容传输工具UI中的自动刷新功能相关的多个错误。
* 包含`wipe=true`的内容传输工具导致目标上的计数器索引不正确。 此问题已修复。

## 最佳实践分析器{#best-practices-analyzer}

### 发布日期 {#release-date-bpa}

Best Practices Analyzer v2.1.12的发布日期是2021年4月12日。

### 错误修复 {#bug-fixes-bpa-april}

* 报告的BPA中发现重复的行。 此问题已修复。
* AEM版本6.4.2上的BPA UI会引发一个JS错误，该错误会禁用“生成报表”按钮。 此问题已修复

