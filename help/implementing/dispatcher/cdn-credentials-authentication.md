---
title: 配置 CDN 凭证和身份验证
description: 了解如何通过在随后使用Cloud Manager配置管道部署的配置文件中声明规则来配置CDN凭据和身份验证。
feature: Dispatcher
exl-id: a5a18c41-17bf-4683-9a10-f0387762889b
role: Admin
source-git-commit: 85cef99dc7a8d762d12fd6e1c9bc2aeb3f8c1312
workflow-type: tm+mt
source-wordcount: '1266'
ht-degree: 2%

---


# 配置 CDN 凭证和身份验证 {#cdn-credentials-authentication}

Adobe提供的CDN具有多种功能和服务，其中一些功能和服务依赖凭据和身份验证以确保适当级别的企业安全。 通过使用Cloud Manager [配置管道部署的配置文件中声明规则，](/help/operations/config-pipeline.md)客户能够以自助方式配置以下内容：

* AdobeCDN用于验证来自客户管理的CDN的的X-AEM-Edge-Key HTTP标头值。
* 用于清除CDN缓存中的资源的API令牌。
* 通过提交基本身份验证表单，可访问受限内容的用户名/密码组合列表。 [此功能可供早期采用者使用。](/help/release-notes/release-notes-cloud/release-notes-current.md#foundation-early-adopter)

下面单独一节介绍了其中的每个术语，包括配置语法。

有一部分介绍了如何[旋转密钥](#rotating-secrets)，这是一种很好的安全做法。

## 客户管理的CDN HTTP标头值 {#CDN-HTTP-value}

如AEM as a Cloud Service](/help/implementing/dispatcher/cdn.md#point-to-point-CDN)页面中的[CDN中所述，客户可以选择通过自己的CDN路由流量，该CDN称为客户CDN（有时也称为BYOCDN）。

作为设置的一部分，AdobeCDN和客户CDN必须同意`X-AEM-Edge-Key` HTTP标头的值。 此值在发送到AdobeCDN之前，在客户CDN中对每个请求进行设置，CDN随后会验证该值是否按预期可用，因此它可以信任其他HTTP标头，包括有助于将请求路由到相应AEM源的标头。

*X-AEM-Edge-Key*&#x200B;值由名为`cdn.yaml`或类似文件中的`edgeKey1`和`edgeKey2`属性引用，位于顶级`config`文件夹下的某个位置。 有关文件夹结构和如何部署配置的详细信息，请参阅[使用配置管道](/help/operations/config-pipeline.md#folder-structure)。

语法说明如下：

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  authentication:
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

有关`data`节点上属性的描述，请参阅[使用配置管道](/help/operations/config-pipeline.md#common-syntax)。 `kind`属性值应为&#x200B;*CDN*，`version`属性应设置为`1`。

其他属性包括：

* 包含子`authentication`节点的`Data`节点。
* 在`authentication`下，有一个`authenticators`节点和一个`rules`节点，两者都是数组。
* 身份验证者：用于声明令牌或凭据的类型，在本例中为Edge密钥。 它包括以下属性：
   * name — 描述性字符串。
   * 类型 — 必须为`edge`。
   * edgeKey1 - *X-AEM-Edge-Key*&#x200B;的值，该值必须引用[Cloud Manager机密类型环境变量](/help/operations/config-pipeline.md#secret-env-vars)。 对于“已应用服务”字段，选择全部。 建议值（例如，`${{CDN_EDGEKEY_052824}}`）反映添加日期。
   * edgeKey2 — 用于轮换密钥，具体说明见下面的[轮换密钥部分](#rotating-secrets)。 定义它的方法与edgeKey1类似。 必须声明`edgeKey1`和`edgeKey2`中的至少一个。
<!--   * OnFailure - defines the action, either `log` or `block`, when a request doesn't match either `edgeKey1` or `edgeKey2`. For `log`, request processing will continue, while `block` will serve a 403 error. The `log` value is useful when testing a new token on a live site since you can first confirm that the CDN is correctly accepting the new token before changing to `block` mode; it also reduces the chance of lost connectivity between the customer CDN and the Adobe CDN, as a result of an incorrect configuration. -->
* 规则：用于声明应使用哪些验证器，以及它是否用于发布和/或预览层。  它包括：
   * name — 描述性字符串。
   * when — 根据[流量过滤器规则](/help/security/traffic-filter-rules-including-waf.md)文章中的语法确定何时应评估规则的条件。 通常，它包括对当前层的比较（例如，发布），以使所有实时流量验证为通过客户CDN的路由。
   * 操作 — 必须指定“authenticate”（身份验证），并引用目标身份验证器。

>[!NOTE]
>在部署引用Edge密钥的配置之前，必须将其配置为[机密类型Cloud Manager环境变量](/help/operations/config-pipeline.md#secret-env-vars)。

## 清除API令牌 {#purge-API-token}

客户可以使用声明的清除API令牌[清除CDN缓存](/help/implementing/dispatcher/cdn-cache-purge.md)。 令牌在名为`cdn.yaml`或类似的文件中声明，位于顶级`config`文件夹下的某个位置。 有关文件夹结构和如何部署配置的详细信息，请参阅[使用配置管道](/help/operations/config-pipeline.md#folder-structure)。

语法说明如下：

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  authentication:
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

有关`data`节点上属性的描述，请参阅[使用配置管道](/help/operations/config-pipeline.md#common-syntax)。 `kind`属性值应为&#x200B;*CDN*，`version`属性应设置为`1`。

其他属性包括：

* 包含子`authentication`节点的`data`节点。
* 在`authentication`下，有一个`authenticators`节点和一个`rules`节点，两者都是数组。
* 身份验证者：用于声明令牌或凭据的类型，在本例中是清除密钥。 它包括以下属性：
   * name — 描述性字符串。
   * 类型 — 必须清除。
   * purgeKey1 — 其值必须引用[Cloud Manager机密类型的环境变量](/help/operations/config-pipeline.md#secret-env-vars)。 对于“已应用服务”字段，选择全部。 建议值（例如`${{CDN_PURGEKEY_031224}}`）反映添加日期。
   * purgeKey2 — 用于轮换密码，有关说明，请参见下面的[轮换密码部分](#rotating-secrets)。 必须声明`purgeKey1`和`purgeKey2`中的至少一个。
* 规则：用于声明应使用哪些验证器，以及它是否用于发布和/或预览层。  它包括：
   * 名称 — 描述性字符串
   * when — 根据[流量过滤器规则](/help/security/traffic-filter-rules-including-waf.md)文章中的语法确定何时应评估规则的条件。 通常，它包括当前层的比较（例如，发布）。
   * 操作 — 必须指定“authenticate”（身份验证），并引用目标身份验证器。

>[!NOTE]
>在部署引用清除密钥的配置之前，必须将清除密钥配置为[机密类型Cloud Manager环境变量](/help/operations/config-pipeline.md#secret-env-vars)。

## 基本身份验证 {#basic-auth}

>[!NOTE]
>此功能尚未普遍可用。要加入率先采用者计划，请发送电子邮件至`aemcs-cdn-config-adopter@adobe.com`。

通过弹出需要用户名和密码的基本身份验证对话框来保护某些内容资源。此功能主要用于轻度身份验证用例（如业务利益相关者对内容的审查），而不是作为最终用户访问权限的完整解决方案。

最终用户将体验到类似于以下内容的基本身份验证对话框：

![basicauth-dialog](/help/implementing/dispatcher/assets/basic-auth-dialog.png)


语法如下：

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

有关`data`节点上属性的描述，请参阅[使用配置管道](/help/operations/config-pipeline.md#common-syntax)。 `kind`属性值应为&#x200B;*CDN*，`version`属性应设置为`1`。

此外，语法包括：

* 包含`experimental_authentication`节点的`data`节点（在发布该功能时将删除实验前缀）。
* 在`experimental_authentication`下，有一个`authenticators`节点和一个`rules`节点，两者都是数组。
* 验证者：在此场景中，声明一个基本验证者，该验证者具有以下结构：
   * 名称 — 描述性字符串
   * 类型 — 必须为`basic`
   * 凭据数组，每个凭据包括以下名称/值对，最终用户可以在基本身份验证对话框中输入这些凭据：
      * user — 用户的名称
      * 密码 — 其值必须引用[Cloud Manager密钥类型环境变量](/help/operations/config-pipeline.md#secret-env-vars)，并且选择&#x200B;**所有**&#x200B;作为服务字段。
* 规则：用于声明应使用哪些身份验证器，以及应保护哪些资源。 每个规则包括：
   * 名称 — 描述性字符串
   * when — 根据[流量过滤器规则](/help/security/traffic-filter-rules-including-waf.md)文章中的语法确定何时应评估规则的条件。 通常，它包括对发布层或特定路径的比较。
   * 操作 — 必须在引用的目标验证者中指定“authenticate”，对于此方案而言，这是基本验证

>[!NOTE]
>在部署引用密码的配置之前，必须将密码配置为[机密类型Cloud Manager环境变量](/help/operations/config-pipeline.md#secret-env-vars)。

## 旋转密钥 {#rotating-secrets}

1. 偶尔更改凭据是很好的安全做法。 虽然清除键使用相同的策略，但可以使用Edge键的示例实现这一点，如下所示。

1. 最初只定义了`edgeKey1`，在本例中引用为`${{CDN_EDGEKEY_052824}}`，作为推荐的约定，它反映创建日期。

   ```
   experimental_authentication:
     authenticators:
       - name: edge-auth
         type: edge
         edgeKey1: ${{CDN_EDGEKEY_052824}}
   ```
1. 轮换密钥时，请创建新的Cloud Manager密钥，例如`${{CDN_EDGEKEY_041425}}`。
1. 在配置中，从`edgeKey2`引用它并进行部署。

   ```
   experimental_authentication:
     authenticators:
       - name: edge-auth
         type: edge
         edgeKey1: ${{CDN_EDGEKEY_052824}}
         edgeKey2: ${{CDN_EDGEKEY_041425}}
   ```

1. 一旦确定不再使用旧的边缘密钥，请从配置中删除`edgeKey1`以删除该密钥。

   ```
   experimental_authentication:
     authenticators:
       - name: edge-auth
         type: edge
         edgeKey2: ${{CDN_EDGEKEY_041425}}
   ```
1. 从Cloud Manager中删除旧密钥引用(`${{CDN_EDGEKEY_052824}}`)并进行部署。

1. 准备下一次轮换时，请遵循相同的过程，但这次您将向配置中添加`edgeKey1`，并引用名为的新Cloud Manager环境密钥，例如`${{CDN_EDGEKEY_031426}}`。

   ```
   experimental_authentication:
     authenticators:
       - name: edge-auth
         type: edge
         edgeKey2: ${{CDN_EDGEKEY_041425}}
         edgeKey1: ${{CDN_EDGEKEY_031426}}
   ```
