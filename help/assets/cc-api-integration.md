---
title: 内容自动化以实现Creative Cloud集成
description: 使用Creative Cloud集成生成资产的变体
contentOwner: AG
feature: 上传、资产处理、发布、Asset compute微服务、工作流
role: User,Admin
source-git-commit: a2c2a1f4ef4a8f0cf1afbba001d24782a6a2a24e
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 0%

---


# 使用[!DNL Adobe Creative Cloud]集成生成资产的变体 {#content-automation}

内容自动化附加组件将Experience Manager资产作为Cloud Service与Adobe Creative Cloud API集成，以创造性地大规模处理您的资产。 Experience Manager使用基于云的[资产微服务](/help/assets/asset-microservices-overview.md)来利用Adobe Creative Cloud功能并自动执行资产创建和媒体处理。

要编辑[!DNL Adobe Photoshop]和[!DNL Adobe Lightroom]中的资产，您无需从中下载、编辑资产并将其上传到[!DNL Experience Manager Assets]。 只需创建并配置处理配置文件，将配置文件应用到文件夹，然后将资产上传到该文件夹即可。 上传到文件夹的资产会进行处理，以创建该资产的不同变体。 对资产进行一致且轻松的批量处理和编辑，可节省手动工作并提高内容速度。 此外，开发人员和合作伙伴可以通过直接访问这些API来扩展资产微服务，并包含自定义逻辑。

用户可以创建处理配置文件以自动对其资产执行以下创意操作：

* **自动色调**:利用人工智能对图像内容进行分析，并根据图像的独特属性智能地进行光和颜色校正。
* **自动垂直**:利用人工智能对图像内容进行分析，并修正图像中的偏斜透视。例如，创建水平视线。
* **Lightroom预设**:对图像应用用户定义的外观，以使用自定义预设获得一致的外观。
* **图像木刻**:利用人工智能在显着对象周围创建选择，并使用单个命令删除背景。
* **图像蒙版**:利用人工智能通过单个命令在显着对象周围创建蒙版。
* **Photoshop操作**:将一系列任务(在Photoshop中)应用到文件或批量文件。
* **智能对象替换**:通过允许您交换图像，同时保留PSD文件中应用的所有效果和调整，来大规模执行个性化。

## 使用处理配置文件处理资产 {#process-assets}

要使用处理配置文件自动创建变体，请执行以下步骤：

1. 联系[Adobe客户关怀](https://experienceleague.adobe.com/#support)以接收许可证。

1. 导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 处理配置文件]**。

1. 选择&#x200B;**[!UICONTROL 创建]**，然后指定&#x200B;**[!UICONTROL 名称]**。

1. 选择&#x200B;**[!UICONTROL Creative]**&#x200B;选项卡，指定输出文件夹，选择&#x200B;**[!UICONTROL Add New]**&#x200B;以添加创作配置。

1. 提供&#x200B;**[!UICONTROL 演绎版名称]**（或输出名称）、**[!UICONTROL 扩展名]**（或文件类型），选择&#x200B;**[!UICONTROL 质量]**（或输出参数），选择包含和排除MIME类型列表（或输入资产过滤器），然后选择所需的创作操作。

1. 某些操作需要额外的参数（资产）。 根据需要为此类其他参数提供值。

1. 将更多创意操作添加为同一处理配置文件的一部分或保存配置文件。

1. 将处理配置文件应用到文件夹。 在文件夹的&#x200B;**[!UICONTROL 属性]**&#x200B;页面上，选择&#x200B;**[!UICONTROL 资产处理]**，然后选择要应用的处理配置文件。

在将处理配置文件应用到DAM文件夹后，此文件夹中上传或更新的所有资产，除了标准处理之外，还会执行定义的操作。 子文件夹将继承与在父文件夹中应用的配置文件相同的配置文件。 用户可以覆盖此继承。

要处理现有资产，请选择资产，选择&#x200B;**[!UICONTROL 重新处理]**&#x200B;选项，然后选择所需的处理配置文件。

## 提示和限制 {#limitations-best-practices}

* [!DNL Experience Manager] 将资产处理限制为每个环境每分钟300个请求，每个组织每分钟700个请求。
* 对于[!DNL Adobe Photoshop] API操作，文件大小限制为4 GB；对于[!DNL Adobe Lightroom]操作，文件大小限制为1 GB。

>[!MORELIKETHIS]
>
>* [通过处理配置文件配置和使用资产微服务](/help/assets/asset-microservices-configure-and-use.md)。
>* [ [!DNL Experience Manager] 与 [!DNL Creative Cloud]](/help/assets/aem-cc-integration-best-practices.md)集成。

