---
Description: Learn how to send data from your Adaptive Form to a SharePoint storage like a SharePoint list when you submit the form.
keywords: 如何为自适应表单连接SharePoint列表？ 、提交到SharePoint、创建SharePoint列表配置、在自适应表单中使用提交到SharePoint提交操作、将自适应表单连接到Microsoft&amp；reg； SharePoint列表。
feature: Adaptive Forms, Core Components, Foundation Components, Edge Delivery Services
title: 如何为自适应表单配置提交操作？
role: User, Developer
exl-id: 9ac3e7be-c6fa-4dbc-9aba-b81741ba6c55
source-git-commit: 1be7bafc1d93a65a81eeb2f7e86cac33cde7aa35
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 30%

---

# 将自适应表单连接到Microsoft® SharePoint列表 {#connect-af-sharepoint-list}

>[!VIDEO](https://video.tv.adobe.com/v/3424820/connect-aem-adaptive-form-to-sharepointlist/?quality=12&learn=on)

<span>此视频仅适用于核心组件。 对于UE/Foundation组件，请参阅文章。</span>

要在自适应表单中使用[!UICONTROL 提交到SharePoint列表]提交操作，请执行以下操作：

1. [创建SharePoint列表配置](#1-create-a-sharepoint-list-configuration)：它将AEM Forms连接到您的Microsoft® Sharepoint列表存储。
1. [在自适应表单中使用表单数据模型(FDM)提交](#2-use-the-submit-using-form-data-model-fdm-in-an-adaptive-form-use-submit-using-fdm)：它将您的自适应表单连接到配置的Microsoft® SharePoint。

## 1.创建SharePoint列表配置

要将AEM Forms连接到Microsoft®Sharepoint列表：

1. 转到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Microsoft® SharePoint]**。
1. 选择&#x200B;**配置容器**。配置存储在选定的配置容器中。
1. 从下拉列表中单击&#x200B;**[!UICONTROL 创建]** > **[!UICONTROL SharePoint列表]**。 这将显示 SharePoint 配置向导。
1. 指定&#x200B;**[!UICONTROL 标题]**、**[!UICONTROL 客户端 ID]**、**[!UICONTROL 客户端密码]**&#x200B;和 **[!UICONTROL OAuth URL]**。有关如何检索 OAuth URL 的客户端 ID、客户端密码、租户 ID 的信息，请参阅 [Microsoft® 文档](https://learn.microsoft.com/en-us/graph/auth-register-app-v2)。
   * 您可以从 Microsoft® Azure 门户检索应用程序的`Client ID` 和`Client Secret`。
   * 在 Microsoft® Azure 门户中，将重定向 URI 添加为 `https://[author-instance]/libs/cq/sharepointlist/content/configurations/wizard.html`。将 `[author-instance]` 替换为创作实例 URL。
   * 在`offline_access`Microsoft® Graph`Sites.Manage.All`选项卡中添加API权限&#x200B;**和**&#x200B;以提供读/写权限。 在`AllSites.Manage`Sharepoint **选项卡中添加**&#x200B;权限以与SharePoint数据进行远程交互。
   * 使用 OAuth URL：`https://login.microsoftonline.com/tenant-id/oauth2/v2.0/authorize`。将 `<tenant-id>` 替换为 Microsoft® Azure 门户中应用程序的 `tenant-id`。

     >[!NOTE]
     >
     > **客户端密码**&#x200B;字段是必填还是可选字段取决于 Azure Active Directory 应用程序配置。如果应用程序配置为使用客户端密码，则必须提供客户端密码。

1. 单击&#x200B;**[!UICONTROL 连接]**。连接成功后，将显示`Connection Successful`消息。
1. 从下拉列表中选择&#x200B;**[!UICONTROL SharePoint站点]**&#x200B;和&#x200B;**[!UICONTROL SharePoint列表]**。
1. 选择&#x200B;**[!UICONTROL 创建]**&#x200B;以创建Microsoft® SharePointList的云配置。


## 2.在自适应表单中使用表单数据模型(FDM)提交 {#use-submit-using-fdm}

您可以在自适应表单中使用创建的SharePoint列表配置，以在SharePoint列表中保存数据或生成的记录文档。 执行以下步骤以在自适应表单中使用SharePoint列表：

1. [使用Microsoft创建表单数据模型(FDM)](/help/forms/create-form-data-models.md)
1. [配置表单数据模型(FDM)以检索和发送数据](/help/forms/work-with-form-data-model.md#configure-services)
1. [创建自适应表单](/help/forms/creating-adaptive-form-core-components.md)
1. [使用表单数据模型(FDM)配置提交操作](/help/forms/using-form-data-model.md)

提交表单时，数据将保存在指定的Microsoft® Sharepoint列表存储中。

>[!NOTE]
>
> 在Microsoft® SharePoint List中，不支持以下列类型：
> * 图像列
> * 元数据列
> * 人员列
> * 外部数据列

## 相关文章

{{af-submit-action}}
