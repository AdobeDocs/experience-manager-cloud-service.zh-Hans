---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 2020.12.0 版的发行说明。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 2020.12.0 版的发行说明。'
exl-id: 16875180-1f23-477d-9d4d-e220998c4983
source-git-commit: aeee895e4a4b959125d08091619988d0ffa09ace
workflow-type: tm+mt
source-wordcount: '693'
ht-degree: 10%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 版的发行说明  {#release-notes}

以下部分概述了 [!DNL Experience Manager] as a Cloud Service。

## 发布日期 {#release-date}

的发行日期 [!DNL Adobe Experience Manager] as a Cloud Service 2020.12.0是2020年12月17日。
以下版本(2021.1.0)将于2021年1月28日发布。

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

* **[内容片段HTTP API](/help/assets/content-fragments/assets-api-content-fragments.md)**:添加使用HTTP API添加/更新和删除内容片段变量的功能。

## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

* 与集成 [!DNL Adobe InDesign Server] 现在可供使用 [!DNL Experience Manager] as a [!DNL Cloud Service]. 它提供了处理的自动化 [!DNL Adobe InDesign] 文件使用 [!DNL Adobe InDesign Server] 脚本，允许用户使用 [!DNL Assets] 模板用户界面，用于创建小册子或广告。 仅 [!DNL InDesign Server] 由托管者 [!DNL Adobe Managed Services] 支持 [!DNL Experience Manager as a Cloud Service]. <!-- TBD: Add link to article. -->

* [!DNL Experience Manager] 增强了在远程中使用资产时跟踪和显示资产引用的功能 [!DNL Experience Manager Sites] 使用“连接的资产”功能进行部署。 新 [!UICONTROL 引用] 选项卡 [!UICONTROL 属性] 页面现在会列出资产的本地和远程引用。 引用允许DAM用户在 [!DNL Sites] 页面和复合资产中的 [!DNL Assets]. 请参阅 [配置和使用连接的资产](/help/assets/use-assets-across-connected-assets-instances.md).

* [!DNL Dynamic Media] 功能现在可通过 [!DNL Sites] 基于图像的核心组件。 作者可以在创建网页时快速配置组件，以使用图像预设、智能裁剪和图像修改工具。 请参阅 [核心组件2.13.0版本](https://github.com/adobe/aem-core-wcm-components/releases/tag/core.wcm.components.reactor-2.13.0).

* [!DNL Experience Manager] 桌面应用程序允许用户通过从桌面应用程序界面上的Windows资源管理器或Mac查找器中拖动文件来上传文件和文件夹。 请参阅 [使用桌面应用程序添加资产](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#upload-and-add-new-assets-to-aem).

## Adobe Experience Manager商务as a Cloud Service {#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* 已发布CIF Venia参考网站 — 2020.12.01，其中包含最新的CIF核心组件版本v1.6.0。请参阅 [CIF Venia参考网站](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.12.01) 以了解更多详细信息。

* 已发布CIF核心组件v1.6.0。请参阅 [CIF核心组件](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.6.0) 以了解更多详细信息。

## Cloud Manager {#cloud-manager}

### 发布日期 {#release-date-cm}

AEMas a Cloud Service中Cloud Manager的发布日期为2020.12.0 2020年12月10日。

### [!DNL Cloud Manager] 的新增功能 {#what-is-new-cm}

* 自助服务管理 [SSL证书](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md) 和 [自定义域名](/help/implementing/cloud-manager/custom-domain-names/introduction.md).

* 自助服务管理 [IP允许列表](/help/implementing/cloud-manager/ip-allow-lists/introduction.md).

* 已更新 **环境** 现在，“详细信息”页面允许用户在其环境中管理自定义域名和IP允许列表。

### 错误修复 {#bug-fixes-cloud-manager}

* 在代码扫描阶段出现一些故障，但未提供已解决的结果。

* 环境卡显示不一致 **添加** 按钮。

## 代码重构工具 {#code-refactoring-tools}

### [!DNL Code Refactoring Tools] 的新增功能 {#what-is-new-crt}

* 已发布新版AIO-CLI插件。 此插件的最新版本包括针对AEM Dispatcher Converter和Repository Modernizer的错误修复，并且还支持新的实用程序 — 索引转换器。 请参阅 [统一体验](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/unified-experience.html?lang=en#benefits) 了解有关此插件的更多信息。

* 索引转换器是一个实用程序，可用于将客户的自定义OAK索引定义转换为AEMas a Cloud Service兼容的OAK索引定义。 请参阅 [索引转换器](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/index-converter) 以了解更多详细信息。

* 向 [Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer) 创建单独的资源包 `ui.config` 以包含所有OSGi配置。

### 错误修复 {#crt-bug-fixes}

* 对AEM Dispatcher Converter和Repository Modernizer工具进行了若干错误修复。 请参阅 [AEM Dispatcher Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter) 和 [Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer).

### 发布日期 {#release-date-ctt}

内容传输工具v1.1.20的发布日期是2021年1月8日。

### [!DNL Content Transfer Tool] 的新增功能 {#what-is-new-ctt}

* 用户现在可以通过将鼠标悬停在内容传输工具(CTT)用户界面的状态图标上来了解其访问令牌是否已过期。 此外，在迁移集详细信息UI中，还会通知他们无法连接到其Cloud Service实例。

### 错误修复 {#ctt-bug-fixes}

* 迁移集的内容传输工具(CTT)用户界面状态在一段时间不活动后不会持续并更改。 此问题已得到修复。
* 如果日志不可用，则用于查看日志的选项会被禁用。 此问题已修复，并且已添加消息来通知用户日志缺失的原因。
* 显示内容传输工具用户界面状态 *失败* 用户停止摄取时。 已修复此问题以显示 *已停止* 中。
