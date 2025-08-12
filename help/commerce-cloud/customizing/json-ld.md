---
title: JSON-LD 元数据
description: 了解如何在AEM CIF中启用和验证JSON+LD功能。
feature: Commerce Integration Framework
role: Admin, Developer
exl-id: 547d3721-e094-4a42-8a7c-27e4ef97ea9c
index: false
source-git-commit: edfefb163e2d48dc9f9ad90fa68809484ce6abb0
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 3%

---

# JSON-LD 元数据 {#json-ld}

本指南介绍如何在AEM CIF中启用和验证JSON+LD功能。

>[!NOTE]
>
> 此功能属于实验性质。

## 在CIF配置中启用JSON+LD {#enabling}

默认情况下，**启用JSON+LD**&#x200B;复选框在CIF配置中不可见。 要启用此功能，项目必须包括必要的OSGi配置，该配置可允许显示复选框。 此配置允许用户在产品页面上切换JSON+LD脚本支持。

要使&#x200B;**启用JSON+LD**&#x200B;复选框在CIF配置中可用，请将以下OSGi配置添加到您的项目中：

`com.adobe.cq.cif.components.models.JsonLdFeatureEnable`。

有关添加此配置的更多详细信息，请参阅公共aem-cif-guides-venia存储库中的[添加Json-Ld](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.config/src/main/content/jcr_root/apps/venia/osgiconfig/config/com.adobe.cq.cif.components.models.JsonLdFeatureEnable.cfg.json)的配置。

添加和部署此配置后，该复选框将在CIF配置设置中可见，以下是启用&#x200B;**JSON+LD**&#x200B;的步骤：

1. 导航到AEM中的CIF配置。
1. 取消继承。
1. 选中&#x200B;**启用JSON+LD**&#x200B;复选框。
1. 保存配置。

## 在产品详细信息页面(PDP)上验证JSON+LD {#verify}

为了说明验证JSON+LD的步骤，以Venia项目为例，其中已添加所需的JSON+LD配置来启用该功能。 以下是需遵循的步骤：

1. 导航到本地AEM实例，然后打开产品详细信息页面(PDP)： http://localhost:4502/editor.html/content/venia/us/en/products/product-page.html
1. 在产品详细信息页面(PDP)上创作产品。
1. 切换到&#x200B;**以发布**&#x200B;模式查看。
1. 在浏览器中打开&#x200B;**查看页面Source**。
1. 在页面源中搜索JSON+LD。

如果配置正确，您将发现与插入到页面中的产品相关联的JSON+LD脚本。

## 产品的JSON+LD结构示例 {#sample}

以下是在Venia项目的PDP页面上创作的Agatha Shirt的示例&#x200B;**JSON+LD**：

```
<script type="application/ld+json">
{
  "@context": "http://schema.org",
  "@type": "Product",
  "sku": "VSK05",
  "name": "Agatha Skirt",
  "image": "https://mcstaging.catalogservice4commerce.fun/media/catalog/product/cache/926ea6fc2ad48a7202ff4587b6c2768e/v/s/vsk05-pe_main_2.jpg",
  "description": "The Agatha Skirt has a large circumference that lends itself to all sorts of drama...",
  "@id": "product-ef4fa1dc72",
  "offers": [
    {
      "@type": "Offer",
      "sku": "VSK05-KH-S",
      "url": "/content/venia/us/en/products/product-page.html/agatha-skirt.html",
      "priceCurrency": "USD",
      "price": 78.0
    },
    {
      "@type": "Offer",
      "sku": "VSK05-RN-XS",
      "availability": "InStock",
      "priceSpecification": {
        "@type": "UnitPriceSpecification",
        "priceType": "https://schema.org/ListPrice",
        "price": 18.0,
        "priceCurrency": "USD"
      },
      "price": 46.0
    }
  ]
}
</script>
```

## 将JSON+LD属性映射到GraphQL {#mapping}

JSON+LD属性可以映射到AEM CIF中的GraphQL查询，确保结构化数据动态反映通过GraphQL检索到的产品信息。

### 示例产品映射 {#example}

| JSON+LD属性 | Magento GraphQL属性 | 必需(Y/N) |
|---------------------------------|-------------------|---|
| sku | sku | N |
| offers.url | 自定义逻辑 | N |
| offers.SpecialPricedate | special_to_date | N |
| offers.sku | sku | N |
| offers.priceSpecification.priceCurrency | 货币 | Y |
| offers.priceSpecification.price | regular_price | N |
| offers.priceCurrency | 货币 | Y |
| offers.price | special_price | Y |
| offers.image | media_gallery.url | N |
| offers.availability | stock_status | N |
| name | name | Y |
| 图像 | media_gallery.url | Y |
| 说明 | 说明 | N |
| aggregateRating.reviewCount | review_count | N |
| aggregateRating.ratingValue | rating_summary | N |
| @id | id | N |

此映射可确保根据通过GraphQL查询检索到的产品数据动态填充JSON+LD脚本。

要测试JSON+LD结构，您可以使用[Rich Results Test - Google Search Console](https://search.google.com/test/rich-results/result?id=wtU3LVIEM8H7Aaf5qqK9qw)。 此工具提供详细的反馈，包括所需属性是否存在或缺失，并有助于确保正确实施结构化数据。
