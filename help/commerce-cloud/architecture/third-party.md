---
title: AEM和第三方商务集成（使用Commerce Integration Framework）
description: AEM和第三方商务集成（使用Commerce Integration Framework）
translation-type: tm+mt
source-git-commit: c5694cf8651cf8ba5331c730fa1b1180310dd35a
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 0%

---


# AEM和第三方商务集成（使用Commerce Integration Framework） {#aem-third-party}

企业企业可能需要额外的第三方商务解决方案来支持其店面。 商务集成框架(CIF)可用于此类集成方案，除Magento外，第三方商务解决方案还需要与AEM集成。 CIF提供了诸如加速器参考店面、AEM CIF核心组件和创作工具等元素，这些工具可用于现成Magento。 要集成AEM和第三方商务解决方案并重复使用这些CIF元素，需要进行一些额外开发。

## 架构 {#architecture}

总体架构如下：

![AEM非Magento/第三方体系结构概述](/help/commerce-cloud/assets/AEM_nonMagento_Architecture.JPG)

AEM -Magento和AEM —— 第三方商务的集成体系结构的主要区别在于添加了集成和数据转换层，如上图所示。 集成层需要托管在Adobe I/O Runtime平台上，该平台是Adobe的无服务器平台。 你可以在这里进一步了解 [Adobe I/O Runtime](https://www.adobe.io/apis/experienceplatform/runtime.html)。

此集成层的目的是将非Magento或第三方的API映射到Adobe商务API(MagentoGraphQL API)。 此映射允许 [AEM CIF核心组件](https://github.com/adobe/aem-core-cif-components) 和CIF创作工具从非Magento解决方案检索数据。 采用这种方法，集成层封装了集成逻辑，并在AEM和第三方解决方案之间产生了关注点分离。 这允许以不可知的方式使用CIF元素与各种第三方解决方案。 在简介中介绍了在项目中使用CIF元素的 [优势](/help/commerce-cloud/overview.md)。

## 开发集成 {#develop-integration}

为了帮助您开始构建所需的集成层，将非Magento/第三方解决方案与AEM集成，我们创建了一个参考实 [施来](https://github.com/adobe/commerce-cif-graphql-integration-reference) 演示这一点。 此引用可用作项目中的起点。
