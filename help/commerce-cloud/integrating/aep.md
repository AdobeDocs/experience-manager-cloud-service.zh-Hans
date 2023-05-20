---
title: AEM-CIF核心元件與Adobe Experience Platform整合
description: 瞭解如何使用CIF - Storefront Connector將店面事件資料從AEM呈現的產品頁面傳送到Experience Platform。Experience Platform
sub-product: Commerce
version: Cloud Service
activity: setup
feature: Commerce Integration Framework
topic: Commerce
role: Architect, Developer
level: Beginner
kt: 10834
thumbnail: 346811.jpeg
exl-id: 30bb9b2c-5f00-488e-ad5c-9af7cd2c4735
source-git-commit: 73fe6ce5bbdf0ad437ae4b47b892ad05e016ab68
workflow-type: tm+mt
source-wordcount: '2080'
ht-degree: 1%

---

# AEM-CIF核心元件與Adobe Experience Platform整合 {#aem-cif-aep-integration}

此 [Commerce Integration Framework (CIF)](https://github.com/adobe/aem-core-cif-components) 核心元件提供與下列專案緊密整合： [Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-overview.html?lang=en) 轉寄店面事件及其來自使用者端互動的資料，例如 __加入購物車__.

此 [AEM CIF Core Components](https://github.com/adobe/aem-core-cif-components) project提供JavaScript程式庫，稱為 [Adobe Commerce的Adobe Experience Platform聯結器](https://github.com/adobe/aem-core-cif-components/tree/master/extensions/experience-platform-connector) 以從Commerce店面收集事件資料。 該事件資料會傳送至Experience Platform，並用於其他Adobe Experience Cloud產品(例如Adobe Analytics和Adobe Target)，以建立涵蓋客戶歷程的360度設定檔。 透過將Commerce資料連線到Adobe Experience Cloud中的其他產品，您可以執行分析網站上的使用者行為、執行AB測試和建立個人化行銷活動等工作。

進一步瞭解 [Experience Platform資料彙集](https://experienceleague.adobe.com/docs/experience-platform/collection/home.html) 可讓您從使用者端來源收集客戶體驗資料的技術套件。

## 傳送 `addToCart` 要Experience Platform的事件資料 {#send-addtocart-to-aep}

下列步驟說明如何傳送 `addToCart` 事件資料會從AEM呈現的產品頁面使用CIF -Experience Platform聯結器傳送至Experience Platform。 您可以使用Adobe Experience Platform Debugger瀏覽器擴充功能，測試並檢閱提交的資料。

![在Adobe Experience Platform Debugger中檢閱addToCart事件資料](../assets/aep-integration/EventData-AEM-AEP.png)

## 前提条件 {#prerequisites}

您必須使用本機開發環境才能完成此示範。 這包括執行中的AEM執行個體，其已設定並連線至Adobe Commerce執行個體。 檢閱的需求和步驟 [使用AEMas a Cloud ServiceSDK設定本機開發](../develop.md).

您還需要以下專案的存取權： [Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-ui/ui-guide.html) 以及建立資料收集之結構、資料集和資料流的許可權。 如需詳細資訊，請參閱 [許可權管理](https://experienceleague.adobe.com/docs/experience-platform/collection/permissions.html).

## AEM Commerceas a Cloud Service設定 {#aem-setup}

若要讓工作正常 __AEM Commerceas a Cloud Service__ 使用必要程式碼和設定的本機環境，請完成以下步驟。

### 本機設定

請遵循 [本機設定](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/content-and-commerce/storefront/developing/develop.html?#local-setup) 建立運作中的AEM Commerceas a Cloud Service環境的步驟。

### 專案設定

請遵循 [AEM專案原型](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/content-and-commerce/storefront/developing/develop.html?#project) 建立全新AEM Commerce (CIF)專案的步驟。

>[!TIP]
>
>在以下範例中，AEM Commerce專案名為： `My Demo Storefront`不過，您可以選擇自己的專案名稱。

![AEM Commerce專案](../assets/aep-integration/aem-project-with-commerce.png)


從專案的根目錄執行下列命令，建置新建立的AEM Commerce專案並將其部署至本機AEM SDK。

```bash
$ mvn clean install -PautoInstallSinglePackage
```

本機部署 `My Demo StoreFront` 具有預設程式碼和內容的商務網站如下所示：

![預設AEM Commerce網站](../assets/aep-integration/demo-aem-storefront.png)

### 安裝Peregrine和CIF-AEP聯結器相依性

若要從此AEM Commerce網站的類別和產品頁面收集並傳送事件資料，您必須安裝金鑰 `npm` 將套件封裝到 `ui.frontend` AEM Commerce專案的模組。

導覽至 `ui.frontend` 模組，並從命令列執行下列命令來安裝所需的套裝軟體。

```bash
npm i --save lodash.get@^4.4.2 lodash.set@^4.3.2
npm i --save apollo-cache-persist@^0.1.1
npm i --save redux-thunk@~2.3.0
npm i --save @adobe/apollo-link-mutation-queue@~1.1.0
npm i --save @magento/peregrine@~12.5.0
npm i --save @adobe/aem-core-cif-react-components --force
npm i --save-dev @magento/babel-preset-peregrine@~1.2.1
npm i --save @adobe/aem-core-cif-experience-platform-connector --force
```

>[!IMPORTANT]
>
>此 `--force` 有時需要引數為 [PWA Studio](https://developer.adobe.com/commerce/pwa-studio/) 受支援的對等相依性限制。 這通常不會造成任何問題。


### 設定Maven以使用 `--force` 引數

在Maven建置流程中，npm全新安裝(使用 `npm ci`)觸發。 這同樣需要 `--force` 引數。

導覽至專案的根POM檔案 `pom.xml` 並找到 `<id>npm ci</id>` 執行區塊。 更新區塊，使其如下所示：

```xml
<execution>
    <id>npm ci</id>
    <goals>
    <goal>npm</goal>
    </goals>
    <configuration>
    <arguments>ci --force</arguments>
    </configuration>
</execution>
```

### 變更Babel組態格式

從預設值切換 `.babelrc` 檔案相對組態檔案格式為 `babel.config.js` 格式。 此為專案範圍的設定格式，可將外掛程式和預設集套用至 `node_module` 擁有更優異的控制力。

1. 導覽至 `ui.frontend` 模組並刪除現有 `.babelrc` 檔案。

1. 建立 `babel.config.js` 使用 `peregrine` 預設集。

   ```javascript
   const peregrine = require('@magento/babel-preset-peregrine');
   
   module.exports = (api, opts = {}) => {
       const config = {
           ...peregrine(api, opts),
           sourceType: 'unambiguous'
       } 
   
       config.plugins = config.plugins.filter(plugin => plugin !== 'react-refresh/babel');
   
       return config;
   }
   ```

### 設定webpack以使用Babel

若要使用Babel載入器傳輸JavaScript檔案(`babel-loader`)和webpack，您需要修改 `webpack.common.js` 檔案。

導覽至 `ui.frontend` 模組並更新 `webpack.common.js` 檔案的下列規則位於 `module` 屬性值：

```javascript
{
    test: /\.jsx?$/,
    exclude: /node_modules\/(?!@magento\/)/,
    loader: 'babel-loader'
}
```

### 設定Apollo使用者端

此 [Apollo使用者端](https://www.apollographql.com/docs/react/) 用於透過GraphQL管理本機與遠端資料。 它也會將GraphQL查詢的結果儲存在本機、正規化的記憶體快取中。

對象 [`InMemoryCache`](https://www.apollographql.com/docs/react/caching/cache-configuration/) 若要有效運作，您需要 `possibleTypes.js` 檔案。 若要產生此檔案，請參閱 [自動產生possibleType](https://www.apollographql.com/docs/react/data/fragments/#generating-possibletypes-automatically). 另請參閱 [PWA Studio參考實作](https://github.com/magento/pwa-studio/blob/1977f38305ff6c0e2b23a9da7beb0b2f69758bed/packages/pwa-buildpack/lib/Utilities/graphQL.js#L106-L120) 和範例 [`possibleTypes.js`](../assets/aep-integration/possibleTypes.js) 檔案。


1. 導覽至 `ui.frontend` 模組，並將檔案另存為 `./src/main/possibleTypes.js`

1. 更新 `webpack.common.js` 檔案的 `DefinePlugin` 區段，以在建置期間取代必要的靜態變數。

   ```javascript
   const { DefinePlugin } = require('webpack');
   const { POSSIBLE_TYPES } = require('./src/main/possibleTypes');
   
   ...
   
   plugins: [
       ...
       new DefinePlugin({
           'process.env.USE_STORE_CODE_IN_URL': false,
           POSSIBLE_TYPES
       })
   ]
   ```

### 初始化Peregrine和CIF核心元件

若要初始化以React為基礎的Peregrine和CIF核心元件，請建立所需的設定和JavaScript檔案。

1. 導覽至 `ui.frontend` 模組，並建立下列資料夾： `src/main/webpack/components/commerce/App`

1. 建立 `config.js` 包含下列內容的檔案：

   ```javascript
   // get and parse the CIF store configuration from the <head>
   const storeConfigEl = document.querySelector('meta[name="store-config"]');
   const storeConfig = storeConfigEl ? JSON.parse(storeConfigEl.content) : {};
   
   // the following global variables are needed for some of the peregrine features
   window.STORE_VIEW_CODE = storeConfig.storeView || 'default';
   window.AVAILABLE_STORE_VIEWS = [
       {
           code: window.STORE_VIEW_CODE,
           base_currency_code: 'USD',
           default_display_currency_code: 'USD',
           id: 1,
           locale: 'en',
           secure_base_media_url: '',
           store_name: 'My Demo StoreFront'
       }
   ];
   window.STORE_NAME = window.STORE_VIEW_CODE;
   window.DEFAULT_COUNTRY_CODE = 'en';
   
   export default {
       storeView: window.STORE_VIEW_CODE,
       graphqlEndpoint: storeConfig.graphqlEndpoint,
       // Can be GET or POST. When selecting GET, this applies to cache-able GraphQL query requests only.
       // Mutations will always be executed as POST requests.
       graphqlMethod: storeConfig.graphqlMethod,
       headers: storeConfig.headers,
   
       mountingPoints: {
           // TODO: define the application specific mount points as they may be used by <Portal> and <PortalPlacer>
       },
       pagePaths: {
           // TODO: define the application specific paths/urls as they may be used by the components
           baseUrl: storeConfig.storeRootUrl
       },
       eventsCollector: {
           // Enable the Experience Platform Connector and define the org and datastream to use
           aep: {
               orgId: // TODO: add your orgId
               datastreamId: // TODO: add your datastreamId
           }
       }
   };
   ```

   >[!IMPORTANT]
   >
   >雖然您可能已經熟悉 [`config.js`](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.frontend/src/main/components/App/config.js) 檔案來源 __AEM Guides - CIF Venia Project__，您需要對此檔案進行一些變更。 首先，檢閱任何 __待辦事項__ 評論。 然後，在內部 `eventsCollector` 屬性，尋找 `eventsCollector > aed` 物件並更新 `orgId` 和 `datastreamId` 屬性至正確的值。 [了解详情](./aep.md#add-aep-values-to-aem).

1. 建立 `App.js` 檔案及下列內容。 此檔案類似於典型的React應用程式起點檔案，並包含React和自訂鉤點和React Context使用方式，以促進Experience Platform整合。

   ```javascript
   import config from './config';
   
   import React, { useEffect } from 'react';
   import ReactDOM from 'react-dom';
   import { IntlProvider } from 'react-intl';
   import { BrowserRouter as Router } from 'react-router-dom';
   import { combineReducers, createStore } from 'redux';
   import { Provider as ReduxProvider } from 'react-redux';
   import { createHttpLink, ApolloProvider } from '@apollo/client';
   import { ConfigContextProvider, useCustomUrlEvent, useReferrerEvent, usePageEvent, useDataLayerEvents, useAddToCartEvent } from '@adobe/aem-core-cif-react-components';
   import { EventCollectorContextProvider, useEventCollectorContext } from '@adobe/aem-core-cif-experience-platform-connector';
   import { useAdapter } from '@magento/peregrine/lib/talons/Adapter/useAdapter';
   import { customFetchToShrinkQuery } from '@magento/peregrine/lib/Apollo/links';
   import { BrowserPersistence } from '@magento/peregrine/lib/util';
   import { default as PeregrineContextProvider } from '@magento/peregrine/lib/PeregrineContextProvider';
   import { enhancer, reducers } from '@magento/peregrine/lib/store';
   
   const storage = new BrowserPersistence();
   const store = createStore(combineReducers(reducers), enhancer);
   
   storage.setItem('store_view_code', config.storeView);
   
   const App = () => {
       const [{ sdk: mse }] = useEventCollectorContext();
   
       // trigger page-level events
       useCustomUrlEvent({ mse });
       useReferrerEvent({ mse });
       usePageEvent({ mse });
       // listen for add-to-cart events and enable forwarding to the magento storefront events sdk
       useAddToCartEvent(({ mse }));
       // enable CIF specific event forwarding to the Adobe Client Data Layer
       useDataLayerEvents();
   
       useEffect(() => {
           // implement a proper marketing opt-in, for demo purpose we hard-set the consent cookie
           if (document.cookie.indexOf('mg_dnt') < 0) {
               document.cookie += '; mg_dnt=track';
           }
       }, []);
   
       // TODO: use the App to create Portals and PortalPlaceholders to mount the CIF / Peregrine components to the server side rendered markup
       return <></>;
   };
   
   const AppContext = ({ children }) => {
       const { storeView, graphqlEndpoint, graphqlMethod = 'POST', headers = {}, eventsCollector } = config;
       const { apolloProps } = useAdapter({
           apiUrl: new URL(graphqlEndpoint, window.location.origin).toString(),
           configureLinks: (links, apiBase) =>
               // reconfigure the HTTP link to use the configured graphqlEndpoint, graphqlMethod and storeView header
   
               links.set('HTTP', createHttpLink({
                   fetch: customFetchToShrinkQuery,
                   useGETForQueries: graphqlMethod !== 'POST',
                   uri: apiBase,
                   headers: { ...headers, 'Store': storeView }
               }))
       });
   
       return (
           <ApolloProvider {...apolloProps}>
               <IntlProvider locale='en' messages={{}}>
                   <ConfigContextProvider config={config}>
                       <ReduxProvider store={store}>
                           <PeregrineContextProvider>
                               <EventCollectorContextProvider {...eventsCollector}>
                                   {children}
                               </EventCollectorContextProvider>
                           </PeregrineContextProvider>
                       </ReduxProvider>
                   </ConfigContextProvider>
               </IntlProvider>
           </ApolloProvider>
       );
   };
   
   window.onload = async () => {
       const root = document.createElement('div');
       document.body.appendChild(root);
   
       ReactDOM.render(
           <Router>
               <AppContext>
                   <App />
               </AppContext>
           </Router>,
           root
       );
   };
   ```

   此 `EventCollectorContext` 匯出React內容，其中：

   - 載入commerce-events-sdk和commerce-events-collector資料庫，
   - 使用指定的Experience Platform和/或ACDS設定將它們初始化
   - 訂閱Peregrine的所有事件，並將其轉送至事件SDK

   您可以檢閱的實作詳細資料 `EventCollectorContext` [此處](https://github.com/adobe/aem-core-cif-components/blob/3d4e44d81fff2f398fd2376d24f7b7019f20b31b/extensions/experience-platform-connector/src/events-collector/EventCollectorContext.js).

### 建置和部署更新的AEM專案

為確保上述套件安裝、程式碼和設定變更正確，請使用以下Maven命令重新建置和部署更新的AEM Commerce專案： `$ mvn clean install -PautoInstallSinglePackage`.

## Experience Platform設定 {#aep-setup}

若要接收並儲存來自AEM Commerce頁面（例如類別和產品）的事件資料，請完成以下步驟：

>[!AVAILABILITY]
>
>確定您屬於正確的一分子 __產品設定檔__ 在 __Adobe Experience Platform__ 和 __Adobe Experience Platform資料彙集__. 如有需要，請與系統管理員合作來建立、更新或指派 __產品設定檔__ 在 [Admin Console](https://adminconsole.adobe.com/).

### 使用商務欄位群組建立結構描述

若要定義商務事件資料的結構，您必須建立體驗資料模型(XDM)結構描述。 結構是一組規則，可代表及驗證資料的結構和格式。

1. 在瀏覽器中導覽至 __Adobe Experience Platform__ 產品首頁。 例如：<https://experience.adobe.com/#/@YOUR-ORG-NAME/sname:prod/platform/home>。

1. 找到 __結構描述__ 功能表，按一下 __建立結構描述__ 按鈕，然後選取 __XDM ExperienceEvent__.

   ![AEP建立結構描述](../assets/aep-integration/AEP-Schema-EventSchema-1.png)

1. 使用為您的結構描述命名 __結構描述屬性>顯示名稱__ 欄位並使用新增欄位群組  __構成>欄位群組>新增__ 按鈕。

   ![AEP結構描述定義](../assets/aep-integration/AEP-Schema-Definition.png)

1. 在 __新增欄位群組__ 對話方塊，搜尋 `Commerce`，選取 __商務詳細資料__ 核取方塊，然後按一下 __新增欄位群組__.

   ![AEP結構描述定義](../assets/aep-integration/AEP-Schema-Field-Group.png)


>[!TIP]
>
>請參閱 [結構描述組合基本概念](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html) 以取得詳細資訊。

### 建立資料集

若要儲存事件資料，您必須建立符合結構描述定義的資料集。 資料集是資料集合的儲存和管理結構，通常是包含方案（欄）和欄位（列）的表格。

1. 在瀏覽器中導覽至 __Adobe Experience Platform__ 產品首頁。 例如：<https://experience.adobe.com/#/@YOUR-ORG-NAME/sname:prod/platform/home>。

1. 找到 __資料集__ 功能表，然後按一下 __建立資料集__ 按鈕。

   ![AEP建立資料集](../assets/aep-integration/AEP-Datasets-Create.png)

1. 在新頁面上，選取 __從結構描述建立資料集__ 卡片。

   ![AEP建立資料集結構描述選項](../assets/aep-integration/AEP-Datasets-Schema-Option.png)

- 在新頁面上， __搜尋並選取__ 您在上一步建立的綱要，然後按一下 __下一個__ 按鈕。

   ![AEP建立資料集選取結構描述](../assets/aep-integration/AEP-Datasets-Select-Schema.png)

1. 使用為您的資料集命名 __設定資料集>名稱__ 欄位並按一下 __完成__ 按鈕。

   ![AEP建立資料集名稱](../assets/aep-integration/AEP-Datasets-Name.png)

>[!TIP]
>
>請參閱 [資料集總覽](https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/overview.html) 以取得詳細資訊。


### 建立資料串流

完成下列步驟，在Experience Platform中建立資料串流。

1. 在瀏覽器中導覽至 __Adobe Experience Platform__ 產品首頁。 例如：<https://experience.adobe.com/#/@YOUR-ORG-NAME/sname:prod/platform/home>。

1. 找到 __資料串流__ 功能表，然後按一下 __新增資料串流__ 按鈕。

   ![AEP建立資料串流](../assets/aep-integration/AEP-Datastream-Create.png)

1. 使用為您的資料流命名 __名稱__ 必填欄位。 在 __事件結構描述__ 欄位中，選取新建立的結構描述並按一下 __儲存__.

   ![aep定義資料串流](../assets/aep-integration/AEP-Datastream-Define.png)

1. 開啟新建立的資料流，然後按一下 __新增服務__.

   ![AEP資料串流新增服務](../assets/aep-integration/AEP-Datastream-Add-Service.png)

1. 在 __服務__ 欄位中，選取 __Adobe Experience Platform__ 選項。 下 __事件資料集__ 欄位中，選取上一步的資料集名稱，然後按一下 __儲存__.

   ![AEP資料串流新增服務詳細資料](../assets/aep-integration/AEP-Datastream-Add-Service-Define.png)

>[!TIP]
>
>請參閱 [資料流概觀](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/overview.html) 以取得詳細資訊。

## 將資料串流值新增至AEM Commerce設定 {#add-aep-values-to-aem}

完成上述Experience Platform設定後，您應 `datastreamId` 資料流詳細資訊的左側邊欄和 `orgId` 右上角 __個人資料圖片>帳戶資訊>使用者資訊__ 強制回應視窗。

![AEP資料串流ID](../assets/aep-integration/AEP-Datastream-ID.png)

1. 在AEM Commerce專案的 `ui.frontend` 模組，更新 `config.js` 檔案，尤其是 `eventsCollector > aep` 物件屬性。

1. 建置和部署更新的AEM Commerce專案


## 觸發 `addToCart` 事件與驗證資料收集 {#event-trigger-verify}

上述步驟已完成AEM Commerce和Experience Platform設定。 您現在可以觸發 `addToCart` 事件並使用Experience Platform偵錯程式和資料集驗證資料收集 __度量和圖表__ 在產品UI中切換。

若要觸發事件，您可以使用AEM作者或本機設定中的發佈服務。 在此範例中，透過登入您的帳戶來使用AEM author。

1. 從「網站」頁面中，選取 __我的示範StoreFront >我們>英文__ 頁面並按一下 __編輯__ 在頂端動作列中。

1. 在頂端動作列中，按一下 __檢視已發佈__，然後按一下店面導覽中任何偏好的類別。

1. 按一下中任何偏好的產品卡 __產品頁面__，然後選取 __顏色，大小__ 以啟用 __加入購物車__ 按鈕。


1. 開啟 __Adobe Experience Platform Debugger__ 從瀏覽器的擴充功能面板中選取擴充功能， __Experience Platform週三SDK__ 在左側邊欄中。

   ![AEP Debugger](../assets/aep-integration/AEP-Debugger.png)


1. 返回 __產品頁面__ 並按一下 __加入購物車__ 按鈕。 這會將資料傳送至Experience Platform。 此 __Adobe Experience Platform Debugger__ 擴充功能會顯示事件詳細資料。

   ![AEP Debugger Add-To-Cart事件資料](../assets/aep-integration/AEP-Debugger-AddToCart-EventData.png)



1. 在Experience Platform產品UI中，導覽至 __資料集>我的示範StoreFront__，位於 __資料集活動__ 標籤。 如果 __度量和圖表__ 切換功能已啟用，則會顯示事件資料統計資料。

   ![Experience Platform資料集資料統計資料](../assets/aep-integration/AEP-Dataset-AddToCart-EventData.png)



## 實作詳細資料 {#implementation-details}

此 [CIFExperience Platform聯結器](https://github.com/adobe/aem-core-cif-components/tree/master/extensions/experience-platform-connector) 建立在 [Adobe Commerce的Experience Platform聯結器](https://marketplace.magento.com/magento-experience-platform-connector.html)，這屬於 [PWA Studio](https://developer.adobe.com/commerce/pwa-studio/) 專案。

PWA Studio專案可讓您建立由Adobe Commerce或Magento Open Source提供支援的Progressive Web Application(PWA)店面。 專案也包含名為的元件庫 [Peregrin](https://developer.adobe.com/commerce/pwa-studio/api/peregrine/) 用於新增邏輯至視覺元件。 此 [Peregrin資料庫](https://developer.adobe.com/commerce/pwa-studio/api/peregrine/) 也會提供以下使用者使用的自訂React鉤點： [Experience Platform聯結器](https://github.com/adobe/aem-core-cif-components/tree/master/extensions/experience-platform-connector) 與Experience Platform緊密整合。


## 支持的事件 {#supported-events}

截至目前，支援下列事件：

__體驗XDM事件：__

1. 加入購物車(AEM)
1. 檢視頁面(AEM)
1. 檢視產品(AEM)
1. 搜尋要求已傳送(AEM)
1. 已收到搜尋回應(AEM)

時間 [Peregrine元件](https://developer.adobe.com/commerce/pwa-studio/guides/packages/peregrine/) 在AEM Commerce專案中重複使用：

__體驗XDM事件：__

1. 從購物車移除
1. 開啟購物車
1. 檢視購物車
1. 立即購買
1. 開始簽出
1. 完成結帳

__設定檔XDM事件：__

1. 登录
1. 创建帐户
1. 編輯帳戶


## 其他资源 {#additional-resources}

如需詳細資訊，請參閱下列資源：

- [PWA Studio](https://developer.adobe.com/commerce/pwa-studio/)
- [Experience Platform聯結器總覽](https://experienceleague.adobe.com/docs/commerce-merchant-services/experience-platform-connector/overview.html)
- [Experience Platform聯結器事件](https://experienceleague.adobe.com/docs/commerce-merchant-services/experience-platform-connector/event-forwarding/events.html)
- [Adobe Experience Platform概觀](https://experienceleague.adobe.com/docs/experience-platform/landing/home.html)
