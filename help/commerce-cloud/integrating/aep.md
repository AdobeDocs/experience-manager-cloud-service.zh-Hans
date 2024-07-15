---
title: AEM-CIF核心组件与Adobe Experience Platform集成
description: 了解如何使用CIF - Storefront Connector将AEM渲染的产品Experience Platform中的storefront事件数据发送到Experience Platform。
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
source-git-commit: bae9a5178c025b3bafa8ac2da75a1203206c16e1
workflow-type: tm+mt
source-wordcount: '1866'
ht-degree: 1%

---


# AEM-CIF核心组件与Adobe Experience Platform集成 {#aem-cif-aep-integration}

[Commerce integration framework(CIF)](https://github.com/adobe/aem-core-cif-components)核心组件提供与[Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-overview.html?lang=en)的无缝集成，以便从客户端交互（如&#x200B;__添加到购物车__）转发店面事件及其数据。

[AEM CIF核心组件](https://github.com/adobe/aem-core-cif-components)项目提供了一个名为[Adobe Experience Platform connector for Adobe Commerce](https://github.com/adobe/aem-core-cif-components/tree/master/extensions/experience-platform-connector)的JavaScript库，用于从Commerce店面收集事件数据。 该事件数据会被发送到Experience Platform，并在其他Adobe Experience Cloud产品(如Adobe Analytics和Adobe Target)中使用，以构建涵盖客户历程的360度个人资料。 通过将Commerce数据连接到Adobe Experience Cloud中的其他产品，您可以执行分析网站上的用户行为、执行AB测试以及创建个性化营销活动等任务。

了解有关[Experience Platform数据收集](https://experienceleague.adobe.com/docs/experience-platform/collection/home.html)套技术的更多信息，这些技术允许您从客户端源收集客户体验数据。

## 将`addToCart`事件数据发送到Experience Platform {#send-addtocart-to-aep}

以下步骤显示了如何使用CIF - Event Connector将`addToCart`事件数据从AEM渲染的产品Experience Platform发送到Experience Platform。 通过使用Adobe Experience Platform Debugger浏览器扩展，您可以测试和查看提交的数据。

![查看Adobe Experience Platform Debugger](../assets/aep-integration/EventData-AEM-AEP.png)中的addToCart事件数据

## 先决条件 {#prerequisites}

使用本地开发环境完成此演示。 这包括正在运行的AEM实例，该实例已配置并连接到Adobe Commerce实例。 查看[使用AEM as a Cloud Service SDK设置本地开发的要求和步骤](../develop.md)。

您还需要访问[Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-ui/ui-guide.html)和权限以创建用于数据收集的架构、数据集和数据流。 有关详细信息，请参阅[权限管理](https://experienceleague.adobe.com/docs/experience-platform/collection/permissions.html)。

## AEM Commerceas a Cloud Service设置 {#aem-setup}

要使具有必要代码和配置的工作中&#x200B;__AEM Commerceas a Cloud Service__&#x200B;本地环境，请完成以下步骤。

### 本地设置

执行[本地设置](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/content-and-commerce/storefront/developing/develop.html?#local-setup)步骤，以便您可以拥有一个有效的AEM Commerceas a Cloud Service环境。

### 项目设置

执行[AEM项目原型](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/content-and-commerce/storefront/developing/develop.html?#project)步骤，以便创建全新的AEM Commerce (CIF)项目。

>[!TIP]
>
>在以下示例中，AEM Commerce项目名为： `My Demo Storefront`，但您可以选择自己的项目名称。

![AEM Commerce项目](../assets/aep-integration/aem-project-with-commerce.png)


通过从项目的根目录运行以下命令，生成已创建的AEM Commerce项目并将其部署到本地AEM SDK。

```bash
$ mvn clean install -PautoInstallSinglePackage
```

本地部署的`My Demo StoreFront`商业网站具有默认代码和内容，如下所示：

![默认AEM Commerce站点](../assets/aep-integration/demo-aem-storefront.png)

### 安装Peregrine和CIF-AEP连接器依赖项

要从此AEM Commerce站点的类别和产品页面收集事件数据并将其发送，请将密钥`npm`包安装到AEM Commerce项目的`ui.frontend`模块中。

导航到`ui.frontend`模块，并通过从命令行运行以下命令来安装所需的包。

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
>`--force`参数有时是必需的，因为[PWA Studio](https://developer.adobe.com/commerce/pwa-studio/)对支持的对等依赖项进行了限制。 通常，这应该不会导致任何问题。


### 配置Maven以使用`--force`参数

在Maven构建过程中，会触发npm全新安装（使用`npm ci`）。 这还需要`--force`参数。

导航到项目的根POM文件`pom.xml`并找到`<id>npm ci</id>`执行块。 更新块，使其类似于以下内容：

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

### 更改Babel配置格式

从默认的`.babelrc`文件相对配置文件格式切换为`babel.config.js`格式。 这是项目范围的配置格式，允许将插件和预设应用于具有较大控制权的`node_module`。

1. 导航到`ui.frontend`模块并删除现有`.babelrc`文件。

1. 创建使用`peregrine`预设的`babel.config.js`文件。

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

### 配置webpack以使用Babel

要使用Babel加载器(`babel-loader`)和Webpack传输JavaScript文件，请编辑`webpack.common.js`文件。

导航到`ui.frontend`模块并更新`webpack.common.js`文件，以便您可以在`module`属性值内使用以下规则：

```javascript
{
    test: /\.jsx?$/,
    exclude: /node_modules\/(?!@magento\/)/,
    loader: 'babel-loader'
}
```

### 配置Apollo客户端

[Apollo客户端](https://www.apollographql.com/docs/react/)用于通过GraphQL管理本地和远程数据。 它还会将GraphQL查询的结果存储在本地的规范化内存缓存中。

为了使[`InMemoryCache`](https://www.apollographql.com/docs/react/caching/cache-configuration/)有效工作，您需要一个`possibleTypes.js`文件。 要生成此文件，请参阅[自动生成possibleTypes](https://www.apollographql.com/docs/react/data/fragments/#generating-possibletypes-automatically)。 另请参阅[PWA Studio引用实现](https://github.com/magento/pwa-studio/blob/1977f38305ff6c0e2b23a9da7beb0b2f69758bed/packages/pwa-buildpack/lib/Utilities/graphQL.js#L106-L120)和[`possibleTypes.js`](../assets/aep-integration/possibleTypes.js)文件的示例。


1. 导航到`ui.frontend`模块并将文件另存为`./src/main/possibleTypes.js`

1. 更新`webpack.common.js`文件的`DefinePlugin`部分，以便在生成期间替换所需的静态变量。

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

### 初始化Peregrine和CIF核心组件

要初始化基于React的Peregrine和CIF核心组件，请创建所需的配置和JavaScript文件。

1. 导航到`ui.frontend`模块并创建以下文件夹： `src/main/webpack/components/commerce/App`

1. 创建包含以下内容的`config.js`文件：

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
           eventForwarding: {
               acds: true,
               aep: false,
           }
       }
   };
   ```

   >[!IMPORTANT]
   >
   >您可能已经熟悉&#x200B;__AEM Guides - CIF Venia项目__&#x200B;中的[`config.js`](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.frontend/src/main/components/App/config.js)文件，但必须对此文件进行一些更改。 首先，查看任何&#x200B;__TODO__&#x200B;备注。 然后，在`eventsCollector`属性内，查找`eventsCollector > aep`对象并将`orgId`和`datastreamId`属性更新为正确的值。 [了解详情](./aep.md#add-aep-values-to-aem)。

1. 创建包含以下内容的`App.js`文件。 此文件类似于典型的React应用程序起点文件，包含React和自定义挂接以及React Context用法，可促进Experience Platform集成。

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
           // implement a proper marketing opt-in, for demo purpose you hard-set the consent cookie
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

   `EventCollectorContext`导出React上下文，其中：

   - 加载commerce-events-sdk和commerce-events-collector库，
   - 使用给定的Experience Platform和/或ACDS配置初始化它们
   - 订阅来自Peregrine的所有事件并将它们转发到事件SDK

   您可以在[此处](https://github.com/adobe/aem-core-cif-components/blob/3d4e44d81fff2f398fd2376d24f7b7019f20b31b/extensions/experience-platform-connector/src/events-collector/EventCollectorContext.js)查看`EventCollectorContext`的实施详细信息。

### 生成和部署更新的AEM项目

要确保上述软件包安装、代码和配置更改正确，请使用以下Maven命令重新生成和部署更新的AEM Commerce项目： `$ mvn clean install -PautoInstallSinglePackage`。

## Experience Platform设置 {#aep-setup}

要接收并存储来自AEM Commerce页面（如类别和产品）的事件数据，请完成以下步骤：

>[!AVAILABILITY]
>
>确保您属于&#x200B;__Adobe Experience Platform__&#x200B;和&#x200B;__Adobe Experience Platform数据收集__&#x200B;下的正确&#x200B;__产品配置文件__。 如果需要，请与系统管理员合作创建、更新或分配[Admin Console](https://adminconsole.adobe.com/)下的&#x200B;__产品配置文件__。

### 使用Commerce字段组创建架构

要定义商务事件数据的结构，您必须创建体验数据模型(XDM)架构。 架构是一组规则，用于表示和验证数据的结构和格式。

1. 在浏览器中，导航到&#x200B;__Adobe Experience Platform__&#x200B;产品主页。 例如：<https://experience.adobe.com/#/@YOUR-ORG-NAME/sname:prod/platform/home>。

1. 在左侧导航部分找到&#x200B;__架构__&#x200B;菜单，单击右上角的&#x200B;__创建架构__&#x200B;按钮，然后选择&#x200B;__XDM ExperienceEvent__。

   ![AEP创建架构](../assets/aep-integration/AEP-Schema-EventSchema-1.png)

1. 使用&#x200B;__架构属性>显示名称__&#x200B;字段命名您的架构，并使用&#x200B;__组合>字段组>添加__&#x200B;按钮添加字段组。

   ![AEP架构定义](../assets/aep-integration/AEP-Schema-Definition.png)

1. 在&#x200B;__添加字段组__&#x200B;对话框中，搜索`Commerce`，选中&#x200B;__Commerce详细信息__&#x200B;复选框，然后单击&#x200B;__添加字段组__。

   ![AEP架构定义](../assets/aep-integration/AEP-Schema-Field-Group.png)


>[!TIP]
>
>有关详细信息，请参阅架构组合](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html)的[基础知识。

### 创建数据集

要存储事件数据，您必须创建符合架构定义的数据集。 数据集是用于数据集合的存储和管理结构，通常是包含架构（列）和字段（行）的表。

1. 在浏览器中，导航到&#x200B;__Adobe Experience Platform__&#x200B;产品主页。 例如：<https://experience.adobe.com/#/@YOUR-ORG-NAME/sname:prod/platform/home>。

1. 在左侧导航部分中找到&#x200B;__数据集__&#x200B;菜单，然后单击右上角部分的&#x200B;__创建数据集__&#x200B;按钮。

   ![AEP创建数据集](../assets/aep-integration/AEP-Datasets-Create.png)

1. 在新页面上，选择&#x200B;__从架构__&#x200B;信息卡创建数据集。

   ![AEP创建数据集架构选项](../assets/aep-integration/AEP-Datasets-Schema-Option.png)

   在新页面上，__搜索并选择__&#x200B;您在上一步中创建的架构，然后单击&#x200B;__下一步__&#x200B;按钮。

   ![AEP创建数据集选择架构](../assets/aep-integration/AEP-Datasets-Select-Schema.png)

1. 使用&#x200B;__配置数据集>名称__&#x200B;字段命名您的数据集，然后单击&#x200B;__完成__&#x200B;按钮。

   ![AEP创建数据集名称](../assets/aep-integration/AEP-Datasets-Name.png)

>[!TIP]
>
>有关详细信息，请参阅[数据集概述](https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/overview.html)。


### 创建数据流

完成以下步骤，以便在Experience Platform中创建数据流。

1. 在浏览器中，导航到&#x200B;__Adobe Experience Platform__&#x200B;产品主页。 例如：<https://experience.adobe.com/#/@YOUR-ORG-NAME/sname:prod/platform/home>。

1. 在左侧导航部分中找到&#x200B;__数据流__&#x200B;菜单，然后单击右上角部分的&#x200B;__新建数据流__&#x200B;按钮。

   ![AEP创建数据流](../assets/aep-integration/AEP-Datastream-Create.png)

1. 使用&#x200B;__Name__&#x200B;必填字段命名您的数据流。 在&#x200B;__事件架构__&#x200B;字段下，选择已创建的架构，然后单击&#x200B;__保存__。

   ![AEP定义数据流](../assets/aep-integration/AEP-Datastream-Define.png)

1. 打开创建的数据流，然后单击&#x200B;__添加服务__。

   ![AEP数据流添加服务](../assets/aep-integration/AEP-Datastream-Add-Service.png)

1. 在&#x200B;__服务__&#x200B;字段下，选择&#x200B;__Adobe Experience Platform__&#x200B;选项。 在&#x200B;__事件数据集__&#x200B;字段下，从上一步中选择数据集名称，然后单击&#x200B;__保存__。

   ![AEP数据流添加服务详细信息](../assets/aep-integration/AEP-Datastream-Add-Service-Define.png)

>[!TIP]
>
>有关详细信息，请参阅[数据流概述](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html)。

## 将数据流值添加到AEM Commerce配置 {#add-aep-values-to-aem}

完成上述Experience Platform设置后，数据流详细信息的左边栏中应该有`datastreamId`，在&#x200B;__配置文件图片>帐户信息>用户信息__&#x200B;模式窗口的右上角应该有`orgId`。

![AEP数据流ID](../assets/aep-integration/AEP-Datastream-ID.png)

1. 在AEM Commerce项目的`ui.frontend`模块中，更新`config.js`文件并具体更新`eventsCollector > aep`对象属性。

1. 生成和部署更新的AEM Commerce项目


## 触发`addToCart`事件并验证数据收集 {#event-trigger-verify}

上述步骤将完成AEM Commerce和Experience Platform设置。 您现在可以在产品UI中使用Google Chrome扩展&#x200B;_雪铲检查器_&#x200B;和数据集&#x200B;__量度和图形__&#x200B;切换触发`addToCart`事件并验证数据收集。

要触发该事件，您可以从本地设置使用AEM创作或发布服务。 对于此示例，请通过登录到您的帐户来使用AEM author。

1. 从Sites页面中，选择&#x200B;__我的演示StoreFront >我们> en__&#x200B;页面，然后单击顶部操作栏中的&#x200B;__编辑__。

1. 在顶部操作栏中，单击&#x200B;__以发布的形式查看__，然后单击店面导航中的任意首选类别。

1. 单击&#x200B;__产品页__&#x200B;中任何首选的产品卡，然后选择&#x200B;__颜色，大小__&#x200B;以启用&#x200B;__添加到购物车__&#x200B;按钮。


1. 从浏览器的扩展面板中打开&#x200B;__Snowplow Inspector__&#x200B;扩展，然后在左边栏中选择&#x200B;__Experience PlatformWed SDK__。


1. 返回&#x200B;__产品页__&#x200B;并单击&#x200B;__添加到购物车__&#x200B;按钮。 这会向Experience Platform发送数据。 __Adobe Experience Platform Debugger__&#x200B;扩展显示事件详细信息。

   ![AEP调试器添加到购物车事件数据](../assets/aep-integration/AEP-Debugger-AddToCart-EventData.png)



1. 在Experience Platform产品UI中的&#x200B;__数据集活动__&#x200B;选项卡下，导航到&#x200B;__数据集> My Demo StoreFront__。 如果启用了&#x200B;__量度和图形__，则会显示事件数据统计信息。

   ![Experience Platform的数据集数据统计信息](../assets/aep-integration/AEP-Dataset-AddToCart-EventData.png)



## 实施详细信息 {#implementation-details}

[CIFExperience Platform连接器](https://github.com/adobe/aem-core-cif-components/tree/master/extensions/experience-platform-connector)构建在Adobe Commerce](https://commercemarketplace.adobe.com/magento-experience-platform-connector.html)的[数据连接之上，它是[PWA Studio](https://developer.adobe.com/commerce/pwa-studio/)项目的一部分。

PWA Studio项目允许您创建由Adobe Commerce或Magento Open Source提供支持的Progressive Web Application(PWA)店面。 该项目还包含一个名为[Peregrin](https://developer.adobe.com/commerce/pwa-studio/api/peregrine/)的组件库，用于向可视化组件添加逻辑。 [Peregrin库](https://developer.adobe.com/commerce/pwa-studio/api/peregrine/)还提供了[CIFExperience Platform连接器](https://github.com/adobe/aem-core-cif-components/tree/master/extensions/experience-platform-connector)用于与Experience Platform无缝集成的自定义React挂接。


## 支持的事件 {#supported-events}

截至目前，支持以下事件：

__体验XDM事件：__

1. 添加到购物车(AEM)
1. 查看页面(AEM)
1. 查看产品(AEM)
1. 已发送搜索请求(AEM)
1. 已收到搜索响应(AEM)

在AEM Commerce项目中重用[Peregrine组件](https://developer.adobe.com/commerce/pwa-studio/guides/packages/peregrine/)时：

__体验XDM事件：__

1. 从购物车中移除
1. 打开购物车
1. 查看购物车
1. 即时购买
1. 开始结帐
1. 完成签出

__配置文件XDM事件：__

1. 登录
1. 创建帐户
1. 编辑帐户


## 其他资源 {#additional-resources}

有关更多信息，请参阅以下资源：

- [PWA Studio](https://developer.adobe.com/commerce/pwa-studio/)
- [[!DNL Data Connection] 概述](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/overview.html)
- [[!DNL Data Connection] 个事件](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/event-forwarding/events.html)
- [Adobe Experience Platform概述](https://experienceleague.adobe.com/docs/experience-platform/landing/home.html)
