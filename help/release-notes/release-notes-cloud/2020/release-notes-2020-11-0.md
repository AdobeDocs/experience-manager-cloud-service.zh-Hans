---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2020.11.0 版的发行说明。'
description: '[!DNL Adobe Experience Manager] 作为2020.11.0的Cloud Service发行说明。'
exl-id: 8066c0fb-c2f5-4625-9448-b0c74ff4e192
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '1265'
ht-degree: 4%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 版的发行说明 {#release-notes}

以下部分概述了[!DNL Experience Manager]作为Cloud Service的常规发行说明。

## 发布日期 {#release-date}

[!DNL Adobe Experience Manager] as aCloud Service2020.11.0的发布日期是2020年12月2日。
以下版本(2020.12.0)将于2020年12月17日发布

## [!DNL Adobe Experience Manager Sites] 作为Cloud Service {#sites}

### [!DNL Sites] {#what-is-new-sites}的新增功能

* **[启动层次结构管理](/help/sites-cloud/authoring/launches/managing-pages.md) 和未 [来时间扭曲](/help/sites-cloud/authoring/launches/preview.md)**:新的UI用于在启动项内添加/删除页面，以及使用时间扭曲浏览网站时，会显示启动项中的未来状态。

* **[扩展内容片段模型和编辑器](/help/assets/content-fragments/content-fragments-models.md)**:可对各种数据类型进行输入验证的新选项，通过新的表单可视化图表改进了枚举数据类型，并且在资产UI中显示和搜索内容片段模型名称。

* **对可用于转出的Live Copy页面进行排序**:新选项，用于使用名称 [!UICONTROL 、上次修改日期]和上次转出日期属性对可用于转出的Live  [!UICONTROL Copy页面]进行  排序。页面的[!UICONTROL 上次转出日期]是引入的新属性。

## [!DNL Adobe Experience Manager Assets] 作为Cloud Service {#assets}

### [!DNL Assets]和[!DNL Dynamic Media] {#what-is-new-assets}的新增功能

* **批量资产摄取**:为客户提供可扩展的云原生摄取服务，该服务将作为 [!DNL Experience Manager] Cloud Service架构（包括资产微服务）。主要用例包括通过监控、报告和计划进行大规模摄取，同时允许使用常用的云上传工具将资产初始传输到云数据存储区。 请参阅[资产批量摄取工具](/help/assets/add-assets.md#asset-bulk-ingestor)。

   此工具适用于系统管理员、顾问或实施合作伙伴角色。 此功能允许进行大规模摄取，理想情况下是在初始摄取或偶尔进行大型摄取时使用。 对于较小的摄取作业，请使用Assets用户界面](/help/assets/add-assets.md#upload-assets)上传[[!DNL Experience Manager] 桌面应用程序](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/introduction.html?lang=en)或[。

   ![批量导入程序的配置](/help/assets/assets/bulk-import-config-low-res.png)

* 用户现在可以在卡片视图和列视图中对数字资产进行排序。

   ![排序资产](/help/assets/assets/asset-sort-options.png)

* 对此版本[!DNL Experience Manager Assets]中的辅助功能进行了以下增强。 有关更多信息，请参阅 [!DNL Assets]](/help/assets/accessibility.md)中的[辅助功能。

   * 使用键盘导航时间轴时，Esc键可以折叠“显示全部”选项，而不会失去焦点。
   * 使用键盘选项卡键导航时，在从添加的标记中删除最后一个标记后，标记字段会保留焦点。
   * [!DNL Experience Manager] 组件现在包含要由屏幕阅读器使用的名称、角色和值的适当信息。
   * 删除“类型/大小”组合框、“链接”组合框、“语言”组合框或“文本编辑”框后，键盘焦点将返回到下一个或上一个用户界面元素或更相关的用户界面元素。
   * 将指针悬停在选项上时，会显示“选择”和“下载”等提示。 使用屏幕放大镜的用户可能看不到文件缩略图，因为这些提示。 现在，在使用`Escape`键删除选项后，可以保留焦点。
   * 从页面中存在的网格中选择网格单元格后，焦点将转移到屏幕上显示的操作栏。
   * 可视用户可以区分普通文本和链接，因为在[!DNL Experience Manager]主页中，将显示指向所有解决方案的链接的可视线索（下划线和V形图标）。

* **Dynamic Media中的批集预设**:现在，在您将资产文件单独或使用批量摄取功能上传到文件夹时，您可以自动创建和组织图像集或旋转集中的多个资产。

   请参阅[关于批集预设](/help/assets/dynamic-media/batch-set-presets-dm.md)。

* [!DNL Dynamic Media]中现在提供了以下辅助功能增强功能：

   * 屏幕阅读器(JAWS、Narrator)在“嵌入大小”菜单选项中讲述菜单项的名称、角色和状态。
   * 用户可以使用`Tab`键导航“电子邮件链接”对话框。
   * 鉴于屏幕阅读器增强功能，创建视频编码配置文件的工作流更易于用户使用。
   * 使用`Tab`键导航时，焦点会移至工作流中相应的用户界面元素，以创建交互式视频。
   * 对“发布”页面、“编辑资产”页面、“编辑智能裁剪”页面和“图像集编辑器”页面进行了改进，以符合Web标准。 辅助技术(AT)用户现在可以轻松导航这些页面并执行裁剪图像等操作。
   * 对查看器进行了改进，允许用户使用键盘进行导航。
   * 键盘和屏幕阅读器用户可以使用裁剪功能。
   * 键盘用户可以更好地管理热点。

   请参阅 [!DNL Dynamic Media]](/help/assets/dynamic-media/accessibility-dm.md)中的[辅助功能。

## Adobe Experience Manager Commerce as aCloud Service{#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* 已发布CIF Venia参考网站 — 2020.11.05，其中包含最新的CIF核心组件版本v1.5.0。有关更多详细信息，请参阅[CIF Venia参考网站](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.10.27)。

* 已发布CIF核心组件v1.5.0。有关更多详细信息，请参阅[CIF核心组件](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.5.0)。

### 错误修复 {#bug-fixes-commerce}

* 如果未在Sling CA配置中直接指定配置，但在其中一个父配置中指定配置，则无法正确读取GraphQL客户端配置。 此问题已修复。

## Cloud Manager {#cloud-manager}

### 发布日期 {#release-date-cm}

AEM as a Cloud Manager的Cloud Service2020.11.0的发布日期是2020年11月12日。

### [!DNL Cloud Manager] {#what-is-new-cm}的新增功能

* 现在，用户可以从&#x200B;**Environments**&#x200B;卡和&#x200B;**Environments**&#x200B;摘要页面上的环境菜单选项中，使用新的菜单选项&#x200B;**Local Login**。
有关更多详细信息，请参阅[管理环境](/help/implementing/cloud-manager/manage-environments.md#login-locally) 。

* Cloud Manager中的&#x200B;**Learn**&#x200B;选项卡已使用UI中的新图像刷新。

### 错误修复 {#bug-fixes-cloud-manager}

* 需要下载Maven插件，才能加载执行生成之前完成的依赖项。
* 现在，Cloud Manager页脚中用于选择语言的链接将导航到正确的位置。
* 有时，在代码扫描期间，SonarQube进程不会启动。 现在将自动检测并尝试重新启动。
* 所有现有的生产管道都将通过体验审核步骤自动启用。

## Adobe Experience Manager as a Cloud Service 基础 {#cloud-service-foundation}

### 工作流 {#workflows}

* 添加了基于工作流标题、工作流模型、状态、启动器、有效负荷路径和开始日期的用于搜索工作流实例的支持。 请参阅[搜索工作流实例](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/administering/workflows-administering.html)。

### 发布层用户数据同步{#user-sync}

* 用户数据（包括用户档案属性和组成员关系）可以保留在发布层上。 在[注册、登录和用户配置文件文档](/help/sites-cloud/authoring/personalization/user-and-group-sync-for-publish-tier.md)中了解有关此功能的更多信息。

### SDK内部版本分析程序 {#analyzers}

AEM as a Maven SDK Build Analyzer Maven插件可检测Maven项目中的问题，包括缺少依赖项。 它使开发人员有机会在本地开发过程中发现问题，而且在使用Cloud Manager部署到云环境之前就已经很早。 有关更多信息，请参阅文档[此处](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html?lang=en#developing)和[此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=en#building-for-the-sdk)。

### 其他 {#others-foundation}

新的[&quot;httpd -t&quot;语法](/help/implementing/dispatcher/disp-overview.md#local-validation)检查在Cloud Manager生成期间执行的Apache和Dispatcher配置，这些配置也可以使用AEM作为Cloud ServiceSDK的Dispatcher工具运行。

## 内容传输工具 {#content-transfer-tool}

请阅读本节内容，了解[内容传输工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html)版本v1.1.12的新增功能和更新。

### 新增功能 {#what-is-new-ctt}

* 改进了日志的用户体验。 提取和摄取日志中添加了时间戳。 添加了消息，以指示日志是否为空。

### 错误修复 {#ctt-bug-fixes}

* 如果迁移集包含的路径具有部分相似的文件名，则内容传输工具会跳过内容文件。 此问题已修复。

## 最佳实践分析器{#best-practices-analyzer}

### 发布日期 {#release-date-bpa}

Best Practices Analyzer的发布日期是2020年11月13日。

### [!DNL Best Practices Analyzer] {#what-is-new-bpa}的新增功能

* Cloud Readiness Analyzer现在更名为Best Practices Analyzer(BPA)。 BPA可对您当前的AEM实施进行最佳实践评估，并帮助评估从现有AEM实例移动到AEM as a Cloud Service的准备情况。

* 添加了新的检测器来检测`java.io.InputStream`的使用情况，如果在AEM中用作Cloud Service，则可能会导致问题。

### 错误修复 {#bpa-bug-fixes}

* 修复了导致与&#x200B;*textfield foundation*&#x200B;组件相关的正值的错误。
