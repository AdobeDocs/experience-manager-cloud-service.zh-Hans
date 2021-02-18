---
title: ' [!DNL Adobe Experience Manager Assets] 作为 [!DNL Cloud Service]的显着变化'
description: 与[!DNL Adobe Experience Manager 6.5相比， [!DNL Adobe Experience Manager Assets] in [!DNL Experience Manager] as a [!DNL Cloud Service] 有显着变化。
translation-type: tm+mt
source-git-commit: 6dc6445e4019664525629fe2204d255cfee37a81
workflow-type: tm+mt
source-wordcount: '743'
ht-degree: 4%

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
* 不支持元数据写回。 请参阅 [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/xmp-writeback.html)中的[元数据写回。
* 使用包管理器上传的资产需要使用[!DNL Assets]用户界面中的&#x200B;**[!UICONTROL 重新处理资产]**&#x200B;操作手动进行重新处理。
* [!DNL Assets] 不会自动检测已上传资产的MIME类型。没有扩展或扩展不正确的数字资产不会根据需要进行处理。 例如，上传此类资产时，资产可能不会发生任何情况或应用不正确的处理用户档案。 用户仍可以存储二进制文件，而无需在DAM中扩展名。 请参阅 [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/detect-asset-mime-type-with-tika.html)中的[MIME类型检测。
* [!DNL Experience Manager] as不 [!DNL Cloud Service] 会为复合资产生成子资产。请参阅 [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/managing-linked-subassets.html#generate-subassets)中的[子资产创建。
* [!DNL Assets] 主页体验不可用。请参见[[!DNL Assets] Home Page experience in [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/assets-home-page.html)。
* 重复资产检测与[在 [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/duplicate-detection.html)中的工作方式不同。
* 与早期的[!DNL Experience Manager]版本相比，仅用于放置(FPO)再现的生成方式有所不同。 请参阅 [!DNL Experience Manager] 的[FPO再现作为 [!DNL Cloud Service]](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/configure-aem-assets-for-asset-link.ug.html)。
* 上传ZIP存档时，作为[!DNL Cloud Service]的[!DNL Experience Manager]不会提取该存档中绑定的资产。 请参阅 [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/manage-assets.htmln#extractzip)中的[ZIP提取。

使用资产微服务生成的标准演绎版使用相同的命名约定以向后兼容的方式存储在资产存储库节点中。

## 开发和测试资产微服务{#asset-microservices}

资产微服务使用云服务提供资产的可扩展且具有弹性的处理。 Adobe管理云服务，以优化处理不同资产类型和处理选项。 Asset microservices有助于避免使用第三方渲染工具和方法（如ImageMagick）并简化配置，同时为常见文件类型提供现成功能。 现在，您可以处理[范围广泛的文件类型](/help/assets/file-format-support.md)，这些文件类型的开箱即用格式比以前版本的Experience Manager可能的格式要多。 例如，PSD和PSB格式的缩览图提取现在可能是之前需要的第三方解决方案，如ImageMagick。 不能将ImageMagick的复杂配置用于[!UICONTROL 处理用户档案]配置。 使用[!DNL Dynamic Media]对视频进行高级FFmpeg转码，并使用处理用户档案对MP4视频](/help/assets/manage-video-assets.md#transcode-video)进行基本转码。[

Asset microservices是一种云本机服务，可自动配置并连接到Cloud Manager中管理的客户项目和环境中的[!DNL Experience Manager]。 为了扩展或自定义[!DNL Experience Manager]，开发人员可以将现有内容或资产与在云环境中生成的演绎版一起使用，以测试和验证其代码，使用、显示、下载资产。

要对代码和流程（包括资产摄取和处理）进行端对端验证，请使用[管道](/help/implementing/cloud-manager/configure-pipeline.md)将代码更改部署到云开发环境，并在资产微服务处理完全执行时进行测试。

## 删除了经典 UI {#classic-ui}

经典UI在[!DNL Experience Manager]中不再作为[!DNL Cloud Service]可用。 只有触屏优化UI才可用。

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

