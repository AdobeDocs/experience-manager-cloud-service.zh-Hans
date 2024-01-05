---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 2023.1.0 版的发行说明。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 2023.1.0 版的发行说明。'
exl-id: f134fdbc-224b-404c-b20f-44cae8bad681
source-git-commit: a77e5dc4273736b969e9a4a62fcac75664495ee6
workflow-type: tm+mt
source-wordcount: '975'
ht-degree: 100%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 2023.1.0 版的发行说明 {#release-notes}

以下部分概述了 2023.1.0 版的 [!DNL Experience Manager] as a Cloud Service 的功能发行说明。

>[!NOTE]
>
>您可以在此部分中导航到早期版本的发行说明；例如，2021 版、2022 版等的发行说明。
>
>查看 [Experience Manager 版本发行路线图](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html)，了解即将推出的 [!DNL Experience Manager] as a Cloud Service 的功能激活。

>[!NOTE]
>
>有关未与版本直接相关的文档更新的详细信息，请参阅[最新文档更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html)。

## 发布日期 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 2023.1.0 功能版本的发布日期为 2023 年 2 月 9 日。下一个功能版本 (2023.2.0) 计划于 2023 年 4 月 12 日发布。

## 发布视频 {#release-video}

观看 2023 年 1 月版概述视频，大致了解 2023.1.0 版的新增功能：

>[!VIDEO](https://video.tv.adobe.com/v/3413479/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### [!DNL Sites] 预发行版本中的新增功能 {#prerelease-features-sites}

* AEM GraphQL 内容交付 API 现在支持 GraphQL[分页](/help/headless/graphql-api/content-fragments.md#paging)和[排序](/help/headless/graphql-api/content-fragments.md#sorting)，提高了获取和呈现大型内容集的效率。利用 GraphQL 分页，可以通过按子集返回结果（而不是一次性返回所有结果）来缩短查询响应时间。利用 GraphQL 排序，可以按所需顺序放置内容集，从而使客户端应用程序能够更轻松地处理内容。AEM GraphQL 引擎中的混合筛选进一步缩短了查询响应时间。现在以与查询筛选器对应的较小集的形式从 JCR 中读取内容。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets] 中的新增功能 {#assets-features}

* 现在利用资产报告，管理员可以从 Experience Manager Assets as a Cloud Service 部署中[生成资产下载报告](/help/assets/asset-reports.md)。此数据进一步支持管理员从关键成功量度获得见解，以便衡量在您的企业内和客户采用资产的情况。

  ![其他格式的 PDF 演绎版](/help/release-notes/assets/choose_report.png)

* 除了用于身份验证的访问密钥外，Experience Manager Assets 现在还[支持 SAS 令牌](/help/assets/add-assets.md#asset-bulk-ingestor)，同时还连接到 Azure Blob 存储数据源，从而使用“批量导入”工具摄取资产。

* 改进了 Asset Compute 中的 CMYK 图像管理，使您能够为 CMYK 图像生成智能裁切和智能标记。

### [!DNL Assets] 预发行版本中的新增功能 {#prerelease-features-assets}

* Experience Manager Assets 现在支持使用“批量导入”工具[从 Google Cloud Platform 大规模摄取资产](/help/assets/add-assets.md#asset-bulk-ingestor)。

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] 中的新增功能 {#new-features-available-in-channel}

* **[生成非交互式 PDF 文档和可打印输出的工作流步骤](/help/forms/aem-forms-workflow-step-reference.md)**：使用 AEM 工作流步骤自动为业务流程创建非交互式 PDF 文档和可打印输出，从而简化文档生成过程并节省时间。
* **[在自适应表单中使用脚注来提供引文或额外信息](/help/forms/footnotes-richtextsupport.md)**：在自适应表单中使用脚注来显示有关如何完成或使用表单的信息。您还可以使用它提供附加信息、版权许可和其他有用信息。

### [!DNL Forms] 预发行版本中的新增功能 {#prerelease-features-forms}

* **[使用数据捕获核心组件以构建自适应表单](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)**:[使用自适应表单编辑器](/help/forms/creating-adaptive-form-core-components.md)创建基于标准化数据捕获组件（核心组件）的表单。对于您的数字注册体验，这些组件可以提供定制功能，缩短开发时间和降低维护成本。
* **[对设置基于核心组件的自适应表单样式的前端管道支持](/help/forms/using-themes-in-core-components.md)**：为基于核心组件的自适应表单使用易于定制的基于 BEM 的主题，方式是使用前端部署管道来部署它们以改进表单外观。
* **[为基于核心组件的自适应表单生成记录文档](/help/forms/generate-document-of-record-core-components.md)**：在提交时为基于核心组件的自适应表单创建记录以进行长期存档（采用打印或文档格式）。

![https://www.aemcomponents.dev/](/help/forms/assets/sample-core-components-based-adaptive-form.png)

* **[将自适应表单提交到 Microsoft SharePoint 和 Microsoft OneDrive](/help/forms/configuring-submit-actions.md)**：利用将自适应表单数据直接发送到 Microsoft SharePoint 和 Microsoft OneDrive 的功能，简化数据提交。您可以提交基于架构的数据和无架构的数据。这些提交操作是对现有可用提交操作的补充。
* **[使用“将自适应表单另存为模板”功能进行高效的表单构建](/help/forms/template-editor.md#save-an-adaptive-form-as-template-saving-adaptive-form-as-template)**：通过将自适应表单另存为模板并将此模板重用于下一个自适应表单来简化表单构建过程。
* **[将 AEM Forms 连接到 JDBC 支持的数据库](/help/forms/configure-data-sources.md#configure-relational-database-configure-relational-database)**：轻松将 AEM Forms 数据模型连接到支持 JDBC 的数据库，从而无缝读取和写入数据。
* **[使用 Open API 3.0 与 REST 端点集成](/help/forms/configure-data-sources.md#configure-restful-services-open-api-specification-version-20-configure-restful-services-swagger-version30)**：将 AEM Forms as a Cloud Service 表单数据模型连接到支持 Open API 规范版本 3.0 的 REST 端点，从而轻松发送和接收数据。
* **[共享自适应表单以进行审阅](/help/forms/create-reviews-forms.md)**：使用自适应表单审阅机制，可允许一个或多个审阅者审阅表单。

## [!DNL Experience Manager as a Cloud Service] Foundation {#foundation}

### 新增功能 {#what-is-new-foundation}

* [快速开发环境](/help/implementing/developing/introduction/rapid-development-environments.md) - RDE 使开发人员能够快速解决问题并在 AEM as a Cloud Service 上部署新功能。

  快速开发环境是一种新型云环境，旨在提供快速、一致且可扩展的方式以验证在本地正常工作的代码在云中也可发挥预期的作用。可使用命令行工具快速地将包、捆绑、内容文件、OSGI 配置或 Dispatcher 配置同步到 RDE。观看以下视频，了解实际操作：

  >[!VIDEO](https://video.tv.adobe.com/v/3413508/?quality=12&learn=on)

  在 RDE 中成功验证代码后，鼓励部署到云开发环境以执行 Cloud Manager 质量门，然后再通过生产管道部署到暂存环境和生产环境。

  每个程序均包含一个 RDE，并且可以选择许可更多 RDE。

  >[!NOTE]
  >
  >在接下来的几周内，将逐步推出 RDE；您可以将电子邮件发送到 aemcs-rde-support@adobe.com 来排在队伍前面。

* [对服务器端 API 访问令牌的扩展支持](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md) - 您现在可以生成多个凭据，这在 API 具有不同特征的场景中很有用。现在还可以通过自助服务方式来撤销凭据。

## 维护发行说明 {#maintenance}

您可以在[此处](/help/release-notes/maintenance/latest.md)找到最新的维护发行说明。

## Cloud Manager {#cloud-manager}

您可以在[此处](/help/implementing/cloud-manager/release-notes/current.md)找到 Cloud Manager 每月发布的完整列表。

## 迁移工具 {#migration-tools}

您可以在[此处](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)找到迁移工具版本的完整列表。
