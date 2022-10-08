---
title: AEM和第三方商务集成使用商务集成框架
description: 企业企业可能需要额外的第三方商务解决方案来支持其店面。 商务集成框架(CIF)可用于此类集成方案，以使用I/O运行时将第三方商务解决方案连接到Adobe Experience Manager。
thumbnail: cif-third-party-architecture.jpg
exl-id: 3ebdb8eb-65ba-46be-aca3-6c06c8d1600c,42dd8922-540d-4a93-9e45-b5e83dc11e16
source-git-commit: ca849bd76e5ac40bc76cf497619a82b238d898fa
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 0%

---

# AEM和第三方商务集成使用商务集成框架 {#aem-third-party}

非Adobe Commerce解决方案的集成是CIF的常见情况。 具有不同API和模式的第三方解决方案通过集成层进行连接。

## 架构 {#architecture}

总体架构如下：

![AEM非Magento/第三方架构概述](../assets//AEM_nonMagento_Architecture.png)

此集成层的用途是根据支持的Adobe Commerce GraphQL API和架构在Experience Manager外映射第三方API和架构。 通过这种封装，集成逻辑和系统可以更新，而无需更改Experience Manager内的代码。

## 集成的解决方案要求

当Experience Manager按需检索数据时，需要产品目录的实时API。

>[!TIP]
>
>如果没有可用的实时API，则应使用包含API的外部产品缓存进行集成。 示例 [Magento开源](https://magento.com/products/magento-open-source).

无需实施完整的GraphQL模式，只需该模式的对象即可启用所需的用例。

## 后端用例

CIF通过实时产品目录访问和产品体验管理工具来扩展Experience Manager。 通过此无缝集成，作者可以根据需要使用嵌入式UI访问商务数据，而无需离开内容上下文。

需要集成产品目录API才能解锁这些用例。

## 前端用例

[AEM CIF核心组件](https://github.com/adobe/aem-core-cif-components) 通过CIF支持的Adobe Commerce API检索和交换数据。 要重复使用组件，需要实施相应的API。

性能关键的客户端组件的建议是直接与第三方解决方案通信，以避免延迟。

## 开发集成 {#develop-integration}

我们建议使用 [Adobe I/O Runtime](https://www.adobe.io/apis/experienceplatform/runtime.html) ，以用于集成层。 它包括在第三方的CIF附件中。 由于它与微服务类方法配合使用，因此非常适合轻松集成多个解决方案。

的 [参考实施](https://github.com/adobe/commerce-cif-graphql-integration-reference) 是构建与商务解决方案集成的绝佳起点。 尽管它支持GraphQL，但也可以与任何其他类型的API（如REST）集成。

如果第三方层可用（例如Mulesoft）或集成以第三方解决方案为基础构建，则无需使用此集成层。

## 预建连接器 {#connectors}

连接器为项目提供了良好的开始。 它们附带特定于商务解决方案的连接和默认API映射。 这些连接器由第三方构建，不由Adobe维护。 请联系相应的合作伙伴以获取相关信息。

* [SAP Commerce](https://github.com/diconium/commerce-cif-graphql-integration-hybris)，由迪库铵建造
* [Commercetools](https://github.com/diconium/commerce-cif-graphql-integration-commercetool)，由迪库铵建造

>[!TIP]
>
>虽然连接器有助于项目加快商务集成，但它们不是即插即用的。 企业商务解决方案通常需要大量自定义，并且需要自定义集成。 需要充分了解商务平台、Adobe Commerce GraphQL架构和Adobe I/O Runtime。
