---
title: ' [!DNL Adobe Experience Manager]  云服务 2020.8.0 版的发行说明。'
description: '[!DNL Adobe Experience Manager] 云服务 2020.8.0 版的发行说明。'
translation-type: tm+mt
source-git-commit: fe769e8acecbc173f2437edc292eeba2585f0509
workflow-type: tm+mt
source-wordcount: '1054'
ht-degree: 6%

---


# [!DNL Adobe Experience Manager] 云服务 2020.8.0 版的发行说明 {#release-notes}

以下部分概述了 Experience Manager 云服务 2020.8.0 版的常规发行说明。


## [!DNL Adobe Experience Manager Sites] 作为Cloud Service {#sites}

### What is new in [!DNL Sites] {#what-is-new-sites}

* 能将页 [面和子页面（页面树）恢复到较早版本](/help/sites-cloud/authoring/features/page-versions.md#reinstating-versions)。

* 可在AEM [SPA Editor中](/help/sites-cloud/authoring/launches/overview.md) 创建 [启动项。](/help/implementing/developing/spa/introduction.md)


## [!DNL Adobe Experience Manager Assets] 作为Cloud Service {#assets}

### What is new in [!DNL Assets] {#what-is-new-assets}

* 现在，资产微型服务支持视频转码。 处理用户档案配置中 [!UICONTROL 的新部分] ，允许您设置视频比特率和尺寸。 输出格式为MP4，采用H.264编解码器。 有关详细信息，请参 [阅管理视频资产](/help/assets/manage-video-assets.md#transcode-video)。 要获得更多转码选项和视频投放, [!DNL Dynamic Media] 请使用加载项。

* 在新部 [!DNL Experience Manager Assets] 署中，现在默认配置智能标记功能。 无需手动与集成 [!DNL Adobe Developer Console]。 在现有部署中，管理 [员会像以前一样配置智能](/help/assets/smart-tags-configuration.md#aio-integration) 标记集成。

* 新的资 [产下载体验](/help/assets/download-assets-from-aem.md) ,

   * 异步下载，以便用户无需等待。
   * 用于开发人员可扩展性的全新模块化API。

* 资产微型服务的元数据提取具有改进的性能。 它提高了整体资产摄取吞吐量。

* 使用处理用户档案，使用计算服务生成自定义元数据。 请参阅 [使用处理用户档案的自定义元数据](/help/assets/manage-metadata.md#metadata-compute-service)。

* 管理员可以配置的更简单的品牌门户用户下载体验。 请参 [阅下载体验概述](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/introduction/whats-new.html#download-configurations)。

* 本机和高保真PDF文档预览现在在Brand Portal中可用。 请参阅 [文档查看器概述](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/introduction/whats-new.html#doc-viewer)。

* 您现在可以将AEM中的CDN(内容投放网络)缓存作为Cloud Service( [!DNL Dynamic Media] 而不是使用)直接 [!DNL Dynamic Media Classic]失效。 它可以确保在几分钟内而不是几小时内提供最新的资产。 请参 [阅通过Dynamic Media使CDN缓存失效](/help/assets/dynamic-media/invalidate-cdn-cache-dynamic-media.md)。

* 在中的用户界面控件、导航、浏览和搜索体验中添加了增强的辅助功能支持 [!DNL Assets]。

   * 如果选择“添加再现”选项 [!UICONTROL 后按Esc键] ，则焦点将返回到工具栏。 <!-- via CQ-4293594-->
   * 使用“电子邮件”组合框时，键盘焦点可以正常工作。 <!-- via CQ-4286215 -->
   * 搜索过滤器部分的折叠元素被解释为标准的可扩展折叠元素。 <!-- via CQ-4273103 -->
   * 将标记应用于资产时，对话框将标记显示为树元素。 ARIA属性适当地应用于树元素，以使它们现在可访问。 <!-- via CQ-4272964 -->

* [!DNL AEM Desktop app] 2.0.3版本现已推出。 它提高了与6. [!DNL Experience Manager] 5.5 Service Pack的兼容性，并具有更新的客户端操作系统兼容列表。 [!DNL Windows] 不支 [!DNL macOS] 持7及10.14之前的版本。

### 修复的错误 [!DNL Assets] {#bugs-fixed}

* 首次单击“相关”和“不相关”选项时，该选项不响应。 (CQ-4299022)
* 下载资产时，如果您选择通过电子邮件接收资产的选项，则不会发送电子邮件。 (CQ-4299146)

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* 产品控制台功能现已可用。 这使AEM中的营销人员／作者能够视图和浏览存储在商务后端中的类别和产品。 还在产品控制台中提供对类别和产品属性的支持。

* 产品和类别选择器经过改进，可让营销人员通过SKU选择产品或通过类别ID选择类别。

## Cloud Manager {#cloud-manager}

### 发布日期 {#release-date-cm}

The Release Date for [!UICONTROL Cloud Manager] Version 2020.8.0 is August 06, 2020.

### 新增功能 {#what-is-new-cloud-manager}

* 内容审核是在Cloud Manager Sites Production Pipelines中启用的一项功能。 具有站点的项目的生产管道配置现在包括名为内容审核的第三 **个选项卡**。 每当运行生产管道时，在进行自定义功能测试后，管道中将包括新的内容审核步骤，该测试将根据包括性能、SEO（搜索引擎优化）、辅助功能、最佳实践和PWA（渐进式Web应用程序）在内的多个维度评估站点。


   >[!NOTE]
   >内容审核现已更名为“体验审核”。

   有关更多 [详细信息，请参](/help/implementing/cloud-manager/experience-audit-testing.md) 阅体验审核测试。

* 现在，资产项目中新创建的环境将自动配置智能内容服务。

* 冬眠环境可以从云管理器的概述页面 **解除** 。

* 能够在页面上执行体验检查，这由Google Lighthouse提供支持。 作为Cloud Manager渠道的一部分，最多可以根据体验KPI检查和验证25个页面，并在Cloud Manager UI中显示分数。

### 错误修复 {#bug-fixes-cm}

* 正在执行一些不必要的和不需要的SonarQube插件，作为代码质量扫描的一部分。

* 在管道执行页面上，分支名称的格式不正确。

* 在某些情况下，已完成的管道执行未被成功记录为已完成，从而防止了管道的新执行。

* 管道执行偶尔会因 *内部* 通信问题而卡住。

* 在设置新组织时，某些除系统管理员以外具有管理角色的用户被错误地授予了对Cloud Manager的访问权限。

* 在某些情况下，更新索引作业多次并行启动，导致部署失败。

* 项目卡上的工具提示不一致正确。

* 在删除环境时，用户界面错误地允许尝试对其执行操作。

* Cloud Manager的“概述”页面上存在颜色不 **匹配** 。

### 已知问题 {#known-issues-cm}

* 包含无效页面，使内容审核平均分数低于应有分数。

* “内容审核”选项卡使用作者域而非发布域错误地显示了基本URL。

* 要激活“内容审核”步骤，用户必须编辑管道，（可选）添加页面。 如果未添加任何页面，则将审核主页。

## 内容传输工具 {#content-transfer-tool}

可查看本节以了解新增功能以及内容传输工具版本1.0.4的更新。

### 新增功能 {#what-is-new-ctt}

* 内容传输工具现在支持共享S3数据存储。

### 错误修复 {#ctt-bug-fixes}

* 为工具添加了更多超时以完成操作。

* 早期版本的UI有时显示成功的提取，即使日志显示错误。

## 代码重构工具 {#code-refactoring-tools}

可查看本节以了解新增功能和代码重构工具的更新。

### 新增功能 {#what-is-new-refactoring}

* 发布的AIO-CLI插件可统一代码重构工具，使开发人员能从一个位置调用和执行代码重构工具。 请参阅 [Git资源：aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration) for more details.

* AEM Dispatcher Converter经过扩展，可支持将内部部署和Adobe Managed Services Dispatcher配置转换为AEM，作为Cloud Service兼容的Dispatcher配置。 请参阅 [Git资源：AEMCloud Service调度程序转换器](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter) ，了解更多详细信息。

* AEM Dispatcher Converter重新写入并 ` node.js ` 与AIO-CLI插件集成。
