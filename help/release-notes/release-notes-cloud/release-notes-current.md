---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 的最新发行说明。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 的最新发行说明。'
mini-toc-levels: 1
source-git-commit: 085ce15ebe4d48d32a437f13e728f60cfc57d0fa
workflow-type: tm+mt
source-wordcount: '733'
ht-degree: 34%

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

的发行日期 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 最新功能版本(2023.2.0)是2023年4月12日发布的。 下一个功能版本 (2023.4.0) 计划于 2023 年 4 月 27 日发布。

## 发布视频 {#release-video}

观看2023年2月版概述视频，了解2023.2.0版本中添加的功能摘要：

>[!VIDEO](https://video.tv.adobe.com/v/3416885/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### [!DNL Experience Manager Sites] 中的新增功能 预租 {#prerelease-sites}

* 将内容片段从AEM as a cloud service导出为JSON选件AdobeTarget。
* 现在，支持GraphQL分页和排序以及内部缓存增强功能，有助于在使用复杂的GraphQL查询和过滤器从AEM获取大量内容集时，提高解耦的客户端应用程序的性能。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets] 中的新增功能 {#assets-features}

* 在Dynamic Media视频交付中为自适应流播放启动了新协议（DASH — 通过HTTP的动态自适应流播放）支持（启用CMAF）：
   * 自适应流播放(DASH/HLS)可确保最终用户更好地观看视频
   * DASH是自适应视频流传输的国际标准协议，在业界得到广泛采用
   * 在NA提供，将通过支持票证启用，即将在APAC、EMEA提供

* 增加了对WebP图像的支持，可自动提取元数据、生成缩略图和自定义演绎版。 这些文件现在还支持智能标记和智能裁剪功能。

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] 中的新增功能 {#new-features-available-in-channel}

* **[使用数据捕获核心组件以构建自适应表单](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=zh-Hans)**:[使用自适应表单编辑器](/help/forms/creating-adaptive-form-core-components.md)创建基于标准化数据捕获组件（核心组件）的表单。对于您的数字注册体验，这些组件可以提供定制功能，缩短开发时间和降低维护成本。

* **[基于自适应Forms的核心组件样式设计前端管道支持](/help/forms/using-themes-in-core-components.md)**:将基于BEM的标准化主题用于基于核心组件的自适应Forms，方法是使用前端部署管道部署这些主题，以增强表单的外观，并与组织品牌批准的设计准则保持一致。

* **[为基于核心组件的自适应Forms生成记录文档](/help/forms/generate-document-of-record-core-components.md)**:创建记录文档，其中包含已提交的数据，这些数据是使用核心组件构建的，用于存档或引用最终用户（以打印形式或文档格式）。

![https://www.aemcomponents.dev/](/help/forms/assets/sample-core-components-based-adaptive-form.png)

* **[使用将自适应表单另存为模板功能来高效构建表单](/help/forms/template-editor.md#save-an-adaptive-form-as-template-saving-adaptive-form-as-template)**:通过将现有品牌批准的表单保存为表单模板以便快速重复使用，从而加快和标准化表单开发。

* **[将AEM Forms连接到JDBC支持的数据库](/help/forms/configure-data-sources.md#configure-relational-database-configure-relational-database)**:使用JDBC协议直接从AEM云服务连接到企业数据库，无需通过REST API公开它们。

* **[使用Open API 3.0与REST端点集成](/help/forms/configure-data-sources.md#configure-restful-services-open-api-specification-version-20-configure-restful-services-swagger-version30)**:无缝集成到支持Open API 3.0的记录系统中，以使用表单数据模型存储和获取数据。

* **[共享自适应表单以进行审阅](/help/forms/create-reviews-forms.md)**：使用自适应表单审阅机制以允许一个或多个审阅者审阅表单。


### 的功能 [!DNL Forms] 预发行 {#prerelease-features-forms}

* **[将自适应Forms提交到Microsoft SharePoint和Microsoft OneDrive](/help/forms/configuring-submit-actions.md)**:提高企业用户快速启动新表单的敏捷性，并将提交的数据存储在日常工具中，如Microsoft SharePoint网站或OneDrive文件夹。

![将自适应Forms提交到Microsoft SharePoint和Microsoft OneDrive](/help/forms/assets/onedrive-and-sharepoint.jpg)


## 无头自适应Forms早期采用者计划 {#forms-early-adopter}

使用无头自适应Forms，使您的开发人员能够创建、发布和管理可通过API访问和交互的交互式表单，而不是通过传统的图形用户界面进行访问和交互。 无头自适应表单可帮助您：

* 使用您选择的编程语言构建高质量的多渠道表单
* 将表单本地集成到桌面和移动设备应用程序、网站和聊天应用程序
* 将您专有的UI组件与表单应用程序结合使用
* 利用Adobe Experience Manager Forms的力量

您可以从官方电子邮件ID向aem-forms-headless@adobe.com发送电子邮件，以加入早期采用者计划。

## 维护发行说明 {#maintenance}

您可以在[此处](/help/release-notes/maintenance/latest.md)找到最新的维护发行说明。

## Cloud Manager {#cloud-manager}

您可以在[此处](/help/implementing/cloud-manager/release-notes/current.md)找到 Cloud Manager 月度发行版本的完整列表。

## 迁移工具 {#migration-tools}

您可以在[此处](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)找到迁移工具版本的完整列表。
