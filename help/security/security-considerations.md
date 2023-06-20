---
title: AEM as a Cloud Service 安全注意事项
description: 了解使用 AEM as a Cloud Service 时的重要安全注意事项
hidefromtoc: true
hide: true
exl-id: d2dfde05-ce02-478e-8697-b939fb8740c3
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 93%

---

# AEM as a Cloud Service 安全注意事项 {#security-considerations}

## AEM 信任库 {#aem-trust-store}

为了支持非对称加密操作，AEM将证书存储在全局信任存储区的内容存储库中。 其内容是公开的，默认情况下，可供发布者实例上的所有人匿名访问。

### 信任库的特征 {#truststore-characteristics}

* 信任库位于 `/etc/truststore` 下方，由 Java 密钥库文件、密钥库密码和存储库元数据组成。请注意，由于技术原因，密码和密钥库本身都已加密，但每个人默认情况下都可以通过 API 访问包含的证书
* 现成的证书仅用于 HTTPS 和 SAML 支持，并且必须先手动创建存储
* 客户可以通过[密钥库 API](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/granite/keystore/KeyStoreService.html#getTrustStore-org.apache.sling.api.resource.ResourceResolver-) 在自己的代码中使用它
* 可以通过 UI（位于&#x200B;**工具** – **安全性** – **信任库**）或通过访问 *`https://serveraddress:serverport/libs/granite/security/content/truststore.html`* 管理信任库，如下所示：

  ![信任库管理](/help/security/assets/global-trust-store-modified.png)

* 可以根据用例，通过存储库访问控制来进一步限制对信任库的访问。

>[!NOTE]
>
>Adobe 建议对信任库使用默认访问控制，这表示该库仍可公开访问。若要实施最安全的配置，您可以对所有人使用 deny jcr:all 策略。

<!--
Commenting out section for now as requested by Lars

## Anonymous Permission Hardening Package {#anonymous-permission-hardening-package}

For more information on the Anonymous Hardening Package, please see the [Security Checklist](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security-checklist.html#anonymous-permission-hardening-package).
-->
