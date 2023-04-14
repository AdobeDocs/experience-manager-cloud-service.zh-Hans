---
title: AEMas a Cloud Service安全注意事项
description: 了解使用AEM as a Cloud Service时的重要安全注意事项
hidefromtoc: true
hide: true
source-git-commit: 39ffd826f5d1e9cea2e6a03a74f39c16647b45fa
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---


# AEMas a Cloud Service安全注意事项 {#security-considerations}

## AEM Trust Store {#aem-trust-store}

为了支持非对称的加密操作，AEM将证书存储在内容存储库内的全局信任存储中。 其内容是公共的，默认情况下，发布者实例上的每个人都可以匿名访问。

### 信任存储的特性 {#truststore-characteristics}

* 信任存储位于以下位置 `/etc/truststore` 和由Java KeyStore文件、KeyStore密码和存储库元数据组成。 请注意，由于技术原因，密码和密钥库本身都进行了加密，即使所有人默认都可通过API访问包含的证书
* 证书现成仅用于HTTPS和SAML支持，且必须先手动创建存储
* 客户可以通过 [密钥库API](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/granite/keystore/KeyStoreService.html#getTrustStore-org.apache.sling.api.resource.ResourceResolver-)
* 可通过UI()管理信任存储 **工具** - **安全性** - **信任存储** 或 *`https://serveraddress:serverport/libs/granite/security/content/truststore.html`*，如下所示：

   ![信任存储管理](/help/security/assets/global-trust-store-modified.png)

* 根据用例，存储库访问控制可以进一步限制对信任存储的访问。

>[!NOTE]
>
>Adobe建议对信任存储使用默认的访问控制，这意味着它仍可公开访问。 对于最安全的配置，您可以对每个人使用拒绝jcr:all策略。

<!--
Commenting out section for now as requested by Lars

## Anonymous Permission Hardening Package {#anonymous-permission-hardening-package}

For more information on the Anonymous Hardening Package, please see the [Security Checklist](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security-checklist.html#anonymous-permission-hardening-package).
-->
