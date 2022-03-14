---
title: 中的显着更改 [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service]
description: 对 [!DNL Adobe Experience Manager Assets] in [!DNL Experience Manager] as a [!DNL Cloud Service] 与 [!DNL Adobe Experience Manager] 6.5。
feature: Release Information
role: User,Leader,Architect,Admin
exl-id: 93e7dbcd-016e-4ef2-a1cd-c554efb5ad34
source-git-commit: fe662a515a52bcf4648585366422064edce1a7fd
workflow-type: tm+mt
source-wordcount: '1032'
ht-degree: 6%

---

# 对 [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#notable-changes}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 为管理Experience Manager项目提供了许多新功能和可能性。 两者之间有许多差异 [!DNL Experience Manager Assets] 与 [!DNL Experience Manager] as a [!DNL Cloud Service]. 本文重点介绍了 [!DNL Assets] 功能。

与 [!DNL Experience Manager] 6.5在以下方面：

* [资产摄取、上传和处理](#asset-ingestion).
* [用于云原生处理的资产微服务](#asset-microservices).
* [删除了经典 UI](#classic-ui).

## 资产摄取、处理和分发 {#asset-ingestion-distribution}

资产上传通过实现更好的摄取扩展、更快的上传、使用微服务加快处理以及批量摄取，从而优化了效率。 产品功能（Web用户界面、桌面客户端）已更新。 此外，这可能会影响一些现有的自定义设置。

* [!DNL Experience Manager] 使用直接二进制访问原则上传和下载资产，并使用资产微服务处理资产。 请参阅 [微服务概述](/help/assets/asset-microservices-overview.md).
   * 资产上传 [直接二进制访问](/help/assets/asset-microservices-overview.md#asset-upload-with-direct-binary-access).
   * 有关技术详细信息，请参阅 [直接二进制上传协议和API](/help/assets/developer-reference-material-apis.md#upload-binary).
   * 有关基本CRUD操作的可用API方法的比较，请参阅 [API和资产操作](/help/assets/developer-reference-material-apis.md#use-cases-and-apis).
*  早期版本中的默认工作流程 **[!UICONTROL DAM 资产更新]**&#x200B;不再可用。[!DNL Experience Manager]相反，资产微服务提供了可扩展且随时可用的服务，该服务涵盖大多数默认资产处理（演绎版、元数据提取和用于索引的文本提取）。
   * 请参阅 [配置和使用资产微服务](/help/assets/asset-microservices-configure-and-use.md)
   * 要在处理中自定义工作流步骤，请 [后处理工作流](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows) 中。

* 无需任何转换即可交付二进制文件的网站组件可以使用直接下载。 SlingGETServlet已更新，允许开发人员默认执行此操作。 通过某些转换交付二进制文件的网站组件（例如，通过Servlet调整其大小）可以继续按原样运行。

使用资产微服务生成的标准演绎版，使用相同的命名约定在资产存储库节点中以向后兼容的方式存储。

## 开发和测试资产微服务 {#asset-microservices}

资产微服务使用云服务提供资产的可扩展且可复原的处理。 Adobe可管理云服务，以优化处理不同资产类型和处理选项。 资产微服务有助于避免需要第三方渲染工具和方法(例如 [!DNL ImageMagick])并简化配置，同时为常见文件类型提供现成功能。 您现在可以处理 [广泛的文件类型](/help/assets/file-format-support.md) 可开箱即用地涵盖的格式多于以前版本的Experience Manager。 例如，现在可以提取PSD和PSB格式的缩略图，这是之前需要的第三方解决方案，例如 [!DNL ImageMagick]. 不能使用 [!DNL ImageMagick] 对于 [!UICONTROL 处理配置文件] 配置。 使用 [!DNL Dynamic Media] 用于高级FFmpeg视频转码，以及将处理配置文件用于 [MP4视频基本转码](/help/assets/manage-video-assets.md#transcode-video).

资产微服务是一种云原生服务，可自动进行配置并连接到 [!DNL Experience Manager] 在Cloud Manager中管理的客户程序和环境中。 扩展或自定义 [!DNL Experience Manager]，开发人员可以使用现有内容或资产以及在云环境中生成的演绎版，来使用、显示、下载资产来测试和验证其代码。

要对代码和流程（包括资产摄取和处理）进行端到端验证，请使用 [管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) 并全面执行资产微服务处理进行测试。

## 与的功能对等性 [!DNL Experience Manager] 6.5 {#cloud-service-feature-status}

[!DNL Experience Manager] as a [!DNL Cloud Service] 为现有功能引入了许多新功能和性能更高的使用方式。 但是，当从 [!DNL Experience Manager] 6.5至 [!DNL Experience Manager] as a [!DNL Cloud Service]，您可能会注意到某些功能的工作方式不同、不可用或部分可用。 以下是此类功能的列表。 此外，请参阅 [已弃用和已删除的功能](/help/release-notes/deprecated-removed-features.md).

| 功能或用例 | 状态 [!DNL Experience Manager] as a [!DNL Cloud Service] | 批注 |
|-----|-----|-----|
| [重复的资产检测](/help/assets/manage-digital-assets.md#detect-duplicate-assets) | 工作方式不同 | 请参阅 [工作原理 [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/duplicate-detection.html). |
| [仅用于放置(FPO)演绎版](/help/assets/configure-fpo-renditions.md) | 工作方式不同 | 处理配置文件使用资产微服务生成FPO演绎版。 在Experience Manager6.5中，第三方解决方案，例如 [!DNL ImageMagick] 可用于生成演绎版。 |
| 元数据写回 | 工作方式不同 | 默认为已禁用. 根据需要启用相应的工作流启动器。 写回由资产微服务处理。 |
| 使用包管理器处理上传的资产 | 需要手动干预 | 使用手动重新处理 **[!UICONTROL 重新处理资产]** 操作。 |
| MIME类型检测 | 不受支持. | 如果您上传的数字资产没有扩展或扩展名不正确，则可能无法按需要进行处理。 用户仍可以在DAM中存储没有扩展名的二进制文件。 请参阅 [中的MIME类型检测 [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/detect-asset-mime-type-with-tika.html). |
| 复合资产的子资产生成 | 不受支持. | 可能无法满足注释等相关用例。 请参阅 [子资产创建 [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/managing-linked-subassets.html#generate-subassets). PDF已开始预览某些文件类型 [2021.7.0版](/help/release-notes/release-notes-cloud/release-notes-current.md). |
| 编辑图像 | 不受支持 | Experience Manageras a Cloud Service不支持编辑资产。 请参阅 [在Experience Manager6.5中的工作原理](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/manage-assets.html#editing-images). |
| 主页 | 不受支持 | 请参阅 [[!DNL Assets] Home Page experience in [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/assets-home-page.html) |
| 从ZIP存档提取资产 | 不受支持 | 请参阅 [中的ZIP提取 [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/manage-assets.html#extractzip). |
| 资产评级 | 不受支持 | 不支持元数据架构编辑器中的评级小组件。 |
| 内容处置过滤器 | 不受支持 | 的常见用例 `ContentDispositionFilter` 是让管理员配置 [!DNL Experience Manager] 以提供HTML文件，并在内联中打开PDF文件，而不是下载这些文件。 在发布实例上，您可以使用Dispatcher配置管理处置。 在创作实例上，Adobe不建议修改内容处置标头。 请参阅 [中的内容处置过滤器 [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/content-disposition-filter.html). |
| [下载报表](/help/assets/asset-reports.md) | 不受支持 | 目前，无法使用通知资产使用的下载报表。 请参阅 [下载报表 [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/asset-reports.html). |
| 产品照片拍摄模板 | 不受支持 | 请参阅 [产品照片模板 [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/projects/managing-product-information.html). |
| 智能翻译 | 不受支持 | [智能翻译](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/translation/smart-translation-search-feature-video-use.html) 不支持 [!DNL Experience Manager] as a [!DNL Cloud Service]. |
| WebDAV | 不受支持 | 有关替代方案，请参阅 [[!DNL Creative Cloud] 集成](/help/assets/aem-cc-integration-best-practices.md) 或 [显影剂参考材料](/help/assets/developer-reference-material-apis.md). |
| 经典 UI | 不受支持 | 只有启用了触屏的用户界面才可用。 |

>[!MORELIKETHIS]
>
>以下资源可供使用 [!DNL Experience Manager] as a [!DNL Cloud Service]:
>
>* [已弃用和已删除功能的列表](/help/release-notes/deprecated-removed-features.md)
>* [简介](/help/overview/introduction.md)
>* [新增功能和不同功能](/help/overview/what-is-new-and-different.md)
>* [架构](/help/overview/architecture.md)
>* [重要更改](/help/release-notes/aem-cloud-changes.md)
>* [重要更改 [!DNL Sites]](/help/sites-cloud/sites-cloud-changes.md)
>* [视频教程](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/overview.html?lang=zh-Hans)

