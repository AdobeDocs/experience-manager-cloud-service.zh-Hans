---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2020.8.0 版的发行说明。'
description: '[!DNL Adobe Experience Manager] 作为Cloud Service2020.8.0发行说明。'
exl-id: 83413130-ae90-4419-bcf7-42fdc740452b
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '1046'
ht-degree: 5%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 2020.8.0 版的发行说明 {#release-notes}

以下部分概述了 Experience Manager as a Cloud Service 2020.8.0 的常规发行说明。


## [!DNL Adobe Experience Manager Sites] 作为Cloud Service {#sites}

### [!DNL Sites] {#what-is-new-sites}的新增功能

* 能够[将页面和子页面（页面树）还原到早期版本](/help/sites-cloud/authoring/features/page-versions.md#reinstating-versions)。

* 能够在AEM [SPA编辑器中[创建Launches](/help/sites-cloud/authoring/launches/overview.md)。](/help/implementing/developing/hybrid/introduction.md)


## [!DNL Adobe Experience Manager Assets] 作为Cloud Service {#assets}

### [!DNL Assets] {#what-is-new-assets}的新增功能

* 现在，资产微服务支持视频转码。 [!UICONTROL 处理配置文件]配置中的新部分允许您设置视频比特率和维度。 输出格式为带H.264编解码器的MP4。 有关详细信息，请参阅[管理视频资产](/help/assets/manage-video-assets.md#transcode-video)。 有关更多转码选项和视频交付选项，请使用[!DNL Dynamic Media]附加组件。

* 在新的[!DNL Experience Manager Assets]部署中，现在默认配置了智能标记功能。 无需手动与[!DNL Adobe Developer Console]集成。 在现有部署中，管理员会像以前一样配置智能标记集成。

* 新的[资产下载体验](/help/assets/download-assets-from-aem.md)允许，

   * 用于大型下载的异步下载，这样用户就不必等待。
   * 用于开发人员扩展性的新模块化API。

* 资产微服务的元数据提取性能得到改进。 它可提高资产摄取的整体吞吐量。

* 使用处理配置文件使用计算服务生成自定义元数据。 请参阅[使用处理配置文件的自定义元数据](/help/assets/manage-metadata.md#metadata-compute-service)。

* 管理员可以配置的更简单的Brand Portal用户下载体验。 请参阅[下载体验概述](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/whats-new.html#download-configurations)。

* 本机和高保真PDF文档预览现在在Brand Portal中提供。 请参阅[文档查看器概述](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/whats-new.html#doc-viewer)。

* 现在，您可以在AEM as aCloud Service中直接从[!DNL Dynamic Media]使CDN（内容分发网络）缓存失效（与使用[!DNL Dynamic Media Classic]不同）。 它可确保在几分钟内而不是几小时内提供最新资产。 请参阅[通过Dynamic Media](/help/assets/dynamic-media/invalidate-cdn-cache-dynamic-media.md)使CDN缓存失效。

* 在[!DNL Assets]的用户界面控件、导航、浏览和搜索体验中添加了增强的辅助功能支持。

   * 如果在选择[!UICONTROL 添加演绎版]选项后按Esc键，则焦点将返回到工具栏。<!-- via CQ-4293594-->
   * 使用“电子邮件”组合框时，键盘焦点可按预期工作。<!-- via CQ-4286215 -->
   * 搜索过滤器部分中的折叠项元素被解释为标准的可扩展折叠项。<!-- via CQ-4273103 -->
   * 将标记应用到资产时，对话框会将标记显示为树元素。 已将ARIA属性适当应用于树元素，以便立即访问它们。<!-- via CQ-4272964 -->

* [!DNL AEM Desktop app] 2.0.3版本现已可用。它改进了与[!DNL Experience Manager] 6.5.5 Service Pack的兼容性，并且包含更新的客户端操作系统兼容性列表。 [!DNL Windows] 不支 [!DNL macOS] 持7和10.14之前的版本。

### 在[!DNL Assets] {#bugs-fixed}中修复的错误

* 首次单击时，“关联”和“取消关联”选项未做出响应。 (CQ-4299022)
* 下载资产时，如果您选择通过电子邮件接收资产的选项，则不会发送电子邮件。 (CQ-4299146)

## Adobe Experience Manager Commerce as aCloud Service{#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* 产品控制台功能现已可用。 这允许AEM中的营销人员/作者查看并导航商务后端中存储的类别和产品。 产品控制台还支持类别属性和产品属性。

* 经过改进的产品和类别选取器允许营销人员通过SKU选择产品，或通过类别ID选择类别。

## Cloud Manager {#cloud-manager}

### 发布日期 {#release-date-cm}

[!UICONTROL Cloud Manager]版本2020.8.0的发行日期是2020年8月6日。

### 新增功能 {#what-is-new-cloud-manager}

* 内容审核是Cloud Manager Sites Production Pipelines中启用的一项功能。 现在，具有Sites的程序的生产管道配置包含名为&#x200B;**内容审核**&#x200B;的第三个选项卡。 每当运行生产管道时，一个新的内容审核步骤将在自定义功能测试后包含在管道中，该步骤将根据多个维度(包括性能、SEO（搜索引擎优化）、辅助功能、最佳实践和PWA（渐进式Web应用程序）在内)来评估站点。


   >[!NOTE]
   >内容审核现已重命名为“体验审核”。

   有关更多详细信息，请参阅[体验审核测试](/help/implementing/cloud-manager/experience-audit-testing.md)。

* 现在， Assets项目中新建的环境将自动配置为智能内容服务。

* 可以从Cloud Manager的&#x200B;**概述**&#x200B;页面中，解除休眠环境的休眠。

* 能够在页面上执行由Google Lighthouse提供支持的“体验检查”功能。 作为Cloud Manager管道的一部分，可通过体验KPI检查和验证多达25个页面，并在Cloud Manager UI中显示得分。

### 错误修复 {#bug-fixes-cm}

* 在代码质量扫描中，正在执行一些不必要的和不需要的SonarQube插件。

* 在管道执行页面上，分支名称的格式不正确。

* 在某些情况下，已完成的管道执行未被成功记录为已完成，从而阻止管道的新执行。

* 由于内部通信问题，管道执行有时会遇到&#x200B;*卡住*&#x200B;的问题。

* 在配置新组织时，系统管理员以外的一些具有管理角色的用户错误地获得了Cloud Manager的访问权限。

* 在某些情况下，更新索引作业并行多次启动，从而导致部署失败。

* 程序卡片上的工具提示并不一致。

* 用户界面错误地允许在删除环境时尝试在环境中执行操作。

* Cloud Manager的&#x200B;**概述**&#x200B;页面上存在颜色不匹配的问题。

### 已知问题 {#known-issues-cm}

* 包含的页面无效，导致内容审核平均分数低于应有值。

* “内容审核”选项卡未正确显示使用创作域而非发布域的基本URL。

* 要激活“内容审核”步骤，用户必须编辑管道，并（可选）添加页面。 如果未添加页面，则会审核主页。

## 内容传输工具 {#content-transfer-tool}

请阅读本节内容，了解内容传输工具版本v1.0.4的新增功能和更新。

### 新增功能 {#what-is-new-ctt}

* 内容传输工具现在支持共享的S3数据存储。

### 错误修复 {#ctt-bug-fixes}

* 为工具添加了其他超时，以完成操作。

* 虽然日志显示错误，但早期版本的UI有时仍显示成功的提取。

## 代码重构工具 {#code-refactoring-tools}

请阅读本节内容，了解代码重构工具的新增功能和更新。

### 新增功能 {#what-is-new-refactoring}

* 发布的AIO-CLI插件可统一代码重构工具，使开发人员能够从一个位置调用和执行代码重构工具。 请参阅[Git资源：aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration) ，以了解更多详细信息。

* 已扩展的AEM Dispatcher Converter，可支持将内部部署和Adobe Managed Services Dispatcher配置转换为与AEM作为Cloud Service兼容的Dispatcher配置。 请参阅[Git资源：AEMCloud ServiceDispatcher Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter) ，以了解更多详细信息。

* AEM Dispatcher Converter在` node.js `中重新编写，并与AIO-CLI插件集成。
