---
title: 使用Commerce integration framework集成AEM和第三方Commerce
description: 企业可能需要其他第三方商业解决方案来强化其店面。 Commerce integration framework(CIF)可用于此类集成方案，以使用I/O运行时将第三方商业解决方案连接到Adobe Experience Manager。
thumbnail: cif-third-party-architecture.jpg
exl-id: 3ebdb8eb-65ba-46be-aca3-6c06c8d1600c
feature: Commerce Integration Framework
role: Admin
source-git-commit: 0e328d013f3c5b9b965010e4e410b6fda2de042e
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 0%

---

# 使用Commerce integration framework集成AEM和第三方Commerce {#aem-third-party}

非Adobe Commerce解决方案的集成是CIF的常见场景。 通过集成层连接具有不同API和架构的第三方解决方案。

## 架构 {#architecture}

整体架构如下：

![AEM非Magento/第三方架构概述](../assets//AEM_nonMagento_Architecture.png)

此集成层的目的是根据Experience Manager外部支持的Adobe Commerce GraphQL API和架构映射第三方API和架构。 借助此封装，集成逻辑和系统可以更新，而无需更改Experience Manager中的代码。

## 集成的解决方案要求

在Experience Manager按需检索数据时，需要产品目录的实时API。

>[!TIP]
>
>如果没有可用的实时API，则应使用具有API的外部产品缓存进行集成。 示例 [Adobe Commerce开放源代码](https://business.adobe.com/products/magento/open-source.html).

无需实施完整的GraphQL架构，只需实施架构的对象即可启用所需的用例。

## 后端用例

CIF通过实时产品目录访问和产品体验管理工具扩展了Experience Manager。 这种无缝集成使作者能够在需要时使用嵌入的UI访问商务数据，而无需离开内容上下文。

需要产品目录API的集成才能解锁这些用例。

## 前端用例

[AEM CIF核心组件](https://github.com/adobe/aem-core-cif-components) 通过CIF支持的Adobe Commerce API检索和交换数据。 要重用组件，必须实施相应的API。

对性能关键的客户端组件的建议是直接与第三方解决方案通信以避免延迟。

## 开发集成 {#develop-integration}

Adobe建议您使用 [Adobe Developer运行时](https://developer.adobe.com/runtime/) 用于集成层。 它包含在适用于第三方的CIF附加组件中。 由于它使用类似微服务的方法，因此非常适合轻松集成多个解决方案。

此 [参考实现](https://github.com/adobe/commerce-cif-graphql-integration-reference) 是构建与您的商务解决方案集成的良好起点。 尽管它支持GraphQL，但它也可以与任何其他类型的API（例如REST）集成。

如果第三方层可用（例如，Mulesoft），或者集成构建在第三方解决方案之上，则不需要此集成层。

## 预建连接器 {#connectors}

连接器为项目提供了一个良好的开始。 它们附带商业解决方案特定的连接和默认API映射。 这些连接器由第三方构建，不由Adobe维护。 请联系相应的合作伙伴以了解相关信息。

* [SAP COMMERCE](https://github.com/diconium/commerce-cif-graphql-integration-hybris)，由Diconium构建
* [Commercetools](https://github.com/diconium/commerce-cif-graphql-integration-commercetool)，由Diconium构建

>[!TIP]
>
>虽然连接器可帮助项目加速商务集成，但它们并不是即插即用的。 企业商务解决方案高度自定义，需要自定义集成。 需要很好地了解Commerce平台、Adobe Commerce GraphQL架构和Adobe I/O Runtime。
