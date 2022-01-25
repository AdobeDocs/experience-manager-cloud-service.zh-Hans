---
title: 高级URL配置
description: 了解如何自定义产品和类别页面的URL。 这允许实施优化搜索引擎的URL并促进发现。
sub-product: Commerce
version: cloud-service
doc-type: technical-video
activity: setup
audience: administrator
feature: Commerce Integration Framework
kt: 4933
thumbnail: 34350.jpg
exl-id: 314494c4-21a9-4494-9ecb-498c766cfde7,363cb465-c50a-422f-b149-b3f41c2ebc0f
source-git-commit: 8c3a1366d076c009262eeab8129e4e589dc4f7c5
workflow-type: tm+mt
source-wordcount: '2046'
ht-degree: 3%

---

# 高级URL配置 {#url}

>[!NOTE]
>
> 搜索引擎优化 (SEO) 已成为许多营销人员关注的重点。因此，需要解决众多 Adobe Experience Manager (AEM) as a Cloud Service 项目中的 SEO 问题。请阅读 [SEO和URL管理最佳实践](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/seo-and-url-management.html) 以了解其他信息。

[AEM CIF核心组件](https://github.com/adobe/aem-core-cif-components) 提供了高级配置，用于自定义产品和类别页面的URL。 许多实施都将自定义这些URL以用于搜索引擎优化(SEO)。 以下视频详细介绍了如何配置 `UrlProvider` 服务和功能 [Sling映射](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) 自定义产品和类别页面的URL。

>[!VIDEO](https://video.tv.adobe.com/v/34350/?quality=12)

## 配置 {#configuration}

配置 `UrlProvider` 服务，并且项目必须为 _CIF URL提供程序配置_.

>[!NOTE]
>
> 自AEM CIF核心组件版本2.0.0起，URL提供程序配置仅提供预定义的URL格式，而不提供1.x版本中已知的可配置自由文本的格式。 此外，使用选择器在URL中传递数据的方法已被替换为后缀。

### 产品页面URL格式 {#product}

这会配置产品页面的URL，并支持以下选项：

* `{{page}}.html/{{sku}}.html#{{variant_sku}}`（默认）
* `{{page}}.html/{{sku}}/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{sku}}/{{category}}/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{sku}}/{{url_path}}.html#{{variant_sku}}`
* `{{page}}.html/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{category}}/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{url_path}}.html#{{variant_sku}}`

对于 [Venia参考存储](https://github.com/adobe/aem-cif-guides-venia):

* `{{page}}` 将替换为 `/content/venia/us/en/products/product-page`
* `{{sku}}` 将被产品的sku(例如， `VP09`
* `{{url_key}}` 将被产品的 `url_key` 属性，例如 `lenora-crochet-shorts`
* `{{url_path}}` 将被产品的 `url_path`，例如 `venia-bottoms/venia-pants/lenora-crochet-shorts`
* `{{variant_sku}}` 将被替换为当前选定的变体，例如 `VP09-KH-S`

自 `url_path` 已弃用，预定义的产品URL格式使用 `url_rewrites` 并选择路径段最多的路径段，如果 `url_path` 不可用。

对于上述示例数据，使用默认URL格式设置的产品变体URL将如下所示 `/content/venia/us/en/products/product-page.html/VP09.html#VP09-KH-S`.

### 类别页面URL格式 {#product-list}

这会配置类别或产品列表页面的URL，并支持以下选项：

* `{{page}}.html/{{url_path}}.html`（默认）
* `{{page}}.html/{{url_key}}.html`

对于 [Venia参考存储](https://github.com/adobe/aem-cif-guides-venia):

* `{{page}}` 将替换为 `/content/venia/us/en/products/category-page`
* `{{url_key}}` 将被类别的 `url_key` 属性
* `{{url_path}}` 将被类别的 `url_path`

根据上述示例数据，使用默认URL格式设置的类别页面URL将如下所示 `/content/venia/us/en/products/category-page.html/venia-bottoms/venia-pants.html`.

>[!NOTE]
> 
> 的 `url_path` 是 `url_keys` 产品或类别的祖先和产品或类别的 `url_key` 分隔 `/` 斜线。 每个 `url_key` 在给定的商店中被视为唯一的。

### 存储特定配置 {#store-specific-urlformats}

由 _CIF URL提供程序配置_ 可针对每个商店进行更改。

在CIF配置中，编辑器可以选择替代产品或类别页面URL格式。 如果未选择任何内容，则实施将回退到系统范围的配置。

更改实时网站的URL格式可能会对网站的自然流量产生负面影响。 请参阅 [最佳实践](#best-practices) 并事先仔细规划URL格式的更改。

![CIF配置中的URL格式](assets/store-specific-url-formats.png)

>[!NOTE]
>
> URL格式的存储特定配置需要 [CIF核心组件2.6.0](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.6.0) 和最新版本的Adobe Experience Manager Content and Commerce加载项。

## 类别感知产品URL {#context-aware-pdps}

由于可以对产品URL中的类别信息进行编码，因此属于多个类别的产品也可能会使用多个产品URL进行编码。

在默认配置中，默认URL格式将使用以下方案选择一个可能的替代方案：

* 如果 `url_path` 由电子商务后端使用它来定义（已弃用）
* 从 `url_rewrites` 使用以产品 `url_key` 作为替代项
* 形成这些替代方案时，会使用路径区段最多的替代方案
* 如果有多个，请按照电子商务后端提供的顺序获取第一个

此方案将选择 `url_path` 具有最先辈的子代，基于子代类别比其父代类别更具体的假设。 选定的 `url_path` 被视为 _正则_ 和将始终用于产品页面或产品站点地图中的规范链接。

但是，当购物者从类别页面导航到产品页面，或从一个产品页面导航到同一类别中的其他相关产品页面时，应保留当前类别上下文。 在本例中， `url_path` 与当前类别上下文相比，所选内容应更偏向于替代内容 _正则_ 上述选择。

此功能必须在 _CIF URL提供程序配置_. 如果启用，则在

* 它们与给定类别的部分匹配 `url_paths` 从开头（模糊前缀匹配）
* 或与给定类别匹配 `url_key` 任意位置（精确的部分匹配）

例如，请考虑 [产品查询](https://devdocs.magento.com/guides/v2.4/graphql/queries/products.html) 下。 如果用户位于“2022年夏季推出的新产品/新产品”类别页面上，且商店使用的是默认类别页面URL格式，则替代的“new-products/new-in-summer-2022/gold-cirque-earrings.html”将匹配上下文从头开始的2个路径区段：“新产品”和“2022年夏季新产品”。 如果存储使用的类别页面URL格式仅包含 `url_key`，则仍将选择相同的替代方法，因为它与上下文的 `url_key` 任何地方。 在这两种情况下，都将为“new-products/new-in-summer-2022/gold-cirque-earrings.html”创建产品页面URL `url_path`.

```
{
  "data": {
    "products": {
      "items": [
        {
          "sku": "VA18-GO-NA",
          "url_key": "gold-cirque-earrings",
          "url_rewrites": [
            {
              "url": "gold-cirque-earrings.html"
            },
            {
              "url": "venia-accessories/gold-cirque-earrings.html"
            },
            {
              "url": "venia-accessories/venia-jewelry/gold-cirque-earrings.html"
            },
            {
              "url": "new-products/gold-cirque-earrings.html"
            },
            {
              "url": "new-products/new-in-summer-2022/gold-cirque-earrings.html"
            }
          ]
        }
      ]
    }
  }
}
```

>[!NOTE]
>
> 类别感知产品URL需要 [CIF核心组件2.6.0](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.6.0) 或更新版本。

## 特定类别和产品页面 {#specific-pages}

可以创建 [多类别和产品页面](../authoring/multi-template-usage.md) 仅适用于目录类别或产品的特定子集。

### 选择标准 {#specific-pages-selection}

根据类别的 `url_path` 或 `url_key`. 仅包含完整类别的URL格式支持匹配子类别 `url_path`. 否则，仅与 `url_key` 是可能的。

特定的产品页面按产品的SKU或类别进行选择。 后者要求在产品URL中对某些类别信息进行编码。 此设置仅适用于某些默认URL格式。 有关URL格式支持按SKU或类别进行特定页面选择的比较，请参阅下表。


| URL格式 | 按sku | 按类别 |
| ----------------------------------------------------- | ------ | ---------------- |
| `{{page}}.html/{{url_key}}.html` | 否 | 否 |
| `{{page}}.html/{{category}}/{{url_key}}.html` | 否 | 仅精确匹配 |
| `{{page}}.html/{{url_path}}.html` | 否 | 是 |
| `{{page}}.html/{{sku}}.html` | 是 | 否 |
| `{{page}}.html/{{sku}}/{{url_key}}.html` | 是 | 否 |
| `{{page}}.html/{{sku}}/{{category}}/{{url_key}}.html` | 是 | 仅精确匹配 |
| `{{page}}.html/{{sku}}/{{url_path}}.html` | 是 | 是 |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
> 需要按类别选择特定产品页面 [CIF核心组件2.6.0](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.6.0) 或更新版本。

### 深层链接 {#specific-pages-deep-linking}

的 `UrlProvider` 已预配置为生成指向创作层实例中特定类别和产品页面的深层链接。 对于使用“预览”模式浏览网站、导航到特定产品或类别页面并切换回“编辑”模式以编辑页面的编辑器而言，此操作非常有用。

另一方面，在发布层实例上，目录页面URL应保持稳定，以免在搜索引擎排名上丢失增益。 由于该发布层实例默认不会呈现指向特定目录页面的深层链接。 要更改此行为，请 _CIF URL提供商特定的页面策略_ 可以配置为始终生成特定的页面URL。

## 自定义 {#customization}

### 自定义URL格式 {#custom-url-format}

要提供自定义URL格式，项目可以在 [`ProductUrlFormat`](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/urls/ProductUrlFormat.html) 或 [`CategoryUrlFormat`](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/urls/CategoryUrlFormat.html) 服务接口，并将实现注册为OSGI服务。 这些实施（如果可用）将替换已配置的预定义格式。 如果注册了多个实施，则具有较高服务排名的实施将替换具有较低服务排名的实施。

自定义URL格式实施必须实施一对方法，以根据给定参数构建URL，并解析URL以分别返回相同的参数。

### 与Sling映射结合使用 {#sling-mapping}

除 `UrlProvider`，则还可以配置 [Sling映射](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) 以便重写和处理URL。 AEM Archetype项目还提供 [示例配置](https://github.com/adobe/aem-cif-project-archetype/tree/master/src/main/archetype/samplecontent/src/main/content/jcr_root/etc/map.publish) 为端口4503（发布）和80（调度程序）配置一些Sling映射。

### 与AEM Dispatcher结合使用 {#dispatcher}

还可以通过将AEM Dispatcher HTTP服务器与 `mod_rewrite` 模块。 的 [AEM项目原型](https://github.com/adobe/aem-project-archetype) 提供引用AEM Dispatcher配置，该配置已包含基本 [重写规则](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/dispatcher.cloud) 的值。

## 最佳实践 {#best-practices}

### 选择最佳URL格式 {#choose-url-format}

正如在选择一种可用的默认格式之前所述，甚至实施自定义格式，都高度取决于存储的需求和要求。 以下建议可能有助于作出有根据的决策。

_**使用包含SKU的产品页面URL格式。**_

CIF核心组件会将SKU用作所有组件中的主要标识符。 如果产品页面URL格式不包含SKU，则需要使用GraphQL查询才能从 `url_key`，这可能会影响到时间到第一字节量度。 此外，购物者可能希望在搜索引擎中按SKU查找产品。

_**使用包含类别上下文的产品页面URL格式。**_

CIF URL提供程序的某些功能仅在使用对类别上下文（如类别）进行编码的产品URL格式时可用 `url_key` 或类别 `url_path`. 即使新存储可能不需要这些功能，但在开头使用其中一种URL格式有助于减少将来的迁移工作。

_**在URL长度和编码信息之间实现平衡。**_

根据目录大小，特别是类别树的大小和深度，可能不合理对全部进行编码 `url_path` 类别。 在这种情况下，可以通过包含类别的 `url_key` 中。 这将启用使用类别时几乎所有可用的功能 `url_path`.

此外，请使用 [Sling映射](#sling-mapping) 以便将sku与产品结合 `url_key`. 在大多数电子商务系统中，SKU遵循特定格式，并将SKU与 `url_key` 对于传入的请求，应该可能。 考虑到这一点，可以将产品页面URL重写为 `/p/{{category}}/{{sku}}-{{url_key}}.html`，以及 `/c/{{url_key}}.html` 相应地。 的 `/p` 和 `/c` 为了将产品和类别页面与其他内容页面区分开，仍需要使用前缀。

### 从一种URL格式迁移到另一种URL格式 {#migrate-url-formats}

许多默认URL格式之间以某种方式相互兼容，这意味着由一个URL格式映射的URL可能会被另一个URL格式解析。 这有助于在URL格式之间迁移。

另一方面，搜索引擎将需要一些时间来使用新的URL格式重新爬网所有目录页面。 为支持此过程并改善最终用户体验，建议提供重定向，以将用户从旧URL转发到新URL。

一种方法是，将暂存环境连接到生产电子商务后端，并将其配置为使用新的URL格式。 之后获取 [由CIF产品站点地图生成器生成的产品站点地图](../../overview/seo-and-url-management.md) 对于暂存环境和生产环境，并使用它们创建 [Apache httpd rewrite map](https://httpd.apache.org/docs/2.4/rewrite/rewritemap.html). 无法将此重写映射与新URL格式的转出一起部署到调度程序。

## 示例 {#example}

的 [Venia参考存储](https://github.com/adobe/aem-cif-guides-venia) 项目包含用于演示产品和类别页面使用自定义URL的示例配置。 这允许每个项目根据其SEO需求为产品和类别页面设置单个URL模式。 CIF的组合 `UrlProvider` 和Sling映射（如上所述）。

>[!NOTE]
>
>此配置必须使用项目使用的外部域进行调整。 Sling映射基于主机名和域运行。 因此，此配置默认处于禁用状态，且必须在部署之前启用。 为此，请重命名Sling映射 `hostname.adobeaemcloud.com` 文件夹 `ui.content/src/main/content/jcr_root/etc/map.publish/https` 根据使用的域名，并通过添加 `resource.resolver.map.location="/etc/map.publish"` 到 `JcrResourceResolver` 项目的配置。

## 其他资源 {#additional}

* [Venia参考存储](https://github.com/adobe/aem-cif-guides-venia)
* [AEM资源映射](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/resource-mapping.html)
* [Sling映射](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)
