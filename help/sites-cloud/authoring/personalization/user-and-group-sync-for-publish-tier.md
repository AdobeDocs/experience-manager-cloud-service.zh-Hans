---
title: '注册、登录和用户配置文件 '
description: 了解AEM as aCloud Service的注册、登录、用户数据和组同步
exl-id: a991e710-a974-419f-8709-ad86c333dbf8
source-git-commit: 4d76d8bac41e19168abb1819841dfc62be07ea0c
workflow-type: tm+mt
source-wordcount: '1177'
ht-degree: 0%

---

# 注册、登录和用户配置文件{#registration-login-and-userprofile}

## 简介 {#introduction}

Web应用程序通常提供帐户管理功能，供最终用户在网站上注册，这会保留他们的用户数据信息，使他们将来能够登录并享受一致的体验。 本文介绍了将AEM作为Cloud Service的以下概念：

* 注册
* 登录
* 存储用户配置文件数据
* 组成员资格
* 数据同步

>[!IMPORTANT]
>
>要使本文中描述的功能正常工作，必须启用用户数据同步功能，此时需要向客户支持部门发出请求，以指明相应的程序和环境。 如果未启用，则用户信息将仅保留一段短时间（1到24小时），然后消失。

## 注册 {#registration}

当最终用户在AEM应用程序上注册帐户时，将在AEM发布服务上创建一个用户帐户，如JCR存储库`/home/users`下的用户资源中所反映的那样。

实施登记的方法有两种，如下所述。

### AEM Managed {#aem-managed-registration}

可以编写自定义注册代码，该代码至少采用最终用户的用户名和密码，并在AEM中创建用户记录，然后使用该记录在登录期间进行身份验证。 通常使用以下步骤来构建此注册机制：

1. 显示收集注册信息的自定义AEM组件
1. 提交后，使用正确配置的服务用户
   1. 使用UserManager API的`findAuthorizables()`方法之一验证现有用户是否不存在
   1. 使用UserManager API的`createUser()`方法之一创建用户记录
   1. 保留使用可授权界面的`setProperty()`方法捕获的任何用户档案数据
1. 可选流程，例如要求用户验证其电子邮件。

### 外部 {#external-managed-registration}

在某些情况下，之前在AEM外的基础结构中会进行注册或用户创建。 在此方案中，登录期间会在AEM中创建用户记录。

## 登录 {#login}

在AEM发布服务上注册最终用户后，这些用户可以登录以拥有经过身份验证的访问权限(使用AEM授权机制)并保留特定于用户的数据（如用户档案数据）。

## 实施 {#implementation}

可以通过以下两种方法来实施登录：

### AEM Managed {#aem-managed-implementation}

客户可以编写自己的自定义组件。 要了解更多信息，请考虑熟悉以下内容：

* [Sling身份验证框架](https://sling.apache.org/documentation/the-sling-engine/authentication/authentication-framework.html)
* 并考虑[向AEM社区专家会议](http://bit.ly/ATACEFeb15)询问有关登录的信息。

### 与身份提供程序{#integration-with-an-idp}集成

客户可以与IdP（身份提供程序）集成，IdP对用户进行身份验证。 集成技术包括SAML和OAuth/SSO，如下所述。

**基于SAML**

客户可以通过其首选的SAML IdP，使用基于SAML的身份验证。 在AEM中使用IdP时，IdP负责验证最终用户的凭据，并通过AEM代理用户的身份验证，根据需要在AEM中创建用户记录，以及按照SAML断言的描述，管理AEM中用户的组成员资格。

>[!NOTE]
>
>只有用户凭据的初始身份验证才会通过IdP验证，并且只要Cookie可用，随后对AEM的请求就会使用AEM登录令牌Cookie执行。

有关[SAML 2.0身份验证处理程序](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/saml-2-0-authenticationhandler.html?lang=en#saml-authentication-handler)的更多信息，请参阅文档。

**OAuth/SSO**

有关使用AEM SSO身份验证处理程序服务的信息，请参阅[单点登录(SSO)文档](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/single-sign-on.html)。

`com.adobe.granite.auth.oauth.provider`接口可通过您选择的OAuth提供程序来实施。

### 置顶会话和封装令牌{#sticky-sessions-and-encapsulated-tokens}

AEM as aCloud Service启用了基于cookie的置顶会话，这可确保在每次请求时将最终用户路由到相同的发布节点。 为了提高性能，默认情况下会启用封装的令牌功能，因此无需在每个请求中引用存储库中的用户记录。 如果替换了最终用户与之有亲和度的发布节点，则其用户ID记录将在新发布节点上可用，如以下数据同步部分所述。

## 用户个人资料 {#user-profile}

根据数据的性质，有多种方法可保留数据。

### AEM存储库{#aem-repository}

用户配置文件信息可以通过两种方式写入和读取：

* 服务器端与`com.adobe.granite.security.user` Interface UserPropertiesManager界面一起使用，该界面将数据放在`/home/users`中用户节点下。 确保未缓存每个用户唯一的页面。
* 客户端使用ContextHub，如[文档](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/personalization/contexthub.html?lang=en#personalization)所述。

### 第三方数据存储{#third-party-data-stores}

最终用户数据可以发送给第三方供应商（如CRM），并在用户登录AEM后通过API进行检索，并在AEM用户的配置文件节点上保留（或刷新），并由AEM根据需要使用。

虽然可以实时访问第三方服务以检索用户档案属性，但务必要确保这不会对AEM中的请求处理造成实质性影响。

## 权限（已关闭的用户组）{#permissions-closed-user-groups}

发布层访问策略(也称为“已关闭的用户组”(CUG))在AEM作者中定义为[，如下所述：](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/cug.html?lang=en#applying-your-closed-user-group-to-content-pages)。 要限制某些用户访问网站的某些部分或页面，请根据需要使用AEM作者应用CUG（如此处所述），并将它们复制到发布层。

* 如果用户使用SAML通过身份提供程序(IdP)进行身份验证来登录，则身份验证处理程序将识别用户的组成员关系（应与发布层上的CUG相匹配），并通过存储库记录保留用户与组之间的关联
* 如果在没有IdP集成的情况下登录完成，则自定义代码可以应用相同的存储库结构关系。

自定义代码与登录无关，还可以根据组织独特要求的要求保留和管理用户组成员关系。

## 数据同步{#data-synchronization}

网站最终用户希望在每个网页请求上获得一致的体验，甚至在使用不同的浏览器登录时也能获得一致的体验，即使他们不知道，他们也会被带到发布层基础架构的不同服务器节点。 AEM as aCloud Service通过快速同步发布层所有节点中的`/home`文件夹层次结构（用户配置文件信息、组成员资格等）来完成此操作。

与其他AEM解决方案不同，AEM as a Cloud Service中的用户和组成员资格同步不使用点对点消息传送方法，而是实施不需要客户配置的发布订阅方法。

>[!NOTE]
>
>默认情况下，用户配置文件和组成员身份同步未启用，因此数据不会同步到发布层，甚至不会永久保留在发布层。 要启用该功能，请向客户支持发送请求，以指示相应的程序和环境。

## 缓存注意事项{#cache-considerations}

经过身份验证的HTTP请求在CDN和Dispatcher上可能很难缓存，因为它们可能会在请求响应中传输特定于用户的状态。 无意中缓存已验证的请求并将其提供给其他请求浏览器可能会导致体验不正确，甚至会泄露受保护或用户数据。

在支持用户特定响应的同时保持请求的高缓存能力的方法包括：

* AEM Dispatcher权限敏感缓存
* Sling动态包含
* AEM ContextHub
