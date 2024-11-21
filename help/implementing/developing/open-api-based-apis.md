---
title: 基于OpenAPI的API
description: 了解AEM as a Cloud Service对基于OpenAPI的API的支持
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 9259b064a0a03db67333c522ebd918883859018f
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 0%

---


# 基于OpenAPI的API {#openapi-based-apis}

>[!NOTE]
>
>OpenAPI作为早期访问计划的一部分提供。 如果您有兴趣访问它们，我们建议您通过电子邮件向[aem-apis@adobe.com](mailto:aem-apis@adobe.com)发送用例说明。

较新的AEM as a Cloud Service API遵循OpenAPI规范，因此可生成一致、有良好文档记录且用户友好的API。 以下页面提供了深入的信息：

* [端到端教程](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/aem-apis/invoke-openapi-based-aem-apis)，介绍如何配置和调用基于OpenAPI的AEM API。
* 信息性[指南](https://developer.adobe.com/experience-cloud/experience-manager-apis/guides/)，包括[API概念和语法](https://developer.adobe.com/experience-cloud/experience-manager-apis/guides/how-to/)。
* API端点[引用文档](https://developer.adobe.com/experience-cloud/experience-manager-apis/)，其中一些API基于OpenAPI，如[此Sites API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/)。 参考文档还包括API游乐场，这使得使用随Adobe Developer Console生成的持有者令牌尝试端点变得简单。

常见的API用例涉及与CRM或PIM等系统的集成，这些系统调用AEM API来检索或保留数据。 作为集成实现的一部分，应用程序可以订阅[AEM发出的事件](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/aem-eventing/overview)，这可以在AdobeApp Builder或其他基础架构中触发业务逻辑。

支持的API身份验证类型因端点而异，但可以是OAuth服务器到服务器、OAuth Web应用程序和OAuth单页应用程序(SPA)。

>[!NOTE]
>
> [端到端教程](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/aem-apis/invoke-openapi-based-aem-apis)是推荐的资源，用于了解如何配置和调用基于OpenAPI的AEM API。


## 配置API访问 {#configuring-api-access}

许多基于OpenAPI的AEM API需要身份验证，这需要使用[Adobe Developer Console](https://developer.adobe.com/developer-console/docs/guides/)生成凭据。 配置涉及以下步骤，将在教程中进行说明：

1. 确保更新您的AEM程序的[产品配置文件](/help/onboarding/aem-cs-team-product-profiles.md#aem-product-profiles)，并启用适当的服务来访问所需的API。
1. 在Adobe Developer Console中创建新项目，并将所需的API添加到项目中，同时选择适当的身份验证类型。
1. 生成凭据，在调用API时，稍后将使用该凭据交换持有者令牌。
1. 通过配置YAML文件在环境中注册客户端ID，该文件使用配置管道（或RDE的命令行）部署。

## 注册客户端ID {#registering-a-client-id}

客户端ID将Adobe Developer Console项目中的APis作用域扩展到特定AEM环境。 其实现方式如下：

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





