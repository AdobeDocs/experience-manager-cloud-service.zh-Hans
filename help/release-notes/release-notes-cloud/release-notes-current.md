---
title: ' [!DNL Adobe Experience Manager] 作为Cloud Service的最新发行说明。'
description: ' [!DNL Adobe Experience Manager] 作为Cloud Service的最新发行说明。'
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
mini-toc-levels: 1
source-git-commit: 14dc3b308a839040fdf2efe42d2fa4ce35253df0
workflow-type: tm+mt
source-wordcount: '1309'
ht-degree: 2%

---


# [!DNL Adobe Experience Manager]作为Cloud Service的最新发行说明 {#release-notes}

以下部分概述了作为Cloud Service的[!DNL Experience Manager]当前（最新）版本的常规发行说明。

>[!NOTE]
>
>从此处，您可以导航到以前版本的发行说明；例如，2020年、2021年，等等。

>[!NOTE]
>
>请参阅[近期文档更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html) ，以了解有关与版本不直接相关的文档更新的详细信息。

## 发布日期 {#release-date}

[!DNL Adobe Experience Manager]作为[!DNL Cloud Service]的当前版本(2021.7.0)的发布日期是2021年7月29日。
以下版本(2021.8.0)发布于2021年8月26日。

## 发行视频 {#release-video}

请查看[2021年7月版概述](https://video.tv.adobe.com/v/335580)视频，了解添加的功能摘要。

## [!DNL Experience Manager] 作为基 [!DNL Cloud Service] 础 {#foundation}

### 新增功能 {#what-is-new-foundation}

* 更灵活的调度程序配置：项目可以更轻松地进行组织。 例如，您现在可以包含多个反映网站结构的重写规则文件。 [了解](/help/implementing/dispatcher/disp-overview.md#validation-debug) 此灵活模式，包括如何构建调度程序配置以利用此模式。
* 应将复制代理的“分发”选项卡下的树复制UI视为已弃用，并计划在9月30日之后删除。 [了解](/help/operations/replication.md#tree-activation) 替代复制策略。
* 已删除用于Sling数据源支持的包`org.apache.sling.datasource-1.0.4.jar`，因为该包的功能已过时，且客户未在使用。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets]的新增功能 {#assets-features}

* “内容自动化”功能允许[!DNL Experience Manager Assets]利用[!DNL Adobe Creative Cloud] API大规模自动化资产生产。 它可显着减少创建同一资产变体所需的时间和迭代次数，从而提高内容速度。 该功能不需要任何编程，也可从DAM内工作。 请参阅[使用Creative Cloud集成生成资产的变体](/help/assets/cc-api-integration.md)。

* [!DNL Experience Manager Assets] 包括PDF [!DNL Document Cloud] 查看器，可以本地预览PDF文档。此功能允许用户预览多页PDF文件，而无需进行任何文件处理或转换。 此功能改进了与[!DNL Experience Manager] 6.5的对等性。查看器中提供的控件包括缩放、导航到页面、取消停放控件以及全屏查看。 用户案例还可预览页面和书签并跳转到页面和书签。 支持对文件本身的注释，在将来的版本中，将会添加对PDF文件内内容的注释和批注。

   ![使用PDF查看器在中 [!DNL Experience Manager] 预览PDF文件](/help/assets/assets/preview-pdf-file-viewer.png)

* Linkshare下载功能使用异步下载来提高下载速度。 请参阅[下载使用链接共享共享的资产](/help/assets/download-assets-from-aem.md#link-share-download)。

   ![下载收件箱](/help/assets/assets/download-inbox.png)

* 视图设置经过增强，允许用户选择默认视图和默认排序参数。

   ![在“视图设置”中设置默 [!UICONTROL 认视图]](/help/assets/assets/view-settings-for-defaults.png)

* 用户可以根据属性谓词搜索和筛选文件夹。

   ![使用搜索谓词筛选搜索文件夹](/help/assets/assets/search-folders-via-predicates.png)

### [!DNL Assets]预发行渠道中提供的新增功能 {#assets-prerelease-features}

<!-- TBD: Not sure about GA of these enh. Shall check with the team.

* A user experience enhancements displays the number of assets present in a folder. For more than 1000 assets in a folder, [!DNL Assets] displays 1000+.

  ![Number of assets in a folder are displayed on the interface](/help/assets/assets/browse-folder-number-of-assets.png)

* You can directly apply a metadata schemas to a folder in its [!UICONTROL Properties].

  ![Add metadata schema from folder properties](/help/assets/assets/metadata-schema-folder-properties.png)
-->

* 当您以链接形式共享数字资产时，用户可以将URL复制到剪贴板。 通过增强功能，您可以更快、更方便地共享资产。

### [!DNL Assets]中修复的错误 {#assets-bugs-fixed}

API `com.day.cq.dam.api.collection.SmartCollection`在[!DNL Experience Manager]中不作为[!DNL Cloud Service]提供。 (CQ-4326322)

## [!DNL Experience Manager Forms] as a  [!DNL Cloud Service] {#forms}

### [!DNL Forms]的新增功能 {#what-is-new-forms}

* 现在，您可以使用Automated forms conversion服务将法语、德语和西班牙语的PDF forms](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?#language-specific-meta-model)转换为自适应表单。[
* 在模板编辑器中添加了一个单独的面板，以显示与自适应表单组件相关的错误。 它有助于将所有自适应表单错误整合到一个位置并缩短解决时间。

### [!DNL Forms]预发行版渠道中提供的新增功能 {#beta-features-forms}

* **[!DNL AEM Forms as a Cloud Service - Communications]**: [通信](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/aem-forms-cloud-service-communications.html) API您可以将XDP模板和XML数据组合在一起，以生成各种格式的打印文档。该服务允许您以同步模式生成文档。 利用API，可创建应用程序，以便：
   * 使用XML数据填充模板文件，以生成文档。
   * 以各种格式生成输出表单，包括非交互式PDF打印流。
   * 从XFA表单PDF和Adobe Acrobat表单生成打印PDF文件。

* **变量数据外部器**:您可以在由您的组织管理的外部存储系统上保存AEM Workflow变量的数据。

* **基于Acroform的记录文档**:除了基于 [XFA的表单模板外，您还可以使用Adobe Acrobat表单PDF(Acroform PDF)](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/create-an-adaptive-form/generate-document-of-record-for-non-xfa-based-adaptive-forms.html) 作为记录文档的模板。

* **Microsoft Azure数据存储连接器**:现在，您可 [以将表单数据模型连接到Microsoft Azure Storage](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/use-form-data-model/configure-azure-storage.html)。它允许您将自适应表单数据作为BLOB检索并存储到Microsoft Azure Storage中。

## CIF附加组件 {#cloud-services-cif}

### 新增功能 {#what-is-new-cif}

* CIF核心组件v2
   * 简化和改进了PDP/PLP URL和SEO配置
   * 在创作模式下暂存产品数据的可视指示器，可更好地显示即将发生的更改
   * 用于内容和商务页面的新站点地图组件

* 支持[Adobe商务Sensei产品推荐，由AEM Storefront中的Adobe Sensei](https://business.adobe.com/products/magento/product-recommendations.html)提供支持，使用预定义或即时创建的推荐

## [!DNL Experience Manager Screens] as a  [!DNL Cloud Service] {#screens}

### 错误修复 {#bug-fixes-screens}

* 现在，将在创建或更新期间验证内容提供程序设置。

* 所有显示的视图都包含文件夹列。

* 您可以展开Screens内容结构。

* `bulk-offline-update-service` 缺少某些环境的所有权限。

* 更新了帮助链接以匹配新的screens云文档。

* 现在可以取消分配播放列表并禁止删除分配了播放器的播放列表。

* 现在，在清除“所有”缓存时，播放器会重新下载资产。

* 如果为后一天设置了&#x200B;*结束时间*，则重复计划现在有效。

* `Back&Forward` 现在可在Screens中作为Cloud ServiceUI使用。

* 无法在之前创建名称相同但命名空间不同的标记。

## 用于Experience Manager为Cloud Service的XML文档 {#xml-documentation}

### 新增功能 {#what-is-new-xml-documentation}

Experience Manager为Cloud Service的XML文档通常可用。 它允许Cloud Service客户购买XML文档，以便跨多个渠道(包括Experience Manager站点)导入、创建、管理和提供技术内容。

## Cloud Manager {#cloud-manager}

本部分概述了AEM as a Cloud 2021.7.0中的Cloud Manager发行说明。

### 发布日期 {#release-cm-july}

AEM as a Cloud Manager 2021.7.0版本的发布日期是2021年7月15日。
下一版本计划于2021年8月12日发布。

### 新增功能 {#what-is-new-cm-july}

* 客户现在能够为其Cloud Manager构建过程使用Azul 8和11个JDK，并且可以选择将其中一个JDK用于与工具链兼容的Maven插件&#x200B;*或*&#x200B;整个Maven进程执行。

* 出站出口IP现在将记录在生成步骤日志文件中。

* 现在，运行旧版AEM的暂存环境和生产环境将报告&#x200B;**可用更新**&#x200B;的状态。

* 支持的最大SSL证书数已增加到每个计划20个。

* 每个环境可配置的最大域数已增加到500个。

* **管理Git**&#x200B;按钮已被命名为&#x200B;**访问Git信息**，对话框已被直观地刷新。

* Cloud Manager使用的AEM项目原型版本已更新至版本28。

### 错误修复 {#bug-fixes-cm-july}

* 在某些情况下，将IP允许列表绑定到环境时，“预览”不是可用选项。

* 手动导航到非现有执行的执行详细信息页面不会显示错误，只是显示无休止的加载屏幕。

* 达到最大数量的SSL证书时显示的错误消息不起作用。

* 在某些情况下， **Overview**&#x200B;页面的管道卡中显示的发行版本可能不一致。

* “添加程序向导”错误地指示创建后无法更改名称。

### 已知问题 {#known-issues-cm-july}

切换使用Azul JDK的客户应该注意到，并非所有现有应用程序都会在Azul JDK上编译而不出错。 强烈建议在切换前在本地进行测试。

## Cloud Acceleration Manager {#cam}

### 发布日期 {#release-date-july-cam}

Cloud Acceleration Manager的发布日期是2021年7月15日。

### 新增功能 {#what-is-new-cam}

Cloud Acceleration Manager是一个基于云的应用程序，旨在引导您的IT团队完成从规划到上线的整个过渡历程。Cloud Service 通过Adobe推荐的最佳实践、提示、文档和工具，为成功的迁移设置团队，以便在到AEM作为Cloud Service的历程的每个阶段提供帮助。 请在此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/getting-started-cam.html?lang=en)了解更多信息。[

>[!NOTE]
>
> 查看此[Cloud Acceleration Manager演示视频](https://video.tv.adobe.com/v/335547)。
