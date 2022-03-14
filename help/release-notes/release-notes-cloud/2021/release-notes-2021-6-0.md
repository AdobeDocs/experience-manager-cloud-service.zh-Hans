---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2021.6.0 版的发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2021.6.0 版的发行说明。'
exl-id: 2c72973b-5a51-4744-bf88-50da0013ba31
source-git-commit: 96a0dacf69f6f9c5744f224d1a48b2afa11fb09e
workflow-type: tm+mt
source-wordcount: '1440'
ht-degree: 25%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 的最新发行说明 {#release-notes}

以下部分概述了当前（最新）版本的 [!DNL Experience Manager] as a Cloud Service 的一般发行说明。

>[!NOTE]
>
>从此处，您可以导航到以前版本的发行说明；例如，2020年、2021年等年份的客户。

>[!NOTE]
>
>有关未与版本直接相关的文档更新的详细信息，请参阅[最新文档更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=zh-Hans)。

## 发布日期 {#release-date}

的发行日期 [!DNL Adobe Experience Manager] as a Cloud Service2021.6.0是2021年6月28日。
以下版本(2021.7.0)将于2021年7月29日发布。

## 发布视频 {#release-video}

请查看 [2021年6月版概述](https://video.tv.adobe.com/v/334296) 视频，了解添加的功能摘要。

## AEM as a Cloud Service的XML Documentation {#xml-documentation}

### 新增功能 {#what-is-new-xml-documentation}

* AEMas a Cloud Service的XML Documentation现在为GA。
* 这将允许现有AEM Cloud Service客户购买XML Documentation添加程序，以便跨多个渠道(包括AEM站点)导入、创建、管理和交付技术内容

## Cloud Manager {#cloud-manager}

本部分概述了AEM 2021.6.0和2021.5.0版中Cloud Manager的发行说明。

### 发布日期 {#release-date-june-cm}

AEM 2021.6.0版中Cloud Manager的发布日期是2021年6月10日。
下一版本计划于2021年7月15日发布。

### 新增功能 {#what-is-new-junecm}

* 预览服务将以滚动方式部署到所有程序。 当客户的计划启用了预览服务后，系统会在产品中通知客户。 请参阅 [访问预览服务](/help/implementing/cloud-manager/manage-environments.md#access-preview-service) 以了解更多详细信息。

* 现在，在生成步骤期间下载的Maven依赖项将在管道执行之间缓存。 未来几周，将为客户启用此功能。

* 现在可以通过编辑程序对话框编辑程序的名称。

* 在项目创建期间和在通过管理Git工作流的默认推送命令中使用的默认分支名称已更改为 `main`.

* 在UI中编辑项目体验已刷新。

* 质量规则 `ImmutableMutableMixCheck` 已更新以进行分类 `/oak:index` 节点不可变。

* 质量规则 `CQBP-84` 和 `CQBP-84--dependencies` 已合并到单个规则中。 作为此整合的一部分，对依赖项的扫描可更准确地识别部署到AEM运行时的第三方依赖项中的问题。

* 为避免混淆，“环境详细信息”页面上的“发布AEM”和“发布Dispatcher”区段行已进行合并。

   ![](/help/implementing/cloud-manager/release-notes-cloud-manager/assets/aem-dispatcher.png)

* 添加了新代码质量规则以验证 `damAssetLucene` 索引。 请参阅 [自定义DAM资产Lucene Oak索引](/help/implementing/cloud-manager/custom-code-quality-rules.md#oakpal-damAssetLucene-sanity-check) 以了解更多详细信息。

* “环境详细信息”页面现在将显示发布和预览服务的多个域名（如果适用）。 请参阅 [环境详细信息](/help/implementing/cloud-manager/manage-environments.md#viewing-environment) 以了解更多详细信息。

### 错误修复 {#bug-fixes-junecm}

* 未正确解析根元素名称后包含换行符的JCR节点定义。

* 列表存储库API不会过滤已删除的存储库。

* 为计划步骤提供无效值时，显示错误消息。

* 有时，用户可能会看到绿色 *活动* IP允许列表旁边的状态，即使未部署该配置也是如此。

* 某些程序编辑序列可能会导致无法创建或编辑生产管道。

* 某些程序编辑序列可能会导致 **概述** 页面显示一条误导性消息以重新执行程序设置。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets] 中的新增功能 {#ga-features-assets}

* “内容自动化”功能允许 [!DNL Experience Manager Assets] 利用 [!DNL Adobe Creative Cloud] 用于大规模自动化资产生产的API。 它可显着减少创建同一资产变体所花费的时间和所需的迭代次数，从而提高内容速度。 该功能不需要任何代码，也可从DAM中使用。
* [!DNL Adobe Asset Link] v3.0 for [!DNL Adobe Photoshop], [!DNL Adobe Illustrator]和 [!DNL Adobe InDesign] 和 [!DNL Adobe Asset Link] v2.0( [!DNL Adobe XD] 已发布。 它提供：

   * 支持 [!DNL Assets Essentials].
   * 能够自动连接到 [!DNL Experience Manager] as a [!DNL Cloud Service] 或 [!DNL Assets Essentials].

<!-- TBD: Checking with PMs if AAE release should be mentioned here.
-->

### 的新增功能 [!DNL Assets] 预发行渠道 {#beta-features-assets}

* 视图设置经过增强，允许用户选择默认视图和默认排序参数。
* Linkshare下载功能使用异步下载来提高下载速度。
* 用户可以根据属性谓词搜索和筛选文件夹。
* [!DNL Experience Manager Assets] 嵌入由提供支持的PDF查看器 [!DNL Adobe Document Cloud] 以预览支持的文档。 此功能允许用户预览PDF和其他多页文件，而无需进行任何复杂的处理。 这改进了与的功能对等性 [!DNL Experience Manager] 6.5。

### [!DNL Assets] 中修复的错误 {#bugs-fixed-assets}

* 在向子文件夹中添加所有者时， [!DNL Assets] 还会添加与父文件夹所有者相同的用户。 (CQ-4323737)
* 在将资产添加到收藏集时，如果用户对收藏集搜索应用过滤器，则用户将无法在列表视图中查看收藏集。 (CQ-4323181)
* 在搜索文件和文件夹时，如果用户应用过滤器并选择 [!UICONTROL 文件和文件夹]，则仅显示文件，而不显示文件夹。 (CQ-4319543)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### [!DNL Sites] 中的新增功能 {#ga-features-sites}

* “发布到预览层”现在在站点管理UI中显示为页面状态
* 现在，发布到预览层会在操作结束时显示预览URL，并在页面属性中保留该URL以供日后参考

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] 的新增功能 {#what-is-new-forms}

* 添加了在 AEM 收件箱中筛选自定义列的功能。
* 添加了使用主题编辑器和自适应表单编辑器的样式层来设置验证码组件样式的功能。
* 提高了自动检测源 PDF 表单中的逻辑部分并将其转换为相应的自适应表单面板的速度和准确性。
* 添加了将 PDF 或 XDP 文件从一个文件夹移动到另一个文件夹的移动操作。

### [!DNL Forms] 的 Beta 版功能 {#what-is-new-forms-prerelease}

* **[!DNL AEM Forms as a Cloud Service - Communications]**：通信 API 可帮助您组合 XDP 模板和 XML 数据以生成各种格式的打印文档。该服务允许您以同步模式生成文档。API 使您能够创建应用程序，这些应用程序允许您：
   * 使用 XML 数据填充模板文件来生成最终表单文档。
   * 生成各种格式的输出表单，包括非交互式 PDF 打印流。
   * 利用 XFA 表单 PDF 和 Adobe Acrobat 表单 (AcroForm) 生成打印版 PDF。

* **变量数据外部化程序**：您可以将 AEM Workflow 变量的数据保存在由组织管理的外部存储系统上。

您可以将电子邮件发送到 [!DNL formscsbeta@adobe.com] 以注册 Beta 项目。

### [!DNL Forms] 中修复的错误 {#forms-bugs-fixed}

* 在通过表单数据模型 (FDM) 向后端服务提交数据之前验证字段时，验证成功，但表单数据模型服务无法调用后期验证。
* 在从 Apple iOS 设备提交包含标准 HTML 上传字段的表单时，有时不会发送文件内容，而在另一端会收到一个 0 字节的文件。这是Apple iOS中的已知问题。 [FB9117687](https://feedbackassistant.apple.com/feedback/9117687)

## [!DNL Experience Manager Screens] as a [!DNL Cloud Service] {#screens}

本部分概述了AEM Screens as a Cloud Service的发行说明。

### 发布日期 {#release-date-june-screens}

AEM Screensas a Cloud Service的发布日期是2021年6月24日。

### 新增功能 {#what-is-new-screens-june}

>[!NOTE]
>请参阅 [AEM Screensas a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/home.html?lang=en) 有关成功安装、配置和运行Screensas a Cloud Service所需的基础知识的指南，并链接到详细概念技术文档。

* 批量设备注册管理意味着可以更快、更高效地配置大量播放器设备。

* 改进了每个设备、显示和渠道清单视图的搜索和过滤选项。

* 设备健康快照通过提供关键状态一目了然来节省时间。

* 对象详细信息页面提供了项目中每个对象最相关信息的摘要。

## CIF 加载项 {#cloud-services-cif}

### 新增功能 {#what-is-new-cif}

* 内容片段的新CIF产品和类别引用数据类型(包括 产品/类别选取器UI支持)
* 新的商务内容片段核心组件
* AEM后端支持的全文商务搜索
* 商务核心组件支持Adobe Commerce Sensei Recs数据收集
* 改进了类别页面的SEO友好URL
* 支持每个站点/配置的自定义HTTP标头

## 内容传输工具 {#content-transfer-tool}

### 发布日期 {#release-date-ctt-latest}

内容传输工具v1.5.4的发布日期是2021年6月28日。

### 新增功能 {#what-is-new-ctt-latest}

* 支持可选 [预拷贝](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en) 添加了要与CTT一起使用的步骤。 当将源AEM实例配置为使用Amazon S3或Azure Blob Storage数据存储时，可以使用预复制步骤显着加快内容传输活动的提取和摄取阶段。

* 向CTT添加了护栏，以防止用户在摄取阶段期间数据到达关键点时停止摄取，并可能损坏数据。

* 提取日志更具描述性，可帮助进行疑难解答。

* 在UI中添加了更具描述性的摄取状态消息。

### 错误修复 {#bug-fixes-ctt-latest}

* 在创作实例上停止摄取时，UI会在发布实例上覆盖之前完成的摄取到 `STOPPED` 从 `FINISHED`. 此问题已得到修复。

## Best Practices Analyzer {#best-practices-analyzer}

### 发布日期 {#release-date-bpa}

Best Practices Analyzer v2.1.16的发布日期是2021年6月30日。

### 新增功能 {#what-is-new-bpa-latest}

* 能够检测并报告文件夹下缺少的子节点 `/content/dam`.

* 能够检测并报告所使用的最佳实践分析器版本。

### 错误修复 {#bug-fixes-bpa-latest}

* 修复了与不支持的存储库结构(URS)相关的日志记录错误。
