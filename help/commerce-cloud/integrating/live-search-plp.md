---
title: ’[!DNL Live Search] 产品列表页CIF组件
description: 使用CIF组件启用 [!DNL Live Search] AEM网站上的产品列表页面组件
source-git-commit: eaec541c191fc8f68d78662f2b6ab9140460aa9f
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 0%

---


# [!DNL Live Search] CIF组件 {#live-search-cif-component}

Adobe Commerce Live Search可提供快速、相关和直观的搜索体验，而无需支付额外费用。 由Adobe Sensei提供支持的实时搜索使用人工智能和机器学习算法来对汇总的访客数据进行深入分析。 此数据与Adobe Commerce目录结合使用后，可提供相关且个性化的购物体验。

本主题介绍如何使用AEM CIF组件实施 [!DNL Live Search] 将产品列表页面(PLP)构件插入您的AEM网站。

## 前提条件 {#prerequisites}

本主题假设您有一个 [AEM环境](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html?lang=zh-Hans) 设置完毕。

PLP组件需要 [[!DNL Live Search] 弹出窗口CIF组件](live-search-popover.md) 即将安装。 PLP构件需要由弹出窗口生成的浏览器会话变量。

## 更新编辑器 {#update-composer}

将事件模块添加到 `ui.frontend/package.json`.

在第27行，更改：

```json
...
  },

  "devDependencies": {

    "@babel/core": "^7.3.4",
...
```

到:

```json
...
  },
  "type": "module",
  "devDependencies": {
    "@adobe/magento-storefront-event-collector": "^1.5.4",
    "@adobe/magento-storefront-events-sdk": "^1.5.4",
    "@babel/core": "^7.3.4",
...
```

## 文件更改 {#files-changes}

必须更新多个文件才能启用 [!DNL Live Search] 功能。 编辑以下文件。 行号可能与此处显示的略有不同。

* ui.apps/src/main/content/jcr_root/apps/venia/clientlibs/clientlib-cif/.content.xml

  附加 `core.cif.productlist.v1` 到 `embed` 行。

  ```
  embed="[core.cif.components.common,core.cif.components.product.v3,core.cif.components.productcarousel.v1,core.cif.components.productcollection.v2,core.cif.components.productteaser.v1,core.cif.components.searchbar.v2,core.cif.components.header.v1,core.cif.components.carousel.v1,core.cif.components.categorycarousel.v1,core.cif.components.featuredcategorylist.v1,core.cif.components.storefront-events.v1,core.cif.components.extensions.product-recs.storefront-events-collector.v1,core.wcm.components.commons.site.link,core.cif.productlist.v1]"
  ```

* ui.apps/src/main/content/jcr_root/apps/venia/components/commerce/productlist/clientlibs/.content.xml

  创建文件 `.content.xml`：

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <jcr:root xmlns:cq="http://www.day.com/jcr/cq/1.0" xmlns:jcr="http://www.jcp.org/jcr/1.0"
    jcr:primaryType="cq:ClientLibraryFolder"
    allowProxy="{Boolean}true"
    categories="[core.cif.productlist.v1]"
    jsProcessor="[default:none,min:none]"/>
  ```

* ui.apps/src/main/content/jcr_root/apps/venia/components/commerce/productlist/clientlibs/css.txt

  创建文件 `css.txt`：

  ```text
  #base=css
  
  productlist.css
  ```

* ui.apps/src/main/content/jcr_root/apps/venia/components/commerce/productlist/clientlibs/css/productlist.css

  创建文件 `productlist.css`

  ```css
    /* #search-plp-root */
  
  html {
    font-size: 62.5% !important;
  }
  
  body {
    font-size: 1.6rem;
  }
  
  .root.container {
    max-width: inherit;
  }
  
  .container {
    margin-left: auto;
    margin-right: auto;
  }
  
  div.ds-sdk-sort-dropdown {
    z-index: 9;
  }
  ```

* ui.apps/src/main/content/jcr_root/apps/venia/components/commerce/productlist/clientlibs/js.txt

  创建文件 `js.txt`：

  ```text
  js/productlist.js
  ```

* ui.apps/src/main/content/jcr_root/apps/venia/components/commerce/productlist/clientlibs/js/productlist.js

  创建文件 `productlist.js`：

  ```javascript
  /*~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
  ~ Copyright 2023 Adobe
  ~
  ~ Licensed under the Apache License, Version 2.0 (the "License");
  ~ you may not use this file except in compliance with the License.
  ~ You may obtain a copy of the License at
  ~
  ~     http://www.apache.org/licenses/LICENSE-2.0
  ~
  ~ Unless required by applicable law or agreed to in writing, software
  ~ distributed under the License is distributed on an "AS IS" BASIS,
  ~ WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
  ~ See the License for the specific language governing permissions and
  ~ limitations under the License.
  ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~*/
  "use strict";
  
  class ProductList {
    constructor() {
      const stateObject = {
        categoryName: null,
        currentCategoryUrlPath: null,
      };
      this._state = stateObject;
      this._init();
    }
  
    _init() {
      this._initWidgetPLP();
    }
  
    _injectStoreScript(src) {
      const script = document.createElement("script");
      script.type = "text/javascript";
      script.src = src;
  
      document.head.appendChild(script);
    }
  
    async _getStoreData() {
      // get from session storage
      const sessionData = sessionStorage.getItem(
        "WIDGET_STOREFRONT_INSTANCE_CONTEXT"
      );
      // WIDGET_STOREFRONT_INSTANCE_CONTEXT is set from searchbar/clientlibs/js/searchbar.js
      // if not, we will need to retrieve from graphql separately here.
  
      if (sessionData) {
        this._state.dataServicesSessionContext = JSON.parse(sessionData);
        return;
      }
    }
  
    getStoreConfigMetadata() {
      const storeConfig = JSON.parse(
        document
          .querySelector("meta[name='store-config']")
          .getAttribute("content")
      );
  
      const { storeRootUrl } = storeConfig;
      const redirectUrl = storeRootUrl.split(".html")[0];
      return { storeConfig, redirectUrl };
    }
  
    async _initWidgetPLP() {
      if (!window.LiveSearchPLP) {
        const liveSearchPlpSrc =
          "https://plp-widgets-ui.magento-ds.com/v1/search.js";
        this._injectStoreScript(liveSearchPlpSrc);
        // wait until script is loaded
        await new Promise((resolve) => {
          const interval = setInterval(() => {
            if (window.LiveSearchPLP && window.LiveSearchAutocomplete) {
              // Widget expects LiveSearchAutocomplete already loaded to rely on data-service-graphql
              clearInterval(interval);
              resolve();
            }
          }, 200);
        });
      }
      await this._getStoreData();
      const { dataServicesSessionContext } = this._state;
      if (!dataServicesSessionContext) {
        console.log("no dataServicesSessionContext");
        return;
      }
  
      const root = document.getElementById("search-plp-root");
      if (!root) {
        console.log("plp root not found.");
        return;
      }
      // get dataset from root
      const categoryUrlPath = root.getAttribute("data-plp-urlPath") || "";
      const categoryName = root.getAttribute("data-plp-title") || "";
      const storeDetails = {
        environmentId: dataServicesSessionContext.environment_id,
        environmentType: dataServicesSessionContext.environment,
        apiKey: dataServicesSessionContext.api_key,
        websiteCode: dataServicesSessionContext.website_code,
        storeCode: dataServicesSessionContext.store_code,
        storeViewCode: dataServicesSessionContext.store_view_code,
        config: {
          pageSize: dataServicesSessionContext.page_size,
          perPageConfig: {
            pageSizeOptions: dataServicesSessionContext.page_size_options,
            defaultPageSizeOption:
              dataServicesSessionContext.default_page_size_option,
          },
          minQueryLength: dataServicesSessionContext.min_query_length,
          currencySymbol: dataServicesSessionContext.currency_symbol,
          currencyRate: dataServicesSessionContext.currency_rate,
          displayOutOfStock: dataServicesSessionContext.display_out_of_stock,
          allowAllProducts: dataServicesSessionContext.allow_all_products,
          locale: dataServicesSessionContext.locale,
          currentCategoryUrlPath: categoryUrlPath,
          categoryName,
          displayMode: "", // "" for plp || "PAGE" for category/catalog
        },
        context: {
          customerGroup: dataServicesSessionContext.customer_group,
        },
        route: ({ sku }) => {
          return `${
            this.getStoreConfigMetadata().redirectUrl
          }.cifproductredirect.html/${sku}`;
        },
        searchQuery: "search_query",
      };
      setTimeout(() => {
        console.log("init PLP");
        window.LiveSearchPLP({ storeDetails, root });
      }, 0);
    }
  }
  
  (function () {
    function onDocumentReady() {
      new ProductList({});
    }
  
    if (document.readyState !== "loading") {
      onDocumentReady();
    } else {
      document.addEventListener("DOMContentLoaded", onDocumentReady);
    }
  })();
  ```

* ui.apps/src/main/content/jcr_root/apps/venia/components/commerce/productlist/productlist.html

  创建文件 `productlist.html`：

  ```html
  <div
  data-sly-use.productList="com.adobe.cq.commerce.core.components.models.productlist.ProductList"
  id="search-plp-root"
  class="productlist__root"
  data-plp-urlPath="${productList.storefrontContext.urlPath}"
  data-plp-title="${productList.title}">
  </div>
  ```

* ui.apps/src/main/content/jcr_root/apps/venia/components/commerce/searchresults/.content.xml

  编辑 `.content.xml` 在第6行：

  ```xml
  sling:resourceSuperType="venia/components/commerce/productlist"
  ```

* ui.content/src/main/content/jcr_root/content/venia/language-masters/en/search/.content.xml

  编辑 `.content.xml` 在第21-22行：

  ```xml
  sling:resourceType="venia/components/commerce/productlist"
  ```

* ui.content/src/main/content/jcr_root/content/venia/us/en/search/.content.xml

  编辑 `.content.xml` 在第26行：

  ```xml
  sling:resourceType="venia/components/commerce/productlist"
  ```

* ui.frontend/src/main/components/App/App.js

  编辑 `App.js` 在47号线，就在那边 `../../site/main.scss`：

  ```javascript
  import '@adobe/magento-storefront-event-collector';
  ```

* ui.tests/test-module/specs/venia/productlist-dialog.js

  编辑 `productlist-dialog.js` 和更改 `describe` 到 `describe.skip` 在第20行：

  ```javascript
  describe.skip('Product List Component Dialog', function () {
  ```

## 非PLP页面 {#non-plp-pages}

可能存在需要默认类别或目录页面而不是使用PLP小部件的某些类别。 在AEM中，必须手动配置这些类别页面。

1. 从创作页面中，选择一个类别页面模板。 _Venia Store — 主页_ > _目录页面_ > _Venia Store — 类别页面_ 并选择“购买外观”或创建新页面模板。

![选择模板](../assets/cif-widget-1.jpg)

1. 单击 _属性_ 部分，然后选择 _商务_ 选项卡。

![选择属性](../assets/cif-widget-2.jpg)

1. 选择要与所选类别页面模板一起显示的类别。

![选择类别](../assets/cif-widget-3.jpg)
