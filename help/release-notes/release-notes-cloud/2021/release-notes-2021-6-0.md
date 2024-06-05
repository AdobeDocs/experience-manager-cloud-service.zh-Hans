---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 2021.6.0 版的发行说明。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 2021.6.0 版的发行说明。'
exl-id: 2c72973b-5a51-4744-bf88-50da0013ba31
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '1432'
ht-degree: 47%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 的最新发行说明 {#release-notes}

以下部分概述了当前（最新）版本的 [!DNL Experience Manager] as a Cloud Service 的一般发行说明。

>[!NOTE]
>
>从此处，您可以导航到以前版本的发行说明；例如，2020版、2021版等的发行说明。

>[!NOTE]
>
>有关未与版本直接相关的文档更新的详细信息，请参阅[最新文档更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html)。

## 发布日期 {#release-date}

的发布日期 [!DNL Adobe Experience Manager] as a Cloud Service2021.6.0为2021年6月28日。
下一个版本(2021.7.0)将于2021年7月29日发布。

## 发布视频 {#release-video}

请查看 [2021年6月发行版概述](https://video.tv.adobe.com/v/334296) 视频以了解新增功能的摘要。

## 适用于AEM as a Cloud Service的XML Documentation {#xml-documentation}

### 新增功能 {#what-is-new-xml-documentation}

* 适用于AEM的XML Documentationas a Cloud Service现已正式推出。
* 这将允许现有AEM Cloud Service客户获取XML Documentation加载项，以便跨多个渠道(包括AEM站点)导入、创建、管理和交付技术内容

## Cloud Manager {#cloud-manager}

本节概述了AEMas a Cloud Service2021.6.0和2021.5.0中的Cloud Manager发行说明。

### 发布日期 {#release-date-june-cm}

AEMas a Cloud Service2021.6.0中的Cloud Manager的发布日期是2021年6月10日。
下一个版本计划于2021年7月15日发布。

### 新增功能 {#what-is-new-junecm}

* “预览”服务将以滚动方式部署到了所有程序。为预览服务启用了客户的程序后，会在产品中通知客户。有关详细信息，请参阅[访问预览服务。](/help/implementing/cloud-manager/manage-environments.md#access-preview-service)

* 现在，在管道执行之间将缓存构建步骤期间下载的 Maven 依赖项。在接下来的几周内，将为客户启用此功能。

* 现在可以通过编辑程序对话框编辑程序名称。

* 通过管理 Git 工作流在项目创建期间以及默认的推送命令中使用的默认分支名称已更改为 `main`。

* UI 中的编辑程序体验已刷新。

* 质量规则 `ImmutableMutableMixCheck` 已更新，以将 `/oak:index` 节点归类为永恒节点。

* 质量规则 `CQBP-84` 和 `CQBP-84--dependencies` 已合并为单一规则。 在此合并过程中，依赖项扫描可以更准确地识别部署到 AEM 运行时的第三方依赖项中的问题。

* 为避免混淆，合并了“环境详细信息”页面上的“发布 AEM”和“发布 Dispatcher”区段行。

  ![Dispatcher环境](/help/implementing/cloud-manager/release-notes/assets/aem-dispatcher.png)

* 添加了新代码质量规则来验证 `damAssetLucene` 索引的结构。 请参阅[自定义 DAM 资源 Lucene Oak 指数](/help/implementing/cloud-manager/custom-code-quality-rules.md#oakpal-damAssetLucene-sanity-check)，了解更多详细信息。

* “环境详细信息”页面现在将酌情显示发布和预览服务的多个域名。 请参阅[环境详细信息](/help/implementing/cloud-manager/manage-environments.md#viewing-environment)，了解更多详细信息。

### 错误修复 {#bug-fixes-junecm}

* 未正确分析根元素名称后包含换行符的 JCR 节点定义。

* 列表存储库 API 不会筛选已删除的存储库。

* 为计划步骤提供无效值时，显示错误消息。

* 有时，即使未部署配置，用户也会在 IP 允许列表旁边看到绿色的&#x200B;*活动*&#x200B;状态。

* 某些程序编辑序列可能导致无法创建或编辑生产管道。

* 某些程序编辑顺序可能会导致&#x200B;**概述**&#x200B;页面显示错误消息，重新执行程序设置。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets] 中的新增功能 {#ga-features-assets}

* 内容自动化功能允许 [!DNL Experience Manager Assets] 使用 [!DNL Adobe Creative Cloud] API可大规模自动进行资源生产。 它通过显着减少创建同一资源的变体所需的时间和反复操作来提高内容速度。 该功能不需要任何代码，并且可在DAM内使用。
* [!DNL Adobe Asset Link] v3.0用于 [!DNL Adobe Photoshop]， [!DNL Adobe Illustrator]、和 [!DNL Adobe InDesign] 和 [!DNL Adobe Asset Link] v2.0用于 [!DNL Adobe XD] 已发布。 它提供：

   * 支持 [!DNL Assets Essentials].
   * 能够自动连接到 [!DNL Experience Manager] as a [!DNL Cloud Service] 或 [!DNL Assets Essentials].

<!-- TBD: Checking with PMs if AAE release should be mentioned here.
-->

### 中可用的新功能 [!DNL Assets] 预发行渠道 {#beta-features-assets}

* 增强了视图设置以允许用户选择默认视图和默认排序参数。
* Linkshare下载功能使用可提高下载速度的异步下载。
* 用户可以根据属性谓词搜索和筛选文件夹。
* [!DNL Experience Manager Assets] 嵌入由提供支持的PDF查看器 [!DNL Adobe Document Cloud] 以预览支持的文档。 利用此功能，用户无需进行任何复杂处理即可预览PDF和其他多页文件。 这改进了与以下各项的功能对等性： [!DNL Experience Manager] 6.5.

### [!DNL Assets] 中修复的错误 {#bugs-fixed-assets}

* 将所有者添加到子文件夹时， [!DNL Assets] 还将该用户添加为父文件夹的所有者。 (CQ-4323737)
* 将资源添加到收藏集时，如果用户对收藏集搜索应用过滤器，则用户无法在“列表”视图中查看收藏集。 (CQ-4323181)
* 搜索文件和文件夹时，如果用户应用过滤器并选择 [!UICONTROL 文件和文件夹]，则仅显示文件，但不显示文件夹。 (CQ-4319543)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### [!DNL Sites] 中的新增功能 {#ga-features-sites}

* 现在，“发布到预览层”在站点管理UI中显示为页面状态
* 现在，“发布到预览层”在操作结束时会显示预览URL，并将URL保留在页面属性中以供将来参考

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
* 在从 Apple iOS 设备提交包含标准 HTML 上传字段的表单时，有时不会发送文件内容，而在另一端会收到一个 0 字节的文件。这是 Apple iOS 中的已知问题。[FB9117687](https://feedbackassistant.apple.com/feedback/9117687)

## [!DNL Experience Manager Screens] as a [!DNL Cloud Service] {#screens}

本节概述了AEM Screensas a Cloud Service的发行说明。

### 发布日期 {#release-date-june-screens}

AEM Screensas a Cloud Service的发布日期是2021年6月24日。

### 新增功能 {#what-is-new-screens-june}

>[!NOTE]
>请参阅 [AEM Screensas a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/home.html) 有关成功安装、配置和运行Screensas a Cloud Service所需的基础知识的指南，以及指向详细概念技术文档的链接。

* 批量设备注册管理意味着可以更快、更高效地配置大量播放器设备。

* 改进了每个设备、显示和渠道库存视图的搜索和筛选选项。

* 设备运行状况快照通过提供关键状态概览来节省时间。

* 对象详细信息页面提供项目中每个对象的最相关信息的摘要。

## CIF 加载项 {#cloud-services-cif}

### 新增功能 {#what-is-new-cif}

* 内容片段的新CIF产品和类别引用数据类型(包括 产品/类别选取器UI支持)
* 新的Commerce内容片段核心组件
* AEM后端支持全文商务搜索
* Commerce核心组件支持Adobe Commerce Sensei Recs数据收集
* 改进了类别页面的SEO友好URL
* 支持每个站点/配置的自定义HTTP标头

## 内容转移工具 {#content-transfer-tool}

### 发布日期 {#release-date-ctt-latest}

内容传输工具版本1.5.4的发布日期为2021年6月28日。

### 新增功能 {#what-is-new-ctt-latest}

* 支持可选 [预复制](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html) 添加了步骤以与CTT一起使用。 当源AEM实例配置为使用Amazon S3或Azure Blob Storage数据存储时，预复制步骤可用于显着加快内容传输活动的提取和摄取阶段。

* 向CTT添加了护栏，以防止用户停止摄取，并防止数据在摄取阶段达到临界点后可能损坏。

* 提取日志更具描述性，可帮助进行故障排除。

* 在UI中添加了更多描述性摄取状态消息。

### 错误修复 {#bug-fixes-ctt-latest}

* 在创作实例上停止引入时，UI会覆盖发布实例上之前完成的引入 `STOPPED` 从 `FINISHED`. 此问题已得到修复。

## Best Practices Analyzer {#best-practices-analyzer}

### 发布日期 {#release-date-bpa}

Best Practices Analyzer v2.1.16的发布日期是2021年6月30日。

### 新增功能 {#what-is-new-bpa-latest}

* 能够检测和报告文件夹下缺少的子节点 `/content/dam`.

* 能够检测和报告所使用的Best Practices Analyzer版本。

### 错误修复 {#bug-fixes-bpa-latest}

* 修复了与不支持的存储库结构(URS)相关的日志记录错误。
