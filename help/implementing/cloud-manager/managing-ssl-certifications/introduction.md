---
title: 简介 — 管理SSL证书
description: 简介 — 管理SSL证书
exl-id: 0d41723c-c096-4882-a3fd-050b7c9996d8
source-git-commit: 4be76f19c27aeab84de388106a440434a99a738c
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 0%

---

# 简介 {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_sslcert"
>title="管理SSL证书"
>abstract="Cloud Manager为客户提供了通过Cloud Manager UI安装SSL证书的自助服务功能。 Cloud Manager使用Platform TLS服务来管理客户拥有的SSL证书和私钥，这些证书和私钥通常从第三方认证机构获得。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-ssl-certificates/view-update-replace-ssl-certificate.html" text="查看、更新和替换SSL证书"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-ssl-certificates/check-status-ssl-certificate.html" text="检查SSL证书的状态"


Cloud Manager为客户提供了通过Cloud Manager UI安装SSL证书的自助服务功能。 Cloud Manager使用Platform TLS服务来管理客户拥有的SSL证书和私钥，这些证书和私钥通常从第三方认证机构获取，例如&#x200B;*Let&#39;s Encrypt*。

## 重要注意事项 {#important-considerations}

* Cloud Manager不提供SSL证书或私钥。 这些证书必须从第三方认证机构获得。 请参阅[获取SSL证书](/help/implementing/cloud-manager/managing-ssl-certifications/get-ssl-certificate.md)以了解更多信息。

* AEM as a Cloud Service仅支持安全的`https`站点。 具有多个自定义域的客户在每次添加域时都不希望上传证书。 因此，此类客户将通过获取一个具有多个域的证书而受益。

* AEM as aCloud Service将仅接受OV（组织验证）或EV（扩展验证）证书。 将不接受DV（域验证）证书。 此外，任何证书都必须是来自受信任的认证中心(CA)的X.509 TLS证书，且具有匹配的2048位RSA私钥。

* AEM as aCloud Service将接受域的通配符SSL证书。

* 在任何给定时间，Cloud Manager将允许最多20个SSL证书，这些证书可以与您计划中的一个或多个环境关联，即使证书已过期也是如此。 但是，在具有此约束的程序中，Cloud Manager UI将允许安装最多50个SSL证书。 通常，证书可以覆盖多个域（最多100个SAN），因此请考虑将同一证书中的多个域分组以保持在此限制下。

Cloud Manager支持以下客户SSL证书要求：

* SSL证书可供多个环境使用，即添加一次并使用多次。
* 每个Cloud Manager环境都可以使用多个证书。
* 私钥可能会颁发多个SSL证书。
* 每个证书通常包含多个域。
* Platform TLS服务会根据用于终止的SSL证书和托管该域的CDN服务，将请求路由到客户的CDN服务。

使用Cloud Manager UI SSL证书页面，具有权限的用户可以执行多项任务来管理程序的SSL证书：

* [添加SSL证书](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)
* [查看、更新或替换SSL证书](/help/implementing/cloud-manager/managing-ssl-certifications/view-update-replace-ssl-certificate.md)
   >[!NOTE]
   >这些操作允许您查看详细信息或替换即将过期的证书。
* [删除SSL证书](/help/implementing/cloud-manager/managing-ssl-certifications/delete-ssl-certificate.md)
