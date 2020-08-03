---
title: 样式AEM CIF核心组件
description: 样式AEM CIF核心组件
translation-type: tm+mt
source-git-commit: 48805b21500ff3f2629efd6aecb40bb1cdc38cd6
workflow-type: tm+mt
source-wordcount: '2568'
ht-degree: 1%

---


# 样式AEM CIF核心组件 {#style-aem-cif-core-components}

CIF项 [目原型创建Adobe Experience Manager](https://github.com/adobe/aem-cif-project-archetype) (AEM)CIF项目，作为使用AEM CIF核心组件的客户项目 [的起点](https://github.com/adobe/aem-core-cif-components)。 最初会将默认样式（称为Venia品牌）应用于该站点。 在本教程中，您将检查由原型生成的新AEM CIF项目，并了解AEM CIF核心组件使用的CSS和JavaScript的组织方式。 您还将使用CSS创建新样式以替换产品Teaser组件的默认样式。

![您将构建的内容](/help/commerce-cloud/assets/style-cif-component/what-you-will-build.png)

>[!NOTE]
> 将为类似于卡的产品Teaser组件实施新样式。

## 前提条件 {#prerequisites}

需要以下工具和技术：

* [Java 1.8](https://www.oracle.com/technetwork/java/javase/downloads/index.html) 或 [Java 11](https://www.oracle.com/technetwork/java/javase/downloads/jdk11-downloads-5066655.html) (仅AEM 6.5+)
* [Apache Maven](https://maven.apache.org/) （3.3.9或更高版本）
* Adobe Experience Manager（本地实例）
   * [AEM 6.5](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/introduction/technical-requirements.html)
   * [AEM 6.4.4+](https://docs.adobe.com/content/help/en/experience-manager-64/release-notes/sp-release-notes.html)
* Magento运 [行与原型兼容的版本](https://github.com/adobe/aem-cif-project-archetype#requirements)

## 生成项目 {#generate-project}

我们将使用CIF项目原型生成一个新的AEM CIF [项目](https://github.com/adobe/aem-cif-project-archetype) ，然后覆盖默认样式。

**您可以随意使用现有项目** （基于CIF项目原型）并跳过本节。

1. 通过在GitHub上查看最新版本，确定CIF [项目原型的最新版本](https://github.com/adobe/aem-cif-project-archetype/releases/latest)。 在下一步中，请 `x.y.z` 替换为最新版本。

1. 运行以下Maven命令以批处理模式生成 [新项目](https://maven.apache.org/archetype/maven-archetype-plugin/examples/generate-batch.html)。

   ```terminal
   mvn archetype:generate -B \
       -DarchetypeGroupId="com.adobe.commerce.cif" \
       -DarchetypeArtifactId="cif-project-archetype" \
       -DarchetypeVersion=x.y.z \
       -DgroupId="com.acme.cif" \
       -DartifactId="acme-store" \
       -Dversion=0.0.1-SNAPSHOT \
       -Dpackage="com.acme.cif" \
       -DappsFolderName="acme" \
       -DartifactName="Acme Store" \
       -DcontentFolderName="acme" \
       -DpackageGroup="acme" \
       -DsiteName="Acme Store" \
       -DoptionAemVersion=6.5.0 \
       -DoptionIncludeExamples=y \
       -DoptionEmbedConnector=y
   ```

1. 构建项目并将其部署到AEM的本地实例：

   ```shell
   $ cd acme-store/
   $ mvn clean install -PautoInstallAll
   ```

1. 添加必要的OSGi配置，将AEM实例连接到Magento实例，或将配置添加到新创建的项目。

1. 此时，您应具有连接到Magento实例的店面的工作版本。 导航到 `US` >页 `Home` 面： [http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html)

   您应当看到店面当前正在使用Venia主题。 展开店面的“主菜单”时，您应当看到各种类别，表明连接Magento正在工作。

   ![使用Venia Theme配置的店面](/help/commerce-cloud/assets/style-cif-component/acme-store-configured.png)

## 客户端库简介 {#introduction-to-client-libraries}

负责呈现店面主题／样式的CSS和JavaScript在AEM中由客户端库 [或clientlibs](https://docs.adobe.com/content/help/en/experience-manager-65/developing/introduction/clientlibs.html) 管理。 客户端库提供一种机制，用于在项目代码中组织CSS和Javascript，然后交付到页面上。

我们向AEM CIF核心组件应用品牌特定样式的方法是添加和覆盖这些客户端库管理的CSS。 了解客户端库的结构和包含在页面上的方式至关重要。

### 项目客户端库 {#project-client-libraries}

接下来，我们将检查原型自动生成的客户端库。 使用您选择的IDE导 [入上一练习中生成的项目](https://docs.adobe.com/content/help/en/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html#set-up-an-integrated-development-environment)。

1. 导航并展开 **ui.apps模块** ，然后展开文件夹层次结构以： `ui.apps/src/main/content/jcr_root/apps/acme/clientlibs`:

   ![ui.apps客户端](/help/commerce-cloud/assets/style-cif-component/ui-apps-clientli-folder.png)

   下面有两个文件 **夹，clientlib-base** 和 **theme**。

1. **clientlib-base** —— 这是一个空的客户端库，它只嵌入AEM核心组件中必 [需的依赖项](https://docs.adobe.com/content/help/zh-Hans/experience-manager-core-components/using/introduction.html)。

   ![Clientlib-base](/help/commerce-cloud/assets/style-cif-component/clientlib-base-folderhierarchy.png)

   下面是clientlib基的 **XML定义** ( `.content.xml` 文件):

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:cq="http://www.day.com/jcr/cq/1.0" xmlns:jcr="http://www.jcp.org/jcr/1.0"
       jcr:primaryType="cq:ClientLibraryFolder"
       allowProxy="{Boolean}true"
       categories="[acme.wcm.base]"
       embed="[core.wcm.components.accordion.v1,core.wcm.components.tabs.v1,core.wcm.components.carousel.v1,core.wcm.components.image.v2,core.wcm.components.breadcrumb.v2,core.wcm.components.search.v1,core.wcm.components.form.text.v2]"/>
   ```

   `acme.wcm.base` 是此客户端库的类别。 把一个类别当做标签。 此组件将用于在页面中包含或嵌入库。

   注意属 `embed` 性和其他clientlib类别的数组。 这些类别中的每个都代表一个客户端库。 例如，包 `core.wcm.components.accordion.v1` 括Accordion组件工 [作所需的](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/accordion.html) javascript。

   使用和属 `embed` 性， `categories` 您可以管理和包含来自不同项目的客户端库。

   `allowProxy=true` 确保客户端库CSS和JavaScript将通过以下前缀的路径提供： `/etc.clientlibs`. 这可确保受保护的应 `/apps` 用程序代码不受最终用户的保护，但网站运行所需的CSS和JavaScript可以匿名提供。 有关allowProxy属 [性的更多详细信息，请参阅此处](https://docs.adobe.com/content/help/en/experience-manager-65/developing/introduction/clientlibs.html#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet)。

1. **theme** —— 这是包含CIF项目的开始主题和CSS的客户端库。 此客户端库设计为由每个实现自定义，它有助于用一些现有样式进行开始，以便组件能够正常开始。

   ![主题客户端库](/help/commerce-cloud/assets/style-cif-component/clientlib-theme-folder-hierarchy.png)

   以下是主题的XML定 **义**:

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:cq="http://www.day.com/jcr/cq/1.0" xmlns:jcr="http://www.jcp.org/jcr/1.0"
       jcr:primaryType="cq:ClientLibraryFolder"
       allowProxy="{Boolean}true"
       categories="[acme.theme]"/>
   ```

   `acme.theme` 是此客户端库的类别，这是将客户端库包含在页面中的方式。

1. 主题客 **户端** 库的下方应当有一个名 **为css.txt的文** 件，位于： `ui.apps/src/main/content/jcr_root/apps/acme/clientlibs/theme/css.txt`:

   ```plain
   #base=.
   common/common.css
   
   components/button/button.css
   
   components/featuredcategorylist/categorylist.css
   
   ...
   ```

   css. **txt** (和 **js.txt**)充当清单，指示在最终CSS文件中包含各个文件的顺序。 订购对CSS和JavaScript都很重要，能创建多个文件以更好地管理代码是件好事。 通过查 **看css.txt** 文件，您可以看到文件是由应用样式的组件组织的。

1. Inspect主题／组 **件下的CSS文件** ，了解ootb组件样式。 稍后我们将在教程中更新其中一些文件。

### 包含基页组件的客户端库

接下来，我们将使用HTL和页面组件检查页面中 [包含](https://docs.adobe.com/content/help/en/experience-manager-65/developing/introduction/clientlibs.html#using-htl) 客户端库的方式。

1. 在ui. **apps模块中** ，导航到组件 `page` 定义： `ui.apps/src/main/content/jcr_root/apps/acme/components/structure/page`. 此 **页面** （由原型生成）组件是用于呈现项目中所有页面的入口点。

1. 如果检查页 **面组** 件的定义(`page/.content.xml`)，您会注意到 `sling:resourceSuperType` 指向的属性 `core/cif/components/structure/page/v1/page`。 这意味着我们项目的(Acme)页 **面组件** 将继承CIF核心页面组 [件的所有功能](https://github.com/adobe/aem-core-cif-components/tree/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/structure/page/v1/page) ，并允许我们管理较少的代码。

1. 在页面 **组件** 下方，您会找到两个文件： **customheaderlibs.html****和customfooterlibs.html**。

   ```html
   <!--/* customheaderlibs.html */-->
   <sly data-sly-use.clientLib="/libs/granite/sightly/templates/clientlib.html"
    data-sly-call="${clientlib.css @ categories='acme.wcm.base'}"/>
   ```

   **customheaderlibs** .html是将在页首呈现的HTL脚本。 它是覆盖和添加项目特定逻辑的通用脚本。 在这种情况下，我们使用它将客户端库包含在类别 `acme.wcm.base`中。 遵循Web开发最佳实践，我们只将CSS包含在页面的头部。

   ```html
   <!--/* customfooterlibs.html */-->
   <sly data-sly-use.clientlib="/libs/granite/sightly/templates/clientlib.html">
       <sly data-sly-call="${clientlib.js @ categories='acme.wcm.base'}"/>
   </sly>
   ```

   **customfooterlibs** .html是一个HTL脚本，将呈现在页面底部，就在结束标记 `</body>` 前。 再次使用的 `acme.wcm.base` 类别，但这次将仅加载客户端库的JavaScript。

修改页面组件 **的HTL** 脚本 `acme.wcm.base` 是在所有页面中包括的方式。 那么呢 `acme.theme`? 在下一个练习中，我们将看到另一个包含客户端库的选项。

### 包含页面模板的客户端库 {#client-library-inclusion-pagetemplates}

有关如何包含客户端库的方法有若干选项。 接下来，我们将通过页面模板检查生成的项目如何包含主题客户端 [库](https://docs.adobe.com/content/help/en/experience-manager-65/developing/platform/templates/page-templates-editable.html)。

打开新浏览器并登录到在本教程开头部署项目的AEM实例。

1. 从AEM开始屏幕导航到 **工具** > **常规** > **模**&#x200B;板。

   ![模板导航](/help/commerce-cloud/assets/style-cif-component/template-location.png)

1. 导航到Acme **Store Configuration** 文件夹。 通过选 **择铅笔图标** ，打开 *类别页面* 模板。

   ![类别页模板卡](/help/commerce-cloud/assets/style-cif-component/category-page-template.png)

1. 在左上角，选择页面信息 **图标** ，然后单 **击页面策略**。

   ![页面策略菜单项](/help/commerce-cloud/assets/style-cif-component/page-policy-menu.png)

1. 这将打开目录页面模板的页面策略：

   ![页面策略——目录页](/help/commerce-cloud/assets/style-cif-component/page-policy-properties.png)

   在右侧，您可以看到一个列表，其中列出了将 **包含** 在使用此模板的所有页面上的客户端库类别。

   * **wcm.foundation.components.page.responsive** —— 提供创作者启用响应式布局 [控件所需](https://docs.adobe.com/content/help/en/experience-manager-65/authoring/siteandpage/responsive-layout.html) 的CSS。
   * **acme.theme** —— 这是原型自动生成的起始主题。 默认情况下，此样式与示例Venia演示商店相似。 但是，正如您从名称中看到的，它旨在由项目实施进行自定义。 *这是我们将在下一节中修改的内容！*
   * **core.cif.components.react** —— 这是一个编译的客户端库，包含几个用于动态功能（如购物车）的React组件。 更多 [信息可在此处找到](https://github.com/adobe/aem-core-cif-components/tree/master/react-components)。

   请注意，其他模板使用相 **同的策略**、 **内容**&#x200B;页、登陆页等…… 通过重新使用同一策略，我们可以确保所有页面都包含相同的客户端库。

   使用“模板”和“页面”策略管理包含客户端库的好处在于，您可以根据模板更改策略。 例如，您可能正在管理同一AEM实例中的两个不同品牌。 每个品牌都有自己独特的风格 *或主题* ，但基本库和代码将相同。 另一个示例是，如果您有一个较大的客户端库，而它只想显示在某些页面上，则可以为该模板制定一个唯一的页面策略。 另一个优势

### 验证页面上的客户端库 {#verify-client-libraries}

此时，我们已查看如何将HTL与 **customheaderlibs** .html **** 和customfooterlibs.html脚本一起使用，以及如何使用模板的页面策略来包含其他客户端库。 接下来，我们将验证站点中是否包含客户端库。

1. 从AEM开始屏幕导航到 **站点** > **Acme Store** > **United States** **>** English打开页面进行编辑： [http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html)。

1. 选择“页 **面信息** ”菜单，然后单 **击“视图为已发布”**:

   ![查看已发布的项目](/help/commerce-cloud/assets/style-cif-component/view-as-published.png)

   此操作将打开页面，而不加载任何AEM作者javascript，就像它在已发布站点上一样。 请注意，url附加了查询 `?wcmmode=disabled` 参数。 在开发CSS和Javascript时，最好使用此参数来简化页面，而无需AEM作者提供的任何内容。

1. 视图页面源，您应该能够识别以下客户端库： **acme.wcm.base**、 **wcm.foundation.components.page.responsive**、 **acme.theme**、 **core.cif.components.react**

   ```html
   <!DOCTYPE html>
   <html lang="en-US">
   <head>
       ...
       <link rel="stylesheet" href="/etc.clientlibs/acme/clientlibs/clientlib-base.css" type="text/css">
       <link rel="stylesheet" href="/libs/wcm/foundation/components/page/responsive.css" type="text/css">
       <link rel="stylesheet" href="/etc.clientlibs/acme/clientlibs/theme.css" type="text/css">
   </head>
   ...
   
       <script type="text/javascript" src="/etc.clientlibs/core/cif/clientlibs/react-components.js"></script>
       <script type="text/javascript" src="/etc.clientlibs/acme/clientlibs/clientlib-base.js"></script>
   </body>
   </html>
   ```

## 设计产品Teaser样式 {#style-product-teaser}

既然我们了解了原型生成的客户端库结构，就可以开始定制AEM CIF核心组件。 我们将修改产品Teaser组件的样式，使其更像“卡”。

### 创作产品Teaser {#author-product-teaser}

首先，我们将使用AEM创作工具将产品Teaser组件的新实例添加到我们站点的主页。

1. 打开新的浏览器选项卡并导 **航到** 站点的主页: [http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html)。

1. 将新的产 **品Teaser** 组件插入页面的主布局容器。

   ![插入产品Teaser](/help/commerce-cloud/assets/style-cif-component/product-teaser-add-component.png)

1. 展开侧面板（如果尚未切换），并将资产查找器下拉列表切换到 **产品**。 这应显示连接列表实例中可用产品的Magento。 选择一个产品 **并将其拖放** 到页面 **上的产品Teaser** 组件上。

   ![拖放产品Teaser](/help/commerce-cloud/assets/style-cif-component/drag-drop-product-teaser.png)

   > 注意，您还可以通过使用对话框配置组件（单击扳手图标）来配 *置显* 示的产品。

1. 您现在应当看到产品Teaser正在显示产品。 产品名称和产品价格是显示的默认属性。

   ![产品Teaser —— 默认样式](/help/commerce-cloud/assets/style-cif-component/product-teaser-default-style.png)

### 更新产品Teaser的CSS {#update-css-product-teaser}

接下来，我们将修改主题客 **户端** 库中的CSS，以便为产品Teaser实现类似卡的样式。

返回到IDE和生成的项目。

1. 在ui. **apps模块中** ，导航到文件夹： `ui.apps/src/main/content/jcr_root/apps/acme/clientlibs/theme/components/productteaser`. 这是定义产品Teaser的所有样式的位置。

1. 打开文件 **teaser.css** 并更新相应的CSS规则(或下载解决 [方案teaser.css文件并替换](/help/commerce-cloud/assets/style-cif-component/solution-teaser.css) )。

   添加投影并在产品Teaser中包含圆角。

   ```css
    .productteaser .item__root {
        position: relative;
        box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);
        transition: 0.3s;
        border-radius: 5px;
        float: left;
        margin-left: 12px;
        margin-right: 12px;
   }
   
   .productteaser .item__root:hover {
      box-shadow: 0 8px 16px 0 rgba(0,0,0,0.2);
   }
   ```

   更改产品Teaser中图像的边框。

   ```css
   .productteaser .item__image {
       border-bottom: 1px solid #c0c0c0;
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

   更新产品名称以显示在Teaser的底部并修改文本颜色。

   ```css
   .productteaser .item__name {
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

   更新产品的价格，使其也显示在Teaser的底部并修改文本颜色。

   ```css
   .productteaser .item__price {
       color: #000;
       display: block;
       float: left;
       font-size: 18px;
       font-weight: 900;
       padding: 0.75em;
       padding-bottom: 2em;
       width: 25%;
   }
   ```

   更新底部的媒体查询，以在小于992像素的屏幕中堆叠名称和价格。

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

   将更改保 **存到teaser.css**。 您可以在此 [处下载解决方案teaser.css文件](/help/commerce-cloud/assets/style-cif-component/solution-teaser.css)。

1. 使用Maven技能 **从命令行终端** ，将ui.apps模块的更新部署到AEM::

   ```shell
           $ cd acme-store/ui.apps/
           $ mvn -PautoInstallPackage clean install
           ...
           saving approx 0 nodes...
           Package imported.
           Package installed in 61ms.
           [INFO] ------------------------------------------------------------------------
           [INFO] BUILD SUCCESS
           [INFO] ------------------------------------------------------------------------
           [INFO] Total time:  6.903 s
           [INFO] Finished at: 2020-02-06T13:21:36-08:00
            [INFO] ------------------------------------------------------------------------
   ```

   >[!NOTE]
   >还有其他IDE [设置和工具](https://docs.adobe.com/content/help/en/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html#set-up-an-integrated-development-environment) ，它们可以将项目文件直接同步到本地AEM实例，而无需执行完全的Maven生成。

### 视图更新的产品Teaser {#view-updated-product-teaser}

项目的代码部署到AEM后，我们现在应该能够看到对产品Teaser的更改。

1. 返回浏览器并重新刷新主页: [http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html)。 您应看到已应用更新的产品Teaser样式。

   ![更新的产品Teaser样式](/help/commerce-cloud/assets/style-cif-component/product-teaser-new-style.png)

1. 通过添加其他产品Teaser进行试验。 使用布局模式更改组件的宽度和偏移，以在一行中显示多个Teaser。

   ![多个产品Teaser](/help/commerce-cloud/assets/style-cif-component/multiple-teasers-final.png)

   >[!NOTE]
   >每个产品Teaser都包含相同的样式。

### 疑难解答 {#troubleshooting}

您可以在CRXDE- [Lite中验证](http://localhost:4502/crx/de/index.jsp) ，已部署更新的CSS文件： [http://localhost:4502/crx/de/index.jsp#/apps/acme/clientlibs/theme/components/productteaser/teaser.css](http://localhost:4502/crx/de/index.jsp#/apps/acme/clientlibs/theme/components/productteaser/teaser.css)

部署新的CSS和／或JavaScript文件时，确保浏览器不提供旧文件也很重要。 您可以通过清除浏览器缓存或启动新的浏览器会话来消除这种情况。

AEM还尝试缓存客户端库以提高性能。 偶尔，在代码部署之后，会提供旧文件。 您可以使用“重新构建客户端库”工具手动使AEM [客户端库缓存失效](http://localhost:4502/libs/granite/ui/content/dumplibs.rebuild.html)。 *如果您怀疑AEM已缓存客户端库的旧版本，则首选使用Invalidate Caches方法。 重新构建库效率低下且耗时。*

### 恭喜 {#congratulations}

您刚设置了第一个AEM CIF核心组件！

### 奖金挑战 {#bonus-challenge}

使用AEM [样式系统](https://docs.adobe.com/content/help/en/experience-manager-65/developing/components/style-system.html) ，创建可由内容作者打开／关闭的两种样式。 [使用样式系统进行开发](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-wknd-tutorial-develop/style-system.html) ，包括如何实现该功能的详细步骤和信息。

![奖金挑战——风格系统](/help/commerce-cloud/assets/style-cif-component/bonus-challenge.png)

## 其他资源 {#additional-resources}

* [AEM CIF原型](https://github.com/adobe/aem-cif-project-archetype)

* [AEM CIF核心组件](https://github.com/adobe/aem-core-cif-components)

* [设置本地AEM开发环境](https://docs.adobe.com/content/help/en/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html)

* [客户端库](https://docs.adobe.com/content/help/en/experience-manager-65/developing/introduction/clientlibs.html)
* [AEM Sites入门](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html)

* [以风格体系发展](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-wknd-tutorial-develop/style-system.html)
