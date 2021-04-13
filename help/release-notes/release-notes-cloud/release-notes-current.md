---
title: 作为Cloud Service的 [!DNL Adobe Experience Manager] 当前发行说明。
description: 作为Cloud Service的 [!DNL Adobe Experience Manager] 当前发行说明。
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
translation-type: tm+mt
source-git-commit: b412ec6b554684b9b41fe6c8991124bc76e200af
workflow-type: tm+mt
source-wordcount: '1588'
ht-degree: 3%

---

# [!DNL Adobe Experience Manager]作为Cloud Service{#release-notes}的当前发行说明

以下部分概述了作为Cloud Service的[!DNL Experience Manager]当前（最新）版本的一般发行说明。

>[!NOTE]
>您可以从此处导航到先前版本的发行说明；例如，2020年、2021年等年。

>[!NOTE]
>
>请参阅[最近文档更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html)，了解与版本不直接相关的文档更新的详细信息。

## 发布日期 {#release-date}

[!DNL Adobe Experience Manager]作为Cloud Service2021.3.0的发布日期为2021年3月25日。
以下版本(2021.4.0)将于2021年4月29日发布。

## [!DNL Adobe Experience Manager Sites] 作为Cloud Service  {#sites}

* [现在，可以通过简单配置在项目](/help/sites-cloud/authoring/features/enable-pwa.md) 级别启用网站的渐进式Web应用程序(PWA)版本。
* 内容片段模型扩展 — 现在可以将多行文本数据类型定义为多字段列表。
* 内容片段编辑器UX增强 — 嵌套子片段现在以痕迹导航显示，并改进了发布、保存和保存退出操作的视图

## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets] {#what-is-new-assets}中的新增功能

<!-- TBD: refine this list of features and enh. for Feb release.

Customers using the Connected Assets feature can now easily view and track assets used on remote Sites instances. This affords customers a complete view of being used across all Sites powered pages, allowing for better tracking, management, and brand consistency.  

Indicators for expired, approved, and rejected statuses now available for assets in Column view.

Ability to select a root path. select if a minimum number of tags is required. 

Add a Boolean or radio widget type to metadata schema setup. -->

* [!DNL Experience Manager] 扩展了“已连接资产”功能，支持在支 [!DNL Dynamic Media] 持的核心组件中使用图像。请参阅[使用连接的资产](/help/assets/use-assets-across-connected-assets-instances.md)。
* Experience Manager管理员可以在特定日期或时间计划批量资产摄取。 此外，管理员可以根据日期和时间计划循环摄取。 请参阅[批量资产摄取](/help/assets/add-assets.md#asset-bulk-ingestor)。

### [!DNL Assets] {#bug-fixes-assets}中的错误修复

* 尝试下载多个受版权管理的资产时，不会显示版权页面。 (CQ-4314403)
* 选择编辑INDD文件时，分辨率会意外更改。 (CQ-4317376)
* 在PDF演绎版中，只有InDesign模板的最后一页。 (CQ-4317305)
* 当选取器是复杂元数据模式的一部分时，打开标记选取器需要很长时间。 (CQ-4316426)
* 上传的资产的文件名与现有资产文件名相同时，不会显示名称冲突对话框以提示用户创建版本。 (CQ-4315424)
* 文件夹元数据属性可从文件夹的“属性”页面的弹出菜单中设置和保存。 选择内容保存在存储库中时，在再次打开文件夹元数据属性时不显示。 (CQ-4314429)
* 文件名包含空格或特殊字符的资产可通过浏览器上传。 (CQ-4318381)

## [!DNL Adobe Experience Manager Forms] a  [!DNL Cloud Service] {#forms}

AEM Forms多年来一直帮助许多组织提供出色的入职和注册体验。 这些体验帮助组织将销售线索转换为销售线索、处理捕获的客户数据、根据受众用户档案提供响应式体验等。 现在，AEM Forms可作为云服务提供。

您可以使用[AEM Forms作为Cloud Service](https://experienceleague.corp.adobe.com/docs/experience-manager-forms-cloud-service/forms/home.html)创建数字表单、将表单连接到现有数据源、将表单与Adobe Sign集成以向表单添加电子签名、生成记录文档(DoR)以将提交的表单存档为PDF文件。 该服务还可以将您现有的PDF forms转换为数字表单。 除标准AEM Forms功能外，该服务还优惠了几个云本机功能，如自动扩展、升级零停机和云本机开发环境。 阅读[此博客文章](https://blog.adobe.com/en/publish/2021/03/11/experience-manager-forms-as-a-cloud-service.html)，了解AEM Forms作为Cloud Service的功能和特性。

您可以联系Adobe代表进行演示或注册服务。

## Adobe Experience Manager Commerce as aCloud Service{#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* 支持Magento 2.4.2

* 现在可以在任何内容页面上使用和配置产品详细信息组件

* 已发布CIF委内瑞拉参考站点 — 2021.03.25，其中包括最新的CIF核心组件版本v1.9.0。有关更多详细信息，请参阅[CIF委内瑞拉参考站点](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.03.25)。

* 已发布CIF核心组件v1.9.0。有关更多详细信息，请参阅[CIF核心组件](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.9.0)。


## Cloud Manager {#cloud-manager}

本节概述AEM中作为Cloud Service 2021.4.0和2021.3.0的Cloud Manager发行说明。

### 发布日期 {#release-date-cm-april}

AEM中Cloud Manager作为Cloud Service 2021.4.0的发布日期为2021年4月8日。
下一版本计划于2021年5月06日发布。

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


### 发布日期 {#release-date-cm-march}

AEM中Cloud Manager作为Cloud Service 2021.3.0的发布日期为2021年3月11日。

### 新增功能 {#what-is-new-march}

* 拥有[IP允许列表](/help/implementing/cloud-manager/ip-allow-lists/check-ip-allow-list-status.md#pre-existing-cdn)、[SSL证书](/help/implementing/cloud-manager/managing-ssl-certifications/check-status-ssl-certificate.md#pre-existing-cdn)和[自定义域名](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md#pre-existing-cdn)预存自定义域名配置的环境的客户将看到有关其先前现有配置的消息，并将能够通过UI自助服务。

* 具有必需权限的用户现在可以编辑项目，允许他们以自助方式执行以下操作：

   * 将站点解决方案添加到包含资产的现有项目，反之亦然。
   * 将站点或资产从包含站点和资产的现有项目中删除。
   * 将第二个未使用的解决方案授权添加到现有项目或作为新项目。

* **AEM Push** Updatelabel现在将同时显示在Pipeline Executive和 *Activity* 屏幕 ** 上。

* 如果环境已休眠，但也有可用的AEM更新，则&#x200B;**已休眠**&#x200B;状态将优先于&#x200B;**可用更新**。

* 现在，用户在导航至Unified Shell的“用户用户档案”图标（右上方）后，通过选择“视图 Cloud Manager角色”选项，即可查看其Cloud Manager角色。

* 标签&#x200B;**申请批准**&#x200B;已重新标记到&#x200B;**生产批准**，以便更清晰。

* **版本**&#x200B;标签已重新标记到“生产”管线执行屏幕中的&#x200B;**Git标签**。

* 当重要量度未达到定义的阈值时定义行为的标签已重新标记，以反映其真实行为：**取消立即**&#x200B;和&#x200B;**立即批准**。

* 类和方法弃用列表已根据AEM Cloud Service SDK的`2021.3.4997.20210303T022849Z-210225`版本进行更新。

* Cloud Manager生产管道现在将包含[自定义UI测试](/help/implementing/cloud-manager/functional-testing.md#custom-ui-testing)功能。

### 错误修复 {#bug-fixes-cm-march}

* 在AEM推送升级期间，在某些情况下跳过了包版本控制。

* 在将包嵌入到其他包中时，未正确发现某些质量问题。

* 在模糊情况下，打开“添加项目”对话框时生成的默认项目名称可能是现有项目名称的重复。

* 有时，如果用户在启动管道后立即从管道执行页面导航离开，将显示一条错误消息，指出操作失败，尽管实际执行会开始。

* 当客户生成导致包无效时，不必要地重新启动生成步骤。

* 有时，即使未部署IP，用户也会在IP旁看到允许列表绿色的“活动”状态。

* 所有现有生产管道将通过体验审核步骤自动启用。

## 内容传输工具 {#content-transfer-tool}

### 发布日期 {#release-date-ctt}

内容传输工具v1.3.4的发布日期为2021年3月19日。

### 错误修复 {#bug-fixes-ctt}

* CTT正在跳过名称相同但名称带有连字符的文件夹中的内容。 此问题已解决。

### 发布日期 {#release-date-ctt-march}

内容传输工具v1.3.0的发布日期为2021年3月04日。

### 内容传输工具{#what-is-new-ctt-march}的新增功能

* CTT现在安装到`/apps`，而不是`/libs`某些页面的浏览器书签可能不再有效。
* 安装CTT后，用户将必须浏览其他级别才能进入“内容传输”页面。 有关详细信息，请参阅[使用内容传输工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html)。

### 错误修复 {#bug-fixes-ctt-march}

* 从特定路径迁移内容时，CTT正在调用不相关的资源。 已修复

## 最佳实践分析器{#best-practices-analyzer}

### 发布日期 {#release-date-bpa}

Best Practices Analyzer v2.1.12的发布日期为2021年4月12日。

### 错误修复 {#bug-fixes-bpa-april}

* 重复行在报告的BPA中。 此问题已解决。
* AEM版本6.4.2上的BPA UI正在引发JS错误，该错误正在禁用“生成报告”按钮。 已修复


## 代码重构工具 {#code-refactoring-tools}

### 代码重构工具{#what-is-new-crt}的新增功能

* Repository Modernizer的新增功能和增强功能。 请参阅[GitHub资源：最新版本的存储库Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer)。
   * 将OSGi配置（RepoInit配置除外）标准化为首选.cfg.json格式。
   * 将OSGi配置文件夹重命名为指定格式。
   * 生成ui.apps.structure项目。
   * 创建分析模块。

* Dispatcher Converter的新增功能和增强功能。 请参阅[GitHub资源：调度程序转换器](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter)
   * 为不同包含创建单独文件，而不是在内容中排列。
   * 能够同时处理vhosts的文件夹路径和vhost文件的路径。
   * 生成客户配置范围在600个以上的农场文件。
