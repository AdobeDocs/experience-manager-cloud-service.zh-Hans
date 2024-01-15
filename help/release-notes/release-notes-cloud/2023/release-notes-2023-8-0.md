---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 2023.8.0 版的发行说明。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 2023.8.0 版的发行说明。'
exl-id: a0ffa6cf-64ae-468c-93f4-ac6805ef907e
source-git-commit: a77e5dc4273736b969e9a4a62fcac75664495ee6
workflow-type: ht
source-wordcount: '1691'
ht-degree: 100%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 2023.8.0 版的发行说明 {#release-notes}

以下部分概述了 2023.8.0 版的 [!DNL Experience Manager] as a Cloud Service 的功能发行说明。

## 发布日期 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 最新功能版本 (2023.8.0) 的发布日期为 2023 年 8 月 31 日。下一个功能版本 (2023.9.0) 计划于 2023 年 9 月 28 日发布。

## 发布视频 {#release-video}

请查看 2023 年 8 月发行版概述视频，了解 2023.8.0 版本中新增功能的摘要：

>[!VIDEO](https://video.tv.adobe.com/v/3423535/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### [!DNL Experience Manager Sites] 中的新增功能 {#sites-features}

* [内容片段控制台](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/content-fragments/content-fragments-console.html)现在允许用户查看标记并按作为元数据应用于内容片段的标记进行搜索。用户将不再需要切换到此功能的资源 UI，这减少了上下文切换并提高了效率。

  ![内容片段控制台中的标记](/help/assets/content-fragments-console-tags.png)
* AEM as a Cloud Service 上现在有新的内容片段编辑器可用。它通过简化内容作者的创作任务并减少在编辑内容时需要在不同的应用程序之间切换的次数，使内容作者提高工作效率。
  ![新的内容片段编辑器](/help/release-notes/assets/newCFEditor.png)

新的内容片段编辑器具备以下这些在原有编辑器中没有的优势：
* 自动保存，可提高创作效率并防止意外丢失编辑内容。
* 内容片段及其引用的分级视图，其中可使用结构树在结构层次很深的片段中快速导航。
  ![内容片段编辑器中的结构树](/help/release-notes/assets/newCFEditor_StructureTree.png)

* 直接上传资源作为内容引用，而不必将它先上传到资源 DAM
* 临时预览由内容片段投放的渲染体验，以帮助作者使前端应用程序上内容的外观可视化
* 从编辑器一键发布和取消发布内容片段
* 在编辑内容片段时查看并导航到语言副本
  ![内容片段编辑器中的语言副本](/help/release-notes/assets/newCFEditor_LanguageCopies.PNG)

* 查看版本以帮助跟踪内容片段的时间线

  ![内容片段编辑器中的版本](/help/release-notes/assets/newCFEditor_Versionhistory.PNG)

* 查看父引用以帮助作者了解其所做编辑产生的影响

  ![内容片段编辑器中的父引用](/help/release-notes/assets/newCFEditor_Parentreferences.PNG)

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### 资源视图中的新增功能 {#assets-view-features}

<!--

**Assign metadata form to a folder**

You can now assign metadata form to a specific folder within your Assets Essentials deployment. All assets in the folder, including assets in the sub-folders, then display properties defined in the assigned metadata form.

![assign metadata form to a folder](/help/release-notes/assets/assign-to-folder.png)

-->

* **从数据源批量导入资源**：管理员现在[可将大量资源从数据源导入到 AEM Assets](/help/assets/bulk-import-assets-view.md)。管理员不再需要将单独的资源或文件夹上传到 AEM Assets。支持批量导入的数据源包括 Azure、AWS、Google Cloud 和 Dropbox。

  ![从数据源批量导入资源](/help/release-notes/assets/bulk-import.png)

* **由 Adobe Express 提供支持的图像编辑工具**：可直接在 AEM Assets 中找到简单而直观的[由 Adobe Express 提供支持的图像编辑工具](/help/assets/edit-images-assets-view.md)以提高内容重用率并提高内容速度。

  ![用 Adobe Express 编辑图像](/help/release-notes/assets/edit-adobe-express.png)

* **可灵活地为“我的工作区”的“快速访问”部分固定各项**：可为您、您的整个组织或一系列组选择并固定各项，以使各项根据您的选择显示在[“我的工作区”的“快速访问”部分](/help/assets/my-workspace-assets-view.md)中。

  ![为组固定项目](/help/release-notes/assets/pin-items-for-groups.png)

### 管理视图中的新增功能 {#admin-view-features}

**搜索增强**

* 管理员现在可[配置在您执行搜索时显示的资源的批次大小](/help/assets/search-assets.md#configure-asset-batch-size)。当您进一步向下滚动以加载资源搜索结果时，将以所配置的批次大小数量的倍数显示这些结果。可选择 200、500 和 1000 个资源的可用批次大小。设置较小的批次大小数字可加快搜索响应速度。

  ![资源批次大小配置](/help/release-notes/assets/assets-batch-size-configuration.png)

* Experience Manager Assets 现在包含新版本 9 的 `damAssetLucene` 索引。`damAssetLucene-9` 将 Oak Query 分面计数的行为更改为[不再评估对底层搜索索引返回的分面计数的访问控制](/help/assets/search-assets.md)，而这导致加快搜索响应速度。

### 可在 [!DNL Experience Manager Assets] 中找到的预发布功能 {#prerelease-features-assets}

* **Dynamic Media**：[Dynamic Media 中支持视频具有多字幕和多音轨](/help/assets/dynamic-media/video.md#about-msma) - 现在可轻松地将多个字幕和多个音轨添加到主视频。此功能意味着全球观众都能看懂您的视频。只需自定义一个主视频，即可发布到多种语言的全球观众，并遵循不同地区的辅助功能准则。此外，作者从用户界面中的一个选项卡即可管理字幕和音轨。

  ![所选视频资源的“属性”页面上的“字幕和音轨”选项卡。](/help/release-notes/assets/msma-aem-cs.png)*所选视频资源的“属性”页面上的“字幕和音轨”选项卡。*

* **Assets**：可选择在 Experience Manager 中管理的 ZIP 存档，并且无需下载文件，即可[将文件直接解压缩到 Experience Manager 中](/help/assets/manage-digital-assets.md#extract-zip-archives)。

  ![为组固定项目](/help/release-notes/assets/extract-archive.png)


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] 中的新增功能 {#new-features-available-in-forms-channel}

* [**Google reCAPTCHA 企业支持**](/help/forms/captcha-adaptive-forms.md)：在自适应表单中使用 Google reCAPTCHA Enterprise 以增强对欺诈活动和垃圾邮件的防御，从而提供更安全的用户体验。借助高级风险分析和无缝集成，真实用户可以轻松提交表单，同时有效阻止机器人。


### 可在 [!DNL Forms] 中找到的预发布功能 {#pre-release-features-available-in-forms-channel}

* **用于表单的 Adobe Analytics with Experience Cloud Setup Automation**：现在按几下按钮即可启用 Adobe Analytics with Experience Cloud Setup Automation。通过它，可将 AEM Forms as a Cloud Service 与 Experience Platform 标签和 Adobe Analytics 建立联系以捕获和跟踪您已发布的表单的绩效量度。

* **适用于自适应表单的 Adobe Analytics 报告模板**：Forms as a Cloud Service 现在提供开箱即用的 Adobe Analytics 报告。它帮助您轻松地了解您表单的绩效。表单级别量度让您了解表单在演绎版数量、访客数、提交次数、平均填写时间等多个关键绩效指标 (KPI) 上表现如何。通过跟踪用户行为和反馈，可确定导致混淆的表单区域，并指导改进表单的设计和功能。

  ![自适应表单用户参与 Adobe Analytics 报告](/help/forms/assets/forms-analytics-report.png)

* **[自适应表单中基于核心组件的表单片段](/help/forms/adaptive-form-fragments-core-components.md)**：在用表单片段提升您的表单生成体验时告别重复、优化数字库存并改善协作。这些可重用的组件无缝集成到多个表单中，从而简化创建一致且外观专业的表单的过程。利用“一次更改，随处反映”功能，表单片段确保实现可重用性、标准化和品牌一致性。由于在一处作出的更新自动传播到所有利用这些片段的表单，因此可体验到更高的可维护性和效率。

* **[增强的 Adobe Sign 工作流步骤](/help/forms/aem-forms-workflow-step-reference.md#sign-document-step-sign-document-step)**：增强了 Adobe Sign 工作流步骤以包括以下各项：
   * **Adobe Sign 的基于 Government ID 的身份验证**：Adobe Acrobat Sign 的基于 Government ID 的身份验证通过使用户可使用政府颁发的 ID（驾照、身份证、护照）验证其身份，多提供一层验证。通过利用可信身份证明文件，此增强将签名过程的可信度提高一级，使其成为需要更高的安全性、合规性和用户验证的场景的理想之选。

   * **Adobe Sign 文档的审核记录**：使用审核记录功能可详细了解 Adobe Sign 文档的生命周期。利用审核记录功能，您现在可保留与文档相关的所有操作和交互的全面记录。其中包括查看者、编辑者或签署文档者以及每个事件的时间戳等详细信息。此增强对于保持合规性、解决争议和确保数字协议的完整性至关重要。

   * **协议接收者在签名者之外的新角色**：Adobe Acrobat Sign 可将协议接收者的角色扩充到仅签名者之外以更好地满足其工作流要求。启用此选项后，协议中的每个接收者均可单独配置其角色，其中签名者为默认角色。

* **[用 Document Assurance API（Communication API 的一部分）保护文档](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance-doc-assurance)**：Document Assurance API 使您可通过为文档签名和加密而保护敏感信息。通过加密，可将文档内容转换为无法读取的格式，从而确保只有获得授权的用户可访问。这一层加强的保护不仅防止未经授权地查看宝贵的数据，还能让人安心。利用 Signature API，您的组织可以保护其分发和接收的 Adobe PDF 文档的安全和隐私。此服务使用数字签名和认证确保只有预期的接收者可更改文档。

* **Communication API 中支持页面计数**：除了通过 Communication API 检索文档之外，现在还可接收关于文档内所含页数的宝贵信息。

* **[使用规则编辑器中的自定义错误处理程序处理错误](/help/forms/add-custom-error-handler-adaptive-forms-core-components.md)**：现在可调用自定义函数以响应外部服务返回的错误，并为最终用户提供量身定制的响应。例如，可在后端为特定的错误代码调用自定义工作流或通知客户服务已停止。


### Headless 自适应表单早期采用者计划 {#forms-early-adopter}

使用 [Headless 自适应表单](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html)可让您的开发人员创建、发布和管理交互式表单，这些交互式表单可通过 API 而不是传统的图形用户界面进行访问和交互。Headless 自适应表单可帮助您：

* 使用选定的编程语言构建高质量的多渠道表单
* 将表单本机集成到您的桌面和移动应用程序、网站和聊天应用程序
* 在表单应用程序中重复使用您的专有 UI 组件
* 利用 Adobe Experience Manager Forms 的强大功能

您可以使用官方电子邮件 ID 将电子邮件发送到 `aem-forms-headless@adobe.com` 以加入早期采用者计划。


## [!DNL Experience Manager]as a[!DNL Cloud Service] Foundation {#foundation}

### CDN 日志 {#cdn-logs}

从 Cloud Manager 下载 CDN 日志，这对于优化缓存命中率和更加了解内容投放流很有用。[了解](/help/implementing/developing/introduction/logging.md#cdn-log) CDN 日志格式。将于 9 月初逐步向客户推出此功能。

### CDN 和 WAF 规则早期采用者计划 {#waf-early-adopter}

基于以下项筛选 CDN 上的流量：

* 请求标头和属性（例如，IP 地址）
* 已知与恶意流量相关的流量模式

想试用该功能并分享反馈吗？使用您的官方电子邮件 ID 将电子邮件发送到 **aemcs-waf-adopter@adobe.com**，了解有关早期采用者计划的更多信息。空间是有限的。

在[此处](/help/security/traffic-filter-rules-including-waf.md)的文章中详细了解该功能。


## 维护发行说明 {#maintenance}

您可以在[此处](/help/release-notes/maintenance/latest.md)找到最新的维护发行说明。

## Cloud Manager {#cloud-manager}

您可以在[此处](/help/implementing/cloud-manager/release-notes/current.md)找到 Cloud Manager 每月发布的完整列表。

## 迁移工具 {#migration-tools}

您可以在[此处](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)找到迁移工具版本的完整列表。
