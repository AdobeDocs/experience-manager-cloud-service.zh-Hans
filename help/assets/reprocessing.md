---
title: 重新处理数字资产
description: 了解重新处理数字资产的各种方法
contentOwner: KK
exl-id: 4759fa8c-10c7-4446-a135-3104b9beaee8
feature: Asset Processing
role: User, Leader, Developer
source-git-commit: ab2cf8007546f538ce54ff3e0b92bb0ef399c758
workflow-type: tm+mt
source-wordcount: '685'
ht-degree: 0%

---

# 重新处理数字资产 {#reprocessing-digital-assets}

如果文件夹已具有您后来更改的现有元数据配置文件，您可以重新处理该文件夹中的资产。 如果希望将新编辑的预设重新应用于文件夹中的现有资源，则必须重新处理文件夹。 您可以根据需要重新处理尽可能多的资产。

如果您遇到以下两种情况之一，请重新处理文件夹中的资产：

* 要在已上传资产的现有资产文件夹上运行批次集预设。
* 您稍后可以编辑之前应用于资产文件夹的现有批次集预设。

## 重新处理资产 {#reprocessing-steps}

要重新处理文件夹中的资产，请执行以下操作：

1. 在[!DNL Experience Manager]中，从Assets页面中，选择新添加的资源或要重新处理的资源。
如果您选择文件夹：

   * 工作流会递归考虑选定文件夹中的所有文件。
   * 如果主选定文件夹中存在一个或多个具有资产的子文件夹，则工作流会重新处理文件夹层次结构中的每个资产。
   * 作为最佳实践，请避免在具有超过1000个资产的文件夹层次结构上运行此工作流。

1. 选择&#x200B;**[!UICONTROL 重新处理Assets]**。 从以下两个选项中进行选择：

   ![重新处理Assets选项](assets/reprocessing-assets-options.png)

   * **[!UICONTROL 完整流程]：**&#x200B;当您要执行包括默认配置文件、自定义配置文件、动态处理（如果已配置）和后处理工作流的整个流程时，请选择此选项。
   * **[!UICONTROL 高级]：**&#x200B;选择此选项可选择高级重新处理。

     ![高级重新处理Assets选项](assets/reprocessing-assets-options-advanced.png)

     从以下高级选项中进行选择：

      * **[!UICONTROL 默认预览演绎版]：**&#x200B;如果要重新处理默认预览的演绎版，请选择此选项。

      * **[!UICONTROL 元数据]：**&#x200B;如果要提取所选资源的元数据信息和智能标记，请选择此选项。

      * **[!UICONTROL 处理配置文件]：**&#x200B;要重新处理选定的配置文件时，请选择此选项。 您可以选择&#x200B;**[!UICONTROL 完整流程]**选项以包括在文件夹级别分配的默认处理和自定义配置文件。
        <!--When assets are uploaded to a folder, [!DNL Experience Manager] checks the containing folder's properties for a processing profile. If none is applied, a parent folder in the hierarchy is checked for a processing profile to apply.-->

      * **[!UICONTROL Post处理工作流]：**&#x200B;选择此选项时，需要额外处理无法使用处理配置文件实现的资源。 可以向配置中添加其他后处理工作流。 Post-processing允许您在使用资源微服务的可配置处理之上添加完全自定义的处理。

请参阅[使用资产微服务和处理配置文件](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/asset-microservices-configure-and-use.html?lang=en)，了解有关处理配置文件和后处理工作流的详细信息。

![高级重新处理Assets选项2](assets/reprocessing-assets-options-advanced-2.png)

选择适当的选项后，单击&#x200B;**[!UICONTROL 重新处理]**。 此时将显示成功消息。

## 重新处理数字资产的情况 {#scenarios-reprocessing}

[!DNL Experience Manager]允许重新处理以下组件的数字资产。

### 智能标记 {#reprocessing-smart-tags}

处理数字资产的组织越来越多地在资产元数据中使用分类控制的词汇。 本质上，它包括员工、合作伙伴和客户通常用于引用和搜索特定类的数字资产的关键字列表。 使用分类控制的词汇标记资产可确保轻松识别和检索资产。

与自然语言词汇相比，根据业务分类标记数字资产有助于使其与公司的业务保持一致，并确保最相关的资产出现在搜索中。

阅读有关[视频资源智能标记](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/smart-tags-video-assets.html?lang=en)的更多信息。

阅读有关[重新处理DAM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/color-tag-images.html?lang=en#color-tags-existing-images)中现有图像的颜色标记的详细信息。

### 智能裁剪 {#reprocessing-smart-crop}

了解有关[Dynamic Media智能裁切](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/image-profiles.html?lang=en)的更多信息，该功能允许您对上传的资源应用特定裁切（**[!UICONTROL 智能裁切]**&#x200B;和像素裁切）和锐化配置。

### 元数据 {#reprocessing-metadata}

[!DNL Adobe Experience Manager Assets]保留每个资源的元数据。 它允许更轻松地分类和组织资产，并帮助查找特定资产的人员。 利用从上载到Experience Manager Assets的文件中提取元数据的功能，元数据管理与创作工作流集成。 利用使用资源保留和管理元数据的功能，您可以根据资源的元数据自动组织和处理资源。

阅读有关[重新处理元数据配置文件](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/metadata-profiles.html?lang=en)的详细信息。

### 重新处理文件夹中的Dynamic Media资源 {#reprocessing-dynamic-media}

如果文件夹已具有现有的Dynamic Media图像配置文件或您后来更改的Dynamic Media视频配置文件，您可以重新处理该文件夹中的资产。 有关详细信息，请访问[重新处理文件夹中的Dynamic Media资源。](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/about-image-video-profiles.html?lang=en)

>[!NOTE]
>
>您需要在环境中配置[!DNL Dynamic Media]以启用Dynamic Media对话框。
>

### 工作流

阅读有关[处理配置文件和后处理工作流](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/asset-microservices-configure-and-use.html?lang=en)的更多信息。
