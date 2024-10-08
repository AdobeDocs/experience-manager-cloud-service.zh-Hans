---
title: 用于Creative Cloud集成的Content Automation
description: 使用Creative Cloud集成生成资源变体
contentOwner: AG
feature: Upload, Asset Processing, Publishing, Asset Compute Microservices
role: User, Admin
exl-id: 4cff355e-d12c-44c7-b519-4cc37f49e396
source-git-commit: e3fd0fe2ee5bad2863812ede2a294dd63864f3e2
workflow-type: tm+mt
source-wordcount: '790'
ht-degree: 5%

---

# 使用[!DNL Adobe Creative Cloud]集成生成资源的变体 {#content-automation}

| [搜索最佳实践](/help/assets/search-best-practices.md) | [元数据最佳实践](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | 具有OpenAPI功能的[Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets开发人员文档](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

内容自动化加载项将[!DNL Adobe Experience Manager Assets]作为[!DNL Cloud Service]和[!DNL Adobe Creative Cloud] API集成在一起，以大规模地创造性地处理您的资产。 [!DNL Experience Manager]使用基于云的[资源微服务](/help/assets/asset-microservices-overview.md)来使用[!DNL Adobe Creative Cloud]功能并自动创建和处理资源。

若要编辑[!DNL Adobe Photoshop]和[!DNL Adobe Lightroom]中的资源，您不必从[!DNL Experience Manager Assets]下载资源，也可以编辑和再次上传这些资源。 您在[!DNL Experience Manager]中创建并配置处理配置文件，将该配置文件应用到文件夹，然后将资产上传到该文件夹。 系统会根据处理配置文件重新处理您上传的资产，并且您会获得这些资产的变体。 一致的轻松批量处理可节省手动操作并提高内容速度，而且无需一流的创意技能。 此外，开发人员和合作伙伴可以通过直接访问这些API来扩展资产微服务，并包含自定义逻辑。

用户可以创建处理配置文件，以对其资产自动执行以下创意操作：

* **自动色调**：使用人工智能分析图像的内容，并根据图像的独特属性智能地校正光和颜色。

* **自动直立**：使用人工智能分析图像的内容并更正图像中的倾斜透视。 例如，创建级别视野。

  ![自动色调](/help/assets/assets/content-automation-autotone.png)

  *图：自动色调和自动拉直可以帮助改善倾斜图像。*

* **Lightroom预设**：将用户定义的外观应用于图像，以使用自定义的预设获得一致的外观。

  ![Lightroom预设](/help/assets/assets/content-automation-lrpresets.png)

  *图：用于以一致的方式提高许多图像的图像质量的Adobe Lightroom预设。*

* **图像剪切**：使用人工智能在显着对象周围创建选区并通过单个命令删除背景。

  ![删除背景并从照片中剪切图像](/help/assets/assets/content-automation-backgroundremove.png)

* **图像蒙版**：使用人工智能通过单个命令在显着对象周围创建蒙版。

  ![使用AI蒙版图像](/help/assets/assets/content-automation-mask.png)

* **Photoshop操作**：将一系列[!DNL Adobe Photoshop]任务应用于一个文件或一批文件。

  ![Photoshop操作](/help/assets/assets/content-automation-psactions.png)

* **智能对象替换**：通过允许您交换图像，同时保留PSD文件中应用的所有效果和调整，可大规模进行个性化。

  ![智能替换对象](/help/assets/assets/content-automation-objectreplace.png)

## 为AEM as a Cloud Service项目启用Content Automation {#enable-content-automation}

要使用Cloud Manager为AEM as a Cloud Service项目启用Content Automation加载项，请执行以下操作：

1. 请联系您的客户代表以许可Content Automation加载项。
1. 访问Cloud Manager，然后使用组织选择器切换到您的组织。
1. 单击&#x200B;**[!UICONTROL 添加程序]**&#x200B;并指定程序名称。
1. 单击&#x200B;**[!UICONTROL 继续]**。
1. 展开&#x200B;**[!UICONTROL Assets]**&#x200B;并选择&#x200B;**[!UICONTROL 内容自动化]**。
1. 单击&#x200B;**[!UICONTROL 创建]**。
1. 运行管道以[将更改部署到Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html)。

如果您需要将Content Automation加载项添加到Cloud Manager中的现有AEM as a Cloud Service程序：

1. 单击项目信息卡上的……。

1. 选择&#x200B;**[!UICONTROL 编辑程序]**，然后选择&#x200B;**[!UICONTROL 解决方案和加载项]**&#x200B;选项卡。

1. 展开&#x200B;**[!UICONTROL Assets]**&#x200B;并选择&#x200B;**[!UICONTROL 内容自动化]**。
1. 单击&#x200B;**[!UICONTROL 更新]**。
1. 运行管道以[将更改部署到Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html)。

## 使用处理配置文件批量编辑您的创意资产 {#process-assets}

要使用处理配置文件自动创建变体，请执行以下步骤：

1. 导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 处理配置文件]**。

1. 选择&#x200B;**[!UICONTROL 创建]**，并指定&#x200B;**[!UICONTROL 名称]**。

1. 选择&#x200B;**[!UICONTROL 创意]**&#x200B;选项卡，指定输出文件夹，选择&#x200B;**[!UICONTROL 新增]**&#x200B;以添加创意配置。

1. 提供&#x200B;**[!UICONTROL 节目名称]**（或输出名称）、**[!UICONTROL 扩展名]**（或文件类型），选择&#x200B;**[!UICONTROL 质量]**（或输出参数），选择&#x200B;**[!UICONTROL 包含]**&#x200B;和&#x200B;**[!UICONTROL 排除]** MIME类型列表（或输入资源筛选器），然后选择所需的创作操作。

   [!UICONTROL 处理配置文件]](assets/creative-processing-profile.png)中的![[!UICONTROL 创意]选项卡

1. 某些操作需要额外的参数（资源）。 如有必要，请为这些额外的参数提供值。

1. 将更多创意操作添加为同一处理配置文件的一部分或保存配置文件。

1. 将处理配置文件应用到文件夹。 在文件夹的&#x200B;**[!UICONTROL 属性]**&#x200B;页面上，选择&#x200B;**[!UICONTROL 资产处理]**，然后选择要应用的处理配置文件。

将处理配置文件应用到DAM文件夹后，此文件夹中上传或更新的所有资产除了执行标准处理之外，还会执行定义的操作。 子文件夹会继承应用于父文件夹的相同配置文件。 用户可以覆盖此继承。

若要处理现有资源，请选择资源，选择&#x200B;**[!UICONTROL 重新处理]**&#x200B;选项，然后选择所需的处理配置文件。

## 提示和限制 {#limitations-best-practices}

* [!DNL Experience Manager]将资源处理限制为每个环境每分钟300个请求，每个组织每分钟700个请求。
* [!DNL Adobe Photoshop] API操作的文件大小限制为4 GB，[!DNL Adobe Lightroom]操作的文件大小限制为1 GB。

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
* [发布资源到 AEM 和 Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)

>[!MORELIKETHIS]
>
>* [通过处理配置文件来配置和使用资源微服务](/help/assets/asset-microservices-configure-and-use.md)。
>* [集成 [!DNL Experience Manager] 与 [!DNL Creative Cloud]](/help/assets/aem-cc-integration-best-practices.md)。
>* [使用资源微服务摄取和处理资源：概览](/help/assets/asset-microservices-overview.md)。
