---
title: 在发布层上为AEM as a Cloud Service打开ID Connect支持
description: 了解如何在发布层上为AEM as a Cloud Service设置Open ID Connect (OIDC)
feature: Security
role: Admin
exl-id: d2f30406-546c-4a2f-ba88-8046dee3e09b
source-git-commit: bf35f847f6f00d21915dfedb10cf38ea74344988
workflow-type: tm+mt
source-wordcount: '1469'
ht-degree: 0%

---

# 在发布层上为AEM as a Cloud Service打开ID Connect支持

## 简介 {#introduction}

随着企业实现数字体验的现代化，安全且可扩展的身份管理成为一项基本要求。 Adobe Experience Manager (AEM) Cloud Service现在在发布层支持OpenID Connect (OIDC)，从而允许与领先的身份提供程序(IdP)进行基于标准的无缝集成，例如Entra ID (Azure AD)、Google、Okta、Auth0、Ping Identity、ForgeRock和OIDC支持的IDP。

OIDC是在OAuth 2.0协议之上的标识层，它支持强大的用户身份验证，同时保持开发人员的简单性。 它广泛用于B2C、Intranet和合作伙伴门户方案，在这些方案中，需要安全的用户登录和身份联合。

此前，AEM客户负责在发布层上实施自己的自定义登录逻辑，这会增加开发时间并带来长期维护和安全挑战。 凭借对OIDC的本机支持，AEM Cloud Service通过为访问Publish环境的最终用户提供安全、可扩展且受Adobe支持的身份验证机制来消除此负担。

无论您是提供个性化的消费者网站还是经过身份验证的内部门户，OIDC on Publish都可通过集中化的身份治理简化身份联合并降低风险。 它还帮助企业在不牺牲灵活性的情况下满足现代合规性和安全标准。

## 为OIDC身份验证配置AEM {#configure-aem-oidc-authentication}

### 先决条件 {#prerequisits}

我们假定以下信息可用或已定义：

1. AEM存储库中受保护内容的路径
1. 要配置的IdP的标识符。 这可以是任意字符串

来自IdP配置的信息：

1. IdP中配置的客户端ID
1. 在Idp中配置的客户端密钥。 如果在Idp上配置了PKCE，则客户端密钥不可用。 请勿将纯文本值存储在配置文件中。 使用CM密钥并引用它
1. 在Idp上配置的范围。 必须至少提供作用域`openid`
1. IdP上是否启用了PKCE
1. `callbackUrl`是使用在点1定义的配置路径之一并添加后缀定义的： `/j_security_check`
1. 用于访问标准`baseUrl`文件的`.well-known`。 例如，如果已知的URL是： `https://login.microsoftonline.com/53279d7a-438f-41cd-a6a0-fdb09efc8891/v2.0/.well-known/openid-configuration`，`baseUrl`是： `https://login.microsoftonline.com/53279d7a-438f-41cd-a6a0-fdb09efc8891`

### 配置文件概述 {#overview-of-the-configuration-files}

在下方查找需要配置的文件列表：

1. **OIDC连接**： `OidcAuthenticationHandler`将使用此连接对用户进行身份验证，或其他组件将使用此连接来[使用OAuth授权访问受IdP保护的资源](https://github.com/apache/sling-org-apache-sling-auth-oauth-client)
1. **OIDC身份验证处理程序**：这是用于验证访问所配置路径的用户身份的身份验证处理程序
1. **UserInfoProcessor**：此组件处理IdP收到的信息。 客户可以对其进行扩展以实施自定义逻辑
1. [**默认同步处理程序**](https://jackrabbit.apache.org/oak/docs/security/authentication/external/defaultusersync.html)：此组件在存储库中创建用户
1. [**ExternalLoginModule**](https://jackrabbit.apache.org/oak/docs/security/authentication/externalloginmodule.html)：此组件对本地oak存储库中的用户进行身份验证。

下图显示了上述配置元素的链接方式。 请注意，由于这些组件是`ServiceFactory`组件，`~uniqueid`可以是任何随机唯一字符串：

![OIDC配置图](/help/security/assets/oidc-diagram.png)

### 配置OIDC连接 {#configure-the-oidc-connection}

首先，我们需要配置OIDC连接。 可以配置多个OIDC连接，并且每个连接必须有不同的名称。

1. 创建将包含配置的新`.cfg.json`文件。 例如，您可以使用`org.apache.sling.auth.oauth_client.impl.OidcConnectionImpl~azure.cfg.json` - **azure**&#x200B;后缀必须是连接的唯一标识符
1. 请遵循以下示例中的配置格式：

   ```
   {
    "name":"azure",
    "scopes":[
      "openid"
    ],
    "baseUrl":"<https://login.microsoftonline.com/53279d7a-438f-41cd-a6a0-fdb09efc8891/v2.0>",
    "clientId":"5199fc45-8000-473e-ac63-989f1a78759f",
    "clientSecret":"xxxxxx"
   }
   ```

1. 按如下方式配置其属性：
   * **“名称”**&#x200B;可由用户定义
   * `baseUrl`、`clientid`和`clientSecret`是来自IdP的配置值。
   * 范围必须至少包含值`openid`。

### 配置OIDC身份验证处理程序 {#configure-oidc-authentication-handler}

现在，配置OIDC身份验证处理程序。 可以配置多个OIDC连接。 每个都必须使用不同的名称。 如果他们共享相同的[OAK外部身份提供程序](https://jackrabbit.apache.org/oak/docs/security/authentication/identitymanagement.html)，则可以共享用户。

1. 创建配置文件。 对于此示例，我们将使用`org.apache.sling.auth.oauth_client.impl.OidcConnectionImpl~azure.cfg.json`。 `azure`后缀必须是唯一标识符。 请参阅下面的配置文件示例：

   ```
   {
     "path":"/content/tests/us/en/test-7",
     "callbackUri":"http://localhost:14503/content/tests/us/en/test-7/j_security_check",
     "pkceEnabled":false,
     "defaultConnectionName":"azure"
     "idp": "azure-idp"
   }
   ```

1. 然后，按如下方式配置其属性：
   * `path`：要保护的路径
   * `callbackUri`：到要保护的路径，添加后缀： `/j_security_check`
   * `defaultConnectionName`：使用在上一步中为OIDC连接定义的相同名称进行配置+
   * `pkceEnabled`：授权代码流上代码交换(PKCE)的`true`验证密钥
   * `idp`： [OAK外部标识提供程序](https://jackrabbit.apache.org/oak/docs/security/authentication/identitymanagement.html)的名称。 请注意，其他OAK IDP不能共享用户或组

### 配置SlingUserInfoProcessor

1. 创建配置文件。 对于此示例，我们将使用`org.apache.sling.auth.oauth_client.impl.SlingUserInfoProcessor~azure.cfg.json`。 `azure`后缀必须是唯一标识符。 请参阅下面的配置文件示例：

   ```
   {
      "groupsInIdToken":true,
      "groupsClaimName": "groups",
      "connection":"azure",
      "storeAccessToken": false,
      "storeRefreshToken": false
   }
   ```

1. 然后，按如下方式配置其属性：
   * `groupsInIdToken`：如果在ID令牌中发送组，则设置为true。 如果值为false或未指定，则从UserInfo端点读取组。
   * `groupsClaimName`：声明的名称包含要在AEM中同步的组。
   * `connection`：使用在上一步中为OIDC连接定义的相同名称进行配置
   * `storeAccessToken`：如果访问令牌必须存储在存储库中，则为true。 默认情况下，这是false。 仅当AEM需要代表受同一IdP保护的外部服务器中存储的用户访问资源时，才应将其设置为true。
   * `storeRefreshToken`：如果刷新令牌必须存储在存储库中，则为true。 默认情况下，这是false。 仅当AEM需要代表存储在受同一IdP保护的外部服务器中的用户访问资源并需要从IdP刷新令牌时，才将其设置为true。
请注意，访问令牌和刷新令牌已使用AEM主密钥加密存储。


### 配置同步处理程序 {#configure-the-synchronization-handler}

必须至少配置一个同步处理程序，才能同步在oak中经过身份验证的用户。 有关更多详细信息，请参阅[此](https://jackrabbit.apache.org/oak/docs/security/authentication/external/defaultusersync.html)页面。

创建名为`org.apache.jackrabbit.oak.spi.security.authentication.external.impl.DefaultSyncHandler~azure.cfg.json`的文件。 **azure**&#x200B;后缀必须是唯一标识符。 有关如何配置其属性的更多信息，请参阅[Oak用户和组同步文档](https://jackrabbit.apache.org/oak/docs/security/authentication/external/defaultusersync.html)。 请查找以下示例配置：

```
{
  "user.expirationTime":"300s",
  "user.membershipExpTime":"300s",
  "user.propertyMapping":[
    "profile/familyName=profile/familyName",
    "profile/givenName=profile/givenName",
    "rep:fullname=cn",
    "profile/email=profile/email",
    "oauth-tokens"
  ],
  "user.pathPrefix":"azure",
  "handler.name":"azure"
}
```

下面是在DefaultSyncHandler中配置的一些最相关的属性。 请注意，应始终在Cloud Services中启用动态组成员资格。

| 属性名称 | 注释 | 建议值 |
|---|---|---|
| `user.expirationTime` | 同步用户过期之前的持续时间。 仅在过期时间后同步用户。 | 1h |
| `user.membershipExpTime` | 同步的用户成员资格过期之前的持续时间。 只有在过期时间之后，才会同步用户成员资格。 | 1h |
| `user.dynamicMembership` | 我们建议启用动态组成员资格 | true |
| `user.enforceDynamicMembership` | 我们建议启用动态组成员资格的实施 | true |
| `group.dynamicGroups` | 我们建议启用动态组 | true |
| user.propertyMapping | 提供的`UserInfoProcessor`实现仅同步少数几个属性。 它可以被修改和定制。 | <code>&quot;profile/givenName=profile/given_name&quot;，</code><br><code>&quot;profile/familyName=profile/family_name&quot;，</code><br><code>&quot;rep:fullname=profile/name&quot;，</code><br><code>&quot;profile/email=profile/email&quot;，</code><br><code>&quot;access_token=access_token&quot;，</code><br><code>&quot;refresh_token=refresh_token&quot;</code> |  |
| `user.membershipNestingDepth` | 同步成员关系时返回组嵌套的最大深度。 如果值为0，则实际上禁用组成员资格查找。 值为1仅添加用户的直接组。 只有在同步用户成员资格祖先时，才同步各个组时，此值无效。 | 1 |

### 配置外部登录模块 {#configure-the-external-login-module}

最后，您需要配置外部登录模块。

1. 创建名为`org.apache.jackrabbit.oak.spi.security.authentication.external.impl.ExternalLoginModuleFactory~azure.cfg.json`的文件。 请参阅下面的示例配置：

   ```
   {
    "sync.handlerName":"azure",
    "idp.name":"azure-idp"
   }
   ```

1. 按如下方式配置其属性：

   * `sync.handlerName`：先前定义的同步处理程序的名称
   * `idp.name`：在OIDC身份验证处理程序中定义的OAK身份提供程序

### 可选：实施自定义UserInfoProcessor {#implement-a-custom-userinfoprocessor}

用户通过ID令牌进行身份验证，并在为IdP定义的`userInfo`端点中获取其他属性。 如果必须执行其他非标准操作，则[UserInfoProcessor](https://github.com/apache/sling-org-apache-sling-auth-oauth-client/blob/master/src/main/java/org/apache/sling/auth/oauth_client/impl/SlingUserInfoProcessorImpl.java)的自定义实现是Sling的默认实现。

## 示例：使用Azure Active Directory配置OIDC身份验证

### 在Azure Active Directory中配置新应用程序 {#configure-a-new-application-in-azure-ad}

1. 按照[Azure Active Directory文档](https://learn.microsoft.com/en-us/power-pages/security/authentication/openid-settings#create-an-app-registration-in-azure)在Azure Active Directory中创建新应用程序。  请参阅下面详细说明应用程序概述的屏幕的外观：

   ![应用程序概述](/help/security/assets/odic-application-overview.png)

1. 如果需要组或应用程序角色，请按照[文档](https://learn.microsoft.com/en-us/entra/external-id/customers/how-to-use-app-roles-customers)为应用程序启用它们，并在ID令牌中发送它们。 以下是已配置组的示例：

![OIDC声明令牌ID](/help/security/assets/oidc-claim-id-token.png)

1. 按照以前记录的步骤创建所需的配置文件。 以下是特定于Azure AD的示例，其中：
   * 我们将oidc连接、身份验证处理程序和DefaultSyncHandler的名称定义为： `azure`
   * 网站URL为： `www.mywebsite.com`
   * 我们保护路径`/content/wknd/us/en/adventures`
   * 租户为： `tennat-id`，
   * 客户端ID为： `client-id`，
   * 密码为： `secret`，
   * 这些组在名为`groups`的声明中的ID令牌中发送

#### org.apache.sling.auth.oauth_client.impl.OidcConnectionImpl~azure.cfg.json

```
{
  "name":"azure",
  "scopes":[
    openid", "User.Read", "profile", "email
  ],
  "baseUrl":"https://login.microsoftonline.com/tenant-id/v2.0",
  "clientId":"client-id",
  "clientSecret":"secret"
}
```

#### org.apache.sling.auth.oauth_client.impl.OidcAuthenticationHandler~azure.cfg.json

```
{
  "callbackUri":"https://www.mywebsite.com/content/wknd/us/en/adventures/j_security_check",
  "path":[
    "/content/wknd/us/en/adventures"
  ],
  "idp":"azure",
  "defaultConnectionName":"azure"
}
```

#### org.apache.jackrabbit.oak.spi.security.authentication.external.impl.ExternalLoginModuleFactory~azure.cfg.json

```
{
  "sync.handlerName":"azure",
  "idp.name":"azure"
}
```

#### org.apache.jackrabbit.oak.spi.security.authentication.external.impl.DefaultSyncHandler~azure.cfg.json

```
{
  "user.expirationTime":"1s",
  "user.membershipExpTime":"1s",
  "user.propertyMapping":[
    "profile/givenName=profile/given_name",
    "profile/familyName=profile/family_name",
    "rep:fullname=profile/name",
    "profile/email=profile/email",
    "access_token=access_token",
    "refresh_token=refresh_token"
  ],
  "user.pathPrefix":"azure",
  "group.pathPrefix": "oidc",
  "user.membershipNestingDepth": "1",
  "handler.name":"azure"
}
```

#### org.apache.sling.auth.oauth_client.impl.SlingUserInfoProcessorImpl~azure.cfg.json

```
{
  "groupsInIdToken": "true",
  "storeAccessToken": "false",
  "storeRefreshToken": "false",
  "connection": "azure",
  "groupsClaimName": "groups"
}
```

### 有关Azure AD组的其他信息 {#additional-information-about-azure-ad-groups}

若要在Microsoft Azure门户中为企业应用程序配置组，您需要在&#x200B;**企业应用程序**&#x200B;上搜索该应用程序，并添加组： <!-- Alexandru: this bit cound be clearer-->

![OIDC组添加](/help/security/assets/oidc-ad-additional-info.png)

要在ID令牌中启用组声明，请在Microsoft Azure门户的&#x200B;**令牌配置**&#x200B;部分中添加声明： <!-- Alexandru: this bit cound be clearer as well-->

![OIDC声明令牌ID](/help/security/assets/oidc-claim-id-token.png)

必须像下面的示例一样修改`SlingUserInfoProcessor`的配置。

需要修改的文件名是`org.apache.sling.auth.oauth_client.impl.SlingUserInfoProcessorImpl.cfg.json`。 应按如下方式配置内容：

```
{
  "connection": "azure",
  "groupsInIdToken": "true",
  "storeAccessToken": "false",
  "storeRefreshToken": "false"
}
```
