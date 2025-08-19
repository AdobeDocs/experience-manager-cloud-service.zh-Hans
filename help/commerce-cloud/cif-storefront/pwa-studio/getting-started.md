---
title: 适用于PWA Studio的AEM扩展快速入门
description: 了解如何使用PWA Studio部署AEM headless Content和Commerce项目。
topics: Commerce
feature: Commerce Integration Framework
thumbnail: 37843.jpg
exl-id: a7c187ba-885e-45bf-a538-3c235b09a0f1
role: Admin
index: false
source-git-commit: 80bd8da1531e009509e29e2433a7cbc8dfe58e60
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 0%

---


# 适用于PWA Studio的AEM扩展快速入门 {#getting-started-pwa}

开箱即用的PWA Studio通过GraphQL与Adobe Commerce无缝集成，提供了无限多的选项用于创建创新和引人入胜的店面及其他数字体验。

内容片段是具有预定义结构的内容片段，允许以无头方式使用GraphQL作为各种格式（例如，JSON、Markdown）的API并独立渲染。 内容片段包括GraphQL所需的所有数据类型和字段，以确保您的应用程序仅请求可用内容并接收预期内容。 它们在结构方面提供的灵活性使其非常适合在多个位置和多个渠道上使用。

使用Adobe Experience Manager中的内容片段模型编辑器，可以轻松设计所需的结构。 将Adobe Experience Manager内容片段（或任何其他数据）与PWA Studio应用程序集成的主要挑战是从多个GraphQL端点获取数据。 这是因为开箱即用地使用PWA Studio与单个Adobe Commerce GraphQL端点配合使用。

## 架构 {#architecture}

![PWA headless架构](/help/commerce-cloud/cif-storefront/assets/PWA-Studio_Architecture.png)

## 设置PWA Studio {#setup-pwa}

按照Adobe Commerce [PWA Studio文档](https://developer.adobe.com/commerce/pwa-studio/tutorials/)设置您的PWA Studio应用程序。

要将PWA Studio与AEM的GraphQL端点连接，您可以使用[适用于PWA Studio的AEM扩展。](https://github.com/adobe/aem-pwa-studio-extensions)

1. 签出存储库

1. 在PWA Studio应用程序中，添加扩展作为开发依赖项。

   ```javascript
   yarn add --dev file:{path-to-extension}/extension
   ```

1. 将Apollo Link包装器添加到您的PWA Studio应用程序。 在`pwa-root/src/index.js`中进行以下更改：

   ```javascript
     import { linkWrapper } from '@adobe/pwa-studio-aem-cfm-blog-extension';
   
   // ...
   
   <Adapter apiBase={apiBase} apollo={{ link: linkWrapper(apolloLink) }} store={store}>
   ```

   您可以在[linkWrapper.js.](https://github.com/adobe/aem-pwa-studio-extensions/blob/master/aem-cfm-blog-extension/extension/src/linkWrapper.js)中找到有关阿波罗客户端自定义设置的更多详细信息

1. 若要使用博客条目扩展导航组件，请将以下自适应项添加到`pwa-root/local-intercept.js`：

   ```javascript
   const addBlogToNavigation = require('@adobe/pwa-studio-aem-cfm-blog-extension/src/addBlogToNavigation');
   
   function localIntercept(targets) {
       addBlogToNavigation(targets);
   }    
   ```

   您可以在[addBlogToNavigation.js](https://github.com/adobe/aem-pwa-studio-extensions/blob/master/aem-cfm-blog-extension/extension/src/addBlogToNavigation.js)和PWA Studio的[可扩展性框架](https://developer.adobe.com/commerce/pwa-studio/guides/general-concepts/extensibility/)文档中查找有关自定义导航组件的更多详细信息。

1. Apollo客户端将预期AEM GraphQL终结点位于`<https://pwa-studio/endpoint.js>`。 要将端点映射到此位置，请自定义PWA Studio应用程序的“向上”配置：
a.将AEM_CFM_GRAPHQL变量添加到pwa-root/.env，并将其调整为指向您的AEM内容片段GraphQL端点。

   示例：`AEM_CFM_GRAPHQL=<http://localhost:4503/content/graphql/global>`

   b.将代理解析程序添加到UPGRADE配置。 UPPER配置示例可能如下所示：

```json
   response:
     resolver: conditional
     when:
       - matches: request.url.pathname
         pattern: ^/endpoint.json(/|$)
         use: aemProxy
     default: veniaResponse

   aemProxy:
     resolver: proxy
     target: env.AEM_CFM_GRAPHQL
     ignoreSSLErrors: true

   status: response.status
   headers: response.headers
   body: response.body
```

## 设置AEM {#setup-aem}

按照AEM内容片段文档中的说明，为AEM项目设置GraphQL端点。 此外，在您的AEM项目中，添加以下配置以允许PWA Studio应用程序访问GraphQL端点：

* Adobe Granite跨源资源共享策略(com.adobe.granite.cors.impl.CORSPolicyImpl)

  将allowedorigin属性设置为PWA应用程序的完整主机名。

  示例： `<https://pwa-studio-test-vflyn.local.pwadev:9366>`

* Apache Sling引用过滤器(org.apache.sling.security.impl.ReferrerFilter.cfg.json)

  将allow.hosts属性设置为PWA应用程序的主机名。

  示例：`pwa-studio-test-vflyn.local.pwadev`

您可以在[此处](https://github.com/adobe/aem-pwa-studio-extensions/tree/master/aem-cfm-blog-extension/aem/config/src/main/content/jcr_root/apps/blog-demo/config)找到这两种配置的完整示例。

为了显示GraphQL端点，有一些通过内容包准备的示例内容片段模型和数据。 这些组件与随PWA Studio扩展提供的React组件配合使用非常好。

## 使用方法 {#how-to-use}

此扩展被视为如何将PWA Studio应用程序与AEM连接以通过GraphQL检索和呈现内容的示例实施。

根据您的用例，要创建自己的自定义内容片段模型，这些模型会产生自定义GraphQL架构，然后您自己的React组件可以使用该架构。

生产设置可能在多个方面有所不同。

* 您可以具有一个联合GraphQL端点，它结合了AEM和Adobe Commerce GraphQL数据，而不是自定义Apollo客户端。
* 您的PWA Studio应用程序可以直接使用AEM GraphQL端点URL，而无需具有UPLOAD的代理。 代理也可以移到其他层（例如，CDN）。
* 哪一种方法最适合您在很大程度上还取决于您如何将PWA Studio应用程序交付给用户。

此扩展提供了两个示例。

### 博客 {#blog}

根据某些内容片段模型显示博客帖子。 此外，它还包含有关如何配置Apollo客户端以使其与AEM GraphQL端点一起使用以及如何在PWA Studio中扩展导航组件的示例。 有关详细信息，请参阅[GitHub](https://github.com/adobe/aem-pwa-studio-extensions/tree/master/aem-cfm-blog-extension)。

### pdp扩充 {#pdp-enrichment}

使营销人员能够轻松地使用作为内容片段管理的附加内容来扩充PDP。  有关详细信息，请参阅[GitHub](https://github.com/adobe/aem-pwa-studio-extensions/tree/master/aem-cif-product-page-extension)。
