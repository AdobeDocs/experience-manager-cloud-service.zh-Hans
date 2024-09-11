---
title: 添加自定义域名
description: 了解如何使用 Cloud Manager 添加自定义域名。
exl-id: 0fc427b9-560f-4f6e-ac57-32cdf09ec623
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: dd696580758e7ab9a5427d47fda4275f9ad7997f
workflow-type: tm+mt
source-wordcount: '1488'
ht-degree: 20%

---


# 添加自定义域名 {#adding-cdn}

了解如何使用 Cloud Manager 添加自定义域名。

## 要求 {#requirements}

在Cloud Manager中添加自定义域名之前，请先满足这些要求。

* 在添加自定义域名之前，您必须为要添加的域添加域SSL证书，如文档[添加SSL证书](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)中所述。
* 您必须具有&#x200B;**业务负责人**&#x200B;或&#x200B;**部署管理员**&#x200B;角色才能在Cloud Manager中添加自定义域名。
* 正在使用Fastly CDN。

>[!IMPORTANT]
>
>即使您使用非AdobeCDN，也仍需要将域添加到Cloud Manager。

## 在何处添加自定义域名{#}

您可以从 Cloud Manager 中的两个位置添加自定义域名：

* [从“域设置”页面](#adding-cdn-settings)
* [从“环境”页面](#adding-cdn-environments)

添加自定义域名时，将使用最具体且有效的证书来提供该域。 如果多个证书具有相同的域，则选择最近更新的证书。 Adobe建议您管理证书，这样就不会有重叠域。

本文档中描述的任一方法的步骤均基于Fastly。 如果您使用其他CDN，请使用您选择使用的CDN配置您的域。

## 从域设置页面添加自定义域名 {#adding-cdn-settings}

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织。

1. 在&#x200B;**[我的程序](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;控制台上，选择该程序。

1. 在左侧导航面板中，选择&#x200B;**域设置**&#x200B;选项卡

   ![域设置窗口](/help/implementing/cloud-manager/assets/cdn/cdn-create.png)

1. 在&#x200B;**域设置**&#x200B;页面的右上角附近，单击&#x200B;**添加域**。

1. 在&#x200B;**添加域**&#x200B;对话框的&#x200B;**域名**字段中，输入您正在使用的自定义域名。
输入域时不要包含 `http://`、`https://` 或空格。

1. 单击&#x200B;**创建**。

1. 在&#x200B;**验证域**&#x200B;对话框中，在&#x200B;**您计划用于此域的证书类型是什么？**&#x200B;下拉列表，选择以下选项之一：

   | 证书类型 | 描述 |
   | --- | --- |
   | Adobe 管理的证书 | 选择是否要使用DV（域验证）证书。 此选项适用于大多数情况，可提供基本的域验证。 Adobe会自动管理和更新证书。 |
   | 客户管理的证书 | 选择是否要使用EV/OV证书。 此选项通过EV（扩展验证）或OV（组织验证）提供增强的安全性。 如果需要对证书进行更严格的验证、更高的信任级别或自定义控制，请使用。 |

1. 在&#x200B;**验证域**&#x200B;对话框中，根据您选择的证书类型，执行以下操作之一：

   | 如果您选择了证书类型 | 描述 |
   | --- | ---  |
   | Adobe 管理的证书 | 在继续下一步之前，请完成[Adobe托管证书步骤](#abobe-managed-cert-steps)。 |
   | 客户管理的证书 | 在继续下一步之前，请完成[客户管理的证书步骤](#customer-managed-cert-steps)。 |

1. 单击&#x200B;**验证**。

1. 您现在已准备好[添加SSL证书](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)。

   >[!NOTE]
   >
   >如果您使用自托管SSL证书和自托管CDN提供程序，则可以跳过此步骤，在准备就绪时直接转到[添加CDN配置](/help/implementing/cloud-manager/cdn-configurations/add-cdn-config.md)。



### Adobe托管证书步骤 {#adobe-managed-cert-steps}

如果您选择了证书类型&#x200B;*Adobe托管证书*，请在&#x200B;**验证域**&#x200B;对话框中完成以下步骤。

![托管证书步骤Adobe](/help/implementing/cloud-manager/assets/cdn/cdn-create-adobe-dv-cert.png)

要验证正在使用的域，需要添加和验证CNAME。

`CNAME`或记录一旦配置，就会将域的所有互联网流量路由到它指向的任何位置。 如果该位置未配置为服务流量，则会出现停机。如果尚未测试，则内容可能有错误。这就是为什么这个步骤总是在测试完成后完成，并且您已经准备好上线。

要配置这些设置，请确定是否必须配置`CNAME`或Apex记录以将您的自定义域名指向Cloud Manager域名。 本文档的以下部分可以帮助您确定哪种类型的记录适合您的DNS配置。

>[!NOTE]
>
>对于Adobe管理的CDN，在使用DV（域验证）证书时，只允许使用ACME验证的站点。

#### 要求 {#dv-requirements}

请在配置DNS记录之前满足这些要求。

* 如果您还不知道您的域主机或注册商，请确定它。
* 能够编辑组织域的DNS记录，或联系能够编辑记录的适当人员。
* 您必须已按照文档[检查域名状态](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md)中所述验证配置的自定义域名。

#### CNAME记录 {#cname-record}

规范名称或 CNAME 记录是一种将别名映射为真实或规范域名的 DNS 记录类型。CNAME 记录通常用于映射子域，例如 `www.example.com` 到托管该子域内容的域。

登录到您的DNS服务提供商并创建一个`CNAME`记录以将您的自定义域名指向目标，如下表所示。

| CNAME | 自定义域名称指向目标 |
| --- | --- |
| `www.customdomain.com` | `cdn.adobeaemcloud.com` |

#### APEX记录 {#apex-record}

Apex 域是不包含子域的自定义域，例如 `example.com`。通过您的DNS提供商，Apex域配置有`A`、`ALIAS`或`ANAME`记录。 Apex 域必须指向特定的IP地址。

通过域提供商将以下`A`记录添加到域的DNS设置中。

* `A RECORD`

* `A record for domain @ pointing to IP 151.101.3.10`

* `A record for domain @ pointing to IP 151.101.67.10`

* `A record for domain @ pointing to IP 151.101.131.10`

* `A record for domain @ pointing to IP 151.101.195.10`



### 客户管理的证书步骤 {#customer-managed-cert-steps}

如果您选择了证书类型&#x200B;*客户管理的证书*，请在&#x200B;**验证域**&#x200B;对话框中完成以下步骤。

![客户管理的证书步骤](/help/implementing/cloud-manager/assets/cdn/cdn-create-customer-cert.png)

要验证正在使用的域，需要添加和验证TXT记录。

文本记录（也称为TXT记录）是域名系统(DNS)中的一种资源记录。 它允许您将任意文本与主机名相关联。 此文本可能包括用户可读的详细信息，如服务器或网络信息。

Cloud Manager使用特定的TXT记录来授权要在CDN服务中托管的域。 在授权Cloud Manager使用自定义域部署CDN服务并将其与后端服务关联的区域中，创建DNS TXT记录。 此关联完全由您控制，并授权 Cloud Manager 将服务中的内容提供给域。 此授权可授予并撤销。 TXT记录特定于域和Cloud Manager环境。

## 要求 {#requirements-customer-cert}

在添加TXT记录之前满足这些要求。

* 如果您还不知道您的域主机或注册商，请确定它。
* 能够编辑组织域的DNS记录，或联系能够编辑记录的适当人员。
* 首先，按照本文前面所述添加自定义域名。

## 添加TXT记录以进行验证 {#verification}

1. 在&#x200B;**验证域**&#x200B;对话框中，Cloud Manager显示用于验证的名称和TXT值。 复制此值。

1. 登录到您的DNS服务提供商并找到DNS记录部分。

1. 将`aemverification.[yourdomainname]`添加为该值的&#x200B;**Name**，并添加与在&#x200B;**域名**&#x200B;字段中显示的一模一样的TXT值。

   **TXT记录示例**

   | 域 | 名称 | TXT 值 |
   | --- | --- | --- |
   | `example.com` | `_aemverification.example.com` | 复制Cloud Manager UI中显示的整个值。 此值特定于域和环境。 例如：<br>`adobe-aem-verification=example.com/[program]/[env]/..*` |
   | `www.example.com` | `_aemverification.www.example.com` | 复制Cloud Manager UI中显示的整个值。 此值特定于域和环境。 例如：<br>`adobe-aem-verification=www.example.com/[program]/[env]/..*` |

1. 将TXT记录保存到域主机。

## 验证TXT记录 {#verify}

完成后，可通过运行以下命令来验证结果。

```shell
dig _aemverification.[yourdomainname] -t txt
```

预期结果应显示Cloud Manager UI的&#x200B;**添加域名**&#x200B;对话框的&#x200B;**验证**&#x200B;选项卡上提供的TXT值。

例如，如果您的域是 `example.com`，然后运行：

```shell
dig TXT _aemverification.example.com -t txt
```

>[!TIP]
>
>有几个[DNS查找工具](https://www.ultratools.com/tools/dnsLookup)可用。 Google DoH可用于查找TXT记录条目并确定TXT记录是否丢失或错误。

>[!NOTE]
>
>由于 DNS 传播延迟，DNS 验证可能需要几个小时才能处理。
>
>Cloud Manager验证所有权并更新状态，可在域设置表中看到该状态。 有关详细信息，请参阅[检查自定义域名状态](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md)。

<!--
## Next Steps {#next-steps}

Now that you created your TXT entry, you can verify your domain name status. Proceed to the document [Checking Domain Name Status](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) to continue setting up your custom domain name. -->

>[!TIP]
>
>TXT条目和CNAME或A记录可以同时设置在管理的DNS服务器上，从而节省时间。
>
><!-- To do this, review the entire process of setting up a custom domain name as detailed in the document [Introduction to custom domain names](/help/implementing/cloud-manager/custom-domain-names/introduction.md) taking special note of the document [help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md) and update your DNS settings appropriately. -->


## 从环境页面添加自定义域名 {#adding-cdn-environments}

从&#x200B;**环境**&#x200B;页面添加自定义域名的步骤与[从“域设置”页面](#adding-cdn-settings)添加自定义域名的步骤相同，但入口点不同。 按照以下步骤从&#x200B;**环境**&#x200B;页面添加自定义域名。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 上登录到 Cloud Manager 并选择适当的组织和项目。

1. 导航到&#x200B;**环境详细信息**&#x200B;有关感兴趣环境的详细信息页面。

   ![在“环境详细信息”页面上输入域名](/help/implementing/cloud-manager/assets/cdn/cdn-create4.png)

1. 使用&#x200B;**域名**&#x200B;表提交自定义域名。

   1. 输入自定义域名。
   1. 从下拉列表中选择与此名称关联的 SSL 证书。
   1. 单击&#x200B;**+添加**。

   ![添加自定义域名](/help/implementing/cloud-manager/assets/cdn/cdn-create3.png)

1. 将打开&#x200B;**添加域名**&#x200B;对话框，显示&#x200B;**域名**&#x200B;选项卡。 像从“域设置”页面](#adding-cdn-settings)添加自定义域名[一样继续。 —>
