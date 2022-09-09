---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 2022.7.0 版的发行说明。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 2022.7.0 版的发行说明。'
source-git-commit: b1c4706d2d148c136eed66b0bff6f792a89e9d8c
workflow-type: tm+mt
source-wordcount: '958'
ht-degree: 100%

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

[!DNL Adobe Experience Manager][!DNL Cloud Service] 当前版本 (2022.7.0) 的发布日期为 2022 年 8 月 8 日。

下一个版本 (2022.8.0) 计划于 2022 年 9 月 1 日发布。

## 发布视频 {#release-video}

请查看 2022 年 7 月发布概述视频，了解 2022.7.0 版本中新增功能摘要：

>[!VIDEO](https://video.tv.adobe.com/v/345409/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### [!DNL Sites] 中的新增功能 {#sites-features}

* [内容片段控制台](/help/sites-cloud/administering/content-fragments/content-fragments-console.md)现在支持[键盘快捷键](/help/sites-cloud/administering/content-fragments/content-fragments-console-keyboard-shortcuts.md)。

* AEM as a Cloud Service 的 [Web 优化图像交付](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/web-optimized-image-delivery.html)，通过交付 WebP 等格式，大大提高了页面速度。这项新的服务还提供了更灵活的图像大小调整和转换选项。所有版本的[核心图像组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/image.html)都允许利用此服务，并可通过单击图像组件策略中的选项将图像作为 WebP 交付。

* AEM 个性化活动现在可以使用体验片段来代替我们的旧功能/服务。该功能：
   * 启用一个迁移路径，其中 AEM 内容会推广体验片段功能/服务，而不是旧的库功能/服务，以便提供与未来大规模个性化保持一致的具有适当样式的内容。
   * 防止内容作者意外在其网站上提供无样式内容。
   * 允许将任何组件的定位模式转换为使用可编辑模板的体验片段（JSON 和 HTML 类型）。

>[!NOTE]
>
>已经使用旧的功能/服务的现有个性化活动可以继续这样操作，但新的个性化活动应该作为体验片段创建（这是推荐的方法）。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets] 预发行渠道中提供的新功能 {#prerelease-features-assets}

您现在可以将 Adobe Experience Manager Assets 配置为[根据 MIME 类型限制用户可以上传的资源类型](/help/assets/configure-asset-upload-restrictions.md)。

![资产上传限制](/help/assets/assets/asset-upload-restrictions.png)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] 中的新增功能 {#forms-features}

* **[涂鸦签名的键盘输入支持](/help/forms/signing-forms-using-scribble.md)**：自适应表单越来越多地用于触摸设备，并且通常会要求支持签名。在触摸设备上签署文件已成为一种可接受的表单签署方式。对于此类用例，自适应表单提供对涂鸦签名和 Adobe Sign 的原生支持。现在，除了其他已支持的选项外，您还可以使用键盘在自适应表单中进行涂鸦签名。它还有助于提高辅助功能符合性。

![iPhone 上对 Scribble 签名的键盘输入支持](/help/release-notes/assets/scribble-keyboard-mobile.png)

* **使用本地语言版本的自适应表单向导**：您可以使用此向导的所选语言版本。它现在支持 Adobe Experience Manager 所支持的所有语言。

### [!DNL Forms]预发行渠道中提供的新功能 {#prerelease-features-forms}

<!-- 

* **[Launch Adaptive Form creation wizard from embed form component](/help/forms/using/embed-adaptive-form-aem-sites.md)**: You can now launch Adaptive Form creation wizard from embed form component. It helps improve content and forms authoring workflows for Sites and Forms practitioners trying to add enrollment experiences to a web page. 

![Keyboard input support for Scribble signatures on iphone](/help/release-notes/assets/froms-container.png) 

-->

* **[调用 DDX – AEM 工作流步骤](/help/forms/aem-forms-workflow-step-reference.md#invokeddx)**：DDX（文档描述 XML）是一种声明性标记语言，其元素代表文档的构建块。这些构建块包括 PDF 和 XDP 文档以及其他元素，例如注释、书签和样式文本。DDX 文档是文档模板，它描述了应出现在结果文档中的源文档的所需特征。单个 DDX 可用于一系列源文档。您可以使用 AEM 工作流中的调用步骤来执行各种操作，例如，汇编和反汇编文档、创建和修改 Acrobat 和 XFA 表单及其他操作，如 [DDX 参考](https://helpx.adobe.com/content/dam/help/en/experience-manager/forms-cloud-service/ddxRef.pdf)文档中所述。

* **[转换为 PDF/A – AEM 工作流步骤](/help/forms/aem-forms-workflow-step-reference.md##convert-pdfa)**：PDF/A 是一种用于长期保存文档内容的存档格式，其中所有字体都将嵌入，并且文件未经压缩。现在，您可以使用 AEM 工作流中的“转换为 PDF/A”步骤，将任意格式的文档或文件转换为 PDF/A 格式。


## CIF 加载项 {#cloud-services-cif}

### 新增功能 {#what-is-new-cif}

* 产品目录扩充现在支持 AEM 页面。这使作者能够管理页面 – 产品关联。

* 多项 CIF 核心组件功能改进

### 错误修复 {#bug-fixes-cif}

* 将登录令牌添加到客户端价格获取流程

* 数据层中的页面组件错误

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### 新增功能 {#what-is-new-foundation}

* [存储库浏览器](/help/implementing/developing/tools/repository-browser.md)现在提供了一个路径输入字段，可用于直接跳转到存储库层次结构中的特定文件夹
* Sling 内容分发 (SCD) 现在支持显式“无效”操作，以便在不发布内容的情况下使内容无效。有关更多详细信息，请参阅 [AEM as a Cloud Service 中的缓存](/help/implementing/dispatcher/caching.md#explicit-invalidation)页面。
* AEM as a Cloud Service 现在提供 mod_macro。请参阅[此表](/help/implementing/dispatcher/disp-overview.md)以查看支持的 Apache 模块的列表。

### AEM as a Cloud Service SDK Dispatcher 工具增强功能 {#dispatcher-tools-enhancements}

* Apache 可使用 `docker_run_hot_reload.sh` 脚本启动，该脚本会自动加载并验证对 Apache 和 Dispatcher 配置进行的任何后续更改，从而加快开发人员的工作速度。仅支持 Dispatcher 工具的灵活模式。此外，有关自动重新加载和验证的更多详细信息，请参阅[调试 Apache 和 Dispatcher 配置](/help/implementing/dispatcher/validation-debug.md#automatic-reloading)。
* 本地 Apache/Dispatcher 配置将更紧密地跟踪云环境中的变化，从而提高两个环境之间的对等性。

### [!DNL Experience Manager] 预发行渠道中提供的新功能 {#prerelease-features-foundation}

* AEM as a Cloud Service 现已与 Unified Shell 集成，以改进用户体验并将其与所有其他 Experience Cloud 应用程序相统一。 请参阅 [Unified Shell 上的 AEM as a Cloud Service](/help/overview/aem-cloud-service-on-unified-shell.md) 以了解更多详细信息。

## Adobe Learning Manager 连接器 {#learn-manage}

* 新的 Adobe Learning Manager 具有用于连接到 Adobe Experience Manager Sites、Marketo Engage 和 Adobe Commerce 的连接器。若要了解详情，请参阅：[Adobe Learning Manager 用户指南](https://helpx.adobe.com/cn/learning-manager/user-guide.html)。

## Cloud Manager {#cloud-manager}

您可以在[此处](/help/implementing/cloud-manager/release-notes-cloud-manager/release-notes-cm-current.md)找到 Cloud Manager 每月发布的完整列表。

## 迁移工具 {#migration-tools}

您可以在[此处](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)找到迁移工具版本的完整列表。
