---
title: 如何将Adobe Sign与AEM Forms集成？
description: 了解如何配置Adobe Sign [!DNL AEM Forms] as a Cloud Service?
feature: Adaptive Forms
role: User
level: Intermediate
exl-id: 609c3072-1c3d-43fa-898a-b4e62db8483b
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '983'
ht-degree: 0%

---

# 集成 [!DNL Adobe Sign] with [!DNL AEM Forms] as a Cloud Service  {#integrate-adobe-sign-with-aem-forms}

[!DNL Adobe Sign] 为自适应Forms启用电子签名工作流。 电子签名可改进工作流，以处理法律、销售、工资单、人力资源管理等许多领域的文档。

在 [!DNL Adobe Sign] 和自适应Forms方案中，用户填充自适应表单以申请服务。 例如，信用卡申请和公民福利表。 当用户填写、提交和签署申请表时，该表单将发送给服务提供商以进一步操作。 服务提供商审核应用程序和使用 [!DNL Adobe Sign] 来标记已批准的申请。 要启用类似的电子签名工作流，您可以集成 [!DNL Adobe Sign] with [!DNL AEM Forms].

使用 [!DNL Adobe Sign] with [!DNL AEM Forms]，配置 [!DNL Adobe Sign] 在AEM云服务中：

## 前提条件 {#prerequisites}

您需要满足以下条件才能集成 [!DNL Adobe Sign] with [!DNL AEM Forms]:

* 活动 [Adobe Sign开发人员帐户](https://acrobat.adobe.com/us/en/sign/developer-form.html).
* 安 [Adobe Sign API应用程序](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/create_app.md).
* 的凭据（客户端ID和客户端密钥） [!DNL Adobe Sign] API应用程序。
* 使用 [相同加密密钥](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security-checklist.html?lang=en#make-sure-you-properly-replicate-encryption-keys-when-needed) 用于创作和发布实例。
* （仅用于基于政府ID的身份验证） [启用身份验证方法](https://helpx.adobe.com/sign/using/adobesign-authentication-government-id.html#AuditReport) 用于政府ID身份验证。

## 配置 [!DNL Adobe Sign] with [!DNL AEM Forms] {#configure-adobe-sign-with-aem-forms}

在满足先决条件后，执行以下步骤以配置 [!DNL Adobe Sign] with [!DNL AEM Forms] 在创作实例上。

1. 在AEM Forms创作实例上，导航到 **[!UICONTROL 工具]** ![锤子](assets/hammer.png) > **[!UICONTROL 常规]** > **[!UICONTROL 配置浏览器]**.
1. 在 **[!UICONTROL 配置浏览器]** 页面，点按 **[!UICONTROL 创建]**.
1. 在 **[!UICONTROL 创建配置]** 对话框，指定 **[!UICONTROL 标题]** 对于配置，请启用 **[!UICONTROL 云配置]**，然后点按 **[!UICONTROL 创建]**. 它会创建一个用于存储Cloud Services的配置容器。 确保文件夹名称不包含任何空格。
1. 导航到 **[!UICONTROL 工具]** ![锤子](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Sign]** 并打开在上一步中创建的配置容器。

   >[!NOTE]
   >
   >创建自适应表单时，请在 **[!UICONTROL 配置容器]** 字段。

1. 在配置页面上，点按 **[!UICONTROL 创建]** 创建 [!DNL Adobe Sign]配置AEM Forms。
1. 在 **[!UICONTROL 常规]** 选项卡 **[!UICONTROL 创建Adobe Sign配置]** 页面，指定 **[!UICONTROL 名称]** 对于配置，请点按 **[!UICONTROL 下一个]**. 您可以选择指定 **[!UICONTROL 标题]** 并浏览以选择 **[!UICONTROL 缩略图]** ，以用于配置。

1. 将当前浏览器窗口中的URL复制到记事本。 需要URL才能配置 [!DNL Adobe Sign] 应用程序 [!DNL AEM Forms] 在后续步骤中。

1. 为 [!DNL Adobe Sign] 应用程序：

   1. 打开浏览器窗口并登录到 [!DNL Adobe Sign] 开发人员帐户。
   1. 选择为 [!DNL AEM Forms]，然后点按 **[!UICONTROL 为应用程序配置OAuth]**.
   1. 在 **[!UICONTROL 重定向URL]** 框中，添加在上一步中复制的URL并单击 **[!UICONTROL 保存]**.
   1. 为 [!DNL Adobe Sign] 应用程序并单击 **[!UICONTROL 保存]**.
   * [!DNL aggrement_read]
   * [!DNL aggrement_write]
   * [!DNL aggrement_send]
   * [!DNL widget_read]
   * [!DNL widget_write]
   * [!DNL workflow_read]

   有关为 [!DNL Adobe Sign] 应用程序和获取密钥，请参阅 [为应用程序配置oAuth设置](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/configure_oauth.md) 开发人员文档。

   ![OAuth配置](assets/oauthconfig_new.png)

1. 返回到 **[!UICONTROL 创建Adobe Sign配置]** 页面。 在 **[!UICONTROL 设置]** 选项卡 **[!UICONTROL OAuth URL]** 字段中会提及默认URL。 URL的格式为：

   `https://<shard>/public/oAuth/v2`

   例如：
   `https://secure.na1.echosign.com/public/oauth/v2`

   其中：

   **na1** 是指默认数据库共享。 您可以修改数据库共享的值。 确保 [!DNL Adobe Sign] 云配置指向 [正确共享](https://helpx.adobe.com/sign/using/identify-account-shard.html).

   如果您创建其他 [!DNL Adobe Sign] 配置Adobe Experience Manager功能或组件时，请确保 [!DNL Adobe Sign] 云配置指向同一个共享。

1. 指定 **[!UICONTROL 客户端ID]** （也称为应用程序ID）和 **[!UICONTROL 客户端密钥]**. 使用您在上一步中创建的Adobe Sign应用程序的客户端ID和客户端密钥。

1. 选择 **[!UICONTROL 为附件启用Adobe Sign]** 用于将附加到自适应表单的文件附加到相应 [!DNL Adobe Sign] 文档已发送以供签名。

1. 点按 **[!UICONTROL 连接到Adobe Sign]**. 提示输入凭据时，请提供创建时所用帐户的用户名和密码 [!DNL Adobe Sign] 应用程序。 当要求确认访问 `your developer account`，单击 **[!UICONTROL 允许访问]**. 如果凭据正确且允许 [!DNL AEM Forms] 访问 [!DNL Adobe Sign] 开发人员帐户中，将显示与以下内容类似的成功消息。

   ![Adobe Sign云配置成功](assets/adobe-sign-cloud-configuration-success.png)

1. 点按 **[!UICONTROL 创建]** 创建 [!DNL Adobe Sign] 配置。

1. 选择配置并单击 **[!UICONTROL 发布]**，选择配置，然后单击 **[!UICONTROL 发布]**. 它会将配置复制到相应的发布环境。

1. 对您的开发人员、暂存和生产实例（以左者为准）重复上述所有步骤以完成配置 [!DNL Adobe Sign] with [!DNL AEM Forms] 的URL。

现在，您可以 [使用将Adobe Sign字段添加到自适应表单](working-with-adobe-sign.md). 确保将用于Cloud Service的配置容器添加到要启用的所有自适应Forms [!DNL Adobe Sign]. 您可以从自适应表单的属性中指定配置容器。

## (仅限AEM工作流)配置 [!DNL Adobe Sign] 调度程序以同步签名状态 {#configure-adobe-sign-scheduler-to-sync-the-signing-status}

使用 [!DNL Adobe Sign] 工作流步骤：对自适应表单进行签名，表单可以依次传递给签名者，也可以同时发送给所有签名者，具体取决于工作流步骤的配置。 [!DNL Adobe Sign] 启用的Adaptive Forms仅在所有签名者完成签名过程后才会提交到Experience Manager Forms Server。

默认情况下， [!DNL Adobe Sign] 计划程序服务每24小时检查（轮询）签名者响应。 您可以更改环境的默认间隔。

要更改默认间隔，请指定 [cron表达式](https://en.wikipedia.org/wiki/Cron#CRON_expression) 对于 **sign.status.exp** 属性 **Adobe Sign配置服务** 配置。

例如，要每天00:00 am运行配置服务，请将 **sign.status.exp** 属性 **Adobe Sign配置服务** 配置 `0 0 0 1/1 * ? *`. 以下JSON文件显示了每天00:00 am运行配置服务的示例：

```json
{
  "sign.status.exp":"0 0 0 1/1 * ? *"
}
```

要设置配置的值， [使用AEM SDK生成OSGi配置](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#generating-osgi-configurations-using-the-aem-sdk-quickstart)和 [部署配置](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en#deployment-process) 到Cloud Service实例。

<!-- , perform the following steps:

1. Log in to [!DNL AEM Forms] Server with admin credentials and navigate to **[!UICONTROL Tools]** &gt;**[!UICONTROL Operations]** &gt; **[!UICONTROL Web Console]**.

   You can also open the following URL in a browser window:
   `https://server/system/console/configMgr`

1. Locate and open the **[!UICONTROL Adobe Sign Configuration Service]** option. Specify a [cron expression](https://en.wikipedia.org/wiki/Cron#CRON_expression) in the **Status Update Scheduler Expression** field and click **Save**. For example, to run the configuration service daily at 00:00 am, specify `0 0 0 1/1 * ? *` in the **Status Update Scheduler Expression** field.

Default interval to sync status of [!DNL Adobe Sign] is now changed. -->

## 相关文章 {#related-articles}

* [在自适应表单中使用Adobe Sign](working-with-adobe-sign.md)

* [将Adobe Sign与自适应Forms结合使用的最佳实践](https://medium.com/adobetech/using-adobe-sign-to-e-sign-an-adaptive-form-heres-the-best-way-to-do-it-dc3e15f9b684)
