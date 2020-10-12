---
title: 样式AEM CIF核心组件
description: 了解如何设计AEM CIF核心组件的样式。 本教程介绍如何使用客户端库或客户端库为Adobe Experience Manager(AEM)商务实施部署和管理CSS和Javascript。 本教程还将介绍如何将ui.frontend模块和Webpack项目集成到端到端构建过程中。
sub-product: 商务
topics: front-end-development
version: cloud-service
doc-type: tutorial
activity: develop
audience: developer
kt: 3456
thumbnail: 3456-style-cif.jpg
translation-type: tm+mt
source-git-commit: 1c518830f0bc9d9c7e6b11bebd6c0abd668ce040
workflow-type: tm+mt
source-wordcount: '2592'
ht-degree: 2%

---


# 样式AEM CIF核心组件 {#style-aem-cif-core-components}

CIF Venia [项目是](https://github.com/adobe/aem-cif-guides-venia) CIF核心组件使用的 [参考代码库](https://github.com/adobe/aem-core-cif-components)。 在本教程中，您将检查Venia参考项目并了解AEM CIF核心组件使用的CSS和JavaScript的组织方式。 您还将使用CSS创建新样式以更新产品Teaser组件的 **默认样式** 。

>[!TIP]
>
> 在启动您 [自己的商务实施](https://github.com/adobe/aem-project-archetype) 时，请使用AEM Project原型。

## 您将构建的内容

在本教程中，将为类似卡的产品Teaser组件实现新样式。 本教程中学到的经验教训可应用于其他CIF核心组件。

![您将构建的内容](../assets/style-cif-component/what-you-will-build.png)

## 前提条件 {#prerequisites}

需要本地开发环境才能完成本教程。 这包括配置并连接到Magento实例的AEM的运行实例。 查看将AEM作为Cloud ServiceSDK [设置本地开发的要求和步骤](../develop.md)。

## 克隆Venia项目 {#clone-venia-project}

我们将克隆 [Venia Project](https://github.com/adobe/aem-cif-guides-venia) ，然后覆盖默认样式。

>[!NOTE]
>
> **您可以随意使用现有项目** (基于包含CIF的AEM Project Archetype)并跳过本节。

1. 运行以下git命令以克隆项目：

   ```shell
   $ git clone git@github.com:adobe/aem-cif-guides-venia.git
   ```

1. 构建项目并将其部署到AEM的本地实例：

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallPackage,cloud
   ```

1. 添加必要的OSGi配置，将AEM实例连接到Magento实例，或将配置添加到新创建的项目。

1. 此时，您应具有连接到Magento实例的店面的工作版本。 导航到 `US` >页 `Home` 面： [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html)。

   您应当看到店面当前正在使用Venia主题。 展开店面的“主菜单”时，您应当看到各种类别，表明连接Magento正在工作。

   ![使用Venia主题配置的店面](../assets/style-cif-component/venia-store-configured.png)

## 客户端库和ui.frontend模块 {#introduction-to-client-libraries}

负责呈现店面主题／样式的CSS和JavaScript在AEM中由客户端库 [或clientlibs](/help/implementing/developing/introduction/clientlibs.md) 管理。 客户端库提供一种机制，用于在项目代码中组织CSS和Javascript，然后交付到页面上。

通过添加和覆盖由这些客户端库管理的CSS，品牌特定样式可应用于AEM CIF核心组件。 了解客户端库的结构和包含在页面上的方式至关重要。

ui. [frontend](https://docs.adobe.com/content/help/zh-Hans/experience-manager-core-components/using/developing/archetype/uifrontend.html) 是一个专用 [Webpack项](https://webpack.js.org/) 目，用于管理项目的所有前端资源。 这允许前端开发人员使用任何语言和技术，如 [TypeScript](https://www.typescriptlang.org/)[、Sass](https://sass-lang.com/) 等等。

该 `ui.frontend` 模块还是Maven模块，通过使用NPM模块aem-clientlib-generator与较 [大的项目集成](https://github.com/wcm-io-frontend/aem-clientlib-generator)。 在构建过程中， `aem-clientlib-generator` 编译后的CSS和JavaScript文件将复制到模块中的客户端 `ui.apps` 库中。

![ui.frontend ui.apps架构](../assets/style-cif-component/ui-frontend-architecture.png)

*在Maven构建过程中，编译的CSS `ui.frontend` 和Javascript `ui.apps` 将作为客户端库从模块复制到模块中*

## 更新Teaser样式 {#ui-frontend-module}

接下来，对Teaser样式做一些小更改，以了解模块和 `ui.frontend` clientlibraries的工作方式。 使 [用您选择的IDE](https://docs.adobe.com/content/help/en/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html#set-up-the-development-ide) ，导入Venia项目。 使用的截屏来自 [Visual Studio代码IDE](https://docs.adobe.com/content/help/en/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html#microsoft-visual-studio-code)。

1. 导航并展开 **ui.frontend模块** ，然后展开文件夹层次结构以： `ui.frontend/src/main/styles/commerce`:

   ![ui.frontend商务文件夹](../assets/style-cif-component/ui-frontend-commerce-folder.png)

   请注意，该文件夹下有`.scss`多个Sass()文件。 这些是每个商务组件的商务特定样式。

1. Open the file `_productteaser.scss`.

1. 更新规 `.item__image` 则并修改边框规则：

   ```scss
   .item__image {
       border: #ea00ff 8px solid; /* <-- modify this rule */
       display: block;
       grid-area: main;
       height: auto;
       opacity: 1;
       transition-duration: 512ms;
       transition-property: opacity, visibility;
       transition-timing-function: ease-out;
       visibility: visible;
       width: 100%;
   }
   ```

   上述规则应为产品Teaser组件添加一个非常粗体的粉红色边框。

1. 打开新的终端窗口并导航到文 `ui.frontend` 件夹：

   ```shell
   $ cd <project-location>/aem-cif-guides-venia/ui.frontend
   ```

1. 运行以下Maven命令：

   ```shell
   $ mvn clean install
   ...
   [INFO] ------------------------------------------------------------------------
   [INFO] BUILD SUCCESS
   [INFO] ------------------------------------------------------------------------
   [INFO] Total time:  29.497 s
   [INFO] Finished at: 2020-08-25T14:30:44-07:00
   [INFO] ------------------------------------------------------------------------
   ```

   Inspect终端输出。 您将看到Maven命令执行了包括在内的几个NPM脚本 `npm run build`。 该 `npm run build` 命令在文件中定 `package.json` 义，具有编译webpack项目和触发客户端库生成的效果。

1. Inspect `ui.frontend/dist/clientlib-site/site.css`:

   ![已编译站点CSS](../assets/style-cif-component/comiled-site-css.png)

   该文件是项目中所有Sass文件的编译和精简版本。

   >[!NOTE]
   >
   > 此类文件会从源代码控件中忽略，因为它们应在生成时生成。

1. Inspect `ui.frontend/clientlib.config.js`。

   ```js
   /* clientlib.config.js*/
   ...
   // Config for `aem-clientlib-generator`
   module.exports = {
       context: BUILD_DIR,
       clientLibRoot: CLIENTLIB_DIR,
       libs: [
           {
               ...libsBaseConfig,
               name: 'clientlib-site',
               categories: ['venia.site'],
               dependencies: ['venia.dependencies', 'aem-core-cif-react-components'],
               assets: {
   ...
   ```

   这是aem-clientlib-generator的配 [置文件](https://github.com/wcm-io-frontend/aem-clientlib-generator) ，它确定编译的CSS和JavaScript将在何处以及如何转换为AEM客户端库。

1. 在模块 `ui.apps` 中，检查文件： `ui.apps/src/main/content/jcr_root/apps/venia/clientlibs/clientlib-site/css/site.css`:

   ![ui.apps中的已编译站点CSS](../assets/style-cif-component/comiled-css-ui-apps.png)

   将复制的文 `site.css` 件复制到项 `ui.apps` 目中。 它现在是使用类别命名的 `clientlib-site` clientlibrary的一部分 `venia.site`。 文件成为模块的一 `ui.apps` 部分后，即可部署到AEM。

   >[!NOTE]
   >
   > 此类文件也会从源代码控件中忽略，因为它们应在生成时生成。

1. 接下来检查项目生成的其他客户端库：

   ![其他客户端库](../assets/style-cif-component/other-clientlibs.png)

   这些客户端库不由模块管 `ui.frontend` 理。 相反，这些客户端库包括由Adobe提供的CSS和JavaScript依赖关系。 这些clientlibraries的定义位于每个文件夹 `.content.xml` 下的文件中。

   **clientlib-base** —— 这是一个空的客户端库，它只嵌入AEM核心组件中必 [需的依赖项](https://docs.adobe.com/content/help/zh-Hans/experience-manager-core-components/using/introduction.html)。 类别是 `venia.base`。

   **clientlib-cif** —— 这也是一个空的客户端库，它只嵌入AEM CIF核心组件 [中必需的依赖项](https://github.com/adobe/aem-core-cif-components)。 类别是 `venia.cif`。

   **clientlib-grid** —— 这包括启用AEM响应式网格功能所需的CSS。 使用AEM网格可在AEM [编辑器中启](https://docs.adobe.com/content/help/en/experience-manager-65/administering/operations/configuring-responsive-layout.html#include-the-responsive-css) 用布局模式，并使内容作者能够重新调整组件大小。 类别已嵌 `venia.grid` 入库中，并已 `venia.base` 嵌入。

1. Inspect的文 `customheaderlibs.html` 件 `customfooterlibs.html` 和下面 `ui.apps/src/main/content/jcr_root/apps/venia/components/page`:

   ![自定义页眉和页脚脚本](../assets/style-cif-component/custom-header-footer-script.png)

   这些脚本 **包含venia** . **base和** venia.cif库，作为所有页面的一部分。

   >[!NOTE]
   >
   > 只有基库作为页面脚本的一部分被“硬编码”。 `venia.site` 不包含在这些文件中，而是作为页面模板的一部分提供，以获得更大的灵活性。 稍后会检查。

1. 从终端，构建整个项目并将其部署到AEM的本地实例：

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallPackage,cloud
   ```

## 创作产品Teaser {#author-product-teaser}

现在已部署代码更新，请使用AEM创作工具将产品Teaser组件的新实例添加到站点主页。 这将允许我们视图更新的样式。

1. 打开新的浏览器选项卡并导 **航到** 站点的主页: [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html)。

1. 在编辑模式下展开资产查找器(侧 **栏** )。 将资产过滤器切换 **为产品**。

   ![展开资产查找器并按产品进行筛选](../assets/style-cif-component/drag-drop-product-page.png)

1. 将新产品拖放到主布局主页中的容器上：

   ![带粉红色边框的产品Teaser](../assets/style-cif-component/pink-border-product-teaser.png)

   您应当看到产品Teaser现在有一个基于先前创建的CSS规则更改的粉红色亮边框。

## 验证页面上的客户端库 {#verify-client-libraries}

接下来，验证是否在页面中包含客户端库。

1. 导航到 **站点** 的主页: [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html)。

1. 选择“页 **面信息** ”菜单，然后单 **击“视图为已发布”**:

   ![查看已发布的项目](../assets/style-cif-component/view-as-published.png)

   此操作将打开页面，而不加载任何AEM作者javascript，就像它在已发布站点上一样。 请注意，url附加了查询 `?wcmmode=disabled` 参数。 在开发CSS和Javascript时，最好使用此参数来简化页面，而无需AEM作者提供的任何内容。

1. 视图页面源，您应该能够识别多个客户端库：

   ```html
   <!DOCTYPE html>
   <html lang="en-US">
   <head>
       ...
       <link rel="stylesheet" href="/etc.clientlibs/venia/clientlibs/clientlib-base.min.css" type="text/css">
       <link rel="stylesheet" href="/etc.clientlibs/venia/clientlibs/clientlib-site.min.css" type="text/css">
   </head>
   ...
       <script type="text/javascript" src="/etc.clientlibs/venia/clientlibs/clientlib-site.min.js"></script>
       <script type="text/javascript" src="/etc.clientlibs/core/wcm/components/commons/site/clientlibs/container.min.js"></script>
       <script type="text/javascript" src="/etc.clientlibs/venia/clientlibs/clientlib-base.min.js"></script>
   <script type="text/javascript" src="/etc.clientlibs/core/cif/clientlibs/common.min.js"></script>
   <script type="text/javascript" src="/etc.clientlibs/venia/clientlibs/clientlib-cif.min.js"></script>
   </body>
   </html>
   ```

   客户端库在传送到页面时带有前缀 `/etc.clientlibs` ，并通过代理提 [供](/help/implementing/developing/introduction/clientlibs.md) ，以避免暴露或中的任 `/apps` 何敏感 `/libs`内容。

   通知 `venia/clientlibs/clientlib-site.min.css` 和 `venia/clientlibs/clientlib-site.min.js`。 这些是从模块派生的编译的CSS和Javascript `ui.frontend` 文件。

## 包含页面模板的客户端库 {#client-library-inclusion-pagetemplates}

有关如何包含客户端库的方法有若干选项。 接下来，检查生成的项目如何通过页 `clientlib-site` 面模板 [包含库](https://docs.adobe.com/content/help/en/experience-manager-65/developing/platform/templates/page-templates-editable.html)。

1. 在AEM **Editor** 中导航到站点的主页: [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html)。

1. 选择“页 **面信息** ”菜单，然 **后单击编辑模板**:

   ![编辑模板](../assets/style-cif-component/edit-template.png)

   这将打开 **主页****所基** 于的登陆页模板。

   >[!NOTE]
   >
   > 要视图AEM开始屏幕中的所有可用模板，请导 **航到** “工具 **”** > **“常规**” > “模板”。

1. 在左上角，选择页面信息 **图标** ，然后单 **击页面策略**。

   ![页面策略菜单项](../assets/style-cif-component/page-policy-menu.png)

1. 这将打开登陆页模板的页面策略：

   ![页面策略-登陆页](../assets/style-cif-component/page-policy-properties.png)

   在右侧，您可以看到一个列表，其中列出了将 **包含** 在使用此模板的所有页面上的客户端库类别。

   * `venia.dependencies` -提供任何依赖的供 `venia.site` 应商库。
   * `venia.site` -这是模块生 `clientlib-site` 成的 `ui.frontend` 类别。

   请注意，其他模板使用相 **同的策略**、 **内容**&#x200B;页、登陆页等……通过重新使用同一策略，我们可以确保所有页面都包含相同的客户端库。

   使用“模板”和“页面”策略管理包含客户端库的好处在于，您可以根据模板更改策略。 例如，您可能正在管理同一AEM实例中的两个不同品牌。 每个品牌都有自己独特的风格 *或主题* ，但基本库和代码将相同。 另一个示例是，如果您有一个较大的客户端库，而它只想显示在某些页面上，则可以为该模板制定一个唯一的页面策略。

## 本地Webpack开发 {#local-webpack-development}

在上一个练习中，对模块中的Sass文件进行了更 `ui.frontend` 新，然后在执行Maven构建后，更改将部署到AEM。 接下来，我们将研究如何利用webpack-dev-server快速开发前端样式。

webpack-dev-server代理来自AEM本地实例的图像和某些CSS/JavaScript，但允许开发人员修改模块中的样式和JavaScript `ui.frontend` 。

1. 在浏览器中，导航到主 **页** ，并导 **航到已发布**: [http://localhost:4502/content/venia/us/en.html?wcmmode=disabled](http://localhost:4502/content/venia/us/en.html?wcmmode=disabled)。

1. 视图页面的源 **** ，并复制页面的原始HTML。

1. 在模块下返回您选择的IDE `ui.frontend` ，打开文件： `ui.frontend/src/main/static/index.html`

   ![静态HTML文件](../assets/style-cif-component/static-index-html.png)

1. 覆盖上一步 `index.html` 中 **复制** 的HTML的内容并粘贴。

1. 查找包含的内 `clientlib-site.min.css`容 `clientlib-site.min.js` 并 **删除** 。

   ```html
   <head>
       <!-- remove this link -->
       <link rel="stylesheet" href="/etc.clientlibs/venia/clientlibs/clientlib-base.min.css" type="text/css">
       ...
   </head>
   <body>
       ...
        <!-- remove this link -->
       <script type="text/javascript" src="/etc.clientlibs/venia/clientlibs/clientlib-site.min.js"></script>
   </body>
   ```

   删除这些组件，因为它们表示由模块生成的CSS和JavaScript的编译 `ui.frontend` 版本。 保留其他客户端库，就像它们将从运行的AEM实例中代理一样。

1. 打开新的终端窗口并导航到该文 `ui.frontend` 件夹。 运行命令 `npm start`:

   ```shell
   $ cd ui.frontend
   $ npm start
   ```

   这将在http://localhost:8080/上开始webpack-dev- [server](http://localhost:8080/)

   >[!CAUTION]
   >
   > 如果出现与Sass相关的错误，请停止服务器并运行该命令 `npm rebuild node-sass` 并重复上述步骤。 如果项目中指定了不同版本 `npm` 的 `node` 项目，则可能发生这种情况 `aem-cif-guides-venia/pom.xml`。

1. 使用与AEM [登录实例](http://localhost:8080/) 相同的浏览器，在新选项卡中导航到http://localhost:8080/。 您应通过webpack-dev-server看到Venia主页:

   ![端口80上的Webpack开发服务器](../assets/style-cif-component/webpack-dev-server-port80.png)

   使webpack-dev-server保持运行。 它将用于下一个练习。

## 为产品Teaser实施卡样式 {#update-css-product-teaser}

接下来，修改模块中 `ui.frontend` 的Sass文件，为Product Teaser实现类似卡的样式。 webpack-dev-server将用于快速查看更改。

返回到IDE和生成的项目。

1. 在ui. **frontend** 模块中，重新打开位 `_productteaser.scss` 于的文件 `ui.frontend/src/main/styles/commerce/_productteaser.scss`。

1. 对产品Teaser边框进行以下更改：

   ```diff
       .item__image {
   -       border: #ea00ff 8px solid;
   +       border-bottom: 1px solid #c0c0c0;
           display: block;
           grid-area: main;
           height: auto;
           opacity: 1;
           transition-duration: 512ms;
           transition-property: opacity, visibility;
           transition-timing-function: ease-out;
           visibility: visible;
           width: 100%;
       }
   ```

   保存更改，webpack-dev-server应使用新样式自动刷新。

1. 添加投影并在产品Teaser中包含圆角。

   ```scss
    .item__root {
        position: relative;
        box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);
        transition: 0.3s;
        border-radius: 5px;
        float: left;
        margin-left: 12px;
        margin-right: 12px;
   }
   
   .item__root:hover {
      box-shadow: 0 8px 16px 0 rgba(0,0,0,0.2);
   }
   ```

1. 更新产品名称以显示在Teaser的底部并修改文本颜色。

   ```css
   .item__name {
       color: #000;
       display: block;
       float: left;
       font-size: 22px;
       font-weight: 900;
       line-height: 1em;
       padding: 0.75em;
       text-transform: uppercase;
       width: 75%;
   }
   ```

1. 更新产品的价格，使其也显示在Teaser的底部并修改文本颜色。

   ```css
   .price {
       color: #000;
       display: block;
       float: left;
       font-size: 18px;
       font-weight: 900;
       padding: 0.75em;
       padding-bottom: 2em;
       width: 25%;
   
       ...
   ```

1. 更新底部的媒体查询，以在小于992px的屏幕中堆叠名称和 **价格**。

   ```css
   @media (max-width: 992px) {
       .productteaser .item__name {
           font-size: 18px;
           width: 100%;
       }
       .productteaser .item__price {
           font-size: 14px;
           width: 100%;
       }
   }
   ```

   您现在应当看到webpack-dev-server中反映的卡样式：

   ![Webpack Dev ServerTeaser更改](../assets/style-cif-component/webpack-dev-server-teaser-changes.png)

   但是，更改尚未部署到AEM。 您可以在此处下 [载解决方案文件](../assets/style-cif-component/_productteaser.scss)。

1. 使用Maven技能从命令行终端部署更新至AEM:

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallPackage,cloud
   ```

   >[!NOTE]
   >还有其他IDE [设置和工具](https://docs.adobe.com/content/help/en/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html#set-up-an-integrated-development-environment) ，它们可以将项目文件直接同步到本地AEM实例，而无需执行完全的Maven生成。

## 视图更新的产品Teaser {#view-updated-product-teaser}

项目的代码部署到AEM后，我们现在应该能够看到对产品Teaser的更改。

1. 返回浏览器并重新刷新主页: [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html)。 您应看到已应用更新的产品Teaser样式。

   ![更新的产品Teaser样式](../assets/style-cif-component/product-teaser-new-style.png)

1. 通过添加其他产品Teaser进行试验。 使用布局模式更改组件的宽度和偏移，以在一行中显示多个Teaser。

   ![多个产品Teaser](../assets/style-cif-component/multiple-teasers-final.png)

## 疑难解答 {#troubleshooting}

您可以在CRXDE- [Lite中验证](http://localhost:4502/crx/de/index.jsp) ，已部署更新的CSS文件： [http://localhost:4502/crx/de/index.jsp#/apps/venia/clientlibs/clientlib-site/css/site.css](http://localhost:4502/crx/de/index.jsp#/apps/venia/clientlibs/clientlib-site/css/site.css)

部署新的CSS和／或JavaScript文件时，确保浏览器不提供旧文件也很重要。 您可以通过清除浏览器缓存或启动新的浏览器会话来消除这种情况。

AEM还尝试缓存客户端库以提高性能。 偶尔，在代码部署之后，会提供旧文件。 您可以使用“重新构建客户端库”工具手动使AEM [客户端库缓存失效](http://localhost:4502/libs/granite/ui/content/dumplibs.rebuild.html)。 *如果您怀疑AEM已缓存客户端库的旧版本，则首选使用Invalidate Caches方法。 重新构建库效率低下且耗时。*

## 恭喜 {#congratulations}

您刚设置了第一个AEM CIF核心组件的样式，并且使用了webpack开发服务器！

## 奖金挑战 {#bonus-challenge}

使用AEM [样式系统](https://docs.adobe.com/content/help/en/experience-manager-65/developing/components/style-system.html) ，创建可由内容作者打开／关闭的两种样式。 [使用样式系统进行开发](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-wknd-tutorial-develop/style-system.html) ，包括如何实现该功能的详细步骤和信息。

![奖金挑战——风格系统](../assets/style-cif-component/bonus-challenge.png)

## 其他资源 {#additional-resources}

* [AEM 项目原型](https://github.com/adobe/aem-project-archetype)
* [AEM CIF核心组件](https://github.com/adobe/aem-core-cif-components)
* [设置本地AEM开发环境](https://docs.adobe.com/content/help/en/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html)
* [客户端库](/help/implementing/developing/introduction/clientlibs.md)
* [AEM Sites入门](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html)
* [以风格体系发展](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-wknd-tutorial-develop/style-system.html)
