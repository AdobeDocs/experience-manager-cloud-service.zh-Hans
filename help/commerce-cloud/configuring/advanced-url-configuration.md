---
title: 高级URL配置
description: 了解如何自定义产品和类别页面的URL。 自定义允许实施优化搜索引擎的URL并促进发现。
sub-product: Commerce
version: Cloud Service
doc-type: technical-video
activity: setup
audience: administrator
feature: Commerce Integration Framework
kt: 4933
thumbnail: 34350.jpg
exl-id: 314494c4-21a9-4494-9ecb-498c766cfde7
role: Admin
source-git-commit: 0e328d013f3c5b9b965010e4e410b6fda2de042e
workflow-type: tm+mt
source-wordcount: '2059'
ht-degree: 2%

---

# 高级URL配置 {#url}

>[!NOTE]
>
> 搜索引擎优化 (SEO) 已成为许多营销人员关注的重点。因此，必须在Adobe Experience Manager (AEM)as a Cloud Service的许多项目中解决SEO问题。 请参阅[SEO和URL管理最佳实践](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/seo-and-url-management.html)以了解更多信息。

[AEM CIF核心组件](https://github.com/adobe/aem-core-cif-components)提供了高级配置以自定义产品和类别页面的URL。 许多实施都会自定义这些URL，以实现搜索引擎优化(SEO)。 以下视频详细介绍如何配置[Sling映射](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)的`UrlProvider`服务和功能以自定义产品和类别页面的URL。

>[!VIDEO](https://video.tv.adobe.com/v/34350/?quality=12)

## 配置 {#configuration}

要根据SEO要求和需求配置`UrlProvider`服务，项目必须提供&#x200B;_CIF URL提供程序配置_&#x200B;的OSGI配置。

>[!NOTE]
>
> 自AEM CIF核心组件版本2.0.0开始，URL提供程序配置仅提供预定义的URL格式，而不提供1.x版本中已知的自由文本可配置格式。 此外，使用选择器在URL中传递数据的方法已替换为后缀。

### 产品页面URL格式 {#product}

配置产品页面的URL并支持以下选项：

* `{{page}}.html/{{sku}}.html#{{variant_sku}}`（默认）
* `{{page}}.html/{{sku}}/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{sku}}/{{category}}/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{sku}}/{{url_path}}.html#{{variant_sku}}`
* `{{page}}.html/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{category}}/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{url_path}}.html#{{variant_sku}}`

如果存在[Venia引用存储](https://github.com/adobe/aem-cif-guides-venia)：

* `{{page}}`已替换为`/content/venia/us/en/products/product-page`
* `{{sku}}`被产品的SKU替换，例如，`VP09`
* `{{url_key}}`被产品的`url_key`属性替换，例如`lenora-crochet-shorts`
* `{{url_path}}`被产品的`url_path`替换，例如`venia-bottoms/venia-pants/lenora-crochet-shorts`
* `{{variant_sku}}`被当前选定的变体替换，例如`VP09-KH-S`

由于`url_path`已被弃用，因此预定义产品URL格式将使用产品的`url_rewrites`，并在`url_path`不可用时选择具有最多路径区段的格式作为替代格式。

对于上述示例数据，使用默认URL格式的产品变体URL类似于`/content/venia/us/en/products/product-page.html/VP09.html#VP09-KH-S`。

### 类别页面URL格式 {#product-list}

配置类别或产品列表页面的URL，并支持以下选项：

* `{{page}}.html/{{url_path}}.html`（默认）
* `{{page}}.html/{{url_key}}.html`

如果存在[Venia引用存储](https://github.com/adobe/aem-cif-guides-venia)：

* `{{page}}`已替换为`/content/venia/us/en/products/category-page`
* `{{url_key}}`被类别的`url_key`属性替换
* `{{url_path}}`被类别的`url_path`替换

对于上述示例数据，使用默认URL格式设置的类别页面URL类似于`/content/venia/us/en/products/category-page.html/venia-bottoms/venia-pants.html`。

>[!NOTE]
> 
> `url_path`是产品或类别祖先的`url_keys`与产品或类别的`url_key`的串联，由`/`斜杠分隔。 每个`url_key`在给定存储中均被视为唯一。

### 特定于存储的配置 {#store-specific-urlformats}

可以更改每个商店的&#x200B;_CIF URL提供程序配置_&#x200B;设置的系统范围类别和产品页面URL格式。

在CIF配置中，编辑器可以选择替代产品或类别页面URL格式。 如果未在该处选择任何内容，则实施将回退到系统范围配置。

更改实时网站的URL格式可能会对网站的自然流量产生负面影响。 请参阅下面的[最佳实践](#best-practices)，并提前仔细规划更改URL格式。

CIF配置中的![URL格式](assets/store-specific-url-formats.png)

>[!NOTE]
>
> URL格式的特定于商店的配置需要[CIF核心组件2.6.0](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.6.0)以及最新版本的Adobe Experience Manager Content和Commerce加载项。

## 类别感知产品页面URL {#context-aware-pdps}

由于可以在产品URL中编码类别信息，因此也可以使用多个产品URL寻址多个类别中的产品。

默认URL格式使用以下方案选择可能的替代方案之一：

* 如果`url_path`由电子商务后端定义，则使用它（已弃用）
* 从`url_rewrites`，将那些以产品的`url_key`结尾的URL用作替代项
* ，则这些替代项会使用具有最多路径区段的替代项
* 如果存在多个，则按照电子商务后端提供的顺序进行排列

此方案基于子类别比其父类别更具体的假设，选择具有最多祖先的`url_path`。 选定的`url_path`被视为&#x200B;_canonical_，并始终用作产品页面或产品站点地图中的规范链接。

但是，当购物者从类别页面导航到产品页面，或从某个产品页面导航到同一类别中的另一个相关产品页面时，有必要保留当前的类别上下文。 在这种情况下，`url_path`选择项应该优先于当前类别上下文中的替代项，而不是上述&#x200B;_canonical_&#x200B;选择项。

必须在&#x200B;_CIF URL提供程序配置_&#x200B;中启用此功能。 如果启用，则选择得分比选项高，当

* 它们从头开始匹配给定类别的`url_path`的各个部分（模糊前缀匹配）
* 或者它们与给定类别的`url_key`任意位置匹配（完全部分匹配）

例如，考虑以下[产品查询](https://devdocs.magento.com/guides/v2.4/graphql/queries/products.html)的响应。 基于以下条件：

* 用户位于“2022年夏季新产品/新增”类别页面
* 商店使用默认类别页面URL格式

替代“new-products/new-in-summer-2022/gold-cirque-earrings.html”从头开始匹配上下文的两个路径区段。 即“new-products”和“new-in-summer-2022”。 如果该商店使用的类别页面URL格式仅包含类别`url_key`，则仍将选择相同的替代项，因为它与上下文的`url_key`任意位置相匹配。 在这两种情况下，都会为“new-products/new-in-summer-2022/gold-cirque-earrings.html”`url_path`创建产品页面URL。

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
> 类别识别产品URL需要[CIF核心组件2.6.0](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.6.0)或更高版本。

## 特定类别和产品页面 {#specific-pages}

只能为目录的特定类别或产品子集创建[多类别和产品页面](../authoring/multi-template-usage.md)。

### 选择标准 {#specific-pages-selection}

根据类别的`url_path`或`url_key`，直接选择特定类别页面。 仅包含完整类别`url_path`的URL格式支持匹配子类别。 否则，只能与`url_key`完全匹配。

特定产品页面由产品的SKU或类别选择。 后者要求在产品URL中对某些类别信息进行编码。 此功能仅适用于某些默认URL格式。 有关支持按SKU或类别进行特定页面选择的URL格式的比较，请参阅下表。


| URL格式 | 按SKU | 按类别 |
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
> 按类别选择特定产品页面需要[CIF核心组件2.6.0](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.6.0)或更高版本。

### 深度链接 {#specific-pages-deep-linking}

`UrlProvider`预配置为生成指向创作层实例上特定类别和产品页面的深层链接。 对于编辑者而言，这项功能非常有用。编辑者使用预览模式浏览站点，导航到特定产品或类别页面，然后切换回编辑模式以编辑页面。

另一方面，在发布层实例中，目录页面URL应保持稳定，以免在搜索引擎排名方面失去优势。 由于该发布层，默认情况下，实例不会呈现指向特定目录页面的深层链接。 若要更改此行为，可以将&#x200B;_CIF URL提供程序特定页面策略_&#x200B;配置为始终生成特定页面URL。

### 多个目录页面 {#multiple-product-pages}

当编辑器希望完全控制网站的顶级导航时，可能不需要使用单个目录页面呈现目录的顶级类别。 相反，编辑者可以创建多个目录页面，每个目录页面对应一个要包含在顶级导航中的目录类别。

对于该使用案例，每个目录页面都可以具有对特定于该目录页面所配置类别的产品和类别页面的引用。 `UrlProvider`使用这些连接为配置的类别中的页面和类别创建链接。 但是，出于性能原因，只考虑站点导航根/登陆页面的直接目录页面子项。

建议目录页面的产品和类别页面是该目录页面的子项，否则导航或痕迹导航等组件可能无法正常工作。

>[!NOTE]
>
> 要完全支持多个目录页面，需要[CIF核心组件2.10.0](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.10.0)或更高版本。

## 自定义 {#customization}

### 自定义URL格式 {#custom-url-format}

要提供自定义URL格式，项目可以实现[`ProductUrlFormat`](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/urls/ProductUrlFormat.html)或[`CategoryUrlFormat`](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/urls/CategoryUrlFormat.html)服务接口，并将该实现注册为OSGI服务。 这些实施（如果可用）会替换已配置的预定义格式。 如果注册了多个实施，则服务排名较高的实施将替换服务排名较低的实施。

自定义URL格式实施必须实施一对方法，以便根据给定参数构建URL，并解析URL以分别返回相同的参数。

### 与Sling映射组合 {#sling-mapping}

除了`UrlProvider`之外，还可以配置[Sling映射](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)以重写并处理URL。 AEM Archetype项目还提供了[示例配置](https://github.com/adobe/aem-cif-project-archetype/tree/master/src/main/archetype/samplecontent/src/main/content/jcr_root/etc/map.publish)，以便为端口4503（发布）和80(Dispatcher)配置一些Sling映射。

### 与AEM Dispatcher相结合 {#dispatcher}

使用带有`mod_rewrite`模块的AEM Dispatcher HTTP Server也可以实现URL重写。 [AEM项目原型](https://github.com/adobe/aem-project-archetype)提供了一个引用AEM Dispatcher配置，该配置已包含所生成大小的基本[重写规则](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/dispatcher.cloud)。

## 最佳实践 {#best-practices}

### 选择最佳的URL格式 {#choose-url-format}

如在选择一种可用的默认格式，甚至实施自定义格式之前所述，这在很大程度上取决于存储的需求和要求。 以下建议可能有助于做出有教育意义的决定。

_**使用包含SKU的产品页面URL格式。**_

CIF核心组件使用SKU作为所有组件中的主要标识符。 如果产品页面URL格式不包含SKU，则需要使用GraphQL查询来对其进行解析。 此解决方案可能会影响第一字节的时间。 此外，可能希望购物者能够使用搜索引擎通过SKU找到产品。

_**使用包含类别上下文的产品页面URL格式。**_

CIF URL提供程序的某些功能仅在使用产品URL格式时可用，这些格式对类别上下文进行编码，如类别`url_key`或类别`url_path`。 即使新存储可能不需要这些功能，一开始使用这些URL格式之一有助于减少未来的迁移工作。

_**URL长度与编码信息之间的平衡。**_

根据目录大小，特别是类别树的大小和深度，将整个`url_path`个类别编码到URL中可能不太合理。 在这种情况下，可以通过仅包含类别的`url_key`来缩短URL长度。 此方法支持使用类别`url_path`时的大多数可用功能。

此外，使用[Sling映射](#sling-mapping)将SKU与产品`url_key`相结合。 在大多数电子商务系统中，SKU遵循特定格式，对于传入请求，应可轻松地将SKU与`url_key`分开。 考虑到这一点，应该可以将产品页面URL分别重写为`/p/{{category}}/{{sku}}-{{url_key}}.html`，将类别URL重写为`/c/{{url_key}}.html`。 要将产品和类别页面与其他内容页面区分开来，仍需要`/p`和`/c`前缀。

### 迁移到新URL格式 {#migrate-url-formats}

许多默认URL格式以某种方式相互兼容，这意味着由一种格式的URL可以由另一种格式解析。 这有助于在URL格式之间迁移。

另一方面，搜索引擎需要时间来使用新的URL格式重新爬网所有目录页面。 为了支持此过程并改善最终用户体验，建议提供可将用户从旧URL转发到新URL的重定向。

其中一种方法是将暂存环境连接到生产电子商务后端，并将其配置为使用新的URL格式。 然后，获取由暂存环境和生产环境的CIF产品Sitemap生成器](../../overview/seo-and-url-management.md)生成的[产品Sitemap，并使用它们创建[Apache httpd重写映射](https://httpd.apache.org/docs/2.4/rewrite/rewritemap.html)。 然后，可以将此重写映射与新URL格式的推出一起部署到Dispatcher。

## 示例 {#example}

[Venia引用存储](https://github.com/adobe/aem-cif-guides-venia)项目包含示例配置，用于演示产品和类别页面的自定义URL的使用情况。 此配置允许每个项目根据其SEO需求为产品和类别页面设置单独的URL模式。 使用如上所述的CIF `UrlProvider`和Sling映射的组合。

>[!NOTE]
>
>此配置必须使用项目使用的外部域进行调整。 Sling映射基于主机名和域工作。 因此，此配置默认处于禁用状态，必须在部署之前启用。 为此，请根据使用的域名重命名`ui.content/src/main/content/jcr_root/etc/map.publish/https`中的Sling映射`hostname.adobeaemcloud.com`文件夹，并通过将`resource.resolver.map.location="/etc/map.publish"`添加到项目的`JcrResourceResolver`配置中来启用此配置。

## 其他资源 {#additional}

* [Venia引用存储](https://github.com/adobe/aem-cif-guides-venia)
* [AEM资源映射](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/resource-mapping.html)
* [Sling映射](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)
