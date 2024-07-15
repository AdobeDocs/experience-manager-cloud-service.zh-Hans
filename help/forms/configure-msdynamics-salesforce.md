---
title: 如何为自适应Forms配置现成的Microsoft Dynamics 365和Salesforce表单数据模型？
description: 了解如何将Microsoft Dynamics 365和Salesforce与自适应Forms集成。
feature: Adaptive Forms, Form Data Model
role: User, Developer
exl-id: 2a43b2db-2dfb-4c79-88be-ea770b44dac1
source-git-commit: 7b31a2ea016567979288c7a8e55ed5bf8dfc181d
workflow-type: tm+mt
source-wordcount: '965'
ht-degree: 2%

---

# 配置Microsoft® Dynamics 365或Salesforce for AEM Forms {#configure-azure-storage}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/oauth2-client-credentials-flow-for-server-to-server-integration.html) |
| AEM as a Cloud Service | 本文 |

[[!DNL Experience Manager Forms] 数据集成](data-integration.md)提供[!DNL Microsoft® Dynamics 365]和[!DNL Salesforce]云服务以将自适应表单与现成的表单数据模型(FDM)集成。 然后，自适应Forms可以与[!DNL Microsoft® Dynamics 365]和[!DNL Salesforce]服务器交互以启用业务工作流。 例如：

* 在提交自适应表单时将数据写入[!DNL Microsoft® Dynamics 365]和[!DNL Salesforce]。
* 通过表单数据模型(FDM)中定义的自定义实体在[!DNL Microsoft® Dynamics 365]和[!DNL Salesforce]中写入数据，反之亦然。
* 查询[!DNL Microsoft® Dynamics 365]和[!DNL Salesforce]服务器以获取数据并预填充Adaptive Forms。
* 从[!DNL Microsoft® Dynamics 365]和[!DNL Salesforce]服务器读取数据。

在您[基于Experience Manager原型](setup-local-development-environment.md#forms-cloud-service-local-development-environment)为Forms设置开发项目后，[!DNL Microsoft® Dynamics 365]和[!DNL Salesforce]云服务和表单数据模型(FDM)在[!DNL AEM Forms]服务器上开箱即用。

>[!NOTE]
>
>仅当您基于[AEM Archetype 30](https://github.com/adobe/aem-project-archetype/releases/tag/aem-project-archetype-30)或更高版本将[!DNL Experience Manager Forms]设置为[!DNL Cloud Service]项目时，Microsoft® Dynamics 365和[!DNL Salesforce]云服务和表单数据模型(FDM)才可开箱即用。

## 配置[!DNL Salesforce]云服务 {#configure-salesforce-cloud-service}

在配置[!DNL Salesforce]云服务之前，请确保您执行以下任务：

* [创建已启用连接的OAuth [!DNL Salesforce] 应用程序](https://help.salesforce.com/s/articleView?id=sf.connected_app_create_api_integration.htm&amp;type=5)。 在创建连接的[!DNL Salesforce]应用程序时，请按以下格式指定回调URL：

  ```
  https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html
  ```

  其中服务器和端口指的是[!DNL AEM Forms]服务器的主机名和端口号。

* 在创建连接的[!DNL Salesforce]应用程序时，指定`full`和`offline_access`作为OAuth作用域的值。

* 记下所连接应用程序的客户端ID（称为使用者密钥）和客户端密钥（称为使用者密钥）的值。

执行以下步骤以配置[!DNL Salesforce]云服务：

1. 在[!DNL AEM Forms]创作实例上，导航到&#x200B;**[!UICONTROL 工具]** ![锤子](assets/hammer.png) > **[!UICONTROL Cloud Service]** > **[!UICONTROL 数据源]**。 可用包装文件夹的列表包括一个具有在[生成AEM原型项目](setup-local-development-environment.md#forms-cloud-service-local-development-environment)时为`DappTitle`指定的标题的文件夹。
1. 选择文件夹名称，选择&#x200B;**[!UICONTROL Salesforce云配置]**，然后选择&#x200B;**[!UICONTROL 属性]**。
1. 在&#x200B;**[!UICONTROL 身份验证设置]**&#x200B;选项卡中：
   1. 在&#x200B;**[!UICONTROL 主机]**&#x200B;字段中指定[!DNL Salesforce]域URL。 例如，[域名].my.salesforce.com。
   1. 为连接的应用程序指定客户端ID（称为使用者密钥）和客户端密码（称为使用者密码）。
   1. 在&#x200B;**[!UICONTROL 授权范围]**&#x200B;字段中指定&#x200B;**full offline_access** （`full`和`offine_access`值，用空格分隔）。
   1. 选择&#x200B;**[!UICONTROL 连接到OAuth]**。 您将被重定向到[!DNL Microsoft® Dynamics]登录页面。
   1. 使用您的[!DNL Salesforce]凭据登录并接受以允许云服务配置连接到[!DNL Salesforce]服务。 如果连接成功，您将被重定向到[!DNL Salesforce]云服务配置页面，该页面将显示一条成功消息。
1. 选择&#x200B;**[!UICONTROL 保存并关闭]**&#x200B;以完成配置设置。

### 访问现成的[!DNL Salesforce]表单数据模型(FDM)

在您[根据Experience Manager原型](setup-local-development-environment.md#forms-cloud-service-local-development-environment)为Forms设置开发项目后，[!DNL Salesforce]表单数据模型(FDM)在[!DNL AEM Forms]服务器上开箱即用。

要访问表单数据模型(FDM)，请导航到&#x200B;**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL 数据集成]**。 可用文件夹的列表包括在[生成AEM原型项目](setup-local-development-environment.md#forms-cloud-service-local-development-environment)时为`DappTitle`指定标题的文件夹。 选择文件夹名称，选择&#x200B;**[!UICONTROL Salesforce数据模型]**，然后选择“编辑![编辑](assets/edit.png)”图标以查看表单数据模型(FDM)。

配置[[!DNL Salesforce] 云配置服务](#configure-salesforce-cloud-service)后，您可以将自适应表单与现成的[!DNL Salesforce]数据模型集成。

## 配置[!DNL Microsoft® Dynamics 365]云服务 {#configure-dynamics-cloud-service}

在配置[!DNL Microsoft® Dynamics 365]云服务之前，请确保您执行以下任务：

* [在Azure Active Directory](https://docs.microsoft.com/en-us/powerapps/developer/data-platform/walkthrough-register-app-azure-active-directory)中注册 [!DNL Microsoft® Dynamics 365] 的应用程序。 在创建连接的[!DNL Microsoft® Dynamics 365]应用程序时，请按照以下格式指定回复URL：

  ```
  https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html
  ```

  其中服务器和端口指的是[!DNL AEM Forms]服务器的主机名和端口号。

* 记下所连接应用程序的客户端ID（也称为应用程序ID）和客户端密钥的值。

执行以下步骤以配置[!DNL Microsoft® Dynamics 365]云服务：

1. 在[!DNL AEM Forms]创作实例上，导航到&#x200B;**[!UICONTROL 工具]** ![锤子](assets/hammer.png) > **[!UICONTROL Cloud Service]** > **[!UICONTROL 数据源]**。 可用包装文件夹的列表包括一个具有在[生成AEM原型项目](setup-local-development-environment.md#forms-cloud-service-local-development-environment)时为`DappTitle`指定的标题的文件夹。
1. 选择文件夹名称，选择&#x200B;**[!UICONTROL Microsoft® Dynamics 365云配置]**，然后选择&#x200B;**[!UICONTROL 属性]**。
1. 在&#x200B;**[!UICONTROL 身份验证设置]**&#x200B;选项卡中：
   1. 输入&#x200B;**[!UICONTROL 服务根]**&#x200B;字段的值。 转到Dynamics实例并导航到[开发人员资源](https://docs.microsoft.com/en-us/powerapps/developer/data-platform/view-download-developer-resources)，以查看服务根字段的值。 例如，`https://<tenant-name>.dynamics.com/api/data/v9.1/`
   1. 为连接的应用程序指定客户端ID（称为应用程序ID）和客户端密码。
   1. 将`{tenant}`替换为&#x200B;**[!UICONTROL OAuth URL]**、**[!UICONTROL 刷新令牌URL]**&#x200B;和&#x200B;**[!UICONTROL 访问令牌URL]**&#x200B;字段中的租户ID。
   1. 在&#x200B;**[!UICONTROL 资源]**&#x200B;字段中指定Dynamics实例URL以使用表单数据模型(FDM)配置[!UICONTROL Microsoft® Dynamics]。 使用服务根URL来派生动态实例URL。 例如：`https://<tenant-name>.dynamics.com`。

   1. 在[!DNL Microsoft® Dynamics 365]上授权进程的&#x200B;**[!UICONTROL 授权范围]**&#x200B;字段中指定`openid`。
   1. 使用您的[!DNL Microsoft® Dynamics 365]凭据登录并接受以允许云服务配置连接到[!DNL Microsoft® Dynamics 365]服务。 如果连接成功，您将被重定向到[!DNL Microsoft® Dynamics 365]云服务配置页面，该页面将显示一条成功消息。
1. 选择&#x200B;**[!UICONTROL 保存并关闭]**&#x200B;以完成配置设置。

### 访问现成的[!DNL Microsoft® Dynamics 365]表单数据模型(FDM)

在您[根据Experience Manager原型](setup-local-development-environment.md##forms-cloud-service-local-development-environment)为Forms设置开发项目后，[!DNL Microsoft® Dynamics 365]表单数据模型(FDM)在[!DNL AEM Forms]服务器上开箱即用。

要访问表单数据模型(FDM)，请导航到&#x200B;**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL 数据集成]**。 可用文件夹的列表包括在[生成AEM原型项目](setup-local-development-environment.md#forms-cloud-service-local-development-environment)时为`DappTitle`指定标题的文件夹。 选择文件夹名称，选择&#x200B;**[!UICONTROL Microsoft® Dynamics 365数据模型]**，然后选择编辑![编辑](assets/edit.png)图标以查看表单数据模型(FDM)。

配置[[!DNL Microsoft® Dynamics 365] 云配置服务](#configure-dynamics-cloud-service)后，您可以将自适应表单与现成的[!DNL Microsoft® Dynamics 365]数据模型集成。

>[!MORELIKETHIS]
>
>* [为AEM Forms配置数据源](/help/forms/configure-data-sources.md)
>* [为AEM Forms配置Azure存储](/help/forms/configure-azure-storage.md)
>  [将Forms门户添加到AEM Sites页面](/help/forms/configure-forms-portal.md)
