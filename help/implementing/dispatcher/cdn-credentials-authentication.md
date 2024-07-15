---
title: 配置 CDN 凭证和身份验证
description: 了解如何通过在随后使用Cloud Manager配置管道部署的配置文件中声明规则来配置CDN凭据和身份验证。
feature: Dispatcher
exl-id: a5a18c41-17bf-4683-9a10-f0387762889b
role: Admin
source-git-commit: 73d0a4a73a3e97a91b2276c86d3ed1324de8c361
workflow-type: tm+mt
source-wordcount: '1400'
ht-degree: 4%

---

# 配置 CDN 凭证和身份验证 {#cdn-credentials-authentication}

>[!NOTE]
>此功能尚未普遍可用。要加入率先采用者计划，请发送电子邮件至`aemcs-cdn-config-adopter@adobe.com`。

Adobe提供的CDN具有多种功能和服务，其中一些功能和服务依赖凭据和身份验证以确保适当级别的企业安全。 通过使用[Cloud Manager配置管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#config-deployment-pipeline)部署的配置文件中声明规则，客户可以自助配置以下内容：

* AdobeCDN用于验证来自客户管理的CDN的HTTP标头值。
* 用于清除CDN缓存中的资源的API令牌。
* 通过提交基本身份验证表单，可访问受限内容的用户名/密码组合列表。


下面单独一节介绍了其中的每个术语，包括配置语法。 “[通用设置](#common-setup)”部分说明了这两个通用设置以及部署的通用设置。 最后，还有一节介绍如何[旋转密钥](#rotating-secrets)，这被认为是一种良好的安全做法。

## 客户管理的CDN HTTP标头值 {#CDN-HTTP-value}

如AEM as a Cloud Service](/help/implementing/dispatcher/cdn.md#point-to-point-CDN)页面中的[CDN中所述，客户可以选择通过自己的CDN路由流量，该CDN称为客户CDN（有时也称为BYOCDN）。

作为设置的一部分，AdobeCDN和客户CDN必须同意`X-AEM-Edge-Key` HTTP标头的值。 此值在发送到AdobeCDN之前，在客户CDN中对每个请求进行设置，CDN随后会验证该值是否按预期可用，因此它可以信任其他HTTP标头，包括有助于将请求路由到相应AEM源的标头。

`X-AEM-Edge-Key`值使用以下语法声明，实际值由edgeKey1和edgeKey2属性引用。 请参阅[常用设置](#common-setup)部分以了解如何部署配置。

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  experimental_authentication:
    authenticators:
      - name: edge-auth
        type: edge
        edgeKey1: ${{CDN_EDGEKEY_052824}}
        edgeKey2: ${{CDN_EDGEKEY_041425}}
    rules:
      - name: edge-auth-rule
        when: { reqProperty: tier, equals: "publish" }
        action:
          type: authenticate
          authenticator: edge-auth
```

`X-AEM-Edge-Key`值的语法包括：

* 类型、版本和元数据。
* 包含子`experimental_authentication`节点的数据节点（释放功能时将删除实验前缀）。
* 在`experimental_authentication`下，有一个`authenticators`节点和一个`rules`节点，两者都是数组。
* 身份验证者：用于声明令牌或凭据的类型，在本例中为Edge密钥。 它包括以下属性：
   * name — 描述性字符串。
   * 类型 — 必须为`edge`。
   * edgeKey1 - *X-AEM-Edge-Key*&#x200B;的值，该值必须引用不应存储在git中的机密令牌，而是声明为类型机密的[Cloud Manager环境变量](/help/implementing/cloud-manager/environment-variables.md)。 对于“已应用服务”字段，选择全部。 建议值（例如，`${{CDN_EDGEKEY_052824}}`）反映添加日期。
   * edgeKey2 — 用于轮换密钥，具体说明见下面的[轮换密钥部分](#rotating-secrets)。 定义它的方法与edgeKey1类似。 必须声明`edgeKey1`和`edgeKey2`中的至少一个。
<!--   * OnFailure - defines the action, either `log` or `block`, when a request doesn't match either `edgeKey1` or `edgeKey2`. For `log`, request processing will continue, while `block` will serve a 403 error. The `log` value is useful when testing a new token on a live site since you can first confirm that the CDN is correctly accepting the new token before changing to `block` mode; it also reduces the chance of lost connectivity between the customer CDN and the Adobe CDN, as a result of an incorrect configuration. -->
* 规则：用于声明应使用哪些验证器，以及它是否用于发布和/或预览层。  它包括：
   * name — 描述性字符串。
   * when — 根据[流量过滤器规则](/help/security/traffic-filter-rules-including-waf.md)文章中的语法确定何时应评估规则的条件。 通常，它包括对当前层的比较（例如，发布），以使所有实时流量验证为通过客户CDN的路由。
   * 操作 — 必须指定“authenticate”（身份验证），并引用目标身份验证器。

>[!NOTE]
>在部署引用Edge密钥的配置之前，必须将其配置为类型为`secret`的[Cloud Manager环境变量](/help/implementing/cloud-manager/environment-variables.md)变量（已为应用服务选择&#x200B;*所有*）。

## 清除API令牌 {#purge-API-token}

客户可以使用声明的清除API令牌[清除CDN缓存](/help/implementing/dispatcher/cdn-cache-purge.md)。 使用以下语法声明令牌。  请参阅[常见设置](#common-setup)部分以了解如何部署它。

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  experimental_authentication:
    authenticators:
       - name: purge-auth
         type: purge
         purgeKey1: ${{CDN_PURGEKEY_031224}}
         purgeKey2: ${{CDN_PURGEKEY_021225}}
    rules:
       - name: purge-auth-rule
         when: { reqProperty: tier, equals: "publish" }
         action:
           type: authenticate
           authenticator: purge-auth
```

语法包括：

* 类型、版本和元数据。
* 包含子`experimental_authentication`节点的数据节点（释放功能后将删除实验前缀）。
* 在`experimental_authentication`下，有一个`authenticators`节点和一个`rules`节点，两者都是数组。
* 身份验证者：用于声明令牌或凭据的类型，在本例中是清除密钥。 它包括以下属性：
   * name — 描述性字符串。
   * 类型 — 必须清除。
   * purgeKey1 — 其值必须引用不应存储在git中的机密令牌，而是声明为类型为`secret`的[Cloud Manager环境变量](/help/implementing/cloud-manager/environment-variables.md)。
   * 对于“已应用服务”字段，选择全部。 建议值（例如`${{CDN_PURGEKEY_031224}}`）反映添加日期。
   * purgeKey2 — 用于轮换密码，有关说明，请参见下面的[轮换密码部分](#rotating-secrets)。 必须声明`purgeKey1`和`purgeKey2`中的至少一个。
* 规则：用于声明应使用哪些验证器，以及它是否用于发布和/或预览层。  它包括：
   * 名称 — 描述性字符串
   * when — 根据[流量过滤器规则](/help/security/traffic-filter-rules-including-waf.md)文章中的语法确定何时应评估规则的条件。 通常，它包括当前层的比较（例如，发布）。
   * 操作 — 必须指定“authenticate”（身份验证），并引用目标身份验证器。

>[!NOTE]
>在部署引用Edge密钥的配置之前，必须将其配置为类型为`secret`的[Cloud Manager环境变量](/help/implementing/cloud-manager/environment-variables.md)变量。

## 基本身份验证 {#basic-auth}

通过弹出需要用户名和密码的基本身份验证对话框来保护某些内容资源。此功能主要用于轻度身份验证用例（如业务利益相关者对内容的审查），而不是作为最终用户访问权限的完整解决方案。

最终用户将体验到类似于以下内容的基本身份验证对话框：

![basicauth-dialog](/help/implementing/dispatcher/assets/basic-auth-dialog.png)


语法声明如下。 有关如何部署该程序的信息，请参阅下面的[常用设置](#common-setup)部分。

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  experimental_authentication:
    authenticators:
       - name: my-basic-authenticator
         type: basic
         credentials:
           - user: johndoe
             password: ${{JOHN_DOE_PASSWORD}}
           - user: janedoe
             password: ${{JANE_DOE_PASSWORD}}
    rules:
       - name: basic-auth-rule
         when: { reqProperty: path, like: "/summercampaign" }
         action:
           type: authenticate
           authenticator: my-basic-authenticator
```

语法包括：

* 类型、版本和元数据。
* 包含`experimental_authentication`节点的数据节点（释放功能后将删除实验前缀）。
* 在`experimental_authentication`下，有一个`authenticators`节点和一个`rules`节点，两者都是数组。
* 验证者：在此场景中，声明一个基本验证者，该验证者具有以下结构：
   * 名称 — 描述性字符串
   * 类型 — 必须为`basic`
   * 凭据数组，每个凭据包括以下名称/值对，最终用户可以在基本身份验证对话框中输入这些凭据：
      * user — 用户的名称
      * 密码 — 其值必须引用一个密码令牌，该令牌不应存储在git中，而是声明为类型为密码的Cloud Manager环境变量（选择&#x200B;**所有**&#x200B;作为服务字段）
* 规则：用于声明应使用哪些身份验证器，以及应保护哪些资源。 每个规则包括：
   * 名称 — 描述性字符串
   * when — 根据[流量过滤器规则](/help/security/traffic-filter-rules-including-waf.md)文章中的语法确定何时应评估规则的条件。 通常，它包括对发布层或特定路径的比较。
   * 操作 — 必须在引用的目标验证者中指定“authenticate”，对于此方案而言，这是基本验证

>[!NOTE]
>在部署引用Edge密钥的配置之前，必须将其配置为类型为`secret`的[Cloud Manager环境变量](/help/implementing/cloud-manager/environment-variables.md)变量。

## 通用设置 {#common-setup}

所有身份验证器的设置如下所示：

* 首先，在Git项目的顶级文件夹中创建以下文件夹和文件结构：

```
config/
     cdn.yaml
```

* 其次，`cdn.yaml`配置文件应包含下例中描述的节点。 `kind`属性应设置为`CDN`，版本应设置为架构版本，当前为`1`。 元数据节点具有“envTypes”属性，该属性指示将在哪些环境类型（开发、暂存、生产）上评估此配置。

* 最后，在Cloud Manager中创建目标部署配置管道。 请参阅[配置生产管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md)和[配置非生产管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)。

请注意：

* RDE当前不支持配置管道。
* 您可以使用 `yq` 在本地验证配置文件（例如 `yq cdn.yaml`）的 YAML 格式。

## 旋转密钥 {#rotating-secrets}

偶尔更改凭据是很好的安全做法。 虽然清除键使用相同的策略，但可以使用Edge键的示例实现这一点，如下所示。

* 最初只定义了`edgeKey1`，在本例中引用为`${{CDN_EDGEKEY_052824}}`，作为推荐的约定，它反映创建日期。

```
experimental_authentication:
  authenticators:
    - name: edge-auth
      type: edge
      edgeKey1: ${{CDN_EDGEKEY_052824}}
```

* 轮换密钥时，请创建新的Cloud Manager密钥，例如`${{CDN_EDGEKEY_041425}}`。
* 在配置中，从`edgeKey2`引用它并进行部署。

```
experimental_authentication:
  authenticators:
    - name: edge-auth
      type: edge
      edgeKey1: ${{CDN_EDGEKEY_052824}}
      edgeKey2: ${{CDN_EDGEKEY_041425}}
```

* 一旦确定不再使用旧的边缘密钥，请从配置中删除`edgeKey1`以删除该密钥。

```
experimental_authentication:
  authenticators:
    - name: edge-auth
      type: edge
      edgeKey2: ${{CDN_EDGEKEY_041425}}
```

* 从Cloud Manager中删除旧密钥引用(`${{CDN_EDGEKEY_052824}}`)并进行部署。
* 准备下一次轮换时，请遵循相同的过程，但这次您将向配置中添加`edgeKey1`，并引用名为的新Cloud Manager环境密钥，例如`${{CDN_EDGEKEY_031426}}`。

```
experimental_authentication:
  authenticators:
    - name: edge-auth
      type: edge
      edgeKey2: ${{CDN_EDGEKEY_041425}}
      edgeKey1: ${{CDN_EDGEKEY_031426}}
```
