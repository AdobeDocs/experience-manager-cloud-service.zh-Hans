---
title: 内容自动化以实现Creative Cloud集成
description: 使用Creative Cloud集成生成资产的变体
contentOwner: AG
feature: 上传、资产处理、发布、Asset compute微服务、工作流
role: User,Admin
source-git-commit: f21f8bf7975fd4e82785a4c368cf4956096608d4
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 0%

---


# 使用[!DNL Adobe Creative Cloud]集成生成资产的变体 {#content-automation}

内容自动附加组件集成了[!DNL Adobe Experience Manager Assets as a Cloud Service]和[!DNL Adobe Creative Cloud] API，以创造性地大规模处理资产。 [!DNL Experience Manager] 使用基于云的 [资](/help/assets/asset-microservices-overview.md) 产微服务来使 [!DNL Adobe Creative Cloud] 用这些功能并自动创建和处理资产。

要编辑[!DNL Adobe Photoshop]和[!DNL Adobe Lightroom]中的资产，您无需从[!DNL Experience Manager Assets]下载资产、编辑资产，然后再次上传资产。 您可以在[!DNL Experience Manager]中创建并配置处理配置文件，将配置文件应用到文件夹，然后将资产上传到该文件夹。 您上传的资产会根据处理配置文件进行重新处理，您会获得这些资产的变体。 一致且轻松的批量处理可节省手动工作并提高内容速度，而无需卓越的创作技能。 此外，开发人员和合作伙伴还可以通过直接访问这些API来扩展资产微服务，并包含自定义逻辑。

用户可以创建处理配置文件以自动对其资产执行以下创意操作：\
![自动执行Adobe Photoshop和AdobeLightroom资产操作](assets/content-automation.png)
* **自动色调**:利用人工智能对图像内容进行分析，并根据图像的独特属性智能地进行光和颜色校正。
* **自动垂直**:使用人工智能来分析图像的内容并纠正图像中的偏斜透视。例如，创建水平视线。
* **Lightroom预设**:对图像应用用户定义的外观，以使用自定义预设获得一致的外观。
* **图像木刻**:使用人工智能在显着对象周围创建选择并使用单个命令删除背景。
* **图像蒙版**:使用人工智能通过单个命令在显着对象周围创建蒙版。
* **Photoshop操作**:将一系列任务(在Photoshop中)应用到文件或批量文件。
* **智能对象替换**:通过允许您交换图像，同时保留PSD文件中应用的所有效果和调整，实现大规模个性化。



## 使用处理配置文件批量编辑您的创意资产 {#process-assets}

要使用处理配置文件自动创建变体，请执行以下步骤：

1. 联系[Adobe客户关怀](https://experienceleague.adobe.com/#support)以接收许可证。

1. 导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 处理配置文件]**。

1. 选择&#x200B;**[!UICONTROL 创建]**，然后指定&#x200B;**[!UICONTROL 名称]**。

1. 选择&#x200B;**[!UICONTROL Creative]**&#x200B;选项卡，指定输出文件夹，选择&#x200B;**[!UICONTROL Add New]**&#x200B;以添加创作配置。

1. 提供&#x200B;**[!UICONTROL 演绎版名称]**（或输出名称）、**[!UICONTROL 扩展名]**（或文件类型）、选择&#x200B;**[!UICONTROL 质量]**（或输出参数）、选择&#x200B;**[!UICONTROL 包括]**&#x200B;和&#x200B;**[!UICONTROL 排除]** MIME类型列表（或输入资产过滤器），然后选择所需的创作操作。<br/>

   ![处理配置文件中的“创作”选项卡](assets/creative-processing-profile.png)

1. 某些操作需要额外的参数（资产）。 根据需要为这些额外参数提供值。

1. 将更多创意操作添加为同一处理配置文件的一部分或保存配置文件。

1. 将处理配置文件应用到文件夹。 在文件夹的&#x200B;**[!UICONTROL 属性]**&#x200B;页面上，选择&#x200B;**[!UICONTROL 资产处理]**，然后选择要应用的处理配置文件。

在将处理配置文件应用到DAM文件夹后，此文件夹中上传或更新的所有资产，除了标准处理之外，还会执行定义的操作。 子文件夹将继承与在父文件夹上应用的配置文件相同。 用户可以覆盖此继承。

要处理现有资产，请选择资产，选择&#x200B;**[!UICONTROL 重新处理]**&#x200B;选项，然后选择所需的处理配置文件。

## 提示和限制 {#limitations-best-practices}

* [!DNL Experience Manager] 将资产处理限制为每个环境每分钟300个请求，每个组织每分钟700个请求。
* 对于[!DNL Adobe Photoshop] API操作，文件大小限制为4 GB；对于[!DNL Adobe Lightroom]操作，文件大小限制为1 GB。

>[!MORELIKETHIS]
>
>* [通过处理配置文件配置和使用资产微服务](/help/assets/asset-microservices-configure-and-use.md)。
>* [ [!DNL Experience Manager] 与 [!DNL Creative Cloud]](/help/assets/aem-cc-integration-best-practices.md)集成。
>* [使用资产微服务获取和处理资产：概述](/help/assets/asset-microservices-overview.md)。

