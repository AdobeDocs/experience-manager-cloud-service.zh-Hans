---
title: 自定义CIF核心组件
description: 了解如何自定义AEM CIF核心组件。 本教程介绍如何安全扩展CIF核心组件以满足业务特定要求。 了解如何扩展GraphQL查询以返回自定义属性并在CIF核心组件中显示新属性。
sub-product: 商务
topics: development
version: cloud-service
doc-type: tutorial
activity: develop
audience: developer
kt: 4279
thumbnail: 4279-customize-cif.jpg
translation-type: tm+mt
source-git-commit: 34b4dc697d3fb8c3f81e16ee3cab5d768e42b99c
workflow-type: tm+mt
source-wordcount: '2550'
ht-degree: 1%

---


# 自定义AEM CIF核心组件 {#customize-cif-components}

CIF Venia [项目是](https://github.com/adobe/aem-cif-guides-venia) CIF核心组件使用的 [参考代码库](https://github.com/adobe/aem-core-cif-components)。 在本教程中，您将进一步扩展 [产品Teaser组件](https://github.com/adobe/aem-core-cif-components/tree/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/productteaser/v1/productteaser) ，以显示来自Magento的自定义属性。 您还将进一步了解AEM和Magento之间的GraphQL集成以及CIF核心组件提供的扩展挂钩。

>[!TIP]
>
> 在启动您 [自己的商务实施](https://github.com/adobe/aem-project-archetype) 时，请使用AEM Project原型。

## 您将构建的内容

韦尼亚品牌最近开始使用可持续材料生产一些产品，该企业希望展示 **Eco Friendly** 徽章作为产品Teaser的一部分。 将在Magento中创建新的自定义属性，以指示产品是否使用 **Eco友好** 材料。 此自定义属性随后将添加为GraphQL查询的一部分，并显示在指定产品的产品Teaser上。

![生态友好徽章最终实施](../assets/customize-cif-components/final-product-teaser-eco-badge.png)

## 前提条件 {#prerequisites}

需要本地开发环境才能完成本教程。 这包括配置并连接到Magento实例的AEM的运行实例。 查看将AEM作为Cloud ServiceSDK [设置本地开发的要求和步骤](../develop.md)。 要完全学习本教程，您需要权限才能在Magento [中向产品添加](https://docs.magento.com/user-guide/catalog/product-attributes-add.html) “属性”。

您还需要GraphQL IDE(如 [GraphiQL](https://github.com/graphql/graphiql) )或浏览器扩展才能运行代码示例和教程。 如果安装浏览器扩展，请确保它能够设置请求标头。 在Google Chrome上， [Altair GraphQL Client](https://chrome.google.com/webstore/detail/altair-graphql-client/flnheeellpciglgpaodhkhmapeljopja) （Altair GraphQL客户端）是可以完成该工作的扩展之一。

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

   ![使用Venia主题配置的店面](../assets/customize-cif-components/venia-store-configured.png)

## 创作产品Teaser {#author-product-teaser}

产品Teaser组件将在本教程中进行扩展。 首先，将产品Teaser的新实例添加到主页以了解基线功能。

1. 导航到 **站点** 的主页: [http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html)

2. 将新的产 **品Teaser** 组件插入页面的主布局容器。

   ![插入产品Teaser](../assets/customize-cif-components/product-teaser-add-component.png)

3. 展开侧面板（如果尚未切换），并将资产查找器下拉列表切换到 **产品**。 这应显示连接列表实例中可用产品的Magento。 选择一个产品 **并将其拖放** 到页面 **上的产品Teaser** 组件上。

   ![拖放产品Teaser](../assets/customize-cif-components/drag-drop-product-teaser.png)

   >[!NOTE]
   >
   > 注意，您还可以通过使用对话框配置组件（单击扳手图标）来配 *置显* 示的产品。

4. 您现在应当看到产品Teaser正在显示产品。 产品名称和产品价格是显示的默认属性。

   ![产品Teaser —— 默认样式](../assets/customize-cif-components/product-teaser-default-style.png)

## 在Magento中添加自定义属性 {#add-custom-attribute}

AEM中显示的产品和产品数据以Magento存储。 接下来，使用Magento **UI** ，将Eco Friendly的新属性添加为产品属性集的一部分。

>[!TIP]
>
> 是否已经有自 **定义“是** /否”属性作为产品属性集的一部分？ 请随时使用它并跳过此部分。

1. 登录Magento实例。
1. 导航到 **目录** > **产品**。
1. 更新搜索筛选器以查找在 **上一练习** 中添加到Teaser组件时使用的可配置产品。 在编辑模式下打开产品。

   ![搜索Valeria产品](../assets/customize-cif-components/search-valeria-product.png)

1. 在产品视图中，单 **击添加属性** > **创建新属性**。
1. 使用以下 **值填写** “新建属性”表单（保留其他值的默认设置）

   | 字段集 | 字段标签 | 值 |
   |-----------|-------------|---------|
   | 属性属性 | 属性标签 | **生态友好** |
   | 属性属性 | 目录输入类型 | **是／否** |
   | 高级属性 | 属性代码 | **eco_friendly** |

   ![新属性表单](../assets/customize-cif-components/attribute-new-form.png)

   完成 **后单击** “保存属性”。

1. 滚动到产品底部并展开“属 **性** ”标题。 您应该看到新的“生 **态友好** ”字段。 将切换切换切换为 **是**。

   ![切换为“是”](../assets/customize-cif-components/eco-friendly-toggle-yes.png)

   **保存** 对产品所做的更改。

   >[!TIP]
   >
   > 有关管理产品属 [性的更多详细信息，请参阅Magento用户指南](https://docs.magento.com/user-guide/catalog/attribute-best-practices.html)。

1. 导航到 **“系统** ”>“工 **具** ” **>“缓**&#x200B;存管理”。 由于对模式进行了更新，因此我们需要使Magento中的某些缓存类型失效。
1. 选中“配置”旁 **的框** ，并提交“刷新”的缓存类 **型**

   ![刷新配置缓存类型](../assets/customize-cif-components/refresh-configuration-cache-type.png)

   >[!TIP]
   >
   > 有关缓存管 [理的更多详细信息，请参阅Magento用户指南](https://docs.magento.com/user-guide/system/cache-management.html)。

## 使用GraphQL IDE验证属性 {#use-graphql-ide}

在跳转到AEM代码之前，使用GraphQL IDE [浏览MagentoGraph](https://devdocs.magento.com/guides/v2.4/graphql/) QL很有用。 与AEM的Magento集成主要通过一系列GraphQL查询完成。 了解和修改GraphQL查询是扩展CIF核心组件的关键方法之一。

然后，使用GraphQL IDE验证属性 `eco_friendly` 是否已添加到产品属性集。 本教程中的屏幕截图使用 [Altair GraphQL客户端](https://chrome.google.com/webstore/detail/altair-graphql-client/flnheeellpciglgpaodhkhmapeljopja)。

1. 打开GraphQL IDE，在IDE `http://<magento-server>/graphql` 或扩展的URL栏中输入URL。
2. 添加以 [下产品查询](https://devdocs.magento.com/guides/v2.4/graphql/queries/products.html) , `YOUR_SKU` 其中 **是上** 一练习中使用的产品的SKU:

   ```json
     {
       products(
       filter: { sku: { eq: "YOUR_SKU" } }
       ) {
           items {
           name
           sku
           eco_friendly
           }
       }
   }
   ```

3. 执行查询，您应得到如下响应：

   ```json
   {
   "data": {
       "products": {
           "items": [
               {
               "name": "Valeria Two-Layer Tank",
               "sku": "VT11",
               "eco_friendly": 1
               }
           ]
           }
       }
   }
   ```

   ![示例GraphlQL响应](../assets/customize-cif-components/sample-graphql-query.png)

   请注意，“是 **”的** 值是整数 **1**。 当我们使用Java编写GraphQL查询时，这将很有用。

   >[!TIP]
   >
   > 有关Magento图QL的 [更多详细文档，请参阅此处](https://devdocs.magento.com/guides/v2.4/graphql/index.html)。

## 更新产品Teaser的Sling模型 {#updating-sling-model-product-teaser}

接下来，我们将通过实施Sling模型来扩展产品Teaser的业务逻辑。 [Sling Models](https://sling.apache.org/documentation/bundles/models.html)是注释驱动的“POJO”(Plain Old Java Objects)，可实现组件所需的任何业务逻辑。 Sling Models与HTL脚本结合使用，作为组件的一部分。 我们将遵循Sling [模型的委托模式](https://github.com/adobe/aem-core-wcm-components/wiki/Delegation-Pattern-for-Sling-Models) ，这样我们只需扩展现有产品Teaser模型的部分。

Sling Models是作为Java实现的，可在生成项 **目的** 核心模块中找到。

使 [用您选择的IDE](https://docs.adobe.com/content/help/en/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html#set-up-the-development-ide) ，导入Venia项目。 使用的截屏来自 [Visual Studio代码IDE](https://docs.adobe.com/content/help/en/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html#microsoft-visual-studio-code)。

1. 在IDE中，在核心模块 **下导** 航到： `core/src/main/java/com/venia/core/models/commerce/MyProductTeaser.java`.

   ![核心位置IDE](../assets/customize-cif-components/core-location-ide.png)

   `MyProductTeaser.java` 是扩展CIF ProductTeaser界面的 [Java界面](https://github.com/adobe/aem-core-cif-components/blob/master/bundles/core/src/main/java/com/adobe/cq/commerce/core/components/models/productteaser/ProductTeaser.java) 。

   如果产品被视为“新”, `isShowBadge()` 则已添加一个名为的新方法来显示徽章。

1. 向接口中添加 `isEcoFriendly()` 新方法：

   ```java
   @ProviderType
   public interface MyProductTeaser extends ProductTeaser {
       // Extend the existing interface with the additional properties which you
       // want to expose to the HTL template.
       public Boolean isShowBadge();
   
       public Boolean isEcoFriendly();
   }
   ```

   这是我们将引入的一种新方法，用于封装逻辑以指示产品的属 `eco_friendly` 性是否设置 **为** “是” **或“否”**。

1. 接下来，检查 `MyProductTeaserImpl.java` 位 `core/src/main/java/com/venia/core/models/commerce/MyProductTeaserImpl.java`置。

   Sling Models [的委托模式](https://github.com/adobe/aem-core-wcm-components/wiki/Delegation-Pattern-for-Sling-Models)`MyProductTeaserImpl` 允许通 `ProductTeaser` 过以下属性引 `sling:resourceSuperType` 用模型：

   ```java
   @Self
   @Via(type = ResourceSuperType.class)
   private ProductTeaser productTeaser;
   ```

   对于我们不想覆盖或更改的所有方法，我们只需返回返回返回的 `ProductTeaser` 值。 例如：

   ```java
   @Override
   public String getImage() {
       return productTeaser.getImage();
   }
   ```

   这将最小化实现需要写入的Java代码量。

1. AEM CIF核心组件提供的额外扩展点之一是 `AbstractProductRetriever` 提供对特定产品属性的访问。 Inspect `initModel()` 的方法：

   ```java
   import javax.annotation.PostConstruct;
   ...
   @Model(adaptables = SlingHttpServletRequest.class, adapters = MyProductTeaser.class, resourceType = MyProductTeaserImpl.RESOURCE_TYPE)
   public class MyProductTeaserImpl implements MyProductTeaser {
       ...
       private AbstractProductRetriever productRetriever;
   
       /* add this method to intialize the proudctRetriever */
       @PostConstruct
       public void initModel() {
           productRetriever = productTeaser.getProductRetriever();
   
           if (productRetriever != null) {
               productRetriever.extendProductQueryWith(p -> p.createdAt());
           }
   
       }
   ...
   ```

   注 `@PostConstruct` 释确保在初始化Sling模型后立即调用此方法。

   请注意，产品GraphQL查询已使用方法进 `extendProductQueryWith` 行扩展以检索附加属 `created_at` 性。 此属性稍后会用作方法的一 `isShowBadge()` 部分。

1. 更新GraphQL查询以将属 `eco_friendly` 性包含在部分查询中：

   ```java
   //MyProductTeaserImpl.java
   
   private static final String ECO_FRIENDLY_ATTRIBUTE = "eco_friendly";
   
   @PostConstruct
   public void initModel() {
       productRetriever = productTeaser.getProductRetriever();
   
       if (productRetriever != null) {
           productRetriever.extendProductQueryWith(p ->
                productRetriever.extendProductQueryWith(p -> p
                   .createdAt()
                   .addCustomSimpleField(ECO_FRIENDLY_ATTRIBUTE)
               );
           );
       }
   }
   ```

   添加到该方 `extendProductQueryWith` 法是确保模型的其余部分可以使用其他产品属性的一种有效方法。 它还会最小化执行的查询数。

   在上面的代码中`addCustomSimpleField` ，该代码用于检索属 `eco_friendly` 性。 这说明了如何查询属于Magento模式的任何自定义属性。

   >[!NOTE]
   >
   > 该方 `createdAt()` 法实际上已作为产品界面的一 [部分实现](https://github.com/adobe/commerce-cif-magento-graphql/blob/master/src/main/java/com/adobe/cq/commerce/magento/graphql/ProductInterface.java)。 大多数常见的模式属性都已实现，因此只使用真正的自 `addCustomSimpleField` 定义属性。

1. 添加记录器以帮助调试Java代码：

   ```java
   import org.slf4j.Logger;
   import org.slf4j.LoggerFactory;
   ...
   @Model(adaptables = SlingHttpServletRequest.class, adapters = MyProductTeaser.class, resourceType = MyProductTeaserImpl.RESOURCE_TYPE)
   public class MyProductTeaserImpl implements MyProductTeaser {
   
   private static final Logger LOGGER = LoggerFactory.getLogger(MyProductTeaserImpl.class);
   ```

1. 接下来，实现 `isEcoFriendly()` 方法：

   ```java
   @Override
   public Boolean isEcoFriendly() {
   
       Integer ecoFriendlyValue;
       try {
           ecoFriendlyValue = productRetriever.fetchProduct().getAsInteger(ECO_FRIENDLY_ATTRIBUTE);
           if(ecoFriendlyValue != null && ecoFriendlyValue.equals(Integer.valueOf(1))) {
               LOGGER.info("*** Product is Eco Friendly**");
               return true;
           }
       } catch (SchemaViolationError e) {
           LOGGER.error("Error retrieving eco friendly attribute");
       }
       LOGGER.info("*** Product is not Eco Friendly**");
       return false;
   }
   ```

   在上述方法中， `productRetriever` 用于获取产品，而 `getAsInteger()` 该方法用于获取属性的 `eco_friendly` 值。 根据我们之前运行的GraphQL查询，我们知道当属性 `eco_friendly` 设置为“是”时的&#x200B;**预期值**&#x200B;实际上是1的 **整数**。

   现在，Sling Model已更新，组件标记需要更新，以实际显示基于Sling Model的 **Eco Friendly** 指示符。

## 自定义产品Teaser的标记 {#customize-markup-product-teaser}

AEM组件的一个常见扩展是修改组件生成的标记。 这是通过覆盖组件 [用于呈现](https://docs.adobe.com/content/help/zh-Hans/experience-manager-htl/using/overview.html) 其标记的HTL脚本来完成的。 HTML模板语言(HTL)是一种轻量级模板语言，AEM组件使用它根据创作的内容动态呈现标记，从而允许重新使用组件。 例如，可以反复重复使用产品Teaser来显示不同的产品。

在我们的情况下，我们希望在Teaser顶部渲染一个横幅，以指示产品基于自定义属性为“Eco Friendly”。 自定义组件 [标记的设计模式](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/customizing.html#customizing-the-markup) 实际上是所有AEM组件(而不仅仅是AEM CIF核心组件)的标准。

1. 在IDE中，导航并展开模 `ui.apps` 块，然后展开文件夹层次结构： `ui.apps/src/main/content/jcr_root/apps/venia/components/commerce/productteaser` 检查文 `.content.xml` 件。

   ![产品Teaser ui.apps](../assets/customize-cif-components/product-teaser-ui-apps-ide.png)

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0" xmlns:cq="http://www.day.com/jcr/cq/1.0" xmlns:jcr="http://www.jcp.org/jcr/1.0"
       jcr:description="Product Teaser Component"
       jcr:primaryType="cq:Component"
       jcr:title="Product Teaser"
       sling:resourceSuperType="core/cif/components/commerce/productteaser/v1/productteaser"
       componentGroup="Venia - Commerce"/>
   ```

   以上是我们项目中产品Teaser组件的组件定义。 注意属性 `sling:resourceSuperType="core/cif/components/commerce/productteaser/v1/productteaser"`。 这是创建代理组 [件的示例](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/get-started/using.html#create-proxy-components)。 我们可以使用继承所有功能，而不是从AEM CIF核心组件复制和粘贴所 `sling:resourceSuperType` 有产品Teaser HTL脚本。

1. Open the file `productteaser.html`. 这是CIF产品Teaser `productteaser.html` 中文 [件的副本](https://github.com/adobe/aem-core-cif-components/blob/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/productteaser/v1/productteaser/productteaser.html)

   ```html
   <!--/* productteaser.html */-->
   <sly data-sly-use.product="com.venia.core.models.commerce.MyProductTeaser"
       data-sly-use.templates="core/wcm/components/commons/v1/templates.html"
       data-sly-use.actionsTpl="actions.html"
       data-sly-test.isConfigured="${properties.selection}"
       data-sly-test.hasProduct="${product.url}">
   ```

   请注意，使用的Sling `MyProductTeaser` 模型已被分配给变 `product` 量。

1. 修 `productteaser.html` 改以调用前一练 `isEcoFriendly` 习中实现的方法：

   ```html
   ...
   <div data-sly-test="${isConfigured && hasProduct}" class="item__root" data-cmp-is="productteaser" data-virtual="${product.virtualProduct}">
       <div data-sly-test="${product.showBadge}" class="item__badge">
           <span>${properties.text || 'New'}</span>
       </div>
       <!--/* Insert call to Eco Friendly here */-->
       <div data-sly-test="${product.ecoFriendly}" class="item__eco">
           <span>Eco Friendly</span>
       </div>
   ...
   ```

   在HTL中调用Sling Model方法时， `get` 将 `is` 丢弃该方法的和部分，并将第一个字母小写。 所以 `isShowBadge()` 变 `.showBadge` 得 `isEcoFriendly` 越来越 `.ecoFriendly`多。 根据返回的布尔值确 `.isEcoFriendly()` 定是否 `<span>Eco Friendly</span>` 显示。

   有关其他 `data-sly-test` HTL块语 [句的更多信息，请访问此处](https://docs.adobe.com/content/help/en/experience-manager-htl/using/htl/block-statements.html#test)。

1. 使用Maven技能保存更改并从命令行终端部署更新至AEM::

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallPackage,cloud
   ```

1. 打开新的浏览器窗口并导航到AEM，然后 **导航到OSGi控** 制台 **>** 状态 **>** Sling模型： [http://localhost:4502/system/console/status-slingmodels](http://localhost:4502/system/console/status-slingmodels)

1. 搜索 `MyProductTeaserImpl` 时，您应看到如下行：

   ```plain
   com.venia.core.models.commerce.MyProductTeaserImpl - venia/components/commerce/productteaser
   ```

   这表示Sling Model已正确部署并映射到正确的组件。

1. 刷新至 **已添加**[产](http://localhost:4502/editor.html/content/venia/us/en.html) 品Teaser的Venia主页。

   ![显示“Eco Friendly（生态友好）”消息](../assets/customize-cif-components/eco-friendly-text-displayed.png)

   如果产品的属 `eco_friendly` 性设置为 **“是**”，则页面上应显示“Eco Friendly”文本。 尝试切换到不同的产品以查看行为变化。

1. 接下来打开AEM `error.log` 查看我们添加的日志语句。 位 `error.log` 于 `<AEM SDK Install Location>/crx-quickstart/logs/error.log`。

   搜索AEM日志以查看在Sling Model中添加的日志语句：

   ```plain
   2020-08-28 12:57:03.114 INFO [com.venia.core.models.commerce.MyProductTeaserImpl] *** Product is Eco Friendly**
   ...
   2020-08-28 13:01:00.271 INFO [com.venia.core.models.commerce.MyProductTeaserImpl] *** Product is not Eco Friendly**
   ...
   ```

   >[!CAUTION]
   >
   > 如果Teaser中使用的产品没有属性作为其属性集的一部分， `eco_friendly` 您也会看到一些堆栈跟踪。

## 为Eco Friendly徽章添加样式 {#add-styles}

此时，显示Eco Friendly徽章的逻辑 **正在工作** ，但纯文本可能使用某些样式。 然后，向模块添加一个图标 `ui.frontend` 和样式以完成实施。

1. 下载 [eco_friendly.svg文件](../assets/customize-cif-components/eco_friendly.svg) 。 此徽章将用作 **环保徽章** 。
1. 返回到IDE并导航到该文 `ui.frontend` 件夹。
1. 将文件 `eco_friendly.svg` 添加到文 `ui.frontend/src/main/resources/images` 件夹：

   ![添加了生态友好型SVG](../assets/customize-cif-components/eco-friendly-svg-added.png)

1. 在打开文 `productteaser.scss` 件 `ui.frontend/src/main/styles/commerce/_productteaser.scss`。
1. 在类中添加以下Sass规 `.productteaser` 则：

   ```scss
   .productteaser {
       ...
       .item__eco {
           width: 60px;
           height: 60px;
           left: 0px;
           overflow: hidden;
           position: absolute;
           padding: 5px;
   
       span {
           display: block;
           position: absolute;
           width: 45px;
           height: 45px;
           text-indent: -9999px;
           background: no-repeat center center url('../resources/images/eco_friendly.svg'); 
           }
       }
   ...
   }
   ```

   >[!NOTE]
   >
   > 有关前 [端工作流的更多详细信息](./style-cif-component.md) ，请查看样式CIF核心组件。

1. 使用Maven技能保存更改并从命令行终端部署更新至AEM::

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallPackage,cloud
   ```

1. 刷新至 **已添加**[产](http://localhost:4502/editor.html/content/venia/us/en.html) 品Teaser的Venia主页。

   ![生态友好徽章最终实施](../assets/customize-cif-components/final-product-teaser-eco-badge.png)

## 恭喜 {#congratulations}

您刚刚自定义了您的第一个AEM CIF组件！ 在此处下 [载完成的解决方案文件](../assets/customize-cif-components/customize-cif-component-SOLUTION_FILES.zip)。

## 奖金挑战 {#bonus-challenge}

查看已在产 **品** Teaser中实现的新徽章的功能。 尝试为作者添加一个额外的复选框，以控制何 **时应显示** Eco Friendly徽章。 您需要在更新组件对话框 `ui.apps/src/main/content/jcr_root/apps/venia/components/commerce/productteaser/_cq_dialog/.content.xml`。

![新徽章实施挑战](../assets/customize-cif-components/new-badge-implementation-challenge.png)

## 其他资源 {#additional-resources}

* [AEM原型](https://docs.adobe.com/content/help/zh-Hans/experience-manager-core-components/using/developing/archetype/overview.html)
* [AEM CIF核心组件](https://github.com/adobe/aem-core-cif-components)
* [自定义AEM CIF核心组件](https://github.com/adobe/aem-core-cif-components/wiki/Customizing-CIF-Core-Components)
* [自定义核心组件](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/customizing.html)
* [AEM Sites入门](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html)