---
title: 发布层上为 AEM as a Cloud Service 提供 Open ID Connect 支持
description: 了解如何在发布层上为 AEM as a Cloud Service 设置 Open ID Connect (OIDC)
feature: Security
role: Admin
exl-id: d2f30406-546c-4a2f-ba88-8046dee3e09b
source-git-commit: eb03c8941f848ff10c38a4880c8fe85387cc441f
workflow-type: tm+mt
source-wordcount: '1469'
ht-degree: 100%

---

# 发布层上为 AEM as a Cloud Service 提供 Open ID Connect 支持 {#open-id-connect-support-for-aem-as-a-cloud-service-on-publish-tier}

## 简介 {#introduction}

随着组织进一步推动其数字体验的现代化，安全且可扩展的身份管理已成为一项基本要求。现在，Adobe Experience Manager (AEM) 云服务在发布层支持 OpenID Connect (OIDC)，允许与领先的身份提供商 (IdP)（例如 Entra ID (Azure AD)、Google、Okta、Auth0、Ping Identity、ForgeRock 和 OIDC 支持的 IDP）进行基于标准的无缝集成。

OIDC 是 OAuth 2.0 协议之上的身份层，可实现强大的用户身份验证，而且方便开发人员使用。它广泛应用于企业对消费者 (B2C)、内联网和合作伙伴门户等需要安全的用户登录和身份联盟的场景。

到目前为止，AEM 客户需要自己负责实施发布层上的自定义登录逻辑，这增加了开发时间并带来了长期维护和安全挑战。通过对 OIDC 的原生支持，AEM Cloud Service 为访问发布环境的最终用户提供一个安全、可扩展、受到 Adobe 支持的身份验证机制，从而消除了这一负担。

无论您提供的是个性化的消费者网站还是经过身份验证的内部门户网站，发布上的 OIDC 都可以简化身份联盟，并通过集中身份治理降低风险。它还可以帮助组织在不影响敏捷度的情况下满足现代合规要求和安全性标准。

## 为 OIDC 身份验证配置 AEM {#configure-aem-oidc-authentication}

### 先决条件 {#prerequisits}

我们假设以下信息可用或已定义：

1. AEM 存储库中需受保护的内容的路径
1. 要配置的 IdP 的标识符。这可以是任何字符串

IdP 配置中的信息：

1. IdP 中配置的客户端 ID
1. IdP 中配置的客户端密码。如果在 Idp 上配置了 PKCE，客户端密码就不可用。不要在配置文件中存储纯文本值。使用 CM 密码并引用它
1. Idp 上配置的范围。至少必须提供范围 `openid`
1. IdP 上是否启用了 PKCE
1. `callbackUrl` 的定义是使用在点 1 处定义的配置路径之一，然后添加后缀：`/j_security_check`
1. `baseUrl` 用于访问标准 `.well-known` 文件。例如，如果众所周知的 URL 是：`https://login.microsoftonline.com/53279d7a-438f-41cd-a6a0-fdb09efc8891/v2.0/.well-known/openid-configuration`，那么 `baseUrl` 就是：`https://login.microsoftonline.com/53279d7a-438f-41cd-a6a0-fdb09efc8891`

### 配置文件概述 {#overview-of-the-configuration-files}

以下是需要配置的文件列表：

1. **OIDC 连接**：`OidcAuthenticationHandler` 将使用它对用户进行身份验证，或者其他组件使用它来[授予对使用 OAuth 受 IdP 保护的资源的访问权限](https://github.com/apache/sling-org-apache-sling-auth-oauth-client)
1. **OIDC 身份验证处理程序**：这个身份验证处理程序用于对访问所配置路径的用户进行身份验证
1. **UserInfoProcessor**：此组件处理 IdP 接收的信息。客户可以将其扩展来实施自定义逻辑
1. [**默认同步处理程序**](https://jackrabbit.apache.org/oak/docs/security/authentication/external/defaultusersync.html)：此组件在存储库中创建用户
1. [**ExternalLoginModule**](https://jackrabbit.apache.org/oak/docs/security/authentication/externalloginmodule.html)：此组件在本地 oak 存储库中对用户进行身份验证。

下图显示了上述配置元素如何链接。请注意，由于这些是 `ServiceFactory` 组件，因此 `~uniqueid` 可以是任何随机的唯一字符串：

![OIDC 配置图](/help/security/assets/oidc-diagram.png)

### 配置 OIDC 连接 {#configure-the-oidc-connection}

首先，我们需要配置 OIDC 连接。可以配置多个 OIDC 连接，每个连接都必须有不同的名称。

1. 创建一个新 `.cfg.json` 文件来存放配置。例如，您可以使用 `org.apache.sling.auth.oauth_client.impl.OidcConnectionImpl~azure.cfg.json` - **azure** 后缀必须是此连接的唯一标识符
1. 遵循以下示例中的配置格式：

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

1. 按照下述方法配置其属性：
   * **“名称”**&#x200B;可由用户定义
   * `baseUrl`、`clientid` 和 `clientSecret` 是 IdP 中的配置值。
   * 范围必须至少包含值 `openid`。

### 配置 OIDC 身份验证处理程序 {#configure-oidc-authentication-handler}

现在，配置 OIDC 身份验证处理程序。可以配置多个 OIDC 连接。每个都必须有不同的名称。如果他们有相同的 [OAK 外部身份提供者](https://jackrabbit.apache.org/oak/docs/security/authentication/identitymanagement.html)，他们就可以共享用户。

1. 创建配置文件。在此例中，我们将使用 `org.apache.sling.auth.oauth_client.impl.OidcAuthenticationHandler~azure.cfg.json`。`azure` 后缀必须是唯一的标识符。请参阅下面的配置文件示例：

   ```
   {
     "path":"/content/tests/us/en/test-7",
     "callbackUri":"http://localhost:14503/content/tests/us/en/test-7/j_security_check",
     "pkceEnabled":false,
     "defaultConnectionName":"azure"
     "idp": "azure-idp"
   }
   ```

1. 然后，按照下述方法配置其属性：
   * `path`：需要保护的路径
   * `callbackUri`：到需要保护的路径，添加后缀：`/j_security_check`
   * `defaultConnectionName`：使用上一步中为 OIDC 连接定义的相同名称进行配置+
   * `pkceEnabled`：`true` 代码交换证明密钥 (PKCE) 授权码流程
   * `idp`：[OAK 外部身份提供者](https://jackrabbit.apache.org/oak/docs/security/authentication/identitymanagement.html)的名称。请注意，不同的 OAK IDP 不能共享用户或组

### 配置 SlingUserInfoProcessor

1. 创建配置文件。在此例中，我们将使用 `org.apache.sling.auth.oauth_client.impl.SlingUserInfoProcessor~azure.cfg.json`。`azure` 后缀必须是唯一的标识符。请参阅下面的配置文件示例：

   ```
   {
      "groupsInIdToken":true,
      "groupsClaimName": "groups",
      "connection":"azure",
      "storeAccessToken": false,
      "storeRefreshToken": false
   }
   ```

1. 然后，按照下述方法配置其属性：
   * `groupsInIdToken`：如果组在 ID 令牌中发送，将其设置为 true。如果值为 false 或未指定，则从 UserInfo 端点读取组。
   * `groupsClaimName`：声明的名称中包含要在 AEM 中同步的组。
   * `connection`：使用上一步中为 OIDC 连接定义的相同名称进行配置
   * `storeAccessToken`：如果访问令牌必须存储在存储库中，此值为 true。默认情况下是 false。只有当 AEM 需要代表用户访问存储在受同一 IdP 保护的外部服务器中的资源时，才将其设置为 true。
   * `storeRefreshToken`：如果刷新令牌必须存储在存储库中，此值为 true。默认情况下是 false。只有当 AEM 需要代表用户访问存储在受同一 IdP 保护的外部服务器中的资源，并且需要从 IdP 刷新令牌时，才将其设置为 true。
请注意，访问令牌和刷新令牌都通过 AEM 主密钥加密存储。


### 配置同步处理程序 {#configure-the-synchronization-handler}

必须至少配置一个同步处理程序来同步在 oak 中经过身份验证的用户。有关更多详细信息，请参阅[此](https://jackrabbit.apache.org/oak/docs/security/authentication/external/defaultusersync.html)页面。

创建名为 `org.apache.jackrabbit.oak.spi.security.authentication.external.impl.DefaultSyncHandler~azure.cfg.json` 的文件。**azure** 后缀必须是唯一的标识符。有关如何配置其属性的更多信息，请参阅 [Oak 用户和组同步文档](https://jackrabbit.apache.org/oak/docs/security/authentication/external/defaultusersync.html)。请参阅下面的配置示例：

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

下面是需要在 DefaultSyncHandler 中配置的一些最相关的属性。请注意，云服务中应始终启用动态组成员资格。

| 属性名称 | 注释 | 建议的值 |
|---|---|---|
| `user.expirationTime` | 直到被同步的用户过期的持续时间。只有在过期后才同步用户。 | 1h |
| `user.membershipExpTime` | 直到被同步的用户会员资格过期的持续时间。只有在过期后才同步用户会员资格。 | 1h |
| `user.dynamicMembership` | 我们建议启用动态组会员资格 | true |
| `user.enforceDynamicMembership` | 我们建议启用强制执行动态组会员资格 | true |
| `group.dynamicGroups` | 我们建议启用动态组 | true |
| user.propertyMapping | 提供的 `UserInfoProcessor` 实施只同步少数几个属性。可以将其修改和自定义。 | <code>&quot;profile/givenName=profile/given_name&quot;,</code><br><code>&quot;profile/familyName=profile/family_name&quot;,</code><br><code>&quot;rep:fullname=profile/name&quot;,</code><br><code>&quot;profile/email=profile/email&quot;,</code><br><code>&quot;access_token=access_token&quot;,</code><br><code>&quot;refresh_token=refresh_token&quot;</code> |  |
| `user.membershipNestingDepth` | 返回在会员资格关系同步时最大的组嵌套深度。值为 0 时可有效禁用组会员资格查找。值为 1 时仅添加用户的直接组。仅在同步一个用户会员资格祖先时才同步各个组的情况下，这个值不起任何作用。 | 1 |

### 配置外部登录模块 {#configure-the-external-login-module}

最后，您需要配置外部登录模块。

1. 创建名为 `org.apache.jackrabbit.oak.spi.security.authentication.external.impl.ExternalLoginModuleFactory~azure.cfg.json` 的文件。请参阅下面的配置示例：

   ```
   {
    "sync.handlerName":"azure",
    "idp.name":"azure-idp"
   }
   ```

1. 按照下述方法配置其属性：

   * `sync.handlerName`：之前定义的同步处理程序的名称
   * `idp.name`：OIDC 身份验证处理程序中定义的 OAK 身份提供者

### 可选：实施一个自定义 UserInfoProcessor {#implement-a-custom-userinfoprocessor}

通过 ID 令牌验证用户身份，在为 IdP 定义的 `userInfo` 端点中获取附加属性。如果必须执行额外的非标准操作，则 [UserInfoProcessor](https://github.com/apache/sling-org-apache-sling-auth-oauth-client/blob/master/src/main/java/org/apache/sling/auth/oauth_client/impl/SlingUserInfoProcessorImpl.java) 的自定义实施是 Sling 的默认实施。

## 示例：通过 Azure Active Directory 配置 OIDC 身份验证

### 在 Azure Active Directory 中配置新的应用程序 {#configure-a-new-application-in-azure-ad}

1. 按照 [Azure Active Directory 文档](https://learn.microsoft.com/en-us/power-pages/security/authentication/openid-settings#create-an-app-registration-in-azure)的说明在 Azure Active Directory 中创建新的应用程序。请参见下面详细展示应用程序概述的屏幕：

   ![应用程序概述](/help/security/assets/odic-application-overview.png)

1. 如果需要组或应用程序角色，请按照[文档](https://learn.microsoft.com/en-us/entra/external-id/customers/how-to-use-app-roles-customers)中的说明为应用程序启用这些角色，并将其发送到 ID 令牌中。以下是已配置组的示例：

![OIDC 声明令牌 ID](/help/security/assets/oidc-claim-id-token.png)

1. 按照前面记录的步骤，创建必需的配置文件。下面是专门针对 Azure AD 的示例：
   * 我们将 oidc 连接、身份验证处理程序和 DefaultSyncHandler 的名称定义为：`azure`
   * 网站 url 为：`www.mywebsite.com`
   * 我们保护路径 `/content/wknd/us/en/adventures`
   * 租户是：`tennat-id`，
   * 客户端 id 是：`client-id`，
   * 密码是：`secret`，
   * 这些组在以下声明中发送到 ID 令牌中：`groups`

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

### 关于 Azure AD 组的其他信息 {#additional-information-about-azure-ad-groups}

要在 Microsoft Azure 门户中为企业应用程序配置组，您需要在&#x200B;**企业应用程序**&#x200B;上搜索该应用程序，然后添加组：<!-- Alexandru: this bit cound be clearer-->

![添加 OIDC 组](/help/security/assets/oidc-ad-additional-info.png)

要在 Id 令牌中启用组声明，请在 Microsoft Azure 门户的&#x200B;**令牌配置**&#x200B;分区中添加声明：<!-- Alexandru: this bit cound be clearer as well-->

![OIDC 声明令牌 ID](/help/security/assets/oidc-claim-id-token.png)

`SlingUserInfoProcessor` 的配置必须像下例中这样进行修改。

需要修改的文件名称为 `org.apache.sling.auth.oauth_client.impl.SlingUserInfoProcessorImpl.cfg.json`。内容应进行如下配置：

```
{
  "connection": "azure",
  "groupsInIdToken": "true",
  "storeAccessToken": "false",
  "storeRefreshToken": "false"
}
```
