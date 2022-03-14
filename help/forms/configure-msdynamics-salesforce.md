---
title: 如何为自适应表单配置Microsoft Dynamics 365和Salesforce即装即用的表单数据模型？
description: 了解如何将Microsoft Dynamics 365和Salesforce与自适应表单相集成。
exl-id: 2a43b2db-2dfb-4c79-88be-ea770b44dac1
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '936'
ht-degree: 1%

---

# 配置[!DNL Microsoft Dynamics 365]和[!DNL Salesforce]云服务 {#configure-azure-storage}

[[!DNL Experience Manager Forms] 数据集成](data-integration.md) 提供 [!DNL Microsoft Dynamics 365] 和 [!DNL Salesforce] 云服务，将自适应表单与开箱即用的表单数据模型相集成。 随后，自适应Forms可以与 [!DNL Microsoft Dynamics 365] 和 [!DNL Salesforce] 服务器启用业务工作流。 例如：

* 将数据写入 [!DNL Microsoft Dynamics 365] 和 [!DNL Salesforce] 在自适应表单提交时。
* 将数据写入 [!DNL Microsoft Dynamics 365] 和 [!DNL Salesforce] 通过在表单数据模型中定义的自定义实体，反之亦然。
* 查询 [!DNL Microsoft Dynamics 365] 和 [!DNL Salesforce] 服务器，并预填充自适应Forms。
* 从读取数据 [!DNL Microsoft Dynamics 365] 和 [!DNL Salesforce] 服务器。

[!DNL Microsoft Dynamics 365] 和 [!DNL Salesforce] 云服务和表单数据模型开箱即用 [!DNL AEM Forms] 服务器 [基于Experience Manager原型的Forms开发项目](setup-local-development-environment.md##forms-cloud-service-local-development-environment).

>[!NOTE]
>
>Microsoft Dynamics 365和 [!DNL Salesforce] 云服务和表单数据模型仅在您设置 [!DNL Experience Manager Forms] as a [!DNL Cloud Service] 项目基于 [AEM原型30](https://github.com/adobe/aem-project-archetype/releases/tag/aem-project-archetype-30) 或更晚。

## 配置 [!DNL Salesforce] 云服务 {#configure-salesforce-cloud-service}

在配置 [!DNL Salesforce] 云服务，请确保您执行以下任务：

* [创建已连接的启用OAuth的 [!DNL Salesforce] 应用程序](https://help.salesforce.com/s/articleView?id=sf.connected_app_create_api_integration.htm&amp;type=5). 创建连接的 [!DNL Salesforce] ，请使用以下格式指定回调URL:

   ```
   https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html
   ```

   其中，服务器和端口是指 [!DNL AEM Forms] 服务器。

* 创建连接的 [!DNL Salesforce] 应用程序，指定 `full` 和 `offline_access` 作为OAuth范围的值。

* 记下所连接应用程序的客户端ID（称为客户端密钥）和客户端密钥（称为客户端密钥）的值。

请执行以下步骤以配置 [!DNL Salesforce] 云服务：

1. 开 [!DNL AEM Forms] 创作实例，导航到 **[!UICONTROL 工具]** ![锤子](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL 数据源]**. 可用的包装器文件夹列表包括一个文件夹，其标题为 `DappTitle`  while [生成AEM原型项目](setup-local-development-environment.md##forms-cloud-service-local-development-environment).
1. 点按文件夹名称，选择 **[!UICONTROL Salesforce云配置]**，然后点按 **[!UICONTROL 属性]**.
1. 在 **[!UICONTROL 身份验证设置]** 选项卡：
   1. 指定 [!DNL Salesforce] 中的域URL **[!UICONTROL 主机]** 字段。 例如， [域名].my.salesforce.com.
   1. 为连接的应用程序指定客户端ID（称为客户端密钥）和客户端密钥（称为客户端密钥）。
   1. 指定 **full offline_access** (`full` 和 `offine_access` 值（以空格分隔） **[!UICONTROL 授权范围]** 字段。
   1. 点按 **[!UICONTROL 连接到OAuth]**. 系统会将您重定向到 [!DNL Microsoft Dynamics] 登录页面。
   1. 使用 [!DNL Salesforce] 凭据和接受，以允许云服务配置连接到 [!DNL Salesforce] 服务。 如果连接成功，您将被重定向到 [!DNL Salesforce] 云服务配置页面，此时会显示一条成功消息。
1. 点按 **[!UICONTROL 保存并关闭]** 完成配置设置。

### 开箱即用访问 [!DNL Salesforce] 表单数据模型

A [!DNL Salesforce] “表单数据模型”在 [!DNL AEM Forms] 服务器 [基于Experience Manager原型的Forms开发项目](setup-local-development-environment.md##forms-cloud-service-local-development-environment).

要访问表单数据模型，请导航到 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL 数据集成]**. 可用文件夹列表包括一个文件夹，其标题为 `DappTitle`  while [生成AEM原型项目](setup-local-development-environment.md##forms-cloud-service-local-development-environment). 点按文件夹名称，选择 **[!UICONTROL Salesforce数据模型]**，然后点按编辑 ![编辑](assets/edit.png) 图标以查看表单数据模型。

配置 [[!DNL Salesforce] 云配置服务](#configure-salesforce-cloud-service)，则您可以开箱即用地集成自适应表单 [!DNL Salesforce] 数据模型。

## 配置 [!DNL Microsoft Dynamics 365] 云服务 {#configure-dynamics-cloud-service}

在配置 [!DNL Microsoft Dynamics 365] 云服务，请确保您执行以下任务：

* [注册申请 [!DNL Microsoft Dynamics 365] 具有Azure Active Directory](https://docs.microsoft.com/en-us/powerapps/developer/data-platform/walkthrough-register-app-azure-active-directory). 创建连接的 [!DNL Microsoft Dynamics 365] ，请使用以下格式指定“回复URL”：

   ```
   https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html
   ```

   其中，服务器和端口是指 [!DNL AEM Forms] 服务器。

* 记下所连接应用程序的客户端ID（也称为应用程序ID）值和客户端密钥。

请执行以下步骤以配置 [!DNL Microsoft Dynamics 365] 云服务：

1. 开 [!DNL AEM Forms] 创作实例，导航到 **[!UICONTROL 工具]** ![锤子](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL 数据源]**. 可用的包装器文件夹列表包括一个文件夹，其标题为 `DappTitle`  while [生成AEM原型项目](setup-local-development-environment.md##forms-cloud-service-local-development-environment).
1. 点按文件夹名称，选择 **[!UICONTROL Microsoft Dynamics 365云配置]**，然后点按 **[!UICONTROL 属性]**.
1. 在 **[!UICONTROL 身份验证设置]** 选项卡：
   1. 输入 **[!UICONTROL 服务根]** 字段。 转到Dynamics实例，然后导航到 [开发人员资源](https://docs.microsoft.com/en-us/powerapps/developer/data-platform/view-download-developer-resources) 查看服务根字段的值。 例如，`https://<tenant-name>.dynamics.com/api/data/v9.1/`
   1. 为连接的应用程序指定客户端ID（称为应用程序ID）和客户端密钥。
   1. 替换 `{tenant}` 的租户ID **[!UICONTROL OAuth URL]**, **[!UICONTROL 刷新令牌URL]**&#x200B;和 **[!UICONTROL 访问令牌URL]** 字段。
   1. 在 **[!UICONTROL 资源]** 配置字段 [!UICONTROL Microsoft Dynamics] （包含表单数据模型）。 使用服务根URL派生Dynamics实例URL。 例如， `https://<tenant-name>.dynamics.com`.

   1. 指定 `openid` 在 **[!UICONTROL 授权范围]** 上的授权过程字段 [!DNL Microsoft Dynamics 365].
   1. 使用 [!DNL Microsoft Dynamics 365] 凭据和接受，以允许云服务配置连接到 [!DNL Microsoft Dynamics 365] 服务。 如果连接成功，您将被重定向到 [!DNL Microsoft Dynamics 365] 云服务配置页面，此时会显示一条成功消息。
1. 点按 **[!UICONTROL 保存并关闭]** 完成配置设置。

### 开箱即用访问 [!DNL Microsoft Dynamics 365] 表单数据模型

A [!DNL Microsoft Dynamics 365] “表单数据模型”在 [!DNL AEM Forms] 服务器 [基于Experience Manager原型的Forms开发项目](setup-local-development-environment.md##forms-cloud-service-local-development-environment).

要访问表单数据模型，请导航到 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL 数据集成]**. 可用文件夹列表包括一个文件夹，其标题为 `DappTitle`  while [生成AEM原型项目](setup-local-development-environment.md##forms-cloud-service-local-development-environment). 点按文件夹名称，选择 **[!UICONTROL Microsoft Dynamics 365数据模型]**，然后点按编辑 ![编辑](assets/edit.png) 图标以查看表单数据模型。

配置 [[!DNL Microsoft Dynamics 365] 云配置服务](#configure-dynamics-cloud-service)，则您可以开箱即用地集成自适应表单 [!DNL Microsoft Dynamics 365] 数据模型。
