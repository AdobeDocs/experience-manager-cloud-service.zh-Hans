---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 的最新发行说明。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 的最新发行说明。'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
source-git-commit: 407afc27911c507d3662fa4897b29e8187bbec7a
workflow-type: tm+mt
source-wordcount: '1934'
ht-degree: 26%

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

的发布日期 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 当前功能版本(2023.8.0)为2023年8月31日。 下一个功能版本(2023.9.0)计划于2023年9月28日发布。

## 发布视频 {#release-video}

请查看 2023 年 8 月发布概述视频，了解 2023.8.0 版本中新增功能的摘要：

>[!VIDEO](https://video.tv.adobe.com/v/3423535/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### [!DNL Experience Manager Sites] 中的新增功能 {#sites-features}

* [内容片段控制台](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/content-fragments/content-fragments-console.html?lang=zh-Hans)现在允许用户查看标记并按作为元数据应用于内容片段的标记进行搜索。用户将不再需要切换到此功能的资源 UI，这减少了上下文切换并提高了效率。

  ![内容片段控制台中的标记](/help/assets/content-fragments-console-tags.png)
* 现在，AEMas a Cloud Service上提供了新的内容片段编辑器。 它通过简化内容作者的创作任务并减少在编辑内容时在不同应用程序之间切换的需求，使内容作者能够更高效。
  ![新的内容片段编辑器](/help/release-notes/assets/newCFEditor.png)

新的内容片段编辑器提供了原始编辑器中未提供的以下优势：
* 自动保存可提高创作效率并防止意外丢失编辑。
* 使用结构树在深度结构化片段中快速导航内容片段及其引用的分级视图。
  ![内容片段编辑器中的结构树](/help/release-notes/assets/newCFEditor_StructureTree.png)

* 无需先将资产上传到资产DAM，即可将资产作为内容引用进行内联上传
* 内容片段交付的呈现体验的临时预览，帮助作者在前端应用程序上可视化内容的外观
* 通过单击从编辑器中发布和取消发布内容片段
* 在编辑内容片段时查看和导航到语言副本
  ![内容片段编辑器中的语言副本](/help/release-notes/assets/newCFEditor_LanguageCopies.PNG)

* 查看版本以帮助跟踪内容片段的时间线

  ![内容片段编辑器中的版本](/help/release-notes/assets/newCFEditor_Versionhistory.PNG)

* 查看父引用以帮助作者了解其编辑的影响

  ![内容片段编辑器中的父引用](/help/release-notes/assets/newCFEditor_Parentreferences.PNG)

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### 资源视图中的新增功能 {#assets-view-features}

<!--

**Assign metadata form to a folder**

You can now assign metadata form to a specific folder within your Assets Essentials deployment. All assets in the folder, including assets in the sub-folders, then display properties defined in the assigned metadata form.

![assign metadata form to a folder](/help/release-notes/assets/assign-to-folder.png)

-->

* **从数据源批量导入资源**：管理员现在拥有 [能够导入大量资源](/help/assets/bulk-import-assets-view.md) 从数据源到AEM Assets。 管理员不再需要将单个资源或文件夹上传到 AEM Assets。支持批量导入的数据源包括 Azure、AWS、Google Cloud 和 Dropbox。

  ![从数据源批量导入资源](/help/release-notes/assets/bulk-import.png)

* **由 Adob&#x200B;&#x200B;e Express 提供支持的图像编辑工具**：简单直观 [由Adobe Express提供支持的图像编辑工具](/help/assets/edit-images-assets-view.md) 可直接在AEM Assets中使用，以提高内容重复使用率并加快内容速度。

  ![使用 Adob&#x200B;&#x200B;e Express 进行图像编辑](/help/release-notes/assets/edit-adobe-express.png)

* **可灵活地为“我的工作区”的“快速访问”部分固定相关的项目**：可以为您、整个组织或组列表选择并固定项目，以便它们显示在 [我的工作区的“快速访问”部分](/help/assets/my-workspace-assets-view.md) 根据您的选择。

  ![为群组固定项目](/help/release-notes/assets/pin-items-for-groups.png)

### “管理员”视图中的新增功能 {#admin-view-features}

**搜索增强功能**

* 管理员现在可以 [配置资产的批次大小](/help/assets/search-assets.md#configure-asset-batch-size) 执行搜索时显示的对象。 当您进一步向下滚动以加载结果时，资源搜索结果将以配置的批次大小数字的倍数显示。 您可以从可用批量大小的200、500和1000项资源中进行选择。 设置较小的批次大小数字可加快搜索响应时间。

  ![资产批次大小配置](/help/release-notes/assets/assets-batch-size-configuration.png)

* Experience Manager Assets现在包含新版本9 `damAssetLucene` 索引。 `damAssetLucene-9` 将Oak查询Facet计数行为更改为 [不再评估Facet计数上的访问控制](/help/assets/search-assets.md) 由基础搜索索引返回，这将导致更快的搜索响应时间。

### [!DNL Experience Manager Assets] 中的预发布功能 {#prerelease-features-assets}

* **Dynamic Media**： [Dynamic Media中支持视频的多字幕和多音频轨道](/help/assets/dynamic-media/video.md#about-msma) — 您现在可以轻松地将多个字幕和多个音轨添加到主视频中。 这项功能意味着您的视频可在全球受众中访问。 您可以采用多种语言向全球受众自定义单个已发布的主视频，并遵守适用于不同地理区域的辅助功能准则。 作者还可以在用户界面中通过单个选项卡管理字幕和音轨。

  ![在所选视频资产的属性页面上，单击“字幕和音频轨道”选项卡。](/help/release-notes/assets/msma-aem-cs.png)*在所选视频资产的属性页面上，单击“字幕和音频轨道”选项卡。*

* **资产**：能够选择在Experience Manager中管理的ZIP存档并 [将文件直接解压到Experience Manager中](/help/assets/manage-digital-assets.md#extract-zip-archives) 而不下载。

  ![为群组固定项目](/help/release-notes/assets/extract-archive.png)


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] 中的预发布功能 {#pre-release-features-available-in-forms-channel}

* [**Google reCAPTCHA 企业支持**](/help/forms/captcha-adaptive-forms-core-components.md)：在自适应表单中使用 Google reCAPTCHA Enterprise 以增强对欺诈活动和垃圾邮件的防御，从而提供更安全的用户体验。借助高级风险分析和无缝集成，真实用户可以轻松提交表单，同时有效阻止机器人。

* [**Adobe Analytics与Forms的Experience Cloud设置自动化**](/help/forms/forms-experience-cloud-setup-automation.md)：您现在可以使用两个按钮来启用具有Experience Cloud设置自动化的Adobe Analytics。 它允许您将AEM Formsas a Cloud Service与Experience Platform标记和Adobe Analytics连接起来，以捕获和跟踪已发布表单的性能指标。

* [**自适应Forms的Adobe Analytics报表模板**](/help/forms/view-understand-aem-forms-analytics-reports.md)：Formsas a Cloud Service现在提供Adobe Analytics报表OOTB。 它有助于您轻松了解表单的性能。 通过表单级量度，可深入分析表单在多个关键绩效指标(KPI)（如呈现版本、访客、提交、平均填充时间）上的执行情况。 通过跟踪用户行为和反馈，您可以识别导致混淆的表单区域，并指导改进表单的设计和功能。

  ![自适应表单用户参与adobe analytics报告](/help/forms/assets/forms-analytics-report.png)

* **[基于核心组件的自适应Forms中的表单片段](/help/forms/adaptive-form-fragments-core-components.md)**：在您提升使用表单片段的表单构建体验时，告别复制、优化数字库存并改进协作。 这些可重复使用的组件可无缝地集成到多种表单中，从而简化了一致且具有专业外观的表单的创建。 表单片段通过“一次更改并随时随地反映”功能确保可重用性、标准化和品牌一致性。 体验更好的可维护性和效率，因为在一个位置进行的更新会自动传播到使用这些片段的所有表单中。

* **[增强的Adobe Sign工作流步骤](/help/forms/aem-forms-workflow-step-reference.md#sign-document-step-sign-document-step)**：Adobe Sign工作流步骤已得到增强，现包括以下内容：
   * **适用于Adobe Sign的基于政府ID的身份验证**：Adobe Acrobat Sign基于Government ID的身份验证允许用户使用政府颁发的ID（驾照、身份证、护照）进行身份验证，从而提供了一层额外的验证。 通过利用受信任的标识文档，此增强功能为签名过程增添了更高的置信度，使其非常适合需要增强的安全性、合规性和用户验证的情况。

   * **Adobe Sign文档的审核跟踪**：使用审核记录功能可详细分析Adobe Sign文档的生命周期。 通过跟踪线索，您现在可以维护与文档相关的所有操作和交互的全面记录。 这包括查看者、编辑者或签名者等详细信息，以及每个事件的时间戳。 此增强功能对于维护合规性、解决争议和确保数字协议的完整性至关重要。

   * **协议收件人的新角色，而不只是签名者**：Adobe Acrobat Sign可以选择将协议接受者的角色扩展至签名者之外，以便更好地匹配他们的工作流要求。 启用后，协议中的每个收件人可以单独配置其角色，签名者是默认角色。

* **[使用Document Assurance API（通信API的一部分）Protect文档](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance-doc-assurance)**：文档保证API允许您通过签名和加密文档来保护敏感信息。 通过加密，文档的内容转换为不可读的格式，确保只有授权用户才能获得访问权限。 此强化的保护层不仅能够保护宝贵的数据不受未经授权的用户的攻击，而且还能让您高枕无忧。 签名API允许贵组织保护其分发和接收的Adobe PDF文档的安全性和隐私。 此服务使用数字签名和认证，确保只有目标收件人才能更改文档。

* **通信API中的页数支持**：现在，在通过通信API检索文档的同时，您还可以收到有关文档中所包含页数的宝贵信息。

* **[在规则编辑器中使用自定义错误处理程序进行错误处理](/help/forms/add-custom-error-handler-adaptive-forms-core-components.md)**：您现在可以调用自定义函数来响应外部服务返回的错误，并为最终用户提供量身定制的响应。 例如，您可以在后端为特定的错误代码调用自定义工作流，或者通知客户服务已停止。

* **[AEM Forms Designer的64位版本](/help/forms/installing-configuring-designer.md)**：AEM Forms Designer的64位版本提供了增强的性能、可扩展性和内存管理，可增强您的表单创建体验。 借助64位架构，您可以轻松处理更大、更复杂的项目，从而确保无缝的设计工作流程和优化的效率。 通过这个尖端版本提升您的表单设计功能并拥抱AEM Forms Designer的未来。


### 率先采用者计划 {#forms-early-adopter}

* **[使用DocAssurance API（通信API的一部分）Protect您的文档](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance-doc-assurance)**：DocAssurance API允许您通过签名和加密文档来保护敏感信息。 通过加密，文档的内容转换为不可读的格式，确保只有授权用户才能获得访问权限。 此强化的保护层不仅能够保护宝贵的数据不受未经授权的用户的攻击，而且还能让您高枕无忧。 签名API允许贵组织保护其分发和接收的Adobe PDF文档的安全性和隐私。 此服务使用数字签名和认证，确保只有目标收件人才能更改文档。

      您可以从官方电子邮件ID写入“aem-forms-early-adopter-program@adobe.com”，以加入率先采用者计划并请求获取该功能的访问权限。
  
* **[Headless自适应Forms](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html)**：使用Headless自适应Forms，让开发人员能够创建、发布和管理可通过API（而不是通过传统的图形用户界面）访问和交互的交互式表单。 Headless 自适应表单可帮助您：

   * 使用选定的编程语言构建高质量的多渠道表单
   * 将表单本机集成到您的桌面和移动应用程序、网站和聊天应用程序
   * 在表单应用程序中重复使用您的专有 UI 组件
   * 利用 Adobe Experience Manager Forms 的强大功能

  您可以使用官方电子邮件 ID 将电子邮件发送到 `aem-forms-headless@adobe.com` 以加入早期采用者计划。


## [!DNL Experience Manager]as a[!DNL Cloud Service] Foundation {#foundation}

### CDN 日志 {#cdn-logs}

从Cloud Manager下载CDN日志，这对于优化缓存命中率以及增强内容投放流的可见性非常有用。 [了解](/help/implementing/developing/introduction/logging.md#cdn-log) cdn日志格式。 该功能将于9月初逐步向客户推出。

### CDN 和 WAF 规则早期采用者计划 {#waf-early-adopter}

基于以下项筛选 CDN 上的流量：
* 请求头和属性（例如，IP 地址）
* 已知与恶意流量相关的流量模式

想试用该功能并分享反馈吗？使用您的官方电子邮件 ID 将电子邮件发送到 **aemcs-waf-adopter@adobe.com**，了解有关早期采用者计划的更多信息。空间是有限的。

在[此处](/help/security/cdn-and-waf-rules.md)的文章中详细了解该功能。


## 维护发行说明 {#maintenance}

您可以在[此处](/help/release-notes/maintenance/latest.md)找到最新的维护发行说明。

## Cloud Manager {#cloud-manager}

您可以在[此处](/help/implementing/cloud-manager/release-notes/current.md)找到 Cloud Manager 每月发布的完整列表。

## 迁移工具 {#migration-tools}

您可以在[此处](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)找到迁移工具版本的完整列表。
