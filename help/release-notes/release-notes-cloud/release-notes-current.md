---
title: 作为Cloud Service的 [!DNL Adobe Experience Manager] 当前发行说明。
description: 作为Cloud Service的 [!DNL Adobe Experience Manager] 当前发行说明。
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
translation-type: tm+mt
source-git-commit: 92de2936fd6eb66198f0a096dd2e0020f14fccb8
workflow-type: tm+mt
source-wordcount: '1906'
ht-degree: 2%

---


# [!DNL Adobe Experience Manager]作为Cloud Service{#release-notes}的当前发行说明

以下部分概述了作为Cloud Service的[!DNL Experience Manager]当前（最新）版本的一般发行说明。

>[!NOTE]
>您可以从此处导航到先前版本的发行说明；例如，2020年、2021年等年。

>[!NOTE]
>
>请参阅[最近文档更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html)，了解与版本不直接相关的文档更新的详细信息。

## 发布日期 {#release-date}

作为Cloud Service2021.4.0的[!DNL Adobe Experience Manager]的发布日期为2021年5月6日。
以下版本(2021.5.0)将于2021年5月27日发布。

## AEM as a Cloud Service Foundation{#aem-as-a-cloud-service-foundation}

### 新增功能 {#what-is-new-foundation}

* [发布内容树工作流](/help/operations/replication.md#publish-content-tree-workflow)  — 新的工作流模型和步骤在发布内容的深层层次结构时提高了性能。

## [!DNL Adobe Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### [!DNL Sites] {#what-is-new-sites}中的新增功能

* GraphQL终结点 — 现在，可以为各个AEM Sites配置启用AEM GraphQL API，并通过使用新的GraphQL控制台UI为这些配置创建自定义GraphQL终结点。 该UI还允许管理GraphQL端点。

* 内容模型、增强的日期和时间数据类型 — 现在可以配置日期和时间日期类型，以仅允许创作日期、时间或日期和时间信息。

* 内容模型、增强的标记数据类型 — 现在可以配置标记数据类型以允许创作单个或多个标记。

* 内容模型、新的制表符占位符数据类型 — 新的制表符占位符数据类型允许将数据类型分组到将在内容片段编辑器的选项卡下呈现的部分中。

### [!DNL Sites] {#bug-fixes-sites}中的错误修复

* 内容片段 — 移动内容片段或文件夹现在会更新片段内的嵌套引用(CQ-4320815)

* GraphQL — 持久查询现在支持特定于AEM Sites配置的用户定义终结点(CQ-4315928)

## [!DNL Adobe Experience Manager Assets] a  [!DNL Cloud Service] {#assets}

### [!DNL Assets] {#what-is-new-assets}中的新增功能

* [!DNL Experience Manager] 不存档下载原始文件的单个资源下载。此增强功能可加快下载速度。

* 当通过链接共享选项下载资产时，您现在可以选择下载或不下载演绎版。 以前，会下载所有资产演绎版。

* 管理员可以配置[!DNL Experience Manager]以在执行批量资产摄取后删除资产源。 请参阅[批量资产摄取](/help/assets/add-assets.md#asset-bulk-ingestor)。

* 当执行运行状况检查以批量导入资产时，Experience Manager现在提供故障的更多信息原因。 请参阅[批量资产摄取](/help/assets/add-assets.md#asset-bulk-ingestor)。

* 使用批量导入工具导入资源时，管理员现在可以选择在成功导入后删除源文件。 请参阅[批量资产摄取](/help/assets/add-assets.md#asset-bulk-ingestor)。

* 编辑元数据模式时，新的根路径选择器字段使管理员能够快速、轻松地进行选择，从而缩短配置时间。

* 许多资产的元数据可以使用CSV文件批量导入，也可以导出到CSV文件。 现在，默认日期格式为`yyyy-MM-dd'T'HH:mm:ss.SSSXXX`。 用户可以通过更新列标题来利用不同的格式。 例如，在CSV文件中将`Date: DateFormat: yyyy-MM-dd'T'HH:mm:ssXXX`添加为列标题，而不是单词`Date`。

* 在“列”视图中浏览资产时，系统会显示每个资产的已批准或已拒绝状态。

* 在列视图中浏览资产时，会为过期的资产显示一个可视指示符。

* 在[!DNL Assets]元数据编辑器中提供了文本区域数据类型。 您可以使用此选项让用户在自由格式文本字段中输入元数据。

### [!DNL Assets] {#bug-fixes-assets}中的错误修复

* 尝试移动多个资产或文件夹时，控制台中会记录一个错误，移动操作尚未完成。 如果标题无法更新，则移动操作将失败。 (CQ-4322080)

* 可以根据规则隐藏元数据字段，这样在满足预定义条件时，元数据就不是必填项。 但是，此类隐藏的元数据字段会显示为必填字段。 (CQ-4321285)

* 由于日期格式不正确，批量元数据导入失败。 (CQ-4319014)

* 当在“属性”页中进行选择以更新元数据时，当模式提供了许多选项时，界面响应速度会很慢。 (CQ-4318538)

* 在单行文本字段中更新和保存元数据值时，即使在下拉菜单中禁用了编辑，下拉菜单中的值也会被删除。 (CQ-4317077)

* 您可以使用省略号作为注释来审阅资产。 使用小椭圆时，椭圆会与打印版本中的注释数重叠。 (CQ-4316792)

## [!DNL Adobe Experience Manager Forms] a  [!DNL Cloud Service] {#forms}

### [!DNL Forms] {#what-is-new-forms}中的新增功能

您可以使用[AEM Forms作为Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/home.html)创建数字表单、将表单连接到现有数据源、将表单与Adobe Sign集成以向表单添加电子签名、生成记录文档(DoR)以将提交的表单存档为PDF文件。 该服务还可以将您现有的PDF forms转换为数字表单。 除标准AEM Forms功能外，该服务还优惠了几个云本机功能，如自动扩展、升级零停机和云本机开发环境。 阅读[此博客文章](https://blog.adobe.com/en/publish/2021/03/11/experience-manager-forms-as-a-cloud-service.html)，了解AEM Forms作为Cloud Service的功能和特性。

* **在启用Adobe Sign的自适应Forms中使用政府ID身份验证方法**

   Adobe Sign的政府ID流程以高级机器学习算法为后盾，为全球公司提供了确保收件人身份的高质量身份验证的能力。 现在，您可以在启用Adobe Sign的自适应Forms中使用政府ID身份验证方法。

   政府ID是一种高级身份验证方法，指示收件人[上传政府颁发的身份文档（驾照、国家ID、护照）](https://helpx.adobe.com/in/sign/using/adobesign-authentication-government-id.html)的图像，然后评估该文档以确保其真实。

* **支持对异步自适应表单提交使用表单签名体验**

   现在，您可以将表单内签名体验用于异步自适应表单提交。 您还可以在[!DNL Experience Manager Sites]页面中嵌入自适应表单，并使用表单内签名体验提交自适应表单。

* **支持在为分配任务步骤预填充自适应表单时使用变量指定附件**

   在为分配任务步骤预填充自适应表单时，您现在可以使用文档类型变量为自适应表单选择输入附件。

* **支持使用文本选项设置JSON类型变量的值**

   您可以使用文本选项在AEM工作流的设置变量步骤中设置JSON类型变量的值。 文本选项允许您以字符串形式指定JSON。

* **使用本地开发环境创建记录文档(DoR)**

   您可以将XDP用作Cloud Service实例上的“记录”模板的文档，将AEM Forms用作Cloud Service SDK(本地开发环境)。 以前，支持仅限于Cloud Service实例。

### [!DNL Forms] {#bug-fixes-forms}中的错误修复

* 将配置为不生成记录文档的自适应表单提交到配置为生成记录文档的AEM工作流时，不会显示错误消息，任务无法提交。

### 其他更新{#misc-2021-04-0-forms}

* 为了更轻松地识别内容，服务现在为XDP、动态PDF和模式文件生成实时缩略图。
* 添加将PDF文件移动到AEM Forms UI中放置的文件夹的功能。

## Adobe Experience Manager Commerce as aCloud Service{#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* 支持类别UID — 这将解锁对类别ID使用字符串的系统的第三方商务集成

* AEM extension for PWA Studio，包括 示例集成

* 扩展WCM导航核心组件的新CIF导航核心组件

* AEM商店中分阶段目录数据的可视指示器

* 现在可通过Cloud Manager UI配置商务端点

### 错误修复 {#bug-fixes-commerce}

* 根类别字段未显示在类别页面页面属性中的“商务”选项卡下


## Cloud Manager {#cloud-manager}

本节概述AEM中作为Cloud Service 2021.5.0和2021.4.0的Cloud Manager发行说明。

### 发布日期 {#release-date-cm-may}

AEM中Cloud Manager作为Cloud Service 2021.5.0的发布日期为2021年5月06日。
下一版本计划于2021年6月03日发布。

### 新增功能 {#what-is-new-may}

* PackageOverlaps质量规则现在检测在同一部署的包集中多次部署同一包的情况，即在多个嵌入式位置中部署同一包。

* 公共API中的存储库端点现在包括Git URL。

* 由Cloud Manager用户下载的部署日志将更直观，现在将包含有关失败和成功方案的详细信息。

* 现在，已解决将代码推送到Adobe Git时遇到的间歇性故障。

* Commerce add-on现在可以在“编辑”项目工作流程中应用到沙箱项目。

* 编辑项目体验已刷新。

* “环境详细信息”页中的“域名”表将通过分页显示多达250个域名。

* 添加项目和编辑项目工作流中的解决方案选项卡将显示解决方案，即使项目仅提供一个解决方案也是如此。

* 生成未生成任何已部署内容包时生成步骤日志中的错误消息不清楚。

### 错误修复 {#bug-fixes-cm-may}

* 有时，即使未部署IP允许列表，用户也可能在IP配置旁看到绿色的“活动”状态。

* 管道变量API将仅以状态&#x200B;**DELETED**&#x200B;标记它们，而不是删除“deleted”变量。

* 某些“代码气味”类型的质量问题错误地影响了“可靠性等级”。

* 由于不支持通配符域，因此UI将禁止用户提交通配符域。

* 当在午夜和凌晨1点之间启动管道执行时，Cloud Manager生成的伪像版本不能保证大于前一天创建的版本。

* 在沙箱项目设置过程中，成功创建包含示例代码的项目后，“管理Git”将显示为“概述”页面中主题卡中的链接。

### 发布日期 {#release-date-cm-april}

AEM中Cloud Manager作为Cloud Service 2021.4.0的发布日期为2021年4月8日。

### 新增功能 {#what-is-new-april}

* 对“添加”和“编辑”项目工作流的UI更新，使其更直观。

* 具有必需权限的用户现在可以通过UI提交商务端点。

* 环境变量现在可以作用于特定服务（创作或发布）。 需要AEM版本`2021.03.5104.20210328T185548Z`或更高版本。

* 即使未配置管线，**管理Git**&#x200B;按钮也会显示在管线卡上。

* Cloud Manager使用的AEM项目原型版本已更新为版本27。

* 云管理器创建的Adobe I/O开发人员控制台中的项目不再可以无意中编辑或删除。

* 当用户添加新环境时，他们将收到通知，创建环境后，无法将其移动到其他区域。

* 环境变量现在可以作用于特定服务（创作或发布）。 需要AEM 2021.03.5104.20210328T185548Z或更高版本。

* 澄清了删除环境时启动管线时的错误消息。

* 现在，规则`CQBP-84--dependencies`中不包括Eclipse项目提供的OSGi捆绑包。

### 错误修复 {#bug-fixes-cm-april}

* 编辑管道的体验审核页面时，以斜杠`( / )`开头的输入路径将不再导致步骤卡在挂起状态中。

* 创建新的生产管道时，如果用户未添加内容审核覆盖，则不会审核默认主页。

* `CloudServiceIncompatibleWorkflowProcess`的问题在可下载的问题CSV文件中严重性不正确。

* `Runmode`检查在非文件夹节点上产生误报。

## 最佳实践分析器{#best-practices-analyzer}

### 发布日期 {#release-date-bpa}

Best Practices Analyzer v2.1.12的发布日期为2021年4月12日。

### 错误修复 {#bug-fixes-bpa-april}

* 重复行在报告的BPA中。 此问题已解决。
* AEM版本6.4.2上的BPA UI正在引发JS错误，该错误正在禁用“生成报告”按钮。 已修复

