---
title: 配置Microsoft&reg； Dynamics 365或Salesforce for AEM Forms
description: 了解如何将Microsoft&reg； Dynamics 365和Salesforce与自适应表单集成。
source-git-commit: 483a72f67f361023ebeefa3d74ec9f35a5f4f765
workflow-type: tm+mt
source-wordcount: '955'
ht-degree: 3%

---

# 配置Microsoft® Dynamics 365或Salesforce for AEM Forms {#configure-azure-storage}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/oauth2-client-credentials-flow-for-server-to-server-integration.html) |
| AEM as a Cloud Service | 本文 |

[[!DNL Experience Manager Forms] 数据集成](data-integration.md) 提供 [!DNL Microsoft® Dynamics 365] 和 [!DNL Salesforce] cloud services ，用于将自适应表单与现成的表单数据模型集成。 然后，自适应Forms可以与进行交互 [!DNL Microsoft® Dynamics 365] 和 [!DNL Salesforce] 启用业务工作流的服务器。 例如：

* 将数据写入 [!DNL Microsoft® Dynamics 365] 和 [!DNL Salesforce] 在提交自适应表单时。
* 将数据写入 [!DNL Microsoft® Dynamics 365] 和 [!DNL Salesforce] 通过表单数据模型中定义的自定义实体，反之亦然。
* 查询 [!DNL Microsoft® Dynamics 365] 和 [!DNL Salesforce] 数据服务器并预填充Adaptive Forms。
* 从读取数据 [!DNL Microsoft® Dynamics 365] 和 [!DNL Salesforce] 服务器。

[!DNL Microsoft® Dynamics 365] 和 [!DNL Salesforce] 云服务和表单数据模型可在以下位置立即使用： [!DNL AEM Forms] 您之后的服务器 [为基于Experience Manager原型的Forms设置开发项目](setup-local-development-environment.md#forms-cloud-service-local-development-environment).

>[!NOTE]
>
>Microsoft® Dynamics 365和 [!DNL Salesforce] 云服务和表单数据模型仅在您设置的情况下才可开箱即用 [!DNL Experience Manager Forms] as a [!DNL Cloud Service] 项目基于 [AEM原型30](https://github.com/adobe/aem-project-archetype/releases/tag/aem-project-archetype-30) 或更高版本。

## 配置 [!DNL Salesforce] 云服务 {#configure-salesforce-cloud-service}

配置之前 [!DNL Salesforce] cloud services，请确保您执行以下任务：

* [创建连接的启用OAuth的 [!DNL Salesforce] 应用程序](https://help.salesforce.com/s/articleView?id=sf.connected_app_create_api_integration.htm&amp;type=5). 在创建连接的 [!DNL Salesforce] 应用程序中，以下列格式指定回调URL：

  ```
  https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html
  ```

  其中服务器和端口指主机名和端口号， [!DNL AEM Forms] 服务器。

* 创建连接的时 [!DNL Salesforce] 应用程序，指定 `full` 和 `offline_access` 作为OAuth范围的值。

* 记下所连接应用程序的客户端ID（称为使用者密钥）和客户端密钥（称为使用者密钥）的值。

执行以下步骤来配置 [!DNL Salesforce] 云服务：

1. 开启 [!DNL AEM Forms] 创作实例，导航到 **[!UICONTROL 工具]** ![锤子](assets/hammer.png) > **[!UICONTROL Cloud Service]** > **[!UICONTROL 数据源]**. 可用包装文件夹的列表包括一个具有为指定的标题的文件夹 `DappTitle`  同时 [生成AEM原型项目](setup-local-development-environment.md#forms-cloud-service-local-development-environment).
1. 点按文件夹名称，选择 **[!UICONTROL Salesforce云配置]**，然后点击 **[!UICONTROL 属性]**.
1. 在 **[!UICONTROL 身份验证设置]** 选项卡：
   1. 指定 [!DNL Salesforce] 中的域URL **[!UICONTROL 主机]** 字段。 例如， [域名].my.salesforce.com.
   1. 为连接的应用程序指定客户端ID（称为使用者密钥）和客户端密码（称为使用者密码）。
   1. 指定 **完全脱机访问** (`full` 和 `offine_access` 值（以空格分隔） **[!UICONTROL 授权范围]** 字段。
   1. 点按 **[!UICONTROL 连接到OAuth]**. 您将被重定向到 [!DNL Microsoft® Dynamics] 登录页面。
   1. 使用您的登录 [!DNL Salesforce] 凭据并接受以允许云服务配置连接到 [!DNL Salesforce] 服务。 如果连接成功，您将被重定向至 [!DNL Salesforce] 云服务配置页面，其中显示成功消息。
1. 点按 **[!UICONTROL 保存并关闭]** 以完成配置设置。

### 开箱即用 [!DNL Salesforce] 表单数据模型

A [!DNL Salesforce] 表单数据模型可在 [!DNL AEM Forms] 您之后的服务器 [为基于Experience Manager原型的Forms设置开发项目](setup-local-development-environment.md#forms-cloud-service-local-development-environment).

要访问表单数据模型，请导航至 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL 数据集成]**. 可用文件夹的列表包括一个具有为指定的标题的文件夹 `DappTitle`  同时 [生成AEM原型项目](setup-local-development-environment.md#forms-cloud-service-local-development-environment). 点按文件夹名称，选择 **[!UICONTROL Salesforce数据模型]**，然后点按编辑 ![编辑](assets/edit.png) 图标以查看表单数据模型。

配置之后 [[!DNL Salesforce] 云配置服务](#configure-salesforce-cloud-service)，您可以将自适应表单与开箱即用的集成 [!DNL Salesforce] 数据模型。

## 配置 [!DNL Microsoft® Dynamics 365] 云服务 {#configure-dynamics-cloud-service}

配置之前 [!DNL Microsoft® Dynamics 365] cloud service，请确保您执行以下任务：

* [注册应用程序 [!DNL Microsoft® Dynamics 365] 使用Azure Active Directory](https://docs.microsoft.com/en-us/powerapps/developer/data-platform/walkthrough-register-app-azure-active-directory). 在创建连接的 [!DNL Microsoft® Dynamics 365] 应用程序，请按照以下格式指定回复URL：

  ```
  https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html
  ```

  其中服务器和端口指主机名和端口号， [!DNL AEM Forms] 服务器。

* 记下所连接应用程序的客户端ID（也称为应用程序ID）和客户端密钥的值。

执行以下步骤来配置 [!DNL Microsoft® Dynamics 365] 云服务：

1. 开启 [!DNL AEM Forms] 创作实例，导航到 **[!UICONTROL 工具]** ![锤子](assets/hammer.png) > **[!UICONTROL Cloud Service]** > **[!UICONTROL 数据源]**. 可用包装文件夹的列表包括一个具有为指定的标题的文件夹 `DappTitle`  同时 [生成AEM原型项目](setup-local-development-environment.md#forms-cloud-service-local-development-environment).
1. 点按文件夹名称，选择 **[!UICONTROL Microsoft® Dynamics 365云配置]**，然后点击 **[!UICONTROL 属性]**.
1. 在 **[!UICONTROL 身份验证设置]** 选项卡：
   1. 输入值 **[!UICONTROL 服务根]** 字段。 转到Dynamics实例并导航到 [开发人员资源](https://docs.microsoft.com/en-us/powerapps/developer/data-platform/view-download-developer-resources) 查看“服务根”字段的值。 例如，`https://<tenant-name>.dynamics.com/api/data/v9.1/`
   1. 为连接的应用程序指定客户端ID（称为应用程序ID）和客户端密码。
   1. 替换 `{tenant}` 具有租户ID **[!UICONTROL OAuth URL]**， **[!UICONTROL 刷新令牌URL]**、和 **[!UICONTROL 访问令牌URL]** 字段。
   1. 在中指定动态实例URL **[!UICONTROL 资源]** 要配置的字段 [!UICONTROL Microsoft® Dynamics] 表单数据模型。 使用服务根URL来派生动态实例URL。 例如：`https://<tenant-name>.dynamics.com`。

   1. 指定 `openid` 在 **[!UICONTROL 授权范围]** 授权流程的字段 [!DNL Microsoft® Dynamics 365].
   1. 使用您的登录 [!DNL Microsoft® Dynamics 365] 凭据并接受以允许云服务配置连接到 [!DNL Microsoft® Dynamics 365] 服务。 如果连接成功，您将被重定向至 [!DNL Microsoft® Dynamics 365] 云服务配置页面，其中显示成功消息。
1. 点按 **[!UICONTROL 保存并关闭]** 以完成配置设置。

### 开箱即用 [!DNL Microsoft® Dynamics 365] 表单数据模型

A [!DNL Microsoft® Dynamics 365] 表单数据模型可在 [!DNL AEM Forms] 您之后的服务器 [为基于Experience Manager原型的Forms设置开发项目](setup-local-development-environment.md##forms-cloud-service-local-development-environment).

要访问表单数据模型，请导航至 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL 数据集成]**. 可用文件夹的列表包括一个具有为指定的标题的文件夹 `DappTitle`  同时 [生成AEM原型项目](setup-local-development-environment.md#forms-cloud-service-local-development-environment). 点按文件夹名称，选择 **[!UICONTROL Microsoft® Dynamics 365数据模型]**，然后点按编辑 ![编辑](assets/edit.png) 图标以查看表单数据模型。

配置之后 [[!DNL Microsoft® Dynamics 365] 云配置服务](#configure-dynamics-cloud-service)，您可以将自适应表单与开箱即用的集成 [!DNL Microsoft® Dynamics 365] 数据模型。
