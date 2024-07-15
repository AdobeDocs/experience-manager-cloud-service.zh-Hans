---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 2021.4.0 版的发行说明。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 2021.4.0 版的发行说明。'
exl-id: 775332b5-24ce-430e-97a2-6eeb80877c64
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '1545'
ht-degree: 44%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 的最新发行说明 {#release-notes}

以下部分概述了当前（最新）版本的 [!DNL Adobe Experience Manager] as a Cloud Service 的一般发行说明。

>[!NOTE]
>在此处，您可以导航到早期版本的发行说明；例如，2020版、2021版等的发行说明。

>[!NOTE]
>
>有关未与版本直接相关的文档更新的详细信息，请参阅[最新文档更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html)。

## 发布日期 {#release-date}

[!DNL Adobe Experience Manager]as a Cloud Service2021.4.0的发布日期是2021年5月6日。
下一个版本(2021.5.0)将于2021年5月27日发布。

## AEM as a Cloud Service Foundation{#aem-as-a-cloud-service-foundation}

### 新增功能 {#what-is-new-foundation}

* [Publish内容树工作流](/help/operations/replication.md#publish-content-tree-workflow) — 新的工作流模型和步骤在发布层次结构较深的内容时提高了性能。

## [!DNL Adobe Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### [!DNL Sites] 的新增功能 {#what-is-new-sites}

* GraphQL端点 — 现在可以为单个AEM Sites配置启用AEM GraphQL API，并使用新的GraphQL Console UI为这些配置创建自定义GraphQL端点。 通过该用户界面，还可管理GraphQL端点。

* 内容模型增强了日期和时间数据类型 — 现在可配置日期和时间数据类型，以便可创作只有日期、只有时间或有日期和时间的信息。

* 内容模型增强了标记数据类型 — 现在可以配置标记数据类型，以便可创作单个或多个标记。

* 内容模型、新选项卡占位符数据类型 — 新的选项卡占位符数据类型允许将数据类型分组到在内容片段编辑器中的选项卡下呈现的部分。

### [!DNL Sites] 中的错误修复 {#bug-fixes-sites}

* 内容片段 — 移动内容片段或文件夹现在会更新片段中的嵌套引用(CQ-4320815)

* GraphQL — 持久查询现在支持特定于AEM Sites配置的用户定义端点(CQ-4315928)

## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets] 的新增功能 {#what-is-new-assets}

* [!DNL Experience Manager]不存档下载原始文件的单个资源下载。 此增强可加快下载速度。

* 现在，通过链接共享选项下载资产时，您可以选择下载或不下载演绎版。 以前，会下载所有资源演绎版。

* 管理员可以将[!DNL Experience Manager]配置为在批量引入资源后删除资源源。 请参阅[批量资源引入](/help/assets/add-assets.md#asset-bulk-ingestor)。

* 在执行运行状况检查以批量导入资源时，Experience Manager现在提供失败原因的详细信息。 请参阅[批量资源引入](/help/assets/add-assets.md#asset-bulk-ingestor)。

* 使用批量导入工具导入资源时，管理员现在可以选择在导入成功后删除源文件。 请参阅[批量资源引入](/help/assets/add-assets.md#asset-bulk-ingestor)。

* 在编辑元数据架构时，新的根路径选择器字段允许管理员快速轻松地作出选择，从而减少配置时间。

* 在编辑元数据架构时，会添加一种数据类型，以在元数据编辑器中提供自由格式文本区域。 用户可以使用此文本区域输入自由格式文本作为资源的元数据。 请参阅[元数据架构编辑器](/help/assets/metadata-schemas.md)。

* 可以使用CSV文件批量导入许多资源的元数据，也可以将元数据导出到CSV文件。 默认日期格式现在为`yyyy-MM-dd'T'HH:mm:ss.SSSXXX`。 用户可以通过更新列标题来使用不同的格式。 例如，在CSV文件中添加`Date: DateFormat: yyyy-MM-dd'T'HH:mm:ssXXX`作为列标题而非`Date`一词。

* 在列视图中浏览资源时，有一个视觉标志显示每个资源的已批准或已拒绝状态。

* 在列视图中浏览资源时，为已过期的资源显示一个视觉标志。

### [!DNL Assets] 中的错误修复 {#bug-fixes-assets}

* 当尝试移动多个资源或文件夹时，控制台中会记录一个错误，并且移动操作未完成。 如果无法更新标题，移动操作失败。 (CQ-4322080)

* 可根据规则隐藏元数据字段，以便在满足预定义条件时，该元数据不是必需的。 但是，此类隐藏的元数据字段显示为必填字段。 (CQ-4321285)

* 由于日期格式不正确，批量元数据导入失败。 (CQ-4319014)

* 在属性页面中选择更新元数据时，如果架构提供了许多选项，则界面响应缓慢。 (CQ-4318538)

* 在单行文本字段中更新和保存元数据值时，即使下拉列表菜单上禁用编辑，下拉列表菜单中的值也会被删除。 (CQ-4317077)

* 您可以将省略号用作注释来查看资产。 使用小椭圆时，椭圆与打印版本中的注释编号重叠。 (CQ-4316792)

* 在搜索资产后从搜索结果中选择资产时，不会显示快速发布选项。 (CQ-4317748)

## [!DNL Adobe Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] 的新增功能 {#what-is-new-forms}

* **在支持 Adobe Sign 的自适应表单中使用 Government ID 身份验证方法**

  通过先进的机器学习算法，Adobe Sign 的 Government ID 流程让世界各地的公司均可确保高质量地验证其收件人的身份。现在，您可以在支持 Adobe Sign 的自适应表单中使用 Government ID 身份验证方法。

  Government ID 是一种高级的身份验证方法，它会指示收件人[上传政府颁发的身份证明文件（驾照、身份证、护照）的图像](https://helpx.adobe.com/cn/sign/using/adobesign-authentication-government-id.html)，然后评估该证明文件以确保真实有效。

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
* 添加将PDF文件移动到放置在AEM Forms UI上的文件夹的功能。

## Adobe Experience Manager Commerceas a Cloud Service {#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* 支持类别UID — 这为将字符串用于类别ID的系统解锁了第三方商业集成

* 适用于PWA Studio的AEM扩展，包括 集成示例

* 新增扩展WCM导航核心组件的CIF导航核心组件

* AEM店面中暂存的目录数据的视觉标志

* Commerce端点现在可通过Cloud Manager UI进行配置

### 错误修复 {#bug-fixes-commerce}

* 根类别字段未显示在类别页面的页面属性中的商务选项卡下

## Cloud Manager {#cloud-manager}

此部分概述了 AEM as a Cloud Service 2021.4.0 中的 Cloud Manager 的发行说明。

### 发布日期 {#release-date-cm-april}

AEM as a Cloud Service 2021.4.0 中的 Cloud Manager 的发布日期是 2021 年 4 月 8 日。
下一个版本计划于 2021 年 06 月 06 日发布。

### 新增功能 {#what-is-new-april}

* “添加和编辑程序”工作流的 UI 进行了更新，变得更加直观。

* 具有必需权限的用户现在可以通过 UI 提交商务端点。

* 现在可以将环境变量的作用域限定为特定服务（创作或发布）。要求 AEM 版本 `2021.03.5104.20210328T185548Z` 或更高版本。

* 即使未配置任何管道，“管道”卡上也会显示&#x200B;**“管理 Git”**&#x200B;按钮。

* Cloud Manager 使用的 AEM 项目原型的版本已更新到版本 27。

* Adobe I/O Developer Console 中由 Cloud Manager 创建的项目不会再被无意中编辑或删除。

* 当用户添加新环境时，将会通知他们，环境在创建后无法移动到其他区域。

* 现在可以将环境变量的作用域限定为特定服务（创作或发布）。 要求 AEM 版本 2021.03.5104.20210328T185548Z 或更高版本。

* 澄清了删除环境后启动管道时的错误消息。

* Eclipse 项目提供的 OSGi 捆绑包现已从规则 `CQBP-84--dependencies` 中排除。

### 错误修复 {#bug-fixes-cm-april}

* 编辑管道的体验审核页面时，以斜杠 `( / )` 开头的输入路径将不再会使步骤停留在挂起状态。

* 创建新的生产管道时，如果用户未添加内容审核覆盖，则默认主页未审核。

* `CloudServiceIncompatibleWorkflowProcess` 的问题在可下载的问题 CSV 文件中的严重性不正确。

* `Runmode` 检查在非文件夹节点上产生误报。

## Best Practices Analyzer {#best-practices-analyzer}

### 发布日期 {#release-date-bpa}

Best Practices Analyzer v2.1.12的发布日期是2021年4月12日。

### 错误修复 {#bug-fixes-bpa-april}

* 在BPA报告中发现重复行。 此问题已得到修复。
* AEM版本6.4.2上的BPA UI引发了JS错误，该错误会禁用“生成报表”按钮。 此问题已得到修复
