---
title: CIF 产品轮播的自定义属性
description: 了解如何通过更新Sling模型和自定义标记来扩展AEM CIF产品轮盘组件。
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: 594f0e6ec88851c86134be8d5d7f1719f74ddf4f
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 4%

---

# CIF 产品轮播的自定义属性 {#product-carousel}

## 简介 {#intro}

在本教程中对产品轮盘组件进行了扩展。 第一步，将产品轮播的实例添加到主页以了解基线功能：

1. 导航到网站的主页，例如[http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html)
1. 将新的产品轮盘组件插入页面上的主布局容器。
   ![产品轮盘组件](/help/commerce-cloud/assets/product-carousel-component.png)
1. 展开侧面板（如果尚未切换）并将资产查找器下拉列表切换为&#x200B;**产品**。
     ![轮播产品](/help/commerce-cloud/assets/carousel-products.png)    
1. 此时应会显示已连接的Adobe Commerce实例中可用产品的列表。
   ![连接的实例](/help/commerce-cloud/assets/connected-instance.png)
1. 产品将显示如下，默认属性为：
   显示的![产品具有属性](/help/commerce-cloud/assets/discount.png)

## 更新Sling模型 {#update-sling-model}

您可以通过实施Sling模型来扩展产品轮播的业务逻辑：

1. 在IDE的核心模块下导航到`core/src/main/java/com/venia/core/models/commerce`，并创建扩展CIF ProductCarousel界面的自定义轮播界面：

   ```
   package com.venia.core.models.commerce;
   import com.adobe.cq.commerce.core.components.models.productcarousel.ProductCarousel;
   public interface CustomCarousel extends ProductCarousel {
   }
   ```
1. 接下来，在`core/src/main/java/com/venia/core/models/commerce/CustomCarouselImpl.java`处创建实现类`CustomCarouselImpl.java`。
Sling模型的委托模式允许`CustomCarouselImpl`通过`sling:resourceSuperType`属性引用`ProductCarousel`模型：

   ```
   @Self
   @Via(type = ResourceSuperType.class)
   private ProductCarousel productCarousel;
   ```

1. @PostConstruct注释可确保在Sling模型初始化时调用此方法。 产品GraphQL查询已使用extendProductQueryWith方法扩展以检索属性。 更新GraphQL查询以包含  部分查询中的属性：

   ```
   @PostConstruct
   private void initModel() {
   productsRetriever = productCarousel.getProductsRetriever();
   
   if(productCarousel.getProductsRetriever() != null)
   productCarousel.getProductsRetriever().extendProductQueryWith(p -> p
   .createdAt()
   .addCustomSimpleField("accessory_gemstone_addon")
   );
   }
   ```

   在上述代码中，`addCustomSimpleField`用于检索`accessory_gemstone_addon`属性。

## 自定义标记 {#customize-markup}

要进一步自定义标记，请执行以下操作：

1. 创建从`/apps/core/cif/components/commerce/productcarousel/v1/productcarousel` （核心组件crxde路径）到ui.apps模块`ui.apps/src/main/content/jcr_root/apps/venia/components/commerce/productcarousel/productcard.html`的`productcard.html`的副本。

1. 编辑`productcard.html`以调用实现类中提到的自定义属性：

   ```xml
   ..
   <div
       data-product-sku="${product.commerceIdentifier.value}"
       data-product-base-sku="${product.combinedSku.baseSku}"
       id="${product.id}"
       data-cmp-data-layer="${product.data.json}"
       class="card product__card">
       <span>${product.product.responseData['accessory_gemstone_addon']}</span>
       <a href="${product.URL}"
           target="${productCarousel.linkTarget}"
   ..
   ```

1. 使用命令行终端的Maven命令保存更改并将更新部署到AEM。 您将能够在页面上看到所选产品的自定义属性`accessory_gemstone_addon`值。
