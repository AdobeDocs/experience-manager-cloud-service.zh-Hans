---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 的最新发行说明。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 的最新发行说明。'
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
mini-toc-levels: 1
source-git-commit: 0ae79facb4233988db4a649b8e79ca3041832584
workflow-type: tm+mt
source-wordcount: '955'
ht-degree: 21%

---


# [!DNL Adobe Experience Manager] as a Cloud Service 的最新发行说明 {#release-notes}

以下部分概述了当前（最新）版本的 [!DNL Experience Manager] as a Cloud Service 的一般发行说明。

>[!NOTE]
>
>您可以在此部分中导航到早期版本的发行说明；例如，2020 版、2021 版等的发行说明。

>[!NOTE]
>
>有关未与版本直接相关的文档更新的详细信息，请参阅[最新文档更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html)。

## 发布日期 {#release-date}

的发行日期 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 最新版本(2022.7.0)是2022年8月8日发行的。

下一版本(2022.8.0)计划于2022年8月25日发布。

## 发布视频 {#release-video}

观看2022年7月版概述视频，了解2022.7.0版本中添加的功能摘要：

>[!VIDEO](https://video.tv.adobe.com/v/345409/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### [!DNL Sites] 中的新增功能 {#sites-features}

* 的 [内容片段控制台](/help/sites-cloud/administering/content-fragments/content-fragments-console.md) 现在支持键盘快捷键。

* AEM asCloud Service [优化了Web图像交付](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/web-optimized-image-delivery.html) 允许通过提供WebP等格式显着提高页面速度。 这项新服务还提供了更灵活的图像大小调整和转换选项。 的所有版本 [核心图像组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/image.html) 允许利用此服务，并通过单击图像组件策略中的选项以WebP形式交付图像。

* AEM个性化活动现在可以利用体验片段来替代我们的旧版选件。 此功能：
   * 启用一个迁移路径，使AEM内容能够提升体验片段选件，而不是旧版库选件，从而提供与今后的个性化规模相符且样式正确的内容。
   * 防止内容作者在其网站上意外提供未设置样式的内容。
   * 允许将任何组件的定位模式转换为使用可编辑模板的体验片段(JSON和HTML类型)。

>[!NOTE]
>
>现有已使用旧版选件的个性化活动可以继续这样做，但应将新的个性化活动创建为体验片段，因为这是今后的推荐方法。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets] 预发行渠道中提供的新功能 {#prerelease-features-assets}

您现在可以将Adobe Experience Manager Assets配置为 [根据MIME类型限制用户可上传的资产类型](/help/assets/configure-asset-upload-restrictions.md).

![资产上传限制](/help/assets/assets/asset-upload-restrictions.png)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] 中的新增功能 {#forms-features}

* **对潦草签名的键盘输入支持**:自适应Forms在触控设备上的使用越来越多，一种常见要求是支持签名。 在触控设备上对文档进行签名已成为一种可接受的签名方式。 Adaptive Forms对Scribble签名和Adobe Sign提供了此类用例的本机支持。 现在，除了其他已受支持的选项外，您还可以使用键盘在自适应表单中涂写签名。 它还有助于提高无障碍合规性。

![在iphone上支持Scribble签名的键盘输入](/help/release-notes/assets/scribble-keyboard-mobile.png)

* **在本地语言中使用自适应Forms向导**:您可以使用所选语言的向导。 现在，它支持Adobe Experience Manager支持的所有语言。

### [!DNL Forms] 预发行渠道中提供的新功能 {#prerelease-features-forms}

<!-- * **[Launch Adaptive Form creation wizard from embed form component](/help/forms/using/embed-adaptive-form-aem-sites.md)**: You can now launch Adaptive Form creation wizard from embed form component. It helps improve content and forms authoring workflows for Sites and Forms practitioners trying to add enrollment experiences to a web page. 

![Keyboard input support for Scribble signatures on iphone](/help/release-notes/assets/froms-container.png) -->

* **调用 — AEM工作流步骤**:文档描述XML(DDX)是一种声明性标记语言，其元素表示文档的构建块。 这些构建基块包括PDF和XDP文档，以及其他元素，如注释、书签和样式化文本。 DDX文档是文档的模板，描述了源文档在生成文档中应显示的所需特征。 单个DDX可与一系列源文档一起使用。 您可以使用调用步骤和AEM工作流执行各种操作，例如汇编反汇编文档、创建和修改Acrobat和XFA Forms，以及 [DDX参考](https://helpx.adobe.com/content/dam/help/en/experience-manager/forms-cloud-service/ddxRef.pdf) 文档。

* **转换为PDF/A - AEM工作流步骤**:PDF/A是用于长期保存文档内容的存档格式，所有字体都会被嵌入，并且文件未压缩。 现在，您可以使用AEM工作流的“转换为PDF/A”步骤，将任何格式的文档或文件转换为PDF/A格式。


## CIF 加载项 {#cloud-services-cif}

### 新增功能 {#what-is-new-cif}

* 产品目录扩充现在支持AEM页面。 这样，作者就可以管理页面 — 产品关联。

* 各种CIF核心组件改进

### 错误修复 {#bug-fixes-cif}

* 将登录令牌添加到客户端价格获取

* 数据层中的页面组件错误

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### 新增功能 {#what-is-new-foundation}

* 的 [存储库浏览器](/help/implementing/developing/tools/repository-browser.md) 现在有一个路径输入字段，以便直接跳转到存储库层次结构中的特定文件夹
* Sling内容分发(SCD)现在支持显式“失效”操作，以便在不发布内容的情况下使内容失效。 请参阅 [AEMas a Cloud Service中的缓存](/help/implementing/dispatcher/caching.md#explicit-invalidation) 页面以了解更多详细信息。
* mod_macro现在在AEMas a Cloud Service中可用。 请参阅 [此表](/help/implementing/dispatcher/disp-overview.md) 以获取受支持Apache模块的列表。

### AEMas a Cloud ServiceSDK Dispatcher工具增强功能 {#dispatcher-tools-enhancements}

* Apache可以以 `update_sdk.sh` 脚本，该脚本将自动加载并验证对apache和dispatcher配置的任何后续更改，从而提高开发人员速度。 仅支持调度程序工具灵活模式。 另请参阅 [调试Apache和Dispatcher配置](/help/implementing/dispatcher/validation-debug.md#automatic-loading) 有关自动加载和验证的更多详细信息。
* 本地Apache/Dispatcher配置将更密切地跟踪云环境中的更改，从而提高两个环境之间的对等性。

### [!DNL Experience Manager] 预发行渠道中提供的新功能 {#prerelease-features-foundation}

* AEM as a Cloud Service 现已与 Unified Shell 集成，以改进用户体验并将其与所有其他 Experience Cloud 应用程序相统一。 请参阅 [Unified Shell 上的 AEM as a Cloud Service](/help/overview/aem-cloud-service-on-unified-shell.md) 以了解更多详细信息。

## Adobe学习管理器连接器 {#learn-manage}

* 新的Adobe学习管理器具有到Adobe Experience Manager Sites、Marketo Engage和Adobe Commerce的连接器。 要了解更多信息，请参阅： [Adobe学习管理器用户指南](https://helpx.adobe.com/learning-manager/user-guide.html).


## Cloud Manager {#cloud-manager}

您可以在[此处](/help/implementing/cloud-manager/release-notes-cloud-manager/release-notes-cm-current.md)找到 Cloud Manager 每月发布的完整列表。

## 迁移工具 {#migration-tools}

您可以在[此处](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)找到迁移工具版本的完整列表。
