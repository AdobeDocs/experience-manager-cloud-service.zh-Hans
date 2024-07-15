---
title: 如何将自适应表单与Microsoft® Power Automate集成？
description: 将自适应表单与Microsoft® Power Automate集成。
exl-id: a059627b-df12-454d-9e2c-cc56986b7de6
keywords: 将AEM表单连接到power automate、Power automate automation AEM Forms、将power automate集成到Adaptive Forms、将数据从Adaptive Forms发送到Power Automate
feature: Adaptive Forms
role: Admin, User, Developer
source-git-commit: 2b76f1be2dda99c8638deb9633055e71312fbf1e
workflow-type: tm+mt
source-wordcount: '1171'
ht-degree: 13%

---


# 将自适应表单与Microsoft® Power Automate连接 {#connect-adaptive-form-with-power-automate}

您可以配置自适应表单以在提交时运行 Microsoft® Power Automate Cloud Flow。配置的自适应表单将捕获的数据、附件和记录文档发送到 Power Automation Cloud Flow 进行处理。 它可帮助您构建自定义数据捕获体验，同时利用 Microsoft® Power Automate 的强大功能围绕捕获的数据构建业务逻辑并自动执行客户工作流。

自适应Forms编辑器提供&#x200B;**调用Microsoft®Power Automate流**&#x200B;提交操作以将自适应表单数据、附件和记录文档发送到Power Automate Cloud Flow。

AEM as a Cloud Service提供了多种现成的提交操作来处理表单提交。 您可以在[自适应表单提交操作](/help/forms/configure-submit-actions-core-components.md)文章中了解有关这些选项的更多信息。


## 优点

以下几个示例说明了在将自适应表单与 Microsoft® Power Automate 集成后可执行的操作：

* 在 Power Automate 业务流程中使用自适应表单数据
* 使用 Power Automate 将捕获的数据发送到 500 多个数据源或任何公开可用的 API
* 对捕获的数据执行复杂计算
* 按预定义的计划将自适应表单数据保存到存储系统

## 先决条件

将自适应表单与Microsoft® Power Automate连接需要以下项：

* Microsoft® Power Automate Premium许可证。
* Microsoft® [带`When an HTTP request is received`触发器的Power Automate流](https://docs.microsoft.com/en-us/power-automate/create-flow-solution)接受自适应表单提交数据。
* 具有[Forms作者](/help/forms/forms-groups-privileges-tasks.md)和[Forms管理员](/help/forms/forms-groups-privileges-tasks.md)权限的Experience Manager用户
* 用于连接到Microsoft的帐户®Power Automate是配置为从自适应表单接收数据的Power Automate流的所有者

## 将Formsas a Cloud Service实例与Microsoft® Power Automate连接 {#connect-forms-server-with-power-automate}

执行以下操作以将您的Formsas a Cloud Service实例连接到Microsoft® Power Automate：

1. [创建Microsoft](#ms-power-automate-application)
1. [创建Microsoft](#microsoft-power-automate-dataverse-cloud-configuration)
1. [创建Microsoft](#create-microsoft-power-automate-flow-cloud-configuration)
1. [Publish Microsoft](#publish-microsoft-power-automate-dataverse-cloud-configuration)

### 创建Microsoft® Azure Active Directory应用程序 {#ms-power-automate-application}

1. 登录到[Azure门户](https://portal.azure.com/)。
1. 从左侧导航中选择[!UICONTROL Azure Active Directory]。
1. 在默认目录页面上，从左侧面板中选择[!UICONTROL 应用程序注册]。
1. 在“应用程序注册”页面上，单击“新建注册”。
1. 在页面上指定名称、支持的帐户类型和重定向URI。 在重定向URI中，指定以下内容，然后单击保存。
   * `https://[Forms as a Cloud Service Server]/libs/fd/powerautomate/content/dataverse/config.html`
   * `https://[Forms as a Cloud Service Server]/libs/fd/powerautomate/content/flowservice/config.html`

   ![注册Azure Active Directory应用程序](assets/power-automate-application.png)

   >[!NOTE]
   >如有必要，您还可以从身份验证页面指定其他重定向URI。
   > 对于支持的帐户类型，请选择单个租户、多个租户或个人Microsoft®帐户，具体取决于您的用例


1. 在“身份验证”页面上，启用以下选项，然后单击“保存”。


   * 访问令牌（用于隐式流）
   * ID令牌（用于隐式流和混合流）

1. 在API权限页面上，单击添加权限。
1. 在Microsoft® API下，选择流服务，然后选择以下权限。
   * Flows.Manage.All
   * Flows.Read.All

   单击“添加权限”以保存权限。
1. 在API权限页面上，单击添加权限。 选择我的组织使用的API并搜索`DataVerse`。
1. 启用user_impersonation ，然后单击“添加权限”。
1. （可选）在“证书和密码”页面上，单击“新建客户端密码”。 在“添加客户端密码”屏幕上，提供密码过期的说明和时间段，然后单击“添加”。 生成一个机密字符串。
1. 记下特定于组织的[动态环境URL](https://docs.microsoft.com/en-us/power-automate/web-api#compose-http-requests)。

### 创建Microsoft® Power Automate Dataverse云配置 {#microsoft-power-automate-dataverse-cloud-configuration}

1. 在AEM Forms创作实例上，导航到&#x200B;**[!UICONTROL 工具]** ![锤子](assets/hammer.png) > **[!UICONTROL 常规]** > **[!UICONTROL 配置浏览器]**。
1. 在&#x200B;**[!UICONTROL 配置浏览器]**&#x200B;页面上，选择&#x200B;**[!UICONTROL 创建]**。
1. 在&#x200B;**[!UICONTROL 创建配置]**&#x200B;对话框中，为配置指定一个&#x200B;**[!UICONTROL 标题]**，启用&#x200B;**[!UICONTROL 云配置]**，然后选择&#x200B;**[!UICONTROL 创建]**。 系统创建一个配置容器来存储 Cloud Services。确保文件夹名称不包含任何空格。
1. 导航到&#x200B;**[!UICONTROL Tools]** ![hammer](assets/hammer.png) > **[!UICONTROL Cloud Service]** > **[!UICONTROL Microsoft®® Power Automate Dataverse]**，然后打开您在上一步中创建的配置容器。


   >[!NOTE]
   >
   >在创建自适应表单时，请在&#x200B;**[!UICONTROL 配置容器]**&#x200B;字段中指定容器名称。

1. 在配置页面上，选择&#x200B;**[!UICONTROL 创建]**&#x200B;以在AEM Forms中创建[!DNL Microsoft®®® Power Automate Flow Service]配置。
1. 在&#x200B;**[!UICONTROL 配置Microsoft®® Power Automate的Dataverse服务]**&#x200B;页面上，指定&#x200B;**[!UICONTROL 客户端ID]** （也称为应用程序ID）、**[!UICONTROL 客户端密钥]**、**[!UICONTROL OAuth URL]**&#x200B;和&#x200B;**[!UICONTROL 动态环境URL]**。 使用您在上一节中创建的[Microsoft® Azure Active Directory应用程序](#ms-power-automate-application)的客户端ID、客户端密钥、OAuth URL和动态环境URL。 在Microsoft®Azure Active Directory应用程序UI中使用端点选项来查找OAuth URL

   ![使用Microsoft Power Automate应用程序UI中的“端点”选项查找OAuth URL](assets/endpoints.png)

1. 选择&#x200B;**[!UICONTROL 连接]** 。 如有要求，请登录您的Microsoft® Azure帐户。 选择&#x200B;**[!UICONTROL 保存]**。

### 创建Microsoft® Power Automate Flow Service云配置 {#create-microsoft-power-automate-flow-cloud-configuration}

1. 导航到&#x200B;**[!UICONTROL Tools]** ![hammer](assets/hammer.png) > **[!UICONTROL Cloud Service]** > **[!UICONTROL Microsoft® Power Automate流服务]**，并打开您在上一节中创建的配置容器。


   >[!NOTE]
   >
   >在创建自适应表单时，请在&#x200B;**[!UICONTROL 配置容器]**&#x200B;字段中指定容器名称。

1. 在配置页面上，选择&#x200B;**[!UICONTROL 创建]**&#x200B;以在AEM Forms中创建[!DNL Microsoft® Power Automate Flow Service]配置。
1. 在&#x200B;**[!UICONTROL 为Microsoft配置Dataverse® Power Automate]**&#x200B;页面上，指定&#x200B;**[!UICONTROL 客户端ID]** （也称为应用程序ID）、**[!UICONTROL 客户端密钥]**、**[!UICONTROL OAuth URL]**&#x200B;和&#x200B;**[!UICONTROL 动态环境URL]**。 使用客户端ID、客户端密钥、OAuth URL和Dynamics环境ID。 在Microsoft®Azure Active Directory应用程序UI中使用端点选项来查找OAuth URL。 打开[我的流](https://us.flow.microsoft.com)链接，然后选择“我的流”，将URL中列出的ID用作动态环境ID。
1. 选择&#x200B;**[!UICONTROL 连接]**。 如有要求，请登录到您的Microsoft® Azure帐户。 选择&#x200B;**[!UICONTROL 保存]**。

### Publish Microsoft®Power Automate Dataverse和Microsoft®Power Automate Flow Service云配置 {#publish-microsoft-power-automate-dataverse-cloud-configuration}

1. 导航到&#x200B;**[!UICONTROL Tools]** ![hammer](assets/hammer.png) > **[!UICONTROL Cloud Service]** > **[!UICONTROL Microsoft® Power Automate Dataverse]**，并打开您在前[创建Microsoft® Power Automate Dataverse云配置](#microsoft-power-automate-dataverse-cloud-configuration)部分中创建的配置容器。
1. 选择`dataverse`配置并选择&#x200B;**[!UICONTROL Publish]**。
1. 在Publish页面上，选择&#x200B;**[!UICONTROL 所有配置]**，然后选择&#x200B;**[!UICONTROL Publish]**。 Publish Power Automate Dataverse和Power Automate Flow Service云配置。

您的Formsas a Cloud Service实例现在已与Microsoft® Power Automate连接。 您现在可以将自适应Forms数据发送到Power Automate流。

## 使用调用Microsoft® Power Automate流提交操作将数据发送到Power Automate流 {#use-the-invoke-microsoft-power-automate-flow-submit-action}

将Formsas a Cloud Service实例与Microsoft® Power Automate](#connect-forms-server-with-power-automate)连接后，执行以下操作以配置自适应表单，以便在提交表单时将捕获的数据发送到Microsoft®流。[

1. 登录到创作实例，选择您的自适应表单并单击&#x200B;**[!UICONTROL 属性]**。
1. 在配置容器中，浏览并选择在[创建Microsoft® Power Automate Dataverse云配置](#microsoft-power-automate-dataverse-cloud-configuration)部分创建的容器，然后选择&#x200B;**[!UICONTROL 保存并关闭]**。
1. 打开自适应表单进行编辑，然后导航到自适应表单容器属性的&#x200B;**[!UICONTROL 提交]**&#x200B;部分。
1. 在属性容器中，为&#x200B;**[!UICONTROL 提交操作]**&#x200B;选择&#x200B;**[!UICONTROL 调用Power Automate流]**&#x200B;选项并选择&#x200B;**[!UICONTROL Power Automate流]**。 选择所需的流程，并在提交时向其提交自适应Forms数据。

   ![配置提交操作](assets/submission.png)

>[!NOTE]
>
> 在提交自适应表单之前，请确保将具有以下JSON架构的`When an HTTP Request is received`触发器添加到您的Power Automate流中。

```
        {
            "type": "object",
            "properties": {
                "attachments": {
                    "type": "array",
                    "items": {
                        "type": "object",
                        "properties": {
                            "filename": {
                                "type": "string"
                            },
                            "data": {
                                "type": "string"
                            },
                            "contentType": {
                                "type": "string"
                            },
                            "size": {
                                "type": "integer"
                            }
                        },
                        "required": [
                            "filename",
                            "data",
                            "contentType",
                            "size"
                        ]
                    }
                },
                "templateId": {
                    "type": "string"
                },
                "templateType": {
                    "type": "string"
                },
                "data": {
                    "type": "string"
                },
                "document": {
                    "type": "object",
                    "properties": {
                        "filename": {
                            "type": "string"
                        },
                        "data": {
                            "type": "string"
                        },
                        "contentType": {
                            "type": "string"
                        },
                        "size": {
                            "type": "integer"
                        }
                    }
                }
            }
        }
```

<!--
## See also

* [Create an Adaptive Form](creating-adaptive-form-core-components.md)
* [Configure a Submit Action](configure-submit-actions-core-components.md)
* [Adobe Experience Manager Connector for Microsoft&reg; Power Automate](https://learn.microsoft.com/en-us/connectors/adobeexperiencemanag/)
* [Connect Adaptive Form to Microsoft® Power Automate](/help/forms/configure-submit-actions-core-components.md#microsoft-power-automate)
-->


## 相关文章

{{af-submit-action}}

<!--

>[!MORELIKETHIS]
>
>* [Connect Adaptive Form to Microsoft Power Automate](/help/forms/configure-submit-actions-core-components.md#microsoft-power-automate)

-->