---
title: 组件参考指南
description: 关于组件及其结构的详细信息的开发人员参考指南
translation-type: tm+mt
source-git-commit: f9a6dbec25b8154fda8069ff213aaaaa1d443ca1
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# 组件参考指南{#components-reference-guide}

组件是在AEM中构建体验的核心。 [核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html)和[AEM项目原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)使您能轻松开始使用一套现成、强大的组件。 [WKND Tutorial](/help/implementing/developing/introduction/develop-wknd-tutorial.md)将指导开发人员如何使用这些工具以及如何构建自定义组件以创建新的AEM站点。

>[!TIP]
>
>在引用此文档之前，请确保您已完成[WKND教程](/help/implementing/developing/introduction/develop-wknd-tutorial.md)，因此熟悉[核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html)和[AEM项目原型。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)

由于WKND教程涵盖大多数使用案例，因此此文档仅作为这些资源的补充。 它详细说明了组件在AEM中的结构和配置方式，不是作为入门指南提供的。

## 概述 {#overview}

本节介绍开发自己的组件时所需的详细信息，包括主要概念和问题。

### 规划 {#planning}

在开始实际配置或编码您的组件之前，您应该询问：

* 您到底需要新组件做什么？
* 您是需要从头开始创建组件，还是可以从现有组件继承基础知识？
* 您的组件是否需要选择/操作内容的逻辑？
   * 逻辑应与用户界面层分开。 HTL旨在帮助确保此情况发生。
* 您的组件是否需要CSS格式？
   * CSS格式应与组件定义分开。 定义命名HTML元素的约定，以便通过外部CSS文件修改它们。
* 您的新组件可能会带来哪些安全影响？

### 重用现有组件{#reusing-components}

在创建全新组件方面投入时间之前，请考虑自定义或扩展现有组件。 [核心组](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) 件提供一套灵活、强大且经过测试的生产就绪组件。

#### 扩展核心组件{#extending-core-components}

核心组件还优惠[清除自定义模式](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html)，您可以使用这些模式来调整它们以满足您自己项目的需要。

#### 覆盖组件{#overlying-components}

还可以基于搜索路径逻辑使用[overlay](/help/implementing/developing/introduction/overlays.md)重定义组件。 但是，在这种情况下，将不会触发[Sling资源合并](/help/implementing/developing/introduction/sling-resource-merger.md)，并且`/apps`必须定义整个叠加。

#### 扩展组件对话框{#extending-component-dialogs}

也可以使用Sling资源合并来覆盖组件对话框并定义属性`sling:resourceSuperType`。

这意味着您只需重定义所需的差异，而不是重定义整个对话框。

### 内容逻辑和渲染标记{#content-logic-and-rendering-markup}

组件将使用[HTML进行呈现。](https://www.w3schools.com/htmL/html_intro.asp) 您的组件需要定义需要的HTML，以便获取所需的内容，然后根据需要在创作和发布环境上呈现它。

建议将负责标记和渲染的代码与控制用于选择组件内容的逻辑的代码分开。

此理念得到[HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/using/overview.html)的支持，该模板语言被有意限制以确保使用真正的编程语言来定义底层业务逻辑。 此机制会突出显示为给定视图调用的代码，并根据需要允许为同一组件的不同视图使用特定逻辑。

此（可选）逻辑可以采用不同的方式实现，并可从HTL中调用特定命令：

* 使用Java - [HTL Java Use-API](https://helpx.adobe.com/experience-manager/htl/using/use-api-java.html)使HTL文件能够访问自定义Java类中的帮助方法。 这允许您使用Java代码实现用于选择和配置组件内容的逻辑。
* 使用JavaScript - [HTL JavaScript Use-API](https://experienceleague.adobe.com/docs/experience-manager-htl/using/htl/use-api-javascript.html)使HTL文件能够访问用JavaScript编写的帮助代码。 这允许您使用JavaScript代码实现用于选择和配置组件内容的逻辑。
* 使用客户端库 — 现代网站严重依赖由复杂JavaScript和CSS代码驱动的客户端处理。 有关详细信息，请参阅文档[将AEM上的客户端库用作Cloud Service](/help/implementing/developing/introduction/clientlibs.md)。

## 组件结构{#structure}

AEM组件的结构强大而灵活。 主要部分有：

* [资源类型](#resource-type)
* [组件定义](#component-definition)
* [组件的属性和子节点](#properties-and-child-nodes-of-a-component)
* [对话框](#dialogs)
* [设计对话框](#design-dialogs)

### 资源类型 {#resource-type}

结构的关键元素是资源类型。

* 内容结构声明意图。
* 资源类型将实现这些类型。

这是一个抽象，有助于确保即使外观随着时间而改变，意图也保持不变。

### 组件定义{#component-definition}

组件的定义可以按如下方式划分：

* AEM组件基于[Sling。](https://sling.apache.org/documentation.html)
* AEM组件位于`/libs/core/wcm/components`下。
* 项目/站点特定组件位于`/apps/<myApp>/components`下。
* AEM标准组件定义为`cq:Component`，并具有以下关键元素：
   * jcr属性 — jcr属性的列表。 这些是变量，某些是可选的，但组件节点、其属性和子节点的基本结构由`cq:Component`定义定义。
   * 资源 — 这些资源定义组件使用的静态元素。
   * 脚本 — 这些脚本用于实现组件的结果实例的行为。

#### 重要属性{#vital-properties}

* **根节点**:
   * `<mycomponent> (cq:Component)`  — 组件的层次结构节点。
* **重要属性**:
   * `jcr:title`  — 组件标题；例如，当组件在组件浏览器和组件控制台中列出时， [将](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser) 用作 [标签](/help/sites-cloud/authoring/features/components-console.md)
   * `jcr:description`  — 组件说明；用作组件浏览器和组件控制台中的鼠标悬停提示
   * 有关详细信息，请参阅[组件图标](#component-icon)部分
* **重要子节点**:
   * `cq:editConfig (cq:EditConfig)`  — 定义组件的编辑属性，并使组件显示在组件浏览器中
      * 如果组件包含对话框，则它将自动显示在组件浏览器或Sidekick中，即使cq:editConfig不存在也是如此。
   * `cq:childEditConfig (cq:EditConfig)`  — 控制未定义其自身的子组件的创作UI方面 `cq:editConfig`。
   * `cq:dialog (nt:unstructured)`  — 此组件的对话框。定义允许用户配置组件和/或编辑内容的界面。
   * `cq:design_dialog (nt:unstructured)`  — 设计编辑此组件

#### 组件图标{#component-icon}

当开发人员创建组件时，组件的图标或缩写是通过组件的JCR属性定义的。 这些属性按以下顺序计算，并使用找到的第一个有效属性。

1. `cq:icon`  — 指向要在组件浏览器中显示的Coral UI库 [中标](https://opensource.adobe.com/coral-spectrum/examples/#icon) 准图标的字符串属性
   * 使用Coral图标的HTML属性值。
1. `abbreviation` - String属性，用于自定义组件浏览器中组件名称的缩写
   * 缩写应限于两个字符。
   * 如果提供空字符串，将从`jcr:title`属性的前两个字符生成缩写。
      * 例如，“Image”的“Im”
      * 本地化标题将用于构建缩写。
   * 仅当组件具有`abbreviation_commentI18n`属性时，缩写才被翻译，然后该属性用作翻译提示。
1. `cq:icon.png` 或 —  `cq:icon.svg` 此组件的图标，显示在组件浏览器中
   * 20 x 20像素是标准组件图标的大小。
      * 将缩小较大的图标（客户端）。
   * 建议的颜色为rgb(112, 112, 112)> #707070
   * 标准组件图标的背景是透明的。
   * 仅支持`.png`和`.svg`文件。
   * 如果通过Eclipse插件从文件系统导入，则文件名需要转义为`_cq_icon.png`或`_cq_icon.svg`。
   * `.png` 如果两者都 `.svg` 存在，就会先例。

如果在组件上找不到上述属性（`cq:icon`、`abbreviation`、`cq:icon.png`或`cq:icon.svg`）：

* 系统将在超级组件上搜索与`sling:resourceSuperType`属性后相同的属性。
* 如果在超级组件级别找不到任何缩写或空缩写，则系统将从当前组件的`jcr:title`属性的第一个字母构建缩写。

要取消超级组件中图标的继承，在组件上设置空`abbreviation`属性将恢复为默认行为。

[组件控制台](/help/sites-cloud/authoring/features/components-console.md#component-details)显示如何定义特定组件的图标。

#### SVG图标示例{#svg-icon-example}

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

### 组件{#properties-and-child-nodes-of-a-component}的属性和子节点

定义组件所需的许多节点/属性对于两种UI都是通用的，其中差异保持独立，这样您的组件就可以在两种环境中工作。

组件是`cq:Component`类型的节点，具有以下属性和子节点：

| 名称 | 类型 | 描述 |
|---|---|---|
| `.` | `cq:Component` | 这表示当前组件。 组件的节点类型为`cq:Component`。 |
| `componentGroup` | `String` | 这表示在[组件浏览器中可以选择组件的组。](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser) 以开始的值用 `.` 于无法从UI中选择的组件，如从其他组件继承的基本组件。 |
| `cq:isContainer` | `Boolean` | 这表示该组件是否为容器组件，因此可以包含段落系统等其他组件。 |
| `cq:dialog` | `nt:unstructured` | 这是组件的编辑对话框的定义。 |
| `cq:design_dialog` | `nt:unstructured` | 这是组件的设计对话框的定义。 |
| `cq:editConfig` | `cq:EditConfig` | 这定义组件的[编辑配置。](#edit-behavior) |
| `cq:htmlTag` | `nt:unstructured` | 这将返回添加到周围HTML标签的其他标签属性。 允许向自动生成的显示添加属性。 |
| `cq:noDecoration` | `Boolean` | 如果为true，则不使用自动生成的div和css类呈现组件。 |
| `cq:template` | `nt:unstructured` | 如果找到，则当从组件浏览器添加组件时，此节点将用作内容模板。 |
| `jcr:created` | `Date` | 这是组件的创建日期。 |
| `jcr:description` | `String` | 这是组件的说明。 |
| `jcr:title` | `String` | 这是组件的标题。 |
| `sling:resourceSuperType` | `String` | 设置后，组件会从此组件继承内容。 |
| `component.html` | `nt:file` | 这是组件的HTL脚本文件。 |
| `cq:icon` | `String` | 此值指向组件](#component-icon)的[图标，并显示在组件浏览器中。 |

如果我们查看&#x200B;**Text**&#x200B;组件，可以看到以下许多元素：

![文本组件结构](assets/components-text.png)

特定权益物业包括：

* `jcr:title`  — 这是用于在组件浏览器中标识组件的组件标题。
* `jcr:description`  — 这是组件的说明。
* `sling:resourceSuperType`  — 这表示在扩展组件（通过覆盖定义）时继承的路径。

特别感兴趣的子节点包括：

* `cq:editConfig`  — 此操作控制编辑时组件的可视方面。
* `cq:dialog`  — 这定义用于编辑此组件内容的对话框。
* `cq:design_dialog`  — 它指定此组件的设计编辑选项。

### 对话框 {#dialogs}

对话框是组件的关键元素，因为它们为作者提供了一个界面，用于在内容页面上配置组件并提供该组件的输入。 有关内容作者如何与组件交互的详细信息，请参阅[创作文档](/help/sites-cloud/authoring/fundamentals/editing-content.md)。

根据组件的复杂性，您的对话框可能需要一个或多个选项卡。

AEM组件的对话框：

* 是`cq:dialog`类型`nt:unstructured`的节点。
* 位于其`cq:Component`节点下，并位于其组件定义旁。
* 定义用于编辑此组件内容的对话框。
* 使用Granite UI组件进行定义。
* 根据内容结构和`sling:resourceType`属性呈现服务器端（作为Sling组件）。
* 包含描述对话框中字段的节点结构
   * 这些节点是`nt:unstructured`，具有必需的`sling:resourceType`属性。

![标题组件的对话框定义](assets/components-title-dialog.png)

在对话框中，定义了单个字段：

![标题组件的对话框定义字段](assets/components-title-dialog-items.png)

### 设计对话框{#design-dialogs}

设计对话框类似于用于编辑和配置内容的对话框，但它们为模板作者提供了界面，以便在页面模板上对该组件进行专业配置并提供设计详细信息。 然后，内容作者使用页面模板创建内容页面。 有关如何创建模板的详细信息，请参阅[模板文档](/help/sites-cloud/authoring/features/templates.md)。

[编辑页面模板时使用设计对话框](/help/sites-cloud/authoring/features/templates.md)，但并非所有组件都需要设计对话框。例如，**标题**&#x200B;和&#x200B;**图像组件**&#x200B;都具有设计对话框，而&#x200B;**社交媒体共享组件**&#x200B;则不具有设计对话框。

### Coral UI和Granite UI {#coral-and-granite}

Coral UI和Granite UI定义AEM的外观。

* [Coral UI可](https://opensource.adobe.com/coral-spectrum/documentation/) 在所有云解决方案中提供一致的UI。
* [Granite UI](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html) 提供打包到Sling组件中的Coral UI标记，用于构建UI控制台和对话框。

Granite UI提供了在创作环境上创建对话框所需的大量基本构件。 必要时，您可以扩展此选择并创建您自己的Widget。

有关其他详细信息，请参阅以下资源：

* [AEM UI的结构](/help/implementing/developing/introduction/ui-structure.md)

### 自定义对话框字段{#customizing-dialog-fields}

>[!TIP]
>
>有关自定义对话框字段的信息，请参阅[AEM Gems会话](https://docs.adobe.com/content/ddc/en/gems/customizing-dialog-fields-in-touch-ui.html)。

要创建在组件对话框中使用的新Widget，需要创建新的Granite UI字段组件。

如果您将对话框视为表单元素的简单容器，则还可以将对话框内容的主要内容作为表单域查看。 创建新表单字段需要创建资源类型；这等同于创建新组件。 为了帮助您在该任务中完成工作，Granite UI将优惠一个要继承的通用字段组件（使用`sling:resourceSuperType`）：

`/libs/granite/ui/components/coral/foundation/form/field`

更具体地说，Granite UI提供了一系列字段组件，这些组件适合在对话框中使用，或更一般地以[形式使用。](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/form/index.html)

创建资源类型后，可以通过在对话框中添加新节点来实例化字段，属性`sling:resourceType`引用您刚引入的资源类型。

#### 访问对话框字段{#access-to-dialog-fields}

您还可以使用渲染条件(`rendercondition`)来控制谁有权访问对话框中的特定选项卡/字段；例如：

```text
+ mybutton
  - sling:resourceType = granite/ui/components/coral/foundation/button
  + rendercondition
    - sling:resourceType = myapp/components/renderconditions/group
    - groups = ["administrators"]
```

## 使用组件{#using-components}

创建组件后，您需要启用它才能使用它。 使用它可显示组件结构与存储库中生成内容的结构之间的关系。

### 将组件添加到模板{#adding-your-component-to-the-template}

定义组件后，必须使组件可供使用。 要使组件可在模板中使用，必须在模板的布局容器策略中启用该组件。

有关如何创建模板的详细信息，请参阅[模板文档](/help/sites-cloud/authoring/features/templates.md)。

### 组件及其创建的{#components-and-the-content-they-create}内容

如果我们在页面上创建并配置&#x200B;**Title**&#x200B;组件的实例：`/content/wknd/language-masters/en/adventures/extreme-ironing.html`

![标题编辑对话框](assets/components-title-dialog.png)

然后，我们可以看到在存储库中创建的内容的结构：

![标题组件节点结构](assets/components-title-content-nodes.png)

尤其是，如果您查看&#x200B;**标题组件**&#x200B;的实际文本：

* 内容包含一个`jcr:title`属性，其中包含作者输入的标题的实际文本。
* 它还包含对组件定义的`sling:resourceType`引用。

定义的属性取决于各个定义。 尽管它们可能比之前更为复杂，但它们仍遵循相同的基本原则。

## 组件层次和继承{#component-hierarchy-and-inheritance}

AEM中的组件受&#x200B;**资源类型层次结构**&#x200B;的约束。 这用于使用属性`sling:resourceSuperType`扩展组件。 这允许组件继承其他组件。

有关详细信息，请参阅[重用组件](#reusing-components)一节。

## 编辑行为{#edit-behavior}

本节介绍如何配置组件的编辑行为。 这包括可用于组件的操作、in.place编辑器的特性以及与组件上的事件相关的侦听器等属性。

通过在组件节点（`cq:Component`类型）下添加`cq:editConfig`类型`cq:EditConfig`的节点，并添加特定属性和子节点，配置组件的编辑行为。 以下属性和子节点可用：

* `cq:editConfig` 节点属性
* [`cq:editConfig` 子节点](#configuring-with-cq-editconfig-child-nodes):
   * `cq:dropTargets` (节点类 `nt:unstructured`型):定义放置列表目标，可接受内容查找器资产中的放置操作(允许单个放置目标)
   * `cq:inplaceEditing` (节点类 `cq:InplaceEditingConfig`型):为组件定义就地编辑配置
   * `cq:listeners` (节点类 `cq:EditListenersConfig`型):定义在组件上执行操作之前或之后发生的情况

AEM中有许多现有配置。 使用&#x200B;**CRXDE Lite**&#x200B;中的查询工具，可以轻松搜索特定属性或子节点。

### 组件占位符{#component-placeholders}

组件必须始终呈现作者可见的某些HTML，即使组件没有内容也是如此。 否则，它可能会从编辑器的界面中以可视方式消失，从而使它在技术上存在，但在页面和编辑器中不可见。 在这种情况下，作者将无法选择空组件并与之交互。

因此，当页面在页面编辑器中呈现时（当WCM模式为`edit`或`preview`时），组件应呈现占位符，只要它们不呈现任何可见输出。
占位符的典型HTML标记如下：

```HTML
<div class="cq-placeholder" data-emptytext="Component Name"></div>
```

呈现上述占位符HTML的典型HTL脚本如下：

```HTML
<div class="cq-placeholder" data-emptytext="${component.properties.jcr:title}"
     data-sly-test="${(wcmmode.edit || wcmmode.preview) && isEmpty}"></div>
```

在上例中，`isEmpty`是一个变量，仅当组件没有内容且作者不可见时才为true。

为避免重复，Adobe建议组件实施者为这些占位符使用HTL模板，[与核心组件提供的模板类似。](https://github.com/adobe/aem-core-wcm-components/blob/master/content/src/content/jcr_root/apps/core/wcm/components/commons/v1/templates.html)

然后，使用以下HTL行来使用上一个链接中的模板：

```HTML
<sly data-sly-use.template="core/wcm/components/commons/v1/templates.html"
     data-sly-call="${template.placeholder @ isEmpty=!model.text}"></sly>
```

在上例中，`model.text`是仅当内容包含内容且可见时才为true的变量。

可在核心组件[中查看此模板的示例使用情况，如标题组件。](https://github.com/adobe/aem-core-wcm-components/blob/master/content/src/content/jcr_root/apps/core/wcm/components/title/v2/title/title.html#L27)

### 使用cq:EditConfig子节点{#configuring-with-cq-editconfig-child-nodes}进行配置

#### 将资产拖入对话框 — cq:dropTargets {#cq-droptargets}

`cq:dropTargets`节点（节点类型`nt:unstructured`）定义了放置目标，该放置模式可以接受从内容查找器中拖动的资产中的放置。 它是`cq:DropTargetConfig`类型的节点。

类型`cq:DropTargetConfig`的子节点定义组件中的放置目标。

### 就地编辑 — cq:inplace编辑{#cq-inplaceediting}

就地编辑器允许用户直接在内容流中编辑内容，无需打开对话框。 例如，标准&#x200B;**Text**&#x200B;和&#x200B;**Title**&#x200B;组件都具有内置编辑器。

对于每个组件类型，就地编辑器并非必需/有意义。

`cq:inplaceEditing`节点（节点类型`cq:InplaceEditingConfig`）为组件定义就地编辑配置。 它可以具有以下属性：

| 属性名称 | 属性类型 | 属性值 |
|---|---|---|
| `active` | `Boolean` | `true` 以启用组件的就地编辑。 |
| `configPath` | `String` | 编辑器配置的路径，可由配置节点指定 |
| `editorType` | `String` | 可用类型有：`plaintext`对于非HTML内容，`title`在开始编辑之前将图形标题转换为纯文本，`text`使用富文本编辑器 |

以下配置启用组件的嵌入式编辑并将`plaintext`定义为编辑器类型：

```text
    <cq:inplaceEditing
        jcr:primaryType="cq:InplaceEditingConfig"
        active="{Boolean}true"
        editorType="plaintext"/>
```

### 处理字段事件- cq:listeners {#cq-listeners}

处理对话框字段事件的方法是使用自定义[客户端库中的侦听器。](/help/implementing/developing/introduction/clientlibs.md)

要将逻辑插入字段，您应：

* 将您的字段标记为给定的CSS类（挂接）。
* 在客户端库中定义一个挂接到该CSS类名的JS侦听器（这可确保您的自定义逻辑仅作用于您的字段，且不影响同一类型的其他字段）。

要实现此目的，您需要了解要与之交互的基础Widget库。 [请参阅Coral UI文](https://opensource.adobe.com/coral-spectrum/documentation/) 档，以确定要对哪个事件做出响应。

`cq:listeners`节点（节点类型`cq:EditListenersConfig`）定义在组件上执行操作之前或之后发生的情况。 下表定义了其可能的属性。

| 属性名称 | 属性值 |
|---|---|
| `beforedelete` | 在删除组件之前触发该处理函数。 |
| `beforeedit` | 在编辑组件之前将触发该处理函数。 |
| `beforecopy` | 在复制组件之前触发处理函数。 |
| `beforeremove` | 在移动组件之前触发处理函数。 |
| `beforeinsert` | 在插入组件之前触发处理函数。 |
| `beforechildinsert` | 该处理函数是在组件插入另一个组件之前触发的(仅容器)。 |
| `afterdelete` | 该处理函数在删除组件后触发。 |
| `afteredit` | 编辑组件后将触发该处理函数。 |
| `aftercopy` | 该处理函数在复制组件后触发。 |
| `afterinsert` | 插入组件后将触发处理函数。 |
| `aftermove` | 处理函数在移动组件后触发。 |
| `afterchildinsert` | 该处理函数是在组件插入另一个组件后触发的(仅容器)。 |

>[!NOTE]
>
>对于嵌套组件，对于定义为`cq:listeners`节点上属性的操作有一些限制。 对于嵌套组件，以下属性&#x200B;**的值必须**&#x200B;为`REFRESH_PAGE`:
>
>* `aftermove`
>* `aftercopy`


事件处理函数可通过自定义实现实现。 例如（其中`project.customerAction`是静态方法）：

`afteredit = "project.customerAction"`

下面的示例等效于`REFRESH_INSERTED`配置：

`afterinsert="function(path, definition) { this.refreshCreated(path, definition); }"`

使用以下配置，在删除、编辑、插入或移动组件后刷新页面：

```text
    <cq:listeners
        jcr:primaryType="cq:EditListenersConfig"
        afterdelete="REFRESH_PAGE"
        afteredit="REFRESH_PAGE"
        afterinsert="REFRESH_PAGE"
        afterMove="REFRESH_PAGE"/>
```

### 字段验证{#field-validation}

使用`foundation-validation` API可以在Granite UI和Granite UI构件中执行字段验证。 有关详细信息，请参阅[`foundation-valdiation` Granite文档](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/clientlibs/foundation/js/validation/index.html)。

### 检测对话框{#dialog-ready}的可用性

如果您有自定义JavaScript，只有在对话框可用且准备就绪时才需要执行，则应侦听`dialog-ready`事件。

当对话框加载（或重新加载）并准备使用时，将触发此事件，这意味着当对话框的DOM中发生更改（创建/更新）时。

`dialog-ready` 可用于在JavaScript自定义代码中挂接，该代码对对话框或类似任务中的字段执行自定义。

## 预览行为{#preview-behavior}

切换到预览模式时，即使页面未刷新，也会设置[ WCM模式](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/wcm/api/WCMMode.html) Cookie。

对于呈现对WCM模式敏感的组件，需要定义这些组件以具体刷新它们，然后依赖Cookie的值。

## 正在记录组件{#documenting-components}

作为开发人员，您需要轻松访问组件文档，以便快速了解组件的：

* 描述
* 预期用途
* 内容结构和属性
* 暴露的API和扩展点
* 等等

因此，很容易将组件本身中可用的任何现有文档标记设置为可用。

您只需将`README.md`文件放入组件结构中。

![组件结构中的README.md](assets/components-documentation.png)

此标记随后将显示在[组件控制台中。](/help/sites-cloud/authoring/features/components-console.md)

![README.md在组件控制台中可见](assets/components-documentation-console.png)

支持的标记与[内容片段的标记相同。](/help/assets/content-fragments/content-fragments.md)