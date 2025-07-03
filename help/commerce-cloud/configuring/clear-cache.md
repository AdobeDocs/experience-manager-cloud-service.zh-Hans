---
title: 组件和 GraphQL 清除缓存
description: 了解如何在AEM CIF中启用和验证clear-cache功能。
feature: Commerce Integration Framework
role: Admin
exl-id: f89c07c7-631f-41a4-b5b9-0f629ffc36f0
index: false
source-git-commit: 173b70aa6f9ad848d0f80923407bf07540987071
workflow-type: tm+mt
source-wordcount: '883'
ht-degree: 3%

---

# 组件和 GraphQL 清除缓存 {#clear-cache}

本文档提供了有关在AEM CIF中启用和验证clear-cache功能的综合指南。

>[!NOTE]
>
> 此功能属于实验性质。

## 在CIF配置中启用清除缓存功能 {#enable-clear-cache}

默认情况下，CIF配置中禁用清除缓存功能。 要启用该功能，您需要将以下内容添加到相应的项目中：

* 启用Servlet `/bin/cif/invalidate-cache`，它可以通过在项目中添加项目中的`com.adobe.cq.cif.cacheinvalidation.internal.InvalidateCacheNotificationImpl.cfg.json`配置来帮助触发清除缓存API及其相应请求，如[此处](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.config/src/main/content/jcr_root/apps/venia/osgiconfig/config.author/com.adobe.cq.cif.cacheinvalidation.internal.InvalidateCacheNotificationImpl.cfg.json)所示。
  >[!NOTE]
  >
  > 只需为创作实例启用配置。

* 通过在项目中添加`com.adobe.cq.commerce.core.cacheinvalidation.internal.InvalidateCacheSupport.cfg.json`配置，使侦听器能够清除AEM的每个实例（发布和创作）的缓存，如[此处](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.config/src/main/content/jcr_root/apps/venia/osgiconfig/config/com.adobe.cq.commerce.core.cacheinvalidation.internal.InvalidateCacheSupport.cfg.json)所示。
   * 应为创作实例和发布实例启用配置。
   * 启用Dispatcher缓存（可选）：您可以通过在上述配置中将`enableDispatcherCacheInvalidation`属性设置为true来启用Dispatcher清除缓存设置。 这提供了从Dispatcher清除缓存的功能。

     >[!NOTE]
     >
     > 这仅适用于发布实例。

   * 此外，请确保提供适合您的产品、类别和CMS页面的相应模式，并将其添加到上述配置文件中，以便将其从Dispatcher缓存中删除。

* 要提高SQL查询查找与产品和类别相关的相应页面的性能，请在项目中添加相应的索引（推荐）。 有关详细信息，请参阅[cifCacheInvalidationSupport](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.apps/src/main/content/jcr_root/_oak_index/cifCacheInvalidationSupport/.content.xml)。

## 验证清除缓存功能 {#verify-clear-cache}

要验证是否正确设置了所有内容，请执行以下操作：

* 触发与创作实例AEM对应的servlet，例如[http://localhost:4502/bin/cif/invalidate-cache](http://localhost:4502/bin/cif/invalidate-cache)，您应会收到200 HTTP响应。
* 验证已在创作实例中的以下路径下创建节点：`/var/cif/cacheinvalidation`。 节点名称遵循以下模式： `cmd_{{timestamp}}`。
* 验证是否已在每个发布实例中创建相同的节点。

现在，要检查缓存是否正确清除，请执行以下操作：
1. 导航到相应的PLP和PDP页面。
2. 在商业引擎中更新产品或类别名称。 根据缓存配置，这些更改不会立即反映在AEM中。
3. 触发servlet API，如下所示：

   ```
   curl --location '{Author AEM Instance Url}/bin/cif/invalidate-cache' \
   --header 'Content-Type: application/json' \
   --header 'Authorization: ••••••' \ // Mandatory
   --header 'Cookie: private_content_version=0299c5e4368a1577a6f454a61370317b' \
   --data '{
       "productSkus": ["Sku1", "Sku2"], // Optional: Pass the corresponding sku which got updated.
       "categoryUids":["CategoryUid"], // Optional : Pass the corresponding category-uid which got updated.
       "storePath": "/content/venia/us/en", // Mandatory : Needs to be given to know for which site we are removing the clear cache.
   }'
   ```

如果一切顺利，新变化将反映在所有实例中。 如果更改在发布实例上不可见，请尝试在私人/无痕浏览器窗口中访问相关的PLP和PDP页面。

>[!NOTE]
>
> 发布实例可以具有多个级别的缓存层。 该功能仅负责从AEM内部内存和Dispatcher中清除缓存。

## 清除缓存失效API {#clear-cache-api}

当您想要从AEM中清除商业相关数据的缓存时，需要触发此API。

请求类型： `POST`

### 标头

| 参数 | 值 | 必填/必填 | 注释 |
|------------------------------|-------------------|---|---|
| `Content-Type` | `application/json` | 必填 |  |
| `Authorization` | 相应作者的用户凭据（身份验证类型：基本身份验证） | 必填 | 添加相应的用户名和密码。 |


### 有效负荷

下表显示了特征现成的现有属性。 这些`InvalidateType`属性需要与必需属性（如`storePath`）一起提供。

| `invalidateType` | 值 | 类型（数组/字符串/布尔值） | 这将清除Dispatcher缓存吗？ | 注释 |
|------------------------------|-------------------|---|---|---|
| `productSkus` | 产品的SKU — 需要从缓存中失效。 | 数组 | 是 | 使用以下模式从内部内存中清除缓存：<br>```"\"sku\":\\s*\""```<br>Dispatcher<br><ul><li>清除相应SKU的PDP页面缓存</li><li>清除其所在的相应类别页面的缓存（基于来自商业的graphql响应）</li><li>基于以下查询清除缓存：</li></ul><br>```SELECT content.[jcr:path] FROM [nt:unstructured] AS content<br>WHERE ISDESCENDANTNODE(content, '{storePath}')<br>AND ( (content.[product] IN ('sku1','sku2') AND content.[productType] = 'combinedSku')<br> OR (content.[selection] IN ('sku1','sku2') AND content.[selectionType] IN ('combinedSku', 'sku')))``` |
| `categoryUids` | 类别的uid — 需要从缓存中使其失效。 | 数组 | 是 | 使用以下模式从内部内存中清除缓存：<br>```"\"uid\"\\s*:\\s*\\{\"id\"\\s*:\\s*\""```<br>Dispatcher<br><ul><li>清除相应数据的类别页面缓存（包括其子类别页面）</li><li>清除具有相应类别的所有PDP页面</li><li>基于以下查询清除缓存：</li></ul><br>```SELECT content.[jcr:path] FROM [nt:unstructured] AS content<br>WHERE ISDESCENDANTNODE(content,'{storePath}')<br>AND ((content.[categoryId] in ('category1','category2')<br>AND content.[categoryIdType] in ('uid'))<br>OR (content.[category] in ('category1','category2') AND content.[categoryType] in ('uid')))``` |
| `regexPatterns` | 如果需要根据正则表达式模式清除GraphQL响应数据，请使用此项。 | 数组 | 否 | |
| `cacheNames` | 此值在相应的CIF GraphQL客户端配置工厂>>相应的StorePath GraphQL配置>> GraphQL缓存配置下定义 | 数组 | 否 | |
| `invalidateAll` | True或false | 布尔值 | 是 | |

下表显示在每个API调用中需要传递的必需属性：

| 属性 | 值 | 类型（数组/字符串/布尔值） | 这将清除Dispatcher缓存吗？ | 注释 |
|------------------------------|-------------------|---|---|---|
| `storePath` | 需要从中删除缓存的站点路径的对应值（示例： `/content/venia/us/en`作为对Venia项目的引用）。 | 字符串 | 是 | 需要以`invalidateType.`的组合提供此值 |

### 示例API请求

```
curl --location 'https://author-p10603-e145552-cmstg.adobeaemcloud.com/bin/cif/invalidate-cache' \
--header 'Content-Type: application/json' \
--header 'Authorization: ••••••' \
--header 'Cookie: private_content_version=0299c5e4368a1577a6f454a61370317b' \
--data '{
"productSkus": ["VP01", "VT10"], // This will clear cache for the corresponding pages related with mentioned skus.
"categoryUids":["Mjk="], // This will clear cache for the corresponding pages related with mentioned categories.
"regexPatterns":["\"uid\"\\s*:\\s*\\{\"id\"\\s*:\\s*\"(Mjk=)\"", "\"sku\":\\s*\"(VP02|VP03)\""],
"cacheNames": ["venia/components/commerce/product"], // If this been added then it will clear respective caches for the corresponding storepath
"storePath": "/content/venia/us/en"
}'
```

## 可扩展性 {#clear-cache-extensibility}

此功能不仅提供了其核心功能，而且还提供了可扩展性，允许开发人员根据需要进一步对其进行构建和自定义。

### 扩展现有属性 {#existing-attribute}

如果需要清除现有基于属性的功能（如`categoryUids`）当前未涵盖的缓存，您可以引用[此参考文件](https://github.com/adobe/aem-cif-guides-venia/blob/main/core/src/main/java/com/venia/core/models/commerce/services/cacheinvalidation/ExtendedCategoryUidInvalidation.java)以添加新模式并定义应从缓存中清除的超出当前实现处理范围的其他`invalidatePaths`。

### 添加新的自定义属性 {#new-custom-attribute}

例如，如果不想使用现有属性来清除缓存，则可以灵活地创建自己的属性并定义其相应的功能。

* 如果只需要从AEM的内部内存中清除缓存（graphql响应），则需要遵循[此引用](https://github.com/adobe/aem-cif-guides-venia/blob/main/core/src/main/java/com/venia/core/models/commerce/services/cacheinvalidation/CustomInvalidation.java)。
* 如果需要从内部内存和Dispatcher缓存中清除缓存，则需要遵循[此引用](https://github.com/adobe/aem-cif-guides-venia/blob/main/core/src/main/java/com/venia/core/models/commerce/services/cacheinvalidation/CustomDispatcherInvalidation.java)。
  >[!NOTE]
  >
  > 您可以通过返回`null`方法的`getPatterns()`来忽略内部清除缓存。
