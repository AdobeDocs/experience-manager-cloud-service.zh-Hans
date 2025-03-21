---
title: 使用Adobe Express在Content Hub中编辑图像
description: 使用Adobe Express在Content Hub中编辑图像
exl-id: c9777862-226c-4d39-87da-9c4a30437dc5
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 18%

---

# 在Content Hub中编辑图像 {#edit-images-content-hub}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime和Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup><a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM Assets与Edge Delivery Services的集成</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>UI可扩展性</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新建</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>启用Dynamic Media Prime和Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>搜索最佳实践</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>元数据最佳实践</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Content Hub</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>具有 OpenAPI 功能的 Dynamic Media</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>AEM Assets 开发人员文档</b></a>
        </td>
    </tr>
</table>

![使用Adobe Express在Content Hub中编辑图像](assets/edit-images-content-hub.png)

>[!AVAILABILITY]
>
>Content Hub 指南现以 PDF 格式提供。下载完整指南并使用 Adobe Acrobat AI 助手来回答您的疑问。
>
>[!BADGE Content Hub 指南 PDF]{type=Informative url="https://helpx.adobe.com/cn/content/dam/help/en/experience-manager/aem-assets/content-hub.pdf"}

Content Hub允许您使用Adobe Express创建新内容。 您可以使用易于使用的工具编辑现有内容，使用模板和品牌元素制作品牌变体，并使用 Adobe Firefly 的最新 GenAI功 能创建新内容。

## 先决条件 {#prereqs-edit-image-content-hub}

有权访问Adobe Express和[Content Hub用户，有权将资源重新混合到新变体](/help/assets/deploy-content-hub.md#onboard-content-hub-users-remix-assets)，可以使用Content Hub编辑图像。

>[!NOTE]
>
您可以使用[!DNL Adobe Express]编辑PNG和JPG/JPEG文件类型的图像。

## 使用 [!DNL Adobe Express] 编辑图像 {#edit-images-using-content-hub}

要使用Content Hub编辑图像，请执行以下操作：

1. 单击需要编辑的图像的资产卡上可用的&#x200B;**[!DNL Open in Adobe Express]**。 或者，单击该图像以打开其详细信息，然后单击[!DNL Adobe Express]徽标。 随后，无需离开Content Hub，即可加载Adobe Express的嵌入式编辑器。

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
