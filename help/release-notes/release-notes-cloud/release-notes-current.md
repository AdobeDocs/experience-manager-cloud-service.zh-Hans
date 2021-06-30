---
title: ' [!DNL Adobe Experience Manager] 作为Cloud Service的最新发行说明。'
description: ' [!DNL Adobe Experience Manager] 作为Cloud Service的最新发行说明。'
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
mini-toc-levels: 1
source-git-commit: bed5a88a545efa4dbfe5c20f4713c0c6adb9847b
workflow-type: tm+mt
source-wordcount: '1544'
ht-degree: 3%

---


# [!DNL Adobe Experience Manager]作为Cloud Service的最新发行说明 {#release-notes}

以下部分概述了作为Cloud Service的[!DNL Experience Manager]当前（最新）版本的常规发行说明。

>[!NOTE]
>
>从此处，您可以导航到以前版本的发行说明；例如，2020年、2021年等年份的客户。

>[!NOTE]
>
>请参阅[近期文档更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html) ，以了解有关与版本不直接相关的文档更新的详细信息。

## 发布日期 {#release-date}

[!DNL Adobe Experience Manager]作为Cloud Service2021.6.0的发布日期是2021年6月28日。
以下版本(2021.7.0)将于2021年7月29日发布。

## 发行视频 {#release-video}

请观看2021年6月版[概述](https://video.tv.adobe.com/v/334296)视频，了解添加的功能摘要。

## AEM as a Cloud Service的XML Documentation {#xml-documentation}

### 新增功能 {#what-is-new-xml-documentation}

* AEM as aCloud Service的XML Documentation现在为GA。
* 这将允许现有AEMCloud Service客户购买XML Documentation添加，以便跨多个渠道(包括AEM站点)导入、创建、管理和交付技术内容

## Cloud Manager {#cloud-manager}

本部分概述了AEM as a 2021.6.0和2021.5.0Cloud Service中Cloud Manager的发行说明。

### 发布日期 {#release-date-june-cm}

AEM as a Cloud Service2021.6.0中Cloud Manager的发布日期是2021年6月10日。
下一版本计划于2021年7月15日发布。

### 新增功能 {#what-is-new-junecm}

* 预览服务将以滚动方式部署到所有程序。 当客户的计划启用了预览服务后，系统会在产品中通知客户。 有关更多详细信息，请参阅[访问预览服务](/help/implementing/cloud-manager/manage-environments.md#access-preview-service) 。

* 现在，在生成步骤期间下载的Maven依赖项将在管道执行之间缓存。 未来几周，将为客户启用此功能。

* 现在可以通过编辑程序对话框编辑程序的名称。

* 在项目创建期间和通过管理git工作流在默认推送命令中使用的默认分支名称已更改为`main`。

* 在UI中编辑项目体验已刷新。

* 质量规则`ImmutableMutableMixCheck`已更新，可将`/oak:index`节点分类为不可变。

* 质量规则`CQBP-84`和`CQBP-84--dependencies`已合并到单个规则中。 作为此整合的一部分，对依赖项的扫描可更准确地识别部署到AEM运行时的第三方依赖项中的问题。

* 为避免混淆，“环境详细信息”页面上的“发布AEM”和“发布Dispatcher”区段行已进行合并。

   ![](/help/onboarding/release-notes-cloud-manager/assets/aem-dispatcher.png)

* 添加了新的代码质量规则来验证`damAssetLucene`索引的结构。 有关更多详细信息，请参阅[自定义DAM资产Lucene Oak索引](/help/implementing/cloud-manager/custom-code-quality-rules.md#oakpal-damAssetLucene-sanity-check)。

* “环境详细信息”页面现在将显示发布和预览服务的多个域名（如果适用）。 有关更多详细信息，请参阅[环境详细信息](/help/implementing/cloud-manager/manage-environments.md#viewing-environment)。

### 错误修复 {#bug-fixes-junecm}

* 未正确解析根元素名称后包含换行符的JCR节点定义。

* 列表存储库API不会过滤已删除的存储库。

* 为计划步骤提供无效值时，显示错误消息。

* 有时，即使未部署该配置，用户也可能在IP允许列表旁看到绿色的&#x200B;*活动*&#x200B;状态。

* 某些程序编辑序列可能会导致无法创建或编辑生产管道。

* 某些程序编辑序列可能会导致在&#x200B;**概述**&#x200B;页面中显示一条误导性消息，以便重新执行程序设置。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets]的新增功能 {#ga-features-assets}

* “内容自动化”功能允许[!DNL Experience Manager Assets]利用[!DNL Adobe Creative Cloud] API大规模自动化资产生产。 它可显着减少创建同一资产变体所需的时间和迭代次数，从而提高内容速度。 该功能不需要任何编程，也可从DAM内工作。 请参阅[使用Creative Cloud集成生成资产的变体](/help/assets/cc-api-integration.md)。

* [[!DNL Adobe Asset Link] 提供了适用于](https://helpx.adobe.com/cn/enterprise/using/adobe-asset-link.html) 、 [!DNL Adobe Photoshop]和 [!DNL Adobe Illustrator]的v3.0 [!DNL Adobe InDesign] 和适用于2.0 [[!DNL Adobe Asset Link] 的](https://helpx.adobe.com/cn/enterprise/using/adobe-asset-link-for-xd.html)  [!DNL Adobe XD] 。它提供：

   * 支持[!DNL Assets Essentials]。
   * 能够自动连接到[!DNL Experience Manager]作为[!DNL Cloud Service]或[!DNL Assets Essentials]。

* [资产批量摄取工具](/help/assets/add-assets.md#asset-bulk-ingestor)允许您在批量摄取期间添加元数据。

### [!DNL Assets]预发行渠道中提供的新增功能 {#beta-features-assets}

* 视图设置经过增强，允许用户选择默认视图和默认排序参数。

   ![在视图设置中设置默认视图](/help/assets/assets/view-settings-for-defaults.png)

* Linkshare下载功能使用异步下载来提高下载速度。

* 用户可以根据属性谓词搜索和筛选文件夹。

   ![使用搜索谓词筛选搜索文件夹](/help/assets/assets/search-folders-via-predicates.png)

* [!DNL Experience Manager Assets] 嵌入PDF查看器以预览支持的文档格式。它由[!DNL Adobe Document Cloud]提供电源。 此功能允许用户预览PDF和其他多页文件，而无需进行任何复杂的处理。 这改进了与[!DNL Experience Manager] 6.5的功能对等性。预览中提供的控件包括缩放、导航到页面、取消停放控件以及全屏查看。 集成的PDF查看器支持AI、DOCX、INDD、PDF和PSD文件格式。 您可以对资产本身进行注释，但不支持在PDF文件中添加注释和批注。

   ![使用PDF查看器在中 [!DNL Experience Manager] 预览PDF文件](/help/assets/assets/preview-pdf-file-viewer.png)

* 用户体验增强功能可显示文件夹中存在的资产数量。 对于文件夹中超过1000个资产，[!DNL Assets]显示的资产数量超过1000个。

   ![文件夹中的资产数量显示在界面上](/help/assets/assets/browse-folder-number-of-assets.png)

* 您可以直接将元数据架构应用到其[!UICONTROL Properties]中的文件夹。

   ![从文件夹属性添加元数据架构](/help/assets/assets/metadata-schema-folder-properties.png)

### [!DNL Assets]中修复的错误 {#bugs-fixed-assets}

* 在向子文件夹中添加所有者时，[!DNL Assets]还会添加与父文件夹所有者相同的用户。 (CQ-4323737)
* 在将资产添加到收藏集时，如果用户对收藏集搜索应用过滤器，则用户将无法在列表视图中查看收藏集。 (CQ-4323181)
* 在搜索文件和文件夹时，如果用户应用过滤器并选择[!UICONTROL Files &amp; Folders]，则只显示文件，而不显示文件夹。 (CQ-4319543)

## [!DNL Experience Manager Sites] as a  [!DNL Cloud Service] {#sites}

### [!DNL Sites]的新增功能 {#ga-features-sites}

* “发布到预览层”现在在站点管理UI中显示为页面状态
* 现在，发布到预览层会在操作结束时显示预览URL，并在页面属性中保留该URL以供日后参考

## [!DNL Adobe Experience Manager Forms] as a  [!DNL Cloud Service] {#forms}

### [!DNL Forms]的新增功能 {#what-is-new-forms}

* 添加了在AEM收件箱中过滤自定义列的功能。
* 添加了使用自适应表单编辑器的主题编辑器和样式层来设置验证码组件样式的功能。
* 提高了自动检测源PDF forms中逻辑部分并将这些逻辑部分转换为相应自适应表单面板的速度和准确性。
* 添加了将PDF或XDP文件从一个文件夹移动到另一个文件夹的移动操作。

### [!DNL Forms]的测试版功能 {#what-is-new-forms-prerelease}

* **[!DNL AEM Forms as a Cloud Service - Communications]**:通信API可帮助您将XDP模板和XML数据结合起来，以生成各种格式的打印文档。该服务允许您以同步模式生成文档。 利用API，可创建应用程序，以便：
   * 使用XML数据填充模板文件，生成最终表单文档。
   * 以各种格式生成输出表单，包括非交互式PDF打印流。
   * 从XFA表单PDF和Adobe Acrobat表单(AcroForm)生成打印PDF。

* **变量数据外部器**:您可以在由您的组织管理的外部存储系统上保存AEM Workflow变量的数据。

您可以写信给[!DNL formscsbeta@adobe.com]注册测试版程序。

### [!DNL Forms]中修复的错误 {#forms-bugs-fixed}

* 在通过表单数据模型(FDM)将数据提交到后端服务之前，如果对字段进行了验证，则验证会成功，但表单数据模型服务无法调用后验证。
* 当您从Apple iOS设备提交包含标准HTML上传字段的表单时，有时不会发送文件内容，而会在另一端收到0字节文件。 这是Apple iOS中的已知问题。 [FB9117687](https://feedbackassistant.apple.com/feedback/9117687)

## [!DNL Adobe Experience Manager Screens] as a  [!DNL Cloud Service] {#screens}

本部分概述了AEM Screens as a Cloud Service的发行说明。

### 发布日期 {#release-date-june-screens}

AEM Screens as a Cloud Service的发布日期是2021年6月24日。

### 新增功能 {#what-is-new-screens-june}

>[!NOTE]
>请参阅[AEM Screens as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/home.html?lang=en)指南，了解成功安装、配置和运行Screens作为Cloud Service所需的基本知识，并链接到详细概念技术文档。

* 批量设备注册管理意味着可以更快、更高效地配置大量播放器设备。

* 改进了每个设备、显示和渠道清单视图的搜索和过滤选项。

* 设备健康快照通过提供关键状态一目了然来节省时间。

* 对象详细信息页面提供了项目中每个对象最相关信息的摘要。

## CIF附加组件 {#cloud-services-cif}

### 新增功能 {#what-is-new-cif}

* 内容片段的新CIF产品和类别引用数据类型(包括 产品/类别选取器UI支持)
* 新的商务内容片段核心组件
* AEM后端支持的全文商务搜索
* 商务核心组件支持Adobe商务Sensei Recs数据收集
* 改进了类别页面的SEO友好URL
* 支持每个站点/配置的自定义HTTP标头

## 内容传输工具 {#content-transfer-tool}

### 发布日期 {#release-date-ctt-latest}

内容传输工具v1.5.4的发布日期是2021年6月28日。

### 新增功能 {#what-is-new-ctt-latest}

* 支持添加了可选的[预复制](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en)步骤以与CTT一起使用。 当将源AEM实例配置为使用Amazon S3或Azure Blob Storage数据存储时，可以使用预复制步骤显着加快内容传输活动的提取和摄取阶段。

* 向CTT添加了护栏，以防止用户在摄取阶段期间数据到达关键点时停止摄取，并可能损坏数据。

* 提取日志更具描述性，可帮助进行疑难解答。

* 在UI中添加了更具描述性的摄取状态消息。

### 错误修复 {#bug-fixes-ctt-latest}

* 在创作实例上停止摄取时，UI会将之前在发布实例上完成的摄取从`FINISHED`覆盖到`STOPPED`。 此问题已修复。


