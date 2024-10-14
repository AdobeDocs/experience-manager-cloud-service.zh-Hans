---
title: 添加自定义域名
description: 了解如何使用Cloud Manager中的域设置添加自定义域名。
exl-id: 0fc427b9-560f-4f6e-ac57-32cdf09ec623
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 02f9b035320bb4b6219d5ed4273554259fc09e59
workflow-type: tm+mt
source-wordcount: '993'
ht-degree: 15%

---


# 添加客户自定义域名 {#adding-cdn}

了解如何使用Cloud Manager中的&#x200B;**域设置**&#x200B;添加自定义域名。

## 要求 {#requirements}

在Cloud Manager中添加自定义域名之前，请先满足这些要求。

* 您必须在添加自定义域名&#x200B;*之前*&#x200B;添加要添加的域的域SSL证书，如文档[添加SSL证书](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)中所述。
* 您必须具有&#x200B;**业务负责人**&#x200B;或&#x200B;**部署管理员**&#x200B;角色才能在Cloud Manager中添加自定义域名。
* 使用Fastly或其他CDN（内容分发网络）。

>[!IMPORTANT]
>
>如果您使用Adobe托管的CDN，则仍需要将域添加到Cloud Manager。

## 在何处添加自定义域名 {#where-to-add-cdn}

您可以从Cloud Manager中的[域设置页面](#adding-cdn-settings)添加自定义域名。

添加自定义域名时，将使用最具体且有效的证书来提供该域。 如果多个证书具有相同的域，则选择最近更新的证书。 Adobe建议您管理证书，这样就不会有重叠域。

本文档中描述的任一方法的步骤均基于Fastly。 如果您使用了其他CDN（内容分发网络），请使用已选择使用的CDN配置您的域。

## 添加客户自定义域名 {#adding-cdn-settings}

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织。

1. 在&#x200B;**[我的程序](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;控制台上，选择该程序。

1. 在侧菜单的&#x200B;**服务**&#x200B;下，单击![设置图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Settings_18_N.svg) **域设置**。

   ![域设置窗口](/help/implementing/cloud-manager/assets/cdn/cdn-create.png)

1. 在&#x200B;**域设置**&#x200B;页面的右上角附近，单击&#x200B;**添加域**。

1. 在&#x200B;**添加域**&#x200B;对话框的&#x200B;**域名**字段中，输入您正在使用的自定义域名。
输入域名时，不要包含`http://`、`https://`或空格。

1. 单击&#x200B;**创建**。

1. 在&#x200B;**验证域**&#x200B;对话框中，在&#x200B;**您计划用于此域的证书类型是什么？**&#x200B;下拉列表，选择以下选项之一：

   | 证书类型选项 | 描述 |
   | --- | --- |
   | Adobe托管(DV) SSL证书 | 如果要使用DV（域验证）证书，请选择此证书类型。 此选项适用于大多数情况，可提供基本的域验证。 Adobe会自动管理和更新证书。 |
   | 客户管理的(OV/EV) SSL证书 | 如果您打算使用EV/OV SSL证书来保护域，请选择此证书类型。 此选项通过OV（组织验证）或EV（扩展验证）提供增强的安全性。 如果需要对证书进行更严格的验证、更高的信任级别或自定义控制，请使用。 |

1. 在&#x200B;**验证域**&#x200B;对话框中，根据您选择的证书类型，执行以下操作之一：

   | 如果您选择了证书类型 | 描述 |
   | --- | ---  |
   | Adobe 管理的证书 | a.完成以下[Adobe托管证书步骤](#adobe-managed-cert-steps)。 完成这些步骤后，在&#x200B;**验证域**&#x200B;对话框中，单击&#x200B;**验证**。<ul><li>由于 DNS 传播延迟，DNS 验证可能需要几个小时才能处理。</li><li>Cloud Manager最终验证域名所有权并更新&#x200B;**域设置**&#x200B;表中的状态。 有关详细信息，请参阅[检查自定义域名状态](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md)。</li>![验证域状态](/help/implementing/cloud-manager/assets/domain-settings-verified.png)</li></ul>b.您现在可以[添加Adobe托管(DV) SSL证书](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md#add-adobe-managed-ssl-cert)。</li></ul> |
   | 客户管理的证书 | a.单击&#x200B;**确定**。<br>b。您现在可以[添加客户管理的(OV/EV) SSL证书](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md#add-customer-managed-ssl-cert)。<br>添加证书后，您的域名在&#x200B;**域设置**&#x200B;表中标记为已验证。 有关详细信息，请参阅[检查自定义域名状态](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md)。</li></ul><br>![验证客户管理的EV/OV证书的域](/help/implementing/cloud-manager/assets/verify-domain-customer-managed-step.png) |

   >[!NOTE]
   >
   >如果您使用客户管理的(OV/EV) SSL证书和客户管理的CDN提供程序，则可以跳过添加SSL证书，并在准备就绪后直接转到[添加CDN配置](/help/implementing/cloud-manager/cdn-configurations/add-cdn-config.md)。

### Adobe托管证书步骤 {#adobe-managed-cert-steps}

如果您选择了证书类型&#x200B;*Adobe托管证书*，请在&#x200B;**验证域**&#x200B;对话框中完成以下步骤。

![托管证书步骤Adobe](/help/implementing/cloud-manager/assets/cdn/cdn-create-adobe-dv-cert.png)

要验证正在使用的域，需要添加和验证CNAME。

`CNAME`或记录一旦配置，就会将域的所有互联网流量路由到它指向的任何位置。 如果该位置未配置为服务流量，则会出现停机。如果尚未测试，则内容可能有错误。这就是为什么这个步骤总是在测试完成后完成，并且您已经准备好上线。

要配置这些设置，请确定是否必须配置`CNAME`或Apex记录以将您的自定义域名指向Cloud Manager域名。 本文档的以下部分可以帮助您确定哪种类型的记录适合您的DNS配置。

>[!NOTE]
>
>对于Adobe管理的CDN，在使用DV（域验证）证书时，只允许使用ACME验证的站点。

#### 要求 {#adobe-managed-cert-dv-requirements}

请在配置DNS记录之前满足这些要求。

* 如果您还不知道您的域主机或注册商，请确定它。
* 能够编辑组织域的DNS记录，或联系能够编辑记录的适当人员。
* 您必须已按照文档[检查域名状态](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md)中所述验证配置的自定义域名。

#### CNAME记录 {#adobe-managed-cert-cname-record}

规范名称或 CNAME 记录是一种将别名映射为真实或规范域名的 DNS 记录类型。CNAME 记录通常用于映射子域，例如 `www.example.com` 到托管该子域内容的域。

登录到您的DNS服务提供商并创建一个`CNAME`记录以将您的自定义域名指向目标，如下表所示。

| CNAME | 自定义域名称指向目标 |
| --- | --- |
| `www.customdomain.com` | `cdn.adobeaemcloud.com` |

#### APEX记录 {#adobe-managed-cert-apex-record}

Apex 域是不包含子域的自定义域，例如 `example.com`。通过您的DNS提供商，Apex域配置有`A`、`ALIAS`或`ANAME`记录。 Apex 域必须指向特定的IP地址。

通过域提供商将以下`A`记录添加到域的DNS设置中。

* `A RECORD`

* `A record for domain @ pointing to IP 151.101.3.10`

* `A record for domain @ pointing to IP 151.101.67.10`

* `A record for domain @ pointing to IP 151.101.131.10`

* `A record for domain @ pointing to IP 151.101.195.10`

>[!TIP]
>
>可以在管理DNS服务器上设置&#x200B;*CNAME*&#x200B;或&#x200B;*A记录*&#x200B;以节省您的时间。

<!--
![Customer managed certificate steps](/help/implementing/cloud-manager/assets/cdn/cdn-create-customer-cert.png)

To verify the domain in use, you are required to add and verify a TXT record.

A text record (also known as a TXT record) is a type of resource record in the Domain Name System (DNS). It lets you associate arbitrary text with a hostname. This text could include human-readable details like server or network information.

Cloud Manager uses a specific TXT record to authorize a domain to be hosted in a CDN service. Create a DNS TXT record in the zone that authorizes Cloud Manager to deploy the CDN service with the custom domain and associate it with the backend service. This association is entirely under your control and authorizes Cloud Manager to serve content from the service to a domain. This authorization may be granted and withdrawn. The TXT record is specific to the domain and the Cloud Manager environment.

#### Requirements {#customer-managed-cert-requirements}

Fulfill these requirements before adding a TXT record.

* Identify your domain host or registrar if you do not know it already.
* Be able to edit the DNS records for your organization's domain, or contact the appropriate person who can.
* First, add a custom domain name as described earlier in this article.

#### Add a TXT record for verification {#customer-managed-cert-verification}

1. In the **Verify domain** dialog box, Cloud Manager displays the name and TXT value to use for verification. Copy this value.

1. Log in to your DNS service provider and find the DNS records section. 

1. Add `aemverification.[yourdomainname]` as the **Name** of the value and add the TXT value exactly as it appears in the **Domain Name** field.

   **TXT record examples**

   | Domain | Name | TXT Value |
   | --- | --- | --- |
   | `example.com` | `_aemverification.example.com` | Copy the entire value displayed in the Cloud Manager UI. This value is specific to the domain and the environment. For example:<br>`adobe-aem-verification=example.com/[program]/[env]/..*` |
   | `www.example.com` | `_aemverification.www.example.com` | Copy the entire value displayed in the Cloud Manager UI. This value is specific to the domain and the environment. For example:<br>`adobe-aem-verification=www.example.com/[program]/[env]/..*` |

1. Save the TXT record to your domain host.

#### Verify TXT record {#customer-managed-cert-verify}

When you are done, you can verify the result by running the following command.

```shell
dig _aemverification.[yourdomainname] -t txt
```

The expected result should display the TXT value provided on the **Verification** tab of the **Add Domain Name** dialog of the Cloud Manager UI.

For example, if your domain is `example.com`, then run:

```shell
dig TXT _aemverification.example.com -t txt
```


>[!TIP]
>
>There are several [DNS lookup tools](https://www.ultratools.com/tools/dnsLookup) available. Google DoH can be used to look up TXT record entries and identify if the TXT record is missing or erroneous.

-->



<!--
## Next Steps {#next-steps}

Now that you created your TXT entry, you can verify your domain name status. Proceed to the document [Checking Domain Name Status](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) to continue setting up your custom domain name. -->


><!-- The TXT entry and the CNAME or A Record can be set simultaneously on the governing DNS server, thus saving time. -->
>
><!-- To do this, review the entire process of setting up a custom domain name as detailed in the document [Introduction to custom domain names](/help/implementing/cloud-manager/custom-domain-names/introduction.md) taking special note of the document [help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md) and update your DNS settings appropriately. -->

