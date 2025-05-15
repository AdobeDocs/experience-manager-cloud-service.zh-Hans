---
title: 基于 OpenAPI 的 API
description: 了解AEM as a Cloud Service对基于OpenAPI的API的支持
feature: Developing
role: Admin, Architect, Developer
exl-id: 4aeafba9-8f9e-4ecb-9e37-8d048b0474cc
source-git-commit: 7feb0c4061ebc9e7a581537fb6e9cad104cda65d
workflow-type: tm+mt
source-wordcount: '638'
ht-degree: 1%

---

# 基于 OpenAPI 的 API {#openapi-based-apis}

较新的AEM as a Cloud Service API遵循OpenAPI规范，因此提供了一组一致且有充分文档记录的API。

>[!NOTE]
>
> 建议使用[端到端教程](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-learn/cloud-service/aem-apis/invoke-openapi-based-aem-apis)来了解如何配置和调用基于OpenAPI的AEM API。

对于需要身份验证的端点，身份验证方法因端点而异，但可能使用OAuth服务器到服务器、OAuth Web应用程序或OAuth单页应用程序(SPA)。 凭据是通过[Adobe Developer Console](https://developer.adobe.com/developer-console/)中的项目配置的。

常见API用例涉及与CRM或PIM等系统的集成，这些系统调用AEM API来检索或保留数据。 作为集成实施的一部分，应用程序可能会订阅[AEM发出的事件](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/aem-eventing/overview)，这些事件可能会在Adobe App Builder或其他基础架构中触发业务逻辑。

本文档可用作概览，但以下页面提供了更深入的文档：

* [参考文档](https://developer.adobe.com/experience-cloud/experience-manager-apis/)中基于OpenAPI的API部分的链接。 每个API的参考文档还包含一个API游乐场，这使得使用随Adobe Developer Console生成的持有者令牌来尝试端点更容易。

* 信息性[指南](https://developer.adobe.com/experience-cloud/experience-manager-apis/guides/)，包括[API概念和语法](https://developer.adobe.com/experience-cloud/experience-manager-apis/guides/how-to/)。

* 描述[身份验证方法](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/aem-apis/openapis/overview#authentication-support)和其他概念的顶级教程。

* 一个教程，其中包含重点介绍[如何配置基于OpenAPI的API](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/aem-apis/openapis/setup)的视频。

* [关于使用服务器到服务器身份验证策略配置和调用OpenAPI的端到端教程](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-learn/cloud-service/aem-apis/invoke-openapi-based-aem-apis)。 此外，还可以找到有关Web应用程序和单页应用程序身份验证方法的类似教程。

## 配置API访问 {#configuring-api-access}

某些基于OpenAPI的AEM API需要身份验证，这需要使用[Adobe Developer Console](https://developer.adobe.com/developer-console/)生成凭据。 配置涉及以下步骤：

1. AEM as a Cloud Service环境的现代化。
1. 使用产品配置文件启用对AEM API的访问。 产品配置文件与表示具有预定义访问控制列表(ACL)的AEM用户组的服务相关联。 默认情况下，某些服务与特定产品配置文件关联，而其他服务则需要显式关联；例如，AEM Assets API Users服务未与任何[产品配置文件](/help/onboarding/aem-cs-team-product-profiles.md#aem-product-profiles)关联，因此您必须启用它才能使用AEM Assets API。 有关详细信息，请参阅[启用AEM API访问](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/aem-apis/openapis/setup#enable-aem-apis-access)教程步骤。
1. 要添加服务器到服务器身份验证，设置集成的用户必须是组织在Adobe Admin Console中的系统管理员，或者作为开发人员添加到与服务关联的产品配置文件中。 有关详细信息，请参阅[启用AEM API访问](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/aem-apis/openapis/setup#enable-aem-apis-access)教程步骤。
1. 创建一个Adobe Developer Console (ADC)项目。
1. 配置ADC项目。 这将生成凭据，在调用API时，稍后将使用这些凭据交换持有者令牌。
1. 配置AEM实例以启用ADC项目通信。 这涉及通过配置和部署YAML文件在环境中注册客户端ID，如下面的[注册客户端ID](#registering-a-client-id)部分中所述。

有关详细的分步说明，请参阅[设置基于OpenAPI的API教程](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/aem-apis/openapis/setup)。

### 注册客户端ID {#registering-a-client-id}

客户端ID将Adobe Developer Console项目中的API范围扩展到特定的AEM环境。 其实现方式如下：

1. 创建名为`api.yaml`或与其类似的文件，其配置类似于下面的代码片段，包括所需的层（创作、发布、预览）。 `Client_id`值应来自您的Adobe Developer Console API项目。

   [配置管道](/help/operations/config-pipeline.md#common-syntax)文章中描述了`kind`、`version`和`metadata`属性。 `kind`属性值应设置为&#x200B;*API*，`version`属性应设置为&#x200B;*1*。

   ```
   kind: "API"
   version: "1"
   metadata:
     envTypes: ["dev"]
   data:
     allowedClientIDs:
       author:
         - "<client_id>"
       publish:
         - "<client_id>"
       preview:
         - "<client_id>"
   ```

1. 将文件放置在名为`config`或类似的顶级文件夹下，如[配置管道](/help/operations/config-pipeline.md#folder-structure)中所述。
1. 对于RDE（使用命令行工具）以外的环境类型，在Cloud Manager中创建目标部署配置管道，如配置管道文章中的[此部分](/help/operations/config-pipeline.md#creating-and-managing)所引用。 请注意，全栈管道和Web层管道不部署配置文件。
1. 部署配置。
