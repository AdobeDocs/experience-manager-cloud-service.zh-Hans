---
title: 高级URL配置
description: 了解如何自定义产品和类别页面的URL。 这允许实施为搜索引擎优化URL并促进发现。
sub-product: 商务
version: cloud-service
doc-type: technical-video
activity: setup
audience: administrator
feature: Commerce Integration Framework
kt: 4933
thumbnail: 34350.jpg
translation-type: tm+mt
source-git-commit: 72d98c21a3c02b98bd2474843b36f499e8d75a03
workflow-type: tm+mt
source-wordcount: '789'
ht-degree: 3%

---


# 高级URL配置 {#url}

[AEM CIF核心组件](https://github.com/adobe/aem-core-cif-components) 提供高级配置，以自定义产品和类别页面的URL。 许多实施将自定义这些URL以用于搜索引擎优化(SEO)。  以下视频详细信息如何配置 `UrlProvider` Sling Mapping的服 [务和功能](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) ，以自定义产品和类别页面的URL。

>[!VIDEO](https://video.tv.adobe.com/v/34350/?quality=12)

## 配置 {#configuration}

要根据SEO `UrlProvider` 要求配置服务，并且需要项目必须为“CIF URL提供者配置”配置提供OSGI配置，并按如下所述配置服务。

>[!NOTE]
>
> 请参见 [下面的](https://github.com/adobe/aem-cif-guides-venia) Venia Reference store项目，其中包括示例配置，用于演示产品和类别页面的自定义URL的用法。

### 产品页面URL模板 {#product}

这将使用以下属性配置产品页面的URL:

* **产品URL模板**:定义包含一组占位符的URL格式。 默认值 `{{page}}.{{url_key}}.html#{{variant_sku}}`为，它最终生成URL，如 `/content/venia/us/en/products/product-page.chaz-kangeroo-hoodie.html#MH01-M-Orange`
   * `{{page}}` 替换为 `/content/venia/us/en/products/product-page`
   * `{{url_key}}` 被Magento的产 `url_key` 品属性所取代，此处 `chaz-kangeroo-hoodie`
   * `{{variant_sku}}` 被当前选定的变体替换，此处 `MH01-M-Orange`
* **产品标识符位置**:定义用于获取产品数据的标识符的位置。 默认值为， `SELECTOR`另一个可能的值为 `SUFFIX`。 对于上一个示例URL，这意味着将 `chaz-kangeroo-hoodie` 使用标识符获取产品数据。
* **产品标识符类型**:定义获取产品数据时要使用的标识符的类型。 默认值为， `URL_KEY`另一个可能的值为 `SKU`。 对于上一个示例URL，这意味着将使用MagentoGraphQL过滤器(如 `filter:{url_key:{eq:"chaz-kangeroo-hoodie"}}`)获取产品数据

### 产品列表页URL模板 {#product-list}

这将使用以下属性配置类别或产品列表页的URL:

* **类别URL模板**:定义包含一组占位符的URL格式。 默认值 `{{page}}.{{id}}.html`为，它最终生成URL，如 `/content/venia/us/en/products/category-page.3.html`
   * `{{page}}` 替换为 `/content/venia/us/en/products/category-page`
   * `{{id}}` 被Magento的 `id` 类别财产所取代 `3`
* **类别标识符位置**:定义用于获取产品数据的标识符的位置。 默认值为， `SELECTOR`另一个可能的值为 `SUFFIX`。 对于上一个示例URL，这意味着将 `3` 使用标识符获取产品数据。
* **类别标识符类型**:定义获取产品数据时要使用的标识符的类型。 默认值和当前仅支持的值为 `ID`。 对于上一个示例URL，这意味着将使用类别GraphQL过滤器(如 `category(id:3)`)获取

只要组件使用设置相应数据，就可以为每个模板添加自定义属性 `UrlProvider`。 检查类的代码示例 `ProductListItemImpl` ，了解如何实现它。

也可以用完全自定义 `UrlProvider` 的OSGi服务替换该服务。 在这种情况下，必须实现该接 `UrlProvider` 口并用更高的服务等级对其进行注册，以替换默认实现。

## 与Sling映射组合 {#sling-mapping}

除了Sling映射 `UrlProvider`之外，还可以配置Sling [映射](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) ，以便重写和处理URL。 AEM Archetype项目还提供了 [一个示例配置](https://github.com/adobe/aem-cif-project-archetype/tree/master/src/main/archetype/samplecontent/src/main/content/jcr_root/etc/map.publish) ，用于为端口4503（发布）和80（调度程序）配置某些Sling映射。

## 与AEM Dispatcher结合使用 {#dispatcher}

URL重写也可以通过将AEM Dispatcher HTTP服务器与模块结合使用来 `mod_rewrite` 实现。 AEM [Project Archetype](https://github.com/adobe/aem-project-archetype) 提供引用AEM Dispatcher配置，该配置已包括生成 [大小的基](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/dispatcher.cloud) 本重写规则。

## 示例

Venia Reference [store项目包含](https://github.com/adobe/aem-cif-guides-venia) 示例配置，用于演示产品和类别页面的自定义URL的用法。 这允许每个项目根据其SEO需求为产品和类别页面设置单独的URL模式。 使用上述 `UrlProvider` CIF和Sling映射的组合。

>[!NOTE]
>
>此配置必须使用项目使用的外部域进行调整。 Sling映射基于主机名和域运行。 因此，此配置默认处于禁用状态，在部署之前必须启用。 为此，请根据使用的 `hostname.adobeaemcloud.com` 域名 `ui.content/src/main/content/jcr_root/etc/map.publish/https` 在中重命名Sling Mapping文件夹，并通过添加 `resource.resolver.map.location="/etc/map.publish"` 到项目 `JcrResourceResolver` 的配置来启用此配置。

## 其他资源

* [Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)
* [AEM资源映射](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/configuring/resource-mapping.html)
* [Sling映射](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)
