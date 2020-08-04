---
title: 自定义CIF核心组件
description: 自定义CIF核心组件
translation-type: tm+mt
source-git-commit: c3cf472f5e207e7ca0788dc3e42105868d9bdf00
workflow-type: tm+mt
source-wordcount: '2520'
ht-degree: 1%

---


# 自定义AEM CIF核心组件 {#customize-cif-components}

[AEM CIF核心组件](https://github.com/adobe/aem-core-cif-components) (CIF Core Components)提供一套标准的商务组件，可用于加快集成Adobe Experience Manager(AEM)和Magento解决方案的项目。 这些组件可以随时进行制作，并可 [以使用CSS轻松设置样式](style-cif-component.md)。 许多实施还希望扩展这些组件以满足业务特定要求。

在本教程中，我们将回顾AEM CIF核心组件和AEM一般提供的几个不同扩展点。 为此，我们将扩展产品Teaser组 [件的功能](https://github.com/adobe/aem-core-cif-components/tree/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/productteaser/v1/productteaser) ，以包含渲染“新”横幅的功能。 内容作者将能够切换此横幅并确定显示该横幅的时间。 产品的“年龄”将基于Magento目录中产品的创建日期。 一旦某个产品有一定的使用时间，“新”横幅将自动消失。

![新横幅扩展](/help/commerce-cloud/assets/customize-cif-components/new-banner-productteaser.png)

## 前提条件 {#prerequisites}

需要以下工具和技术：

* [Java 11](https://www.oracle.com/technetwork/java/javase/downloads/jdk11-downloads-5066655.html)
* [Apache Maven](https://maven.apache.org/) （3.3.9或更高版本）
* [AEM Cloud SKD（带CIF加载项）](../develop.md)
* Magento与CIF核心组件兼容

建议在继续本教程之前查看以下内容：

* [将AEM作为Cloud Service引入商务集成框架](/help/commerce-cloud/overview.md)
* [样式AEM CIF核心组件——教程](style-cif-component.md)

## 入门项目

我们提供了一个要与本教程一起使用的入门项目。 项目是使用 [CIF项目原型](https://github.com/adobe/aem-cif-project-archetype/releases/tag/cif-project-archetype-0.7.0) v0.7.0生成的。 在开始新项目时，始终使用最 [新版](https://github.com/adobe/aem-cif-project-archetype/releases/latest) 本的原型，这被认为是最佳实践。

1. 将启动项 [**目acme-store **](/help/commerce-cloud/assets/customize-cif-components/acme-store.zip).zip下载到桌面。

1. 解压缩 **acme-store.zip** ，您应看到以下文件夹结构：

   ```plain
   /acme-store
      /ui.content
      /ui.apps
      /samplecontent
      /core
      /all
      + pom.xml
      + README.md
   ```

1. 打开新的终端窗口，构建项目并部署到AEM的本地实例；

   ```shell
   $ cd acme-store/
   $ mvn clean install -PautoInstallAll
   ```

1. 添加必要的OSGi配置，将AEM实例连接到Magento实例，或将配置添加到新创建的项目。

1. 此时，您应具有连接到Magento实例的店面的工作版本。 导航到 `US` >页 `Home` 面： [http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html)

   您应当看到店面当前正在使用Venia主题。 展开店面的“主菜单”时，您应当看到各种类别，表明连接Magento正在工作。

   ![使用Venia Theme配置的店面](/help/commerce-cloud/assets/customize-cif-components/acme-store-configured.png)

## 创作产品Teaser {#author-product-teaser}

我们将在本教程中扩展产品Teaser组件。 作为第一步，我们将向主页添加一个新的产品Teaser实例，以了解基线功能。

1. 导航到 **站点** 的主页: [http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html)

1. 将新的产 **品Teaser** 组件插入页面的主布局容器。

   ![插入产品Teaser](/help/commerce-cloud/assets/customize-cif-components/product-teaser-add-component.png)

1. 展开侧面板（如果尚未切换），并将资产查找器下拉列表切换到 **产品**。 这应显示连接列表实例中可用产品的Magento。 选择一个产品 **并将其拖放** 到页面 **上的产品Teaser** 组件上。

   ![拖放产品Teaser](/help/commerce-cloud/assets/customize-cif-components/drag-drop-product-teaser.png)

   > 注意，您还可以通过使用对话框配置组件（单击扳手图标）来配 *置显* 示的产品。

1. 您现在应当看到产品Teaser正在显示产品。 产品名称和产品价格是显示的默认属性。

   ![产品Teaser —— 默认样式](/help/commerce-cloud/assets/customize-cif-components/product-teaser-default-style.png)

## 自定义产品Teaser的标记 {#customize-markup-product-teaser}

AEM组件的一个常见扩展是修改组件生成的标记。 这是通过覆盖组件 [用于呈现](https://docs.adobe.com/content/help/zh-Hans/experience-manager-htl/using/overview.html) 其标记的HTL脚本来完成的。 HTML模板语言(HTL)是一种轻量级模板语言，AEM组件使用它根据创作的内容动态呈现标记，从而允许重新使用组件。 例如，可以反复重复使用产品Teaser来显示不同的产品。

在我们的情况下，我们希望在Teaser顶部渲染一个横幅，以指示产品是“新”的，并且最近已添加到目录中。 自定义组件 [标记的设计模式](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/customizing.html#customizing-the-markup) 实际上是所有AEM组件(而不仅仅是AEM CIF核心组件)的标准。

使用您选择的IDE打 [开在教程开始](https://docs.adobe.com/content/help/en/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html#set-up-an-integrated-development-environment) 时下载的启动项项目。

1. 导航并展开 **ui.apps模块** ，然后展开文件夹层次结构以： `ui.apps/src/main/content/jcr_root/apps/acme/components/commerce/productteaser` 检查文 `.content.xml` 件。

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0" xmlns:cq="http://www.day.com/jcr/cq/1.0" xmlns:jcr="http://www.jcp.org/jcr/1.0"
       jcr:description="Product Teaser Component"
       jcr:primaryType="cq:Component"
       jcr:title="Product Teaser"
       sling:resourceSuperType="core/cif/components/commerce/productteaser/v1/productteaser"
       componentGroup="acme"/>
   ```

   以上是我们项目中产品Teaser组件的组件定义。 注意属性 `sling:resourceSuperType="core/cif/components/commerce/productteaser/v1/productteaser"`。 这是创建代理组 [件的示例](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/get-started/using.html#create-proxy-components)。 我们可以使用继承所有功能，而不是从AEM CIF核心组件复制和粘贴所 `sling:resourceSuperType` 有产品Teaser HTL脚本。

1. 打开新浏览器并导 [航到AEM中的](http://localhost:4502/crx/de/index.jsp#/apps/core/cif/components/commerce/productteaser/v1/productteaser) CRXDE-Lite。 展开树以视图组件 `productteaser` 在下： `/apps/core/cif/components/commerce/productteaser/v1/productteaser`:

   ![CRXDE Lite产品Teaser](/help/commerce-cloud/assets/customize-cif-components/crxde-productteaser.png)

   这是产品Teaser组件的完整组件定义。

1. 切换回IDE和Acme Store项目。 创建名为下面的 `productteaser.html` 新文 `ui.apps/src/main/content/jcr_root/apps/acme/components/commerce/productteaser`件。

1. 从CRXDE-Lite `productteaser.html` 复 [制内容](http://localhost:4502/crx/de/index.jsp#/apps/core/cif/components/commerce/productteaser/v1/productteaser/productteaser.html) ，并将其粘贴到新创建的文件中的Acme-Store `productteaser.html` 项目。

   ![产品Teaser html覆盖](/help/commerce-cloud/assets/customize-cif-components/productteaser-html-overwrite.png)

1. 在Acme-Store项目中，修改文 `productteaser.html` 件并插入一个表示产品图像标记上方的徽章的新div:

   ```html
   ...
   <div data-sly-test.isvalid="${product.url}" class="item__root" data-cmp-is="productteaser">
       <!-- Add Badge -->
       <div class="item__badge">
           <span>New</span>
       </div>
       <!-- end add badge -->
       <a class="item__images" href=${product.url}>
           <img class="item__image" width="100%" height="100%"
                   src="${product.image}" alt="${product.image}"/>
       </a>
       <a class="item__name" href=${product.url}><span>${product.name}</span></a>
       <div class="item__price">
           <span> ${product.formattedPrice} </span>
       </div>
       <sly data-sly-call="${actionsTpl.actions @ product=product}"></sly>
   </div>
   ```

1. 使用您的专业技能或IDE的功能将更新的代码 [部署到AEM的本地实例](https://docs.adobe.com/content/help/en/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html#set-up-an-integrated-development-environment):

   ```shell
   $ cd ui.apps
   $ mvn -PautoInstallPackage clean install
   ```

1. 在浏览器中，返回 [AEM商店前面的主页](http://localhost:4502/editor.html/content/acme/us/en.html) 。 刷新后，您应会看到组件的右上角出现一个“新”横幅。

   ![新横幅扩展](/help/commerce-cloud/assets/customize-cif-components/new-banner-productteaser.png)

   当前，在何时显示横幅时，没有逻辑。 在接下来的几次练习中，我们将纠正这一点。

   > 注意，用于呈现横幅的CSS是作为启动项目的一部分提供的，可在以下位置找到： `ui.apps/../apps/acme/clientlibs/theme/components/productteaser/teaser.css`. 有关更多详细信息， [请查看样式CIF核心组件教程](style-cif-component.md)。

## 自定义产品Teaser的对话框 {#customize-dialog-product-teaser}

接下来，我们将自定义产品Teaser组件的对话框，以允许作者确定产品被视为“新”的日期范围以及是否应显示横幅。 为此，我们将自 [定义产品](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/customizing.html#customizing-dialogs) Teaser的对话框作为Acme Store项目的一部分。

1. 在您选择的IDE中打开Acme Store项目并导航到 `ui.apps/src/main/content/jcr_root/apps/acme/components/commerce/productteaser`。

1. 在文件夹 `productteaser` 下，添加一个名为的新文件 `_cq_dialog`夹。 将新文件添加到名 `_cq_dialog` 为的文件夹 `.content.xml`。 您现在应具有以下文件结构：

   ```plain
   ../acme
       /components
           /commerce
               /productteaser
                  /_cq_dialog
                     + .content.xml
                  /_cq_template
                  + .content.xml
                  + productteaser.html
   ```

1. 使用 `_cq_dialog/.content.xml` 以下XML进行更新：

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0" 
       xmlns:cq="http://www.day.com/jcr/cq/1.0" 
       xmlns:jcr="http://www.jcp.org/jcr/1.0" 
       xmlns:nt="http://www.jcp.org/jcr/nt/1.0" 
       jcr:primaryType="nt:unstructured" 
       jcr:title="My Product Teaser" 
       sling:resourceType="cq/gui/components/authoring/dialog" 
       trackingFeature="cif-core-components:productteaser:v1">
       <content jcr:primaryType="nt:unstructured" 
           sling:resourceType="granite/ui/components/coral/foundation/container">
           <items jcr:primaryType="nt:unstructured">
               <tabs jcr:primaryType="nt:unstructured" 
                   sling:resourceType="granite/ui/components/coral/foundation/tabs" 
                   maximized="{Boolean}true">
                   <items jcr:primaryType="nt:unstructured">
                       <badge jcr:primaryType="nt:unstructured" 
                           jcr:title="Badge" 
                           sling:resourceType="granite/ui/components/coral/foundation/container" 
                           margin="{Boolean}true">
                           <items jcr:primaryType="nt:unstructured">
                               <columns jcr:primaryType="nt:unstructured" 
                                   sling:resourceType="granite/ui/components/coral/foundation/fixedcolumns" 
                                   margin="{Boolean}true">
                                   <items jcr:primaryType="nt:unstructured">
                                       <column jcr:primaryType="nt:unstructured" 
                                           sling:resourceType="granite/ui/components/coral/foundation/container">
                                           <items jcr:primaryType="nt:unstructured">
                                               <badge jcr:primaryType="nt:unstructured" 
                                                   sling:resourceType="granite/ui/components/coral/foundation/form/checkbox" 
                                                   text="Display 'New' badge" 
                                                   value="true" 
                                                   uncheckedValue="false" 
                                                   name="./badge" />
                                               <age jcr:primaryType="nt:unstructured" 
                                                   sling:resourceType="granite/ui/components/coral/foundation/form/numberfield" 
                                                   fieldDescription="The maximum age in days the 'new' badge should be shown" 
                                                   fieldLabel="Max Product Age" 
                                                   name="./age"
                                                   min="{Long}0" 
                                                   value="10" />
                                               <ageTypeHint jcr:primaryType="nt:unstructured" 
                                                   sling:resourceType="granite/ui/components/foundation/form/hidden" 
                                                   ignoreData="{Boolean}true" 
                                                   name="./age@TypeHint" 
                                                   value="Long" />
                                           </items>
                                       </column>
                                   </items>
                               </columns>
                           </items>
                       </badge>
                   </items>
               </tabs>
           </items>
       </content>
   </jcr:root>
   ```

   在上面，我们添加了2个附加字段作为新选项卡和单个隐藏字段的一部分。

   1. 用于显示“新建”徽章的复选框
   2. 用于定义最大产品年龄的数字字段
   3. 隐藏字段，以确保将最大产品时间保存为长时间(有关更多详 [细信息，请参](https://sling.apache.org/documentation/bundles/manipulating-content-the-slingpostservlet-servlets-post.html) 阅@TypeHint)

   定义为代理组件一部分的对话框将继承所有现有对话框字段，其特性称为“ [Sling资源合并”](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/sling-resource-merger.html)。 因此，我们不必重新定义属于产品Teaser的现有字段。

1. 更 `productteaser.html` 新徽章并 `data-sly-test` 为徽 `<div>` 章添加一个。 如果用户已检查“true”，这将是一个简单的测试，用于决定呈现徽章。

   ```html
       ...
       <div data-sly-test.isvalid="${product.url}" class="item__root" data-cmp-is="productteaser">
   
           <!--/* add test to see if properties.badge equals true */-->
           <div data-sly-test="${properties.badge == 'true'}" class="item__badge">
               <span>New</span>
           </div>
   ...
   ```

1. 使用IDE的功能或使用您的专业技能，将更新的代码部署到AEM的本地实例：

   ```shell
   $ cd ui.apps
   $ mvn -PautoInstallPackage clean install
   ```

1. 返回至“产品Teaser”组件，单击扳手 *图标* 以打开对话框。 您现在应该看到一个标记选 **项卡** ，其中包含两个附加字段。 更新这些字段会将值保留到AEM。 您应该能够通过复选框打开／关闭徽章：

   ![切换徽章](/help/commerce-cloud/assets/customize-cif-components/toggle-badge-checkbox.gif)

   这使作者能够控制徽章出现的时间。 但是，如果产品达到某一日龄，则根据Max Product Age（最大产品年龄）的条目，徽章会自动 **消失**。 为此，我们需要实现一些后端逻辑。

## 更新产品Teaser的Sling模型 {#updating-sling-model-product-teaser}

接下来，我们将通过实施Sling模型来扩展产品Teaser的业务逻辑。 [Sling Models](https://sling.apache.org/documentation/bundles/models.html)是注释驱动的“POJO”(Plain Old Java Objects)，可实现组件所需的任何业务逻辑。 Sling Models与HTL脚本结合使用，作为组件的一部分。 我们将遵循Sling [模型的委托模式](https://github.com/adobe/aem-core-wcm-components/wiki/Delegation-Pattern-for-Sling-Models) ，这样我们只需扩展现有产品Teaser模型的部分。

Sling Models是作为Java实现的，可在生成项 **目的** 核心模块中找到。

1. 在您选择的IDE中打开Acme Store项目，并在核心模块 **下导** 航到： `core/src/main/java/com/acme/cif/core/models/MyProductTeaser.java`. **MyProductTeaser.java是我们** 预先创建的一个Java界面，它扩展了CIF ProductTeaser **界面** 。

1. 接下来，打开位 **于以下位置的文件** MyProductTeaserImpl.java: `core/src/main/java/com/acme/cif/core/models/MyProductTeaserImpl.java`. `MyProductTeaserImpl` 是接口的实现类 `MyProductTeaser`。

   使用 [Sling模型的委托模式](https://github.com/adobe/aem-core-wcm-components/wiki/Delegation-Pattern-for-Sling-Models) ，我们可以 `ProductTeaser` 通过以下属性引 `sling:resourceSuperType` 用类：

   ```java
   @Self
   @Via(type = ResourceSuperType.class)
   private ProductTeaser productTeaser;
   ```

   对于我们不想覆盖或更改的所有方法，我们只需返回返回返回的 `ProductTeaser` 值：

   ```java
   @Override
   public String getImage() {
       return productTeaser.getImage();
   }
   ```

1. AEM CIF核心组件提供的额外扩展点之一 `AbstractProductRetriever` 是允许我们访问特定产品属性。 添加以下方法以在方 `AbstractProductRetriever` 法中初始 `init()` 化：

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
   
       }
   ...
   ```

1. 允许通过修改格式化的价格并覆盖中的逻辑来测试这些更改 `getFormattedPrice()`。 进行以下更新，以便我们根据德语区域设置明确设置价格格式。 （或选择其他国家！）

   ```java
           import java.util.Locale;
           import java.text.NumberFormat;
            ...
   
               @Override
                   public String getFormattedPrice() 
                   {
                   //return productTeaser.getFormattedPrice();
                   NumberFormat germanCurrencyFormat = NumberFormat.getCurrencyInstance(Locale.GERMANY);
                   Double price =  productRetriever.fetchProduct().getPrice().getRegularPrice().getAmount().getValue();
                       if(price != null) 
                       {
                           return germanCurrencyFormat.format(price);
                       }
                   return null;
                   }
   ```

   请注意该对 `productRetriever` 象如何通过方法为 `ProductInterface` 我们提供对象 `fetchProduct()` 访问。 您可以在此处查看所 [有可用方法](https://github.com/adobe/commerce-cif-magento-graphql/blob/master/src/main/java/com/adobe/cq/commerce/magento/graphql/ProductInterface.java)。

   > 注意*将区域设置修改为德语只是查看覆盖的一个有趣示例。 实际上，ProductTeaser使用 [页面的区域设置确定格式](https://github.com/adobe/aem-core-cif-components/blob/master/bundles/core/src/main/java/com/adobe/cq/commerce/core/components/internal/models/v1/productteaser/ProductTeaserImpl.java#L173)。

1. 接下来，我们需要更 **新ui.apps模块中****的productteaser.html** ，以引用我们新的Sling Model: `com.acme.cif.core.models.MyProductTeaser`.

   ```diff
     <!--/* productteaser.html - change the use.product to point to MyProductTeaser */-->
     <sly data-sly-use.clientlib="/libs/granite/sightly/templates/clientlib.html"
   -  data-sly-use.product="com.adobe.cq.commerce.core.components.models.productteaser.ProductTeaser"
   +  data-sly-use.product="com.acme.cif.core.models.MyProductTeaser"
      data-sly-use.actionsTpl="actions.html">
      ...
   ```

   将更改保存到 `productteaser.html`。

1. 将代码库部署到AEM的本地实例。 由于对ui.apps和核心 **模块进行了****更改** ，因此从根构建和部署项目：

   ```shell
   $ cd acme-store
   $ mvn -PautoInstallPackage clean install
   ```

1. 打开浏览器并导航到： [http://localhost:4502/system/console/status-slingmodels](http://localhost:4502/system/console/status-slingmodels)。 此控制台显示系统中注册的所有Sling型号。 多次检查以确保MyTeaserModelImpl已部署并正确映射。 您应该能够看到类似的内容：

   ```plain
   com.acme.cif.core.models.MyProductTeaserImpl - acme/components/commerce/productteaser
   ```

1. 最后，导航到您创作产品Teaser组件的位置，您现在应看到采用德国货币格式的价格：

   ![价格格式已更新](/help/commerce-cloud/assets/customize-cif-components/german-currency-update.png)

## 实现isShowBadge逻辑 {#implement-isshowbadge}

现在，我们有机会尝试覆盖Sling Model方法，让我们实施何时显示“新”徽章的逻辑。

1. 返回IDE并打开 **MyProductTeaser.java** 文件： `core/src/main/java/com/acme/cif/core/models/MyProductTeaser.java`.

1. 向接口中添加 `isShowBadge()` 新方法：

   ```java
   @ProviderType
   public interface MyProductTeaser extends ProductTeaser {
       // Extend the existing interface with the additional properties which you
       // want to expose to the HTL template.
       public Boolean isShowBadge();
   }
   ```

   这是我们将引入的一种新方法，用于封装是否显示标记的逻辑。

1. 然后，重新打 **开MyProductTeaserImpl.java** at `core/src/main/java/com/acme/cif/core/models/MyProductTeaserImpl.java`。

1. “new”徽章将显示多长时间的逻辑将基于产品 `created_at` 的属性。 为了能够访问该属性，我们需要扩展 **ProductTeaser执行的** GraphQL查询。 我们可以通过更新MyProductTeaserImpl. `init()` java中的 **方法来实现此目的**:

   ```java
   //MyProductTeaserImpl.java
   
   @PostConstruct
   public void initModel() {
       productRetriever = productTeaser.getProductRetriever();
   
       if (productRetriever != null) {
           // Pass your custom partial query to the ProductRetriever. This class will
           // automatically take care of executing your query as soon
           // as you try to access any product property.
           productRetriever.extendProductQueryWith(p ->
               p.addCustomSimpleField("created_at")
           );
       }
   }
   ```

   添加到该方 `extendProductQueryWith` 法是确保模型的其余部分可以使用其他产品属性的一种有效方法。 它还会最小化执行的查询数。

   >[!NOTE]
   >在上面的代码中`addCustomSimpleField` ，我们使用 `created_at` 属性。 这说明了如何查询属于Magento模式的任何自定义属性。
   >
   > 但是， `created_at` 该属性实际上已作为产品界面的一 [部分实现](https://github.com/adobe/commerce-cif-magento-graphql/blob/master/src/main/java/com/adobe/cq/commerce/magento/graphql/ProductInterface.java) ，最好的做法是重复使用如下方法： `productRetriever.extendProductQueryWith(p -> p.createdAt());`. 大多数常见的模式属性都已实现，因此只使用真正的自 `addCustomSimpleField` 定义属性。

1. 接下来，我们将实现该 `isShowBadge()` 方法：

   ```java
   import java.time.format.DateTimeFormatter;
   import java.util.Locale;
   import java.time.temporal.ChronoUnit;
   
   ...
   
   @Override
   public Boolean isShowBadge() {
        final DateTimeFormatter formatter = DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss");
   
        //Look at the checkbox from the dialog to see if we should even attempt to show the badge
        final boolean showBadge = properties.get("badge", false);
        if (showBadge) {
   
            //Look at the numberfield set from the dialog to determine the max "age" in days to compare too
            final int maxAgeProp = properties.get("age", 0);
   
           String createdAtString;
           try {
               //Grab the created_at property from the product
               //Here we show the example of retrieving the attribute as if it was a custom attribute
               // an alternative that would work is productRetriever.fetchProduct().getCreatedAt()
               createdAtString = productRetriever.fetchProduct().getAsString("created_at");
               log.info("***CREATED_AT**** " + createdAtString);
           } catch (SchemaViolationError e) {
               //it is possible that a schema error could be thrown if the attribute is not part of the schema
               log.error("Error determining to showBadge" , e);
               return false;
           }
   
            // Custom code to calc the date difference of the product creation
            // compared to today
           final LocalDate createdAt = LocalDate.parse(createdAtString, formatter);
            if (createdAt != null) {
   
                final long ageInDays = ChronoUnit.DAYS.between(createdAt, LocalDate.now());
                if (ageInDays < maxAgeProp) {
                    return true;
                }
            }
        }
        return false;
    }
   ```

   在以上方法中，我们首先检查作者是否已通过复选框启用标记功能。 接下来，我们读取设置为对 `age` 话框一部分的属性值，它表示在横幅消失之前产品的最大使用天数。 最后，我们根据日期计算产品的年 `created_at` 龄。 如果比较这两个值后，我们返 `true` 回以显示徽章，在所 `false` 有其他情况下。

1. 最后，需要对脚本再加一 `productteaser.html` 个，以调用该方 `isShowBadge()` 法。 在打开文件 `ui.apps/src/main/content/jcr_root/apps/acme/components/commerce/productteaser/productteaser.html`。 进行以下更新：

   ```diff
   ...
   - <div data-sly-test="${properties.badge == 'true'}" class="item__badge">
   + <div data-sly-test="${product.showBadge}" class="item__badge">
        <span>New</span>
    </div>
   ...
   ```

1. 将代码库部署到AEM的本地实例。 由于对ui.apps和核心 **模块进行了****更改** ，因此从根构建和部署项目：

   ```shell
   $ cd acme-store
   $ mvn -PautoInstallPackage clean install
   ```

1. 返回AEM和ProductTeaser组件，尝试不同的数字以显示产品的最大年龄。 根据产品的年龄，可能需要输入一些非常大的数字才能显示徽章。

   ![最高产品年龄999](/help/commerce-cloud/assets/customize-cif-components/max-age-working.png)

1. 最后，搜索AEM日志以查看在上述步骤5中输入的日志语句。 这应打印来自Magento `created_at` 的属性的值。 可以通过打开文件视图AEM的 `error.log` 日志。 此文件位于已安 `crx-quickstart/logs/error.log` 装AEM jar的下方。 您会看到如下行项目：

   ```plain
   com.acme.cif.core.models.MyProductTeaser ***CREATED_AT**** 2019-06-05 06:51:33
   ```

   现在，您可以验证我们实现的逻辑是否正确！

### 恭喜 {#congratulations}

您刚刚自定义了您的第一个AEM CIF组件！ 在此处 [下载完成的解决方案包](/help/commerce-cloud/assets/customize-cif-components/acme-store-solution.zip)。

## 其他资源 {#additional-resources}

* [AEM原型](https://docs.adobe.com/content/help/zh-Hans/experience-manager-core-components/using/developing/archetype/overview.html)
* [AEM CIF核心组件](https://github.com/adobe/aem-core-cif-components)
* [自定义AEM CIF核心组件](https://github.com/adobe/aem-core-cif-components/wiki/Customizing-CIF-Core-Components)
* [自定义核心组件](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/customizing.html)
