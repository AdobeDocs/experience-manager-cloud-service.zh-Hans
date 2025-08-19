---
title: AEM - 使用 Commerce Integration Framework 的商业集成常见问题解答
description: AEM - 使用 Commerce Integration Framework 的商业集成常见问题解答
exl-id: 0a946d98-22c7-445d-984a-9e09c306ce45
feature: Commerce Integration Framework
role: Admin, Architect, User
source-git-commit: 80bd8da1531e009509e29e2433a7cbc8dfe58e60
workflow-type: tm+mt
source-wordcount: '960'
ht-degree: 97%

---


# AEM - 使用 Commerce Integration Framework 的商业集成常见问题解答

## &#x200B;1. CIF GraphQL 仅用于商业还是可用于查询在 AEM JCR 上创作的内容？ {#faq-1}

Adobe 已采用 Adobe Commerce 的 GraphQL API 作为其所有与商业相关的数据的官方商业 API。因此，AEM 使用 GraphQL 与 Adobe Commerce 交换商业数据，并通过 I/O Runtime 与任何商业引擎交换商业数据。此 GraphQL API 独立于 AEM 的 GraphQL API 来访问内容片段。

## &#x200B;2. 产品资源（图像）是否可以通过 Adobe Commerce 管理员从 AEM 存储和引用？如何使用 Dynamic Media 中的资源？ {#faq-2}

没有可用的官方 AEM Assets - Adobe Commerce 集成。[marketplace上有可用的合作伙伴连接器。](https://commercemarketplace.adobe.com)

或者，作为解决方法，您可以将产品资源（图像）存储在 AEM Assets 中，但必须手动将资源 URL 存储在 Adobe Commerce 中。Dynamic Media 现在是 AEM Assets 的一部分，并且工作原理相同。

## &#x200B;3. 商业解决方案部署在哪里重要吗？（本地或在云中） {#faq-3}

不重要，您的商业解决方案部署在哪里并不重要。CIF 和 AEM 店面的工作方式与部署模型无关。但是，如果使用推荐的 E2E 参考架构部署解决方案，则可以针对代表典型企业客户配置文件的性能 KPI 运行 E2E 测试。此方法提供了可用作基准的附加信息。

## &#x200B;4. 如何在 AEM 中创建目录页面或产品页面？它们如何在 AEM 中持久存在？ {#faq-4}

目录页面和产品页面是根据通用目录和产品页面模板在 AEM 中动态创建和缓存的。AEM 中不会导入和存储产品或目录数据。

## &#x200B;5. 当您在商业解决方案中更新产品数据时，这会实时推送到 AEM 吗？或者它是一个批处理过程吗？ {#faq-5}

与 AEM Cloud Service 结合使用的 CIF 插件使数据能够按需从商务解决方案流向 AEM。因此，当您的商务解决方案存在更新时，这不是实时推送或批处理过程。

## &#x200B;6. 带有 CIF 的 AEM 支持多大的目录大小？ {#faq-6}

这取决于您必须考虑的一些其他方面。您的目录数据和页面的缓存比率是多少？您预计高峰时段会有多少并发请求？您的商业解决方案的 API 的可扩展性如何？

## &#x200B;7. PIM 如何在该框架中发挥作用？ {#faq-7}

PIM 数据通过 GraphQL 请求向 AEM 和客户端公开。我们的建议是将 PIM 与商业引擎（Adobe Commerce 或其他）集成，以便可以从商业引擎检索 PIM 数据。

## &#x200B;8. 您是否还会通过 Dispatcher 缓存定价和其他数据？这是否会引发频繁的缓存失效问题？ {#faq-8}

价格或库存等动态数据不会缓存在 Dispatcher 上。动态数据是通过 GraphQL API 在客户端直接通过 Web 组件获取的。仅静态数据（例如产品或类别数据）会缓存在 Dispatcher 上。如果产品数据发生变化，就需要缓存失效。

## &#x200B;9. AEM Dispatcher 的缓存失效如何与 AEM 和 Commerce 配合使用？ {#faq-9}

Adobe 建议为 Dispatcher 上缓存的页面设置基于 TTL 的缓存失效。对于价格或库存等动态信息，Adobe 建议在客户端呈现数据。有关基于 TTL 的缓存失效的详细信息，请参阅[优化 Dispatcher 缓存。](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17458.html)

## &#x200B;10. 对于使用 Commerce 跨 AEM 内容进行统一搜索有什么建议吗？ {#faq-10}

提供产品搜索参考实施，但没有与内容进行统一搜索。此功能是特定于客户的，可以在特定于项目的级别上得到更好地解决。

## &#x200B;11. 搜索功能如何与 AEM 以及使用 CIF 的 Commerce 配合使用？ {#faq-11}

CIF 提供搜索栏和搜索结果组件。搜索栏组件将带有搜索词的 GraphQL 请求发送到商业解决方案，然后商业解决方案会返回包含产品名称、价格、SLUG 等的产品列表。然后，搜索结果组件会在 AEM 中创建的搜索结果页面上的图库视图中显示搜索结果。搜索功能支持基本的全文搜索。我们使用 SLUG/url 键来构建对 PDP 的引用。

## &#x200B;12. 产品数据如何用于 MSM 或翻译？ {#faq-12}

产品数据已在 PIM 或 Adobe Commerce 中进行翻译。AEM - Adobe Commerce 集成支持连接到多个 Adobe Commerce 商店和商店视图。在 MSM 设置中，通常会将一个 AEM 站点链接到一个 Adobe Commerce 商店视图。

## &#x200B;13. 有没有办法用商业文本来增强产品数据？在哪里进行该操作？在 AEM 中还是在商业解决方案中？ {#faq-13}

Adobe 建议在 AEM 中管理与营销相关的数据和内容。利用内容片段使用附加属性装饰商业解决方案中的产品数据，或者为非结构化内容创建体验片段并将其链接到您的产品。

## &#x200B;14. 在整个表示层使用 AEM 时，如何确保 PCI 合规性？ {#faq-14}

Adobe 建议使用抽象的付款方式。这会使浏览器客户端与支付网关提供商直接通信，以便 Adobe 或商业解决方案都不会保存或传递持卡人数据。此方法仅需要 3 级 PCI 合规性。但是，要完全符合 PCI 标准，还需要考虑其他事项，例如员工如何与系统和数据交互。有关Adobe Commerce PCI合规性的详细信息，请参阅[PCI合规性要求。](https://business.adobe.com/products/magento/pci-compliance.html)

## &#x200B;15. 如果我使用的是 AEM 和 Adobe Commerce 云版本，此联合解决方案是否符合 PCI 要求？ {#faq-15}

是的，可根据要求提供自我评估问卷 D 和合规证明。

## &#x200B;16. 如何申请 I/O Runtime 试用许可证？ {#faq-16}

有关申请试用许可证以使用 I/O Runtime 的详细信息，请参阅 [获取 Access](https://developer.adobe.com/runtime/docs/guides/overview/getting_access/)。
