---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2021.3.0 版的发行说明。'
description: '[!DNL Adobe Experience Manager] as a Cloud Service的2021.3.0发行说明。'
exl-id: 0c07364c-ba25-4081-8e35-3c1c84ed556f
source-git-commit: 05a412519a2d2d0cba0a36c658b8fed95e59a0f7
workflow-type: tm+mt
source-wordcount: '1319'
ht-degree: 9%

---

# [!DNL Adobe Experience Manager]as a Cloud Service 的最新发行说明 {#release-notes}

以下部分概述了当前（最新）版本的 [!DNL Experience Manager] as a Cloud Service 的一般发行说明。

>[!NOTE]
>从此处，您可以导航到以前版本的发行说明；例如，2020年、2021年等年份的客户。

>[!NOTE]
>
>有关未与版本直接相关的文档更新的详细信息，请参阅[最新文档更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=zh-Hans)。

## 发布日期 {#release-date}

的发行日期 [!DNL Adobe Experience Manager] as a Cloud Service2021.3.0是2021年3月25日。
以下版本(2021.4.0)将于2021年4月29日发布。

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

* [网站的渐进式Web应用程序(PWA)版本](/help/sites-cloud/authoring/features/enable-pwa.md) 现在可以通过简单配置在项目级别启用。
* 内容片段模型扩展 — 现在，可以将多行文本数据类型定义为多字段列表。
* 内容片段编辑器UX增强功能 — 嵌套的子片段现在显示在痕迹导航中，并改进了发布、保存和保存&amp;退出操作的视图

## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets] 的新增功能 {#what-is-new-assets}

<!-- TBD: refine this list of features and enh. for Feb release.

Customers using the Connected Assets feature can now easily view and track assets used on remote Sites instances. This affords customers a complete view of being used across all Sites powered pages, allowing for better tracking, management, and brand consistency.  

Indicators for expired, approved, and rejected statuses now available for assets in Column view.

Ability to select a root path. select if a minimum number of tags is required. 

Add a Boolean or radio widget type to metadata schema setup. -->

* [!DNL Experience Manager] 扩展了“连接的资产”功能以支持使用 [!DNL Dynamic Media] 支持的核心组件中的图像。 请参阅 [使用连接的资产](/help/assets/use-assets-across-connected-assets-instances.md).
* Experience Manager管理员可以在特定日期或时间计划批量资产摄取。 此外，管理员还可以根据日期和时间计划定期摄取。 请参阅 [批量资产摄取](/help/assets/add-assets.md#asset-bulk-ingestor).

### [!DNL Assets] 中的错误修复 {#bug-fixes-assets}

* 尝试下载多个权限管理的资产时，不会显示版权页面。 (CQ-4314403)
* 选择编辑INDD文件时，分辨率会意外更改。 (CQ-4317376)
* “InDesign模板”的最后一页在“PDF呈现”中。 (CQ-4317305)
* 当选取器是复杂元数据架构的一部分时，标记选取器需要很长时间才能打开。 (CQ-4316426)
* 在上传文件名与现有资产相同的资产时，不会显示名称冲突对话框以提示用户创建版本。 (CQ-4315424)
* 可以从文件夹的“属性”页面的弹出菜单中设置并保存文件夹元数据属性。 选择保存在存储库中，但在再次打开文件夹元数据属性时不显示该选择。 (CQ-4314429)
* 文件名包含空格或特殊字符的资产将使用浏览器上传。 (CQ-4318381)

## [!DNL Adobe Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

AEM Forms多年来一直帮助许多组织提供出色的入门和注册体验。 这些体验帮助组织将潜在客户转化为销售，处理捕获的客户数据，根据受众配置文件提供响应式体验，等等。 现在，AEM Forms已作为云服务提供。

您可以使用 [AEM Formsas a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/home.html) 要创建数字表单、将表单连接到现有数据源、将表单与Adobe Sign集成以向表单添加电子签名、生成记录文档(DoR)以将提交的表单存档为PDF文件。 该服务还可以将您现有的PDF forms转换为数字表单。 除了标准的AEM Forms功能外，该服务还提供了若干云原生功能，如自动扩展、升级无停机以及云原生开发环境。 读取 [此博客帖子](https://blog.adobe.com/en/publish/2021/03/11/experience-manager-forms-as-a-cloud-service.html) 了解AEM Forms as a Cloud Service的功能和特性。

您可以联系Adobe代表以观看演示或注册该服务。

## Adobe Experience Manager商务as a Cloud Service {#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* 支持Adobe Commerce 2.4.2

* 现在，可以在任何内容页面上使用和配置产品详细信息组件

* 已发布CIF Venia参考网站 — 2021.03.25，其中包括最新的CIF核心组件版本v1.9.0。请参阅 [CIF Venia参考网站](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.03.25) 以了解更多详细信息。

* 已发布CIF核心组件v1.9.0。请参阅 [CIF核心组件](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.9.0) 以了解更多详细信息。


## Cloud Manager {#cloud-manager}

此部分概述了 AEM as a Cloud Service 2021.3.0 中的 Cloud Manager 的发行说明。

## 发布日期 {#release-date-cm-march}

AEM 2021.3.0版中Cloud Manager的发布日期是2021年3月11日。
下一版本计划于2021年4月8日发布。

### 新增功能 {#what-is-new-march}

* 具有以下客户： [IP允许列表](/help/implementing/cloud-manager/ip-allow-lists/check-ip-allow-list-status.md#pre-existing-cdn), [SSL证书](/help/implementing/cloud-manager/managing-ssl-certifications/check-status-ssl-certificate.md#pre-existing-cdn) 和 [自定义域名](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md#pre-existing-cdn) 将看到有关其以前现有配置的消息，并能够通过UI自助服务。

* 具有必需权限的用户现在可以编辑程序，允许他们以自助方式执行以下操作：

   * 将站点解决方案添加到包含资产的现有项目中，反之亦然。
   * 从同时具有站点和资产的现有项目中删除站点或资产。
   * 将第二个未使用的解决方案权利添加到现有项目或作为新项目。

* **AEM推送更新** 标签现在将显示为 *管道执行* 和 *活动* 屏幕。

* 如果某个环境已休眠，但同时也有一个AEM更新可用，则 **冬眠** 状态将优先于 **更新可用**.

* 现在，用户在导航到Unified Shell的“用户配置文件”图标（右上方）后，通过选择“查看Cloud Manager角色”选项，可以查看其Cloud Manager角色。

* 标签 **申请批准** 已重新标记为 **生产审批** 更清楚。

* 的 **版本** 标签已重新标记为 **Git标记** 在生产管道执行屏幕中。

* 重新标记了在重要量度未达到定义的阈值时定义行为的标签，以反映其真实行为： **立即取消** 和 **立即批准**.

* 类和方法弃用列表已根据版本进行了更新 `2021.3.4997.20210303T022849Z-210225` AEM Cloud Service SDK的ID。

* Cloud Manager生产管道现在将包括 [自定义UI测试](/help/implementing/cloud-manager/functional-testing.md#custom-ui-testing) 功能。

### 错误修复 {#bug-fixes-cm-march}

* 在AEM推送升级期间，在某些情况下跳过了包版本控制。

* 将包嵌入到其他包中时，未正确发现某些质量问题。

* 在模糊的情况下，打开“添加程序”对话框时生成的默认程序名称可能与现有程序名称重复。

* 有时，如果用户在启动管道后立即离开管道执行页面，则会显示一条错误消息，指出操作失败，尽管实际开始执行。

* 当客户生成导致无效的包时，不必要地重新启动生成步骤。

* 有时，即使未部署该配置，用户也会在IP旁允许列表看到绿色的“活动”状态。

* 所有现有的生产管道都将通过体验审核步骤自动启用。

## 内容传输工具 {#content-transfer-tool}

### 发布日期 {#release-date-ctt}

内容传输工具v1.3.4的发布日期是2021年3月19日。

### 错误修复 {#bug-fixes-ctt}

* CTT正在跳过具有相同名称但名称中带有连字符的文件夹中的内容。 此问题已修复。

### 发布日期 {#release-date-ctt-march}

内容传输工具v1.3.0的发布日期是2021年3月4日。

### 内容传输工具的新增功能 {#what-is-new-ctt-march}

* CTT现在安装到 `/apps` 而不是 `/libs` 某些页面的浏览器书签可能不再有效。
* 安装CTT后，用户必须导航到其他级别才能转到内容传输页面。 请参阅 [使用内容传输工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html) 以了解更多详细信息。

### 错误修复 {#bug-fixes-ctt-march}

* 从特定路径迁移内容时，CTT正在提取不相关的资源。 此问题已修复

## Best Practices Analyzer {#best-practices-analyzer}

### 发布日期 {#release-date-bpa}

Best Practices Analyzer v2.1.8的发布日期是2021年3月22日。

### Best Practices Analyzer的新增功能 {#what-is-new-bpa}

* 能够从UI中的BPA报表以及导出为CSV文件的报表中过滤出ACS Commons发现结果。

## 代码重构工具 {#code-refactoring-tools}

### 代码重构工具的新增功能 {#what-is-new-crt}

* Repository Modernizer的新增功能和增强功能。 请参阅 [GitHub资源：Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer) ，以了解最新版本。
   * 将OSGi配置（RepoInit配置除外）标准化为首选的.cfg.json格式。
   * 将OSGi配置文件夹重命名为指定的格式。
   * 生成ui.apps.structure项目。
   * 创建分析模块。

* Dispatcher Converter的新增功能和增强功能。 请参阅 [GitHub资源：Dispatcher Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter)
   * 为不同的包含项创建单独的文件，而不是在内容的内容内排列。
   * 能够同时处理vhosts的文件夹路径和vhost文件的路径。
   * 生成客户配置范围在600及更高的场文件。
