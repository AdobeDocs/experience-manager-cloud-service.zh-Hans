---
title: AEM - Commerce Integration using Commerce Integration Framework常见问题解答
description: AEM - Commerce Integration using Commerce Integration Framework常见问题解答
translation-type: tm+mt
source-git-commit: ad831b2cc3657666678662eeff0eaf371ce4da49
workflow-type: tm+mt
source-wordcount: '1284'
ht-degree: 0%

---


# AEM - Commerce Integration using Commerce Integration Framework常见问题解答


## 1. CIF GraphQL是否仅用于商务，或者它是否可用于查询在AEM. JCR上创作的内容？

Adobe已采用Magento的GraphQL API作为其所有商务相关数据的官方商务API。 因此，AEM使用GraphQL与Magento以及通过I/O Runtime与任何商务引擎交换商务数据。 此GraphQL API独立于AEM GraphQL API以访问内容片段。

## 2.Adobe I/O是如何发挥作用的？ AEM是否直接与Magento沟通？

AEM无需I/O Runtime层即可直接连接到Magento。 如果需要将非Magento商务后端（第三方解决方案）与AEM集成，则I/O Runtime平台可用于托管映射层，以将Magento GraphQL API连接到任何第三方解决方案API。 有关此的详细信息，请参阅此[参考实现](https://github.com/adobe/commerce-cif-graphql-integration-reference)。 对于非Magento解决方案，将配置AEM以指向I/O Runtime端点。

I/O Runtime平台还可用于扩展或自定义商务服务。 对于此用例，您将调用I/O Runtime端点，该端点随后将托管各个服务的自定义实现。 可以将集成和扩展用例组合在一起。

## 3.产品资产（图像）是否可以通过Magento管理员从AEM存储和引用？ 如何使用Dynamic Media中的资产？

目前还没有AEM Assets -Magento集成。 作为解决方法，您可以在AEM Assets中存储产品资产（图像），但您必须在Magento中手动存储资产URL。 Dynamic Media现在是AEM Assets的一部分，将以同样的方式工作。

## 4.商务解决方案部署在何处是否重要？ （在云中或在云中）

商务解决方案的部署位置并不重要。 无论部署模型如何，集成和新的AEM Venia商店阵线都将正常工作。 但是，如果根据经批准的E2E参考体系结构部署E2E测试，则将根据收集的表示企业客户用户档案的性能KPI运行E2E测试。 因此，这将为您提供其他信息，以便您用作基准。

## 5.如何在AEM中创建目录页面或产品页面？ 他们如何在AEM中坚持？

目录页面和产品页面是根据通用目录和产品页面模板在AEM中动态创建和缓存的。 没有产品或目录数据导入并存储在AEM中。

## 6.在您的商务解决方案中更新产品数据时，是否实时推送到AEM? 还是说，这是批量流程？

与AEM Cloud Service一起使用的CIF加载项使数据能够从商务解决方案流到AEM点播。 因此，当您的商务解决方案中存在更新时，这不是实时推送或批处理。

## 7.AEM支持哪些目录大小？

这取决于您需要考虑的其他几个方面。 目录数据和页面的缓存比率是多少？ 在高峰时段，您预计有多少个并发请求？ 您的商务解决方案的API有多大的可扩展性？

## 8. PIM如何融入这个框架？

PIM数据通过GraphQL请求暴露给AEM和客户端。 我们的推荐是将PIM与商务引擎(Magento或其他)集成，以便PIM数据随后可从商务引擎中检索。

## 9.您是否也通过Dispatcher缓存定价和其他数据。 这是否会引发频繁的缓存失效挑战？

不会在调度程序上缓存价格或库存等动态数据。 动态数据通过GraphQL API直接通过Web组件在客户端获取。 只有静态数据(如产品或类别数据)才会缓存在Dispatcher上。 如果产品数据发生更改，则需要缓存失效。

## 10. AEM Dispatcher的缓存失效如何与AEM和商务一起使用？

我们建议为在调度程序上缓存的页面设置基于TTL的缓存失效。 对于价格或库存等动态信息，我们建议呈现日期客户端。 有关基于TTL的缓存失效的详细信息，请参阅[AEM Dispatcher](https://helpx.adobe.com/experience-manager/kb/optimizing-the-dispatcher-cache.html)

## 11.是否建议使用商务跨AEM内容进行统一搜索？

提供了产品搜索参考实施，但没有对内容进行统一搜索。 此功能通常非常针对客户，并且在项目特定级别得到更好的解决。

## 12.搜索如何使用CIF与AEM和商务协作？

CIF提供搜索栏和搜索结果组件。 搜索栏组件会向商务解决方案发送包含搜索词的GraphQL请求，该解决方案随后会返回包含产品名称、价格、辅助信息域等的产品列表。 然后，搜索结果组件会在AEM中创建的搜索结果页面的库视图中显示搜索结果。 “搜索”支持基本的全文搜索。 我们使用SLUG/url键来构建对PDP的引用。

## 13.如何在MSM或翻译中使用产品数据？

产品数据通常已在PIM或Magento中翻译。 AEM - Magento集成支持连接到多个Magento商店和商店视图。 在MSM设置中，通常有一个AEM站点链接到一个Magento存储视图。

## 14. CIF如何与非Magento商务平台合作？

通过I/O Runtime平台与第三方解决方案(如其他商务解决方案(非Magento))集成。  我们构建了一个[引用实现](https://github.com/adobe/commerce-cif-graphql-integration-reference)来演示如何实现。 这允许通过在任何第三方商务平台上公开Magento GraphQL API来重复使用[AEM CIF云连接器](https://github.com/adobe/commerce-cif-connector)和[AEM CIF核心组件](https://github.com/adobe/aem-core-cif-components)。 为了优惠最大的灵活性和可伸缩性，此集成层部署在无服务器[Adobe I/O Runtime平台](https://www.adobe.io/apis/experienceplatform/runtime.html)上。

## 15.是否有办法用商业文本增强产品数据？ 你从哪儿做的？ 在AEM中还是在商务解决方案中？

我们建议在AEM中管理与营销相关的数据和内容。 使用内容片段的其他属性装饰您的商务解决方案中的产品数据，或为不结构化的内容创建体验片段并将其与您的产品链接。

## 16.使用Adobe I/O Runtime平台时，AEM-Magento之间的集成是否会发生变化？

希望扩展商务服务的客户可以使用I/O Runtime平台上托管的相同集成和写入操作序列来注入业务逻辑并丰富商务服务。

## 17. SPA商店前端是否将与AEM SPA编辑器一起使用？

AEM可用作任何种类的商店前的创作工具。 目前，在AEM商店中使用服务器端和客户端渲染（混合）。 我们将在2021年晚些时候发布PWA支持，用于无头和无头内容创作。


## 18.如何确保整个表示层使用AEM时的PCI兼容性？

建议采用抽象的支付方式。 这使得浏览器客户端与支付网关提供商直接通信，以便Adobe或商务解决方案都不持有或传递持卡人数据。 此方法只需要3级PCI兼容性。 但是，还有其他一些事项需要考虑完全符合PCI规范，例如员工如何与系统和数据交互。 有关Magento PCI兼容性的更多信息，请参阅https://magento.com/pci-compliance

## 19.如果我使用AEM和Magento云版本，此联合解决方案是否符合PCI标准？

是，可应要求提供自我评估调查表D和合规性证明。


## 20.如何申请I/O Runtime试用许可？

您可以在此处](https://adobeio.typeform.com/to/obqgRm)申请试用许可证以使用I/O Runtime [。
