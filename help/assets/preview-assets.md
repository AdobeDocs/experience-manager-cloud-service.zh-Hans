---
title: 在您的AEM Sites页面中使用资源之前对其进行预览
description: 通过具有OpenAPI功能的Dynamic Media，您可以在Adobe Experience Manager (AEM) Sites预览页面上预览资源。 通过此资产预览，您和利益相关者可在发布创作页面（包含更新的资产）供公众使用之前，查看和验证资产的更新。
role: Admin, User
exl-id: 6f071ca9-0f84-45fc-a6b3-047cca9d5e65
source-git-commit: 3f3e091d09b94418fc2cda0bd3b3ce950555b7a9
workflow-type: tm+mt
source-wordcount: '731'
ht-degree: 0%

---


# 在AEM Sites页面中使用资源之前进行预览 {#asset-preview-using-Dynamic-Media-with-OpenAPI-capabilities}

[!DNL Dynamic Media with OpenAPI capabilities]允许您在公开资源之前预览[!DNL Adobe Experience Manager (AEM) Sites]创作页面中可用的资源。 资源预览在网站的创作层和预览层上可用。

要[在AEM Sites预览页面上预览资源](#asset-preview-on-sites-pages-using-Dynamic-Media-with-OpenAPI-capabilities)，请通过添加要预览的资源或替换实时站点页面中可用的现有资源来更新网站的作者页面。 将更新的创作页面发布到预览层以生成预览URL。

与利益相关者共享预览页面，以收集关于更新资源的视觉质量和上下文对齐的反馈。 根据反馈优化资源。 在审核周期中创建和管理资产的多个版本。

最终确定可供公众使用的资产后，在创作页面中更新这些资产，并将页面发布到发布层以供公众访问。

## 开始之前{#prerequisites-for-previewing-assets-using-Dynamic-Media-with-OpenAPI-capabilities}

确保您具有：

* 访问[!DNL AEM Assets as a Cloud Service]。
* 编辑资产的Status属性的权限。
* [已将[!UICONTROL 预览]值添加到应用于包含要预览的资源文件夹的元数据表单的[!UICONTROL 基本]选项卡[!UICONTROL 中的]状态](/help/assets/metadata-assets-view.md#edit-metadata-forms)元数据属性中。
  ![添加预览选项](/help/assets/assets/metedata-form-preview.png)
* 用于生成预览令牌的键。 [联系Adobe支持](https://helpx.adobe.com/in/contact.html)并提出密钥请求。

## 在站点预览页面中预览资产 {#asset-preview-on-sites-pages-using-Dynamic-Media-with-OpenAPI-capabilities}

您可以预览已批准的新资源或资源。 批准的资产仅显示在您的实时站点页面上。

执行以下步骤以将资源状态设置为在[!DNL Assets View]中预览，然后将站点创作页面发布到预览层以生成页面的预览URL：

1. 通过执行以下步骤，将资源状态设置为&#x200B;**[!UICONTROL 预览]**：

   1. 在[!DNL Assets View]中，选择&#x200B;**[!UICONTROL Assets]**&#x200B;并导航到您的文件夹。
   1. 选择要预览的资源。
   1. 单击&#x200B;**[!UICONTROL 详细信息]**。
   1. 在[!UICONTROL 信息面板]中，将&#x200B;**[!UICONTROL 状态]**&#x200B;设置为&#x200B;**[!UICONTROL 预览]**，然后单击&#x200B;**[!UICONTROL 保存]**。
      ![预览](/help/assets/assets/preview-boat-at-bay.png)

1. 导航到站点创作页面。 执行[访问AEM页面编辑器中的远程资源](/help/assets/integrate-remote-approved-assets-with-sites.md#access-remote-assets-in-aem-page-editor)部分中的步骤，以使用“资源选择器”面板选择您最近设置为“预览”的资源（状态）。

   >[!NOTE]
   >
   > 资源选择器显示最近状态更新设置为“已批准”或“预览”的资源。

1. 使用&#x200B;**[!UICONTROL 管理发布]**&#x200B;选项将页面发布到预览层。 执行[将内容发布到预览](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/sites/authoring/sites-console/previewing-content)部分中的步骤以将页面发布到预览层。 发布后，生成页面的预览URL。 “预览”页面显示站点页面中的资源（具有最近的状态更新）。

与利益相关者共享此预览URL，以供审阅和反馈。 确保您的利益相关者有权访问预览页面。 有关提供预览页面访问权限的信息，请参阅[访问预览服务](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-environments#access-preview-service)。

>[!NOTE]
>
>默认情况下，[图像V3核心组件](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/wcm-components/image#version-and-compatibility)支持预览版本的资源。 使用[资源选择器](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/manage/asset-selector/asset-selector-upload)面板选择资源的预览版本（具有预览状态的资源）时，图像V3组件会在预览层（站点作者页面上的预览版本）中自动呈现该资源。

在最终确定资源版本后，[将您的页面发布到发布层](#publish-your-pages-to-publish-tier)以供公众使用。

## 使用批准的资产发布页面以供公共使用{#publish-your-pages-to-publish-tier}

最终确定资源版本以供公共使用后，将资源状态设置为&#x200B;**[!UICONTROL 已批准]**。 然后将页面发布到发布层。 执行以下步骤以发布页面：

1. 按照上面[在网站预览页面](#asset-preview-on-sites-pages-using-Dynamic-Media-with-OpenAPI-capabilities)中预览资源部分中的步骤1，将资源状态更改为&#x200B;**[!UICONTROL 已批准]**。
1. 导航到您的站点作者页面并将其发布到[!DNL Publish tier]。 通过执行从页面编辑器[部分中](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/sites/authoring/page-editor/publishing#publishing-from-the-page-editor)发布中的步骤来发布页面。
或者，按照[从站点控制台](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/sites/authoring/sites-console/publishing-pages#publishing-from-the-sites-console)部分发布页面中的步骤操作，从站点控制台发布页面。

   >[!NOTE]
   >
   > 发布层上只能交付已批准的资产。 批准资产，然后再将页面发布到发布层供公共使用。

   ![页面已发布](/help/assets/assets/the-page-has-been-publushed.png)
成功发布后，将显示一条确认消息&#x200B;**[!UICONTROL 页面已发布]**。 导航到发布层上的已发布页面，以确认更新已上线并且内容按预期显示。
