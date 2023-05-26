---
title: 高级URL配置
description: 了解如何自定义产品和类别页面的URL。 这允许实施优化搜索引擎的URL并促进发现。
sub-product: Commerce
version: Cloud Service
doc-type: technical-video
activity: setup
audience: administrator
feature: Commerce Integration Framework
kt: 4933
thumbnail: 34350.jpg
exl-id: 314494c4-21a9-4494-9ecb-498c766cfde7,363cb465-c50a-422f-b149-b3f41c2ebc0f
source-git-commit: 9c25d9991b41a5a714df3f07e84946162e5495c0
workflow-type: tm+mt
source-wordcount: '2211'
ht-degree: 4%

---

# 高级URL配置 {#url}

>[!NOTE]
>
> 搜索引擎优化 (SEO) 已成为许多营销人员关注的重点。因此，需要解决众多 Adobe Experience Manager (AEM) as a Cloud Service 项目中的 SEO 问题。请阅读 [seo和URL管理最佳实践](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/seo-and-url-management.html) 以获取其他信息。

[AEM CIF核心组件](https://github.com/adobe/aem-core-cif-components) 提供高级配置以自定义产品和类别页面的URL。 许多实施将自定义这些URL以实现搜索引擎优化(SEO)。 以下视频详细介绍如何配置 `UrlProvider` 的服务和功能 [Sling映射](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) 自定义产品和类别页面的URL。

>[!VIDEO](https://video.tv.adobe.com/v/34350/?quality=12)

## 配置 {#configuration}

要配置 `UrlProvider` 服务根据SEO要求和需求，项目必须提供 _CIF URL提供程序配置_.

>[!NOTE]
>
> 自AEM CIF核心组件2.0.0版以来，“URL提供程序”配置仅提供预定义的URL格式，而不提供1.x版中已知的自由文本可配置格式。 此外，使用选择器在URL中传递数据的方法已替换为后缀。

### 产品页面URL格式 {#product}

这会配置产品页面的URL，并支持以下选项：

* `{{page}}.html/{{sku}}.html#{{variant_sku}}`（默认）
* `{{page}}.html/{{sku}}/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{sku}}/{{category}}/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{sku}}/{{url_path}}.html#{{variant_sku}}`
* `{{page}}.html/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{category}}/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{url_path}}.html#{{variant_sku}}`

对于 [Venia引用存储](https://github.com/adobe/aem-cif-guides-venia)：

* `{{page}}` 将替换为 `/content/venia/us/en/products/product-page`
* `{{sku}}` 将被产品的SKU替换，例如， `VP09`
* `{{url_key}}` 将由产品的 `url_key` 属性，例如， `lenora-crochet-shorts`
* `{{url_path}}` 将由产品的 `url_path`例如， `venia-bottoms/venia-pants/lenora-crochet-shorts`
* `{{variant_sku}}` 将被当前选定的变体替换，例如， `VP09-KH-S`

由于 `url_path` 已弃用，预定义的产品URL格式使用产品的 `url_rewrites` 并选取路径分段数最多的路径作为替代路径，如果 `url_path` 不可用。

对于上述示例数据，使用默认URL格式的产品变体URL将如下所示 `/content/venia/us/en/products/product-page.html/VP09.html#VP09-KH-S`.

### 类别页面URL格式 {#product-list}

这将配置类别或产品列表页面的URL，并支持以下选项：

* `{{page}}.html/{{url_path}}.html`（默认）
* `{{page}}.html/{{url_key}}.html`

对于 [Venia引用存储](https://github.com/adobe/aem-cif-guides-venia)：

* `{{page}}` 将替换为 `/content/venia/us/en/products/category-page`
* `{{url_key}}` 将被类别的 `url_key` 属性
* `{{url_path}}` 将被类别的 `url_path`

对于上述示例数据，使用默认URL格式设置的类别页面URL如下所示 `/content/venia/us/en/products/category-page.html/venia-bottoms/venia-pants.html`.

>[!NOTE]
> 
> 此 `url_path` 是以下项的连接： `url_keys` 产品或类别的祖先以及产品或类别的 `url_key` 分隔方式 `/` slash。 每个 `url_key` 在给定存储中被视为唯一。

### 存储特定配置 {#store-specific-urlformats}

由设置的系统范围的类别和产品页面URL格式 _CIF URL提供程序配置_ 可以针对每个商店进行更改。

在CIF配置中，编辑者可以选择替代产品或类别页面URL格式。 如果未选择任何内容，则实施将回退到系统范围配置。

更改实时网站的URL格式可能会对网站的自然流量产生负面影响。 请参阅 [最佳实践](#best-practices) ，并提前仔细规划URL格式的更改。

![CIF配置中的URL格式](assets/store-specific-url-formats.png)

>[!NOTE]
>
> 存储特定的URL格式配置需要 [CIF核心组件2.6.0](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.6.0) 以及最新版本的Adobe Experience Manager Content and Commerce加载项。

## 类别感知产品页面URL {#context-aware-pdps}

由于可以对产品URL中的类别信息进行编码，因此也可以使用多个产品URL来寻址多个类别中的产品。

默认URL格式将使用以下方案选择一种可能的替代方案：

* 如果 `url_path` 由电子商务后端使用它来定义（已弃用）
* 从 `url_rewrites` 使用以产品的 `url_key` 作为替代项
* ，则这些替代项会使用具有最多路径区段的替代项
* 如果存在多个，则按照电子商务后端给定的顺序获取第一个

此方案将选择 `url_path` 具有最多祖先，基于子类别比父类别更具体的假设。 如此选择的 `url_path` 已考虑 _规范_ 和将始终用作产品页面或产品站点地图中的规范链接。

但是，当购物者从类别页面导航到产品页面，或从某个产品页面导航到同一类别中的另一个相关产品页面时，有必要保留当前类别上下文。 在本例中， `url_path` 选择应优先选择位于当前类别上下文中的替代项，而不是 _规范_ 选项（如上所述）。

必须在中启用此功能 _CIF URL提供程序配置_. 如果启用，则当满足以下条件时，该选择将提高备选项的分数

* 它们匹配给定类别的 `url_path` 从开头（模糊前缀匹配）
* 或者它们与给定类别的 `url_key` 任意位置（精确部分匹配）

例如，考虑对的响应 [产品查询](https://devdocs.magento.com/guides/v2.4/graphql/queries/products.html) 下面的。 假定用户在“New Products / New in Summer 2022”类别页面上，并且商店使用默认类别页面URL格式，则替代“new-products/new-in-summer-2022/gold-cirque-earrings.html”将从头匹配上下文路径区段中的2个：“new-products”和“new-in-summer-2022”。 如果商店使用的类别页面URL格式仅包含类别，则 `url_key`，仍会选择相同的替代项，因为它与上下文的 `url_key` 任何地方。 在这两种情况下，都会为“new-products/new-in-summer-2022/gold-cirque-earrings.html”创建产品页面URL `url_path`.

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
> 类别识别产品URL需要 [CIF核心组件2.6.0](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.6.0) 或更新版本。

## 特定类别和产品页面 {#specific-pages}

可以创建 [多个类别和产品页面](../authoring/multi-template-usage.md) 仅用于特定类别子集或目录产品。

### 选择标准 {#specific-pages-selection}

根据类别的 `url_path` 或 `url_key`. 仅包含完整类别的URL格式支持匹配子类别 `url_path`. 否则，只有完全匹配的 `url_key` 是可能的。

特定产品页面可按产品的SKU或类别进行选择。 后者要求在产品URL中对某些类别信息进行编码。 这仅适用于某些默认URL格式。 请参阅下表，比较哪种URL格式支持按SKU或类别选择特定的页面。


| URL格式 | 按sku | 按类别 |
| ----------------------------------------------------- | ------ | ---------------- |
| `{{page}}.html/{{url_key}}.html` | 否 | 否 |
| `{{page}}.html/{{category}}/{{url_key}}.html` | 否 | 仅完全匹配 |
| `{{page}}.html/{{url_path}}.html` | 否 | 是 |
| `{{page}}.html/{{sku}}.html` | 是 | 否 |
| `{{page}}.html/{{sku}}/{{url_key}}.html` | 是 | 否 |
| `{{page}}.html/{{sku}}/{{category}}/{{url_key}}.html` | 是 | 仅完全匹配 |
| `{{page}}.html/{{sku}}/{{url_path}}.html` | 是 | 是 |

{style="table-layout:auto"}

>[!NOTE]
>
> 需要按类别选择特定产品页面 [CIF核心组件2.6.0](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.6.0) 或更新版本。

### 深度链接 {#specific-pages-deep-linking}

此 `UrlProvider` 已预配置为在创作层实例上生成指向特定类别和产品页面的深层链接。 这对于编辑器非常有用，编辑器使用预览模式浏览网站，导航到特定产品或类别页面，然后切换回编辑模式以编辑页面。

另一方面，在发布层实例上，目录页面URL应保持稳定，以免失去搜索引擎排名等优势。 因此，默认情况下，发布层实例不会呈现指向特定目录页面的深层链接。 要更改此行为，请 _特定于CIF URL提供程序的页面策略_ 可以配置为始终生成特定的页面URL。

### 多个目录页面 {#multiple-product-pages}

当编辑器希望完全控制站点的顶级导航时，可能不需要使用单个目录页面呈现目录的顶级类别。 相反，编辑者可以创建多个目录页面，每个目录页面对应一个要包含在顶级导航中的目录类别。

对于该用例，每个目录页面都可以具有对特定于为目录页面配置的类别的产品和类别页面的引用。 此 `UrlProvider` 将使用这些链接为配置的类别中的页面和类别创建链接。 但是，出于性能原因，只考虑站点导航根/登陆页面的直接目录页面子项。

建议目录页面的产品和类别页面成为该目录页面的子项，否则导航或痕迹导航等组件可能无法正常工作。

>[!NOTE]
>
> 要全面支持多个目录页面，需要 [CIF核心组件2.10.0](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.10.0) 或更新版本。

## 自定义 {#customization}

### 自定义URL格式 {#custom-url-format}

要提供自定义URL格式，项目可以实施 [`ProductUrlFormat`](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/urls/ProductUrlFormat.html) 或 [`CategoryUrlFormat`](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/urls/CategoryUrlFormat.html) 服务接口，并将实现注册为OSGI服务。 这些实施（如果可用）将替换已配置的预定义格式。 如果注册了多个实施，则服务排名较高的实施将替换服务排名较低的实施。

自定义URL格式实施必须实施一对方法，以便从给定参数构建URL，并解析URL以分别返回相同的参数。

### 与Sling映射组合 {#sling-mapping}

除了 `UrlProvider`，也可以配置 [Sling映射](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) 以重写和处理URL。 AEM原型项目还提供 [示例配置](https://github.com/adobe/aem-cif-project-archetype/tree/master/src/main/archetype/samplecontent/src/main/content/jcr_root/etc/map.publish) 为端口4503（发布）和80（调度程序）配置一些Sling映射。

### 与AEM调度程序相结合 {#dispatcher}

通过将AEM Dispatcher HTTP服务器与结合使用，还可以实现URL重写 `mod_rewrite` 模块。 此 [AEM项目原型](https://github.com/adobe/aem-project-archetype) 提供了参考AEM Dispatcher配置，其中已包含基本 [重写规则](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/dispatcher.cloud) 生成的大小。

## 最佳实践 {#best-practices}

### 选择最佳的URL格式 {#choose-url-format}

如在选择一种可用的默认格式，甚至实施自定义格式之前所述，这在很大程度上取决于存储的需求和要求。 以下建议可能有助于做出有根据的决定。

_**使用包含SKU的产品页面URL格式。**_

CIF核心组件使用sku作为所有组件中的主要标识符。 如果产品页面URL格式不包含SKU，则需要使用GraphQL查询来解析它。 这可能会影响第一字节的时间。 此外，可能希望购物者能够通过使用搜索引擎通过SKU找到产品。

_**使用包含类别上下文的产品页面URL格式。**_

CIF URL提供程序的某些功能仅在使用产品URL格式时可用，这些格式对类别上下文（如类别）进行编码 `url_key` 或类别 `url_path`. 即使新存储可能不需要这些功能，在开始时使用这些URL格式之一有助于减少未来的迁移工作。

_**URL长度和编码信息之间的平衡。**_

根据目录大小，特别是类别树的大小和深度，对完整目录进行编码可能不太合理 `url_path` 类别到URL中。 在这种情况下，可以通过仅包含类别的 `url_key` 而是。 这将支持使用类别时可用的大多数功能 `url_path`.

此外，利用 [Sling映射](#sling-mapping) 以将sku与产品相结合 `url_key`. 在大多数电子商务系统中，SKU遵循特定的格式，并将SKU与 `url_key` 对于传入请求，应该很容易实现。 考虑到这一点，应该可以将产品页面URL重写到 `/p/{{category}}/{{sku}}-{{url_key}}.html`，类别URL为 `/c/{{url_key}}.html` 分别地。 此 `/p` 和 `/c` 要将产品和类别页面与其他内容页面区分开来，仍然需要使用前缀。

### 迁移到新URL格式 {#migrate-url-formats}

许多默认URL格式以某种方式相互兼容，这意味着由一种格式设置的URL可能由另一种格式解析。 这有助于在URL格式之间迁移。

另一方面，搜索引擎将需要一些时间来使用新的URL格式重新爬网所有目录页面。 为了支持此过程并改善最终用户体验，建议提供可将用户从旧URL转发到新URL的重定向。

其中一种方法是将暂存环境连接到生产电子商务后端，并将其配置为使用新的URL格式。 然后，获取 [CIF产品Sitemap生成器生成的产品Sitemap](../../overview/seo-and-url-management.md) 用于暂存和生产环境，并使用它们创建 [Apache httpd重写映射](https://httpd.apache.org/docs/2.4/rewrite/rewritemap.html). 此重写映射可以与新URL格式的推出一起部署到Dispatcher。

## 示例 {#example}

此 [Venia引用存储](https://github.com/adobe/aem-cif-guides-venia) project包含示例配置，用于演示自定义URL在产品和类别页面中的用法。 这样，每个项目就可以根据其SEO需求，为产品和类别页面设置单独的URL模式。 CIF组合 `UrlProvider` 和如上所述的Sling映射一起使用。

>[!NOTE]
>
>必须使用该项目使用的外部域调整此配置。 Sling映射基于主机名和域工作。 因此，此配置在默认情况下处于禁用状态，必须在部署之前启用。 为此，请重命名Sling映射 `hostname.adobeaemcloud.com` 文件夹位置 `ui.content/src/main/content/jcr_root/etc/map.publish/https` 根据使用的域名，并通过添加以下内容启用此配置 `resource.resolver.map.location="/etc/map.publish"` 到 `JcrResourceResolver` 项目的配置。

## 其他资源 {#additional}

* [Venia引用存储](https://github.com/adobe/aem-cif-guides-venia)
* [AEM资源映射](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/resource-mapping.html)
* [Sling映射](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)
