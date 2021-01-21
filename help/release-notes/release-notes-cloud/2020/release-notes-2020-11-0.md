---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2020.11.0 版的发行说明。'
description: '[!DNL Adobe Experience Manager] cloud service发行说明。'
translation-type: tm+mt
source-git-commit: 13774cc8684166c98f85bf4096d2c7de8d257746
workflow-type: tm+mt
source-wordcount: '1269'
ht-degree: 4%

---


# [!DNL Adobe Experience Manager] as a Cloud Service 版的发行说明 {#release-notes}

以下部分概述了作为Cloud Service的[!DNL Experience Manager]的一般发行说明。

## 发布日期 {#release-date}

[!DNL Adobe Experience Manager]作为Cloud Service2020.11.0的发布日期为2020年12月2日。
以下版本(2020.12.0)将于2020年12月17日发布

## [!DNL Adobe Experience Manager Sites] 作为Cloud Service  {#sites}

### [!DNL Sites] {#what-is-new-sites}中的新增功能

* **[启动层次结构管理](/help/sites-cloud/authoring/launches/managing-pages.md) 和 [未来时间扭曲](/help/sites-cloud/authoring/launches/preview.md)**:用于在启动项内添加／删除页面以及使用时间扭曲浏览站点的新UI显示启动项中的未来状态。

* **[扩展内容片段模型和编辑器](/help/assets/content-fragments/content-fragments-models.md)**:新的选项可用于各种数据类型的输入验证，新的表单可视化功能改进了明细列表数据类型，内容片段模型名称在资产UI中显示并可搜索。

* **对可用于转出的Live Copy页面进行排序**:使用“名称”、“上次修改日期”和“上次转出日期”属性对可 [!UICONTROL 用于转出]的Live Copy页 [!UICONTROL 面进行排序的新]  选项。页面的[!UICONTROL 上次转出日期]是引入的新属性。

## [!DNL Adobe Experience Manager Assets] 作为Cloud Service  {#assets}

### [!DNL Assets]和[!DNL Dynamic Media] {#what-is-new-assets}的新增功能

* **批量资产摄取**:为客户提供可扩展的、云本地摄取服务，该服 [!DNL Experience Manager] 务利用Cloud Service架构（包括资产微服务）。主要用例包括通过监控、报告和计划进行大规模摄取，同时允许使用通用云上传工具将资产初始传输到云数据存储。 请参阅[资产批量收录工具](/help/assets/add-assets.md#asset-bulk-ingestor)。

   此工具适用于系统管理员、顾问或实施合作伙伴角色。 此功能允许进行大规模摄取，最好在初始摄取或偶尔进行大型摄取时使用。 对于较小的摄取作业，请使用资产用户界面](/help/assets/add-assets.md#upload-assets)上传[[!DNL Experience Manager] 桌面应用程序](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/introduction.html?lang=en)或[。

   ![批量导入程序配置](/help/assets/assets/bulk-import-config-low-res.png)

* 用户现在可以在卡片和列视图中对数字资产进行排序。

   ![排序资产](/help/assets/assets/asset-sort-options.png)

* 对此版本中[!DNL Experience Manager Assets]的辅助功能进行了以下增强。 有关详细信息，请参阅 [!DNL Assets]](/help/assets/accessibility.md)中的[辅助功能。

   * 使用键盘导航时间轴时，Esc键可以折叠“显示全部”选项而不失焦点。
   * 使用键盘Tab键导航时，在从添加的标记中删除最后一个标记后，标记字段将保留焦点。
   * [!DNL Experience Manager] 组件现在包含屏幕阅读器要使用的名称、角色和值的适当信息。
   * 删除“类型／大小”组合框、“链接”组合框、“语言”组合框或“文本”编辑框后，键盘焦点将返回到下一个或上一个用户界面元素或更相关的用户界面元素。
   * 将指针悬停在选项上时，将显示“选择”和“下载”等提示。 使用屏幕放大镜的用户可能看不到文件缩略图，因为这些提示。 现在，在使用`Escape`键删除选项后，可以保留焦点。
   * 从页面中出现的网格中选择网格单元格后，焦点将转移到屏幕上显示的操作栏。
   * 可视用户可以区分普通文本和链接，因为在[!DNL Experience Manager]主页中，将显示可视提示（下划线和V形图标），用于链接到所有解决方案。

* **Dynamic Media的批集预设**:现在，您可以在将资产文件单独或使用批量摄取上传到文件夹时，自动创建和组织图像集或旋转集中的多个资产。

   请参阅[关于批集预设](/help/assets/dynamic-media/batch-set-presets-dm.md)。

* [!DNL Dynamic Media]中现在提供以下辅助功能增强功能：

   * 屏幕阅读器(JAWS,Narrator)在“嵌入大小”菜单选项中对菜单项的名称、角色和状态进行解说。
   * 用户可以使用`Tab`键导航“电子邮件链接”对话框。
   * 考虑到屏幕阅读器的增强功能，创建视频编码用户档案的工作流程更为用户友好。
   * 使用`Tab`键导航时，焦点将移至工作流中相应的用户界面元素，以创建交互式视频。
   * “发布”页、“编辑资产”页、“编辑智能裁切”页和“图像集编辑器”页经过改进，符合Web标准。 辅助型技术(AT)用户现在可以轻松导航这些页面并执行裁剪图像等操作。
   * 对查看器进行了改进，使用户能够使用键盘进行导航。
   * 键盘和屏幕阅读器用户可以使用裁剪功能。
   * 键盘用户可以更好地管理热点。

   请参阅 [!DNL Dynamic Media]](/help/assets/dynamic-media/accessibility-dm.md)中的[辅助功能。

## Adobe Experience Manager商务作为Cloud Service{#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* 已发布CIF Venia参考站点- 2020.11.05，其中包括最新的CIF核心组件版本v1.5.0。有关更多详细信息，请参阅[CIF Venia参考站点](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.10.27)。

* 已发布CIF核心组件v1.5.0。有关更多详细信息，请参阅[CIF核心组件](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.5.0)。

### 错误修复 {#bug-fixes-commerce}

* 如果未直接在Sling CA配置中指定配置，但在父配置中指定配置，则GraphQL客户端配置无法读取正确。 已修复。

## Cloud Manager {#cloud-manager}

### 发布日期 {#release-date-cm}

AEM中Cloud Manager作为Cloud Service2020.11.0的发布日期为2020年11月12日。

### [!DNL Cloud Manager] {#what-is-new-cm}中的新增功能

* 现在，用户可从&#x200B;**环境**&#x200B;卡和&#x200B;**环境**&#x200B;摘要页上的环境菜单选项使用新的菜单选项&#x200B;**本地登录**。
有关详细信息，请参阅[管理环境](/help/implementing/cloud-manager/manage-environments.md##login-locally)。

* Cloud Manager中的&#x200B;**Learn**&#x200B;选项卡已用UI中的新图像刷新。

### 错误修复 {#bug-fixes-cloud-manager}

* 需要下载Maven插件，才能加载执行构建之前完成的依赖项。
* 现在，从Cloud Manager页脚中选择语言的链接将导航到正确的位置。
* 有时，在代码扫描过程中，SonarQube进程不会开始。 现在将自动检测并尝试重新启动。
* 所有现有的生产管道都将通过体验审核步骤自动启用。

## Adobe Experience Manager as a Cloud Service 基础 {#cloud-service-foundation}

### 工作流 {#workflows}

* 增加了根据工作流标题、工作流模型、状态、发起者、有效负荷路径和开始日期搜索工作流实例的支持。 请参阅[搜索工作流实例](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/sites/administering/workflows-administering.html)。

### 发布层用户数据同步{#user-sync}

* 用户数据(包括用户档案属性和组成员关系)可以保留在发布层上。 在[注册、登录和用户用户档案文档](/help/sites-cloud/authoring/personalization/user-and-group-sync-for-publish-tier.md)中了解有关此功能的更多信息。

### SDK Build Analyzers {#analyzers}

AEM作为Cloud ServiceSDK构建分析器主插件可检测主项目中的问题，包括缺少依赖项。 它为开发人员提供了在本地开发过程中发现问题的机会，而且很早之后，您就可以使用Cloud Manager部署到云环境。 有关详细信息，请参阅文档[此处](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html?lang=en#developing)和[此处](https://experienceleague.corp.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=en#building-for-the-sdk)。

### 其他 {#others-foundation}

新的[&quot;httpd -t&quot;语法](/help/implementing/dispatcher/disp-overview.md#local-validation)检查在Cloud Manager构建过程中执行的apache和调度程序配置，也可以使用AEM作为Cloud ServiceSDK的调度程序工具运行该配置。

## 内容传输工具 {#content-transfer-tool}

可查看本节以了解[内容传输工具](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html)版本1.1.12的新增功能和更新。

### 新增功能 {#what-is-new-ctt}

* 改进了日志的用户体验。 添加到提取和摄取日志的时间戳。 添加的消息，指示日志是否为空。

### 错误修复 {#ctt-bug-fixes}

* 如果迁移集包含的路径与文件名部分相似，则内容传输工具将跳过内容文件。 已修复。

## 最佳实践分析器{#best-practices-analyzer}

### 发布日期 {#release-date-bpa}

最佳实践分析器发布日期为2020年11月13日。

### [!DNL Best Practices Analyzer] {#what-is-new-bpa}中的新增功能

* 云就绪性分析器现在是最佳实践分析器(BPA)。 BPA为您当前的AEM实施提供最佳实践评估，并帮助评估从现有AEM实例迁移到AEM作为Cloud Service的准备情况。

* 添加了新的检测器以检测`java.io.InputStream`的使用，如果在AEM中作为Cloud Service使用，则会导致问题。

### 错误修复 {#bpa-bug-fixes}

* 修复了导致与&#x200B;*textfield foundation*&#x200B;组件相关的正面错误。
