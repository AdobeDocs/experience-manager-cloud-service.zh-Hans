---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2020.12.0 版的发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2020.12.0 版的发行说明。'
exl-id: 16875180-1f23-477d-9d4d-e220998c4983
source-git-commit: aeee895e4a4b959125d08091619988d0ffa09ace
workflow-type: tm+mt
source-wordcount: '693'
ht-degree: 6%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 版的发行说明 {#release-notes}

以下部分概述了[!DNL Experience Manager]作为Cloud Service的常规发行说明。

## 发布日期 {#release-date}

[!DNL Adobe Experience Manager] as aCloud Service2020.12.0的发布日期是2020年12月17日。
以下版本(2021.1.0)将于2021年1月28日发布。

## [!DNL Adobe Experience Manager Sites] 作为Cloud Service {#sites}

* **[内容片段HTTP API](/help/assets/content-fragments/assets-api-content-fragments.md)**:添加使用HTTP API添加/更新和删除内容片段变量的功能。

## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

* 与[!DNL Adobe InDesign Server]的集成现在可用于[!DNL Experience Manager]作为[!DNL Cloud Service]。 它提供使用[!DNL Adobe InDesign Server]脚本处理[!DNL Adobe InDesign]文件的自动化功能，并允许用户使用[!DNL Assets]模板用户界面创建小册子或广告。 [!DNL Experience Manager as a Cloud Service]仅支持由[!DNL Adobe Managed Services]托管的[!DNL InDesign Server]。 <!-- TBD: Add link to article. -->

* [!DNL Experience Manager] 增强了功能，可在远程部署中使用资产时跟踪和显示资 [!DNL Experience Manager Sites] 产引用。资产[!UICONTROL 属性]页面中新的[!UICONTROL 引用]选项卡现在列出了资产的本地和远程引用。 该引用允许DAM用户跟踪[!DNL Sites]页面和[!DNL Assets]复合资产中的资产使用情况。 请参阅[配置和使用连接的资产](/help/assets/use-assets-across-connected-assets-instances.md)。

* [!DNL Dynamic Media] 功能现在可通过基 [!DNL Sites] 于图像的核心组件访问。作者可以在创建网页时快速配置组件，以使用图像预设、智能裁剪和图像修改工具。 请参阅[核心组件2.13.0版本](https://github.com/adobe/aem-core-wcm-components/releases/tag/core.wcm.components.reactor-2.13.0)。

* [!DNL Experience Manager] 桌面应用程序允许用户通过从桌面应用程序界面上的Windows资源管理器或Mac“访达”中拖动文件来上传文件和文件夹。请参阅[使用桌面应用程序添加资产](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#upload-and-add-new-assets-to-aem)。

## Adobe Experience Manager Commerce as aCloud Service{#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* 已发布CIF Venia参考网站 — 2020.12.01，其中包含最新的CIF核心组件版本v1.6.0。有关更多详细信息，请参阅[CIF Venia参考网站](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.12.01)。

* 已发布CIF核心组件v1.6.0。有关更多详细信息，请参阅[CIF核心组件](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.6.0)。

## Cloud Manager {#cloud-manager}

### 发布日期 {#release-date-cm}

AEM as a Cloud Manager在as a Cloud Service中的发布日期2020.12.0是2020年12月10日。

### [!DNL Cloud Manager] {#what-is-new-cm}的新增功能

* 对[SSL证书](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md)和[自定义域名](/help/implementing/cloud-manager/custom-domain-names/introduction.md)进行自助服务管理。

* [IP允许列表的自助服务管理](/help/implementing/cloud-manager/ip-allow-lists/introduction.md)。

* 更新了&#x200B;**环境**&#x200B;详细信息页面现在允许用户管理其环境中的自定义域名和IP允许列表。

### 错误修复 {#bug-fixes-cloud-manager}

* 在代码扫描阶段出现一些故障，但未提供已解决的结果。

* 环境卡显示&#x200B;**Add**&#x200B;按钮时显示不一致。

## 代码重构工具 {#code-refactoring-tools}

### [!DNL Code Refactoring Tools] {#what-is-new-crt}的新增功能

* 已发布新版AIO-CLI插件。 此插件的最新版本包括针对AEM Dispatcher Converter和Repository Modernizer的错误修复，并且还支持新的实用程序 — 索引转换器。 请参阅[统一体验](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/unified-experience.html?lang=en#benefits)以了解有关此插件的更多信息。

* 索引转换器是一个实用程序，可用于将客户的自定义OAK索引定义转换为AEM作为与Cloud Service兼容的OAK索引定义。 有关更多详细信息，请参阅[索引转换器](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/index-converter)。

* 向[Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer)添加的新功能，该功能可创建单独的包`ui.config`以包含所有OSGi配置。

### 错误修复 {#crt-bug-fixes}

* 对AEM Dispatcher Converter和Repository Modernizer工具进行了若干错误修复。 请参阅[AEM Dispatcher Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter)和[Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer)。

### 发布日期 {#release-date-ctt}

内容传输工具v1.1.20的发布日期是2021年1月8日。

### [!DNL Content Transfer Tool] {#what-is-new-ctt}的新增功能

* 用户现在可以通过将鼠标悬停在内容传输工具(CTT)用户界面的状态图标上来了解其访问令牌是否已过期。 此外，在迁移集详细信息UI中，还会通知他们无法连接到其Cloud Service实例。

### 错误修复 {#ctt-bug-fixes}

* 迁移集的内容传输工具(CTT)用户界面状态在一段时间不活动后不会持续并更改。 此问题已修复。
* 如果日志不可用，则用于查看日志的选项会被禁用。 此问题已修复，并且已添加消息来通知用户日志缺失的原因。
* 内容传输工具用户界面状态在用户停止摄取时显示&#x200B;*失败*。 此问题已修复，改为显示&#x200B;*STOPPED*。
