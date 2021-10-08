---
title: 组件参考指南
description: 有关组件及其结构的详细信息的开发人员参考指南
exl-id: 45e5265b-39d6-4a5c-be1a-e66bb7ea387d
source-git-commit: c08e442e58a4ff36e89a213aa7b297b538ae3bab
workflow-type: tm+mt
source-wordcount: '3659'
ht-degree: 1%

---

# 组件参考指南 {#components-reference-guide}

组件是在AEM中构建体验的核心。 通过[核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hans)和[AEM项目原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)，可轻松开始使用一组现成的强大组件。 [WKND Tutorial](/help/implementing/developing/introduction/develop-wknd-tutorial.md)向开发人员介绍如何使用这些工具以及如何构建自定义组件以创建新的AEM站点。

>[!TIP]
>
>在引用本文档之前，请确保您已完成[WKND Tutorial](/help/implementing/developing/introduction/develop-wknd-tutorial.md)，并因此熟悉[核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html)和[AEM项目原型。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)

由于WKND教程涵盖大多数用例，因此本文档仅作为这些资源的补充。 本指南详细介绍了组件在AEM中的结构和配置方式，不是入门指南。

## 概述 {#overview}

本节介绍一些关键概念和问题，并介绍开发您自己的组件时所需的详细信息。

### 规划 {#planning}

在开始实际配置或编码组件之前，您应该先询问：

* 您到底需要新组件执行哪些操作？
* 您是需要从头开始创建组件，还是可以从现有组件继承基础知识？
* 您的组件是否需要逻辑才能选择/操作内容？
   * 逻辑应与用户界面层分开。 HTL旨在帮助确保实现此目的。
* 您的组件是否需要CSS格式？
   * CSS格式应与组件定义分开。 定义命名HTML元素的约定，以便您能够通过外部CSS文件修改它们。
* 您的新组件可能会引入哪些安全影响？

### 重用现有组件 {#reusing-components}

在花时间创建全新组件之前，请考虑自定义或扩展现有组件。 [核心组](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) 件提供了一套灵活、强大且经过良好测试的生产就绪型组件。

#### 扩展核心组件 {#extending-core-components}

核心组件还提供[清除自定义模式](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html)，您可以使用这些模式根据您自己项目的需求进行调整。

#### 将组件覆盖 {#overlying-components}

组件也可基于搜索路径逻辑通过[覆盖](/help/implementing/developing/introduction/overlays.md)重定义。 但是，在这种情况下，将不会触发[Sling资源合并器](/help/implementing/developing/introduction/sling-resource-merger.md)，并且`/apps`必须定义整个叠加。

#### 扩展组件对话框 {#extending-component-dialogs}

还可以使用Sling资源合并器覆盖组件对话框，并定义属性`sling:resourceSuperType`。

这表示您只需重定义所需的差异，而不需要重定义整个对话框。

### 内容逻辑和渲染标记  {#content-logic-and-rendering-markup}

组件将以[HTML呈现。](https://www.w3schools.com/htmL/html_intro.asp) 您的组件需要定义获取所需内容所需的HTML，然后在创作和发布环境中根据需要进行渲染。

建议将负责标记和渲染的代码与用于控制组件内容选择逻辑的代码分开。

[HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/using/overview.html?lang=zh-Hans)支持此理念，它是一种模板语言，经过刻意限制，可确保使用真正的编程语言来定义底层业务逻辑。 此机制会突出显示为给定视图调用的代码，并在必要时，允许对同一组件的不同视图使用特定逻辑。

此（可选）逻辑可以通过不同方式实现，并可通过特定命令从HTL中调用：

* 使用Java - [HTL Java Use-API](https://helpx.adobe.com/experience-manager/htl/using/use-api-java.html)使HTL文件能够访问自定义Java类中的Helper方法。 这允许您使用Java代码实施用于选择和配置组件内容的逻辑。
* 使用JavaScript - [HTL JavaScript Use-API](https://experienceleague.adobe.com/docs/experience-manager-htl/using/htl/use-api-javascript.html)使HTL文件能够访问使用JavaScript编写的帮助程序代码。 这允许您使用JavaScript代码实施用于选择和配置组件内容的逻辑。
* 使用客户端库 — 现代网站严重依赖由复杂JavaScript和CSS代码驱动的客户端处理。 有关更多信息，请参阅文档[在AEMas a Cloud Service上使用客户端库](/help/implementing/developing/introduction/clientlibs.md) 。

## 组件结构 {#structure}

AEM组件的结构强大而灵活。 主要部分包括：

* [资源类型](#resource-type)
* [组件定义](#component-definition)
* [组件的属性和子节点](#properties-and-child-nodes-of-a-component)
* [对话框](#dialogs)
* [设计对话框](#design-dialogs)

### 资源类型 {#resource-type}

结构的一个关键元素是资源类型。

* 内容结构声明意图。
* 资源类型将实施它们。

这是一个抽象，有助于确保即使外观随时间而改变，意图也会保持不变。

### 组件定义 {#component-definition}

组件的定义可按如下方式划分：

* AEM组件基于[Sling.](https://sling.apache.org/documentation.html)
* AEM组件位于`/libs/core/wcm/components`下。
* 项目/站点特定组件位于`/apps/<myApp>/components`下。
* AEM标准组件定义为`cq:Component`，且具有关键元素：
   * jcr属性 — jcr属性的列表。 这些是变量，有些是可选的，但组件节点、其属性和子节点的基本结构由`cq:Component`定义定义。
   * 资源 — 这些资源定义组件使用的静态元素。
   * 脚本 — 这些脚本用于实施组件生成实例的行为。

#### 重要属性 {#vital-properties}

* **根节点**:
   * `<mycomponent> (cq:Component)`  — 组件的层次结构节点。
* **重要属性**:
   * `jcr:title`  — 组件标题；例如，当组件在组件浏览器和组件控制台中列出时， [会](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser) 用作 [标签](/help/sites-cloud/authoring/features/components-console.md)
   * `jcr:description`  — 组件说明；在组件浏览器和组件控制台中用作鼠标悬停提示
   * 有关详细信息，请参阅[组件图标](#component-icon)部分
* **重要子节点**:
   * `cq:editConfig (cq:EditConfig)`  — 定义组件的编辑属性，并使组件显示在组件浏览器中
      * 如果组件具有对话框，则它将自动显示在组件浏览器或Sidekick中，即使cq:editConfig不存在也是如此。
   * `cq:childEditConfig (cq:EditConfig)`  — 控制未定义其自身的子组件的创作UI方 `cq:editConfig`面。
   * `cq:dialog (nt:unstructured)`  — 此组件的对话框。定义允许用户配置组件和/或编辑内容的界面。
   * `cq:design_dialog (nt:unstructured)`  — 编辑此组件的设计

#### 组件图标 {#component-icon}

组件的图标或缩写是在开发人员创建组件时，通过组件的JCR属性来定义的。 这些属性将按以下顺序计算，并使用找到的第一个有效属性。

1. `cq:icon`  — 字符串属性，指向要在组件浏览器中 [显示](https://opensource.adobe.com/coral-spectrum/examples/#icon) 的Coral UI库中的标准图标
   * 使用Coral图标的HTML属性值。
1. `abbreviation`  — 用于自定义组件浏览器中组件名称的缩写的字符串属性
   * 缩写应限制为两个字符。
   * 如果提供空字符串，则将从`jcr:title`属性的前两个字符生成缩写。
      * 例如，“Image”的“Im”
      * 将使用本地化的标题来构建缩写。
   * 仅当组件具有`abbreviation_commentI18n`属性时，缩写才会被翻译，该属性随后会用作翻译提示。
1. `cq:icon.png` 或 —  `cq:icon.svg` 此组件的图标，该图标显示在组件浏览器中
   * 20 x 20像素是标准组件的图标大小。
      * 大图标的大小将会缩小（客户端）。
   * 推荐颜色为rgb(112, 112, 112)> #707070
   * 标准组件图标的背景是透明的。
   * 仅支持`.png`和`.svg`文件。
   * 如果通过Eclipse插件从文件系统导入，则文件名需要转义为`_cq_icon.png`或`_cq_icon.svg`。
   * `.png` 如果两者都 `.svg` 存在，就会先例。

如果在组件上找不到上述属性（`cq:icon`、`abbreviation`、`cq:icon.png`或`cq:icon.svg`）：

* 系统将在超级组件上搜索与`sling:resourceSuperType`属性后面的相同属性。
* 如果在超级组件级别中未找到任何缩写或空缩写，则系统将从当前组件`jcr:title`属性的前几个字母构建缩写。

要取消超级组件中图标的继承，在组件上设置空`abbreviation`属性将还原为默认行为。

[组件控制台](/help/sites-cloud/authoring/features/components-console.md#component-details)显示特定组件图标的定义方式。

#### SVG图标示例 {#svg-icon-example}

```xml
<?xml version="1.0" encoding="utf-8"?>
<!DOCTYPE svg PUBLIC "-//W3C//DTD SVG 1.1//EN" "https://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd">
<svg version="1.1" id="Layer_1" xmlns="https://www.w3.org/2000/svg" xmlns:xlink="https://www.w3.org/1999/xlink" x="0px" y="0px"
     width="20px" height="20px" viewBox="0 0 20 20" enable-background="new 0 0 20 20" xml:space="preserve">
    <ellipse cx="5" cy="5" rx="3" ry="3" fill="#707070"/>
    <ellipse cx="15" cy="5" rx="4" ry="4" fill="#707070"/>
    <ellipse cx="5" cy="15" rx="5" ry="5" fill="#707070"/>
    <ellipse cx="15" cy="15" rx="4" ry="4" fill="#707070"/>
</svg>
```

### 组件的属性和子节点 {#properties-and-child-nodes-of-a-component}

定义组件所需的许多节点/属性对于两个UI都是通用的，其中差异仍保持独立，因此您的组件可以在这两个环境中工作。

组件是`cq:Component`类型的节点，具有以下属性和子节点：

| 名称 | 类型 | 描述 |
|---|---|---|
| `.` | `cq:Component` | 这表示当前组件。 组件的节点类型为`cq:Component`。 |
| `componentGroup` | `String` | 这表示在[组件浏览器中可以选择组件的组。](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser) 以开头的值 `.` 用于无法从UI中进行选择的组件，例如其他组件从中继承的基本组件。 |
| `cq:isContainer` | `Boolean` | 这表示组件是否是容器组件，因此可以包含段落系统等其他组件。 |
| `cq:dialog` | `nt:unstructured` | 这是组件的编辑对话框的定义。 |
| `cq:design_dialog` | `nt:unstructured` | 这是组件的设计对话框的定义。 |
| `cq:editConfig` | `cq:EditConfig` | 这定义组件的[编辑配置。](#edit-behavior) |
| `cq:htmlTag` | `nt:unstructured` | 这会返回添加到周围标记的其他标记属性HTML。 允许向自动生成的div中添加属性。 |
| `cq:noDecoration` | `Boolean` | 如果为true，则组件不会呈现为自动生成的div和css类。 |
| `cq:template` | `nt:unstructured` | 如果找到，则当从组件浏览器添加组件时，此节点将用作内容模板。 |
| `jcr:created` | `Date` | 这是组件的创建日期。 |
| `jcr:description` | `String` | 这是组件的描述。 |
| `jcr:title` | `String` | 这是组件的标题。 |
| `sling:resourceSuperType` | `String` | 设置后，组件会从此组件继承内容。 |
| `component.html` | `nt:file` | 这是组件的HTL脚本文件。 |
| `cq:icon` | `String` | 此值指向组件](#component-icon)的[图标，并显示在组件浏览器中。 |

如果我们查看&#x200B;**Text**&#x200B;组件，可以看到以下许多元素：

![文本组件结构](assets/components-text.png)

特定权益的物业包括：

* `jcr:title`  — 这是用于在组件浏览器中标识组件的组件标题。
* `jcr:description`  — 此为组件的描述。
* `sling:resourceSuperType`  — 这表示扩展组件（通过覆盖定义）时的继承路径。

特定感兴趣的子节点包括：

* `cq:editConfig`  — 此操作可在编辑时控制组件的可视化方面。
* `cq:dialog`  — 这定义用于编辑此组件内容的对话框。
* `cq:design_dialog`  — 这可指定此组件的设计编辑选项。

### 对话框 {#dialogs}

对话框是组件的关键元素，因为它们为作者提供了一个界面，用于在内容页面上配置组件并提供该组件的输入。 有关内容作者如何与组件进行交互的详细信息，请参阅[创作文档](/help/sites-cloud/authoring/fundamentals/editing-content.md)。

根据组件的复杂性，对话框可能需要一个或多个选项卡。

AEM组件的对话框：

* 是`nt:unstructured`类型的`cq:dialog`节点。
* 位于其`cq:Component`节点下，且位于其组件定义旁边。
* 定义用于编辑此组件内容的对话框。
* 使用Granite UI组件进行定义。
* 根据组件的内容结构和`sling:resourceType`属性，在服务器端呈现（作为Sling组件）。
* 包含描述对话框中字段的节点结构
   * 这些节点是`nt:unstructured`，且属性为必需的`sling:resourceType`。

![标题组件的对话框定义](assets/components-title-dialog.png)

在对话框中，定义了各个字段：

![标题组件的对话框定义字段](assets/components-title-dialog-items.png)

### 设计对话框 {#design-dialogs}

设计对话框与用于编辑和配置内容的对话框类似，但它们为模板作者提供了界面，用于在页面模板上预配置和提供该组件的设计详细信息。 然后，内容作者使用页面模板来创建内容页面。 有关如何创建模板的详细信息，请参阅[模板文档](/help/sites-cloud/authoring/features/templates.md)。

[编辑页面模板时会使用设计对话框](/help/sites-cloud/authoring/features/templates.md)，但并非所有组件都需要设计对话框。例如，**标题**&#x200B;和&#x200B;**图像组件**&#x200B;都具有设计对话框，而&#x200B;**社交媒体共享组件**&#x200B;则没有。

### Coral用户界面和Granite用户界面 {#coral-and-granite}

Coral用户界面和Granite用户界面可定义AEM的外观。

* [Coral UI为](https://opensource.adobe.com/coral-spectrum/documentation/) 所有云解决方案提供了一致的UI。
* [Granite UI](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html) 提供了封装在Sling组件中的Coral UI标记，用于构建UI控制台和对话框。

Granite UI提供了在创作环境中创建对话框所需的一系列基本小组件。 必要时，您可以扩展此选择并创建自己的小组件。

有关更多详细信息，请参阅以下资源：

* [AEM UI的结构](/help/implementing/developing/introduction/ui-structure.md)

### 自定义对话框字段 {#customizing-dialog-fields}

<!--
Content not found

>[!TIP]
>
>See the [AEM Gems session](https://docs.adobe.com/content/ddc/en/gems/customizing-dialog-fields-in-touch-ui.html) on customizing dialog fields.
-->

要创建在组件对话框中使用的新小组件，需要创建新的Granite UI字段组件。

如果将对话框视为表单元素的简单容器，则还可以将对话框内容的主要内容视为表单字段。 创建新表单字段需要创建资源类型；这等同于创建新组件。 为了帮助您完成该任务，Granite UI提供了一个要从中继承的通用字段组件（使用`sling:resourceSuperType`）：

`/libs/granite/ui/components/coral/foundation/form/field`

更具体地说，Granite UI提供了一系列字段组件，这些组件适合在对话框中使用，或者通常在[表单中使用。](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/form/index.html)

创建资源类型后，您可以通过在对话框中添加新节点来实例化字段，该节点的属性`sling:resourceType`引用了您刚才引入的资源类型。

#### 对对话框字段的访问权限 {#access-to-dialog-fields}

您还可以使用渲染条件(`rendercondition`)来控制谁有权访问对话框中的特定选项卡/字段；例如：

```text
+ mybutton
  - sling:resourceType = granite/ui/components/coral/foundation/button
  + rendercondition
    - sling:resourceType = myapp/components/renderconditions/group
    - groups = ["administrators"]
```

## 使用组件 {#using-components}

创建组件后，您需要启用该组件才能使用它。 使用它可显示组件结构与存储库中生成内容的结构有何关系。

### 将组件添加到模板 {#adding-your-component-to-the-template}

定义组件后，必须使其可供使用。 要使组件可在模板中使用，必须在模板布局容器的策略中启用该组件。

有关如何创建模板的详细信息，请参阅[模板文档](/help/sites-cloud/authoring/features/templates.md)。

### 组件及其创建的内容 {#components-and-the-content-they-create}

如果在页面上创建并配置&#x200B;**Title**&#x200B;组件的实例：`/content/wknd/language-masters/en/adventures/extreme-ironing.html`

![标题编辑对话框](assets/components-title-dialog.png)

然后，我们可以看到在存储库中创建的内容的结构：

![标题组件节点结构](assets/components-title-content-nodes.png)

特别是，如果您查看&#x200B;**标题组件**&#x200B;的实际文本：

* 内容包含`jcr:title`属性，该属性包含作者输入的标题的实际文本。
* 它还包含对组件定义的`sling:resourceType`引用。

定义的属性取决于各个定义。 尽管它们可能比上面更复杂，但它们仍遵循相同的基本原则。

## 组件层次结构和继承 {#component-hierarchy-and-inheritance}

AEM中的组件受&#x200B;**资源类型层次结构**&#x200B;的约束。 用于使用属性`sling:resourceSuperType`扩展组件。 这允许组件继承其他组件。

有关更多信息，请参阅[重用组件](#reusing-components)一节。

## 编辑行为 {#edit-behavior}

本节介绍如何配置组件的编辑行为。 这包括一些属性，例如组件可用的操作、in.place编辑器的特性，以及与组件上的事件相关的侦听器。

组件的编辑行为通过以下方法进行配置：在组件节点（`cq:Component`类型）下添加`cq:editConfig`类型的节点，并添加特定属性和子节点。 `cq:EditConfig`以下属性和子节点可用：

* `cq:editConfig` 节点属性
* [`cq:editConfig` 子节点](#configuring-with-cq-editconfig-child-nodes):
   * `cq:dropTargets` (节点类 `nt:unstructured`型):定义可以接受内容查找器资产中删除的放置目标列表（允许单个放置目标）
   * `cq:inplaceEditing` (节点类 `cq:InplaceEditingConfig`型):为组件定义就地编辑配置
   * `cq:listeners` (节点类 `cq:EditListenersConfig`型):定义在组件上执行操作之前或之后发生的情况

AEM中现有的配置很多。 使用&#x200B;**CRXDE Lite**&#x200B;中的“查询”工具，可以轻松搜索特定属性或子节点。

### 组件占位符 {#component-placeholders}

组件必须始终呈现一些对作者可见的HTML，即使组件没有内容也是如此。 否则，它可能会从编辑器的界面中以可视方式消失，从而使其在技术上呈现，但在页面和编辑器中却不可见。 在这种情况下，作者将无法选择空组件并与之进行交互。

因此，只要组件在页面编辑器中呈现页面时（当WCM模式为`edit`或`preview`时）不呈现任何可见输出，组件就应呈现占位符。
占位符的典型HTML标记如下所示：

```HTML
<div class="cq-placeholder" data-emptytext="Component Name"></div>
```

呈现上述占位符HTML的典型HTL脚本如下所示：

```HTML
<div class="cq-placeholder" data-emptytext="${component.properties.jcr:title}"
     data-sly-test="${(wcmmode.edit || wcmmode.preview) && isEmpty}"></div>
```

在上一个示例中，`isEmpty`是一个变量，仅当组件没有内容且作者不可见时，该变量才为true。

为避免重复，Adobe建议组件实施者为这些占位符使用HTL模板， [类似于核心组件提供的模板。](https://github.com/adobe/aem-core-wcm-components/blob/master/content/src/content/jcr_root/apps/core/wcm/components/commons/v1/templates.html)

然后，使用以下HTL行完成模板在上一个链接中的使用：

```HTML
<sly data-sly-use.template="core/wcm/components/commons/v1/templates.html"
     data-sly-call="${template.placeholder @ isEmpty=!model.text}"></sly>
```

在上一个示例中，`model.text`是仅当内容包含且可见时才为true的变量。

此模板的用法示例可在核心组件[中查看，如标题组件中。](https://github.com/adobe/aem-core-wcm-components/blob/master/content/src/content/jcr_root/apps/core/wcm/components/title/v2/title/title.html#L27)

### 使用cq:EditConfig子节点配置 {#configuring-with-cq-editconfig-child-nodes}

#### 将资产放入对话框 — cq:dropTargets {#cq-droptargets}

`cq:dropTargets`节点（节点类型`nt:unstructured`）定义了可接受从内容查找器中拖动的资产中拖放的放置目标。 它是`cq:DropTargetConfig`类型的节点。

类型`cq:DropTargetConfig`的子节点定义组件中的放置目标。

### 就地编辑 — cq:inplaceEditing {#cq-inplaceediting}

就地编辑器允许用户直接在内容流中编辑内容，而无需打开对话框。 例如，标准的&#x200B;**Text**&#x200B;和&#x200B;**Title**&#x200B;组件都具有嵌入式编辑器。

对于每种组件类型，并非都需要/有意义的就地编辑器。

`cq:inplaceEditing`节点（节点类型`cq:InplaceEditingConfig`）为组件定义就地编辑配置。 它可以具有以下属性：

| 属性名称 | 属性类型 | 属性值 |
|---|---|---|
| `active` | `Boolean` | `true` 以启用组件的就地编辑。 |
| `configPath` | `String` | 编辑器配置的路径，可由配置节点指定 |
| `editorType` | `String` | 可用类型包括：`plaintext`对于非HTML内容，`title`在开始编辑之前将图形标题转换为纯文本，`text`使用富文本编辑器 |

以下配置允许对组件进行内置编辑，并将`plaintext`定义为编辑器类型：

```text
    <cq:inplaceEditing
        jcr:primaryType="cq:InplaceEditingConfig"
        active="{Boolean}true"
        editorType="plaintext"/>
```

### 处理字段事件 — cq:listeners {#cq-listeners}

在自定义[客户端库中，对对话框字段中的事件进行处理的方法已通过侦听器完成。](/help/implementing/developing/introduction/clientlibs.md)

要在字段中插入逻辑，您应：

* 使用给定的CSS类（挂接）标记字段。
* 在客户端库中定义一个挂接到该CSS类名称的JS侦听器（这可确保自定义逻辑的范围仅限您的字段，并且不会影响其他相同类型的字段）。

要实现此目的，您需要了解要与之交互的底层小组件库。 [请参阅Coral用户](https://opensource.adobe.com/coral-spectrum/documentation/) 界面文档，以确定要对哪个事件做出响应。

`cq:listeners`节点（节点类型`cq:EditListenersConfig`）定义在对组件执行操作之前或之后所发生的情况。 下表定义了其可能的属性。

| 属性名称 | 属性值 |
|---|---|
| `beforedelete` | 处理程序在删除组件之前触发。 |
| `beforeedit` | 处理程序在编辑组件之前触发。 |
| `beforecopy` | 在复制组件之前触发处理程序。 |
| `beforeremove` | 在移动组件之前触发处理程序。 |
| `beforeinsert` | 在插入组件之前触发处理程序。 |
| `beforechildinsert` | 在将组件插入其他组件（仅限容器）之前，会触发处理程序。 |
| `afterdelete` | 处理程序在删除组件后触发。 |
| `afteredit` | 编辑组件后会触发处理程序。 |
| `aftercopy` | 处理程序在复制组件后触发。 |
| `afterinsert` | 在插入组件后触发处理程序。 |
| `aftermove` | 处理程序在组件移动后触发。 |
| `afterchildinsert` | 将组件插入另一个组件（仅限容器）后，将触发处理程序。 |

>[!NOTE]
>
>对于嵌套的组件，对于定义为`cq:listeners`节点上属性的操作有一些限制。 对于嵌套的组件，以下属性&#x200B;**的值必须**&#x200B;为`REFRESH_PAGE`:
>
>* `aftermove`
>* `aftercopy`


事件处理程序可以通过自定义实施来实施。 例如（其中`project.customerAction`是静态方法）：

`afteredit = "project.customerAction"`

以下示例等效于`REFRESH_INSERTED`配置：

`afterinsert="function(path, definition) { this.refreshCreated(path, definition); }"`

通过以下配置，在删除、编辑、插入或移动组件后会刷新页面：

```text
    <cq:listeners
        jcr:primaryType="cq:EditListenersConfig"
        afterdelete="REFRESH_PAGE"
        afteredit="REFRESH_PAGE"
        afterinsert="REFRESH_PAGE"
        afterMove="REFRESH_PAGE"/>
```

### 字段验证 {#field-validation}

可使用`foundation-validation` API在Granite UI和Granite UI小组件中完成字段验证。 有关详细信息，请参阅[`foundation-valdiation` Granite文档](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/clientlibs/foundation/js/validation/index.html)。

### 检测对话框的可用性 {#dialog-ready}

如果您有一个自定义JavaScript，该JavaScript需要仅在对话框可用且准备就绪时才执行，则应该侦听`dialog-ready`事件。

当对话框加载（或重新加载）并准备就绪以供使用时，将触发此事件，这意味着每当对话框的DOM中发生更改（创建/更新）时。

`dialog-ready` 可用于挂接JavaScript自定义代码，该代码可对对话框或类似任务中的字段执行自定义。

## 预览行为 {#preview-behavior}

切换到预览模式时，即使页面未刷新，也会设置[WCM模式](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/wcm/api/WCMMode.html) Cookie。

对于呈现的对WCM模式敏感的组件，需要定义它们以专门刷新它们，然后依赖Cookie的值。

## 记录组件 {#documenting-components}

作为开发人员，您希望轻松访问组件文档，以便快速了解组件的以下功能：

* 描述
* 预期用途
* 内容结构和属性
* 公开的API和扩展点
* 等等

因此，很容易就会在组件中使用您现有的任何文档标记。

您只需在组件结构中放置一个`README.md`文件即可。

![组件结构中的README.md](assets/components-documentation.png)

然后，此标记将显示在[组件控制台中。](/help/sites-cloud/authoring/features/components-console.md)

![组件控制台中显示README.md](assets/components-documentation-console.png)

支持的标记与[内容片段的标记相同。](/help/assets/content-fragments/content-fragments.md)
