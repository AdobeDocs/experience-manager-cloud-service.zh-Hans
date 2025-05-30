---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 2020.8.0 版的发行说明。'
description: "[!DNL Adobe Experience Manager]个2020.8.0版as a Cloud Service发行说明。"
exl-id: 83413130-ae90-4419-bcf7-42fdc740452b
feature: Release Information
role: Admin
source-git-commit: cfaa3be31195929b80310610120a779a20537c61
workflow-type: tm+mt
source-wordcount: '1031'
ht-degree: 35%

---

# [!DNL Adobe Experience Manager]as a Cloud Service2020.8.0版发行说明 {#release-notes}

以下部分概述了 Experience Manager as a Cloud Service 2020.8.0 的常规发行说明。


## [!DNL Adobe Experience Manager Sites]个as a Cloud Service {#sites}

### [!DNL Sites] 的新增功能 {#what-is-new-sites}

* 能够[将页面和子页面（页面树）还原到早期版本](/help/sites-cloud/authoring/sites-console/page-versions.md#reinstating-versions)。

* 能够在AEM [SPA编辑器](/help/implementing/developing/hybrid/introduction.md)中[创建启动项](/help/sites-cloud/authoring/launches/overview.md)。


## [!DNL Adobe Experience Manager Assets]个as a Cloud Service {#assets}

### [!DNL Assets] 的新增功能 {#what-is-new-assets}

* 现在，资产微服务支持视频转码。 [!UICONTROL 处理配置文件]配置中的新部分允许您设置视频比特率和维度。 输出格式为带有H.264编解码器的MP4。 有关详细信息，请参阅[管理视频资源](/help/assets/manage-video-assets.md#transcode-video)。 如需更多转码选项和视频分发选项，请使用[!DNL Dynamic Media]加载项。

* 在新[!DNL Experience Manager Assets]部署中，现在默认配置了智能标记功能。 无需手动与[!DNL Adobe Developer Console]集成。 在现有部署中，管理员会像之前一样配置智能标记集成。

* 新的[资源下载体验](/help/assets/download-assets-from-aem.md)允许、

   * 适用于大型文件的异步下载，因此用户无需等待。
   * 用于开发人员扩展性的新模块化API。

* 资源微服务的元数据提取提高了性能。 它可以提高总体资源摄取吞吐量。

* 使用处理配置文件以使用计算服务生成自定义元数据。 查看使用处理配置文件[&#128279;](/help/assets/manage-metadata.md#metadata-compute-service)的自定义元数据。

* 管理员可配置的更简单的Brand Portal用户下载体验。 请参阅[下载体验概述](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/whats-new.html?lang=zh-Hans#download-configurations)。

* Brand Portal现在提供本机和高保真PDF文档预览。 请参阅[文档查看器概述](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/whats-new.html?lang=zh-Hans#doc-viewer)。

* 现在，您可以在AEM as a Cloud Service中直接从[!DNL Dynamic Media]使CDN（内容分发网络）缓存失效（与使用[!DNL Dynamic Media Classic]不同）。 它确保在几分钟内而不是几小时内提供最新资产。 请参阅[通过Dynamic Media](/help/assets/dynamic-media/invalidate-cdn-cache-dynamic-media.md)使CDN缓存失效。

* 在[!DNL Assets]中，用户界面控件、导航、浏览和搜索体验添加了增强的辅助功能支持。

   * 如果在选择[!UICONTROL 添加演绎版]选项后按Esc键，则焦点将返回到工具栏。<!-- via CQ-4293594-->
   * 使用电子邮件组合框时，键盘焦点按预期工作。<!-- via CQ-4286215 -->
   * 搜索筛选器部分中的折叠元素解释为标准可展开折叠项。<!-- via CQ-4273103 -->
   * 将标记应用于资源时，对话框会将标记显示为树元素。 ARIA属性已正确应用于树元素，以便现在可以访问。<!-- via CQ-4272964 -->

* [!DNL AEM Desktop app] 2.0.3版本现已可用。 它改进了与[!DNL Experience Manager] 6.5.5 Service Pack的兼容性，并更新了客户端操作系统兼容性列表。 不支持10.14之前的[!DNL Windows] 7和[!DNL macOS]版本。

### [!DNL Assets] 中修复的错误 {#bugs-fixed}

* 首次单击“关联和取消关联”选项时，该选项不会响应。 (CQ-4299022)
* 下载资源时，如果您选择通过电子邮件接收该资源，则不会发送电子邮件。 (CQ-4299146)

## Adobe Experience Manager Commerceas a Cloud Service {#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* 产品控制台功能现已可用。 这允许AEM中的营销人员/作者查看和导航商务后端中存储的类别和产品。 此外，产品控制台还支持类别属性和产品属性。

* 改进后的产品和类别选取器允许营销人员通过SKU选择产品，或通过类别ID选择类别。

## Cloud Manager {#cloud-manager}

### 发布日期 {#release-date-cm}

[!UICONTROL Cloud Manager]版本2020.8.0的发布日期为2020年8月6日。

### 新增功能 {#what-is-new-cloud-manager}

* 内容审核是 Cloud Manager Sites 生产管道上启用的一项功能。带有 Sites 的程序的生产管道配置现在包括名为&#x200B;**内容审核**&#x200B;的第三个选项卡。无论何时运行生产管道，都会在自定义功能测试后在管道中包含一个新的“内容审核”步骤，该步骤将依据多个维度(包括性能、SEO（搜索引擎优化）、可访问性、最佳实践和PWA（渐进式Web应用程序）在内)来评估站点。


  >[!NOTE]
  >内容审核已重命名为体验审核。

  有关详细信息，请参阅[体验审核测试。](/help/implementing/cloud-manager/experience-audit-dashboard.md)

* Assets 程序中新建环境现在将自动配置为智能内容服务。

* 休眠环境可以从 Cloud Manager 的&#x200B;**概述**&#x200B;页面中解除休眠。

* 能够在页面上执行体验检查，由 Google Lighthouse 提供支持。作为 Cloud Manager 管道的一部分，最多可以根据体验 KPI 检查和验证 25 个页面，分数显示在 Cloud Manager UI 中。

### 错误修复 {#bug-fixes-cm}

* 作为代码质量扫描的一部分，正在执行一些不必要且不受欢迎的 SonarQube 插件。

* 在管道执行页面上，分支名称的格式不正确。

* 在某些情况下，已完成的管道执行未成功记录为已完成，从而阻止了新的管道执行。

* 由于内部通信问题，管道执行偶尔会&#x200B;*卡住*。

* 在配置新组织时，一些具有系统管理员以外管理角色的用户被错误地授予访问 Cloud Manager 的权限。

* 在某些情况下，更新索引作业同时多次启动，导致部署失败。

* 程序卡上的工具提示不一致。

* 删除用户界面时，错误地允许在环境上尝试操作。

* Cloud Manager 的&#x200B;**概述**&#x200B;页面上颜色不匹配。

### 已知问题 {#known-issues-cm}

* 包含无效页面，使内容审核平均分数低于应有值。

* “内容审核”选项卡使用作者域而非发布域错误地显示了基本 URL。

* 为了激活“内容审核”步骤，用户必须编辑管道，也可以选择添加页面。如果没有添加页面，则会审核主页。

## 内容传输工具 {#content-transfer-tool}

阅读本节内容，了解内容传输工具版本1.0.4的新增功能和更新。

### 新增功能 {#what-is-new-ctt}

* 内容传输工具现在支持共享的S3数据存储。

### 错误修复 {#ctt-bug-fixes}

* 为工具完成操作添加了其他超时。

* 即使日志显示错误，早期版本UI有时也会显示成功提取。

## 代码重构工具 {#code-refactoring-tools}

阅读本节内容，了解代码重构工具的新增功能和更新。

### 新增功能 {#what-is-new-refactoring}

* 发布的AIO-CLI插件可统一代码重构工具，使开发人员能够从一个位置调用和执行代码重构工具。 有关更多详细信息，请参阅[Git资源：aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration)。

* 扩展的AEM Dispatcher Converter支持将内部部署和AdobeManaged Services Dispatcher配置转换为与AEM as a Cloud Service兼容的Dispatcher配置。 有关详细信息，请参阅[Git资源：AEM Cloud Service Dispatcher Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter)。

* 在` node.js `中重写AEM Dispatcher Converter并与AIO-CLI插件集成。
