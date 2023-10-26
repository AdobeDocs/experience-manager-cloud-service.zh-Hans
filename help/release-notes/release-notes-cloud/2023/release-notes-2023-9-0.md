---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 2023.9.0 版的发行说明。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 2023.9.0 版的发行说明。'
source-git-commit: 8f6611bdee755e0aa6f59c8f322a26cd1a071f23
workflow-type: tm+mt
source-wordcount: '1443'
ht-degree: 98%

---


# [!DNL Adobe Experience Manager] as a Cloud Service 的最新发行说明 {#release-notes}

以下部分概述了当前（最新）版本的 [!DNL Experience Manager] as a Cloud Service 的功能发行说明。

>[!NOTE]
>
>您可以在此部分中导航到早期版本的发行说明；例如，2021 版或 2022 版等的发行说明。
>
>查看 [Experience Manager 版本发行路线图](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html)，了解即将推出的 [!DNL Experience Manager] as a Cloud Service 的功能激活。

>[!NOTE]
>
>有关未与版本直接相关的文档更新的详细信息，请参阅[最新文档更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html)。

## 发布日期 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 的当前功能版本 (2023.9.0) 的发布日期为 2023 年 9 月 28 日。下一个功能版本 (2023.10.0) 计划于 2023 年 10 月 26 日发布。

## 维护发行说明 {#maintenance}

您可以在[此处](/help/release-notes/maintenance/latest.md)找到最新的维护发行说明。

## 发布视频 {#release-video}

请查看2023年9月发布概述视频，了解2023.9.0版本中新增功能摘要：

>[!VIDEO](https://video.tv.adobe.com/v/3424826/?quality=12)

## AEMEdge Delivery Services {#edge-delivery}

Edge Delivery 是一组新的可组合服务，专注于最大限度地发挥内容的作用，以便在客户交互时推动可衡量的业务成果。

有关 Edge Delivery Services 的更多信息，请参阅[此处](/help/edge/overview.md)的文章。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### 资源视图中的新增功能 {#assets-view-features}

**将元数据表单分配给文件夹**

现在可将元数据表单分配给部署中的特定文件夹。随后该文件夹中的所有资源（包括子文件夹中的资源）显示在所分配的元数据表单中定义的属性。

![将元数据表单分配给文件夹](/help/release-notes/assets/assign-to-folder.png)

### 管理视图中的新增功能 {#admin-view-features}

* **将 AEM Assets as a Cloud Service 与 Edge Delivery Services 的基于文档的创作集成**：将 AEM Assets 与 Edge Delivery Services 的基于文档的创作集成，使网站作者能够[在 Microsoft Word 或 Google Docs 中创作文档时使用 AEM Assets 存储库中提供的图像](/help/edge/using.md#integrate-assets-edge)。

* **提取 ZIP 存档**：可选择在 Experience Manager 中管理的 ZIP 存档，并且无需下载文件，即可[将文件直接提取到 Experience Manager 中](/help/assets/manage-digital-assets.md#extract-zip-archives)。

  ![为组固定项目](/help/release-notes/assets/extract-archive.png)

### 可在 [!DNL Experience Manager Assets] 中找到的预发布功能 {#prerelease-features-assets}

* **Dynamic Media**：[Dynamic Media 中支持视频具有多字幕和多音轨](/help/assets/dynamic-media/video.md#about-msma) - 现在可轻松地将多个字幕和多个音轨添加到主视频。此功能意味着全球观众都能看懂您的视频。只需自定义一个主视频，即可发布到多种语言的全球观众，并遵循不同地区的辅助功能准则。此外，作者从用户界面中的一个选项卡即可管理字幕和音轨。

  ![所选视频资源的“属性”页面上的“字幕和音轨”选项卡。](/help/release-notes/assets/msma-aem-cs.png)*所选视频资源的“属性”页面上的“字幕和音轨”选项卡。*

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Experience Manager Forms] 中的新增功能 {#forms-features}

* [**Google reCAPTCHA 企业支持**](/help/forms/captcha-adaptive-forms-core-components.md)：在自适应表单中使用 Google reCAPTCHA Enterprise 以增强对欺诈活动和垃圾邮件的防御，从而提供更安全的用户体验。借助高级风险分析和无缝集成，真实用户可以轻松提交表单，同时有效阻止机器人。

* [**用于表单的 Adobe Analytics with Experience Cloud Setup Automation**](/help/forms/enable-adobe-analytics-adaptive-form-using-experience-cloud-setup-automation.md)：现在按几下按钮即可启用 Adobe Analytics with Experience Cloud Setup Automation。通过它，可将 AEM Forms as a Cloud Service 与 Experience Platform 标签和 Adobe Analytics 建立联系以捕获和跟踪您已发布的表单的绩效量度。

  >[!VIDEO](https://video.tv.adobe.com/v/3424577/enable-adobe-analytics/?quality=12&learn=on)

* [**适用于自适应表单的 Adobe Analytics 报告模板**](/help/forms/view-understand-aem-forms-analytics-reports.md)：Forms as a Cloud Service 现在提供开箱即用的 Adobe Analytics 报告。它帮助您轻松地了解您表单的绩效。表单级别量度让您了解表单在演绎版数量、访客数、提交次数、平均填写时间等多个关键绩效指标 (KPI) 上表现如何。通过跟踪用户行为和反馈，可确定导致混淆的表单区域，并指导改进表单的设计和功能。

  ![自适应表单用户参与 Adobe Analytics 报告](/help/forms/assets/forms-analytics-report.png)

* **[自适应表单中基于核心组件的表单片段](/help/forms/adaptive-form-fragments-core-components.md)**：在用表单片段提升您的表单生成体验时告别重复、优化数字库存并改善协作。这些可重用的组件无缝集成到多个表单中，从而简化创建一致且外观专业的表单的过程。利用“一次更改，随处反映”功能，表单片段确保实现可重用性、标准化和品牌一致性。由于在一处作出的更新自动传播到所有利用这些片段的表单，因此可体验到更高的可维护性和效率。

* **[增强的 Adobe Sign 工作流步骤](/help/forms/aem-forms-workflow-step-reference.md#sign-document-step-sign-document-step)**：增强了 Adobe Sign 工作流步骤以包括以下各项：
   * **Adobe Sign 的基于 Government ID 的身份验证**：Adobe Acrobat Sign 的基于 Government ID 的身份验证通过使用户可使用政府颁发的 ID（驾照、身份证、护照）验证其身份，多提供一层验证。通过利用可信身份证明文件，此增强将签名过程的可信度提高一级，使其成为需要更高的安全性、合规性和用户验证的场景的理想之选。

   * **Adobe Sign 文档的审核记录**：使用审核记录功能可详细了解 Adobe Sign 文档的生命周期。利用审核记录功能，您现在可保留与文档相关的所有操作和交互的全面记录。其中包括查看者、编辑者或签署文档者以及每个事件的时间戳等详细信息。此增强对于保持合规性、解决争议和确保数字协议的完整性至关重要。

   * **协议接收者在签名者之外的新角色**：Adobe Acrobat Sign 可将协议接收者的角色扩充到仅签名者之外以更好地满足其工作流要求。启用此选项后，协议中的每个接收者均可单独配置其角色，其中签名者为默认角色。

* **Communication API 中支持页面计数**：除了通过 Communication API 检索文档之外，现在还可接收关于文档内所含页数的宝贵信息。

* **[使用规则编辑器中的自定义错误处理程序处理错误](/help/forms/add-custom-error-handler-adaptive-forms-core-components.md)**：现在可调用自定义函数以响应外部服务返回的错误，并为最终用户提供量身定制的响应。例如，可在后端为特定的错误代码调用自定义工作流或通知客户服务已停止。

* **[64 位版本的 AEM Forms Designer](/help/forms/installing-configuring-designer.md)**：64 位版本的 AEM Forms Designer 提供了增强的性能、可扩展性和内存管理，以提升您的表单创建体验。利用 64 位架构，您可以轻松处理更大、更复杂的项目，确保无缝的设计工作流程和优化的效率。利用此最新版本，提升您的表单设计能力并迎接 AEM Forms Designer 的未来。

### 早期采用者计划 {#forms-early-adopter}

* **[用 DocAssurance API（Communication API 的一部分）保护文档](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance-doc-assurance)**：DocAssurance API 使您能够通过为文档签名和加密来保护敏感信息。通过加密，可将文档内容转换为无法读取的格式，从而确保只有获得授权的用户可访问。这一层加强的保护不仅防止未经授权地查看宝贵的数据，还能让人安心。利用 Signature API，您的组织可以保护其分发和接收的 Adobe PDF 文档的安全和隐私。此服务使用数字签名和认证确保只有预期的接收者可更改文档。

  您可以通过您的官方电子邮件 ID 向 `aem-forms-early-adopter-program@adobe.com` 发送电子邮件，以加入早期采用者计划并请求对该功能的访问权限。

* **[Headless 自适应表单](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html)**：使用 Headless 自适应表单使您的开发人员可创建、发布和管理可通过 API 而非传统图形用户界面访问和交互的交互式表单。Headless 自适应表单可帮助您：

   * 使用选定的编程语言构建高质量的多渠道表单
   * 将表单本机集成到您的桌面和移动应用程序、网站和聊天应用程序
   * 在表单应用程序中重复使用您的专有 UI 组件
   * 利用 Adobe Experience Manager Forms 的强大功能

  您可以使用官方电子邮件 ID 将电子邮件发送到 `aem-forms-headless@adobe.com` 以加入早期采用者计划。

## [!DNL Experience Manager]as a[!DNL Cloud Service] Foundation {#foundation}

### 与营销活动相关的 URL 参数的新 CDN 缓存行为 {#cache-url-params}

对于新环境，CDN 默认删除与营销相关的查询参数，以提高营销活动的效果和缓存命中率。现有环境不受影响。[了解详情。](/help/implementing/dispatcher/caching.md#marketing-parameters)

### 流量过滤规则（包括 WAF 规则）早期采用者计划 {#waf-early-adopter}

基于以下项筛选 CDN 上的流量：
* 请求头和属性（例如，IP 地址）
* 已知与恶意流量相关的流量模式

想试用该功能并分享反馈吗？使用您的官方电子邮件 ID 将电子邮件发送到 **aemcs-waf-adopter@adobe.com**，了解有关早期采用者计划的更多信息。空间是有限的。

在[此处](/help/security/traffic-filter-rules-including-waf.md)的文章中详细了解该功能。

## Cloud Manager {#cloud-manager}

您可以在[此处](/help/implementing/cloud-manager/release-notes/current.md)找到 Cloud Manager 每月发布的完整列表。

## 迁移工具 {#migration-tools}

您可以在[此处](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)找到迁移工具版本的完整列表。
