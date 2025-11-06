---
title: 如何为自适应Forms配置现成的Salesforce表单数据模型？
description: 了解如何将Salesforce与自适应Forms集成。
feature: Adaptive Forms, Form Data Model
role: User, Developer
exl-id: 184db05b-7237-4dce-8059-03c39b93d7d7
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 0%

---

# 为AEM Forms配置Salesforce {#configure-azure-storage}

[[!DNL Experience Manager Forms] 数据集成](data-integration.md)提供了[!DNL Salesforce]个云服务以将自适应Forms与OOTB表单数据模型(FDM)集成。 然后，自适应Forms可以与[!DNL Salesforce]服务器交互以启用业务工作流。 例如：

* 在提交自适应表单时将数据写入[!DNL Salesforce]。
* 通过表单数据模型(FDM)中定义的自定义实体在[!DNL Salesforce]中写入数据，反之亦然。
* 查询[!DNL Salesforce]服务器以获取数据并预填充Adaptive Forms。
* 从[!DNL Salesforce]服务器读取数据。

在您[!DNL Salesforce]为基于Experience Manager原型的Forms设置开发项目[!DNL AEM Forms]之后，[云服务和表单数据模型(FDM)在](setup-local-development-environment.md#forms-cloud-service-local-development-environment)服务器上开箱即用。

>[!NOTE]
>
>仅当您基于[!DNL Salesforce]AEM Archetype 30[!DNL Experience Manager Forms]或更高版本将[!DNL Cloud Service]设置为[项目时，](https://github.com/adobe/aem-project-archetype/releases/tag/aem-project-archetype-30)云服务和表单数据模型(FDM)才可开箱即用。

## 配置[!DNL Salesforce]云服务 {#configure-salesforce-cloud-service}

在配置[!DNL Salesforce]云服务之前，请确保您执行以下任务：

* [创建已启用连接的OAuth [!DNL Salesforce] 应用程序](https://help.salesforce.com/s/articleView?id=sf.connected_app_create_api_integration.htm&type=5)。 在创建连接的[!DNL Salesforce]应用程序时，请按以下格式指定回调URL：

  ```
  https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html
  ```

  其中服务器和端口指的是[!DNL AEM Forms]服务器的主机名和端口号。

* 在创建连接的[!DNL Salesforce]应用程序时，指定`full`和`offline_access`作为OAuth作用域的值。

* 记下所连接应用程序的客户端ID（称为使用者密钥）和客户端密钥（称为使用者密钥）的值。

执行以下步骤以配置[!DNL Salesforce]云服务：

1. 在[!DNL AEM Forms]创作实例上，导航到&#x200B;**[!UICONTROL 工具]** ![锤子](assets/hammer.png) > **[!UICONTROL 云服务]** > **[!UICONTROL 数据源]**。
2. 选择文件夹名称，选择&#x200B;**[!UICONTROL Salesforce云配置]**，然后选择&#x200B;**[!UICONTROL 属性]**。
3. 在&#x200B;**[!UICONTROL 身份验证设置]**&#x200B;选项卡中：
   1. 在[!DNL Salesforce]主机&#x200B;**[!UICONTROL 字段中指定]**&#x200B;域URL。 例如，[域名].my.salesforce.com。
   2. 为连接的应用程序指定客户端ID（称为使用者密钥）和客户端密码（称为使用者密码）。
   3. 在&#x200B;**授权范围**&#x200B;字段中指定`full`full offline_access`offine_access` （**[!UICONTROL 和]**&#x200B;值，用空格分隔）。
   4. 选择&#x200B;**[!UICONTROL 连接到OAuth]**。 您将被重定向到[!DNL Salesforce]登录页面。
   5. 使用您的[!DNL Salesforce]凭据登录并接受以允许云服务配置连接到[!DNL Salesforce]服务。 如果连接成功，您将被重定向到[!DNL Salesforce]云服务配置页面，该页面将显示一条成功消息。
4. 选择&#x200B;**[!UICONTROL 保存并关闭]**&#x200B;以完成配置设置。

### 访问现成的[!DNL Salesforce]表单数据模型(FDM)

在您[!DNL Salesforce]为基于Experience Manager原型的Forms设置开发项目[!DNL AEM Forms]之后，[表单数据模型(FDM)在](setup-local-development-environment.md#forms-cloud-service-local-development-environment)服务器上开箱即用。

要访问表单数据模型(FDM)，请执行以下操作：

1. 导航到&#x200B;**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL 数据集成]**。
1. 选择文件夹名称，选择&#x200B;**[!UICONTROL Salesforce数据模型]**，然后选择编辑![编辑](assets/edit.png)图标以查看表单数据模型(FDM)。

配置[[!DNL Salesforce] 云配置服务](#configure-salesforce-cloud-service)后，您可以将自适应表单与现成的[!DNL Salesforce]数据模型集成。

>[!MORELIKETHIS]
>
>* [为AEM Forms配置数据源](/help/forms/configure-data-sources.md)
>* [为AEM Forms配置Azure存储](/help/forms/configure-azure-storage.md)
>  [将Forms门户添加到AEM Sites页面](/help/forms/configure-forms-portal.md)
