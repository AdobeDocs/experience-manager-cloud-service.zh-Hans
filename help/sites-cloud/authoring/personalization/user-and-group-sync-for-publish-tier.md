---
title: 注册、登录和用户配置文件
description: 了解 AEM as a Cloud Service 的注册、登录、用户数据和组同步
exl-id: a991e710-a974-419f-8709-ad86c333dbf8
solution: Experience Manager Sites
feature: Authoring, Personalization
role: User
source-git-commit: 54159c25b60277268ade16b437891f268873fecf
workflow-type: tm+mt
source-wordcount: '1340'
ht-degree: 66%

---

# 注册、登录和用户配置文件 {#registration-login-and-userprofile}

## 简介 {#introduction}

Web 应用程序通常会为最终用户提供帐户管理功能以便在网站上注册，这将保留用户数据信息，以便最终用户将来登录并获得一致体验。本文描述了有关 AEM as a Cloud Service 的以下概念：

* 注册
* 登录
* 存储用户配置文件数据
* 组成员资格
* 数据同步

## 注册 {#registration}

当最终用户在 AEM 应用程序上注册帐户时，会在 AEM Publish 服务上创建一个用户帐户，这将反映在 JCR 存储库中 `/home/users` 下的用户资源中。

可通过如下所述的两种方法进行注册。

### AEM 托管 {#aem-managed-registration}

可以编写自定义注册码，至少需要用户用户名和密码，并在AEM中创建用户记录，然后可以在登录期间使用该记录进行身份验证。 以下步骤通常用于构建此注册机制：

1. 显示收集注册信息的自定义 AEM 组件
1. 提交后，使用适当配置的服务用户来
   1. 通过 UserManager API 的某种 `findAuthorizables()` 方法验证现有用户是否存在
   1. 通过 UserManager API 的某种 `createUser()` 方法创建用户记录
   1. 保留通过可授权界面的 `setProperty()` 方法捕获的任何配置文件数据
1. 可选流程，例如要求用户验证其电子邮件。

**先决条件：**

要使上述逻辑正常工作，请通过提交启用[数据同步](#data-synchronization-data-synchronization)
向客户支持部门发送请求，说明适当的项目和环境。

### 外部 {#external-managed-registration}

在某些情况下，注册或用户创建以前是在 AEM 之外的基础架构中进行的。在此情况下，用户记录是在登录期间在 AEM 中创建的。

## 登录 {#login}

一旦最终用户在 AEM Publish 服务上注册，这些用户就可以登录以获得经过身份验证的访问权限（使用 AEM 授权机制）并保留用户特定的数据，例如配置文件数据。

## 实施 {#implementation}

可以通过以下两种方法实施登录：

### AEM 托管 {#aem-managed-implementation}

客户可以编写自己的自定义组件。要了解更多信息，请考虑熟悉：

* [Sling 身份验证框架](https://sling.apache.org/documentation/the-sling-engine/authentication/authentication-framework.html)
* 并考虑[请求关于登录的 AEM Community Experts 讲座](https://bit.ly/ATACEFeb15)。

**先决条件：**

要使上述逻辑正常工作，请通过提交启用[数据同步](#data-synchronization-data-synchronization)
向客户支持部门发送请求，说明适当的项目和环境。

### 与标识提供者集成 {#integration-with-an-idp}

客户可以与 IdP（标识提供者）集成来验证用户身份。集成技术包括 SAML 和 OAuth/SSO，如下所述。

**基于 SAML**

客户可以通过其首选 SAML IdP 使用基于 SAML 的身份验证。在将IdP与AEM结合使用时，IdP负责验证用户的凭据并使用AEM代理用户的身份验证，根据需要在AEM中创建用户记录，以及管理用户在AEM中的组成员资格，如SAML断言所述。

>[!NOTE]
>
>IdP 仅执行对用户凭据的初始身份验证，只要 AEM 登录令牌 Cookie 可用，就可使用该 Cookie 执行对 AEM 的后续请求。

请参阅文档，了解有关 [SAML 2.0 身份验证处理程序](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/authentication/saml-2-0.html)的更多信息。

**OAuth/SSO**

请参阅[单点登录 (SSO) 文档](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/single-sign-on.html)，了解有关使用 AEM 的 SSO 身份验证处理程序服务的信息。

可以使用您选择的 OAuth 提供程序来实施 `com.adobe.granite.auth.oauth.provider` 接口。

**先决条件：**

作为最佳实践，在存储用户特定的数据时，始终依靠idP（身份提供程序）作为单一信任点。 如果其他用户信息存储在非idP一部分的本地存储库中，请通过向客户支持提交请求（指明适当的项目和环境）来启用[数据同步](#data-synchronization-data-synchronization)。 除了[数据同步](#data-synchronization-data-synchronization)之外，对于SAML身份验证提供程序，请确保已启用[动态组成员资格](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/authentication/saml-2-0)。

### 粘性会话和封装令牌 {#sticky-sessions-and-encapsulated-tokens}

AEM as a Cloud Service启用基于Cookie的粘性会话，确保最终用户在每次请求时都被路由到相同的发布节点。 在特定情况下（例如用户流量尖峰），封装令牌功能可能会提高性能，因此无需在每次请求时都引用存储库中的用户记录。 如果最终用户具有关联的发布节点被替换，则其用户ID记录将在新发布节点上可用，如下面的[数据同步](#data-synchronization-data-synchronization)部分中所述。

要利用封装的令牌功能，请向客户支持提交请求，并指明适当的项目和环境。 更重要的是，封装令牌在没有[数据同步](#data-synchronization-data-synchronization)的情况下无法启用，必须一起启用。 因此，在启用之前仔细审查用例，并确保该功能至关重要。

## 用户配置文件 {#user-profile}

根据数据的性质，可通过多种方法保留数据。

### AEM 存储库 {#aem-repository}

可通过两种方式写入和读取用户配置文件信息：

* 通过 `com.adobe.granite.security.user` 接口 UserPropertiesManager 接口进行服务器端使用，这会将数据放置在 `/home/users` 中的用户节点下。确保不缓存每个用户的唯一页面。
* 使用 ContextHub 的客户端，如[文档](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/personalization/contexthub.html#personalization)所述。

**先决条件：**

要使服务器端用户配置文件持久性逻辑正常工作，请通过提交启用[数据同步](#data-synchronization-data-synchronization)
向客户支持部门发送请求，说明适当的项目和环境。

### 第三方数据存储 {#third-party-data-stores}

最终用户数据可发送到第三方供应商（例如 CRM），该数据可在用户登录 AEM 时通过 API 进行检索，在 AEM 用户的配置文件节点上保留（或更新），并根据需要供 AEM 使用。

可以实时访问第三方服务以检索配置文件属性，但请务必确保这不会对 AEM 中的请求处理产生实质性影响。

**先决条件：**

要使上述逻辑正常工作，请通过提交启用[数据同步](#data-synchronization-data-synchronization)
向客户支持部门发送请求，说明适当的项目和环境。

## 权限（封闭用户组） {#permissions-closed-user-groups}

发布层访问策略（也称为封闭用户组 (CUG)）是在 AEM 创作实例中定义的，如[此处所述](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/cug.html#applying-your-closed-user-group-to-content-pages)。为了限制某些用户访问网站的某些部分或页面，请使用 AEM 创作实例根据需要应用 CUG（如此处所述），并将它们复制到发布层。

* 如果用户通过使用 SAML 向标识提供者 (IdP) 进行身份验证来登录，则身份验证处理程序将识别用户的组成员资格（应与发布层上的 CUG 匹配），并通过存储库记录保留用户与组之间的关联
* 如果在没有 IdP 集成的情况下完成登录，则自定义代码可应用相同的存储库结构关系。

独立于登录，自定义代码还可以根据组织的独特要求保留和管理用户的组成员资格。

## 数据同步 {#data-synchronization}

网站最终用户期望在每个网页请求方面获得一致的体验，甚至当他们使用不同的浏览器登录时，（即使他们不知道）他们也将转至发布层基础架构的不同服务器节点。AEM as a Cloud Service通过在发布层的所有节点中快速同步`/home`文件夹层次结构（用户配置文件信息、组成员资格等）来实现这一点。

与其他 AEM 解决方案不同，AEM as a Cloud Service 中的用户和组成员资格同步不使用点对点消息传递方法，而是实施不需要客户配置的发布-订阅方法。

>[!NOTE]
>
>默认情况下，用户配置文件和组成员资格同步未启用，因此数据不会同步到发布层，甚至不会永久保存到发布层。要启用该功能，请向客户支持发送请求，并指明适当的项目和环境。

>[!IMPORTANT]
>
>在生产环境中启用数据同步之前，请大规模测试实施。 根据用例以及保留的数据，可能会出现一些一致性和延迟问题。

## 缓存注意事项 {#cache-considerations}

经过身份验证的 HTTP 请求可能难以在 CDN 和 Dispatcher 上进行缓存，因为它们可能会将用户特定的状态作为请求响应的一部分传输。无意中缓存经过身份验证的请求并将它们提供给其他请求浏览器可能会导致不正确的体验，甚至泄露受保护的数据或用户数据。

在支持用户特定的响应时，保持请求的高缓存能力的方法包括：

* AEM Dispatcher 权限敏感型缓存
* Sling Dynamic 包括
* AEM ContextHub
