---
Title: How to send data to a SharePoint storage on submission of an Adaptive Form?
Description: Learn how to send data from your Adaptive Form to a SharePoint storage like a SharePoint list or Document library when you submit the form.
keywords: 如何为自适应表单连接SharePoint列表？ 、如何为自适应表单连接SharePoint文档库、提交到SharePoint、创建SharePoint文档库配置、在自适应表单中使用提交到SharePoint提交操作、将自适应表单连接到Microsoft&reg；SharePoint列表。
feature: Adaptive Forms, Core Components
exl-id: e925a750-5fb5-4950-afd3-78551eec985d
source-git-commit: 81951a9507ec3420cbadb258209bdc8e2b5e2942
workflow-type: tm+mt
source-wordcount: '1042'
ht-degree: 34%

---

# 将自适应表单连接到Microsoft® SharePoint

此 **[!UICONTROL 提交到SharePoint]** 通过提交操作，可将自适应表单与Microsoft® SharePoint存储无缝连接。 在您提交表单后，它会将表单数据发送到您选择的SharePoint存储中。

AEMas a Cloud Service提供了多种现成的提交操作来处理表单提交。 有关这些选项的更多信息，请参阅 [自适应表单提交操作](/help/forms/configure-submit-actions-core-components.md)  文章。

## 优点

将数据从自适应表单提交到SharePoint存储的一些优势包括：

* 它有助于将表单数据直接提交到SharePoint，为存储和管理信息提供一个集中的位置。
* 通过应用SharePoint的访问控制和权限功能，可确保只有授权人员才能查看或修改提交的数据。

使用 **[!UICONTROL 提交到SharePoint]**，您可以：

* [将自适应表单连接到SharePoint文档库](#connect-af-sharepoint-doc-library)
* [将自适应表单连接到SharePoint列表](#connect-af-sharepoint-list)

## 将自适应表单连接到SharePoint文档库 {#connect-af-sharepoint-doc-library}

要使用 **[!UICONTROL 提交到SharePoint文档库]** 以自适应表单提交操作：

1. [创建SharePoint文档库配置](#create-a-sharepoint-configuration-create-sharepoint-configuration)：用于将AEM Forms连接到Microsoft® Sharepoint存储。
2. [在自适应表单中使用“提交到 SharePoint”提交操作](#use-sharepoint-configuartion-in-af)：它将自适应表单连接到配置的 Microsoft® SharePoint。

### 创建SharePoint文档库配置 {#create-sharepoint-configuration}

要将AEM Forms连接到Microsoft®Sharepoint文档库存储，请执行以下操作：

1. 转到您的 **AEM Forms Author** 实例> **[!UICONTROL 工具]** > **[!UICONTROL Cloud Service]** >  **[!UICONTROL Microsoft®SharePoint]**.
1. 一旦您选择 **[!UICONTROL Microsoft®SharePoint]**，您将被重定向到 **[!UICONTROL SharePoint Browser]**.
1. 选择&#x200B;**配置容器**。配置存储在选定的配置容器中。
1. 单击 **[!UICONTROL 创建]** > **[!UICONTROL SharePoint文档库]** 下拉列表中。 这将显示 SharePoint 配置向导。

   ![SharePoint 配置](/help/forms/assets/sharepoint_configuration.png)
1. 指定&#x200B;**[!UICONTROL 标题]**、**[!UICONTROL 客户端 ID]**、**[!UICONTROL 客户端密码]**&#x200B;和 **[!UICONTROL OAuth URL]**。有关如何检索 OAuth URL 的客户端 ID、客户端密码、租户 ID 的信息，请参阅 [Microsoft® 文档](https://learn.microsoft.com/en-us/graph/auth-register-app-v2)。
   * 您可以从 Microsoft® Azure 门户检索应用程序的`Client ID` 和`Client Secret`。
   * 在 Microsoft® Azure 门户中，将重定向 URI 添加为 `https://[author-instance]/libs/cq/sharepoint/content/configurations/wizard.html`。将 `[author-instance]` 替换为创作实例 URL。
   * 添加 API 权限 `offline_access` 和 `Sites.Manage.All` 以提供读/写权限。
   * 使用 OAuth URL：`https://login.microsoftonline.com/tenant-id/oauth2/v2.0/authorize`。将 `<tenant-id>` 替换为 Microsoft® Azure 门户中应用程序的 `tenant-id`。

   >[!NOTE]
   >
   > **客户端密码**&#x200B;字段是必填还是可选字段取决于 Azure Active Directory 应用程序配置。如果应用程序配置为使用客户端密码，则必须提供客户端密码。

1. 单击&#x200B;**[!UICONTROL 连接]**。连接成功后，将显示`Connection Successful`消息。

1. 现在，选择 **SharePoint站点** > **文档库** > **SharePoint文件夹**，以保存数据。

   >[!NOTE]
   >
   >* 默认情况下， `forms-ootb-storage-adaptive-forms-submission` 在选定的SharePoint站点上出现。
   >* 创建文件夹为 `forms-ootb-storage-adaptive-forms-submission`，如果列表中尚未存在 `Documents` 选定SharePoint站点的库，方法是单击 **创建文件夹**.

现在，您可以在自适应表单中将此SharePoint Sites配置用于提交操作。

### 在自适应表单中使用SharePoint文档库配置 {#use-sharepoint-configuartion-in-af}

您可以在自适应表单中使用创建的SharePoint文档库配置，将数据或生成的记录文档保存到SharePoint文件夹中。 执行以下步骤以在自适应表单中使用SharePoint文档库存储配置，如下所示：

1. 创建[自适应表单](/help/forms/creating-adaptive-form-core-components.md)。

   >[!NOTE]
   >
   > * 选择相同的 [!UICONTROL 配置容器] 用于自适应表单，您已在该表单中创建了SharePoint Document Library存储。
   > * 如果未选择[!UICONTROL 配置容器]，则全局[!UICONTROL 存储配置]文件夹将显示在提交操作属性窗口中。

1. 选择&#x200B;**[!UICONTROL 提交到 SharePoint]** 作为&#x200B;**提交操作**。
   ![SharepointGIF](/help/forms/assets/sharedrive-video.gif)
1. 选择要用于保存数据的&#x200B;**[!UICONTROL 存储配置]**。
1. 单击&#x200B;**[!UICONTROL 保存]**&#x200B;以保存提交设置。

提交表单时，数据将保存在指定的Microsoft® Sharepoint文档库存储中。
用于保存数据的文件夹结构是 `/folder_name/form_name/year/month/date/submission_id/data`。

## 将自适应表单连接到Microsoft® SharePoint列表 {#connect-af-sharepoint-list}

>[!VIDEO](https://video.tv.adobe.com/v/3424820/connect-aem-adaptive-form-to-sharepointlist/?quality=12&learn=on)

要使用 [!UICONTROL 提交到SharePoint列表] 以自适应表单提交操作：

1. [创建SharePoint列表配置](#create-sharepoint-list-configuration)：用于将AEM Forms连接到Microsoft® Sharepoint List Storage。
1. [在自适应表单中使用表单数据模型(FDM)提交](#use-submit-using-fdm)：它将您的自适应表单连接到配置的Microsoft® SharePoint。

### 创建SharePoint列表配置 {#create-sharepoint-list-configuration}

要将AEM Forms连接到Microsoft®Sharepoint列表：

1. 转到 **[!UICONTROL 工具]** > **[!UICONTROL Cloud Service]** >  **[!UICONTROL Microsoft®SharePoint]**.
1. 选择&#x200B;**配置容器**。配置存储在选定的配置容器中。
1. 单击 **[!UICONTROL 创建]** > **[!UICONTROL SharePoint列表]** 下拉列表中。 这将显示 SharePoint 配置向导。
1. 指定&#x200B;**[!UICONTROL 标题]**、**[!UICONTROL 客户端 ID]**、**[!UICONTROL 客户端密码]**&#x200B;和 **[!UICONTROL OAuth URL]**。有关如何检索 OAuth URL 的客户端 ID、客户端密码、租户 ID 的信息，请参阅 [Microsoft® 文档](https://learn.microsoft.com/en-us/graph/auth-register-app-v2)。
   * 您可以从 Microsoft® Azure 门户检索应用程序的`Client ID` 和`Client Secret`。
   * 在 Microsoft® Azure 门户中，将重定向 URI 添加为 `https://[author-instance]/libs/cq/sharepointlist/content/configurations/wizard.html`。将 `[author-instance]` 替换为创作实例 URL。
   * 添加API权限 `offline_access` 和 `Sites.Manage.All` 在 **Microsoft® Graph** 选项卡以提供读/写权限。 添加 `AllSites.Manage` 中的权限 **Sharepoint** 选项卡，以与SharePoint数据远程交互。
   * 使用 OAuth URL：`https://login.microsoftonline.com/tenant-id/oauth2/v2.0/authorize`。将 `<tenant-id>` 替换为 Microsoft® Azure 门户中应用程序的 `tenant-id`。

     >[!NOTE]
     >
     > **客户端密码**&#x200B;字段是必填还是可选字段取决于 Azure Active Directory 应用程序配置。如果应用程序配置为使用客户端密码，则必须提供客户端密码。

1. 单击&#x200B;**[!UICONTROL 连接]**。连接成功后，将显示`Connection Successful`消息。
1. 选择 **[!UICONTROL SharePoint站点]** 和 **[!UICONTROL SharePoint列表]** 下拉列表中。
1. 选择 **[!UICONTROL 创建]** 创建Microsoft® SharePointList的云配置。


### 在自适应表单中使用表单数据模型(FDM)提交 {#use-submit-using-fdm}

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
