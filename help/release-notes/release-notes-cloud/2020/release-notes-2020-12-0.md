---
title: 作为Cloud Service的 [!DNL Adobe Experience Manager] 当前发行说明。
description: 作为Cloud Service的 [!DNL Adobe Experience Manager] 当前发行说明。
translation-type: tm+mt
source-git-commit: 6ea94126d29a470820ee1dc39b239bb10951afac
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 4%

---


# [!DNL Adobe Experience Manager] as a Cloud Service 版的发行说明 {#release-notes}

以下部分概述了作为Cloud Service的[!DNL Experience Manager]的一般发行说明。

## 发布日期 {#release-date}

[!DNL Adobe Experience Manager]作为Cloud Service2020.12.0的发布日期为2020年12月17日。
以下版本(2021.1.0)将于2021年1月28日发布。

## [!DNL Adobe Experience Manager Sites] 作为Cloud Service  {#sites}

* **[内容片段HTTP API](/help/assets/content-fragments/assets-api-content-fragments.md)**:添加使用HTTP API添加／更新和删除内容片段变体的功能。

## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

* 现在，与[!DNL Adobe InDesign Server]集成可用于[!DNL Experience Manager]作为[!DNL Cloud Service]。 它提供使用[!DNL Adobe InDesign Server]脚本处理[!DNL Adobe InDesign]文件的自动化，并允许用户使用[!DNL Assets]模板用户界面创建小册子或广告。 [!DNL Experience Manager as a Cloud Service]仅支持由[!DNL Adobe Managed Services]托管的[!DNL InDesign Server]。 <!-- TBD: Add link to article. -->

* [!DNL Experience Manager] 该功能经过增强，可在使用已连接资产功能在远程部署中使用资产时 [!DNL Experience Manager Sites] 跟踪和显示资产引用。资产的[!UICONTROL 属性]页面中新增的[!UICONTROL 引用]选项卡现在会列表资产的本地和远程引用。 引用允许DAM用户跟踪[!DNL Sites]页面和[!DNL Assets]复合资产中的资产使用情况。 请参阅[配置和使用连接的资产](/help/assets/use-assets-across-connected-assets-instances.md)。

* [!DNL Dynamic Media] 现在可通过基于图像 [!DNL Sites] 的核心组件访问这些功能。作者可以在创建网页时快速配置组件以使用图像预设、智能裁剪和图像修饰符。 请参阅[核心组件2.13.0版本](https://github.com/adobe/aem-core-wcm-components/releases/tag/core.wcm.components.reactor-2.13.0)。

* [!DNL Experience Manager] 桌面应用程序允许用户通过从Windows资源管理器或桌面应用程序界面上的Mac Finder拖动文件来上传文件和文件夹。请参阅[使用桌面应用程序](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#upload-and-add-new-assets-to-aem)添加资产。

## Adobe Experience Manager商务作为Cloud Service{#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* 已发布CIF Venia参考站点- 2020.12.01，其中包括最新的CIF核心组件版本v1.6.0。有关更多详细信息，请参阅[CIF Venia参考站点](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.12.01)。

* 已发布CIF核心组件v1.6.0。有关更多详细信息，请参阅[CIF核心组件](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.6.0)。

## Cloud Manager {#cloud-manager}

### 发布日期 {#release-date-cm}

AEM中Cloud Manager作为Cloud Service2020.12.0的发布日期为2020年12月10日。

### [!DNL Cloud Manager] {#what-is-new-cm}中的新增功能

* 对[SSL证书](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md)和[自定义域名](/help/implementing/cloud-manager/custom-domain-names/introduction.md)进行自助管理。

* [IP允许列表](/help/implementing/cloud-manager/ip-allow-lists/introduction.md)的自助服务管理。

* 更新的&#x200B;**环境**&#x200B;详细信息页面现在允许用户管理其环境上的自定义域名和IP允许列表。

### 错误修复 {#bug-fixes-cloud-manager}

* 在代码扫描阶段发生的一些故障没有提供已解决的结果。

* 环境卡显示&#x200B;**添加**&#x200B;按钮时不一致。

## 代码重构工具 {#code-refactoring-tools}

### [!DNL Code Refactoring Tools] {#what-is-new-crt}中的新增功能

* 已发布新版AIO-CLI插件。 此插件的最新版本包括AEM Dispatcher Converter和Repository Modernizer的错误修复，还支持新的实用程序——索引转换器。 请参阅[统一体验](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/unified-experience.html?lang=en#benefits)以进一步了解此插件。

* Index Converter是一个实用程序，可用于将客户的自定义OAK索引定义转换为AEM作为Cloud Service兼容的OAK索引定义。 有关详细信息，请参阅[索引转换器](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/index-converter)。

* 添加到[存储库Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer)的新功能，该功能创建单独的包`ui.config`以包含所有OSGi配置。

### 错误修复 {#crt-bug-fixes}

* 对AEM Dispatcher Converter和Repository Modernizer工具执行了若干错误修复。 请参阅[AEM Dispatcher Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter)和[存储库Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer)。
