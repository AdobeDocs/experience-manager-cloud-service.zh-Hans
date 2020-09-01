---
title: 页面模板
description: 页面模板用于创建将用作新页面基础的页面
translation-type: tm+mt
source-git-commit: 0799a817095558edd49b53ddc915c9474181fef7
workflow-type: tm+mt
source-wordcount: '3244'
ht-degree: 7%

---


# 页面模板 {#page-templates}

创建页面时，您需要选择模板。 页面模板用作新页面的基础。 模板可定义生成页面的结构、任何初始内容以及可使用的组件（设计属性）。这具有以下几个优点：

* 页面模板允许专业作者创 [建和编辑模板](/help/sites-cloud/authoring/features/templates.md)。
   * 此类专业作者称为模 **板作者**
   * 模板作者必须是组的成 `template-authors` 员。
* 页面模板可保留与通过它们创建的任何页面的动态连接。 这可确保模板的任何更改都反映在页面本身中。
* 页面模板使页面组件更加通用，因此无需自定义即可使用核心页面组件。

使用页面模板，可以在组件中隔离生成页面的部分。 您可以在UI中配置组件的必要组合，从而无需为每个页面变体开发新的页面组件。

本文档：

* 概述创建页面模板
* 描述创建可编辑模板所需的管理员／开发人员任务
* 描述可编辑模板的技术基础
* 描述AEM如何评估模板的可用性

>[!NOTE]
>
>此文档假定您已经熟悉创建和编辑模板。 请参阅创作文档 [创建页面模板](/help/sites-cloud/authoring/features/templates.md)，该模板详细介绍了模板作者可编辑模板的功能。

>[!TIP]
>
>[WKND教程通过实](/help/implementing/developing/introduction/develop-wknd-tutorial.md) 施示例深入介绍了如何使用页面模板，对于了解如何在新项目中设置模板非常有用

## Creating a New Template {#creating-a-new-template}

创建页面模板主要由模板作者 [使用模板控制台和模板](/help/sites-cloud/authoring/features/templates.md) 编辑器来完成。 本节概述了此过程，并随后介绍了在技术层面发生的情况。

创建新的可编辑模板时，您需要执行以下步骤：

1. 为模 [板创建文件夹](#template-folders)。 这不是强制性的，但建议采用最佳实践。
1. 选择模 [板类型](#template-type)。 复制此模板以创建 [模板定义](#template-definitions)。

   >[!NOTE]
   >
   >现成提供模板类型选项。 您还可以根 [据需要创建自己的站点特定模板类](#creating-template-types) 型。

1. 配置新模板的结构、内容策略、初始内容和布局。

   **结构**

   * 该结构允许您为模板定义组件和内容。
   * 不能在生成页面上移动在模板结构中定义的组件，也不能从任何生成页面中删除这些组件。
   * 如果要使页面作者能够添加和删除组件，请在模板中添加段落系统。
   * 可以解锁组件，然后再将其锁定，以便定义初始内容。

   有关模板作者如何定义结构的详细信息，请参阅 [创建页面模板](/help/sites-cloud/authoring/features/templates.md#editing-a-template-structure-template-author)。

   有关结构的技术详细信息，请参 [阅此文档](#structure) 中的“结构”。

   **策略**

   * 内容策略定义组件的设计属性。

      * 例如，可用的组件或最小/最大尺寸。
   * 这些属性适用于模板（和使用模板创建的页面）。

   有关模板作者如何定义策略的详细信息，请参 [阅创建页面模板](/help/sites-cloud/authoring/features/templates.md#editing-a-template-structure-template-author)。

   有关策略的技术详细信息，请参 [阅此文档](#content-policies) 中的内容策略。

   **初始内容**

   * 初始内容定义首次根据模板创建页面时将显示的内容。
   * 初始内容随后可由页面作者编辑。

   有关模板作者如何定义结构的详细信息，请参阅 [创建页面模板](/help/sites-cloud/authoring/features/templates.md#editing-a-template-initial-content-author)。

   有关初始内容的技术详细信息，请 [参阅此文档](#initial-content) 中的初始内容。

   **布局**

   * 您可以为各种设备定义模板布局。
   * 模板的响应式布局与页面创作时的响应式布局功能相同。

   有关模板作者如何定义模板布局的详细信息，请参阅 [创建页面模板](/help/sites-cloud/authoring/features/templates.md#editing-a-template-layout-template-author)。

   有关模板布局的技术详细信息，请参 [阅此文档](#layout) 中的布局。

1. 启用模板，然后为特定内容树允许它。

   * 可以启用或禁用模板，以使其对页面作者可用或不可用。
   * 可以使模板可用于或不可用于某些页面分支。

   有关模板作者如何启用模板的详细信息，请参阅创 [建页面模板](/help/sites-cloud/authoring/features/templates.md#enabling-and-allowing-a-template-template-author)。

   有关启用模板的技术详细信息，请 [参阅启用和允许在此文档](#enabling-and-allowing-a-template-for-use)中使用模板

1. 使用它创建内容页面。

   * 使用静态模板和可编辑的模板创建新页面的过程没有明显的区别，也没有孰优孰劣之分。
   * 对于页面作者而言，该创建过程一目了然。

   有关页面作者如何使用模板创建页面的详细信息，请参 [阅创建和组织页面](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#templates)。

   有关使用可编辑模板创建页面的技术详细信息，请 [参阅此文档中的](#resultant-content-pages) “生成内容页面”。

>[!NOTE]
>
>编辑器客户端库假定内容页 `cq.shared` 面中存在命名空间，如果不存在，则将 `Uncaught TypeError: Cannot read property 'shared' of undefined` 导致JavaScript错误。
>
>所有示例内容页面都 `cq.shared`包含，因此基于这些页面的任何内容都会自动 `cq.shared`包含。 但是，如果您决定从头开始创建自己的内容页面，而不是基于示例内容，则必须确保包含 `cq.shared` 命名空间。

<!--See [Using Client-Side Libraries](/help/sites-developing/clientlibs.md) for further information.-->

>[!CAUTION]
>
>切勿在模板中输入任何需要国际化的信息。

## 模板文件夹 {#template-folders}

要组织模板，您可以使用以下文件夹：

* `global`
* 站点特定

>[!NOTE]
>
>即使您可以嵌套文件夹，当用户在“模板”控制台中视图文 **件夹** 时，它们也会显示为平面结构。

In a standard AEM instance the `global` folder already exists in the template console. 此文件夹会保存默认模板，如果在当前文件夹中没有找到策略和/或模板类型，则此文件夹可以充当备用。您可以将默认模板添加到此文件夹或创建新文件夹（推荐）。

>[!NOTE]
>
>最好创建一个新文件夹来保存您的自定义模板，而不使用该文 `global` 件夹。

>[!CAUTION]
>
>文件夹必须由具有权限的用户 `admin` 创建。

模板类型和策略会按照以下优先顺序继承到所有文件夹：

1. 当前文件夹
1. 当前文件夹的父级
1. `/conf/global`
1. `/apps`
1. `/libs`

将创建所有允许条目的列表。 如果任何配置重 `path`叠( `label`/)，则只向用户显示最接近当前文件夹的实例。

要创建新文件夹，您可以执行以下操作之一：

* 以编程方式或通过CRXDE Lite
* 使用配置浏览器

## 使用CRXDE Lite {#using-crxde-lite}

1. 可以通过编程或CRXDE Lite为实例创建新文件夹（在/conf下）。

   必须使用以下结构：

   ```xml
   /conf
       <your-folder-name> [sling:Folder]
           settings [sling:Folder]
               wcm [cq:Page]
                   templates [cq:Page]
                   policies [cq:Page]
   ```

1. 然后，您可以在文件夹根节点上定义以下属性：

   `<your-folder-name> [sling:Folder]`

   * 名称: `jcr:title`
   * 类型: `String`
   * 值：要显示在“模板”控制台中的标题(用于 **文件夹** )。

1. 除了标准创作权限和权限(例如， `content-authors`)，您现在需要为作者分配组并定义所需的访问权限(ACL)，以便在新文件夹中创建模板。

   组 `template-authors` 是需要分配的默认组。 有关详细信息， [请参阅ACL](#acls-and-groups) 和组一节。

   <!--See [Access Right Management](/help/sites-administering/user-group-ac-admin.md#access-right-management) for full details on managing and assigning access rights.-->

### 使用配置浏览器 {#using-the-configuration-browser}

1. 转到“全 **局导航** ”-> **“工具** ” **>“配**&#x200B;置浏览器”。

   现有文件夹将列在左侧，包括该文 `global` 件夹。

1. 单击&#x200B;**创建**。
1. 在创 **建配置** 对话框中，需要配置以下字段：

   * **标题**:提供配置文件夹的标题
   * **可编辑模板**:勾号，允许在此文件夹内创建可编辑的模板

1. Click **Create**

>[!NOTE]
>
>在配置浏览器中，如果您希望在该文件夹内创建模板，可以编辑 **全局文件夹** ，并激活“可编辑模板”选项，但建议不要这样做。

### ACL和组 {#acls-and-groups}

在创建模板文件夹（通过CRXDE或使用配置浏览器）后，必须为模板文件夹的相应组定义ACL，以确保适当的安全性。

WKND教程的模 [板文件夹](/help/implementing/developing/introduction/develop-wknd-tutorial.md) ，可以作为示例。

#### 模板作者组 {#the-template-authors-group}

组 `template-authors` 是用于管理模板访问权限的组，它是AEM的标准组，但为空。 必须将用户添加到项目／站点的组。

>[!CAUTION]
>
>该 `template-authors` 用户组仅适用于必须能够创建新模板的用户。
>
>编辑模板功能非常强大，如果不能正确编辑，现有模板就会损坏。 因此，该角色应集中并仅包括合格用户。

下表详细列出了进行模板编辑所需的权限。

<table>
 <tbody>
  <tr>
   <th>路径</th>
   <th>角色／组</th>
   <th>权限<br /> </th>
   <th>描述</th>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/&lt;<i>your-folder</i>&gt;/settings/wcm/templates</code></td>
   <td>模板作者<br /> </td>
   <td>读、写、复制</td>
   <td>在站点特定空间中创建、读取、更新、删除和复制模板的模板作 <code>/conf</code> 者</td>
  </tr>
  <tr>
   <td>匿名Web用户</td>
   <td>读</td>
   <td>匿名Web用户在呈现页面时必须阅读模板</td>
  </tr>
  <tr>
   <td>内容作者</td>
   <td>复制</td>
   <td>replicateContent作者在激活页面时需要激活页面的模板</td>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/&lt;<i>your-folder</i>&gt;/settings/wcm/policies</code></td>
   <td><code>Template Author</code></td>
   <td>读、写、复制</td>
   <td>在站点特定空间中创建、读取、更新、删除和复制模板的模板作 <code>/conf</code> 者</td>
  </tr>
  <tr>
   <td>匿名Web用户</td>
   <td>读</td>
   <td>匿名Web用户在呈现页面时必须阅读策略</td>
  </tr>
  <tr>
   <td>内容作者</td>
   <td>复制</td>
   <td>内容作者在激活页面时需要激活页面模板的策略</td>
  </tr>
  <tr>
   <td rowspan="2"><code>/conf/&lt;site&gt;/settings/template-types</code></td>
   <td>模板作者</td>
   <td>读</td>
   <td>模板作者根据预定义的模板类型之一创建新模板。</td>
  </tr>
  <tr>
   <td>匿名Web用户</td>
   <td>无</td>
   <td>匿名Web用户不能访问模板类型</td>
  </tr>
 </tbody>
</table>

此默认 `template-authors` 组仅涵盖项目设置，所有成员 `template-authors` 都可以访问和创作所有模板。 对于更复杂的设置，在这些设置中，需要多个模板作者组才能单独访问模板，必须创建更多自定义模板作者组。 但是，模板作者组的权限将保持不变。

## Template Type {#template-type}

创建新模板时，您需要指定模板类型：

* 模板类型有效地为模板提供模板。 创建新模板时，将使用所选模板类型的结构和初始内容创建新模板。

   * 将复制模板类型以创建模板。
   * 复制完成后，模板与模板类型之间的唯一连接就是静态引用，供参考。

* 模板类型允许您定义：

   * 页面组件的资源类型。
   * 根节点的策略，它定义模板编辑器中允许的组件。
   * 建议在模板类型上为响应式网格和移动模拟器的设置定义断点。 这是可选的，因为配置也可以在单个模板上定义(请参阅模 [板类型和移动设备组](#p-template-type-and-mobile-device-groups-br-p))。

* AEM提供一些现成的模板类型选项，如HTML5页面和自适应表单页面。

   * WKND教程中提供了其他 [示例。](/help/implementing/developing/introduction/develop-wknd-tutorial.md)

* 模板类型通常由开发人员定义。

现成模板类型存储在以下位置：

* `/libs/settings/wcm/template-types`

>[!CAUTION]
>
>您不得更改路径中的任 `/libs` 何内容。 这是因为对AEM的更 `/libs` 新可以随时覆盖其内容。

站点特定的模板类型应存储在以下可比位置：

* `/apps/settings/wcm/template-types`

自定义模板类型的定义应存储在用户定义的文件夹（推荐）中，或者存储在中 `global`。 例如：

* `/conf/<my-folder-01>/<my-folder-02>/settings/wcm/template-types`
* `/conf/<my-folder>/settings/wcm/template-types`
* `/conf/global/settings/wcm/template-types`

>[!CAUTION]
>
>模板类型必须遵循正确的文件夹结构(即 `/settings/wcm/...`)，否则将找不到模板类型。

<!--
### Template Type and Mobile Device Groups {#template-type-and-mobile-device-groups-br}

The [device groups](/help/sites-developing/mobile.md#device-groups) used for an editable template (set as relative path of the property `cq:deviceGroups`) define which mobile devices are available as emulators in the [layout mode](/help/sites-authoring/responsive-layout.md) of page authoring. This value can be set in two places:

* On the editable template type
* On the editable template

When creating a new editable template, the value is copied from the template type to the individual template. If the value is not set on the type, it can be set on the template. Once a template is created, there is no inheritance from the type to the template.

>[!CAUTION]
>
>The value of `cq:deviceGroups` must be set as a relative path such as `mobile/groups/responsive` and not as an absolute path such as `/etc/mobile/groups/responsive`.

>[!NOTE]
>
>With static templates /help/sites-developing/page-templates-static.md, the value of `cq:deviceGroups` could be set at the root of the site.
>
>With editable templates, this value is now stored at the template level and is not supported at the page root level.
-->

### 创建模板类型 {#creating-template-types}

如果已创建可用作其他模板基础的模板，则可以将此模板复制为模板类型。

1. 按照此处所述创建模板，以 [便创建任何页面](/help/sites-cloud/authoring/features/templates.md#creating-a-new-template-template-author)模板，它将作为模板类型的基础。
1. 使用CRXDE Lite，将新创建的模板从节点 `templates` 复制到模板 `template-types` 文件夹下 [的节点](#template-folders)。
1. 从模板文件夹下 `templates` 的节点中 [删除模板](#template-folders)。
1. 在节点下的模板副本中，删 `template-types` 除所有属 `cq:template` 性 `cq:templateType``jcr:content` 和属性。

您还可以根据GitHub提供的示例可编辑模板，开发您自己的模板类型。

GITHUB上的代码

您可以在GitHub上找到此页面的代码

* [在GitHub上打开aem-sites-example-custom-template-type项目](https://github.com/Adobe-Marketing-Cloud/aem-sites-example-custom-template-type)
* 以ZIP文件的 [形式下载项目](https://github.com/Adobe-Marketing-Cloud/aem-sites-example-custom-template-type/archive/master.zip)

## 模板定义 {#template-definitions}

可编辑模板的定义存储 [在用户定义的文件夹](#template-folders) （推荐）中，或者 `global`在。 例如：

* `/conf/<my-folder>/settings/wcm/templates`
* `/conf/<my-folder-01>/<my-folder-02>/settings/wcm/templates`
* `/conf/global/settings/wcm/templates`

模板的根节点的类型为 `cq:Template` 骨架结构：

```xml
<template-name>
  initial
    jcr:content
      root
        <component>
        ...
        <component>
  jcr:content
    @property status
  policies
    jcr:content
      root
        @property cq:policy
        <component>
          @property cq:policy
        ...
        <component>
          @property cq:policy
  structure
    jcr:content
      root
        <component>
        ...
        <component>
      cq:responsive
        breakpoints
  thumbnail.png
```

主要元素有：

* `<template-name>`

   * ` [initial](#initial-content)`
   * `jcr:content`
   * ` [structure](#structure)`
   * ` [policies](#policies)`
   * `thumbnail.png`

### jcr:content {#jcr-content}

此节点包含模板的属性：

* **名称**: `jcr:title`
* **名称**: `status`
   * ``**类型**: `String`
   * **值**: `draft`, `enabled` or `disabled`

### 结构 {#structure}

定义生成页面的结构：

* 在创建新页面时，与 `/initial`初始内容()合并。
* 对结构所做的更改将反映在使用模板创建的任何页面中。
* ( `root` )节 `structure/jcr:content/root`点定义将在生成页面中可用的组件的列表。
   * 在模板结构中定义的组件不能移动到任何生成页面或从任何生成页面中删除。
   * 解锁组件后， `editable` 属性将设置为 `true`。
   * 解锁已包含内容的组件后，此内容将移到分 `initial` 支。

* 该节 `cq:responsive` 点保存响应式布局的定义。

### 初始内容 {#initial-content}

定义新页面在创建时将包含的初始内容：

* 包含复 `jcr:content` 制到任何新页面的节点。
* 创建新页面时 `/structure`与结构()合并。
* 如果初始内容在创建后发生更改，则不会更新任何现有页面。
* 节 `root` 点包含一列表组件，用于定义在生成页面中可用的组件。
* 如果内容以结构模式添加到组件，并且该组件随后被解锁（反之亦然），则此内容将用作初始内容。

### 布局 {#layout}

编辑 [模板时，您可以定义布局](/help/sites-cloud/authoring/features/templates.md)，这会使 [用标准响应式布局](/help/sites-cloud/authoring/features/responsive-layout.md)。

<!-- that can also be [configured](/help/sites-administering/configuring-responsive-layout.md). -->

### Content Policies {#content-policies}

内容策略定义组件的设计属性。 例如，可用的组件或最小/最大尺寸。这些属性适用于模板（和使用模板创建的页面）。可以在模板编辑器中创建和选择内容策略。

* 节点 `cq:policy`上的属 `root` 性
   `/conf/<your-folder>/settings/wcm/templates/<your-template>/policies/jcr:content/root`
为页面的段落系统提供对内容策略的相对引用。

* 属性位 `cq:policy`于组件显式节点下， `root`提供指向各个组件策略的链接。

* 实际策略定义存储在：
   `/conf/<your-folder>/settings/wcm/policies/wcm/foundation/components`

>[!NOTE]
>
>策略定义的路径取决于组件的路径。 `cq:policy` 保存对配置本身的相对引用。

### 页面策略 {#page-policies}

页面策略允许您在模 [板或生成页](#content-policies) 面中为页面（主parsys）定义内容策略。

### 启用和允许使用模板 {#enabling-and-allowing-a-template-for-use}

1. **启用模板**

   必须通过以下任一方式启用模板才能使用模板：

   * [从“模板](/help/sites-cloud/authoring/features/templates.md#enablingatemplateauthor) ”控制台 **启用模** 板。

   * 设置节点上的状态 `jcr:content` 属性。

      * 例如，在：
         `/conf/<your-folder>/settings/wcm/templates/<your-template>/jcr:content`

      * 定义属性：

         * 名称：状态
         * 类型：字符串
         * 值: `enabled`

1. **允许的模板**

   * [在子分支的相应页面或根页 **面的**](/help/sites-cloud/authoring/features/templates.md#allowing-a-template-author) “页面属性”中定义允许的模板路径。
   * 设置属性：
      `cq:allowedTemplates`
在 
`jcr:content` 所需分支的节点。
   例如，值为：

   `/conf/<your-folder>/settings/wcm/templates/.*`

## 生成内容页面 {#resultant-content-pages}

从可编辑模板创建的页面：

* 是使用从模板中合并的子 `structure` 树 `initial` 创建的

* 具有对模板和模板类型中信息的引用。 这是通过具有以下属 `jcr:content` 性的节点实现的：

   * `cq:template` -提供对实际模板的动态引用；允许在实际页面上反映对模板所做的更改。

   * `cq:templateType` -提供对模板类型的引用。

![模板、内容和组件如何相互关联](assets/templates-content-components.png)

上图显示了模板、内容和组件之间如何相互关联：

* 控制器 `/content/<my-site>/<my-page>` -引用模板的生成页面。 内容控制整个过程。 根据定义，它访问相应的模板和组件。
* 配置- `/conf/<my-folder>/settings/wcm/templates/<my-template>` 模板和 [相关内容策略定义](#template-definitions) 页面配置。
* 模型- OSGi捆绑包- [OSGI捆绑](/help/implementing/deploying/configuring-osgi.md) 实现功能。
* 视图- `/apps/<my-site>/components` 在创作环境和发布上，内容由组件呈现。

呈现页面时：

* **模板**:

   * 将引 `cq:template` 用其节 `jcr:content` 点的属性以访问与该页面对应的模板。

* **组件**:

   * 页面组件将合并 `structure/jcr:content` 模板的树和页 `jcr:content` 面的树。
      * 页面组件将仅允许作者编辑已标记为可编辑的模板结构的节点（以及任何子节点）。
      * 在页面上渲染组件时，该组件的相对路径将从节点中取 `jcr:content` 出；随后将搜索模 `policies/jcr:content` 板节点下的同一路径。
         * 此 `cq:policy` 节点的属性指向实际的内容策略（即它包含该组件的设计配置）。
            * 这允许您拥有多个可重复使用相同内容策略配置的模板。

### 模板可用性 {#template-availability}

在站点管理界面中创建新页面时，可用模板的列表取决于新页面的位置以及在每个模板中指定的放置限制。

以下属性确定是 `T` 否允许将新页面用作页面的子页面使用模板 `P`。 这些属性中的每个属性都是一个多值字符串，其中包含用于与路径匹配的零个或多个常规表达式:

* 子 `cq:allowedTemplates` 节点或 `jcr:content` 其祖 `P` 代的属性 `P`。

* 属 `allowedPaths` 性 `T`。

* 属 `allowedParents` 性 `T`。

* 模 `allowedChildren` 板的属性 `P`。

评价工作如下：

* 对页面层次结构 `cq:allowedTemplates` 的升序（以开头）时找到的第一个非空属 `P` 性与路径进行匹配 `T`。 如果所有值均不匹配，则 `T` 拒绝。

* 如 `T` 果具有非空属 `allowedPaths` 性，但所有值均与路径不匹配 `P`，则 `T` 拒绝。

* 如果以上两个属性为空或不存在，则拒绝， `T` 除非它属于与相同的应用程序 `P`。 `T` 属于同一应用程 `P` 序，并且仅当路径的第二级名称与路径的 `T` 第二级名称相同时，才属于 `P`。 例如，模板属 `/apps/geometrixx/templates/foo` 于与页面相同的应用程序 `/content/geometrixx`。

* 如 `T` 果具有非空属 `allowedParents` 性，但所有值均与路径不匹配 `P`，则 `T` 拒绝。

* 如果模板的 `P` 属性为非空 `allowedChildren` 属性，但没有任何值与路径匹配 `T`，则会 `T` 拒绝。

* 在所有其他情况下， `T` 都允许使用。

下图描述了模板评估流程：

![模板评估流程](assets/template-evaluation.png)

>[!CAUTION]
>
>AEM优惠多个属性以控制站点下允许的 **模板**。 但是，将这些规则组合在一起可能会导致非常复杂的规则，难以跟踪和管理。
>
>因此，Adobe建议您通过定义以下各项来简化开始:
>
>* 仅属 `cq:allowedTemplates` 性
   >
   >
* 仅在站点根目录上
>
>
有关示例，请参阅 [WKND教程](/help/implementing/developing/introduction/develop-wknd-tutorial.md) : `/content/wknd/jcr:content`
>
>属性 `allowedPaths`、属 `allowedParents`性 `allowedChildren` 和属性也可放置在模板上以定义更复杂的规则。 但是，如果需要进 *一步限* 制允许的模板 `cq:allowedTemplates` ，则在站点的子部分上定义更多属性要简单得多。
>
>另一个优势是，作 `cq:allowedTemplates` 者可以在页面属性的高级选项卡 **中** 更新 **属性**。 其他模板属性无法使用（标准）UI进行更新，因此需要开发人员为每次更改维护规则和代码部署。

#### 限制子页面中使用的模板 {#limiting-templates-used-in-child-pages}

要限制可用于在给定页面下创建子页面的模板 `cq:allowedTemplates` ，请 `jcr:content` 使用页面节点的属性指定允许作为子页面的模板列表。 例如，列表中的每个值都必须是允许的子页面的模板的绝对路径 `/apps/wknd/templates/page-content`。

您可以使用模 `cq:allowedTemplates` 板节点上的属性 `jcr:content` 将此配置应用到使用此模板的所有新创建的页面。

如果要添加更多约束（例如，关于模板层次结构），可以使用模 `allowedParents/allowedChildren` 板上的属性。 然后，您可以明确指定从模板T创建的页面必须是从模板T创建的页面的父／子页面。
