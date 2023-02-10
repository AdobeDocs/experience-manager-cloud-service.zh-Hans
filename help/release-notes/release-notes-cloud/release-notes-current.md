---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 的最新发行说明。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 的最新发行说明。'
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
mini-toc-levels: 1
source-git-commit: 400e9fa0263b3e9bdae10dc80d524b291f99496d
workflow-type: tm+mt
source-wordcount: '1032'
ht-degree: 21%

---


# [!DNL Adobe Experience Manager] as a Cloud Service 的最新发行说明 {#release-notes}

以下部分概述了当前（最新）版本的 [!DNL Experience Manager] as a Cloud Service。

>[!NOTE]
>
>您可以在此部分中导航到早期版本的发行说明；例如，2021 版、2022 版等的发行说明。
>
>请查看 [Experience Manager版本路线图](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=zh-Hans) 要了解即将启动的 [!DNL Experience Manager] as a Cloud Service。

>[!NOTE]
>
>有关未与版本直接相关的文档更新的详细信息，请参阅[最新文档更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html)。

## 发布日期 {#release-date}

的发行日期 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 最新功能发布(2023.1.0)是2023年2月9日。 下一个功能版本(2023.2.0)计划于2023年3月2日发布。

## 发布视频 {#release-video}

观看2023年1月版概述视频，了解2023.1.0版中添加的功能摘要：

>[!VIDEO](https://video.tv.adobe.com/v/3413479/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### [!DNL Sites] 预发布中的新增功能 {#prerelease-features-sites}

* AEM GraphQL内容交付API现在支持GraphQL [分页](/help/headless/graphql-api/content-fragments.md#paging) 和 [排序](/help/headless/graphql-api/content-fragments.md#sorting)，以提高获取和渲染大内容集的效率。 GraphQL分页允许通过在子集中返回结果而不是一次全部返回来缩短查询响应时间。 GraphQL排序允许按所需的顺序放置内容集，从而让客户端应用程序更轻松地处理内容。  在AEM GraphQL引擎中使用混合过滤功能可进一步缩短查询响应时间。 现在，在与查询过滤器对应的较小集中，从JCR读取内容。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets] 中的新增功能 {#assets-features}

* 资产报表现在包括管理员 [生成资产下载报表](/help/assets/asset-reports.md) 从Experience Manager Assetsas a Cloud Service部署。 此数据进一步允许管理员从关键成功量度中获得洞察，以衡量企业内和客户对资产的采用情况。

   ![其他格式的 PDF 演绎版](/help/release-notes/assets/choose_report.png)

* 除了用于身份验证的 Access 密钥外，Experience Manager Assets 现在还[支持 SAS 令牌](/help/assets/add-assets.md#asset-bulk-ingestor)，同时还连接到 Azure Blob 存储数据源，从而使用“批量导入”工具摄取资产。

* 改进了Asset compute中CMYK图像的管理，使您能够为CMYK图像生成智能裁剪和智能标记。

### [!DNL Assets] 预发布中的新增功能 {#prerelease-features-assets}

* Experience Manager Assets现在支持 [从Google云平台大规模摄取资产](/help/assets/add-assets.md#asset-bulk-ingestor) 使用“批量导入”工具。

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] 中的新增功能 {#new-features-available-in-channel}

* **[生成非交互式PDF文档和可打印输出的工作流步骤](/help/forms/aem-forms-workflow-step-reference.md)**:使用AEM Workflow步骤自动创建非交互式PDF文档和为业务流程打印的输出，从而简化文档生成过程并节省时间。
* **[使用脚注在《自适应Forms》中提供引文或额外信息](/help/forms/footnotes-richtextsupport.md)**:在自适应表单中使用脚注可显示有关如何完成或使用表单的信息。 您还可以使用它提供父主题信息、版权权限和其他有用信息。

### [!DNL Forms] 预发布中的新增功能 {#prerelease-features-forms}

* **[使用数据捕获核心组件构建自适应Forms](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=en)**: [使用自适应Forms编辑器](/help/forms/creating-adaptive-form-core-components.md) 创建基于标准化数据捕获组件（核心组件）的表单。 这些组件为您的数字注册体验提供了自定义功能、缩短了开发时间并降低了维护成本。
* **[基于自适应Forms的核心组件样式设计前端管道支持](/help/forms/using-themes-in-core-components.md)**:利用基于BEM的基于核心组件的自适应Forms轻松自定义的主题，通过使用前端部署管道部署这些主题来增强表单的外观。
* **[为基于核心组件的自适应Forms生成记录文档](/help/forms/generate-document-of-record-core-components.md)**:在提交以供长期存档、打印或文档格式时，为基于核心组件的自适应表单创建记录。

![https://www.aemcomponents.dev/](/help/forms/assets/sample-core-components-based-adaptive-form.png)

* **[将自适应Forms提交到Microsoft SharePoint和Microsoft OneDrive](/help/forms/configuring-submit-actions.md)**:简化数据提交过程，并且能够将自适应表单数据直接发送到Microsoft SharePoint和Microsoft OneDrive。 您可以提交基于架构和无架构的数据。 这些提交操作是除现有提交操作之外的其他操作。
* **[使用将自适应表单另存为模板功能来高效构建表单](/help/forms/template-editor.md#save-an-adaptive-form-as-template-saving-adaptive-form-as-template)**:通过将自适应表单保存为模板并重新使用用于下一个自适应表单的模板，可简化表单构建过程。
* **[将AEM Forms连接到JDBC支持的数据库](/help/forms/configure-data-sources.md#configure-relational-database-configure-relational-database)**:轻松将AEM Forms数据模型连接到支持JDBC的数据库，从而使您能够无缝地读写数据。
* **[使用Open API 3.0与REST端点集成](/help/forms/configure-data-sources.md#configure-restful-services-open-api-specification-version-20-configure-restful-services-swagger-version30)**:将AEM Formsas a Cloud Service表单数据模型连接到支持Open API规范版本3.0的REST端点，以便您轻松发送和接收数据。
* **[共享自适应表单以供审阅](/help/forms/create-reviews-forms.md)**:使用自适应Forms审阅机制，允许一个或多个审阅人审阅表单。


## CIF 加载项 {#cloud-services-cif}

### 新增功能 {#what-is-new-cif}

* 作者可以使用体验片段动态丰富产品列表（例如：在产品列表之间放置横幅）。
* 列表组件现在支持关联产品/类别页面，可动态显示相关页面。
* 添加了对 Peregrine 12.5 组件的支持。
* 添加了对产品 Teaser 和轮播中客户端价格加载的支持。

## [!DNL Experience Manager as a Cloud Service] Foundation {#foundation}

### 新增功能 {#what-is-new-foundation}

* [快速开发环境](/help/implementing/developing/introduction/rapid-development-environments.md) - RDE使开发人员能够快速排查问题并在AEMas a Cloud Service上部署新功能。

   快速开发环境是一种新型的云环境，旨在作为一种快速、一致且可扩展的方式，验证在本地工作的代码在云中也能按预期工作。 使用命令行工具，将内容包、包、内容文件、OSGI配置或调度程序配置快速“同步”到RDE。 请在以下视频中观看该视频的实际操作：

   >[!VIDEO](https://video.tv.adobe.com/v/3413508/?quality=12&learn=on)

   在RDE中成功验证代码后，我们鼓励先将该代码部署到云开发环境以执行Cloud Manager质量门，然后再通过生产管道部署到暂存环境和生产环境。

   每个程序都包括一个RDE，并且可选地，可以授权更多程序。

   >[!NOTE]
   >
   >未来几周将逐步推出RDE;您可以向aemcs-rde-support@adobe.com发送电子邮件，以跳到前线。

* [扩展了对服务器端API访问令牌的支持](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md)  — 您现在可以生成多个凭据，这对于API具有不同特征的情况非常有用。 现在，还可以以自助方式撤消凭据。

## 维护发行说明 {#maintenance}

您可以找到最新的维护发行说明 [此处](/help/release-notes/maintenance/latest.md).

## Cloud Manager {#cloud-manager}

您可以在[此处](/help/implementing/cloud-manager/release-notes-cloud-manager/release-notes-cm-current.md)找到 Cloud Manager 每月发布的完整列表。

## 迁移工具 {#migration-tools}

您可以在[此处](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)找到迁移工具版本的完整列表。
