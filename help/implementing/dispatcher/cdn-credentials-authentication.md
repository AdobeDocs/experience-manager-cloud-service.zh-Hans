---
title: 配置 CDN 凭证和身份验证
description: 了解如何通过在随后使用Cloud Manager配置管道部署的配置文件中声明规则来配置CDN凭据和身份验证。
feature: Dispatcher
exl-id: a5a18c41-17bf-4683-9a10-f0387762889b
role: Admin
source-git-commit: bfe0538660474d445a60fa1c8174d7a690b1dc4c
workflow-type: tm+mt
source-wordcount: '1939'
ht-degree: 3%

---


# 配置 CDN 凭证和身份验证 {#cdn-credentials-authentication}

Adobe提供的CDN具有多种功能和服务，其中一些功能和服务依赖凭据和身份验证以确保适当级别的企业安全。 通过使用Cloud Manager [配置管道](/help/operations/config-pipeline.md)部署的配置文件中声明规则，客户可以自助配置以下内容：

* Adobe CDN用于验证来自客户管理的CDN的请求的X-AEM-Edge-Key HTTP标头值。
* 用于清除CDN缓存中的资源的API令牌。
* 通过提交基本身份验证表单，可访问受限内容的用户名/密码组合列表。

下面单独一节介绍了其中的每个术语，包括配置语法。

有一部分介绍了如何[旋转密钥](#rotating-secrets)，这是一种很好的安全做法。

>[!NOTE]
> 定义为环境变量的密钥应被视为不可变。 您应该创建一个具有新名称的新密码并在配置中引用该密码，而不是更改其值。 否则，将导致无法可靠地更新密钥。

>[!WARNING]
>请勿删除CDN配置中引用的环境变量。 这样做可能会导致更新CDN配置失败（例如，更新规则或自定义域和证书）。

## 客户管理的CDN HTTP标头值 {#CDN-HTTP-value}

如AEM as a Cloud Service[&#128279;](/help/implementing/dispatcher/cdn.md#point-to-point-CDN)页面中的CDN中所述，客户可以选择通过自己的CDN路由流量，该CDN称为客户CDN（有时也称为BYOCDN）。

作为设置的一部分，Adobe CDN和客户CDN必须同意`X-AEM-Edge-Key` HTTP标头的值。 此值在发送到Adobe CDN之前，在客户CDN上针对每个请求进行设置，CDN随后会验证该值是否按预期可用，因此它可以信任其他HTTP标头，包括有助于将请求路由到相应AEM源的标头。

*X-AEM-Edge-Key*&#x200B;值由名为`cdn.yaml`或类似文件中的`edgeKey1`和`edgeKey2`属性引用，位于顶级`config`文件夹下的某个位置。 有关文件夹结构和如何部署配置的详细信息，请参阅[使用配置管道](/help/operations/config-pipeline.md#folder-structure)。  以下示例中介绍了语法。

有关进一步的调试信息和常见错误，请检查[常见错误](/help/implementing/dispatcher/cdn.md#common-errors)。

>[!WARNING]
>对于符合条件的所有请求（在以下示例中，表示对发布层的所有请求），不通过正确的X-AEM-Edge-Key直接访问将被拒绝。 如果您需要逐步引入身份验证，请参阅[安全迁移以降低流量受阻的风险](#migrating-safely)部分。

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

请参阅 [使用配置管道](/help/operations/config-pipeline.md#common-syntax)，了解 `data` 节点上方属性的描述。`kind`属性值应为&#x200B;*CDN*，`version`属性应设置为`1`。

有关更多详细信息，请参阅[配置和部署HTTP标头验证CDN规则](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/content-delivery/custom-domain-names-with-customer-managed-cdn#configure-and-deploy-http-header-validation-cdn-rule)教程步骤。

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
>在部署引用Edge密钥的配置之前，必须将其配置为[机密类型Cloud Manager环境变量](/help/operations/config-pipeline.md#secret-env-vars)。 建议使用长度最小为32字节的唯一随机密钥；例如，Open SSL加密库可以通过执行命令`openssl rand -hex 32`来生成随机密钥。

### 安全迁移以降低流量受阻的风险 {#migrating-safely}

如果您的站点已上线，请在迁移到客户管理的CDN时务必谨慎，因为错误配置可能会阻止公共流量；这是因为Adobe CDN只会接受具有预期X-AEM-Edge-Key标头值的请求。 建议采用一种方法，在此方法中身份验证规则中临时包含附加条件，这样只有当包含测试标头或匹配路径时，才会阻止请求：

```
    - name: edge-auth-rule
        when:
          allOf:  
            - { reqProperty: tier, equals: "publish" }
            - { reqHeader: x-edge-test, equals: "test" }
        action:
          type: authenticate
          authenticator: edge-auth
```

```
    - name: edge-auth-rule
        when:
          allOf:
            - { reqProperty: tier, equals: "publish" }
            - { reqProperty: path, like: "/test*" }
        action:
          type: authenticate
          authenticator: edge-auth
```

可以使用以下`curl`请求模式：

```
curl https://publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com -H "X-Forwarded-Host: example.com" -H "X-AEM-Edge-Key: <CONFIGURED_EDGE_KEY>" -H "x-edge-test: test"
```

成功测试后，可以删除其他条件并重新部署配置。

### 迁移过程(如果Adobe支持以前生成了`X-AEM-Edge-Key` HTTP标头值) {#migrating-legacy}

>[!NOTE]
>在继续迁移之前，请在暂存环境中安排测试迁移以验证策略。

>[!WARNING]
> 在步骤4之前，请勿更改客户管理的CDN中的键。

以前，与客户管理的CDN集成的过程涉及客户向Adobe支持请求X-AEM-Edge-Key HTTP标头值，而不是自行定义该值。 要迁移到新的自助方法（用于定义自己的Edge键值），请按照以下步骤确保顺利过渡且无停机：

1. 使用指定为`edgeKey1`和`edgeKey2`的新密码（客户生成的）和旧密码(Adobe生成的)配置CDN配置。 这是[旋转密钥](/help/implementing/dispatcher/cdn-credentials-authentication.md#rotating-secrets)文档的变体。

2. 部署密钥和自助式CDN配置。 在此过程中的这一阶段，Adobe定义的旧密钥仍应保留为客户管理的CDN传递的X-AEM-Edge-Key值。

3. 联系Adobe支持部门，请求Adobe切换使用自助配置，并指定您已部署该配置。

4. 在Adobe确认已执行该操作后，将客户管理的CDN配置为对`X-AEM-Edge-Key` HTTP标头值使用客户定义的新密钥。

5. 从CDN配置中删除旧键并重新部署配置管道。

>[!WARNING]
>如果您未同时配置这两个密钥的回退，则可能会导致迁移期间出现停机。

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

请参阅 [使用配置管道](/help/operations/config-pipeline.md#common-syntax)，了解 `data` 节点上方属性的描述。`kind`属性值应为&#x200B;*CDN*，`version`属性应设置为`1`。

其他属性包括：

* 包含子`authentication`节点的`data`节点。
* 在`authentication`下，有一个`authenticators`节点和一个`rules`节点，两者都是数组。
* 身份验证者：用于声明令牌或凭据的类型，在本例中是清除密钥。 它包括以下属性：
   * name — 描述性字符串。
   * 类型 — 必须清除。
   * purgeKey1 — 其值必须引用[Cloud Manager机密类型的环境变量](/help/operations/config-pipeline.md#secret-env-vars)。 对于“已应用服务”字段，选择全部。 建议值（例如`${{CDN_PURGEKEY_031224}}`）反映添加日期。
   * purgeKey2 — 用于轮换密钥，下面的[轮换密钥](#rotating-secrets)部分中对此进行了说明。 必须声明`purgeKey1`和`purgeKey2`中的至少一个。
* 规则：用于声明应使用哪些验证器，以及它是否用于发布和/或预览层。  它包括：
   * 名称 — 描述性字符串
   * when — 根据[流量过滤器规则](/help/security/traffic-filter-rules-including-waf.md)文章中的语法确定何时应评估规则的条件。 通常，它包括当前层的比较（例如，发布）。
   * 操作 — 必须指定“authenticate”（身份验证），并引用目标身份验证器。

>[!NOTE]
>在部署引用清除密钥的配置之前，必须将清除密钥配置为[机密类型Cloud Manager环境变量](/help/operations/config-pipeline.md#secret-env-vars)。 建议使用长度最小为32字节的唯一随机密钥；例如，Open SSL加密库可以通过执行命令openssl rand -hex 32来生成随机密钥

您可以引用[教程](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/caching/how-to/purge-cache)，该教程侧重于配置清除密钥和执行CDN缓存清除。

## 基本身份验证 {#basic-auth}

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
  authentication:
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

请参阅 [使用配置管道](/help/operations/config-pipeline.md#common-syntax)，了解 `data` 节点上方属性的描述。`kind`属性值应为&#x200B;*CDN*，`version`属性应设置为`1`。

此外，语法包括：

* 包含`authentication`节点的`data`节点。
* 在`authentication`下，有一个`authenticators`节点和一个`rules`节点，两者都是数组。
* 验证者：在此场景中，声明一个基本验证者，该验证者具有以下结构：
   * 名称 — 描述性字符串
   * 类型 — 必须为`basic`
   * 一个最多包含10个凭据的数组，每个凭据包含以下名称/值对，最终用户可以在基本身份验证对话框中输入这些名称/值对：
      * user — 用户的名称。
      * 密码 — 其值必须引用[Cloud Manager密钥类型环境变量](/help/operations/config-pipeline.md#secret-env-vars)，并且选择&#x200B;**所有**&#x200B;作为服务字段。
* 规则：用于声明应使用哪些身份验证器，以及应保护哪些资源。 每个规则包括：
   * 名称 — 描述性字符串
   * when — 根据[流量过滤器规则](/help/security/traffic-filter-rules-including-waf.md)文章中的语法确定何时应评估规则的条件。 通常，它包括对发布层或特定路径的比较。
   * 操作 — 必须在引用的目标验证者中指定“authenticate”，对于此方案而言，这是基本验证

>[!NOTE]
>在部署引用密码的配置之前，必须将密码配置为[机密类型Cloud Manager环境变量](/help/operations/config-pipeline.md#secret-env-vars)。

## 旋转密钥 {#rotating-secrets}

定期更改凭据是一种良好的安全做法。 请记住，环境变量不应直接更改，而应创建新密钥并在配置中引用新名称。

虽然清除键也可使用相同的策略，但此用例使用边缘键的示例如下所示。

1. 最初只定义了`edgeKey1`，在本例中引用为`${{CDN_EDGEKEY_052824}}`，作为推荐的约定，它反映创建日期。

   ```
   authentication:
     authenticators:
       - name: edge-auth
         type: edge
         edgeKey1: ${{CDN_EDGEKEY_052824}}
   ```

1. 轮换密钥时，请创建新的Cloud Manager密钥，例如`${{CDN_EDGEKEY_041425}}`。
1. 在配置中，从`edgeKey2`引用它并进行部署。

   ```
   authentication:
     authenticators:
       - name: edge-auth
         type: edge
         edgeKey1: ${{CDN_EDGEKEY_052824}}
         edgeKey2: ${{CDN_EDGEKEY_041425}}
   ```

1. 一旦确定不再使用旧的边缘密钥，请从配置中删除`edgeKey1`以删除该密钥。

   ```
   authentication:
     authenticators:
       - name: edge-auth
         type: edge
         edgeKey2: ${{CDN_EDGEKEY_041425}}
   ```

1. 从Cloud Manager中删除旧密钥引用(`${{CDN_EDGEKEY_052824}}`)并进行部署。

1. 准备下一次轮换时，请遵循相同的过程，但这次您将向配置中添加`edgeKey1`，并引用名为的新Cloud Manager环境密钥，例如`${{CDN_EDGEKEY_031426}}`。

   ```
   authentication:
     authenticators:
       - name: edge-auth
         type: edge
         edgeKey2: ${{CDN_EDGEKEY_041425}}
         edgeKey1: ${{CDN_EDGEKEY_031426}}
   ```

当旋转在请求标头中设置的密钥（例如针对后端进行身份验证）时，建议分两步进行旋转，以确保标头值切换时没有临时间隙。

1. 旋转前的初始配置。 在此状态下，将旧密钥发送到后端。

   ```
   requestTransformations:
     rules:
       - name: set-api-key-header
         actions:
           - type: set
             reqHeader: x-api-key
             value ${{API_KEY_1}}
   ```

1. 通过两次设置相同的标头来引入新键`API_KEY_2`（新键应在旧键之后设置）。 部署此项后，您将在后端中看到新键。

   ```
   requestTransformations:
     rules:
       - name: set-api-key-header
         actions:
           - type: set
             reqHeader: x-api-key
             value ${{API_KEY_1}}
           - type: set
             reqHeader: x-api-key
             value ${{API_KEY_2}}
   ```

1. 从配置中删除旧键`API_KEY_1`。 部署此密钥后，您将在后端看到新密钥，可以安全地删除旧密钥的环境变量。


   ```
   requestTransformations:
     rules:
       - name: set-api-key-header
         actions:
           - type: set
             reqHeader: x-api-key
             value ${{API_KEY_2}}
   ```


