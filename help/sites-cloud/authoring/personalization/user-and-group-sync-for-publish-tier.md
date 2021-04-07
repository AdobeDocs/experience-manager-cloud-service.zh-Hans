---
title: '注册、登录和用户用户档案 '
description: 了解作为Cloud Service的AEM的注册、登录、用户数据和组同步
exl-id: a991e710-a974-419f-8709-ad86c333dbf8
translation-type: tm+mt
source-git-commit: 4d76d8bac41e19168abb1819841dfc62be07ea0c
workflow-type: tm+mt
source-wordcount: '1177'
ht-degree: 0%

---

# 注册、登录和用户用户档案{#registration-login-and-userprofile}

## 简介 {#introduction}

Web 应用程序经常为最终用户提供帐户管理功能，以便在网站上注册，这会保留他们的用户数据信息，允许他们将来登录并享受一致的体验。 本文将介绍AEM作为Cloud Service的以下概念：

* 注册
* 登录
* 存储用户用户档案数据
* 用户组成员关系
* 数据同步

>[!IMPORTANT]
>
>为了使本文中描述的功能正常工作，必须启用用户数据同步功能，此时需要向客户支持部门发出请求，指明相应的项目和环境。 如果未启用，则用户信息将仅持续一段短时间（1到24小时）后才会消失。

## 注册{#registration}

当最终用户在AEM应用程序上注册帐户时，将在AEM发布服务上创建用户帐户，如JCR存储库中`/home/users`下的用户资源上所反映的那样。

实施登记有两种方法，如下所述。

### AEM Managed {#aem-managed-registration}

可以编写自定义注册代码，其至少需要最终用户的用户名和密码，并在AEM中创建用户记录，然后在登录过程中用于进行身份验证。 通常使用以下步骤构建此注册机制：

1. 显示收集注册信息的自定义AEM组件
1. 提交后，会使用正确设置的服务用户
   1. 使用UserManager API的`findAuthorizables()`方法之一验证现有用户是否尚不存在
   1. 使用UserManager API的`createUser()`方法之一创建用户记录
   1. 保留使用可授权界面的`setProperty()`方法捕获的任何用户档案数据
1. 可选流，如要求用户验证其电子邮件。

### 外部 {#external-managed-registration}

在某些情况下，以前在AEM之外的基础结构中会进行注册或用户创建。 在此方案中，用户记录在登录时在AEM中创建。

## 登录 {#login}

在AEM发布服务上注册最终用户后，这些用户可以登录以获得经过身份验证的访问(使用AEM授权机制)并保留特定于用户的数据，如用户档案数据。

## 实施 {#implementation}

可通过以下两种方法实现登录：

### AEM Managed {#aem-managed-implementation}

客户可以编写自己的自定义组件。 要了解更多信息，请考虑熟悉：

* [Sling身份验证框架](https://sling.apache.org/documentation/the-sling-engine/authentication/authentication-framework.html)
* 并考虑[向AEM Community Experts会话](http://bit.ly/ATACEFeb15)询问有关登录的信息。

### 与标识提供者{#integration-with-an-idp}集成

客户可以与对用户进行身份验证的IdP（标识提供者）集成。 集成技术包括SAML和OAuth/SSO，如下所述。

**基于SAML**

客户可以通过其首选SAML IdP使用基于SAML的身份验证。 在AEM中使用IdP时，IdP负责验证最终用户的凭据并代理用户的AEM身份验证，根据需要在AEM中创建用户记录，以及管理AEM中用户的组成员关系（如SAML断言所述）。

>[!NOTE]
>
>只有IdP验证用户凭据的初始身份验证，并且只要Cookie可用，随后向AEM发出的请求就使用AEM登录令牌Cookie执行。

有关[SAML 2.0身份验证处理程序](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/saml-2-0-authenticationhandler.html?lang=en#saml-authentication-handler)的详细信息，请参阅文档。

**OAuth/SSO**

有关使用AEM SSO身份验证处理程序服务的信息，请参阅[单点登录(SSO)文档](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/single-sign-on.html)。

`com.adobe.granite.auth.oauth.provider`接口可以通过您选择的OAuth提供程序实现。

### 粘滞会话和封装令牌{#sticky-sessions-and-encapsulated-tokens}

AEM作为Cloud Service启用了基于cookie的即时会话，这可确保最终用户在每次请求时路由到相同的发布节点。 为了提高性能，默认情况下启用封装的令牌功能，因此不需要在每个请求上引用存储库中的用户记录。 如果替换了最终用户要关联的发布节点，则新发布节点上将提供其用户ID记录，如下面的数据同步部分所述。

## 用户个人资料 {#user-profile}

根据数据的性质，有多种方法来保存数据。

### AEM存储库{#aem-repository}

用户用户档案信息可以通过两种方式编写和读取：

* 服务器端与`com.adobe.granite.security.user`接口UserPropertiesManager接口一起使用，该接口将数据放在`/home/users`中用户节点下。 确保未缓存每个用户唯一的页面。
* 客户端使用ContextHub，如[文档](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/personalization/contexthub.html?lang=en#personalization)所述。

### 第三方数据存储{#third-party-data-stores}

最终用户数据可发送给第三方供应商（如CRM），在用户登录AEM后通过API进行检索，并在AEM用户的用户档案节点上保留（或刷新），并由AEM根据需要使用。

可以实时访问第三方服务以检索用户档案属性，但必须确保这不会对AEM中的请求处理产生实质性影响。

## 权限（已关闭的用户组）{#permissions-closed-user-groups}

发布层访问策略(也称为已关闭的用户组(CUG))在AEM作者中定义为[，此处](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/cug.html?lang=en#applying-your-closed-user-group-to-content-pages)对此进行了说明。 要限制某些用户访问某个网站的特定部分或页面，请使用此处所述的AEM作者根据需要应用CUG，并将它们复制到发布层。

* 如果用户使用SAML通过与标识提供者(IdP)进行身份验证来登录，则身份验证处理程序将标识用户的组成员关系（应与发布层上的CUG匹配），并通过存储库记录保持用户与组之间的关联
* 如果登录在没有IdP集成的情况下完成，则自定义代码可以应用相同的存储库结构关系。

根据组织的独特要求，自定义代码还可以独立于登录名而保留和管理用户组成员关系。

## 数据同步{#data-synchronization}

网站最终用户期望在每个网页请求上获得一致的体验，甚至在使用不同的浏览器登录时，即使他们不知道，也会将他们带到发布层基础架构的不同服务器节点。 AEM作为Cloud Service，通过快速同步发布层所有节点上的`/home`文件夹层次结构(用户用户档案信息、组成员关系等)来实现这一点。

与其他AEM解决方案不同，作为Cloud Service,AEM中的用户和用户组成员同步不使用点对点消息传递方法，而是实施不需要客户配置的发布订阅方法。

>[!NOTE]
>
>默认情况下，不启用用户用户档案和用户组成员关系同步，因此数据不会同步到发布层，甚至不会在发布层上永久保留。 要启用该功能，请向客户支持发送请求，指明相应的项目和环境。

## 缓存注意事项{#cache-considerations}

身份验证的HTTP请求在CDN和Dispatcher上可能很难缓存，因为它们可能会作为请求响应的一部分传输用户特定状态。 无意中缓存经过身份验证的请求并将它们提供给其他请求的浏览器可能会导致不正确的体验，甚至泄露受保护的或用户数据。

在支持用户特定响应的同时保持请求的高缓存能力的方法包括：

* AEM Dispatcher权限敏感缓存
* Sling Dynamic Include
* AEM ContextHub
