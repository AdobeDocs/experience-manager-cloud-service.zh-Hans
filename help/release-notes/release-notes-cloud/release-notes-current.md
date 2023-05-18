---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 的最新发行说明。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 的最新发行说明。'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
source-git-commit: d202b0543020b277de982e3965475074a71b286d
workflow-type: tm+mt
source-wordcount: '730'
ht-degree: 98%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 的最新发行说明 {#release-notes}

以下部分概述了当前（最新）版本的 [!DNL Experience Manager] as a Cloud Service 的功能发行说明。

>[!NOTE]
>
>您可以在此部分中导航到早期版本的发行说明；例如，2021 版、2022 版等的发行说明。
>
>查看 [Experience Manager 版本发行路线图](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html)，了解即将推出的 [!DNL Experience Manager] as a Cloud Service 的功能激活。

>[!NOTE]
>
>有关未与版本直接相关的文档更新的详细信息，请参阅[最新文档更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html)。

## 发布日期 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 最新功能版本 (2023.2.0) 的发布日期为 2023 年 4 月 12 日。下一个功能版本 (2023.4.0) 计划于 2023 年 5 月 25 日发布。

## 发布视频 {#release-video}

观看 2023 年 2 月版概述视频，大致了解 2023.2.0 版的新增功能：

>[!VIDEO](https://video.tv.adobe.com/v/3416885/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### [!DNL Experience Manager Sites] 中的新增功能预发行版 {#prerelease-sites}

* 将内容片段作为 JSON 选件从 AEM as a Cloud Service 导出到 Adobe Target。
* 现在，利用对 GraphQL 分页和排序的支持以及内部缓存增强功能，可以在使用复杂的 GraphQL 查询和筛选条件从 AEM 获取大型内容集时帮助提高已解耦客户端应用程序的性能。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets] 中的新增功能 {#assets-features}

* 推出了面向 Dynamic Media 视频交付（已启用 CMAF）中的自适应流式处理的新协议（DASH – 基于 HTTP 的动态自适应流式处理）支持：
   * 自适应流式处理 (DASH/HLS) 可确保最终用户获得更出色的视频观看体验
   * DASH 是自适应视频流式处理的国际标准协议，在业界得到广泛应用
   * 已在北美推出，将通过支持票证启用，并且即将在亚太地区以及欧洲、中东和非洲推出

* 增加了对 WebP 图像的支持，可自动提取元数据、生成缩略图和自定义演绎版。这些文件现在也支持智能标记功能。

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] 中的新增功能 {#new-features-available-in-channel}

* **[使用数据捕获核心组件以构建自适应表单](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=zh-Hans)**:[使用自适应表单编辑器](/help/forms/creating-adaptive-form-core-components.md)创建基于标准化数据捕获组件（核心组件）的表单。对于您的数字注册体验，这些组件可以提供定制功能，缩短开发时间和降低维护成本。

* **[对设置基于核心组件的自适应表单样式的前端管道支持](/help/forms/using-themes-in-core-components.md)**：为基于核心组件的自适应表单使用标准化的 BEM 相关主题，方式是使用前端部署管道部署，从而改进表单外观并遵循组织品牌批准的设计准则。

* **[为基于核心组件的自适应表单生成记录文档](/help/forms/generate-document-of-record-core-components.md)**：为使用核心组件构建的自适应表单创建包含提交数据的记录文档以进行存档或供最终用户参考（采用打印或文档格式）。

![https://www.aemcomponents.dev/](/help/forms/assets/sample-core-components-based-adaptive-form.png)

* **[使用“将自适应表单另存为模板”功能高效构建表单](/help/forms/template-editor.md#save-an-adaptive-form-as-template-saving-adaptive-form-as-template)**：通过将现有品牌批准的表单另存为表单模板以便快速重复使用，来加快和标准化表单制作。

* **[将 AEM Forms 连接到支持 JDBC 的数据库](/help/forms/configure-data-sources.md#configure-relational-database-configure-relational-database)**：使用 JDBC 协议直接从 AEM Cloud 服务连接到企业数据库，而无需通过 REST API 公开它们。

* **[使用 Open API 3.0 与 REST 端点集成](/help/forms/configure-data-sources.md#configure-restful-services-open-api-specification-version-20-configure-restful-services-swagger-version30)**：无缝集成到支持 Open API 3.0 的记录系统中，以使用表单数据模型存储和提取数据。

* **[共享自适应表单以进行审阅](/help/forms/create-reviews-forms.md)**：使用自适应表单审阅机制，可允许一个或多个审阅者审阅表单。


### [!DNL Forms] 预发行版本中的功能 {#prerelease-features-forms}

* **[将自适应表单提交到 Microsoft SharePoint 和 Microsoft OneDrive](/help/forms/configuring-submit-actions.md)**：提高业务用户的敏捷性，以快速启用新表单并将提交的数据存储在日常使用工具中，例如 Microsoft SharePoint 站点或 OneDrive 文件夹。

![将自适应表单提交到 Microsoft SharePoint 和 Microsoft OneDrive](/help/forms/assets/onedrive-and-sharepoint.jpg)


## Headless 自适应表单早期采用者计划 {#forms-early-adopter}

使用 Headless 自适应表单可让您的开发人员创建、发布和管理交互式表单，这些交互式表单可通过 API 而不是传统的图形用户界面进行访问和交互。Headless 自适应表单可帮助您：

* 使用选定的编程语言构建高质量的多渠道表单
* 将表单本机集成到您的桌面和移动应用程序、网站和聊天应用程序
* 在表单应用程序中重复使用您的专有 UI 组件
* 利用 Adobe Experience Manager Forms 的强大功能

您可以使用官方电子邮件 ID 将电子邮件发送到 aem-forms-headless@adobe.com 以加入早期采用者计划。

## 维护发行说明 {#maintenance}

您可以在[此处](/help/release-notes/maintenance/latest.md)找到最新的维护发行说明。

## Cloud Manager {#cloud-manager}

您可以在[此处](/help/implementing/cloud-manager/release-notes/current.md)找到 Cloud Manager 月度发行版本的完整列表。

## 迁移工具 {#migration-tools}

您可以在[此处](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)找到迁移工具版本的完整列表。
