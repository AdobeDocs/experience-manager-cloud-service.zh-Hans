---
title: ' [!DNL Adobe Experience Manager Assets] 中作为a [!DNL Cloud Service]的显着更改'
description: 与[!DNL Adobe Experience Manager 6.5相比，对 [!DNL Adobe Experience Manager Assets] in [!DNL Experience Manager] as a [!DNL Cloud Service] 的显着更改。
feature: 发行信息
role: Business Practitioner,Leader,Architect,Administrator
exl-id: 93e7dbcd-016e-4ef2-a1cd-c554efb5ad34
source-git-commit: e3efbaf5cb590b079ccc228a0f130ecec198d2ff
workflow-type: tm+mt
source-wordcount: '858'
ht-degree: 5%

---

# 对[!DNL Experience Manager Assets]作为[!DNL Cloud Service]的显着更改 {#notable-changes}

[!DNL Adobe Experience Manager] as a为管 [!DNL Cloud Service] 理Experience Manager项目提供了许多新功能和可能性。与[!DNL Experience Manager]作为[!DNL Cloud Service]的相比，[!DNL Experience Manager Assets]本地或作为Adobe托管服务的之间存在许多差异。 本文重点介绍了[!DNL Assets]功能的重要差异。

与[Experience Manager] 6.5相比，主要区别在以下方面：

* [资产摄取、上传和处理](#asset-ingestion)。
* [用于云原生处理的资产微服务](#asset-microservices)。
* [删除了经典 UI](#classic-ui).

## 资产摄取、处理和分发 {#asset-ingestion-distribution}

资产上传通过实现更好的摄取扩展、更快的上传、使用微服务加快处理以及批量摄取，从而优化了效率。 产品功能（Web用户界面、桌面客户端）已更新。 此外，这可能会影响一些现有的自定义设置。

* [!DNL Experience Manager] 使用直接二进制访问原则上传和下载资产，并使用资产微服务处理资产。请参阅[微服务概述](/help/assets/asset-microservices-overview.md)。
   * 资产上传[，并直接访问二进制文件](/help/assets/asset-microservices-overview.md#asset-upload-with-direct-binary-access)。
   * 有关技术详细信息，请参阅[直接二进制上传协议和API](/help/assets/developer-reference-material-apis.md#upload-binary)。
   * 有关基本CRUD操作的可用API方法的比较，请参阅[API和资产操作](/help/assets/developer-reference-material-apis.md#use-cases-and-apis)。
*  早期版本中的默认工作流程 **[!UICONTROL DAM 资产更新]**&#x200B;不再可用。[!DNL Experience Manager]相反，资产微服务提供了可扩展且随时可用的服务，该服务涵盖大多数默认资产处理（演绎版、元数据提取和用于索引的文本提取）。
   * 请参阅[配置和使用资产微服务](/help/assets/asset-microservices-configure-and-use.md)
   * 要在处理过程中执行自定义的工作流步骤，可以使用[后处理工作流](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows)。

* 无需任何转换即可交付二进制文件的网站组件可以使用直接下载。 SlingGETServlet已更新，允许开发人员默认执行此操作。 通过某些转换交付二进制文件的网站组件（例如，通过Servlet调整其大小）可以继续按原样运行。

使用资产微服务生成的标准演绎版，使用相同的命名约定在资产存储库节点中以向后兼容的方式存储。

## 开发和测试资产微服务 {#asset-microservices}

资产微服务使用云服务提供资产的可扩展且可复原的处理。 Adobe可管理云服务，以优化处理不同资产类型和处理选项。 资产微服务有助于避免使用第三方渲染工具和方法（如ImageMagick）并简化配置，同时为常见文件类型提供现成功能。 现在，您可以处理广泛的文件类型[](/help/assets/file-format-support.md)，这些文件类型的开箱即用格式比以前版本的Experience Manager所能处理的格式多。 例如，现在可以提取PSD和PSB格式的缩略图，而以前需要的第三方解决方案（如ImageMagick）就可以了。 不能将ImageMagick的复杂配置用于[!UICONTROL 处理配置文件]配置。 使用[!DNL Dynamic Media]进行高级FFmpeg视频转码，并使用处理配置文件进行MP4视频的[基本转码](/help/assets/manage-video-assets.md#transcode-video)。

资产微服务是一种云原生服务，在Cloud Manager中管理的客户程序和环境中自动进行配置并连接到[!DNL Experience Manager]。 要扩展或自定义[!DNL Experience Manager]，开发人员可以使用现有内容或资产以及在云环境中生成的演绎版，以使用、显示、下载资产来测试和验证其代码。

要对代码和流程（包括资产摄取和处理）进行端到端验证，请使用[管道](/help/implementing/cloud-manager/configure-pipeline.md)将代码更改部署到云开发环境，并通过完全执行资产微服务处理进行测试。

## 与[!DNL Experience Manager] 6.5的功能对等性 {#cloud-service-feature-status}

[!DNL Experience Manager] as a为现 [!DNL Cloud Service] 有功能引入了许多新功能和更高性能的工作方式。但是，当从[!DNL Experience Manager] 6.5作为[!DNL Cloud Service]从[!DNL Experience Manager]移动到时，您可能会注意到某些功能的工作方式不同、不可用或部分可用。 以下是此类功能的列表。 此外，请参阅[已弃用和已删除的功能](/help/release-notes/deprecated-removed-features.md)。

| 功能或用例 | [!DNL Experience Manager]中的[!DNL Cloud Service]状态 | 评论 |
|-----|-----|-----|
| [重复的资产检测](/help/assets/manage-digital-assets.md#detect-duplicate-assets) | 工作方式不同。 | 请参阅[它在 [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/duplicate-detection.html)中的工作方式。 |
| [仅用于放置(FPO)演绎版](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/configure-aem-assets-for-asset-link.ug.html#configfporendition) | 工作方式不同 |  |
| 元数据写回 | 工作方式不同 | 默认为已禁用. 根据需要启用相应的工作流启动器。 写回由资产微服务处理。 |
| 使用包管理器处理上传的资产 | 需要人工干预。 | 使用&#x200B;**[!UICONTROL 重新处理资产]**&#x200B;操作手动重新处理。 |
| MIME类型检测 | 不受支持. | 如果您上传的数字资产没有扩展或扩展名不正确，则可能无法按需要进行处理。 用户仍可以在DAM中存储没有扩展名的二进制文件。 请参阅 [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/detect-asset-mime-type-with-tika.html)中的[MIME类型检测。 |
| 复合资产的子资产生成或注释 | 不受支持. | 未满足相关用例。 例如，无法查看或注释多页PDF、INDD、PPT、PPTX和AI文件。 请参阅 [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/managing-linked-subassets.html#generate-subassets)中的[子资产创建。 |
| 主页 | 不受支持. | 请参阅[[!DNL Assets] Home Page experience in [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/assets-home-page.html) |
| 从ZIP存档提取资产 | 不受支持. | 请参阅 [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/manage-assets.html#extractzip)中的[ZIP提取。 |
| 资产评级 | 不受支持. | 不支持元数据架构编辑器中的评级小组件。 |
| 经典 UI | 不受支持. | 只有启用了触屏的用户界面才可用。 |

>[!MORELIKETHIS]
>
>以下资源可用于[!DNL Experience Manager]作为[!DNL Cloud Service]:
>
>* [已弃用和已删除功能的列表](/help/release-notes/deprecated-removed-features.md)
* [简介](/help/overview/introduction.md)
* [新增功能和不同功能](/help/overview/what-is-new-and-different.md)
* [架构](/help/core-concepts/architecture.md)
* [显着更改](/help/release-notes/aem-cloud-changes.md)
* [显着更改 [!DNL Sites]](/help/sites-cloud/sites-cloud-changes.md)
* [视频教程](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/overview.html)

