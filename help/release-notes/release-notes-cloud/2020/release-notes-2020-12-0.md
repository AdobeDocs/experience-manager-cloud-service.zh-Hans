---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 2020.12.0 版的发行说明。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 2020.12.0 版的发行说明。'
exl-id: 16875180-1f23-477d-9d4d-e220998c4983
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '652'
ht-degree: 11%

---

# [!DNL Adobe Experience Manager]as a Cloud Service的发行说明 {#release-notes}

以下部分概述了[!DNL Experience Manager]as a Cloud Service的常规发行说明。

## 发布日期 {#release-date}

[!DNL Adobe Experience Manager]as a Cloud Service2020.12.0的发布日期是2020年12月17日。
以下版本(2021.1.0)为2021年1月28日。

## [!DNL Adobe Experience Manager Sites]个as a Cloud Service {#sites}

* **[内容片段HTTP API](/help/assets/content-fragments/assets-api-content-fragments.md)**：添加使用HTTP API添加/更新和删除内容片段变体的功能。

## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

* 与[!DNL Adobe InDesign Server]的集成现在可作为[!DNL Cloud Service]用于[!DNL Experience Manager]。 它提供了使用[!DNL Adobe InDesign Server]脚本处理[!DNL Adobe InDesign]文件的自动化功能，并允许用户使用[!DNL Assets]模板用户界面创建小册子或广告。 [!DNL Experience Manager as a Cloud Service]仅支持由[!DNL Adobe Managed Services]托管的[!DNL InDesign Server]。<!-- TBD: Add link to article. -->

* [!DNL Experience Manager]已得到增强，可在远程[!DNL Experience Manager Sites]部署中使用资产时，通过“连接的Assets”功能来跟踪和显示资产引用。 资产[!UICONTROL 属性]页面中新增的[!UICONTROL 引用]选项卡现在列出了资产的本地和远程引用。 引用允许DAM用户跟踪[!DNL Sites]页面和[!DNL Assets]复合资产中的资产使用情况。 请参阅[配置和使用“连接的Assets”](/help/assets/use-assets-across-connected-assets-instances.md)。

* 现在可以通过AEM [!DNL Sites]基于图像的核心组件访问[!DNL Dynamic Media]功能。 作者可以在创建网页时快速配置组件，以使用图像预设、智能裁切和图像修饰符。 请参阅[核心组件2.13.0版本](https://github.com/adobe/aem-core-wcm-components/releases/tag/core.wcm.components.reactor-2.13.0)。

* [!DNL Experience Manager]桌面应用程序允许用户通过从桌面应用程序界面上的Windows资源管理器或Mac Finder拖动文件来上传文件和文件夹。 请参阅[使用桌面应用程序添加资源](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#upload-and-add-new-assets-to-aem)。

## Adobe Experience Manager Commerceas a Cloud Service {#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* 发布了CIF Venia参考网站 — 2020.12.01，其中包括最新的CIF核心组件版本v1.6.0。有关详细信息，请参阅[CIF Venia引用站点](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.12.01)。

* 已发布CIF核心组件v1.6.0。有关详细信息，请参阅[CIF核心组件](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.6.0)。

## Cloud Manager {#cloud-manager}

### 发布日期 {#release-date-cm}

Adobe Experience Manager (AEM) 2020.12.0as a Cloud Service中的Cloud Manager的发布日期是2020年12月10日。

### [!DNL Cloud Manager] 的新增功能 {#what-is-new-cm}

* [SSL 证书](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md)和[自定义域名](/help/implementing/cloud-manager/custom-domain-names/introduction.md)的自助管理。

* [IP 允许列表](/help/implementing/cloud-manager/ip-allow-lists/introduction.md)自助管理。

* 更新的&#x200B;**环境**&#x200B;详细信息页面现在允许用户管理其环境中的自定义域名和IP允许列表。

### 错误修复 {#bug-fixes-cloud-manager}

* 解决了在代码扫描阶段出现的一些故障但未提供结果。

* 环境信息卡未一致显示&#x200B;**添加**&#x200B;按钮。

## 代码重构工具 {#code-refactoring-tools}

### [!DNL Code Refactoring Tools] 的新增功能 {#what-is-new-crt}

* 发布了AIO-CLI插件的新版本。 此增效工具的最新版本包括对AEM Dispatcher Converter和Repository Modernizer的错误修复，并且支持新的实用程序 — 索引转换器。 请参阅[Unified Experience](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/refactoring-tools/unified-experience.html#benefits)，您可以在其中了解有关此插件的更多信息。

* 索引转换器是一个实用程序，可用于将客户的自定义Oak索引定义转换为与AEM as a Cloud Service兼容的Oak索引定义。 有关详细信息，请参阅[索引转换器](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/index-converter)。

* 添加到[Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer)的新功能可创建单独的包`ui.config`以包含所有OSGi配置。

### 错误修复 {#crt-bug-fixes}

* 对AEM Dispatcher Converter和Repository Modernizer工具进行了若干错误修复。 请参阅[AEM Dispatcher Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter)和[Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer)。

### 发布日期 {#release-date-ctt}

内容传输工具版本1.1.20的发布日期为2021年1月8日。

### [!DNL Content Transfer Tool] 的新增功能 {#what-is-new-ctt}

* 用户现在可以通过将鼠标悬停在内容传输工具(CTT)用户界面中的状态图标上来了解其访问令牌是否已过期。 此外，系统还会通知他们在迁移集详细信息UI中无法连接到其Cloud Service实例。

### 错误修复 {#ctt-bug-fixes}

* 迁移集的内容传输工具(CTT)用户界面状态在一段时间不活动后没有保留并发生了更改。 此问题已得到修复。
* 如果日志不可用，则查看日志的选项将被禁用。 此问题已修复，并且添加了消息以通知用户日志缺失的原因。
* 当用户停止引入时，内容传输工具用户界面状态显示为&#x200B;*失败*。 此问题已修复，改为显示&#x200B;*已停止*。
