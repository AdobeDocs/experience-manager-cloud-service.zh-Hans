---
title: 中的显着更改 [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service]
description: 对的重要更改 [!DNL Adobe Experience Manager Assets] 在 [!DNL Experience Manager] as a [!DNL Cloud Service] 与 [!DNL Adobe Experience Manager] 6.5.
feature: Release Information
role: User,Leader,Architect,Admin
exl-id: 93e7dbcd-016e-4ef2-a1cd-c554efb5ad34
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '1034'
ht-degree: 11%

---

# 对的重要更改 [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#notable-changes}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 提供了许多管理Experience Manager项目的新功能和可能性。 两者之间有许多差异 [!DNL Experience Manager Assets] 内部部署或作为Adobe托管服务托管，而非 [!DNL Experience Manager] as a [!DNL Cloud Service]. 本文重点介绍了以下各项的重要差异 [!DNL Assets] 功能。

与以下各项的主要区别 [!DNL Experience Manager] 6.5包括以下方面：

* [资产摄取、上传和处理](#asset-ingestion).
* [用于云原生处理的资产微服务](#asset-microservices).
* [删除了经典 UI](#classic-ui).

## 资产提取、处理和分发 {#asset-ingestion-distribution}

通过更好地扩展摄取、更快上传、使用微服务更快处理和批量摄取，资产上传已针对效率进行了优化。 产品功能（Web用户界面、桌面客户端）已更新。 此外，这可能会影响一些现有的自定义设置。

* [!DNL Experience Manager] 使用直接二进制访问原则上传和下载资产，并使用资产微服务处理资产。 参见 [微服务概述](/help/assets/asset-microservices-overview.md).
   * 资产上传 [通过直接二进制访问](/help/assets/asset-microservices-overview.md#asset-upload-with-direct-binary-access).
   * 有关技术详细信息，请参阅 [直接二进制上传协议和API](/help/assets/developer-reference-material-apis.md#upload-binary).
   * 有关基本CRUD操作的可用API方法的比较，请参阅 [API和资产操作](/help/assets/developer-reference-material-apis.md#use-cases-and-apis).
*  早期版本中的默认工作流程 **[!UICONTROL DAM 资产更新]**&#x200B;不再可用。[!DNL Experience Manager]相反，资产微服务提供可扩展、现成的服务，涵盖大多数默认资产处理（演绎版、元数据提取和索引的文本提取）。
   * 参见 [配置和使用资源微服务](/help/assets/asset-microservices-configure-and-use.md)
   * 要在处理过程中自定义工作流步骤，请执行以下操作： [后处理工作流](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows) 可以使用。

* 在不进行任何转换的情况下交付二进制文件的网站组件可以使用直接下载。 SlingGETservlet已更新，默认情况下允许开发人员执行此操作。 在进行某些转换后交付二进制文件的网站组件（例如，通过servlet调整其大小）可以继续按原样操作。

通过资源微服务生成的标准演绎版使用相同的命名约定以向后兼容的方式存储在资源存储库节点中。

## 开发和测试资产微服务 {#asset-microservices}

资源微服务使用云服务来对资源进行可扩展的弹性处理。Adobe 管理云服务以实施对不同的资源类型和处理选项的最优处理。资产微服务有助于避免使用第三方渲染工具和方法(例如 [!DNL ImageMagick])并简化了配置，同时为常见文件类型提供了现成可用的功能。 您现在可以处理 [多种文件类型](/help/assets/file-format-support.md) 比以前版本的Experience Manager所具有的更多现成格式。 例如，现在可以提取PSD和PSB格式的缩略图，而之前需要第三方解决方案，例如 [!DNL ImageMagick]. 您不能使用的复杂配置 [!DNL ImageMagick] 对于 [!UICONTROL 处理配置文件] 配置。 使用 [!DNL Dynamic Media] 用于视频的高级FFmpeg转码，并使用处理配置文件 [MP4视频的基本转码](/help/assets/manage-video-assets.md#transcode-video).

资产微服务是一种云原生服务，可自动配置并连接到 [!DNL Experience Manager] 在Cloud Manager中管理的客户程序和环境中。 要扩展或自定义 [!DNL Experience Manager]，开发人员可以使用现有内容或资产以及在云环境中生成的演绎版，以使用、显示、下载资产来测试和验证其代码。

要对代码和流程（包括资产摄取和处理）进行端到端验证，请使用将代码更改部署到云开发环境 [管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) 和测试，以完全执行资产微服务处理。

## 功能等同于 [!DNL Experience Manager] 6.5 {#cloud-service-feature-status}

[!DNL Experience Manager] as a [!DNL Cloud Service] 引入了许多新功能和更多高性能方法来使现有功能正常工作。 但是，当从 [!DNL Experience Manager] 6.5至 [!DNL Experience Manager] as a [!DNL Cloud Service]中，您可能会注意到某些功能的工作方式不同、不可用或部分可用。 以下是此类功能的列表。 此外，请参见 [已弃用和已删除的功能](/help/release-notes/deprecated-removed-features.md).

| 功能或用例 | 中的状态 [!DNL Experience Manager] as a [!DNL Cloud Service] | 评论 |
|-----|-----|-----|
| [重复资产检测](/help/assets/manage-digital-assets.md#detect-duplicate-assets) | 工作方式不同 | 参见 [它如何在 [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/duplicate-detection.html). |
| [仅用于置入(FPO)演绎版](/help/assets/configure-fpo-renditions.md) | 工作方式不同 | 处理配置文件使用资产微服务生成FPO演绎版。 在Experience Manager6.5中，第三方解决方案，例如 [!DNL ImageMagick] 可用于生成演绎版。 |
| 元数据写回 | 工作方式不同 | 默认为已禁用. 如果需要，请启用相应的工作流启动器。 写回由资源微服务处理。 |
| 处理使用包管理器上传的资产 | 需要手动干预 | 使用手动重新处理 **[!UICONTROL 重新处理资产]** 操作。 |
| MIME类型检测 | 不受支持. | 如果您上传的数字资产没有扩展或扩展名不正确，则可能无法按需要处理该资产。 用户仍然可以在DAM中存储不带扩展名的二进制文件。 参见 [中的MIME类型检测 [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/detect-asset-mime-type-with-tika.html). |
| 复合资产的子资产生成 | 不受支持. | 可能无法实现批注等依赖用例。 参见 [子资产创建于 [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/managing-linked-subassets.html#generate-subassets). 某些文件类型的PDF预览从 [2021.7.0发行版](/help/release-notes/release-notes-cloud/release-notes-current.md). |
| 编辑图像 | 不受支持 | Experience Manageras a Cloud Service不支持编辑资源。 参见 [如何在Experience Manager6.5中工作](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/manage-assets.html#editing-images). |
| 主页 | 不受支持 | 参见 [[!DNL Assets] Home Page experience in [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/assets-home-page.html) |
| 从ZIP存档中提取资产 | 不受支持 | 参见 [中的压缩提取 [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/manage-assets.html#extractzip). |
| 资产评级 | 不受支持 | 不支持元数据架构编辑器中的评级小组件。 |
| 内容处置过滤器 | 不受支持 | 的常见用例 `ContentDispositionFilter` 是让管理员配置 [!DNL Experience Manager] 提供HTML文件，并内联打开PDF文件而不是下载这些文件。 在Publish实例上，您可以使用Dispatcher配置管理部署。 在“创作”实例上，Adobe不建议修改“内容处置”标头。 参见 [中的内容处置过滤器 [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/content-disposition-filter.html). |
| 产品照片拍摄模板 | 不受支持 | 参见 [中的产品照片拍摄模板 [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/projects/managing-product-information.html). |
| 智能翻译 | 不受支持 | [智能翻译](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/translation/smart-translation-search-feature-video-use.html) 不支持 [!DNL Experience Manager] as a [!DNL Cloud Service]. |
| WebDAV | 不受支持 | 有关备选方案，请参阅 [[!DNL Creative Cloud] 集成](/help/assets/aem-cc-integration-best-practices.md) 或 [开发人员参考资料](/help/assets/developer-reference-material-apis.md). |
| 经典 UI | 不受支持 | 仅触屏用户界面可用。 |

**另请参阅**

* [翻译资源](translate-assets.md)
* [Assets HTTP API](mac-api-assets.md)
* [资源支持的文件格式](file-format-support.md)
* [搜索资源](search-assets.md)
* [连接的资源](use-assets-across-connected-assets-instances.md)
* [资源报告](asset-reports.md)
* [元数据架构](metadata-schemas.md)
* [下载资源](download-assets-from-aem.md)
* [管理元数据](manage-metadata.md)
* [搜索 Facet](search-facets.md)
* [管理收藏集](manage-collections.md)
* [批量元数据导入](metadata-import-export.md)

>[!MORELIKETHIS]
>
>以下资源可用于 [!DNL Experience Manager] as a [!DNL Cloud Service]：
>
>* [已弃用和已删除的功能列表](/help/release-notes/deprecated-removed-features.md)
>* [简介](/help/overview/introduction.md)
>* [新增功能和不同功能](/help/overview/what-is-new-and-different.md)
>* [架构](/help/overview/architecture.md)
>* [重要更改](/help/release-notes/aem-cloud-changes.md)
>* [重要更改 [!DNL Sites]](/help/sites-cloud/sites-cloud-changes.md)
>* [视频教程](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/overview.html?lang=zh-Hans)

