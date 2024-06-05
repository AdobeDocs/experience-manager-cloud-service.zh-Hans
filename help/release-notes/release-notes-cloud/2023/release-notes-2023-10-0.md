---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 2023.10.0 版的发行说明。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 2023.10.0 版的发行说明。'
exl-id: 81a6cbd2-7101-429b-8572-2650c5bea963
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '918'
ht-degree: 91%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 2023.10.0 版的发行说明 {#release-notes}

以下部分概述了 2023.10.0 版的 [!DNL Experience Manager] as a Cloud Service 的功能发行说明。

>[!NOTE]
>
>您可以在此部分中导航到早期版本的发行说明；例如，2021 版或 2022 版等的发行说明。
>
>查看 [Experience Manager 版本发行路线图](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html)，了解即将推出的 [!DNL Experience Manager] as a Cloud Service 的功能激活。

>[!NOTE]
>
>有关未与版本直接相关的文档更新的详细信息，请参阅[最新文档更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html)。

## 发布日期 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 的当前功能版本 (2023.10.0) 的发布日期为 2023 年 10 月 26 日。下一个功能版本 (2023.11.0) 计划于 2023 年 11 月 30 日发布。

## 维护发行说明 {#maintenance}

您可以在[此处](/help/release-notes/maintenance/latest.md)找到最新的维护发行说明。

## 发布视频 {#release-video}

观看 2023 年 10 月版概述视频，大致了解 2023.10.0 版的新增功能：

>[!VIDEO](https://video.tv.adobe.com/v/3425186/?quality=12)

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### 新增功能 {#assets-features}

**适用于Adobe Express的AEM Assets加载项**：Experience Manager Assets现在为Adobe Express提供了一个加载项。 通过该插件可以直接从 Adobe Express 用户界面访问存储在 Experience Manager Assets 内的资源。可将在 AEM Assets 中管理的内容放入 Express 画布，然后将新内容或经过编辑的内容保存在 AEM Assets 存储库中。该加载项主要有以下几项优势：

* 通过在 AEM 中编辑和保存新资源，提高了内容重用程度

* 减少了创建新资源或创建现有资源的新版本所需的总体时间和工作量

  ![从 Assets 加载项纳入资源](/help/assets/assets/aem-assets-add-on-include-assets.png)

### 资源视图中的新增功能 {#assets-view-features}

* **从OneDrive数据源批量导入资产**：管理员现在能够 [将大量资源从OneDrive导入到AEM Assets](/help/assets/bulk-import-assets-view.md#onedrive-developer-application). 支持批量导入的数据源的更新列表包括 Azure、AWS、Google Cloud、Dropbox 和 OneDrive。

  ![将元数据表单分配给文件夹](/help/assets/assets/bulk-import-source-details-onedrive.png)

* **跨组织授权库支持**：现在通过Experience Manager Assets可配置对其他IMS组织中的Creative Cloud库的访问权限。 这样可更轻松地访问 Creative Cloud 与 Experience Manager 之间最新的跨产品工作流，并减少创意人员花费的时间和精力。

### 可在 [!DNL Experience Manager Assets] 中找到的预发布功能 {#prerelease-features-assets}

* **Dynamic Media**：[Dynamic Media 中的视频支持多字幕和多音轨](/help/assets/dynamic-media/video.md#about-msma)，现在可轻松地将多个字幕和多个音轨添加到主视频。此功能意味着全球观众都能看懂您的视频。只需自定义一个主视频，即可发布到多种语言的全球观众，并遵循不同地区的辅助功能准则。此外，作者从用户界面中的一个选项卡即可管理字幕和音轨。

  ![所选视频资源的“属性”页面上的“字幕和音轨”选项卡。](/help/release-notes/assets/msma-aem-cs.png)*所选视频资源的“属性”页面上的“字幕和音轨”选项卡。*

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Experience Manager Forms] 中的新增功能 {#forms-features}

* **[自适应表单的自定义属性](/help/forms/template-editor-core-components.md#add-a-custom-group-name-in-the-policy-of-template-editor)**：您可以将自定义属性（键值对）与表单模板或自适应表单组件相关联，以允许表单开发人员提供根据这些自定义属性的值进行调整的动态表单行为。例如，开发人员可以根据自定义属性的值在移动、桌面或 Web 平台上制作 Headless Forms 组件的不同版本，从而显着增强各种设备上的用户体验。

* **主题和模板**：使用我们新的主题和模板开始您的表单创建过程，这些主题和模板专为经验丰富的专业人士和新表单作者定制。这些精心策划的主题和模板是使用自适应表单核心组件无缝构建的，可让您快速开始为常见用例创建表单。

  ![现成的模板](/help/forms/assets/form-templates-ootb.png)


### 早期采用者计划 {#forms-early-adopter}

* **[用 DocAssurance API（Communication API 的一部分）保护文档](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance-doc-assurance)**：DocAssurance API 使您能够通过为文档签名和加密来保护敏感信息。通过加密，可将文档内容转换为无法读取的格式，从而确保只有获得授权的用户可访问。这一层加强的保护不仅防止未经授权地查看宝贵的数据，还能让人安心。利用 Signature API，您的组织可以保护其分发和接收的 Adobe PDF 文档的安全和隐私。此服务使用数字签名和认证确保只有预期的接收者可更改文档。

  您可以通过您的官方电子邮件 ID 向 `aem-forms-ea@adobe.com` 发送电子邮件，以加入早期采用者计划并请求对该功能的访问权限。

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### 流量过滤规则（包括 WAF） {#traffic-filter-rules-waf}

[通过声明按属性（包括 URL、IP 地址和用户代理）匹配网站流量的规则，过滤 Adobe Managed CDN ](/help/security/traffic-filter-rules-including-waf.md)上的流量，或设置自定义流量速率限制以防范 DoS 攻击。客户还可以许可一组高级 Web 应用程序防火墙 (WAF) 规则，以针对复杂的网站威胁提供额外的保护。

我们建议您通过以下方式熟悉流量过滤器规则 [试用教程](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/security/traffic-filter-and-waf-rules/overview.html)！ 它会引导您完成设置新的 Cloud Manager 配置管道、在配置文件中声明规则，以及分析 CDN 日志中的恶意流量。

目前开发环境上具有可用的流量过滤规则，并将会在 11 月份逐步推广到暂存和生产环境。通过向 **aemcs-waf-adopter@adobe.com** 发送电子邮件，可申请提前在暂存和生产环境上使用该功能。

高级 WAF 流量过滤规则可在今年晚些时候通过增强安全性或 WAF-DDoS 防护产品获得许可。

## Cloud Manager {#cloud-manager}

您可以在[此处](/help/implementing/cloud-manager/release-notes/current.md)找到 Cloud Manager 每月发布的完整列表。

## 迁移工具 {#migration-tools}

您可以在[此处](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)找到迁移工具版本的完整列表。
