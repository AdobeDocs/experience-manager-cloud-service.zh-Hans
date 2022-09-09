---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 2020.11.0 版的发行说明。'
description: '"[!DNL Adobe Experience Manager] as a Cloud Service的2020.11.0发行说明。”'
exl-id: 8066c0fb-c2f5-4625-9448-b0c74ff4e192
source-git-commit: bc4da79735ffa99f8c66240bfbfd7fcd69d8bc13
workflow-type: tm+mt
source-wordcount: '1265'
ht-degree: 10%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 版的发行说明  {#release-notes}

以下部分概述了 [!DNL Experience Manager] as a Cloud Service。

## 发布日期 {#release-date}

的发行日期 [!DNL Adobe Experience Manager] as a Cloud Service 2020.11.0是2020年12月2日。
以下版本(2020.12.0)将于2020年12月17日发布

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

### [!DNL Sites] 的新增功能 {#what-is-new-sites}

* **[启动层次结构管理](/help/sites-cloud/authoring/launches/managing-pages.md) &amp; [未来时间扭曲](/help/sites-cloud/authoring/launches/preview.md)**:新的UI用于在启动项内添加/删除页面，以及使用时间扭曲浏览网站时，会显示启动项中的未来状态。

* **[扩展内容片段模型和编辑器](/help/assets/content-fragments/content-fragments-models.md)**:可对各种数据类型进行输入验证的新选项，通过新的表单可视化图表改进了枚举数据类型，并且在资产UI中显示和搜索内容片段模型名称。

* **对可用于转出的Live Copy页面进行排序**:新选项，用于使用 [!UICONTROL 名称], [!UICONTROL 上次修改日期]和 [!UICONTROL 上次转出日期] 属性。 的 [!UICONTROL 上次转出日期] 对于页面，是引入的新属性。

## [!DNL Adobe Experience Manager Assets] as a Cloud Service {#assets}

### 的新增功能 [!DNL Assets] 和 [!DNL Dynamic Media] {#what-is-new-assets}

* **批量资产摄取**:为客户提供可扩展的云原生摄取服务，该服务可利用 [!DNL Experience Manager] as a Cloud Service架构，包括资产微服务。 主要用例包括通过监控、报告和计划进行大规模摄取，同时允许使用常用的云上传工具将资产初始传输到云数据存储区。 请参阅 [资产批量摄取工具](/help/assets/add-assets.md#asset-bulk-ingestor).

   此工具适用于系统管理员、顾问或实施合作伙伴角色。 此功能允许进行大规模摄取，理想情况下是在初始摄取或偶尔进行大型摄取时使用。 对于较小的摄取作业，请使用 [[!DNL Experience Manager] 桌面应用程序](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/introduction.html?lang=en) 或 [使用Assets用户界面上传](/help/assets/add-assets.md#upload-assets).

   ![批量导入程序的配置](/help/assets/assets/bulk-import-config-low-res.png)

* 用户现在可以在卡片视图和列视图中对数字资产进行排序。

   ![排序资产](/help/assets/assets/asset-sort-options.png)

* 对中的辅助功能进行了以下增强 [!DNL Experience Manager Assets] 在此版本中。 有关更多信息，请参阅 [辅助功能 [!DNL Assets]](/help/assets/accessibility.md).

   * 使用键盘导航时间轴时，Esc键可以折叠“显示全部”选项，而不会失去焦点。
   * 使用键盘选项卡键导航时，在从添加的标记中删除最后一个标记后，标记字段会保留焦点。
   * [!DNL Experience Manager] 组件现在包含要由屏幕阅读器使用的名称、角色和值的适当信息。
   * 删除“类型/大小”组合框、“链接”组合框、“语言”组合框或“文本编辑”框后，键盘焦点将返回到下一个或上一个用户界面元素或更相关的用户界面元素。
   * 将指针悬停在选项上时，会显示“选择”和“下载”等提示。 使用屏幕放大镜的用户可能看不到文件缩略图，因为这些提示。 现在，在使用删除选项后，可以保留焦点 `Escape` 键。
   * 从页面中存在的网格中选择网格单元格后，焦点将转移到屏幕上显示的操作栏。
   * 可视化用户可以区分普通文本和链接，因为在中，将显示指向所有解决方案的链接的可视线索（下划线和V形图标） [!DNL Experience Manager] 主页。

* **Dynamic Media中的批集预设**:现在，在您将资产文件单独或使用批量摄取功能上传到文件夹时，您可以自动创建和组织图像集或旋转集中的多个资产。

   请参阅 [关于批集预设](/help/assets/dynamic-media/batch-set-presets-dm.md).

* 现在，中提供了以下辅助功能增强功能 [!DNL Dynamic Media]:

   * 屏幕阅读器(JAWS、Narrator)在“嵌入大小”菜单选项中讲述菜单项的名称、角色和状态。
   * 用户可以使用 `Tab` 键。
   * 鉴于屏幕阅读器增强功能，创建视频编码配置文件的工作流更易于用户使用。
   * 使用 `Tab` 键，焦点会移至工作流中相应的用户界面元素以创建交互式视频。
   * 对“发布”页面、“编辑资产”页面、“编辑智能裁剪”页面和“图像集编辑器”页面进行了改进，以符合Web标准。 辅助技术(AT)用户现在可以轻松导航这些页面并执行裁剪图像等操作。
   * 对查看器进行了改进，允许用户使用键盘进行导航。
   * 键盘和屏幕阅读器用户可以使用裁剪功能。
   * 键盘用户可以更好地管理热点。

   请参阅 [中的辅助功能 [!DNL Dynamic Media]](/help/assets/dynamic-media/accessibility-dm.md).

## Adobe Experience Manager商务as a Cloud Service {#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* 已发布CIF Venia参考网站 — 2020.11.05，其中包括最新的CIF核心组件版本v1.5.0。请参阅 [CIF Venia参考网站](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.10.27) 以了解更多详细信息。

* 已发布CIF核心组件v1.5.0。请参阅 [CIF核心组件](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.5.0) 以了解更多详细信息。

### 错误修复 {#bug-fixes-commerce}

* 如果未在Sling CA配置中直接指定配置，但在其中一个父配置中指定配置，则无法正确读取GraphQL客户端配置。 此问题已得到修复。

## Cloud Manager {#cloud-manager}

### 发布日期 {#release-date-cm}

AEMas a Cloud Service中Cloud Manager的发行日期为2020.11.0 2020年11月12日。

### [!DNL Cloud Manager] 的新增功能 {#what-is-new-cm}

* 新菜单选项 **本地登录** 现在，用户可从 **环境** 卡片和 **环境** 摘要页面。
有关更多详细信息，请参阅[管理环境](/help/implementing/cloud-manager/manage-environments.md#login-locally)。

* 的 **学习** 选项卡，此选项卡已在UI中刷新为新图像。

### 错误修复 {#bug-fixes-cloud-manager}

* 需要下载Maven插件，才能加载执行生成之前完成的依赖项。
* 现在，Cloud Manager页脚中用于选择语言的链接将导航到正确的位置。
* 有时，在代码扫描期间，SonarQube进程不会启动。 现在将自动检测并尝试重新启动。
* 所有现有的生产管道都将通过体验审核步骤自动启用。

## Adobe Experience Manager as a Cloud Service 基础 {#cloud-service-foundation}

### 工作流 {#workflows}

* 添加了基于工作流标题、工作流模型、状态、启动器、有效负荷路径和开始日期的用于搜索工作流实例的支持。 请参阅 [搜索工作流实例](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/administering/workflows-administering.html).

### 发布层用户数据同步 {#user-sync}

* 用户数据（包括用户档案属性和组成员关系）可以保留在发布层上。 在 [注册、登录和用户配置文件文档](/help/sites-cloud/authoring/personalization/user-and-group-sync-for-publish-tier.md).

### SDK 内部版本分析程序 {#analyzers}

AEM as a Cloud Service SDK 生成分析器 Maven 插件可检测 Maven 项目中的问题，包括缺少依赖项的问题。 它使开发人员有机会在使用 Cloud Manager 部署到云环境之前，在本地开发期间发现问题。有关更多信息，请参阅此文档 [此处](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html?lang=zh-Hans#developing) 和 [此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=en#building-for-the-sdk).

### 其他 {#others-foundation}

新建 [&quot;httpd -t&quot;语法](/help/implementing/dispatcher/disp-overview.md#local-validation) 检查在Cloud Manager生成期间执行的apache和dispatcher配置，该配置也可以使用AEMas a Cloud ServiceSDK的Dispatcher工具运行。

## 内容转移工具 {#content-transfer-tool}

请阅读本节内容，了解的新增功能和更新 [内容传输工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html) 版本1.1.12。

### 新增功能 {#what-is-new-ctt}

* 改进了日志的用户体验。 提取和摄取日志中添加了时间戳。 添加了消息，以指示日志是否为空。

### 错误修复 {#ctt-bug-fixes}

* 如果迁移集包含的路径具有部分相似的文件名，则内容传输工具会跳过内容文件。 此问题已得到修复。

## Best Practices Analyzer {#best-practices-analyzer}

### 发布日期 {#release-date-bpa}

Best Practices Analyzer的发布日期是2020年11月13日。

### [!DNL Best Practices Analyzer] 的新增功能 {#what-is-new-bpa}

* Cloud Readiness Analyzer现在更名为Best Practices Analyzer(BPA)。 BPA可对您当前的AEM实施进行最佳实践评估，并帮助评估从现有AEM实例迁移到AEM as a Cloud Service的准备情况。

* 添加了新的检测器以检测 `java.io.InputStream`，在AEMas a Cloud Service中使用时可能会导致问题。

### 错误修复 {#bpa-bug-fixes}

* 导致与 *textfield foundation* 组件已修复。
