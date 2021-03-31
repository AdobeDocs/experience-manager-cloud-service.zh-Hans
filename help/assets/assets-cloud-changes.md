---
title: ' [!DNL Adobe Experience Manager Assets] 作为 [!DNL Cloud Service]的显着变化'
description: 与[!DNL Adobe Experience Manager 6.5相比， [!DNL Adobe Experience Manager Assets] in [!DNL Experience Manager] as a [!DNL Cloud Service] 有显着变化。
feature: 发行信息
role: 业务从业者，领导者，架构师，管理员
translation-type: tm+mt
source-git-commit: 6fa911f39d707687e453de270bc0f3ece208d380
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 6%

---


# 对[!DNL Experience Manager Assets]作为[!DNL Cloud Service] {#notable-changes}的显着更改

[!DNL Adobe Experience Manager] 这为管 [!DNL Cloud Service] 理您的Experience Manager项目带来了许多新功能和可能性。与作为[!DNL Cloud Service]的[!DNL Experience Manager]相比，[!DNL Experience Manager Assets]内部部署或作为Adobe托管服务托管存在许多差异。 本文重点介绍了[!DNL Assets]功能的重要差异。

与[Experience Manager] 6.5相比，主要区别在以下方面：

* [资产摄取、上传和处理](#asset-ingestion)。
* [用于云本机处理的资产微服务](#asset-microservices)。
* [删除了经典 UI](#classic-ui).

## 资产摄取和处理{#asset-ingestion}

通过支持更好的摄取缩放、更快的上载、使用微服务更快的处理和批量摄取，资源上传已经过优化，从而提高效率。 产品功能（Web用户界面、桌面客户端）已更新。 此外，这可能会影响一些现有自定义设置。

* [!DNL Experience Manager] 使用直接二进制访问原则上传和下载资产，使用资产microservices处理资产。请参见microservices的[概述](/help/assets/asset-microservices-overview.md)。
   * 资产上传[，直接二进制访问](/help/assets/asset-microservices-overview.md#asset-upload-with-direct-binary-access)。
   * 有关技术详细信息，请参阅[直接二进制上载协议和API](/help/assets/developer-reference-material-apis.md#upload-binary)。
   * 有关基本CRUD操作的可用API方法的比较，请参阅[API和资产操作](/help/assets/developer-reference-material-apis.md#use-cases-and-apis)。
*  早期版本中的默认工作流程 **[!UICONTROL DAM 资产更新]**&#x200B;不再可用。[!DNL Experience Manager]相反，资产微服务提供了可扩展、随时可用的服务，涵盖大多数默认资产处理(演绎版、元数据提取和用于索引的文本提取)。
   * 请参阅[配置和使用资产microservices](/help/assets/asset-microservices-configure-and-use.md)
   * 要在处理过程中具有自定义的工作流步骤，可以使用[后处理工作流](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows)。

使用资产微服务生成的标准演绎版使用相同的命名约定以向后兼容的方式存储在资产存储库节点中。

## 开发和测试资产微服务{#asset-microservices}

资产微服务使用云服务提供资产的可扩展且具有弹性的处理。 Adobe管理云服务，以优化处理不同资产类型和处理选项。 Asset microservices有助于避免使用第三方渲染工具和方法（如ImageMagick）并简化配置，同时为常见文件类型提供现成功能。 现在，您可以处理[范围广泛的文件类型](/help/assets/file-format-support.md)，这些文件类型的开箱即用格式比以前版本的Experience Manager可能的格式要多。 例如，PSD和PSB格式的缩览图提取现在可能是之前需要的第三方解决方案，如ImageMagick。 不能将ImageMagick的复杂配置用于[!UICONTROL 处理用户档案]配置。 使用[!DNL Dynamic Media]对视频进行高级FFmpeg转码，并使用处理用户档案对MP4视频](/help/assets/manage-video-assets.md#transcode-video)进行基本转码。[

Asset microservices是一种云本机服务，可自动配置并连接到Cloud Manager中管理的客户项目和环境中的[!DNL Experience Manager]。 为了扩展或自定义[!DNL Experience Manager]，开发人员可以将现有内容或资产与在云环境中生成的演绎版一起使用，以测试和验证其代码，使用、显示、下载资产。

要对代码和流程（包括资产摄取和处理）进行端对端验证，请使用[管道](/help/implementing/cloud-manager/configure-pipeline.md)将代码更改部署到云开发环境，并在资产微服务处理完全执行时进行测试。


## 与[!DNL Experience Manager] 6.5 {#cloud-service-feature-status}的功能奇偶校验

[!DNL Experience Manager] 为现 [!DNL Cloud Service] 有功能引入了许多新功能和更高性能的工作方式。但是，当从[!DNL Experience Manager] 6.5移动到[!DNL Experience Manager]作为[!DNL Cloud Service]时，您可能会注意到某些功能的工作方式不同、不可用或部分可用。 以下是这些功能的列表:

| 功能或用例 | [!DNL Experience Manager]中的状态为[!DNL Cloud Service] | 评论 |
|-----|-----|-----|
| [重复资产检测](/help/assets/manage-digital-assets.md#detect-duplicate-assets) | 工作方式不同。 | 请参见[它在 [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/duplicate-detection.html)中的工作方式。 |
| [仅用于放置(FPO)再现](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/configure-aem-assets-for-asset-link.ug.html#configfporendition) | 工作方式不同 |  |
| 元数据写回 | 不受支持. | 请参阅 [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/xmp-writeback.html)中的[元数据写回 |
| 处理使用包管理器上传的资产 | 需要手动干预。 | 使用&#x200B;**[!UICONTROL 重新处理资产]**&#x200B;操作手动重新处理。 |
| MIME类型检测 | 不受支持. | 如果您上传的数字资产没有扩展名或扩展名不正确，可能无法按需要进行处理。 用户仍可以存储二进制文件，而无需在DAM中扩展名。 请参阅 [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/detect-asset-mime-type-with-tika.html)中的[MIME类型检测。 |
| 复合资产的子资产生成 | 不受支持. | 未完成从属使用案例。 例如，多页PDF文件的批注会受到影响。 请参阅 [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/managing-linked-subassets.html#generate-subassets)中的[子资产创建。 |
| 主页 | 不受支持. | 请参阅[[!DNL Assets] Home Page experience in [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/assets-home-page.html) |
| 从ZIP存档提取资源 | 不受支持. | 请参阅 [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/manage-assets.html#extractzip)中的[ZIP提取。 |
| 经典 UI | 不受支持. | 只有触屏优化UI才可用。 |

>[!MORELIKETHIS]
>
>[!DNL Experience Manager]为[!DNL Cloud Service]提供了以下资源：
>
>* [简介](/help/overview/introduction.md)
>* [新增功能和不同功能](/help/overview/what-is-new-and-different.md)
>* [架构](/help/core-concepts/architecture.md)
>* [显着变化](/help/release-notes/aem-cloud-changes.md)
>* [显着变化 [!DNL Sites]](/help/sites-cloud/sites-cloud-changes.md)
>* [视频教程](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/overview.html)

