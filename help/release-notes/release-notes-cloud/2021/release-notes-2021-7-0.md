---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 2021.7.0 版的发行说明。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 2021.7.0 版的发行说明。'
exl-id: 848f6a29-2e0f-4976-8ed7-6b7f69408c1b
source-git-commit: cc6565121a76f70b958aa9050485e0553371f3a3
workflow-type: tm+mt
source-wordcount: '1316'
ht-degree: 50%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 的最新发行说明 {#release-notes}

以下部分概述了当前（最新）版本的 [!DNL Experience Manager] as a Cloud Service 的一般发行说明。

>[!NOTE]
>
>从此处，您可以导航到早期版本的发行说明；例如，2020版、2021版等的发行说明。

>[!NOTE]
>
>有关未与版本直接相关的文档更新的详细信息，请参阅[最新文档更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html)。

## 发布日期 {#release-date}

的发布日期 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 当前版本(2021.7.0)为2021年7月29日。
以下版本(2021.8.0)的发布日期为2021年8月26日。

## 发布视频 {#release-video}

请查看 [2021年7月发行版概述](https://video.tv.adobe.com/v/335580) 视频，以了解新增功能的摘要。

## Experience Manager基础as a Cloud Service {#foundation}

### 新增功能 {#what-is-new-foundation}

* 更灵活的Dispatcher配置：可以更轻松地组织项目。 例如，您现在可以包含反映站点结构的多个重写规则文件。 [了解](/help/implementing/dispatcher/disp-overview.md#validation-debug) 这种灵活的模式，包括如何构建Dispatcher配置以对其进行利用。
* 复制代理的“分发”选项卡下的树复制UI应被视为已弃用，计划在9月30日后删除。 [了解](/help/operations/replication.md#tree-activation) 替代复制策略。
* 捆绑 `org.apache.sling.datasource-1.0.4.jar` 的for Sling数据源支持已删除，因为它具有过时的功能，并且未由客户使用。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets] 中的新增功能 {#assets-features}

* 内容自动化功能允许 [!DNL Experience Manager Assets] 利用 [!DNL Adobe Creative Cloud] 用于大规模自动化资产生产的API。 它通过显着减少创建同一资源的变体所需的时间和迭代来提高内容速度。 该功能不需要进行任何编程，并且可在DAM内使用。 参见 [使用Creative Cloud集成生成资源变体](/help/assets/cc-api-integration.md).

* [!DNL Experience Manager Assets] 包括 [!DNL Document Cloud] PDF查看器以本机预览PDF文档。 此功能允许用户预览多页PDF文件，而无需进行任何文件处理或转换。 此功能改进了与 [!DNL Experience Manager] 6.5.查看器中可用的控件包括缩放、导航到页面、取消停靠控件以及全屏查看。 用户案例还可以预览和跳转到页面和书签。 支持对文件本身进行评论，并且将在未来版本中添加对PDF文件中内容进行评论和批注。

   ![在中预览PDF文件 [!DNL Experience Manager] 使用PDF查看器](/help/assets/assets/preview-pdf-file-viewer.png)

* Linkshare下载功能使用可提高下载速度的异步下载。 参见 [下载使用链接共享功能共享的资源](/help/assets/download-assets-from-aem.md#link-share-download).

   ![下载收件箱](/help/assets/assets/download-inbox.png)

* 增强了视图设置以允许用户选择默认视图和默认排序参数。

   ![在中设置默认视图 [!UICONTROL 查看设置]](/help/assets/assets/view-settings-for-defaults.png)

* 用户可以根据属性谓词搜索和筛选文件夹。

   ![使用搜索谓词筛选搜索文件夹](/help/assets/assets/search-folders-via-predicates.png)

### 中可用的新功能 [!DNL Assets] 预发行渠道 {#assets-prerelease-features}

<!-- TBD: Not sure about GA of these enh. Shall check with the team.

* A user experience enhancements displays the number of assets present in a folder. For more than 1000 assets in a folder, [!DNL Assets] displays 1000+.

  ![Number of assets in a folder are displayed on the interface](/help/assets/assets/browse-folder-number-of-assets.png)

* You can directly apply a metadata schemas to a folder in its [!UICONTROL Properties].

  ![Add metadata schema from folder properties](/help/assets/assets/metadata-schema-folder-properties.png)
-->

* 在将数字资产作为链接共享时，用户可以将URL复制到剪贴板。 增强功能可让您以更快、更方便的方式共享资产。

### [!DNL Assets] 中修复的错误 {#assets-bugs-fixed}

API `com.day.cq.dam.api.collection.SmartCollection` 在中不可用 [!DNL Experience Manager] as a [!DNL Cloud Service]. (CQ-4326322)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] 的新增功能 {#what-is-new-forms}

* 您现在可以使用 Automated Forms Conversion Service 将[法语、德语和西班牙语版本的 PDF 表单](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?#language-specific-meta-model)转换为自适应表单。
* 已向模板编辑器添加一个单独的面板，以显示与自适应表单组件相关的错误。它有助于在一个位置整合所有自适应表单错误并减少解决时间。

### [!DNL Forms] 预发行渠道中提供的新功能 {#beta-features-forms}

* **[!DNL AEM Forms as a Cloud Service - Communications]**：[通信 API](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications.html) 帮助您组合 XDP 模板和 XML 数据以生成各种格式的打印文档。该服务允许您以同步模式生成文档。 API 使您能够创建应用程序，这些应用程序允许您：
   * 使用 XML 数据填充模板文件来生成文档。
   * 生成各种格式的输出表单，包括非交互式 PDF 打印流。
   * 利用 XFA 表单 PDF 和 Adobe Acrobat 表单生成打印版 PDF 文件。

* **变量数据外部化程序**：您可以将 AEM Workflow 变量的数据保存在由组织管理的外部存储系统上。

* **基于 Acroform 的记录文档**：除了基于 XFA 的表单模板，您还可以[使用 Adobe Acrobat Form PDF (Acroform PDF)](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/create-an-adaptive-form/generate-document-of-record-for-non-xfa-based-adaptive-forms.html) 作为记录文档的模板。

* **Microsoft Azure 数据存储连接器**：您现在可以[将表单数据模型连接到 Microsoft Azure Storage](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/use-form-data-model/configure-azure-storage.html)。它可让您检索自适应表单数据并将这些数据作为 BLOB 存储到 Microsoft Azure Storage。

## CIF 加载项 {#cloud-services-cif}

### 新增功能 {#what-is-new-cif}

* CIF核心组件v2
   * 简化并改进了PDP/PLP URL和SEO的配置
   * 创作模式下暂存产品数据的视觉指示器，用于更好地显示即将发生的更改
   * 内容和商务页面的新站点地图组件

* 支持 [Adobe Commerce Sensei产品推荐，由Adobe Sensei提供支持](https://business.adobe.com/products/magento/product-recommendations.html) 在AEM Storefront中使用预定义或动态创建的推荐

## [!DNL Experience Manager Screens] as a [!DNL Cloud Service] {#screens}

### 错误修复 {#bug-fixes-screens}

* 内容提供程序设置现在会在创建或更新过程中进行验证。

* 所有显示视图都有文件夹列。

* 您可以展开Screens内容结构。

* `bulk-offline-update-service` 缺少某些环境的所有权限。

* 更新了“帮助”链接以匹配新的screens cloud文档。

* 现在可以取消分配播放列表并禁止删除已分配播放器的播放列表。

* 播放器现在会在“全部”缓存清除后重新下载资产。

* 现在，如果 *结束时间* 设置为第二天。

* `Back&Forward` 现在适用于Screensas a Cloud ServiceUI。

* 以前无法创建具有相同名称但命名空间不同的标记。

## XML DocumentationExperience Manageras a Cloud Service {#xml-documentation}

### 新增功能 {#what-is-new-xml-documentation}

适用于Experience Manageras a Cloud Service的XML Documentation现已正式推出。 它允许Experience Manageras a Cloud Service的客户促使XML Documentation加载项跨多个渠道(包括Experience Manager Sites)导入、创建、管理和交付技术内容。

## Cloud Manager {#cloud-manager}

此部分概述了 AEM as a Cloud Service 2021.7.0 中的 Cloud Manager 的发行说明。

### 发布日期 {#release-cm-july}

AEM as a Cloud Service 2021.7.0 中的 Cloud Manager 的发布日期是 2021 年 7 月 15 日。下一个版本计划于2021年8月12日发布。

### 新增功能 {#what-is-new-cm-july}

* 客户现在可以将 Azul 8 和 11 JDK 用于其 Cloud Manager 构建过程，并且可以选择将这些 JDK 之一用于与工具链兼容的 Maven 插件&#x200B;*或*&#x200B;整个 Maven 流程执行。

* 出站出口 IP 现在将记录在构建步骤日志文件中。

* 运行旧版本的 AEM 的暂存环境和生产环境现在将报告&#x200B;**更新可用**&#x200B;状态。

* 每个程序支持的 SSL 证书的最大数量已增至 20。

* 每个环境可配置的域的最大数量已增至 500。

* **管理 Git** 按钮已更名为&#x200B;**访问 Git 信息**，并且对话框的外观已更新。

* Cloud Manager 使用的 AEM 项目原型的版本已更新到版本 28。

### 错误修复 {#bug-fixes-cm-july}

* 在某些情况下，将 IP 允许列表绑定到环境时，“预览”选项不可用。

* 手动导航到不存在的执行的执行详细信息页面并没有显示错误，只显示了一个无休止的加载屏幕。

* 当达到 SSL 证书的最大数量时显示的错误消息没有帮助。

* 在某些情况下，**概述**&#x200B;页面上的管道信息卡中显示的版本可能存在差异。

* 添加程序向导错误地指出，创建后无法更改名称。

### 已知问题 {#known-issues-cm-july}

改用 Azul JDK 的客户应该知道，并非所有现有应用程序都能在 Azul JDK 上编译无误。 强烈建议在切换前进行本地测试。

## Cloud Acceleration Manager {#cam}

### 发布日期 {#release-date-july-cam}

Cloud Acceleration Manager的发布日期是2021年7月15日。

### 新增功能 {#what-is-new-cam}

Cloud Acceleration Manager 是一个基于云的应用程序，旨在指导您的 IT 团队在 Cloud Service 上完成从规划到上线的过渡过程。使用 Adobe 推荐的最佳实践、技巧、文档和工具在迁移到 AEM as Cloud Service 的历程中的每个阶段提供帮助，让您的团队成功完成迁移。了解详情 [此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/getting-started-cam.html?lang=en).

>[!NOTE]
>
> 检查此 [Cloud Acceleration Manager演示视频](https://video.tv.adobe.com/v/335547).
