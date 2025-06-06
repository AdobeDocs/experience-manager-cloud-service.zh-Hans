---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 2021.3.0 版的发行说明。'
description: "[!DNL Adobe Experience Manager]个2021.3.0版as a Cloud Service发行说明。"
exl-id: 0c07364c-ba25-4081-8e35-3c1c84ed556f
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '1271'
ht-degree: 34%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 的最新发行说明 {#release-notes}

以下部分概述了当前（最新）版本的 [!DNL Experience Manager] as a Cloud Service 的一般发行说明。

>[!NOTE]
>在此处，您可以导航到早期版本的发行说明；例如，2020版、2021版等的发行说明。

>[!NOTE]
>
>有关未与版本直接相关的文档更新的详细信息，请参阅[最新文档更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=zh-Hans)。

## 发布日期 {#release-date}

[!DNL Adobe Experience Manager]as a Cloud Service2021.3.0的发布日期是2021年3月25日。
下一个版本(2021.4.0)将于2021年4月29日发布。

## [!DNL Adobe Experience Manager Sites]个as a Cloud Service {#sites}

* [现在可以通过简单的配置在项目级别启用网站的渐进式Web应用程序(PWA)版本](/help/sites-cloud/authoring/sites-console/enable-pwa.md)。
* 内容片段模型扩展 — 现在可以将多行文本数据类型定义为多字段列表。
* 内容片段编辑器UX增强功能 — 嵌套的子片段现在显示在痕迹导航中，并改进了有关发布、保存以及保存并退出操作的视图

## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets] 的新增功能 {#what-is-new-assets}

<!-- TBD: refine this list of features and enh. for Feb release.

Customers using the Connected Assets feature can now easily view and track assets used on remote Sites instances. This affords customers a complete view of being used across all Sites powered pages, allowing for better tracking, management, and brand consistency.  

Indicators for expired, approved, and rejected statuses now available for assets in Column view.

Ability to select a root path. select if a minimum number of tags is required. 

Add a Boolean or radio widget type to metadata schema setup. -->

* [!DNL Experience Manager]扩展了连接的Assets功能，以支持在支持的核心组件中使用[!DNL Dynamic Media]映像。 请参阅[使用连接的Assets](/help/assets/use-assets-across-connected-assets-instances.md)。
* Experience Manager管理员可以安排在特定日期或时间进行批量资源引入。 此外，管理员可以根据日期和时间安排重复引入。 请参阅[批量资源引入](/help/assets/add-assets.md#asset-bulk-ingestor)。

### [!DNL Assets] 中的错误修复 {#bug-fixes-assets}

* 尝试下载多个权限管理的资产时，不显示版权页面。 (CQ-4314403)
* 当选择编辑INDD文件时，分辨率意外更改。 (CQ-4317376)
* PDF呈现版本中仅存在InDesign模板的最后一页。 (CQ-4317305)
* 当标记选取器是复杂元数据架构的一部分时，该选取器需要很长时间才能打开。 (CQ-4316426)
* 上传与现有资源具有相同文件名的资源时，不会显示名称冲突对话框以提示用户创建版本。 (CQ-4315424)
* 可以从文件夹“属性”页面的弹出菜单中设置和保存文件夹元数据属性。 所选内容保存在存储库中时，再次打开文件夹元数据属性时不会显示该内容。 (CQ-4314429)
* 文件名中包含空格或特殊字符的Assets使用浏览器上传。 (CQ-4318381)

## [!DNL Adobe Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

多年以来，AEM Forms已帮助众多组织创造了优异的入职和注册体验。 这些体验已帮助组织将潜在客户转化为销售、处理捕获的客户数据、根据受众个人资料提供响应式体验等等。 现在，AEM Forms以Cloud Service的形式提供。

您可以使用[AEM Formsas a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/home.html?lang=zh-Hans)创建数字表单、将表单连接到现有数据源、将表单与Adobe Sign集成以将电子签名添加到表单、生成记录文档(DoR)以将提交的表单存档为PDF文件。 该服务还可将您现有的PDF forms转换为数字表单。 除了标准的AEM Forms功能外，该服务还提供若干云原生功能，如自动扩展、升级零停机以及云原生开发环境。

您可以联系Adobe代表以索取演示或注册该服务。

## Adobe Experience Manager Commerceas a Cloud Service {#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* 支持Adobe Commerce 2.4.2

* 现在可以在任何内容页面上使用和配置产品详细信息组件

* 发布了CIF Venia参考网站 — 2021.03.25，其中包括最新的CIF核心组件版本v1.9.0。有关详细信息，请参阅[CIF Venia引用站点](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.03.25)。

* 已发布CIF核心组件v1.9.0。有关详细信息，请参阅[CIF核心组件](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.9.0)。


## Cloud Manager {#cloud-manager}

此部分概述了 AEM as a Cloud Service 2021.3.0 中的 Cloud Manager 的发行说明。

## 发布日期 {#release-date-cm-march}

AEM as a Cloud Service 2021.3.0中的Cloud Manager的发布日期是2021年3月11日。
下一个版本计划于2021年4月8日发布。

### 新增功能 {#what-is-new-march}

* 如果客户的环境中已有[IP允许列表](/help/implementing/cloud-manager/ip-allow-lists/managing-ip-allow-lists.md#pre-existing-cdn)、[SSL证书](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md#pre-existing-cdn)和[自定义域名](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md#pre-existing-cdn)的自定义域名配置，则客户会看到有关其以前现有配置的消息，并可通过用户界面进行自助服务。

* 具有所需权限的用户现在可编辑计划，于是这些用户可按自助方式执行以下操作：

   * 将 Sites 解决方案添加到具有 Assets 的现有项目，反之亦然。
   * 从具有 Sites 和 Assets 的现有项目中删除 Sites 或 Assets。
   * 将另一未使用的解决方案权利添加到现有计划或添加为新计划。

* **AEM推送更新**&#x200B;标签现在将显示在&#x200B;*Pipeline Execution*&#x200B;和&#x200B;*Activity*&#x200B;屏幕上。

* 如果环境已休眠，但还有 AEM 更新可用，则&#x200B;**已休眠**&#x200B;状态优先于&#x200B;**有可用更新**&#x200B;状态。

* 用户们现在通过在导航到 Unified Shell 的“用户个人资料”图标（右上角）之后选择“查看 Cloud Manager 角色”选项，即可查看其 Cloud Manager 角色。

* 为了更加清晰明了，**申请批准**&#x200B;标签已变为&#x200B;**批准生产**。

* “生产管道执行”屏幕中的&#x200B;**版本**&#x200B;标签已变为 **Git 标签**。

* 已改变定义在重要指标不符合所定义的阈值时发生的行为的若干标签以反映其真实行为：**立即取消**&#x200B;和&#x200B;**立即批准**。

* 已根据 AEM Cloud Service SDK 的 `2021.3.4997.20210303T022849Z-210225` 版本更新了类和方法的弃用列表。

* Cloud Manager Production 管道现在将包括[自定义 UI 测试](/help/implementing/cloud-manager/functional-testing.md#custom-ui-testing)功能。

### 错误修复 {#bug-fixes-cm-march}

* 在 AEM 推送升级过程中，某些情况下跳过了包版本控制。

* 当包嵌入到其他包中时，没有正确发现一些质量问题。

* 在不明显的情况下，打开“添加程序”对话框时生成的默认程序名可能与现有程序名重复。

* 有时，如果用户在启动管道后立即离开管道执行页面，则会显示一条错误消息，说明操作失败，尽管执行实际上已开始。

* 当客户生成导致无效包时，不必要地重新启动了生成步骤。

* 有时，即使未部署配置，用户也会在 IP 允许列表旁边看到绿色的“活动”状态。

* 所有现有生产管道都会通过体验审核步骤自动启用。

## 内容转移工具 {#content-transfer-tool}

### 发布日期 {#release-date-ctt}

内容传输工具版本1.3.4的发布日期为2021年3月19日。

### 错误修复 {#bug-fixes-ctt}

* CTT从名称相同但名称中包含连字符的文件夹中跳过内容。 此问题已得到修复。

### 发布日期 {#release-date-ctt-march}

内容传输工具版本1.3.0的发布日期为2021年3月4日。

### 内容传输工具的新增功能 {#what-is-new-ctt-march}

* CTT现在安装到`/apps`，而不是`/libs`。某些页面的浏览器书签可能不再有效。
* 安装CTT后，用户必须导航到其他级别才能转到内容传输页面。 有关详细信息，请参阅[使用内容传输工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=zh-Hans)。

### 错误修复 {#bug-fixes-ctt-march}

* 从特定路径迁移内容时，CTT会拉入不相关的资源。 此问题已得到修复

## Best Practices Analyzer {#best-practices-analyzer}

### 发布日期 {#release-date-bpa}

Best Practices Analyzer v2.1.8的发布日期是2021年3月22日。

### Best Practices Analyzer的新增功能 {#what-is-new-bpa}

* 能够从用户界面中的BPA报告和导出为CSV文件的报告中过滤掉ACS Commons调查结果。

## 代码重构工具 {#code-refactoring-tools}

### 代码重构工具的新增功能 {#what-is-new-crt}

* Repository Modernizer的新增功能和增强功能。 有关最新版本，请参阅[GitHub资源：存储库现代化器](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer)。
   * 将OSGi配置（RepoInit配置除外）标准化为首选的.cfg.json格式。
   * 将OSGi配置文件夹重命名为指定的格式。
   * 生成ui.apps.structure项目。
   * 创建分析模块。

* Dispatcher Converter的新增功能和增强功能。 查看[GitHub资源：Dispatcher Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter)
   * 为不同的包含内容创建单独的文件，而不是在内容中置入。
   * 能够处理vhosts的文件夹路径和vhost文件的路径。
   * 生成具有600个及以上的大型客户配置的场文件。
