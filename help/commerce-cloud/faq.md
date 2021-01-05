---
title: AEM -Magento集成（使用Commerce Integration Framework FAQ）
description: AEM -Magento集成（使用Commerce Integration Framework FAQ）
translation-type: tm+mt
source-git-commit: cafe8825fe34f158c74b94b95b7252394de26e4d
workflow-type: tm+mt
source-wordcount: '1321'
ht-degree: 0%

---


# AEM -Magento集成（使用Commerce Integration Framework FAQ）


## 1. GraphQL是否仅用于Magento，或者它是否可用于查询在AEM上创作的内容？ JCR?

Adobe已采用Magento的GraphQL API作为其官方商务API来处理所有与商务相关的数据。 因此，AEM使用GraphQL通过I/O Runtime与Magento和任何商务引擎交换商务数据。

## 2.Adobe I/O是如何发挥作用的？ AEM是否直接与Magento沟通？

AEM无需I/O Runtime层即可直接连接到Magento。 如果需要将非Magento商务后端（第三方解决方案）与AEM集成，则I/O Runtime平台可用于托管映射层，以将MagentoGraphQL API连接到任何第三方解决方案API。 有关此的详细信息，请参阅此[引用实现](https://github.com/adobe/commerce-cif-graphql-integration-reference)。 对于非Magento解决方案，AEM将配置为指向I/O Runtime端点。

I/O运行时平台还可用于扩展或自定义商务服务。 对于此用例，您将调用I/O Runtime端点，该端点随后将承载各个服务的自定义实现。 集成和扩展用例可以结合使用。

## 3.产品资产（图像）是否可以通过Magento管理员从AEM进行存储和引用？ 如何消费Dynamic Media的资产？

目前没有AEM Assets-Magento整合。 作为解决方法，您可以在AEM Assets存储产品资产（图像），但必须在Magento中手动存储资产URL。 Dynamic Media现在是AEM Assets的一部分，将采取同样的方式工作。

## 4.在何处部署Magento是否重要？ （在云端或在云端）

在何处部署Magento并不重要。 无论部署模式如何，集成和新的AEM Venia商店前端都将正常工作。 但是，如果它是基于经批准的E2E参考体系结构部署的，则将根据收集的代表企业客户用户档案的性能KPI运行E2E测试。 因此，这将为您提供可用作基准的其他信息。

## 5.如何在AEM中创建目录页面或产品页面？ 他们如何在AEM中坚持？

目录页面和产品页面是根据通用目录和产品页面模板在AEM中动态创建和缓存的。 不导入任何产品或目录数据并将其存储在AEM中。

## 6.是否还可以通过Dispatcher缓存定价和其他数据。 这是否会带来频繁的缓存失效挑战？

动态数据（如价格或库存）不会缓存在调度程序上。 动态数据是通过GraphQL API直接通过Web组件在客户端获取的。 只有静态数据(如产品或类别数据)会缓存在调度程序上。 如果产品数据发生更改，则需要缓存失效。

## 7. AEM Dispatcher的缓存失效如何与AEM-Magento配合工作？

我们建议为在调度程序上缓存的页面设置基于TTL的缓存失效。 对于价格或库存等动态信息，我们建议呈现日期客户端。 有关基于TTL的缓存失效的详细信息，请参阅[AEM Dispatcher](https://helpx.adobe.com/experience-manager/kb/optimizing-the-dispatcher-cache.html)

## 8.为什么不使用We.Retail?

Venia主题(由Magento开发)首先用于移动，并与Magento的PWA保持一致。 Venia主题代表CSS样式和AEM核心组件的最新功能。

## 9.在Magento中更新产品数据时，这是否是实时推送到AEM? 还是批处理？

与AEMCloud Service一起使用的CIF加载项使数据能够从Magento流到AEM on-demand。 因此，当Magento中有更新时，这不是实时推送或批处理。

## 10.是否建议通过商务跨AEM内容进行统一搜索？

提供了产品搜索参考实施，但没有对内容进行统一搜索。 此功能通常非常针对客户，并且在项目特定级别上得到更好的解决。

## 11.搜索如何与AEM-Magento一起使用CIF?

CIF提供搜索栏和搜索结果组件。 搜索栏组件会向Magento发送包含搜索词的GraphQL请求。 Magento然后返回包含产品名称、价格、辅助信息域等的产品列表。 搜索结果组件随后会在AEM中创建的搜索结果页面的库视图中显示搜索结果。 “搜索”支持基本全文搜索。 我们使用SLUG/url键来构建对PDP的引用。

## 11.如何在MSM或翻译中使用产品数据？

产品数据通常已在PIM或Magento中翻译。 AEM -Magento集成支持与多个Magento商店和商店视图的连接。 在MSM设置中，通常一个AEM站点链接到一个Magento存储视图。

## 13. CIF公司如何与其他商业平台合作？

通过I/O Runtime平台与其他商务解决方案(非Magento)等第三方解决方案集成。  我们构建了一个[参考实现](https://github.com/adobe/commerce-cif-graphql-integration-reference)来演示如何实现。 这允许通过在任何第三方商务平台上公开MagentoGraphQL API来重用[AEM CIF云连接器](https://github.com/adobe/commerce-cif-connector)和[AEM CIF核心组件](https://github.com/adobe/aem-core-cif-components)。 为了优惠最大的灵活性和可伸缩性，此集成层部署在无服务器[Adobe I/O Runtime平台](https://www.adobe.io/apis/experienceplatform/runtime.html)上。

## 14.是否有一种方法能够用商业文本增强产品数据？ 你从哪儿做的？ 在AEM还是在Magento?

实现此目的有多种方法，具体取决于用例。 一种方法是使用自定义属性。 允许AEM作者在AEM的产品编辑器中转换这些字段，并将数据同步回PIM。 另一个选项是利用AEM Experience Fragments，将其注入产品页面。

## 15.使用Adobe I/O Runtime平台时，AEM-Magento之间的集成是否发生变化？

希望扩展商务服务的客户可以使用I/O运行时平台上托管的相同集成和编写操作序列，以注入业务逻辑并丰富商务服务。

## 16.由于AEM根据AEM中的通用模板动态创建产品和目录页面，如果要打开CRXDE Lite并检查内容下，我会看到什么？ 我是否会根据Magento中的产品看到整个产品树？ 如果不是，作者将如何增强这些页面？

不再有JCR目录或产品页面。 见问题12。

## 17. SPA会与AEM SPA编辑一起进行前期工作吗？

AEM可用作任何类型的商店前的创作工具。 目前，混合渲染用于新店面。 将来，AEM将用于SPA和PWA的创作。

## 18. PIM如何进入此框架？

PIM数据通过GraphQL请求暴露给AEM和客户端。 我们的推荐是将PIM与商务引擎(Magento或其他)集成，这样PIM数据就可以从商务引擎中检索。

## 19.在整个表示层使用AEM时，我们如何确保PCI的兼容性？

使用AEM在AMS和Magento云部署时，必须使用抽象的支付方法。 这使得浏览器客户端与支付网关提供商直接通信，以便Adobe云或Magento云都不保存或传递持卡人数据。 此方法可覆盖技术堆栈和数据中心的PCI合规性。 但是，还有其他事项需要考虑完全符合PCI规范，如员工如何与系统和数据交互。 有关MagentoPCI规范的更多信息，请参阅https://magento.com/pci-compliance

## 20.如何申请I/O Runtime试用许可？

您可以在此处](https://github.com/AdobeDocs/adobeio-runtime/blob/master/overview/request_a_trial.md)申请试用许可证以使用I/O运行时[。



