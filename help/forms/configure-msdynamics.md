---
title: 如何为自适应Forms配置现成的Microsoft Dynamics 365表单数据模型？
description: 了解如何将Microsoft Dynamics 365与自适应Forms集成。
feature: Adaptive Forms, Form Data Model
role: User, Developer
source-git-commit: fadbe44e0dba4e7dcbad230c286d6126e68910bc
workflow-type: tm+mt
source-wordcount: '915'
ht-degree: 2%

---


# 配置Microsoft® Dynamics 365 for AEM Forms

Adobe Experience Manager Forms数据集成提供了云服务配置，以便将表单与Microsoft Dynamics服务器集成。 它使您能够根据在Microsoft Dynamics服务中定义的实体、属性和服务来创建表单数据模型(FDM)。 表单数据模型(FDM)可用于创建与Microsoft Dynamics服务器交互以启用业务工作流程的Adaptive Forms。 例如：
* 查询Microsoft Dynamics服务器以获取数据并预填充Adaptive Forms。
* 在提交自适应表单时将数据写入Microsoft Dynamics。
* 通过表单数据模型(FDM)中定义的自定义实体在Microsoft Dynamics中写入数据。

AEM as a Cloud Service提供了多种现成的提交操作来处理表单提交。 您可以在[自适应表单提交操作](/help/forms/configure-submit-actions-core-components.md)文章中了解有关这些选项的更多信息。

<!-- 
[[!DNL Experience Manager Forms] Data Integration](data-integration.md) provides [!DNL Microsoft&reg; Dynamics 365] Cloud Services to integrate Adaptive Forms with out of the box Form Data Model (FDM). The Adaptive Forms can then interact with [!DNL Microsoft&reg; Dynamics 365] servers to enable business workflows. For example:

* Write data into [!DNL Microsoft&reg; Dynamics 365] on Adaptive Form submission.
* Write data in [!DNL Microsoft&reg; Dynamics 365] through custom entities defined in Form Data Model (FDM) and conversely.
* Query [!DNL Microsoft&reg; Dynamics 365]server for data and prepopulate Adaptive Forms.
* Read data from [!DNL Microsoft&reg; Dynamics 365] server.

[!DNL Microsoft&reg; Dynamics 365] cloud services and Form Data Model (FDM) are available out of the box on the [!DNL AEM Forms] Server after you [set up a development project for Forms based on Experience Manager archetype](setup-local-development-environment.md#forms-cloud-service-local-development-environment).

>[!NOTE]
>
>Microsoft&reg; Dynamics 365 cloud services and Form Data Model (FDM) are available out of the box only if you set up an [!DNL Experience Manager Forms] as a [!DNL Cloud Service] project based on [AEM Archetype 30](https://github.com/adobe/aem-project-archetype/releases/tag/aem-project-archetype-30) or later.-->

## 先决条件

将[!DNL Microsoft® Dynamics 365]与AEM Forms as a Cloud Service集成之前，请确保已执行以下步骤：


1. **在Microsoft Dynamics 365中设置帐户**

   按照视频中介绍的步骤设置Microsoft Dynamics 365帐户。 在此视频中，创建试用帐户是为了演示。

   >[!VIDEO](https://video.tv.adobe.com/v/3444389/)

1. **在Power Platform管理中心中创建帐户**
在**Power Platform管理中心**&#x200B;中创建帐户以：
   * 添加Dataverse
   * 启用Microsoft Dynamics 365应用程序

   按照视频中的步骤在Power Platform管理中心中创建帐户。 在此视频中，创建了一个试用帐户用于演示。
   >[!VIDEO](https://video.tv.adobe.com/v/3444388)

1. **在Azure Active Directory中为[!DNL Microsoft® Dynamics 365]注册应用程序**

   按照视频中的步骤在Azure Active Directory中注册[!DNL Microsoft® Dynamics 365]的应用程序。

   >[!VIDEO](https://video.tv.adobe.com/v/3444369/dynamics365integration-microsoftdynamics-apiaccess-azuread-appregistration)

   >[!NOTE]
   >
   > * 要创建连接的[!DNL Microsoft® Dynamics 365]应用程序，请选择&#x200B;**Web**&#x200B;作为平台，并以下列格式指定&#x200B;**重定向URI**： `https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/fdm.html`。
   > * 请确保保存客户端ID（也称为应用程序ID）和客户端密钥以供将来参考。

## 将Forms连接到Microsoft® Dynamics 365

配置上述先决条件后，您可以继续将自适应Forms与Microsoft® Dynamics 365集成。 要在提交表单时将数据发送到Microsoft® Dynamics 365，请执行以下步骤：

[1. 配置Microsoft Dynamics](#1-configure-cloud-service-configuration-for-microsoft-dynamics)的云服务配置
[2。 创建表单数据模型(FDM)](#2-create-form-data-model-fdm)

### 1.配置Microsoft Dynamics的云服务配置

>[!VIDEO](https://video.tv.adobe.com/v/3444370/cloudconfiguration-dataintegration-adobeexperiencemanager-aemforms-microsoftdynamics)

执行以下步骤以配置[!DNL Microsoft® Dynamics 365]云服务配置：

1. 导航到[!DNL AEM Forms]创作实例上的&#x200B;**[!UICONTROL 工具]** ![锤子](assets/hammer.png) > **[!UICONTROL 云服务]** > **[!UICONTROL 数据源]**。

   ![选择云数据Source](/help/forms/assets/dynamics-data-source.png)
1. 选择配置容器。 配置存储在选定的配置容器中。
1. 单击&#x200B;**[!UICONTROL 创建]**。

   ![创建云配置](/help/forms/assets/dynamics-select-configuration.png)

   出现&#x200B;**创建数据Source配置**&#x200B;配置向导。

   ![创建数据Source配置向导](/help/forms/assets/dynamics-create-data-configuration.png)

1. 指定&#x200B;**[!UICONTROL Title]**、**[!UICONTROL Name]**&#x200B;并选择&#x200B;**[!UICONTROL 服务类型]**&#x200B;作为&#x200B;**OData服务**。
1. 单击&#x200B;**[!UICONTROL “下一个”。]**&#x200B;出现&#x200B;**身份验证**&#x200B;选项卡。

   ![身份验证选项卡](/help/forms/assets/dynamics-authentication-tab.png)

1. 指定&#x200B;**[!UICONTROL 服务根]**&#x200B;字段的值。

   转到&#x200B;**Power Platform管理中心**&#x200B;中的Dynamics实例，然后导航到[开发人员资源](https://docs.microsoft.com/en-us/powerapps/developer/data-platform/view-download-developer-resources)以查看&#x200B;**服务根**&#x200B;的值。 **Web API终结点**&#x200B;表示要与自适应Forms集成的Dynamics实例的&#x200B;**服务根**&#x200B;值。 **服务根** URL的格式如下： `https://<tenant-name>.dynamics.com/api/data/v9.1/`

   ![服务根字段](/help/forms/assets/dynamics-service-root.png)

1. 选择&#x200B;**[!UICONTROL 身份验证类型]**&#x200B;作为&#x200B;**OAuth2.0**。
1. 为连接的应用程序指定&#x200B;**客户端ID** （称为应用程序ID）和&#x200B;**客户端密钥**。
您可以从Azure Active Directory应用程序中检索**客户端ID**&#x200B;和&#x200B;**客户端密钥**。

   ![客户端ID和客户端密钥](/help/forms/assets/dynamics-azure-app-resgistration.png)

1. 在&#x200B;**[!UICONTROL OAuth URL]**、**[!UICONTROL 刷新令牌URL]**&#x200B;和&#x200B;**[!UICONTROL 访问令牌URL]**字段中指定以下内容。
您可以从Azure Active Directory应用程序的**端点**&#x200B;部分中检索&#x200B;**[!UICONTROL OAuth URL]**、**[!UICONTROL 刷新令牌URL]**&#x200B;和&#x200B;**[!UICONTROL 访问令牌URL]**。

   ![Azure应用终结点](/help/forms/assets/dynamics-azure-app-endpoints.png)

1. 在[!DNL Microsoft® Dynamics 365]上授权进程的&#x200B;**[!UICONTROL 授权范围]**&#x200B;字段中指定`openid`。
1. 在&#x200B;**[!UICONTROL 资源]**&#x200B;字段中指定动态实例URL以使用表单数据模型(FDM)配置[!DNL Microsoft® Dynamics 365]。
您可以从**Power Platform管理中心**&#x200B;复制&#x200B;**环境URL**&#x200B;或使用&#x200B;**服务根** URL派生Dynamics实例URL。 资源URL的格式如下： `https://<tenant-name>.dynamics.com`。

   ![电源应用资源字段](/help/forms/assets/dynamics-resource-field.png)

1. 使用您的[!DNL Microsoft® Dynamics 365]凭据登录并接受以允许云服务配置连接到[!DNL Microsoft® Dynamics 365]服务。 如果连接成功，您将被重定向到[!DNL Microsoft® Dynamics 365]云服务配置页面，该页面将显示一条成功消息。
1. 选择&#x200B;**[!UICONTROL 创建]**&#x200B;以保存配置。

### 2.创建表单数据模型(FDM)

>[!VIDEO](https://video.tv.adobe.com/v/3444367/aemforms-adobeexperiencemanager-formdatamodel--dataintegration-digitalforms)

您可以使用创建的[!DNL Microsoft® Dynamics 365]云配置来创建表单数据模型(FDM)。 执行以下步骤以创建表单数据模型：

1. 导航到&#x200B;**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL 数据集成]**。
   ![创建表单数据模型](/help/forms/assets/dynamics-create-fdm.png)

1. 单击&#x200B;**[!UICONTROL 创建]**&#x200B;并选择&#x200B;**[!UICONTROL 表单数据模型]**。
   ![选择表单数据模型](/help/forms/assets/dynamics-select-fdm.png)

   出现&#x200B;**创建表单数据模型**&#x200B;向导。
1. 单击&#x200B;**[!UICONTROL 下一步]**。
1. 从&#x200B;**选择数据源**选项卡中选择创建的云配置。
   ![选择云配置](/help/forms/assets/dynamics-select-cloud-config.png)

1. 单击编辑![编辑](assets/edit.png)图标以查看和配置表单数据模型(FDM)。

接下来，您可以[配置表单数据模型(FDM)](/help/forms/work-with-form-data-model.md#configure-services)并将其用于各种自适应表单用例，例如：

* 通过查询[!DNL Microsoft Dynamics]实体和服务中的信息来预填充自适应表单
* 使用自适应表单规则调用在表单数据模型(FDM)中定义的[!DNL Microsoft Dynamics]服务器操作
* 将提交的表单数据写入[!DNL Microsoft Dynamics]实体
* 您可以为自适应表单配置表单数据模型提交操作以将数据发送到[!DNL Microsoft Dynamics]。

然后，您可以在&#x200B;**自适应表单**&#x200B;中使用[使用表单数据模型(FDM)](/help/forms/using-form-data-model.md)提交选项将数据从表单传输到配置的[!DNL Microsoft® Dynamics 365]。


>[!MORELIKETHIS]
>
>* [为AEM Forms配置数据源](/help/forms/configure-data-sources.md)
>* [为AEM Forms配置Azure存储](/help/forms/configure-azure-storage.md)
>  [将Forms门户添加到AEM Sites页面](/help/forms/configure-forms-portal.md)