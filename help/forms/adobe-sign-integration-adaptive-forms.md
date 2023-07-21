---
title: 如何将Adobe Acrobat Sign与AEM Forms集成？
description: 了解如何为配置Adobe Acrobat Sign [!DNL AEM Forms] as a Cloud Service？
feature: Adaptive Forms
role: User
level: Intermediate
source-git-commit: 8c125d834ebfff5601f56646d59ce00a80fcc0ba
workflow-type: tm+mt
source-wordcount: '1943'
ht-degree: 31%

---

# Connect [!DNL AEM Forms] as a Cloud Service于 [!DNL Adobe Acrobat Sign] {#integrate-adobe-sign-with-aem-forms}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/adobe-sign-integration-adaptive-forms.html#adobe-acrobat-sign-for-government) |
| AEM as a Cloud Service | 本文 |

[!DNL Adobe Acrobat Sign] 为自适应Forms和AEM工作流启用电子签名工作流。 电子签名改进了法律、销售、工资单、人力资源管理和其他许多方面的文档的处理工作流。

在典型的 [!DNL Adobe Acrobat Sign] 和自适应表单方案中，用户需填写自适应表单来申请服务。例如，信用卡申请表和公民权益表。在用户填写、签署和提交申请表后，该表将发送给服务提供商以执行后续操作。服务提供商将审核申请，并使用 [!DNL Adobe Acrobat Sign] 将申请标记为已批准。AEM Forms支持Adobe Acrobat Sign和Adobe Acrobat Sign Solutions政府版。 根据您的许可证和要求，您可以将AEM Forms与以下任一解决方案集成或连接：

* [将AEM Forms与Adobe Acrobat Sign连接](#adobe-sign)
* [将AEM Forms与适用于政府的Adobe Acrobat Sign Solutions连接](#adobe-acrobat-sign-for-government)

## 将AEM Forms与Adobe Acrobat Sign连接 {#adobe-sign}

连接 **[!DNL AEM Forms]** 替换为 **[!DNL Adobe Acrobat Sign]**，设置先决条件部分中列出的软件和帐户，并在您的Formsas a Cloud Service创作和发布实例中配置Adobe Sign Cloud Service：

### 将AEM Forms与Adobe Acrobat Sign连接的先决条件 {#prerequisites-for-adobe-sign}

您需要以下设置才能集成 [!DNL Adobe Acrobat Sign] 替换为 [!DNL AEM Forms]：

1. 活动 [Adobe Acrobat Sign开发人员帐户](https://acrobat.adobe.com/us/en/sign/developer-form.html).
1. An [Adobe Acrobat Sign API应用程序](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/create_app.md).
1. [!DNL Adobe Acrobat Sign] API 应用程序的凭据（客户端 ID 和客户端密码）。
1. （仅适用于基于Government ID的身份验证） [启用身份验证方法](https://helpx.adobe.com/sign/using/adobesign-authentication-government-id.html#AuditReport) 用于政府ID身份验证。



### 将AEM Forms创作和发布实例与Adobe Acrobat Sign连接 {#configure-adobe-sign-with-aem-forms}

满足前提条件后，执行以下步骤以在创作实例上使用 [!DNL AEM Forms] 配置 [!DNL Adobe Acrobat Sign]。

1. 在AEM Forms创作实例上，导航到 **[!UICONTROL 工具]** ![锤子](assets/hammer.png) > **[!UICONTROL 常规]** > **[!UICONTROL 配置浏览器]**.
1. 在 **[!UICONTROL 配置浏览器]** 页面，点按 **[!UICONTROL 创建]**.
1. 在 **[!UICONTROL 创建配置]** 对话框，请指定 **[!UICONTROL 标题]** 对于配置，启用 **[!UICONTROL 云配置]**，然后点按 **[!UICONTROL 创建]**. 系统创建一个配置容器来存储 Cloud Services。确保文件夹名称不包含任何空格。
1. 导航到 **[!UICONTROL 工具]** ![锤子](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Acrobat Sign]** 并打开您在上一步中创建的配置容器。

   >[!NOTE]
   >
   >创建自适应表单时，请在 **[!UICONTROL 配置容器]** 字段。

1. 在配置页面上，点按 **[!UICONTROL 创建]** 创建 [!DNL Adobe Acrobat Sign] AEM Forms配置。
1. 在 **[!UICONTROL 常规]** 的选项卡 **[!UICONTROL 创建Adobe Acrobat Sign配置]** 页面，指定 **[!UICONTROL 名称]** ，然后点按 **[!UICONTROL 下一个]**. 您可以选择指定 **[!UICONTROL 标题]** 并浏览以选择 **[!UICONTROL 缩略图]** 用于配置。

1. 现在您可以 **[!UICONTROL 选择解决方案]** 以选择 [!DNL Adobe Acrobat Sign].

   ![Adobe Acrobat Sign Solutions政府版](assets/adobe-sign-solution.png)

1. 将当前浏览器窗口中显示的URL复制到记事本并删除部分 `/ui#/aem` 从URL访问。 然后，需要修改的URL才能配置 [!DNL Adobe Acrobat Sign] 应用程序 [!DNL AEM Forms]，在后续步骤中。 点按 **[!UICONTROL 下一个]**.

1. 在 **[!UICONTROL 设置]** 选项卡， **[!UICONTROL OAuth URL]** 字段包含默认URL。 URL 的格式为：

   `https://<shard>/public/oAuth/v2`

   例如：
   `https://secure.na1.echosign.com/public/oauth/v2`

   其中：

   **na1** 指默认数据库分片。您可以修改数据库分片的值。确保 [!DNL  Adobe Acrobat Sign] 云配置指向[正确分片](https://helpx.adobe.com/sign/using/identify-account-shard.html)。

   如果为 Adobe Experience Manager 功能或组件创建另一个 [!DNL Adobe Acrobat Sign] 配置，请确保所有 [!DNL Adobe Acrobat Sign] 云配置指向同一分片。

   >[!NOTE]
   >
   > 保留 **创建Adobe Acrobat Sign配置** 页面打开。 不要关闭它。 您可以检索 **客户端ID** 和 **客户端密码** 在为配置OAuth设置后 [!DNL Adobe Acrobat Sign] 应用程序（如即将执行的步骤中所述）。


1. 配置 [!DNL Adobe Acrobat Sign] 应用程序的 OAuth 设置：

   1. 打开浏览器窗口，并登录到您的 [!DNL Adobe Acrobat Sign] 开发人员帐户。
   1. 选择为配置的应用程序 [!DNL AEM Forms]，然后点按 **[!UICONTROL 为应用程序配置OAuth]**.
   1. 在 **[!UICONTROL 重定向URL]** 框中，添加在上一步（步骤8）中复制的URL并单击 **[!UICONTROL 保存]**.
   1. 为以下内容启用以下范围 [!DNL Adobe Acrobat Sign] 应用程序并单击 **[!UICONTROL 保存]**.

   * [!DNL aggrement_read]
   * [!DNL aggrement_write]
   * [!DNL aggrement_send]
   * [!DNL widget_read]
   * [!DNL widget_write]
   * [!DNL workflow_read]

   有关为 [!DNL Adobe Acrobat Sign] 应用程序配置 OAuth 设置并获取密钥的分步信息，请参阅[为应用程序配置 OAuth 设置](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/configure_oauth.md)开发人员文档。

   ![OAuth 配置](assets/oauthconfig_new.png)

1. 返回至 **[!UICONTROL 创建Adobe Acrobat Sign配置]** 页面。 在 **[!UICONTROL 设置]** 选项卡，指定[**[!UICONTROL 客户端ID]** （也称为应用程序ID）和 **[!UICONTROL 客户端密码]**]。 使用 [Adobe Acrobat Sign应用程序的客户端ID和客户端密码](https://opensource.adobe.com/acrobat-sign/developer_guide/helloworld.html#get-the-app-id-and-secret) 您在上一步中创建了。

1. 选择 **[!UICONTROL 为附件启用Adobe Acrobat Sign]** 用于将附加到自适应表单的文件追加到相应表单的选项 [!DNL Adobe Acrobat Sign] 文档已发送供签名。

1. 点按 **[!UICONTROL 连接到Adobe Acrobat Sign]**. 在系统提示输入凭据时，提供 **用户名** 和 **密码** 创建时使用的帐户的 [!DNL Adobe Acrobat Sign] 应用程序。 当要求确认时，访问 `your developer account`，单击 **[!UICONTROL 允许访问]**. 如果凭据正确，并且您允许 [!DNL AEM Forms] 访问您的 [!DNL Adobe Acrobat Sign] 开发人员帐户，系统会显示一条与以下内容类似的成功消息。

   ![Adobe Acrobat Sign云配置成功](assets/adobe-sign-cloud-configuration-success.png)

1. 点按 **[!UICONTROL 创建]** 创建 [!DNL Adobe Acrobat Sign] 配置。

1. 选择配置并单击 **[!UICONTROL Publish]**，选择配置，然后单击 **[!UICONTROL Publish]**. 这会将配置复制到相应的发布环境。

1. 在开发人员实例、暂存实例和生产实例（以剩下的实例为准）上重复上述所有步骤以使用 [!DNL AEM Forms] 为环境配置 [!DNL Adobe Acrobat Sign]。

现在，您可以 [使用将Adobe Acrobat Sign字段添加到自适应表单](working-with-adobe-sign.md). 确保将用于 Cloud Service 的配置容器添加到为 [!DNL Adobe Acrobat Sign] 启用的所有自适应表单。您可以在自适应表单的属性中指定配置容器。

## 将AEM Forms与适用于政府的Adobe Acrobat Sign Solutions连接 {#adobe-acrobat-sign-for-government}

将AEM Forms与面向政府的Adobe Acrobat Sign Solutions连接是一个多步骤的过程。 它涉及：

* 为您的AEM实例创建重定向URL
* 与适用于政府团队的Adobe Sign解决方案共享重定向URL和范围
* 从Adobe Sign团队接收凭据
* 使用收到的凭据将AEM Forms与适用于政府的Adobe Acrobat Sign Solutions连接

![Adobe Sign政府工作流程](/help/forms/assets/adobe-acrobat-sign-govt-workflow.png)


AEM Formsas a Cloud Service提供开发、暂存和生产环境。 您可以开始将的开发环境与适用于政府的Adobe Acrobat Sign Solutions连接，并在以后连接暂存环境和生产环境。

### 开始之前 {#prerequisites-for-adobe-sign-for-acrobat-sign-for-government}

在开始将AEM Forms与Adobe Acrobat Sign解决方案连接之前，请确保 [Adobe Acrobat Sign Solutions政府版](https://opensource.adobe.com/acrobat-sign/signgov/gstarted.html#account-provisioning) 已配置帐户。


### 将AEM Formsas a Cloud Service与适用于政府的Adobe Acrobat Sign Solutions连接 {#connect-adobe-acrobat-sign-for-government}

#### 为您的AEM实例创建重定向URL

1. 在Formsas a Cloud Service创作实例上，导航到 **[!UICONTROL 工具]** ![锤子](assets/hammer.png) > **[!UICONTROL 常规]** > **[!UICONTROL 配置浏览器]**.
1. 在 **[!UICONTROL 配置浏览器]** 页面，点按 **[!UICONTROL 创建]**.
1. 在 **[!UICONTROL 创建配置]** 对话框，请指定 **[!UICONTROL 标题]** 对于配置，启用 **[!UICONTROL 云配置]**，然后点按 **[!UICONTROL 创建]**. 系统创建一个配置容器来存储 Cloud Services。确保文件夹名称不包含任何空格。
1. 导航到 **[!UICONTROL 工具]** ![锤子](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Acrobat Sign]** 并打开您在上一步中创建的配置容器。 创建自适应表单时，请在 **[!UICONTROL 配置容器]** 字段。
1. 在配置页面上，点按 **[!UICONTROL 创建]** 创建 [!DNL Adobe Acrobat Sign] AEM Forms配置。
1. 将当前浏览器窗口的URL复制到记事本并删除 `/ui#/aem` 从URL访问。 此URL称为 `re-direct URL`. 在下一部分中，您共享 `re-direct URL` 和 `Scopes` 包含Adobe Sign团队和请求凭据（客户端ID和客户端密钥）。


#### 与Adobe Sign团队共享重定向URL和作用域并接收凭据

Adobe Acrobat Sign政府解决方案团队要求 `re-direct URL` 以及要为您的Adobe Acrobat Sign应用程序启用的特定范围（如下所列），以生成凭据（客户端ID和客户端密钥），从而允许您将AEM Forms与适用于政府的Adobe Acrobat Sign Solutions连接。

共享 `scopes` （如下所列）和 `re-direct URL` 与您的Adobe Acrobat Sign政府解决方案代表([Adobe Professional Services团队成员](https://opensource.adobe.com/acrobat-sign/signgov/gstarted.html#password))。

**_范围_**

* [!DNL aggrement_read]
* [!DNL aggrement_write]
* [!DNL aggrement_send]
* [!DNL widget_read]
* [!DNL widget_write]
* [!DNL workflow_read]
* [!DNL offline_access]

该代表会生成凭据并与您共享。 在下一部分中，您将使用凭据（客户端ID和客户端密钥）将AEM Forms与用于政府管理的Adobe Acrobat Sign Solutions连接。

#### 使用收到的凭据将AEM Forms与适用于政府的Adobe Acrobat Sign Solutions连接

1. 打开 `re-direct URL` 在浏览器中。 您已创建并记下 `re-direct URL` 在 [在您的AEM实例上创建重定向URL](#create-redirect-url) 部分。

1. 在 **[!UICONTROL 常规]** 的选项卡 **[!UICONTROL 创建Adobe Sign配置]** 页面，指定 **[!UICONTROL 名称]** ，然后点按 **[!UICONTROL 下一个]**. 您可以选择指定 **[!UICONTROL 标题]** 并浏览以选择 **[!UICONTROL 缩略图]** 用于配置。 单击&#x200B;**[!UICONTROL 下一步]**。

1. 在 **[!UICONTROL 设置]** 的选项卡 **[!UICONTROL 创建Adobe Sign配置]** 页面，用于 **[!UICONTROL 选择解决方案]** 选项，选择 [!DNL Adobe Acrobat Sign Solutions for Government].

   ![Adobe Acrobat Sign Solutions政府版](assets/adobe-sign-for-govt.png)

1. 在 **[!UICONTROL 电子邮件]** 字段，为政府帐户指定与您的Adobe Acrobat Sign Solutions关联的电子邮件地址。

1. 此 **[!UICONTROL OAuth URL]** 字段指定Adobe Sign数据库分片。 字段包含默认URL。 请勿更改URL。

1. 使用Adobe Acrobat Sign为政府解决方案代表共享的凭据([Adobe Professional Services团队成员])在上一部分中作为[**[!UICONTROL 客户端ID]** 和 **[!UICONTROL 客户端密码]**]。

1. 选择 **[!UICONTROL 为附件启用Adobe Acrobat Sign]** 用于将附加到自适应表单的文件追加到相应表单的选项 [!DNL Adobe Acrobat Sign] 文档已发送供签名。

1. 点按 **[!UICONTROL 连接到Adobe Sign]**. 在系统提示输入凭据时，提供在创建 [!DNL Adobe Acrobat Sign] 应用程序时所用帐户的用户名和密码。当要求确认访问时 `your developer account`，单击 **[!UICONTROL 允许访问]**. 如果凭据正确，并且您允许 [!DNL AEM Forms] 访问您的 [!DNL Adobe Acrobat Sign] 开发人员帐户，系统会显示一条与以下内容类似的成功消息。

   ![Adobe Acrobat Sign云配置成功](assets/adobe-sign-cloud-configuration-success.png)

   <!-- > When prompted for credentials, provide username and password of the account used while creating [!DNL Adobe Acrobat Sign] application. When asked to confirm access for `your developer account`, Click **[!UICONTROL Allow Access]**. -->

1. 点按 **[!UICONTROL 创建]** 以创建配置。

1. 选择配置并单击 **[!UICONTROL Publish]**，选择配置，然后单击 **[!UICONTROL Publish]**. 它会将配置复制到相应的发布环境。

1. 在开发人员实例、暂存实例和生产实例（以剩下的实例为准）上重复上述所有步骤以使用 [!DNL AEM Forms] 为环境配置 [!DNL Adobe Acrobat Sign Solutions for Government]。

现在，您可以 [在自适应表单中添加字段Adobe Acrobat Sign](working-with-adobe-sign.md) 或 [AEM Workflow](/help/forms/aem-forms-workflow-step-reference.md#sign-document-step-sign-document-step). 确保将用于Cloud Service配置的配置容器添加到启用的所有自适应Forms [!DNL Adobe Acrobat Sign]. 您可以在自适应表单的属性中指定配置容器。

## （仅适用于 AEM Workflow）配置 [!DNL Adobe Acrobat Sign] 调度程序以同步签名状态 {#configure-adobe-sign-scheduler-to-sync-the-signing-status}

在使用 [!DNL Adobe Acrobat Sign] Workflow 步骤对自适应表单进行签名时，可以将表单逐个传送给签名者，也可以将表单同时发送给所有签名者，具体取决于工作流步骤的配置。仅在所有签名者完成签名过程后，[!DNL Adobe Acrobat Sign] 支持的自适应表单才提交到 Experience Manager Forms Server。

默认情况下，[!DNL Adobe Acrobat Sign] 调度程序服务每 24 小时检查（轮询）一次签名者响应。您可以为您的环境更改此默认间隔。

要更改默认间隔，请指定 [cron表达式](https://en.wikipedia.org/wiki/Cron#CRON_expression) 对于 **sign.status.exp** 的属性 **Adobe Acrobat Sign配置服务** 配置。

例如，要在每天凌晨00:00运行配置服务，请将 **sign.status.exp** 的属性 **Adobe Acrobat Sign配置服务** 要指定的配置 `0 0 0 1/1 * ? *`. 以下 JSON 文件显示了每天凌晨 00:00 运行配置服务的示例：

```json
{
  "sign.status.exp":"0 0 0 1/1 * ? *"
}
```

要设置配置的值，请[使用 AEM SDK 生成 OSGi 配置](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#generating-osgi-configurations-using-the-aem-sdk-quickstart)，并向 Cloud Service 实例[部署配置](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en#deployment-process)。


## 相关文章 {#related-articles}

* [在自适应表单中使用Adobe Acrobat Sign](working-with-adobe-sign.md)

* [将Adobe Acrobat Sign与自适应Forms结合使用的最佳实践](https://medium.com/adobetech/using-adobe-sign-to-e-sign-an-adaptive-form-heres-the-best-way-to-do-it-dc3e15f9b684)
