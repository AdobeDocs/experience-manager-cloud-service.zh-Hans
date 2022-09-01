---
title: 为 Screens as a Cloud Service 开发自定义组件
description: 以下教程将演示为AEM Screens创建自定义组件的步骤。 AEM Screens可重复使用其他AEM产品的许多现有设计模式和技术。 本教程重点介绍了在为AEM Screens开发时存在的差异和特殊注意事项。
exl-id: fe8e7bf2-6828-4a5a-b650-fb3d9c172b97
source-git-commit: 421ad8506435e8538be9c83df0b78ad8f222df0c
workflow-type: tm+mt
source-wordcount: '2115'
ht-degree: 2%

---

# 为AEM Screensas a Cloud Service开发自定义组件{#developing-a-custom-component-for-aem-screens}

以下教程将演示为AEM Screens创建自定义组件的步骤。 AEM Screens可重复使用其他AEM产品的许多现有设计模式和技术。 本教程重点介绍了在为AEM Screens开发时存在的差异和特殊注意事项。

## 概述 {#overview}

本教程面向不熟悉AEM Screens的开发人员。 在本教程中，为AEM Screens中的序列渠道构建了一个简单的“Hello World”组件。 通过对话框，作者可以更新显示的文本。


## 前提条件 {#prerequisites}

要完成本教程，需要满足以下条件：

1. 最新Screens功能包

1. AEM Screens 播放器

1. 本地开发环境

使用 **CRXDE-Lite**. IDE还可用于完成本教程。 有关使用IDE进行开发的更多信息 [与AEM的关联。](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-wknd-tutorial-develop/part1.html#eclipse-ide)


## 项目设置 {#project-setup}

Screens项目的源代码通常作为多模块Maven项目进行管理。 为加快教程进度，已使用 [AEM项目原型13](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype). 有关 [可在此处找到使用Maven AEM项目原型创建项目](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-wknd-tutorial-develop/part1.html#maven-multimodule).

1. 使用 [CRX包管理器](http://localhost:4502/crx/packmgr/index.jsp):

[获取文件](/help/screens-cloud/developing/assets/base-screens-weretail-runuiapps-001-snapshot.zip)

   [获取文件](/help/screens-cloud/developing/assets/base-screens-weretail-runuiapps-001-snapshot.zip)
   **（可选）** 如果使用Eclipse或其他IDE，请下载以下源包。 使用Maven命令将项目部署到本地AEM实例：

   **`mvn -PautoInstallPackage clean install`**

   启动HelloWorld SRC Screens We.Retail运行项目

[获取文件](/help/screens-cloud/developing/assets/src-screens-weretail-run.zip)

1. 在 [CRX包管理器](http://localhost:4502/crx/packmgr/index.jsp) 验证是否安装了以下两个包：

   1. **screens-weretail-run.ui.content-0.0.1-SNAPSHOT.zip**
   1. **screens-weretail-run.ui.apps-0.0.1-SNAPSHOT.zip**

   ![Screens We.Retail运行Ui.Apps和Ui.Content包，这些包通过CRX包管理器安装](assets/crx-packages.png)

   Screens We.Retail运行Ui.Apps和Ui.Content包，这些包通过CRX包管理器安装

1. 的 **screens-weretail-run.ui.apps** 软件包安装代码 `/apps/weretail-run`.

   此包包含负责为项目渲染自定义组件的代码。 此包中包含组件代码以及所需的任何JavaScript或CSS。 此包也嵌入了 **screens-weretail-run.core-0.0.1-SNAPSHOT.jar** ，其中包含项目所需的任何Java代码。

   >[!NOTE]
   >
   >在本教程中，不会编写Java代码。 如果需要更复杂的业务逻辑，可以使用核心Java包创建和部署后端Java。

   ![ui.apps代码在CRXDE Lite中的表示形式](/help/screens-cloud/developing/assets/uipps-contents.png)

   ui.apps代码在CRXDE Lite中的表示形式

   的 **螺旋世界** 组件当前只是占位符。 在本教程中，将添加允许作者更新组件显示的消息的功能。

1. 的 **screens-weretail-run.ui.content** 包安装代码如下：

   * `/conf/we-retail-run`
   * `/content/dam/we-retail-run`
   * `/content/screens/we-retail-run`

   此包包含项目所需的开始内容和配置结构。 **`/conf/we-retail-run`** 包含We.Retail Run项目的所有配置。 **`/content/dam/we-retail-run`** 包括为项目启动数字资产。 **`/content/screens/we-retail-run`** 包含Screens内容结构。 所有这些路径下方的内容主要在AEM中更新。 为了提高环境（本地、开发、暂存、生产）之间的一致性，通常在源代码管理中保存基本内容结构。

1. **导航到AEM Screens > We.Retail Run项目：**

   从AEM开始菜单>单击屏幕图标。 验证是否可以看到We.Retail运行项目。

   ![we-retaiul-run-starter](/help/screens-cloud/developing/assets/we-retaiul-run-starter.png)

## 创建Hello World组件 {#hello-world-cmp}

“Hello World”组件是一个简单的组件，允许用户输入要在屏幕上显示的消息。 组件基于 [AEM Screens组件模板：https://github.com/Adobe-Marketing-Cloud/aem-screens-component-template](https://github.com/Adobe-Marketing-Cloud/aem-screens-component-template).

AEM Screens存在一些有趣的限制，但传统WCM Sites组件未必存在这些限制。

* 大多数Screens组件需要在目标数字标牌设备上以全屏方式运行
* 大多数Screens组件需要嵌入到序列渠道中才能生成幻灯片
* 创作应允许在序列渠道中编辑各个组件，因此无需全屏渲染组件

1. 在 **CRXDE-Lite** `http://localhost:4502/crx/de/index.jsp` （或选择的IDE）导航到 `/apps/weretail-run/components/content/helloworld.`

   将以下属性添加到 `helloworld` 组件：

   ```
       jcr:title="Hello World"
       sling:resourceSuperType="foundation/components/parbase"
       componentGroup="We.Retail Run - Content"
   ```

   ![/apps/weretail-run/components/content/helloworld的属性](/help/screens-cloud/developing/assets/2018-04-28_at_4_23pm.png)

   /apps/weretail-run/components/content/helloworld的属性

   的 **螺旋世界** 组件 **foundation/components/parbase** 组件，以便在序列渠道中正确使用。

1. 在下方创建文件 `/apps/weretail-run/components/content/helloworld` 已命名 `helloworld.html.`

   使用以下内容填充文件：

   ```xml
   <!--/*
   
    /apps/weretail-run/components/content/helloworld/helloworld.html
   
   */-->
   
   <!--/* production: preview authoring mode + unspecified mode (i.e. on publish) */-->
   <sly data-sly-test.production="${wcmmode.preview || wcmmode.disabled}" data-sly-include="production.html" />
   
   <!--/* edit: any other authoring mode, i.e. edit, design, scaffolding, etc. */-->
   <sly data-sly-test="${!production}" data-sly-include="edit.html" />
   ```

   屏幕组件需要两种不同的渲染，具体取决于 [创作模式](https://helpx.adobe.com/experience-manager/6-4/sites/authoring/using/author-environment-tools.html#PageModes) 正在使用：

   1. **生产**:预览或发布模式(wcmmode=disabled)
   1. **编辑**:用于所有其他创作模式，例如编辑、设计、基架、开发人员……

   `helloworld.html`充当交换机，检查当前处于活动状态的创作模式并重定向到其他HTL脚本。 屏幕组件使用的常见约定是 `edit.html` 用于编辑模式的脚本和 `production.html` 脚本。

1. 在下方创建文件 `/apps/weretail-run/components/content/helloworld` 已命名 `production.html.`

   使用以下内容填充文件：

   ```xml
   <!--/*
    /apps/weretail-run/components/content/helloworld/production.html
   
   */-->
   
   <div data-duration="${properties.duration}" class="cmp-hello-world">
    <h1 class="cmp-hello-world__message">${properties.message}</h1>
   </div>
   ```

   上面是Hello World组件的生产标记。 A `data-duration` 属性，因为组件在序列渠道中使用。 的 `data-duration` 序列渠道使用属性来了解序列项目的显示时长。

   组件会呈现 `div` 和 `h1` 标记。 `${properties.message}` 是HTL脚本的一部分，该脚本将输出名为的JCR属性的内容 `message`. 稍后将创建一个对话框，允许用户为 `message` 属性文本。

   另请注意，组件使用BEM（块元素修饰符）符号。 BEM是一种CSS编码约定，可更轻松地创建可重用组件。 BEM是使用的符号 [AEM核心组件](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components/wiki/CSS-coding-conventions). <!-- WEBSITE WAS NOT ACCESSIBLE AS OF SEPTEMBER 1, 2022 More info can be found at: [https://getbem.com/](https://getbem.com/) -->

1. 在下方创建文件 `/apps/weretail-run/components/content/helloworld` 已命名 `edit.html.`

   使用以下内容填充文件：

   ```xml
   <!--/*
   
    /apps/weretail-run/components/content/helloworld/edit.html
   
   */-->
   
   <!--/* if message populated */-->
   <div
    data-sly-test.message="${properties.message}"
    class="aem-Screens-editWrapper cmp-hello-world">
    <p class="cmp-hello-world__message">${message}</p>
   </div>
   
   <!--/* empty place holder */-->
   <div data-sly-test="${!message}"
        class="aem-Screens-editWrapper cq-placeholder cmp-hello-world"
        data-emptytext="${'Hello World' @ i18n, locale=request.locale}">
   </div>
   ```

   上面是Hello World组件的编辑标记。 如果填充了对话框消息，则第一个块会显示组件的编辑版本。

   如果未输入对话框消息，则会呈现第二个块。 的 `cq-placeholder` 和 `data-emptytext` 呈现标签 ***《你好世界》*** 作为这种情况下的占位符。 为了支持在多个区域设置中进行创作，可以使用i18n将标签的字符串国际化。

1. **复制屏幕图像对话框以用于Hello World组件。**

   最简单的方法是从现有对话框开始，然后进行修改。

   1. 从以下位置复制对话框： `/libs/screens/core/components/content/image/cq:dialog`
   1. 在下方粘贴对话框 `/apps/weretail-run/components/content/helloworld`

   ![copy-image-dialog](/help/screens-cloud/developing/assets/copy-image-dialog.gif)

1. **更新“Hello World”对话框以包含消息的选项卡。**

   更新对话框，使其与以下内容匹配。 最终对话框的JCR节点结构以XML形式显示如下：

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0" xmlns:nt="https://www.jcp.org/jcr/nt/1.0"
       jcr:primaryType="nt:unstructured"
       jcr:title="Hello World"
       sling:resourceType="cq/gui/components/authoring/dialog">
       <content
           jcr:primaryType="nt:unstructured"
           sling:resourceType="granite/ui/components/coral/foundation/tabs"
           size="L">
           <items jcr:primaryType="nt:unstructured">
               <message
                   jcr:primaryType="nt:unstructured"
                   jcr:title="Message"
                   sling:resourceType="granite/ui/components/coral/foundation/fixedcolumns">
                   <items jcr:primaryType="nt:unstructured">
                       <column
                           jcr:primaryType="nt:unstructured"
                           sling:resourceType="granite/ui/components/coral/foundation/container">
                           <items jcr:primaryType="nt:unstructured">
                               <message
                                   jcr:primaryType="nt:unstructured"
                                   sling:resourceType="granite/ui/components/coral/foundation/form/textfield"
                                   fieldDescription="Message for component to display"
                                   fieldLabel="Message"
                                   name="./message"/>
                           </items>
                       </column>
                   </items>
               </message>
               <sequence
                   jcr:primaryType="nt:unstructured"
                   jcr:title="Sequence"
                   sling:resourceType="granite/ui/components/coral/foundation/fixedcolumns">
                   <items jcr:primaryType="nt:unstructured">
                       <column
                           jcr:primaryType="nt:unstructured"
                           sling:resourceType="granite/ui/components/coral/foundation/container">
                           <items jcr:primaryType="nt:unstructured">
                               <duration
                                   jcr:primaryType="nt:unstructured"
                                   sling:resourceType="granite/ui/components/coral/foundation/form/numberfield"
                                   defaultValue=""
                                   fieldDescription="Amount of time the image will be shown in the sequence, in milliseconds"
                                   fieldLabel="Duration (ms)"
                                   min="0"
                                   name="./duration"/>
                           </items>
                       </column>
                   </items>
               </sequence>
           </items>
       </content>
   </jcr:root>
   ```

   消息的文本字段将保存到名为 `message` 以及持续时间的number字段将保存到名为 `duration`. 这两个属性均在 `/apps/weretail-run/components/content/helloworld/production.html` 由HTL作为 `${properties.message}` 和 `${properties.duration}`.

   ![Hello World — 已完成对话框](/help/screens-cloud/developing/assets/2018-04-29_at_5_21pm.png)

   Hello World — 已完成对话框

## 创建客户端库 {#clientlibs}

客户端库提供了一种机制，用于组织和管理实施AEM所必需的CSS和JavaScript文件。

AEM Screens组件在编辑模式与预览/生产模式下的呈现方式不同。 将创建两个客户端库，一个用于编辑模式，另一个用于预览/生产。

1. 为Hello World组件的客户端库创建文件夹。

   下 `/apps/weretail-run/components/content/helloworld`创建名为 `clientlibs`.

   ![2018-04-30_at_1046am](/help/screens-cloud/developing/assets/2018-04-30_at_1046am.png)

1. 在 `clientlibs` 文件夹创建名为的新节点 `shared` 类型 `cq:ClientLibraryFolder.`

   ![2018-04-30_at_1115am](/help/screens-cloud/developing/assets/2018-04-30_at_1115am.png)

1. 将以下属性添加到共享客户端库：

   * `allowProxy` | 布尔型 | `true`

   * `categories`|字符串[] | `cq.screens.components`

   ![/apps/weretail-run/components/content/helloworld/clientlibs/shared的属性](/help/screens-cloud/developing/assets/2018-05-03_at_1026pm.png)

   /apps/weretail-run/components/content/helloworld/clientlibs/shared的属性

   类别属性是一个用于标识客户端库的字符串。 在“编辑”和“预览”/“生产”模式中，均使用cq.screens.components类别。 因此，在sharedclientlib中定义的任何CSS/JS都会在所有模式下加载。

   最佳做法是，切勿在生产环境中直接向/apps显示任何路径。 allowProxy属性可确保客户端库CSS和JS通过前缀of/etc.clientlibs引用。

1. 创建名为 `css.txt` 共享文件夹下方。

   使用以下内容填充文件：

   ```
   #base=css
   
   styles.less
   ```

1. 创建名为的文件夹 `css` 在 `shared` 文件夹。 添加名为 `style.less` 在 `css` 文件夹。 客户端库的结构现在应如下所示：

   ![2018-04-30_at_3_11pm](/help/screens-cloud/developing/assets/2018-04-30_at_3_11pm.png)

   本教程不使用LESS，而是直接编写CSS。 [LESS](https://lesscss.org/) 是一种常用的CSS预编译器，它支持CSS变量、混合和函数。 AEM客户端库本身支持LESS编译。 Sas或其他预编译器可以使用，但需要在AEM之外进行编译。

1. 填充 `/apps/weretail-run/components/content/helloworld/clientlibs/shared/css/styles.less` ，具有以下特点：

   ```css
   /**
       Shared Styles
      /apps/weretail-run/components/content/helloworld/clientlibs/shared/css/styles.less
   
   **/
   
   .cmp-hello-world {
       background-color: #fff;
   
    &__message {
     color: #000;
     font-family: Helvetica;
     text-align:center;
    }
   }
   ```

1. 复制并粘贴 `shared` 客户端库文件夹，用于创建名为 `production`.

   ![复制共享的客户端库以创建新的生产客户端库](/help/screens-cloud/developing/assets/copy-clientlib.gif)

   复制共享的客户端库以创建新的生产客户端库

1. 更新 `categories` 要 `cq.screens.components.production.`

   这可确保样式仅在“预览”/“生产”模式下加载。

   ![/apps/weretail-run/components/content/helloworld/clientlibs/production的属性](/help/screens-cloud/developing/assets/2018-04-30_at_5_04pm.png)

   /apps/weretail-run/components/content/helloworld/clientlibs/production的属性

1. 填充 `/apps/weretail-run/components/content/helloworld/clientlibs/production/css/styles.less` ，具有以下特点：

   ```css
   /**
       Production Styles
      /apps/weretail-run/components/content/helloworld/clientlibs/production/css/styles.less
   
   **/
   .cmp-hello-world {
   
       height: 100%;
       width: 100%;
       position: fixed;
   
    &__message {
   
     position: relative;
     font-size: 5rem;
     top:25%;
    }
   }
   ```

   以上样式将在屏幕中间显示消息，但仅在生产模式下显示。

第三个clientlibrary类别： `cq.screens.components.edit` 可用于向组件添加仅限编辑的特定样式。

| Clientlib类别 | 用途 |
|---|---|
| `cq.screens.components` | 在编辑模式和生产模式之间共享的样式和脚本 |
| `cq.screens.components.edit` | 仅在编辑模式下使用的样式和脚本 |
| `cq.screens.components.production` | 仅在生产模式中使用的样式和脚本 |

## 创建设计页面 {#design-page}

AEM Screens使用 [静态页面模板](https://helpx.adobe.com/cn/experience-manager/6-5/sites/developing/using/page-templates-static.html) 和 [设计配置](https://helpx.adobe.com/experience-manager/6-4/sites/authoring/using/default-components-designmode.html) ，以便进行全局更改。 设计配置通常用于在渠道上为Parsys配置允许的组件。 最佳实践是以特定于应用程序的方式存储这些配置。

在创建的We.Retail运行设计页面下，该页面将存储特定于We.Retail运行项目的所有配置。

1. 在 **CRXDE-Lite** `http://localhost:4502/crx/de/index.jsp#/apps/settings/wcm/designs` 导航到 `/apps/settings/wcm/designs`
1. 在designs文件夹下创建新节点，该节点名为 `we-retail-run` 具有 `cq:Page`.
1. 在 `we-retail-run` 页面，添加另一个名为 `jcr:content` 类型 `nt:unstructured`. 将以下属性添加到 `jcr:content` 节点：

   | 名称 | 类型 | 值 |
   |---|---|---|
   | jcr:title | 字符串 | We.Retail运行 |
   | sling:resourceType | 字符串 | wcm/core/components/designer |
   | cq:doctype | 字符串 | html_5 |

   ![位于/apps/settings/wcm/designs/we-retail-run的“设计”页面](/help/screens-cloud/developing/assets/2018-05-07_at_1219pm.png)

   位于/apps/settings/wcm/designs/we-retail-run的“设计”页面

## 创建序列渠道 {#create-sequence-channel}

“Hello World”组件将用于序列渠道。 要测试组件，将创建一个新的序列渠道。

1. 从AEM开始菜单导航到 **Screens** > **We.Retail Ru** n >选择 **渠道**.

1. 单击 **创建** 按钮

   1. 选择 **创建实体**

   ![2018-04-30_at_5_18pm](/help/screens-cloud/developing/assets/2018-04-30_at_5_18pm.png)

1. 在创建向导中：

1. 模板步骤 — 选择 **序列渠道**

   1. 属性步骤
   * 基本选项卡>标题= **空闲渠道**
   * “渠道”选项卡>选中 **使渠道联机**

   ![空闲渠道](/help/screens-cloud/developing/assets/idle-channel.gif)

1. 打开空闲渠道的页面属性。 更新“设计”字段以指向 `/apps/settings/wcm/designs/we-retail-run,`在上一部分中创建的设计页面。

   ![设计配置/apps/settings/wcm/designs/we-retail-run](/help/screens-cloud/developing/assets/2018-05-07_at_1240pm.png)

   指向/apps/settings/wcm/designs/we-retail-run的设计配置

1. 编辑新创建的空闲渠道以将其打开。

1. 将页面模式切换为 **设计** 模式

   1. 单击 **扳手** Parsys中用于配置允许的组件的图标

   1. 选择 **Screens** 及 **We.Retail运行 — 内容** 群组。

   ![2018-04-30_at_5_43pm](assets/2018-04-30_at_5_43pm.png)

1. 将页面模式切换为 **编辑**. 现在，可以将“Hello World”组件添加到页面中，并与其他序列渠道组件组合使用。

   ![2018-04-30_at_5_53pm](assets/2018-04-30_at_5_53pm.png)

1. 在 **CRXDE-Lite** `http://localhost:4502/crx/de/index.jsp#/apps/settings/wcm/designs/we-retail-run/jcr%3Acontent/sequencechannel/par` 导航到 `/apps/settings/wcm/designs/we-retail-run/jcr:content/sequencechannel/par`. 请注意 `components` 现在包含 `group:Screens`, `group:We.Retail Run - Content`.

   ![/apps/settings/wcm/designs/we-retail-run下的设计配置](/help/screens-cloud/developing/assets/2018-05-07_at_1_14pm.png)

   /apps/settings/wcm/designs/we-retail-run下的设计配置

## 自定义处理程序模板 {#custom-handlers}

如果您的自定义组件使用外部资源(如资产（图像、视频、字体、图标等）、特定资产演绎版或客户端库（css、js等），则这些资源不会自动添加到离线配置中，因为默认情况下，我们仅捆绑HTML标记。

为了让您自定义和优化下载到播放器的确切资产，我们为自定义组件提供了一个扩展机制，用于在Screens中显示它们对离线缓存逻辑的依赖关系。

以下部分显示了自定义离线资源处理程序的模板，以及 `pom.xml` 特定项目。

```java
package …;

import javax.annotation.Nonnull;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;
import org.apache.sling.api.resource.Resource;
import org.apache.sling.api.resource.ResourceUtil;
import org.apache.sling.api.resource.ValueMap;

import com.adobe.cq.screens.visitor.OfflineResourceHandler;

@Service(value = OfflineResourceHandler.class)
@Component(immediate = true)
public class MyCustomHandler extends AbstractResourceHandler {

 @Reference
 private …; // OSGi services injection

 /**
  * The resource types that are handled by the handler.
  * @return the handled resource types
  */
 @Nonnull
 @Override
 public String[] getSupportedResourceTypes() {
     return new String[] { … };
 }

 /**
  * Accept the provided resource, visit and traverse it as needed.
  * @param resource The resource to accept
  */
 @Override
 public void accept(@Nonnull Resource resource) {
     ValueMap properties = ResourceUtil.getValueMap(resource);
     
     /* You can directly add explicit paths for offline caching using the `visit`
        method of the visitor. */
     
     // retrieve a custom property from the component
     String myCustomRenditionUrl = properties.get("myCustomRenditionUrl", String.class);
     // adding that exact asset/rendition/path to the offline manifest
     this.visitor.visit(myCustomRenditionUrl);
     
     
     /* You can delegate handling for dependent resources so they are also added to
        the offline cache using the `accept` method of the visitor. */
     
     // retrieve a referenced dependent resource
     String referencedResourcePath = properties.get("myOtherResource", String.class);
     ResourceResolver resolver = resource.getResourceResolver();
     Resource referencedResource = resolver.getResource(referencedResourcePath);
     // let the handler for that resource handle it
     if (referencedResource != null) {
         this.visitor.accept(referencedResource);
     }
   }
}
```

以下代码提供了 `pom.xml` 对于该特定项目：

```css
   <dependencies>
        …
        <!-- Felix annotations -->
        <dependency>
            <groupId>org.apache.felix</groupId>
            <artifactId>org.apache.felix.scr.annotations</artifactId>
            <version>1.9.0</version>
            <scope>provided</scope>
        </dependency>

        <!-- Screens core bundle with OfflineResourceHandler/AbstractResourceHandler -->
        <dependency>
            <groupId>com.adobe.cq.screens</groupId>
            <artifactId>com.adobe.cq.screens</artifactId>
            <version>1.5.90</version>
            <scope>provided</scope>
        </dependency>
        …
      </dependencies>
```

## 融于一起 {#putting-it-all-together}

以下视频显示完成的组件以及如何将其添加到序列渠道。 然后，该渠道会添加到“位置”显示屏，并最终分配给Screens播放器。

>[!VIDEO](https://video.tv.adobe.com/v/22385?quaity=9)

## 完成的代码 {#finished-code}

以下是教程中完成的代码。 的 **screens-weretail-run.ui.apps-0.0.1-SNAPSHOT.zip** 和 **screens-weretail-run.ui.content-0.0.1-SNAPSHOT.zip** 是编译的AEM包。 **SRC-screens-weretail-run-0.0.1.zip **是未编译的源代码，可使用Maven部署。

[获取文件](/help/screens-cloud/developing/assets/screens-weretail-runuiapps-001-snapshot.zip)

[获取文件](/help/screens-cloud/developing/assets/screens-weretail-runuicontent-001-snapshot.zip)

[获取文件](/help/screens-cloud/developing/assets/screens-weretail-run.zip)
