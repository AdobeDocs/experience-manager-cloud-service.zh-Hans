---
title: 如何在提交自适应表单时将数据发送到SharePoint List存储区？
Description: Learn how to send data from your Adaptive Form to a SharePoint storage like a SharePoint list when you submit the form.
keywords: 如何为自适应表单连接SharePoint列表？ 、提交到SharePoint、创建SharePoint列表配置、在自适应表单中使用提交到SharePoint提交操作、将自适应表单连接到Microsoft&reg； SharePoint列表。
feature: Adaptive Forms, Core Components, Foundation Components, Edge Delivery Services
role: User, Developer
badgeSaas: label="AEM Forms" type="Positive" tooltip="适用于AEM Forms)。"
exl-id: 9ac3e7be-c6fa-4dbc-9aba-b81741ba6c55
source-git-commit: 0e5045b87719781301d91874c7355eda9426beef
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 22%

---

# 将自适应表单连接到® SharePoint列表 {#connect-af-sharepoint-list}

>[!VIDEO](https://video.tv.adobe.com/v/3424820/connect-aem-adaptive-form-to-sharepointlist/?quality=12&learn=on)

<span>此视频仅适用于核心组件。 对于UE/Foundation组件，请参阅文章。</span>

要在自适应表单中使用[!UICONTROL 提交到SharePoint列表]提交操作，请执行以下操作：

1. [创建SharePoint列表配置](#1-create-a-sharepoint-list-configuration)：它将AEM Forms连接到您的Microsoft® Sharepoint列表存储。
1. [在自适应表单中使用表单数据模型(FDM)提交](#2-use-the-submit-using-form-data-model-fdm-in-an-adaptive-form-use-submit-using-fdm)：它将您的自适应表单连接到配置的® SharePoint。

## &#x200B;1. 创建SharePoint列表配置

要将AEM Forms连接到Microsoft®Sharepoint列表：

1. 转到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL ® SharePoint]**。
1. 选择&#x200B;**配置容器**。 配置存储在选定的配置容器中。
1. 从下拉列表中单击&#x200B;**[!UICONTROL 创建]** > **[!UICONTROL SharePoint列表]**。 这将显示 SharePoint 配置向导。
1. 指定&#x200B;**[!UICONTROL 标题]**、**[!UICONTROL 客户端 ID]**、**[!UICONTROL 客户端密码]**&#x200B;和 **[!UICONTROL OAuth URL]**。 有关如何检索 OAuth URL 的客户端 ID、客户端密码、租户 ID 的信息，请参阅 [Microsoft® 文档](https://learn.microsoft.com/en-us/graph/auth-register-app-v2)。
   * 您可以从 Microsoft® Azure 门户检索应用程序的`Client ID` 和`Client Secret`。
   * 在 Microsoft® Azure 门户中，将重定向 URI 添加为 `https://[author-instance]/libs/cq/sharepointlist/content/configurations/wizard.html`。 将 `[author-instance]` 替换为创作实例 URL。
   * 在&#x200B;**® Graph**&#x200B;选项卡中添加API权限`offline_access`和`Sites.Manage.All`以提供读/写权限。 在&#x200B;**Sharepoint**&#x200B;选项卡中添加`AllSites.Manage`权限以与SharePoint数据进行远程交互。
   * 使用 OAuth URL：`https://login.microsoftonline.com/tenant-id/oauth2/v2.0/authorize`。 将 `<tenant-id>` 替换为 Microsoft® Azure 门户中应用程序的 `tenant-id`。

     >[!NOTE]
     >
     > **客户端密码**&#x200B;字段是必填还是可选字段取决于 Azure Active Directory 应用程序配置。 如果应用程序配置为使用客户端密码，则必须提供客户端密码。

1. 单击&#x200B;**[!UICONTROL 连接]**。 连接成功后，将显示`Connection Successful`消息。
1. 从下拉列表中选择&#x200B;**[!UICONTROL SharePoint站点]**&#x200B;和&#x200B;**[!UICONTROL SharePoint列表]**。
1. 选择&#x200B;**[!UICONTROL 创建]**&#x200B;以创建® SharePointList的云配置。

### 基于证书的身份验证 {#certificate-based-authentication}

SharePoint列表配置的基于证书的身份验证位于<span class="preview">早期采用者计划下。 您可以使用官方电子邮件 ID 写信给 aem-forms-ea@adobe.com，加入早期采用者计划并申请使用该功能。</span>

在SharePoint列表配置向导中：

1. 将&#x200B;**[!UICONTROL 身份验证类型]**&#x200B;设置为&#x200B;**基于证书的身份验证**。
1. 指定&#x200B;**[!UICONTROL 标题]**、**[!UICONTROL 客户端ID]**、**[!UICONTROL 证书别名]**、**[!UICONTROL 租户ID]**&#x200B;和&#x200B;**[!UICONTROL 租户名称]**。
1. 输入&#x200B;**[!UICONTROL SharePoint站点URL]**，根据需要验证站点连接，然后选择&#x200B;**[!UICONTROL SharePoint列表]**。
1. 单击&#x200B;**[!UICONTROL 连接]**&#x200B;以验证连接，然后单击&#x200B;**[!UICONTROL 保存并关闭]**&#x200B;以保存配置。

以下屏幕截图显示了具有&#x200B;**基于证书的身份验证**&#x200B;的SharePoint列表配置：

![SharePoint列表配置具有基于证书的身份验证](/help/forms/assets/sharepoint-list-certificate-auth-configuration.png){width=50%, height=50%, align=center}

要为AEM和Microsoft Azure准备证书，请在AEM中执行以下步骤，然后在Microsoft Azure中注册公共证书。

在AEM中&#x200B;****

1. 转到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 安全性]** > **[!UICONTROL 用户]**。
1. 搜索&#x200B;**[!UICONTROL fd-cloudservice]**，选择用户，然后单击&#x200B;**[!UICONTROL 属性]**。
1. 打开&#x200B;**[!UICONTROL 密钥库]**&#x200B;选项卡。 如果尚未创建密钥库，请单击&#x200B;**[!UICONTROL 创建密钥库]**，并完成提示以设置密钥库密码。
1. 将私钥添加到密钥库：展开&#x200B;**[!UICONTROL 从Keystore文件添加私钥]**&#x200B;并上传&#x200B;**.jks**&#x200B;文件。
1. 输入与SharePoint列表配置中的&#x200B;**[!UICONTROL 证书别名]**&#x200B;匹配的&#x200B;**[!UICONTROL 别名]**，提交密钥资料，然后单击&#x200B;**[!UICONTROL 保存并关闭]**。

屏幕快照会在添加证书后显示密钥库。 **[!UICONTROL 别名]**&#x200B;必须与SharePoint List云配置中的&#x200B;**[!UICONTROL 证书别名]**&#x200B;匹配：

具有证书别名](/help/forms/assets/fd-cloudservice-keystore-certificate.png){width=50%, height=50%, align=center}的![fd-cloudservice用户密钥库

在Microsoft Azure中&#x200B;****

1. 打开应用程序注册，然后转到&#x200B;**证书和密钥** > **证书**。
1. 选择&#x200B;**上载证书**&#x200B;并上载Azure必须信任该应用程序的证书文件（公钥）。

屏幕快照显示Azure门户中的&#x200B;**证书**&#x200B;选项卡，您可以在其中上传用于应用程序注册的证书：

![Azure应用程序注册证书和密钥](/help/forms/assets/azure-app-registration-sharepoint-certificates.png){width=50%, height=50%, align=center}

## &#x200B;2. 在自适应表单中使用表单数据模型(FDM)提交 {#use-submit-using-fdm}

您可以在自适应表单中使用创建的SharePoint列表配置，以在SharePoint列表中保存数据或生成的记录文档。 执行以下步骤以在自适应表单中使用SharePoint列表：

1. [使用® SharePoint列表配置创建表单数据模型(FDM)](/help/forms/create-form-data-models.md)
1. [配置表单数据模型(FDM)以检索和发送数据](/help/forms/work-with-form-data-model.md#configure-services)
1. [创建自适应表单](/help/forms/creating-adaptive-form-core-components.md)
1. [使用表单数据模型(FDM)配置提交操作](/help/forms/using-form-data-model.md)

提交表单时，数据将保存在指定的® Sharepoint列表存储中。

>[!NOTE]
>
> 在® SharePoint List中，不支持以下列类型：
>
> * 图像列
> * 元数据列
> * 人员列
> * 外部数据列

## 相关文章

{{af-submit-action}}
