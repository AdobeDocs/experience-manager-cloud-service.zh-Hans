---
title: Adobe ID
description: 本页介绍有关Adobe ID的介绍性信息。
source-git-commit: 312b1ce7dc660d1bb4fe199be0e7403069d30161
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 1%

---


# Adobe ID {#adobe-id}

Adobe ID只是一个电子邮件地址，用于作为Cloud Service或任何Adobe解决方案登录和访问AEM。 这是与您的[identity](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/identity.ug.html)关联的电子邮件地址，系统管理员使用该地址来访问您的组织拥有的任何Adobe解决方案。

>[!IMPORTANT]
>Adobe ID对于使用Adobe应用程序和服务获得安全且个性化的体验至关重要，当您想要购买Adobe产品时，也需要它。 通过使用Adobe ID，您可以将所有Adobe计划和产品与单个帐户关联。 请参阅[创建或更新Adobe ID](https://helpx.adobe.com/ca/manage-account/using/create-update-adobe-id.html#HowtocreateorupdateyourAdobeID)以了解更多信息。


有三种类型的Adobe ID:

* **个人ID**。这是默认的帐户类型。 基本上，用户需要在adobe.com上创建帐户。 换言之，此帐户由Adobe管理，任何人都可以创建此类型的帐户。

* **Enterprise ID**:组织通常希望加强对用户帐户的控制。通过Enterprise ID，只有系统管理员才能创建此类帐户，并且组织拥有这些帐户；Adobe仅托管它们。

* **Federated ID**。这是组织完全拥有和控制帐户的地方。 在这种情况下，您需要将Adobe Experience Cloud与SAML2 SSO系统相集成。 最终结果是，用户针对其公司的SSO系统进行身份验证，而不是针对托管在Adobe的帐户进行身份验证。 请参阅[SAML 2.0身份验证处理程序](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/saml-2-0-authenticationhandler.html#security)以了解更多信息。

   >[!NOTE]
   >如果您的Enterprise ID或Federated ID尚未设置，则系统管理员可以决定使用个人ID载入您的团队。设置Enterprise或Federated ID后，可以使用此ID将成员转换为。




