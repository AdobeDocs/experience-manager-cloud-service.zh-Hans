---
title: 如何将Adobe Acrobat Sign与AEM Forms集成？
description: 了解如何为 [!DNL AEM Forms] as a Cloud Service配置Adobe Acrobat Sign？
feature: Adaptive Forms, Acrobat Sign
role: Admin, User
level: Intermediate
source-git-commit: 551123925e43c98f8870f4a5da028d211f5c8ffb
workflow-type: tm+mt
source-wordcount: '2195'
ht-degree: 23%

---

# 将[!DNL AEM Forms]as a Cloud Service与[!DNL Adobe Acrobat Sign]连接 {#integrate-adobe-sign-with-aem-forms}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/adobe-sign-integration-adaptive-forms.html#adobe-acrobat-sign-for-government) |
| AEM as a Cloud Service | 本文 |

[!DNL Adobe Acrobat Sign]为自适应Forms和AEM工作流启用电子签名工作流。 电子签名改进了法律、销售、工资单、人力资源管理和其他许多方面的文档的处理工作流。

在典型的 [!DNL Adobe Acrobat Sign] 和自适应表单方案中，用户需填写自适应表单来申请服务。例如，信用卡申请表和公民权益表。在用户填写、签署和提交申请表后，该表将发送给服务提供商以执行后续操作。服务提供商将审核申请，并使用 [!DNL Adobe Acrobat Sign] 将申请标记为已批准。AEM Forms支持Adobe Acrobat Sign和Adobe Acrobat Sign Solutions政府版。 根据您的许可证和要求，您可以将AEM Forms与以下任一解决方案集成或连接：

* [将AEM Forms与Adobe Acrobat Sign连接](#adobe-sign)
* [将AEM Forms与适用于政府的Adobe Acrobat Sign Solutions连接](#adobe-acrobat-sign-for-government)

## 将AEM Forms与Adobe Acrobat Sign连接 {#adobe-sign}

要将&#x200B;**[!DNL AEM Forms]**&#x200B;与&#x200B;**[!DNL Adobe Acrobat Sign]**&#x200B;连接，请设置先决条件部分中列出的软件和帐户，并在Formsas a Cloud Service创作实例和Publish实例中配置Adobe Sign Cloud Service：

### 将AEM Forms连接到Adobe Acrobat Sign的先决条件 {#prerequisites-for-adobe-sign}

您需要以下安装程序才能将[!DNL Adobe Acrobat Sign]与[!DNL AEM Forms]集成：

1. 有效的[Adobe Acrobat Sign开发人员帐户](https://acrobat.adobe.com/us/en/sign/developer-form.html)。
1. [Adobe Acrobat Sign API应用程序](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/create_app.md)。
1. [!DNL Adobe Acrobat Sign] API 应用程序的凭据（客户端 ID 和客户端密码）。
1. （仅适用于基于Government ID的身份验证）[为政府ID身份验证启用身份验证方法](https://helpx.adobe.com/sign/using/adobesign-authentication-government-id.html#AuditReport)。

### 将AEM Forms创作和发布实例连接到Adobe Acrobat Sign {#configure-adobe-sign-with-aem-forms}

满足前提条件后，执行以下步骤以在创作实例上使用 [!DNL AEM Forms] 配置 [!DNL Adobe Acrobat Sign]。

1. 在AEM Forms创作实例上，导航到&#x200B;**[!UICONTROL 工具]** ![锤子](assets/hammer.png) > **[!UICONTROL 常规]** > **[!UICONTROL 配置浏览器]**。
1. 在&#x200B;**[!UICONTROL 配置浏览器]**&#x200B;页面上，选择&#x200B;**[!UICONTROL 创建]**。
1. 在&#x200B;**[!UICONTROL 创建配置]**&#x200B;对话框中，为配置指定一个&#x200B;**[!UICONTROL 标题]**，启用&#x200B;**[!UICONTROL 云配置]**，然后选择&#x200B;**[!UICONTROL 创建]**。 系统创建一个配置容器来存储 Cloud Services。确保文件夹名称不包含任何空格。
1. 导航到&#x200B;**[!UICONTROL 工具]** ![锤子](assets/hammer.png) > **[!UICONTROL Cloud Service]** > **[!UICONTROL Adobe Acrobat Sign]**，然后打开您在上一步中创建的配置容器。

   >[!NOTE]
   >
   >在创建自适应表单时，请在&#x200B;**[!UICONTROL 配置容器]**&#x200B;字段中指定容器名称。

1. 在配置页面上，选择&#x200B;**[!UICONTROL 创建]**&#x200B;以在AEM Forms中创建[!DNL Adobe Acrobat Sign]配置。
1. 在&#x200B;**[!UICONTROL 创建Adobe Acrobat Sign配置]**&#x200B;页面的&#x200B;**[!UICONTROL 常规]**&#x200B;选项卡中，为配置指定一个&#x200B;**[!UICONTROL 名称]**，然后选择&#x200B;**[!UICONTROL 下一步]**。 您可以选择指定&#x200B;**[!UICONTROL 标题]**&#x200B;并浏览以选择配置的&#x200B;**[!UICONTROL 缩略图]**。

1. 现在您可以&#x200B;**[!UICONTROL 选择解决方案]**&#x200B;以选择[!DNL Adobe Acrobat Sign]。

   <!--![Adobe Acrobat Sign Solutions](assets/adobe-sign-solution.png)-->
   ![Adobe Acrobat Sign Solutions配置](assets/adobe-sign-solution-config.png)

<!--

[create URL](#create-a-redirect-url-for-your-aem-instance)
 -->

1. 将当前浏览器窗口中存在的URL复制到笔记本，并从URL中删除部分`/ui#/aem`。 在后续步骤中，需要修改的URL才能使用[!DNL AEM Forms]配置[!DNL Adobe Acrobat Sign]应用程序。 选择&#x200B;**[!UICONTROL 下一步]**。

1. 在&#x200B;**[!UICONTROL 设置]**&#x200B;选项卡中，
   * **[!UICONTROL OAuth URL]**&#x200B;字段包含包含Adobe Sign数据库分片的默认URL。 URL 的格式为：

     `https://<shard>/public/oauth/v2`

     例如：
     `https://secure.na1.echosign.com/public/oauth/v2`

   * **[!UICONTROL Access令牌URL]**&#x200B;字段包含包含Adobe Sign数据库分片的默认URL。 URL 的格式为：

     `https://<shard>/oauth/v2/token`

     例如：
     `https://api.na1.echosign.com/oauth/v2/token`

   其中：

   **na1** 指默认数据库分片。您可以修改数据库分片的值。确保 [!DNL  Adobe Acrobat Sign] 云配置指向[正确分片](https://helpx.adobe.com/sign/using/identify-account-shard.html)。

   >[!NOTE]
   >
   >* 保持&#x200B;**创建Adobe Acrobat Sign配置**&#x200B;页面打开。 不要关闭它。 在为[!DNL Adobe Acrobat Sign]应用程序配置OAuth设置后，您可以检索&#x200B;**客户端ID**&#x200B;和&#x200B;**客户端密钥**，如即将执行的步骤中所述。
   > * 登录Adobe Sign帐户后，导航到&#x200B;**[!UICONTROL Acrobat Sign API]** > **[!UICONTROL API信息]** > **[!UICONTROL REST API方法文档]** > **[!UICONTROL OAuth访问令牌]**，以访问与Adobe Sign OAuth URL和访问令牌URL相关的信息。

1. 配置 [!DNL Adobe Acrobat Sign] 应用程序的 OAuth 设置：

   1. 打开浏览器窗口，并登录到您的 [!DNL Adobe Acrobat Sign] 开发人员帐户。
   1. 选择为[!DNL AEM Forms]配置的应用程序，然后选择&#x200B;**[!UICONTROL 为应用程序]**&#x200B;配置OAuth。
   1. 在&#x200B;**[!UICONTROL 重定向URL]**&#x200B;框中，添加上一步中复制的URL（步骤8），然后单击&#x200B;**[!UICONTROL 保存]**。
   1. 为[!DNL Adobe Acrobat Sign]应用程序启用以下作用域，然后单击&#x200B;**[!UICONTROL 保存]**。

   * [!DNL aggrement_read]
   * [!DNL aggrement_write]
   * [!DNL aggrement_send]
   * [!DNL widget_read]
   * [!DNL widget_write]
   * [!DNL workflow_read]

   
   > 您可以直接从AEM UI中将作用域修饰符从`self`更改为`account`，如步骤12中所述。

   有关为 [!DNL Adobe Acrobat Sign] 应用程序配置 OAuth 设置并获取密钥的分步信息，请参阅[为应用程序配置 OAuth 设置](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/configure_oauth.md)开发人员文档。

   ![OAuth 配置](/help/forms/assets/oauthconfig-new.png)

1. 返回&#x200B;**[!UICONTROL 创建Adobe Acrobat Sign配置]**&#x200B;页面。 在&#x200B;**[!UICONTROL 设置]**&#x200B;选项卡中，指定[**[!UICONTROL 客户端ID]** （也称为应用程序ID）和&#x200B;**[!UICONTROL 客户端密钥]**]。 使用您在上一步中创建的Adobe Acrobat Sign应用程序](https://opensource.adobe.com/acrobat-sign/developer_guide/helloworld.html#get-the-app-id-and-secret)的[客户端ID和客户端密钥。

1. 在[!UICONTROL 授权范围]部分中，您可以根据需要通过将前缀“self”或“account”添加到范围中，将范围修改为“account”或“self”。
   ![授权范围](/help/forms/assets/authorization-scope.png)

1. 选择&#x200B;**[!UICONTROL 为附件启用Adobe Acrobat Sign]**&#x200B;选项以将附加到自适应表单的文件附加到已发送以供签名的相应[!DNL Adobe Acrobat Sign]文档。

1. 选择&#x200B;**[!UICONTROL 连接到Adobe Acrobat Sign]**。 在系统提示输入凭据时，提供创建[!DNL Adobe Acrobat Sign]应用程序时使用的帐户的&#x200B;**用户名**&#x200B;和&#x200B;**密码**。 当要求您确认`your developer account`的访问时，请单击&#x200B;**[!UICONTROL 允许访问]**。 如果凭据正确，并且您允许 [!DNL AEM Forms] 访问您的 [!DNL Adobe Acrobat Sign] 开发人员帐户，系统会显示一条与以下内容类似的成功消息。

   ![Adobe Acrobat Sign云配置成功](assets/adobe-sign-cloud-configuration-success.png)

1. 选择&#x200B;**[!UICONTROL 创建]**&#x200B;以创建[!DNL Adobe Acrobat Sign]配置。

1. 选择配置并单击&#x200B;**[!UICONTROL Publish]**，选择配置，然后单击&#x200B;**[!UICONTROL Publish]**。 这会将配置复制到相应的发布环境。

1. 在开发人员实例、暂存实例和生产实例（以剩下的实例为准）上重复上述所有步骤以使用 [!DNL AEM Forms] 为环境配置 [!DNL Adobe Acrobat Sign]。

现在，您可以[将Adobe Acrobat Sign字段添加到自适应表单](working-with-adobe-sign.md)。 确保将用于 Cloud Service 的配置容器添加到为 [!DNL Adobe Acrobat Sign] 启用的所有自适应表单。您可以在自适应表单的属性中指定配置容器。

>[!NOTE]
>
> 要配置Adobe Sign沙盒，您可以按照[Adobe Sign](#adobe-sign)中所述的相同配置步骤操作。

#### 疑难解答 {#resolve-config-error}

当您将[!DNL Adobe Acrobat Sign]与[!DNL AEM Forms]连接并查找错误`Unable to authorize access because the client configuration is invalid: invalid_request`时，如下图所示。 可执行以下步骤来解决此问题：

![配置错误](/help/forms/assets/config_error_sign.png)

1. 将当前浏览器窗口中存在的URL复制到笔记本，并从URL中删除部分`/ui#/aem`。
1. 打开浏览器窗口，并登录到您的 [!DNL Adobe Acrobat Sign] 开发人员帐户。
1. 选择为[!DNL AEM Forms]配置的应用程序，然后选择&#x200B;**[!UICONTROL 为应用程序]**&#x200B;配置OAuth。
1. 在&#x200B;**[!UICONTROL 重定向URL]**&#x200B;框中，添加上一步中复制的URL，然后单击&#x200B;**[!UICONTROL 保存]**。

## 将AEM Forms与适用于政府的Adobe Acrobat Sign Solutions连接 {#adobe-acrobat-sign-for-government}

将AEM Forms与面向政府的Adobe Acrobat Sign Solutions连接是一个多步骤过程。 它涉及：

* 为您的AEM实例创建重定向URL
* 与面向政府团队的Adobe Sign解决方案共享重定向URL和范围
* 从Adobe Sign团队接收凭据
* 使用收到的凭据将AEM Forms与适用于政府的Adobe Acrobat Sign Solutions连接

![Adobe Sign政府工作流程](/help/forms/assets/adobe-acrobat-sign-govt-workflow.png)


AEM Formsas a Cloud Service提供开发、暂存和生产环境。 您可以将的开发环境与的Adobe Acrobat Sign Solutions政府版连接，以后再连接暂存环境和生产环境。

### 开始之前 {#prerequisites-for-adobe-sign-for-acrobat-sign-for-government}

在开始将AEM Forms与Adobe Acrobat Sign解决方案连接之前，请确保已配置您的[Adobe Acrobat Sign Solutions for Government](https://opensource.adobe.com/acrobat-sign/signgov/gstarted.html#account-provisioning)帐户。


### 将AEM Formsas a Cloud Service与适用于政府的Adobe Acrobat Sign Solutions连接 {#connect-adobe-acrobat-sign-for-government}

#### 为您的AEM实例创建重定向URL

1. 在Formsas a Cloud Service创作实例上，导航到&#x200B;**[!UICONTROL 工具]** ![锤子](assets/hammer.png) > **[!UICONTROL 常规]** > **[!UICONTROL 配置浏览器]**。
1. 在&#x200B;**[!UICONTROL 配置浏览器]**&#x200B;页面上，选择&#x200B;**[!UICONTROL 创建]**。
1. 在&#x200B;**[!UICONTROL 创建配置]**&#x200B;对话框中，为配置指定一个&#x200B;**[!UICONTROL 标题]**，启用&#x200B;**[!UICONTROL 云配置]**，然后选择&#x200B;**[!UICONTROL 创建]**。 它将创建一个配置容器来存储Cloud Service。 确保文件夹名称不包含任何空格。
1. 导航到&#x200B;**[!UICONTROL 工具]** ![锤子](assets/hammer.png) > **[!UICONTROL Cloud Service]** > **[!UICONTROL Adobe Acrobat Sign]**，然后打开您在上一步中创建的配置容器。 在创建自适应表单时，请在&#x200B;**[!UICONTROL 配置容器]**&#x200B;字段中指定容器名称。
1. 在配置页面上，选择&#x200B;**[!UICONTROL 创建]**&#x200B;以在AEM Forms中创建[!DNL Adobe Acrobat Sign]配置。
1. 将当前浏览器窗口的URL复制到记事本，并从URL中删除`/ui#/aem`。 此URL称为`re-direct URL`。
在下一部分中，您与Adobe Sign团队共享`re-direct URL`和`Scopes`，并请求凭据（客户端ID和客户端密钥）。

#### 与Adobe Sign团队共享重定向URL和作用域并接收凭据

Adobe Acrobat Sign政府解决方案团队要求为您的Adobe Acrobat Sign应用程序（如下所列）启用`re-direct URL`和某些范围，以生成凭据（客户端ID和客户端密钥），从而允许您将AEM Forms与适用于政府的Adobe Acrobat Sign Solutions连接。

与您的Adobe Acrobat Sign政府解决方案代表([Adobe Professional Services团队成员](https://opensource.adobe.com/acrobat-sign/signgov/gstarted.html#password))共享`scopes`（如下所列），并共享在上一部分中创建并记下的最后一步的`re-direct URL`。

**_范围_**

* [!DNL aggrement_read]
* [!DNL aggrement_write]
* [!DNL aggrement_send]
* [!DNL widget_read]
* [!DNL widget_write]
* [!DNL workflow_read]
* [!DNL offline_access]

该代表会生成凭据并与您共享。 在下一部分中，您使用凭据（客户端ID和客户端密钥）将AEM Forms与用于政府的Adobe Acrobat Sign Solutions连接。

#### 使用收到的凭据将AEM Forms与适用于政府的Adobe Acrobat Sign Solutions连接

1. 在浏览器中打开`re-direct URL`。 您在[在AEM实例](#create-a-redirect-url-for-your-aem-instance)部分中创建重定向URL的最后一步中创建并记下了`re-direct URL`。

1. 在&#x200B;**[!UICONTROL 创建Adobe Sign配置]**&#x200B;页面的&#x200B;**[!UICONTROL 常规]**&#x200B;选项卡中，为配置指定一个&#x200B;**[!UICONTROL 名称]**，然后选择&#x200B;**[!UICONTROL 下一步]**。 您可以选择指定&#x200B;**[!UICONTROL 标题]**&#x200B;并浏览以选择配置的&#x200B;**[!UICONTROL 缩略图]**。 单击&#x200B;**[!UICONTROL 下一步]**。

1. 在&#x200B;**[!UICONTROL 创建Adobe Sign配置]**&#x200B;页面的&#x200B;**[!UICONTROL 设置]**&#x200B;选项卡中，对于&#x200B;**[!UICONTROL 选择解决方案]**&#x200B;选项，选择[!DNL Adobe Acrobat Sign Solutions for Government]。


   政府用![Adobe Acrobat Sign Solutions](assets/adobe-sign-for-govt.png)

1. 在&#x200B;**[!UICONTROL 电子邮件]**&#x200B;字段中，为政府帐户指定与您的Adobe Acrobat Sign Solutions关联的电子邮件地址。

1. 在&#x200B;**[!UICONTROL 设置]**&#x200B;选项卡中，
   * **[!UICONTROL OAuth URL]**&#x200B;字段包含包含Adobe Sign数据库分片的默认URL。 URL 的格式为：

     `https://<shard>/api/gateway/adobesignauthservice/api/v1/authorize`

     例如：
     `https://secure.na1.adobesign.us/api/gateway/adobesignauthservice/api/v1/authorize`

   * **[!UICONTROL Access令牌URL]**&#x200B;字段包含包含Adobe Sign数据库分片的默认URL。 URL 的格式为：

     `https://<shard>/api/gateway/adobesignauthservice/api/v1/token`

     例如：
     `https://secure.na1.adobesign.us/api/gateway/adobesignauthservice/api/v1/token`

   其中：

   **na1** 指默认数据库分片。您可以修改数据库分片的值。确保 [!DNL  Adobe Acrobat Sign] 云配置指向[正确分片](https://helpx.adobe.com/sign/using/identify-account-shard.html)。

   >[!NOTE]
   >
   > * 登录Adobe Sign帐户后，导航到&#x200B;**[!UICONTROL Acrobat Sign API]** > **[!UICONTROL API信息]** > **[!UICONTROL REST API方法文档]** > **[!UICONTROL OAuth访问令牌]**，以访问与Adobe Sign oAuth URL和访问令牌URL相关的信息。

1. 将Adobe Acrobat Sign在上一节中为政府解决方案代表([Adobe Professional Services团队成员])共享的凭据用作[**[!UICONTROL 客户端ID]**&#x200B;和&#x200B;**[!UICONTROL 客户端密钥]**]。

1. 选择&#x200B;**[!UICONTROL 为附件启用Adobe Acrobat Sign]**&#x200B;选项以将附加到自适应表单的文件附加到已发送以供签名的相应[!DNL Adobe Acrobat Sign]文档。

1. 选择&#x200B;**[!UICONTROL 连接到Adobe Sign]**。 在系统提示输入凭据时，提供在创建 [!DNL Adobe Acrobat Sign] 应用程序时所用帐户的用户名和密码。当要求您确认`your developer account`的访问时，请单击&#x200B;**[!UICONTROL 允许访问]**。 如果凭据正确，并且您允许 [!DNL AEM Forms] 访问您的 [!DNL Adobe Acrobat Sign] 开发人员帐户，系统会显示一条与以下内容类似的成功消息。

   ![Adobe Acrobat Sign云配置成功](assets/adobe-sign-cloud-configuration-success.png)

   <!-- > When prompted for credentials, provide username and password of the account used while creating [!DNL Adobe Acrobat Sign] application. When asked to confirm access for `your developer account`, Click **[!UICONTROL Allow Access]**. -->

1. 选择&#x200B;**[!UICONTROL 创建]**&#x200B;以创建配置。

1. 选择配置并单击&#x200B;**[!UICONTROL Publish]**，选择配置，然后单击&#x200B;**[!UICONTROL Publish]**。 这会将配置复制到相应的发布环境。

1. 在开发人员实例、暂存实例和生产实例（以剩下的实例为准）上重复上述所有步骤以使用 [!DNL AEM Forms] 为环境配置 [!DNL Adobe Acrobat Sign Solutions for Government]。

现在，您可以[在自适应表单](working-with-adobe-sign.md)或[AEM Workflow](/help/forms/aem-forms-workflow-step-reference.md#sign-document-step-sign-document-step)中添加Adobe Acrobat Sign字段。 确保将用于Cloud Service配置的配置容器添加到为[!DNL Adobe Acrobat Sign]启用的所有自适应Forms。 您可以在自适应表单的属性中指定配置容器。

## 配置[!DNL Adobe Acrobat Sign]计划程序以同步签名状态 {#configure-adobe-sign-scheduler-to-sync-the-signing-status}

AEM Formsas a Cloud Service提供调度程序服务，可按定义的时间间隔检查签名者的状态。 配置计划程序服务的方案：

* 如果您使用[提交表单（在每个收件人完成签字仪式后）](/help/forms/working-with-adobe-sign.md#select-adobe-sign-cloud-service-and-signing-order)来签署文档，则只有在所有签名者都签署表单后才提交表单。
* 如果您使用AEM Workflow](/help/forms/aem-forms-workflow-step-reference.md#sign-document-step)中的[签名步骤对文档进行签名，则签名步骤将等待所有签名者签名该文档，然后再继续工作流的下一步。

默认情况下，[!DNL Adobe Acrobat Sign] 调度程序服务每 24 小时检查（轮询）一次签名者响应。您可以为您的环境更改此默认间隔。

要更改默认间隔，请为&#x200B;**Adobe Acrobat Sign Configuration Service**&#x200B;配置的&#x200B;**sign.status.exp**&#x200B;属性指定[cron表达式](https://en.wikipedia.org/wiki/Cron#CRON_expression)。

例如，要在每天凌晨00:00运行配置服务，请设置&#x200B;**Adobe Acrobat Sign Configuration Service**&#x200B;配置的&#x200B;**sign.status.exp**&#x200B;属性以指定`0 0 0 1/1 * ? *`。 以下 JSON 文件显示了每天凌晨 00:00 运行配置服务的示例：

```json
{
  "sign.status.exp":"0 0 0 1/1 * ? *"
}
```

要设置配置的值，请[使用 AEM SDK 生成 OSGi 配置](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#generating-osgi-configurations-using-the-aem-sdk-quickstart)，并向 Cloud Service 实例[部署配置](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en#deployment-process)。

## 常见问题解答

* **问：我能否在iframe中渲染Adobe Sign GovCloud签名页面？**
* **A：**&#x200B;是，您可以在iframe中渲染Adobe Sign GovCloud签名页面。

>[!MORELIKETHIS]
>
>* [使用涂写签名对表单进行电子签名](/help/forms/signing-forms-using-scribble.md)
>* [将Adobe Acrobat Sign与自适应Forms结合使用的最佳实践](https://medium.com/adobetech/using-adobe-sign-to-e-sign-an-adaptive-form-heres-the-best-way-to-do-it-dc3e15f9b684)