---
title: 用于Creative Cloud集成的Content Automation
description: 使用Creative Cloud集成生成资源变体
contentOwner: AG
feature: Upload,Asset Processing,Publishing,Asset Compute Microservices,Workflow
role: User,Admin
exl-id: 4cff355e-d12c-44c7-b519-4cc37f49e396
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '777'
ht-degree: 4%

---

# 使用以下方式生成资源的变体 [!DNL Adobe Creative Cloud] 集成 {#content-automation}

内容自动化加载项集成了 [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] 和 [!DNL Adobe Creative Cloud] 用于大规模创造性处理您的资产的API。 [!DNL Experience Manager] 使用基于云的 [资源微服务](/help/assets/asset-microservices-overview.md) 以使用 [!DNL Adobe Creative Cloud] 并自动创建资源和处理媒体。

在中编辑资产 [!DNL Adobe Photoshop] 和 [!DNL Adobe Lightroom]，您无需从以下位置下载资产 [!DNL Experience Manager Assets]，再次编辑和上传它们。 您可以在中创建和配置处理配置文件 [!DNL Experience Manager]，将配置文件应用到文件夹，然后将资产上传到文件夹。 系统会根据处理配置文件重新处理您上传的资产，并且您会获得这些资产的变体。 一致且轻松的批量处理节省了手动操作并提高了内容速度，同时还无需一流的创作技能。 此外，开发人员和合作伙伴可以通过直接访问这些API来扩展资产微服务，并包含自定义逻辑。

用户可以创建处理配置文件，以对其资产自动执行以下创意操作：

* **自动色调**：使用人工智能分析图像的内容，并根据图像的独特属性智能地进行光照和颜色校正。

* **自动直立**：使用人工智能分析图像的内容并纠正图像中的倾斜透视。 例如，创建级别视野。

   ![自动色调](/help/assets/assets/content-automation-autotone.png)

   *图：自动色调和自动拉直可以帮助改善倾斜图像。*

* **Lightroom预设**：将用户定义的外观应用于图像，以使用自定义的预设实现一致的外观。

   ![Lightroom预设](/help/assets/assets/content-automation-lrpresets.png)

   *图：用于以一致的方式提高许多图像的图像质量的Adobe Lightroom预设。*

* **图像剪切**：使用人工智能围绕突出显示对象创建选区并通过单个命令删除背景。

   ![删除背景并从照片中剪切图像](/help/assets/assets/content-automation-backgroundremove.png)

* **图像蒙版**：使用人工智能通过单个命令围绕突出显示对象创建蒙版。

   ![使用AI蒙版图像](/help/assets/assets/content-automation-mask.png)

* **Photoshop操作**：应用一系列 [!DNL Adobe Photoshop] 任务到某个文件或一批文件。

   ![Photoshop操作](/help/assets/assets/content-automation-psactions.png)

* **智能对象替换**：通过允许您交换图像而大规模地进行个性化，同时保留在PSD文件中应用的所有效果和调整。

   ![智能地替换对象](/help/assets/assets/content-automation-objectreplace.png)

## 为AEMas a Cloud Service程序启用Content Automation {#enable-content-automation}

要使用Cloud Manager为AEMas a Cloud Service程序启用Content Automation加载项，请执行以下操作：

1. 请联系您的客户代表以许可Content Automation加载项。
1. 访问Cloud Manager并使用组织选择器切换到您的组织。
1. 单击 **[!UICONTROL 添加项目]** 并指定项目名称。
1. 单击&#x200B;**[!UICONTROL “继续”]**。
1. 展开 **[!UICONTROL 资产]** 并选择 **[!UICONTROL 内容自动化]**.
1. 单击&#x200B;**[!UICONTROL 创建]**。
1. 将管道运行到 [将更改部署到Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html).

如果您需要将Content Automation加载项添加到Cloud Manager中的现有AEMas a Cloud Service程序：

1. 单击项目信息卡上的……。

1. 选择 **[!UICONTROL 编辑项目群]** 然后选择 **[!UICONTROL 解决方案和加载项]** 选项卡。

1. 展开 **[!UICONTROL 资产]** 并选择 **[!UICONTROL 内容自动化]**.
1. 单击&#x200B;**[!UICONTROL 更新]**。
1. 将管道运行到 [将更改部署到Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html).

## 使用处理配置文件批量编辑您的创意资产 {#process-assets}

要使用处理配置文件自动创建变体，请执行以下步骤：

1. 导航到 **[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 处理配置文件]**.

1. 选择 **[!UICONTROL 创建]**，并指定 **[!UICONTROL 名称]**.

1. 选择 **[!UICONTROL Creative]** 选项卡，指定输出文件夹，选择 **[!UICONTROL 新增]** 以添加创意配置。

1. 提供 **[!UICONTROL 节目名称]** （或输出名称）， **[!UICONTROL 扩展]** （或文件类型），选择 **[!UICONTROL 质量]** （或输出参数），选择 **[!UICONTROL 包括]** 和 **[!UICONTROL 排除]** MIME类型列表（或输入资产过滤器），然后选择所需的创意操作。

   ![[!UICONTROL Creative] 按Tab键进入 [!UICONTROL 处理配置文件]](assets/creative-processing-profile.png)

1. 某些操作需要额外的参数（资源）。 如有必要，请提供这些额外参数的值。

1. 将更多创意操作添加为同一处理配置文件的一部分，或保存配置文件。

1. 将处理配置文件应用到文件夹。 在文件夹的 **[!UICONTROL 属性]** 页面，选择 **[!UICONTROL 资产处理]**，然后选择要应用的处理配置文件。

将处理配置文件应用到DAM文件夹后，此文件夹中上传或更新的所有资产除了执行标准处理之外，还会执行定义的操作。 子文件夹将继承与应用于父文件夹相同的配置文件。 用户可以覆盖此继承。

要处理现有资源，请选择资源，然后选择 **[!UICONTROL 重新处理]** 选项，然后选择所需的处理配置文件。

## 提示和限制 {#limitations-best-practices}

* [!DNL Experience Manager] 将资产处理限制为每个环境每分钟300个请求，每个组织每分钟700个请求。
* 文件大小限制为4 GB [!DNL Adobe Photoshop] API操作，1 GB用于 [!DNL Adobe Lightroom] 操作。

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
>* [通过处理配置文件配置和使用资源微服务](/help/assets/asset-microservices-configure-and-use.md).
>* [ [!DNL Experience Manager] 与 集成 [!DNL Creative Cloud]](/help/assets/aem-cc-integration-best-practices.md).
>* [使用资源微服务摄取和处理资源：概述](/help/assets/asset-microservices-overview.md).

