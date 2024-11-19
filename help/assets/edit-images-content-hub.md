---
title: 在Content Hub中使用Adobe Express编辑图像
description: 在Content Hub中使用Adobe Express编辑图像
exl-id: c9777862-226c-4d39-87da-9c4a30437dc5
source-git-commit: ed7331647ea2227e6047e42e21444b743ee5ce6d
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 6%

---

# 在Content Hub中编辑图像 {#edit-images-content-hub}

| [搜索最佳实践](/help/assets/search-best-practices.md) | [元数据最佳实践](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | [具有 OpenAPI 功能的 Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets 开发人员文档](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

![使用Adobe Express在Content Hub中编辑图像](assets/edit-images-content-hub.png)

>[!AVAILABILITY]
>
>Content Hub指南现在提供了PDF格式。 下载整个指南，并使用Adobe Acrobat AI Assistant来回答您的疑问。
>
>[!BADGE Content Hub指南PDF]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/content-hub.pdf"}

Content Hub允许您使用Adobe Express创建新内容。 您可以通过易于使用的工具编辑现有内容，使用模板和品牌元素生成品牌内变体，以及通过Adobe Firefly中的最新GenAI功能创建新内容。

## 先决条件 {#prereqs-edit-image-content-hub}

有权访问Adobe Express和有权将资源重新混合到新变体的[Content Hub用户](/help/assets/deploy-content-hub.md#onboard-content-hub-users-remix-assets)可以使用Content Hub编辑图像。

>[!NOTE]
>
您可以使用[!DNL Adobe Express]编辑PNG和JPG/JPEG文件类型的图像。

## 使用 [!DNL Adobe Express] 编辑图像 {#edit-images-using-content-hub}

要使用Content Hub编辑图像，请执行以下操作：

1. 单击需要编辑的图像的资产卡上可用的&#x200B;**[!DNL Open in Adobe Express]**。 或者，单击该图像以打开其详细信息，然后单击[!DNL Adobe Express]徽标。 然后，无需离开Content Hub即可加载用于Adobe Express的嵌入式编辑器。

   您可以利用[!DNL Adobe Express]功能执行所有与图像编辑相关的操作，如[调整图像大小](https://helpx.adobe.com/express/using/resize-image.html)、[删除或更改背景颜色](https://helpx.adobe.com/express/using/remove-background.html)、[裁切图像](https://helpx.adobe.com/express/using/crop-image.html)、将图像与AI生成的图像或文本组合等等。

1. 执行修改并单击&#x200B;**[!UICONTROL 保存]**&#x200B;可将编辑后的资源保存为以下任一格式类型：

   * **[!UICONTROL PNG]**（用作高质量的图像格式）
   * **[!UICONTROL JPG]** （适用于小文件）
   * **[!UICONTROL PDF]** （适用于文档）

   ![使用 Adobe Express 保存图像](assets/adobe-express-save-as.png)

1. 在&#x200B;**[!UICONTROL 另存为]**&#x200B;字段中指定资源的名称。

1. 使用&#x200B;**[!UICONTROL 促销活动名称]**&#x200B;字段指定资产的促销活动名称。 您可以使用现有名称或创建新名称。 键入名称时，Content Hub会为您提供更多选项。<!--You can define multiple Campaign names for your upload. While you are typing a name, either click anywhere else within the dialog box or press the `,` (Comma) key to register the name.-->

   作为最佳实践，Adobe建议在其他字段中指定值，并且为上传的资源创建增强的搜索体验。

1. [可选]定义&#x200B;**[!UICONTROL 关键字]**、**[!UICONTROL 渠道]**、**[!UICONTROL 时间范围]**&#x200B;和&#x200B;**[!UICONTROL 区域]**&#x200B;字段的值。 通过按关键字、渠道和位置对资产进行标记和分组，使用您批准的公司内容的每个人都可以找到这些资产并保持其井然有序。

1. 单击&#x200B;**[!UICONTROL 另存为新资源]**&#x200B;以保存该资源。

管理员还可以配置在向Content Hub添加资源时显示的必填和可选字段，例如营销策划名称、关键字、渠道等。 有关详细信息，请参阅[配置Content Hub用户界面](configure-content-hub-ui-options.md#configure-upload-options-content-hub)。
