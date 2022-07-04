---
title: 将自适应表单与Microsoft® Power集成自动化
description: 将自适应表单与Microsoft® Power自动集成。
hide: true
hidefromtoc: true
exl-id: a059627b-df12-454d-9e2c-cc56986b7de6
source-git-commit: ccc4d487cb180273284276cf9cdf18680a3efcb8
workflow-type: tm+mt
source-wordcount: '1183'
ht-degree: 2%

---

# 将自适应表单与Microsoft®电源自动连接 {#connect-adaptive-form-with-power-automate}

您可以配置自适应表单以在提交时运行Microsoft® Power自动云流。 配置的自适应表单会发送捕获的数据、附件和记录文档，以增强云流自动化以进行处理。 它可帮助您构建自定义数据捕获体验，同时利用Microsoft® Power Automate的强大功能围绕捕获的数据构建业务逻辑并自动执行客户工作流。 以下是将自适应表单与Microsoft®电源自动化集成后可以执行的操作的一些示例：

* 在强大的自动化业务流程中使用自适应Forms数据
* 使用自动化功能将捕获的数据发送到500多个数据源或任何公开可用的API
* 对捕获的数据执行复杂计算
* 按预定义的时间表将自适应Forms数据保存到存储系统

自适应Forms编辑器提供了 **调用Microsoft®电源自动化流程** 用于发送自适应表单数据、附件和记录文档的提交操作将发送到Power Automate云流。 要使用“提交”操作将捕获的数据发送到Microsoft®电源自动化， [使用Microsoft® Power Automate连接Formsas a Cloud Service实例](forms-microsoft-power-automate-integration.md#connect-forms-server-with-power-automate)

## 前提条件

将自适应表单与Microsoft®电源自动化连接需要满足以下条件：

* Microsoft® Power Automate Premium许可证。
* Microsoft® [电源自动化流程](https://docs.microsoft.com/en-us/power-automate/create-flow-solution) 和 `When an HTTP request is received` 触发器接受自适应表单提交数据。


* 具有Forms作者和Forms管理员权限的Experience Manager用户。
* 确保用于连接到电源自动化的帐户是电源自动化流程的所有者。


## 使用Microsoft® Power Automate连接Formsas a Cloud Service实例 {#connect-forms-server-with-power-automate}

执行以下操作，将Formsas a Cloud Service实例与Microsoft® Power Automate连接：

1. 创建Microsoft® Azure Active Directory应用程序
1. 创建Microsoft® Power自动化Dataverse Cloud配置。
1. 创建Microsoft®电源自动化流程服务云配置
1. 发布Microsoft® Power自动化Dataverse Cloud配置。

### 创建Microsoft® Azure Active Directory应用程序 {#ms-power-automate-application}

1. 登录到 [Azure门户](https://portal.azure.com/).
1. 选择 [!UICONTROL Azure Active Directory] 的上界。
1. 在“默认目录”页面上，选择 [!UICONTROL 应用程序注册] 中。
1. 在“应用程序注册”页面上，单击“新建注册”。
1. 在页面上指定名称、支持的帐户类型和重定向URI。 在重定向URI中，指定以下内容并单击保存。
   * `https://[Forms as a Cloud Service Server]/libs/fd/powerautomate/content/dataverse/config.html`
   * `https://[Forms as a Cloud Service Server]/libs/fd/powerautomate/content/flowservice/config.html`

   ![注册Azure Active Directory应用程序](assets/power-automate-application.png)

   >[!NOTE]
   >您还可以根据需要从“身份验证”页面指定其他重定向URI。
   > 对于支持的帐户类型，请根据您的用例选择单个租户、多个租户或个人Microsoft帐户


1. 在“Authentication（身份验证）”页面上，启用以下选项，然后单击Save（保存）。


   * 访问令牌（用于隐式流）
   * ID令牌（用于隐式和混合流）

1. 在API权限页面上，单击添加权限。
1. 在Microsoft® API下，选择流量服务，然后选择以下权限。
   * Flows.Manage.All
   * Flows.Read.All

   单击添加权限以保存权限。
1. 在API权限页面上，单击添加权限。 选择我的组织使用和搜索的API `DataVerse`.
1. 启用user_impersonation并单击添加权限。
1. （可选）在“证书和密钥”页面上，单击“新建客户端密钥”。 在添加客户端密钥屏幕上，提供密钥的过期说明和时间段，然后单击添加。 将生成一个密钥字符串。
1. 记下您组织的特定信息 [Dynamics环境URL](https://docs.microsoft.com/en-us/power-automate/web-api#compose-http-requests).

### 创建Microsoft® Power自动配置Dataverse Cloud {#microsoft-power-automate-dataverse-cloud-configuration}

1. 在AEM Forms创作实例上，导航到 **[!UICONTROL 工具]** ![锤子](assets/hammer.png) > **[!UICONTROL 常规]** > **[!UICONTROL 配置浏览器]**.
1. 在 **[!UICONTROL 配置浏览器]** 页面，点按 **[!UICONTROL 创建]**.
1. 在 **[!UICONTROL 创建配置]** 对话框，指定 **[!UICONTROL 标题]** 对于配置，请启用 **[!UICONTROL 云配置]**，然后点按 **[!UICONTROL 创建]**. 系统创建一个配置容器来存储 Cloud Services。确保文件夹名称不包含任何空格。
1. 导航到 **[!UICONTROL 工具]** ![锤子](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Microsoft® Power自动化Dataverse]** 并打开在上一步中创建的配置容器。

   >[!NOTE]
   >
   >创建自适应表单时，请在 **[!UICONTROL 配置容器]** 字段。
1. 在配置页面上，点按 **[!UICONTROL 创建]** 创建 [!DNL Microsoft® Power Automate Flow Service] 配置AEM Forms。
1. 在 **[!UICONTROL 为Microsoft® Power自动配置Dataverse Service]** 页面，指定 **[!UICONTROL 客户端ID]** （也称为应用程序ID）， **[!UICONTROL 客户端密钥]**, **[!UICONTROL OAuth URL]** 和 **[!UICONTROL 动态环境URL]**. 使用的客户端ID、客户端密钥、OAuth URL和动态环境URL [Microsoft® Azure Active Directory应用程序](#ms-power-automate-application) 您在上一部分中创建。 使用Microsoft® Azure Active Directory应用程序UI中的“端点”选项查找OAuth URL

![使用Microsoft Power自动化应用程序UI中的“使用端点”选项来查找OAuth URL](assets/endpoints.png)
使用Microsoft® Power自动化应用程序UI中的“使用端点”选项以查找OAuth URL

1. 点按 **[!UICONTROL 连接]** . 如果需要，请登录您的Microsoft® Azure帐户。 点按&#x200B;**[!UICONTROL 保存]**。

### 创建Microsoft®电源自动化流程服务云配置。

1. 导航到 **[!UICONTROL 工具]** ![锤子](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Microsoft®电源自动化流程服务]** 并打开在上一部分中创建的配置容器。

   >[!NOTE]
   >
   >创建自适应表单时，请在 **[!UICONTROL 配置容器]** 字段。
1. 在配置页面上，点按 **[!UICONTROL 创建]** 创建 [!DNL Microsoft® Power Automate Flow Service] 配置AEM Forms。
1. 在 **[!UICONTROL 为Microsoft®电源自动配置Dataverse]** 页面，指定 **[!UICONTROL 客户端ID]** （也称为应用程序ID）， **[!UICONTROL 客户端密钥]**, **[!UICONTROL OAuth URL]** 和 **[!UICONTROL 动态环境URL]**. 使用客户端ID、客户端密钥、OAuth URL和Dynamics环境ID。 使用Microsoft® Azure Active Directory应用程序UI中的“端点”选项查找OAuth URL。 打开 [我的流程](https://us.flow.microsoft.com) 链接并点按我的流量会将URL中列出的ID用作Dynamics环境ID。
1. 点按 **[!UICONTROL 连接]**. 如果出现问题，请登录您的Microsoft® Azure帐户。 点按&#x200B;**[!UICONTROL 保存]**。

### 发布Microsoft® Power自动化Dataverse和Microsoft® Power自动化Flow Service云配置 {#publish-microsoft-power-automate-dataverse-cloud-configuration}

1. 导航到 **[!UICONTROL 工具]** ![锤子](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Microsoft® Power自动化Dataverse]** ，然后打开在上一个 [创建Microsoft® Power自动配置Dataverse Cloud](#microsoft-power-automate-dataverse-cloud-configuration) 中。
1. 选择 `dataverse` 配置和点按 **[!UICONTROL 发布]**.
1. 在发布页面上，选择 **[!UICONTROL 所有配置]** 点按 **[!UICONTROL 发布]**. 发布Power Automate Dataverse和Power Automate Flow Service云配置。

您的Formsas a Cloud Service实例现已与Microsoft® Power Automate连接。 您现在可以将自适应Forms数据发送到电源自动化流程。

## 使用调用Microsoft®电源自动化流程提交操作将数据发送到电源自动化流程 {#use-the-invoke-microsoft-power-automate-flow-submit-action}

在 [使用Microsoft® Power Automate连接Formsas a Cloud Service实例](#connect-forms-server-with-power-automate)，请执行以下操作以配置您的自适应表单，以在表单提交时将捕获的数据发送到Microsoft®流程。

1. 登录到创作实例，选择自适应表单并单击 **[!UICONTROL 属性]**.
1. 在配置容器中，浏览并选择在部分中创建的容器 [创建Microsoft® Power自动配置Dataverse Cloud](#microsoft-power-automate-dataverse-cloud-configuration)，然后点按 **[!UICONTROL 保存并关闭]**.
1. 打开自适应表单进行编辑，然后导航到 **[!UICONTROL 提交]** 部分。
1. 在属性容器中， **[!UICONTROL 提交操作]** 选择 **[!UICONTROL 调用电源自动化流]** 选项。 可用电源自动化流程列表将可用 **[!UICONTROL 电源自动化流程]** 选项。 选择所需的流程，并在提交时将自适应Forms数据提交到该流程。

![配置提交操作](assets/submission.png)

>[!NOTE]
>
> 在提交自适应表单之前，请确保 `When an HTTP Request is received` 您的Power Automate流程中添加了以下JSON模式的触发器。

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

