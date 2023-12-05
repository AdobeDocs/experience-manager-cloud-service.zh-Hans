---
title: AEM - Commerce集成使用Commerce integration framework常见问题解答
description: AEM - Commerce集成使用Commerce integration framework常见问题解答
exl-id: 0a946d98-22c7-445d-984a-9e09c306ce45
source-git-commit: abe5f8a4b19473c3dddfb79674fb5f5ab7e52fbf
workflow-type: tm+mt
source-wordcount: '963'
ht-degree: 0%

---

# AEM - Commerce集成使用Commerce integration framework常见问题解答

## 1. CIF GraphQL是否仅用于商务，还是可用于查询在AEM JCR上创作的内容？

Adobe已采用Adobe Commerce的GraphQL API作为适用于所有商业相关数据的官方Commerce API。 因此，AEM使用GraphQL通过I/O运行时与Adobe Commerce和任何商业引擎交换商业数据。 此GraphQL API独立于AEM GraphQL API，可用于访问内容片段。

## 2.能否通过Adobe Commerce管理员从AEM存储和引用产品资产（图像）？ 如何使用Dynamic Media中的资源？

没有正式的AEM Assets - Adobe Commerce集成可用。 在上有合作伙伴连接器 [marketplace](https://marketplace.magento.com) <!-- THIS IS THE OLD URL THAT WAS USED. IT WAS 404 (https://marketplace.magento.com/bounteous-dam.html) -->

或者，作为解决方法，您可以在AEM Assets中存储产品资源（图像），但必须在Adobe Commerce中手动存储资源URL。 Dynamic Media现在是AEM Assets的一部分，并且以相同的方式工作。

## 3.在哪里部署商业解决方案是否重要？ （内部部署或云中）

不，将您的商务解决方案部署在何处无关紧要。 CIF和AEM店面的工作方式与部署模型无关。 但是，如果解决方案是使用推荐的E2E参考体系结构部署的，则E2E测试可以根据代表典型企业客户配置文件的性能KPI运行。 此方法提供可以用作基准的其他信息。

## 4.如何在AEM中创建目录页面或产品页面？ 它们如何在AEM中保留？

目录页面和产品页面是基于通用目录和产品页面模板在AEM中动态创建和缓存的。 AEM中不会导入和存储任何产品或目录数据。

## 5.在商务解决方案中更新产品数据时，是否实时推送到AEM？ 还是说它是一个批处理？

与AEM Cloud Service一起使用的CIF加载项使得数据能够按需从商务解决方案流入AEM。 因此，当您的商业解决方案中有更新时，这不是实时推送或批处理。

## 6. AEM支持CIF的目录大小是多少？

这取决于您必须考虑的其他几个方面。 您的目录数据和页面的缓存比率是多少？ 您预计在高峰时段有多少并发请求？ 您的商业解决方案的API可扩展性如何？

## 7. PIM如何在这个框架中发挥作用？

PIM数据通过GraphQL请求向AEM和客户端公开。 我们的建议是将PIM与商务引擎(Adobe Commerce或其他)集成，以便随后可以从商务引擎检索PIM数据。

## 8.您是否还通过Dispatcher缓存定价和其他数据？ 这是否会带来频繁的缓存失效挑战？

Dispatcher上不会缓存价格或库存等动态数据。 使用Web组件直接通过GraphQL API在客户端获取动态数据。 Dispatcher上仅缓存静态数据（如产品或类别数据）。 如果产品数据发生更改，则需要使缓存失效。

## 9. AEM Dispatcher的缓存失效如何与AEM和commerce一起使用？

Adobe建议为Dispatcher上缓存的页面设置基于TTL的缓存失效。 对于价格或库存等动态信息，Adobe建议在客户端渲染数据。 有关基于TTL的缓存失效的详细信息，请参见 [优化Dispatcher缓存](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17458.html) 和 [AEM性能优化](https://experienceleague.adobe.com/docs/commerce-operations/deliver-commerce-at-scale/performance.html).

## 10.是否有任何关于使用Commerce跨AEM内容进行统一搜索的建议？

提供了产品搜索引用实施，但未提供包含内容的统一搜索。 此功能特定于客户，并且可在特定于项目的级别上更好地解决。

## 11. Search如何与使用CIF的AEM和Commerce一起使用？

CIF提供搜索栏和搜索结果组件。 搜索栏组件将带有搜索词的GraphQL请求发送到商业解决方案，然后该解决方案返回包含产品名称、价格、概要(SLUG)等的产品列表。 然后，搜索结果组件将在AEM中创建的搜索结果页上的库视图中显示搜索结果。 “搜索”支持基本的全文搜索。 我们使用SLUG/url键构建对PDP的引用。

## 12.如何在MSM或翻译中使用产品数据？

产品数据已在PIM或Adobe Commerce中转换。 AEM - Adobe Commerce集成支持与多个Adobe Commerce商店和商店视图的连接。 在MSM设置中，通常一个AEM站点链接到一个Adobe Commerce商店视图。

## 13.有没有办法用商业文本加强产品数据？ 你在哪里做这件事？ 在AEM中还是在商业解决方案中？

Adobe建议在AEM中管理与营销相关的数据和内容。 使用内容片段使用其他属性修饰商业解决方案中的产品数据，或者为非结构化内容创建体验片段并将其链接到您的产品。

## 14.在整个表示层使用AEM时，如何确保PCI合规性？

Adobe建议使用抽象的支付方式。 这使得浏览器客户端与支付网关提供商直接通信，因此Adobe或商业解决方案都不会保留或传递持卡人数据。 此方法只需要第3级PCI符合性。 但是，还需要考虑其他完全符合PCI标准的因素，例如员工如何与系统和数据交互。 有关Adobe Commerce PCI合规性的更多信息，请参见 [PCI合规性要求](https://business.adobe.com/products/magento/pci-compliance.html).

## 15.如果我使用AEM和Adobe Commerce云版本，则此联合解决方案是否符合PCI标准？

是的，可应要求提供自我评估问卷D和合规证明。

## 16.如何申请I/O运行时试用许可证？

您可以请求试用许可证以使用I/O运行时 [此处](https://developer.adobe.com/app-builder/trial/).
