---
title: 对邮件服务的OAuth2支持
description: Oauth2对Adobe Experience Manager as aCloud Service中邮件服务的支持
source-git-commit: 67c4aabea838c1430e43f5ebaa8a52ec55362936
workflow-type: tm+mt
source-wordcount: '674'
ht-degree: 0%

---


# OAuth2对邮件服务{#oauth2-support-for-the-mail-service}的支持

AEM as a Cloud Service为其集成的邮件服务提供了OAuth2支持，以便组织能够遵守安全的电子邮件要求。

您可以为多个电子邮件提供程序配置OAuth。 下面是配置AEM Mail Service以通过OAuth2与Microsoft Office 365 Outlook进行身份验证的分步说明。 其他供应商也可以以类似的方式进行配置。

有关AEM as a A Mail Service的更多信息，请参阅[发送电子邮件](/help/implementing/developing/introduction/development-guidelines.md#sending-email)。

## Microsoft Outlook {#microsoft-outlook}

1. 转到[https://portal.azure.com/](https://portal.azure.com/)并登录。
1. 在搜索栏中搜索&#x200B;**Azure Active Directory**&#x200B;并单击结果。 或者，您也可以直接浏览到[https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview)
1. 单击&#x200B;**应用程序注册** - **新建注册**

   ![](assets/oauth-outlook1.png)

1. 根据您的要求填写信息，然后单击&#x200B;**Register**
1. 转到新创建的应用程序，然后选择&#x200B;**API权限**
1. 转到&#x200B;**Add Permission** - **Graph Permission** - **Delegated Permissions**
1. 选择您的应用程序的以下权限，然后单击&#x200B;**添加权限**:
   * `SMTP.Send`
   * `Mail.Read`
   * `Mail.Send`
   * `openid`
   * `offline_access`
1. 转到&#x200B;**Authentication** - **添加平台** - **Web**，并在&#x200B;**Redirect Urls**&#x200B;部分中，添加以下URL — 一个带正斜杠，一个不带正斜杠：
   * `http://localhost/`
   * `http://localhost`
1. 添加每个URL后，按&#x200B;**配置**，并根据您的要求配置设置
1. 接下来，转到&#x200B;**Certificates and Secrets**，单击&#x200B;**New client secret**，然后按照屏幕上的步骤创建密钥。 请务必注意此密码，供以后使用
1. 在左窗格中按&#x200B;**Overview**，并复制&#x200B;**应用程序（客户端）ID**&#x200B;和&#x200B;**目录（租户）ID**&#x200B;的值，以供以后使用

要重新查看，您需要以下信息来在AEM端为Mail服务配置OAuth2:

* 身份验证URL，将使用租户ID构建。 它将具有以下表单：`https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/authorize`
* 令牌URL，将使用租户ID构建。 它将具有以下表单：`https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/token`
* 刷新URL，将使用租户ID构建。 它将具有以下表单：`https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/token`
* 客户端ID
* 客户端密钥

### 生成刷新令牌{#generating-the-refresh-token}

接下来，您需要生成刷新令牌，该令牌将在后续步骤中成为OSGi配置的一部分。

您可以按照以下步骤操作：

1. 将`clientID`和`tenantID`替换为特定于您帐户的值后，在浏览器中打开以下URL:`https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/authorize?client_id=<clientId>&response_type=code&redirect_uri=http://localhost&response_mode=query&scope=https%3A%2F%2Foutlook.office365.com%2FSMTP.Send%20EWS.AccessAsUser.All%20https%3A%2F%2Foutlook.office365.com%2FSMTP.Send%20https%3A%2F%2Foutlook.office365.com%2FMail.Read%20https%3A%2F%2Foutlook.office365.com%2FMail.Send%20openid%20offline_access&state=12345`
1. 在被要求时允许权限
1. 该URL将重定向到一个以下格式构建的新位置：`http://localhost/?code=<code>&state=12345&session_state=4f984c6b-cc1f-47b9-81b2-66522ea83f81#`
1. 复制上面示例中的`<code>`值
1. 使用以下cURL命令获取refreshToken。 您需要将tenantID、clientID和clientSecret替换为您帐户的值以及`<code>`的值：

   ```
   curl --location --request POST 'https://login.microsoftonline.com/<tenantId>/oauth2/v2.0/token' \
   --header 'Content-Type: application/x-www-form-urlencoded' \
   --header 'Cookie: buid=0.ARgAep0nU49DzUGmoP2wnvyIkcQjsx26HEpOnvHS0akqXQgYAAA.AQABAAEAAAD--DLA3VO7QrddgJg7Wevry9XPJSKbGVlPt5NWYxLtTl3K1W0LwHXelrffApUo_K02kFrkvmGm94rfBT94t25Zq4bCd5IM3yFOjWb3V22yDM7-rl112sLzbBQBRCL3QAAgAA; esctx=AQABAAAAAAD--DLA3VO7QrddgJg7Wevr4a8wBjYcNbBXRievdTOd15caaeAsQdXeBAQA3tjVQaxmrOXFGkKaE7HBzsJrzA-ci4RRpor-opoo5gpGLh3pj_iMZuqegQPEb1V5sUVQV8_DUEbBv5YFV2eczS5EAhLBAwAd1mHx6jYOL8LwZNDFvd2-MhVXwPd6iKPigSuBxMogAA; x-ms-gateway-slice=estsfd; stsservicecookie=estsfd; fpc=Auv6lTuyAP1FuOOCfj9w0U_5vR5dAQAAALDXP9gOAAAAwIpkkQEAAACT2T_YDgAAAA' \
   --data-urlencode 'client_id=<clientID>' \
   --data-urlencode 'scope=https://outlook.office365.com/SMTP.Send https://outlook.office365.com/Mail.Read https://outlook.office365.com/Mail.Send openid' \
   --data-urlencode 'redirect_uri=http://localhost' \
   --data-urlencode 'grant_type=authorization_code' \
   --data-urlencode 'client_secret=<clientSecret>' \
   --data-urlencode 'code=<code>'
   ```

1. 记下refreshToken和accessToken。

### 验证令牌{#validating-the-tokens}

在AEM端继续配置OAuth之前，请确保按以下过程验证accessToken和refreshToken :

1. 使用上一过程中生成的refreshToken生成accessToken。 您可以通过以下curl来实现此目的，它会替换`<client_id>`、`<client_secret>`和`<refreshToken>`的值：

   ```
   curl --location --request POST 'https://login.microsoftonline.com/<tenetId>/oauth2/v2.0/token' \
   --header 'Content-Type: application/x-www-form-urlencoded' \
   --header 'Cookie: buid=0.ARgAep0nU49DzUGmoP2wnvyIkcQjsx26HEpOnvHS0akqXQgYAAA.AQABAAEAAAD--DLA3VO7QrddgJg7Wevry9XPJSKbGVlPt5NWYxLtTl3K1W0LwHXelrffApUo_K02kFrkvmGm94rfBT94t25Zq4bCd5IM3yFOjWb3V22yDM7-rl112sLzbBQBRCL3QAAgAA; esctx=AQABAAAAAAD--DLA3VO7QrddgJg7Wevr4a8wBjYcNbBXRievdTOd15caaeAsQdXeBAQA3tjVQaxmrOXFGkKaE7HBzsJrzA-ci4RRpor-opoo5gpGLh3pj_iMZuqegQPEb1V5sUVQV8_DUEbBv5YFV2eczS5EAhLBAwAd1mHx6jYOL8LwZNDFvd2-MhVXwPd6iKPigSuBxMogAA; x-ms-gateway-slice=estsfd; stsservicecookie=estsfd; fpc=Auv6lTuyAP1FuOOCfj9w0U_IezHLAQAAAPeNSdgOAAAA' \
   --data-urlencode 'client_id=<client_id>' \
   --data-urlencode 'scope=https://outlook.office365.com/SMTP.Send https://outlook.office365.com/Mail.Read https://outlook.office365.com/Mail.Send openid' \
   --data-urlencode 'redirect_uri=http://localhost' \
   --data-urlencode 'grant_type=refresh_token' \
   --data-urlencode 'client_secret=<client_secret>' \
   --data-urlencode 'refresh_token=<refreshToken>'
   ```

1. 使用accessToken发送邮件，以查看是否正常工作。

>[!NOTE]
>
> 您可以从[此位置](https://docs.microsoft.com/en-us/azure/active-directory/develop/v2-oauth2-auth-code-flow)获取Postman API集合。

### 与AEM as aCloud Service集成{#integration-with-aem-as-a-cloud-service}

1. 使用以下语法在`/apps/<my-project>/osgiconfig/config`下创建名为`com.day.cq.mailer.oauth.impl.OAuthConfigurationProviderImpl.cfg.json`的OSGI属性文件：

   ```
   {
       authUrl: "<Authorization Url>",
       tokenUrl: "<Token Url>",
       clientId: "<clientID>",
       clientSecret: "$[secret:SECRET_SMTP_OAUTH_CLIENT_SECRET]",
       scopes: [
          "scope1",
          "scope2"
       ],
       refreshUrl: "<Refresh token Url>",
       refreshToken: "$[secret:SECRET_SMTP_OAUTH_REFRESH_TOKEN]"
   }
   ```

1. 按照上一节所述，通过构建`authUrl`、`tokenUrl`和`refreshURL`来填写。
1. 将以下作用域添加到配置中：
   * `openid`
   * `offline_access`
   * `https://outlook.office365.com/Mail.Send`
   * `https://outlook.office365.com/Mail.Read`
   * `https://outlook.office365.com/SMTP.Send`
1. 创建OSGI属性文件`called com.day.cq.mailer.impl.DefaultMailService.cfg.json`
在 
`/apps/<my-project>/osgiconfig/config`  使用以下语法：

   ```
   {
    "smtp.host": "<smtp hostname>"
    "smtp.user": "<user account that logged into get the oauth tokens>",
    "smtp.password": "value not used",
    "smtp.port": 587,
    "from.address": "<from address used for sending>"
    "smtp.ssl": false,
    "smtp.starttls": true,
    "smtp.requiretls": true,
    "debug.email": false,
    "oauth.flow": true
   }
   ```

1. 对于outlook，`smtp.host`配置值为`smtp.office365.com`
1. 在运行时，使用Cloud Manager变量API传递`refreshToken values`和`clientSecret`密钥，如[此处](/help/implementing/deploying/configuring-osgi.md#setting-values-via-api)所述。 应定义变量`SECRET_SMTP_OAUTH_REFRESH_TOKEN`和`SECRET_SMTP_OAUTH_CLIENT_SECRET`的值。

### 疑难解答 {#troubleshooting}

如果邮件服务无法正常运行，您在大多数情况下将需要按如上所述重新生成`refreshToken`，并通过Cloud Manager API传递新值。 部署新值需要几分钟时间。
