---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 2020.11.0 版的发行说明。'
description: "[!DNL Adobe Experience Manager]个2020.11.0版as a Cloud Service发行说明。"
exl-id: 8066c0fb-c2f5-4625-9448-b0c74ff4e192
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '1223'
ht-degree: 15%

---

# [!DNL Adobe Experience Manager]as a Cloud Service的发行说明 {#release-notes}

以下部分概述了[!DNL Experience Manager]as a Cloud Service的常规发行说明。

## 发布日期 {#release-date}

[!DNL Adobe Experience Manager]as a Cloud Service2020.11.0的发布日期是2020年12月2日。
下一个版本(2020.12.0)将于2020年12月17日发布

## [!DNL Adobe Experience Manager Sites]个as a Cloud Service {#sites}

### [!DNL Sites] 的新增功能 {#what-is-new-sites}

* **[启动项层次结构管理](/help/sites-cloud/authoring/launches/managing-pages.md)和[未来时间扭曲](/help/sites-cloud/authoring/launches/preview.md)**：新的UI可在启动项中添加/删除页面，并使用“时间扭曲”浏览网站，可显示启动项的未来状态。

* **[扩展的内容片段模型和编辑器](/help/assets/content-fragments/content-fragments-models.md)**：对各种数据类型进行输入验证的新选项、通过新表单可视化效果改进的枚举数据类型，以及在Assets UI中显示和可搜索的内容片段模型名称。

* **对可用于转出的Live Copy页面进行排序**：新增选项可使用[!UICONTROL 名称]、[!UICONTROL 上次修改日期]和[!UICONTROL 上次转出日期]属性对可用于转出的Live Copy页面进行排序。 页面的[!UICONTROL 上次转出日期]是引入的新属性。

## [!DNL Adobe Experience Manager Assets]个as a Cloud Service {#assets}

### [!DNL Assets]和[!DNL Dynamic Media]的新增功能 {#what-is-new-assets}

* **批量资源摄取**：为客户提供使用[!DNL Experience Manager]as a Cloud Service架构（包括资源微服务）的可扩展、云原生摄取服务。 关键用例包括大规模的摄取，以及监控、报告和计划，同时允许使用通用云上传工具将资产初始传输到云数据存储。 请参阅[资源批量引入器工具](/help/assets/add-assets.md#asset-bulk-ingestor)。

  此工具适用于系统管理员、顾问或实施合作伙伴角色。 此功能允许进行大规模摄取，最好在初始摄取或偶尔进行大规模摄取期间使用。 对于较小的引入作业，请使用[[!DNL Experience Manager] 桌面应用程序](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/introduction.html)或使用Assets用户界面](/help/assets/add-assets.md#upload-assets)的[上传。

  ![批量导入程序的配置](/help/assets/assets/bulk-import-config-low-res.png)

* 用户现在可以在卡片视图和列视图中对数字资源进行排序。

  ![排序资源](/help/assets/assets/asset-sort-options.png)

* 在此版本中，为[!DNL Experience Manager Assets]中的辅助功能进行了以下增强。 有关详细信息，请参阅 [!DNL Assets]](/help/assets/accessibility.md)中的[辅助功能。

   * 使用键盘导航时间轴时，Esc键可以折叠显示全部选项而不会失去焦点。
   * 使用键盘Tab键导航时，从添加的标记中删除最后一个标记后，标记字段将保持焦点。
   * [!DNL Experience Manager]组件现在包含屏幕阅读器使用的名称、角色和值的相应信息。
   * 删除“类型/大小”组合框、“链接”组合框、“语言”组合框或“文本”编辑框后，键盘焦点将返回到下一个或上一个用户界面元素，或者返回到更相关的用户界面元素。
   * 当指针悬停在选项上时，将显示“选择”和“下载”等提示。 由于这些提示，使用屏幕放大镜的用户可能无法看到文件缩略图。 现在，在使用`Escape`键删除选项后，可以保留焦点。
   * 从页面中显示的网格中选择网格单元格时，焦点会转移到屏幕上显示的操作栏。
   * 可视用户可以区分普通文本和链接，因为可视线索（下划线和V形图标）会显示到[!DNL Experience Manager]主页中所有解决方案的链接。

* **Dynamic Media中的批次集预设**：现在，您可以在单独或使用批量摄取将资源文件上传到文件夹时，自动在图像集或旋转集中创建和组织多个资源。

  请参阅[关于批次集预设](/help/assets/dynamic-media/batch-set-presets-dm.md)。

* [!DNL Dynamic Media]中现在提供了以下辅助功能增强功能：

   * 屏幕阅读器（JAWS、讲述人）在“嵌入大小”菜单选项中讲述菜单项的名称、角色和状态。
   * 用户可以使用`Tab`键导航电子邮件链接对话框。
   * 鉴于屏幕阅读器增强功能，创建视频编码配置文件的工作流对用户更加友好。
   * 使用`Tab`键导航时，焦点将移动到工作流中相应的用户界面元素，以创建交互式视频。
   * 改进了“Publish”页面、“编辑资产”页面、“编辑智能裁剪”页面和“图像集编辑器”页面，以符合Web标准。 现在，辅助技术(AT)用户可以轻松地导航这些页面并在其上执行操作，如裁切图像。
   * 改进了查看器，以允许用户使用键盘导航。
   * 键盘和屏幕阅读器用户可以使用裁切功能。
   * 键盘用户可以更好地管理热点。

  查看 [!DNL Dynamic Media]](/help/assets/dynamic-media/accessibility-dm.md)中的[辅助功能。

## Adobe Experience Manager Commerceas a Cloud Service {#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* 发布了CIF Venia参考网站 — 2020.11.05，其中包括最新的CIF核心组件版本v1.5.0。有关详细信息，请参阅[CIF Venia引用站点](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.10.27)。

* 已发布CIF核心组件v1.5.0。有关详细信息，请参阅[CIF核心组件](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.5.0)。

### 错误修复 {#bug-fixes-commerce}

* 如果未直接在Sling CA配置中指定配置，但未在其中一个父配置中指定配置，则GraphQL客户端配置无法正确读取。 此问题已得到修复。

## Cloud Manager {#cloud-manager}

### 发布日期 {#release-date-cm}

AEM as a Cloud Service 2020.11.0 中的 Cloud Manager 的发布日期是 2020 年 11 月 12 日。

### [!DNL Cloud Manager] 的新增功能 {#what-is-new-cm}

* 用户现在可以从&#x200B;**环境**&#x200B;卡和&#x200B;**环境**&#x200B;摘要页面上的环境菜单选项中使用新的菜单选项&#x200B;**本地登录**。
有关详细信息，请参阅[管理环境](/help/implementing/cloud-manager/manage-environments.md#login-locally)。

* Cloud Manager 中的&#x200B;**学习**&#x200B;选项卡已在 UI 中用新图像刷新。

### 错误修复 {#bug-fixes-cloud-manager}

* 在构建执行之前完成的依赖项加载需要下载 Maven 插件。
* Cloud Manager 页脚中用于选择语言的链接现在将导航到正确的位置。
* 有时在代码扫描期间，SonarQube 进程不会启动。 现在将自动检测并尝试重新启动。
* 所有现有生产管道都会通过体验审核步骤自动启用。

## Adobe Experience Manager as a Cloud Service 基础 {#cloud-service-foundation}

### 工作流 {#workflows}

* 添加了基于工作流标题、工作流模型、状态、启动器、有效负荷路径和开始日期的用于搜索工作流实例的支持。 请参阅[搜索工作流实例](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/administering/workflows-administering.html)。

### Publish层用户数据同步 {#user-sync}

* 用户数据（包括用户档案属性和组成员资格）可以保留在发布层上。 在[注册、登录和用户配置文件文档](/help/sites-cloud/authoring/personalization/user-and-group-sync-for-publish-tier.md)中了解有关此功能的更多信息。

### SDK 内部版本分析程序 {#analyzers}

AEM as a Cloud Service SDK 生成分析器 Maven 插件可检测 Maven 项目中的问题，包括缺少依赖项的问题。 它使开发人员有机会在使用Cloud Manager部署到云环境之前，在本地开发期间发现问题。 有关详细信息，请参阅文档[此处](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html?lang=zh-Hans#developing)和[此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-as-a-cloud-service-sdk.html#building-for-the-sdk)。

### 其他  {#others-foundation}

新增了[&quot;httpd -t&quot;语法](/help/implementing/dispatcher/disp-overview.md#local-validation)以检查在Cloud Manager构建期间执行的Apache和Dispatcher配置，这些配置也可以使用AEM as a Cloud Service SDK的Dispatcher Tools运行。

## 内容传输工具 {#content-transfer-tool}

阅读本节内容，了解[内容传输工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html)版本v1.1.12的新增功能和更新。

### 新增功能 {#what-is-new-ctt}

* 改进了日志的用户体验。 已将“时间戳”添加到提取和摄取日志。 添加了消息，以指示日志是否为空。

### 错误修复 {#ctt-bug-fixes}

* 如果迁移集包含的路径具有部分相似的文件名，则内容传输工具将跳过内容文件。 此问题已得到修复。

## Best Practices Analyzer {#best-practices-analyzer}

### 发布日期 {#release-date-bpa}

Best Practices Analyzer的发布日期是2020年11月13日。

### [!DNL Best Practices Analyzer] 的新增功能 {#what-is-new-bpa}

* Cloud Readiness Analyzer现在更名为Best Practices Analyzer (BPA)。 BPA可以为您当前的AEM实施提供最佳实践评估，并帮助您评估从现有AEM实例迁移至AEM as a Cloud Service的准备工作。

* 已添加新的检测器来检测`java.io.InputStream`的使用，如果将其用于AEM as a Cloud Service，则可能会导致问题。

### 错误修复 {#bpa-bug-fixes}

* 修复了导致与&#x200B;*textfield foundation*&#x200B;组件相关的积极值的错误。
