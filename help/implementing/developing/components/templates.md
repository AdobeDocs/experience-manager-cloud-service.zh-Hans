---
title: 页面模板
description: 创建用作新页面基础的页面时，将使用页面模板
exl-id: ea42fce9-9af2-4349-a4e4-547e6e8da05c
source-git-commit: e2505c0fec1da8395930f131bfc55e1e2ce05881
workflow-type: tm+mt
source-wordcount: '3287'
ht-degree: 8%

---

# 页面模板 {#page-templates}

创建页面时，您需要选择模板。 页面模板用作新页面的基础。 模板定义生成页面的结构、任何初始内容以及可以使用的组件（设计属性）。 这有几个优点：

* 利用页面模板，专业作者可以 [创建和编辑模板](/help/sites-cloud/authoring/features/templates.md).
   * 这种专业作者被称为 **模板作者**
   * 模板作者必须是 `template-authors` 组。
* 页面模板会保留与从中创建的任何页面的动态连接。 这可确保对模板所做的任何更改都会反映在页面本身中。
* 页面模板使页面组件变得更通用，以便无需自定义即可使用核心页面组件。

使用页面模板，构成页面的片段被隔离在组件中。 您可以在UI中配置必要的组件组合，从而无需为每个页面变体开发新的页面组件。

本文档：

* 提供了创建页面模板的概述
* 描述创建可编辑模板所需的管理员/开发人员任务
* 描述可编辑模板的技术基础
* 描述AEM如何评估模板的可用性

>[!NOTE]
>
>本文档假设您已熟悉创建和编辑模板。 请参阅创作文档 [创建页面模板](/help/sites-cloud/authoring/features/templates.md)，详细介绍向模板作者公开的可编辑模板的功能。

>[!TIP]
>
>[WKND教程](/help/implementing/developing/introduction/develop-wknd-tutorial.md) 通过实施示例深入了解如何使用页面模板，这对于了解如何在新项目中设置模板非常有用

## 创建新模板 {#creating-a-new-template}

创建页面模板主要是通过 [模板控制台和模板编辑器](/help/sites-cloud/authoring/features/templates.md) 模板作者执行的操作。 本节概述了此过程，并在后面描述了技术级别所发生的情况。

创建新的可编辑模板时，您需要执行以下步骤：

1. 创建 [模板文件夹](#template-folders). 这并非强制要求，但建议采用最佳实践。
1. 选择 [模板类型](#template-type). 这将被复制以创建 [模板定义](#template-definitions).

   >[!NOTE]
   >
   >现成提供模板类型选择。 您还可以 [创建您自己的特定于站点的模板类型](#creating-template-types) 如果需要。

1. 配置新模板的结构、内容策略、初始内容和布局。

   **结构**

   * 利用结构，可为模板定义组件和内容。
   * 不能在生成页面上移动在模板结构中定义的组件，也不能从任何生成页面中删除这些组件。
   * 如果要使页面作者能够添加和删除组件，请在模板中添加段落系统。
   * 可以解锁组件，然后再将其锁定，以便定义初始内容。

   有关模板作者如何定义结构的详细信息，请参阅 [创建页面模板](/help/sites-cloud/authoring/features/templates.md#editing-a-template-structure-template-author).

   有关结构的技术详细信息，请参阅 [结构](#structure) 在本文档中。

   **策略**

   * 内容策略定义组件的设计属性。

      * 例如，可用的组件或最小/最大尺寸。

   * 这些属性适用于模板（和使用模板创建的页面）。

   有关模板作者如何定义策略的详细信息，请参阅 [创建页面模板](/help/sites-cloud/authoring/features/templates.md#editing-a-template-structure-template-author).

   有关策略的技术详细信息，请参阅 [内容策略](#content-policies) 在本文档中。

   **初始内容**

   * 初始内容定义首次根据模板创建页面时将显示的内容。
   * 随后，页面作者可以编辑初始内容。

   有关模板作者如何定义结构的详细信息，请参阅 [创建页面模板](/help/sites-cloud/authoring/features/templates.md#editing-a-template-initial-content-author).

   有关初始内容的技术详细信息，请参阅 [初始内容](#initial-content) 在本文档中。

   **布局**

   * 您可以为各种设备定义模板布局。
   * 模板的响应式布局与页面创作时的响应式布局功能相同。

   有关模板作者如何定义模板布局的详细信息，请参阅 [创建页面模板](/help/sites-cloud/authoring/features/templates.md#editing-a-template-layout-template-author).

   有关模板布局的技术详细信息，请参阅 [布局](#layout) 在本文档中。

1. 启用模板，然后为特定内容树允许该模板。

   * 可以启用或禁用模板，使其对页面作者可用或不可用。
   * 可以使模板可用于或不可用于某些页面分支。

   有关模板作者如何启用模板的详细信息，请参阅 [创建页面模板](/help/sites-cloud/authoring/features/templates.md#enabling-and-allowing-a-template-template-author).

   有关启用模板的技术详细信息，请参阅 [为我们启用和允许模板](#enabling-and-allowing-a-template-for-use)e在此文档中

1. 使用它创建内容页面。

   * 使用模板创建页面时，静态模板与可编辑模板之间没有可见的区别和指示。
   * 对于页面作者，该过程是透明的。

   有关页面作者如何使用模板创建页面的详细信息，请参阅 [创建和组织页面](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#templates).

   有关使用可编辑模板创建页面的技术详细信息，请参阅 [生成内容页面](#resultant-content-pages) 在本文档中。

>[!TIP]
>
>切勿在模板中输入任何需要国际化的信息。出于内部化的目的， [核心组件的本地化功能](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/localization.html) 建议使用。

>[!NOTE]
>
>模板是简化页面创建工作流的强大工具。不过，太多的模板会让作者不知所措，并使页面创建变得混乱。一个好的经验法则是将模板的数量保持在 100 个以内。
>
>由于潜在的性能影响，Adobe 建议不要使用超过 1000 个模板。

>[!NOTE]
>
>编辑器客户端库假定存在 `cq.shared` 命名空间在内容页面中，如果它不存在，则会出现JavaScript错误 `Uncaught TypeError: Cannot read property 'shared' of undefined` 就会有结果。
>
>所有示例内容页面都包含 `cq.shared`，因此任何基于它们的内容都会自动包含 `cq.shared`. 但是，如果您决定从头开始创建自己的内容页面，而不基于示例内容，则必须确保包含 `cq.shared` 命名空间。
>
>请参阅 [使用客户端库](/help/implementing/developing/introduction/clientlibs.md) 以了解详细信息。



## 模板文件夹 {#template-folders}

要组织模板，您可以使用以下文件夹：

* `global`
* 站点特定

>[!NOTE]
>
>即使您可以嵌套文件夹，当用户在 **模板** 控制台，它们以扁平结构呈现。

在标准AEM实例中， `global` 模板控制台中已存在文件夹。 此文件夹会保存默认模板，如果在当前文件夹中没有找到策略和/或模板类型，则此文件夹可以充当备用。您可以将默认模板添加到此文件夹或创建文件夹（推荐）。

>[!NOTE]
>
>最佳做法是创建一个文件夹来存放您的自定义模板，而不是使用 `global` 文件夹。

>[!CAUTION]
>
>文件夹必须由具有以下权限的用户创建： `admin` 权限。

模板类型和策略将按照以下优先级顺序跨所有文件夹继承：

1. 当前文件夹
1. 当前文件夹的父文件夹
1. `/conf/global`
1. `/apps`
1. `/libs`

将创建所有允许条目的列表。 如果任何配置重叠( `path`/ `label`)，则只有最接近当前文件夹的实例才会呈现给用户。

要创建文件夹，您可以执行以下操作：

* 以编程方式或使用CRXDE Lite
* 使用 [配置浏览器](/help/implementing/developing/introduction/configurations.md#using-configuration-browser)

## 使用 CRXDE Lite {#using-crxde-lite}

1. 可以通过编程方式或使用CRXDE Lite为实例创建新文件夹（位于/conf下）。

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

   * 名称：`jcr:title`
   * 类型：`String`
   * 值：您希望在中显示的标题（针对文件夹） **模板** 控制台。

1. 除了标准创作权限之外(例如， `content-authors`)现在，您需要分配组并定义作者所需的访问权限(ACL)，以便能够在新文件夹中创建模板。

   此 `template-authors` group是需要分配的默认组。 请参阅部分 [ACL和组](#acls-and-groups) 以了解详细信息。

   <!--See [Access Right Management](/help/sites-administering/user-group-ac-admin.md#access-right-management) for full details on managing and assigning access rights.-->

### 使用配置浏览器 {#using-the-configuration-browser}

1. 转到 **全局导航** -> **工具** > [**配置浏览器**](/help/implementing/developing/introduction/configurations.md#using-configuration-browser).

   左侧列出了现有文件夹，包括 `global` 文件夹。

1. 单击&#x200B;**创建**。
1. 在 **创建配置** 对话框需要配置以下字段：

   * **标题**：提供配置文件夹的标题
   * **可编辑的模板**：勾选以允许在此文件夹中使用可编辑的模板

1. 单击 **创建**

>[!NOTE]
>
>在 [配置浏览器，](/help/implementing/developing/introduction/configurations.md#using-configuration-browser) 您可以编辑全局文件夹并激活 **可编辑的模板** 选项，但建议不要使用此文件夹创建模板。

### ACL和组 {#acls-and-groups}

创建模板文件夹（通过CRXDE或使用配置浏览器）后，必须为模板文件夹的相应组定义ACL，以确保适当的安全性。

的模板文件夹 [wknd教程](/help/implementing/developing/introduction/develop-wknd-tutorial.md) 可用作示例。

#### 模板作者组 {#the-template-authors-group}

此 `template-authors` group是用于管理对模板的访问权限的组，它是AEM的标准配置，但为空。 必须将用户添加到项目/站点的组中。

>[!CAUTION]
>
>此 `template-authors` 组仅适用于必须能够创建新模板的用户。
>
>编辑模板的功能非常强大，如果不正确编辑模板，现有模板可能会受损。 因此，此角色应重点明确，仅包含符合条件的用户。

下表详细列出了模板编辑所需的权限。

<table>
 <tbody>
  <tr>
   <th>路径</th>
   <th>角色/组</th>
   <th>权限<br /> </th>
   <th>描述</th>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/&lt;<i>your-folder</i>&gt;/settings/wcm/templates</code></td>
   <td>模板作者<br /> </td>
   <td>读取、写入、复制</td>
   <td>在特定站点中创建、读取、更新、删除和复制模板的模板作者 <code>/conf</code> 空间</td>
  </tr>
  <tr>
   <td>匿名Web用户</td>
   <td>读取</td>
   <td>匿名Web用户在呈现页面时必须读取模板</td>
  </tr>
  <tr>
   <td>内容作者</td>
   <td>复制</td>
   <td>复制激活页面时，内容作者需要激活页面的模板</td>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/&lt;<i>your-folder</i>&gt;/settings/wcm/policies</code></td>
   <td><code>Template Author</code></td>
   <td>读取、写入、复制</td>
   <td>在特定站点中创建、读取、更新、删除和复制模板的模板作者 <code>/conf</code> 空间</td>
  </tr>
  <tr>
   <td>匿名Web用户</td>
   <td>读取</td>
   <td>匿名Web用户在呈现页面时必须读取策略</td>
  </tr>
  <tr>
   <td>内容作者</td>
   <td>复制</td>
   <td>内容作者在激活页面时需要激活页面模板的策略</td>
  </tr>
  <tr>
   <td rowspan="2"><code>/conf/&lt;site&gt;/settings/template-types</code></td>
   <td>模板作者</td>
   <td>读取</td>
   <td>模板作者根据预定义的模板类型之一创建新模板。</td>
  </tr>
  <tr>
   <td>匿名Web用户</td>
   <td>无</td>
   <td>匿名Web用户不得访问模板类型</td>
  </tr>
 </tbody>
</table>

此默认值 `template-authors` 组仅涵盖项目设置，其中 `template-authors` 允许成员访问和创作所有模板。 对于更复杂的设置，需要多个模板作者组来分隔对模板的访问，则必须创建更多自定义模板作者组。 但是，模板作者组的权限将仍然相同。

## 模板类型 {#template-type}

创建新模板时，您需要指定模板类型：

* 模板类型可以有效地为模板提供模板。 创建新模板时，使用所选模板类型的结构和初始内容创建新模板。

   * 将复制模板类型以创建模板。
   * 复制完成后，模板和模板类型之间的唯一连接是用作信息的静态引用。

* 模板类型允许您定义：

   * 页面组件的资源类型。
   * 根节点的策略，用于定义模板编辑器中允许的组件。
   * 建议为响应式网格定义断点，并在模板类型上设置移动设备模拟器。

* AEM提供了少量的现成模板类型，如“HTML5页面”和“自适应表单页面”。

   * 其他示例作为 [wknd教程](/help/implementing/developing/introduction/develop-wknd-tutorial.md).

* 模板类型通常由开发人员定义。

现成的模板类型存储在下：

* `/libs/settings/wcm/template-types`

>[!CAUTION]
>
>您不得更改 `/libs` 路径。 这是因为 `/libs` 可随时通过AEM更新覆盖。

特定于站点的模板类型应存储在类似位置：

* `/apps/settings/wcm/template-types`

自定义模板类型的定义应存储在用户定义的文件夹中（推荐）或者存储在 `global`. 例如：

* `/conf/<my-folder-01>/<my-folder-02>/settings/wcm/template-types`
* `/conf/<my-folder>/settings/wcm/template-types`
* `/conf/global/settings/wcm/template-types`

>[!CAUTION]
>
>模板类型必须遵循正确的文件夹结构(即， `/settings/wcm/...`)，否则将无法找到模板类型。

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

如果您已创建可作为其他模板基础的模板，则可以将此模板作为模板类型复制。

1. 创建模板，就像创建任何页面模板一样 [如此处记录的](/help/sites-cloud/authoring/features/templates.md#creating-a-new-template-template-author)，以作为模板类型的基础。
1. 使用CRXDE Lite从复制新创建的模板 `templates` 节点到 `template-types` 下的节点 [模板文件夹](#template-folders).
1. 从删除模板 `templates` 下的节点 [模板文件夹](#template-folders).
1. 在位于以下位置的模板副本中 `template-types` 节点，删除所有 `cq:template` 和 `cq:templateType` 属性来自所有 `jcr:content` 节点。

您还可以在GitHub上使用示例可编辑模板作为基础来开发自己的模板类型。

GITHUB上的代码

您可以在GitHub上找到此页面的代码

* [在GitHub上打开aem-sites-example-custom-template-type项目](https://github.com/Adobe-Marketing-Cloud/aem-sites-example-custom-template-type)
* 将项目下载为 [ZIP文件](https://github.com/Adobe-Marketing-Cloud/aem-sites-example-custom-template-type/archive/master.zip)

## 模板定义 {#template-definitions}

可编辑模板的定义已存储 [用户定义的文件夹](#template-folders) （推荐）或在 `global`. 例如：

* `/conf/<my-folder>/settings/wcm/templates`
* `/conf/<my-folder-01>/<my-folder-02>/settings/wcm/templates`
* `/conf/global/settings/wcm/templates`

模板的根节点属于类型 `cq:Template` 骨架结构为：

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

主要内容包括：

* `<template-name>`

   * ` [initial](#initial-content)`
   * `jcr:content`
   * ` [structure](#structure)`
   * ` [policies](#policies)`
   * `thumbnail.png`

### jcr：content {#jcr-content}

此节点保存模板的属性：

* **名称**：`jcr:title`
* **名称**：`status`
   * ``**类型**: `String`
   * **值**： `draft`， `enabled` 或 `disabled`

### 结构 {#structure}

定义生成页面的结构：

* 与初始内容合并( `/initial`)。
* 对结构所做的更改会反映在使用模板创建的任何页面中。
* 此 `root` ( `structure/jcr:content/root`)节点定义生成页面中可用的组件列表。
   * 无法在任何生成页面上移动或删除在模板结构中定义的组件。
   * 解锁组件后， `editable` 属性设置为 `true`.
   * 解锁已包含内容的组件后，此内容将被移至 `initial` 分支。

* 此 `cq:responsive` 节点包含响应布局的定义。

### 初始内容 {#initial-content}

定义新页面在创建时将具有的初始内容：

* 包含 `jcr:content` 复制到任何新页面的节点。
* 与结构合并( `/structure`)。
* 如果在创建后更改了初始内容，则不会更新任何现有页面。
* 此 `root` 节点包含组件列表，用于定义生成的页面中可用的组件。
* 如果在结构模式下将内容添加到组件且随后解锁该组件（反之亦然），则此内容将用作初始内容。

### 布局 {#layout}

时间 [编辑模板您可以定义布局](/help/sites-cloud/authoring/features/templates.md)，此函数使用 [标准响应布局](/help/sites-cloud/authoring/features/responsive-layout.md).

<!-- that can also be [configured](/help/sites-administering/configuring-responsive-layout.md). -->

### 内容策略 {#content-policies}

内容策略定义组件的设计属性。 例如，可用的组件或最小/最大尺寸。这些属性适用于模板（和使用模板创建的页面）。可以在模板编辑器中创建和选择内容策略。

* 属性 `cq:policy`，位于 `root` 节点
  `/conf/<your-folder>/settings/wcm/templates/<your-template>/policies/jcr:content/root`
为页面的段落系统提供内容策略的相对引用。

* 属性 `cq:policy`，位于下的组件显式节点上 `root`，提供指向各个组件策略的链接。

* 实际的策略定义存储在以下位置：
  `/conf/<your-folder>/settings/wcm/policies/wcm/foundation/components`

>[!NOTE]
>
>策略定义的路径取决于组件的路径。 `cq:policy` 保存对配置本身的相对引用。

### 页面策略 {#page-policies}

页面策略允许您定义 [内容策略](#content-policies) 页面（主parsys）的模板或生成页面中。

### 启用和允许使用模板 {#enabling-and-allowing-a-template-for-use}

1. **启用模板**

   在使用模板之前，必须通过以下任一方式启用模板：

   * [启用模板](/help/sites-cloud/authoring/features/templates.md) 从 **模板** 控制台。

   * 在上设置状态属性 `jcr:content` 节点。

      * 例如，在：
        `/conf/<your-folder>/settings/wcm/templates/<your-template>/jcr:content`

      * 定义属性：

         * 名称：状态
         * 类型：字符串
         * 价值: `enabled`

1. **允许的模板**

   * [在上定义允许的模板路径 **页面属性**](/help/sites-cloud/authoring/features/templates.md#allowing-a-template-author) 子分支的相应页面或根页面的ID。
   * 设置属性：
     `cq:allowedTemplates`
在 `jcr:content` 所需分支的节点。

   例如，其值为：

   `/conf/<your-folder>/settings/wcm/templates/.*`

## 生成内容页面 {#resultant-content-pages}

从可编辑模板创建的页面：

* 使用合并的子树创建 `structure` 和 `initial` 在模板中

* 具有对模板和模板类型中包含的信息的引用。 这是通过实现的 `jcr:content` 节点的属性：

   * `cq:template`  — 提供对实际模板的动态引用；使对模板所做的更改能够反映在实际页面上。

   * `cq:templateType`  — 提供对模板类型的引用。

![模板、内容和组件如何相互关联](assets/templates-content-components.png)

上图显示了模板、内容和组件如何相互关联：

* 控制器 —  `/content/<my-site>/<my-page>`  — 引用模板的结果页面。 内容控制着整个过程。 根据定义，访问相应的模板和组件。
* 配置 —  `/conf/<my-folder>/settings/wcm/templates/<my-template>` - [模板和相关内容策略](#template-definitions) 定义页面配置。
* 模型 — OSGi包 —  [OSGi包](/help/implementing/deploying/configuring-osgi.md) 实施相关功能。
* 视图 —  `/apps/<my-site>/components`  — 在创作和发布环境中，内容均由组件渲染。

呈现页面时：

* **模板**:

   * 此 `cq:template` 其属性 `jcr:content` 节点被引用以访问与该页面对应的模板。

* **组件**:

   * 页面组件将合并 `structure/jcr:content` 模板树 `jcr:content` 页面的树。
      * 页面组件将仅允许作者编辑已标记为可编辑的模板结构的节点（以及任何子节点）。
      * 在页面上呈现组件时，该组件的相对路径将从 `jcr:content` 节点；同一路径位于 `policies/jcr:content` 随后将搜索模板的节点。
         * 此 `cq:policy` 此节点的属性指向实际内容策略（即，它包含该组件的设计配置）。
            * 这样，您就可以拥有多个重复使用相同内容策略配置的模板。

### 模板可用性 {#template-availability}

在站点管理界面中创建新页面时，可用模板的列表取决于新页面的位置以及在每个模板中指定的版面限制。

以下属性确定模板是否 `T` 允许用于作为页面的子项放置的新页面 `P`. 以下每个属性都是一个多值字符串，其中包含零个或多个用于与路径匹配的正则表达式：

* 此 `cq:allowedTemplates` 的属性 `jcr:content` 子节点 `P` 或祖先 `P`.

* 此 `allowedPaths` 属性 `T`.

* 此 `allowedParents` 属性 `T`.

* 此 `allowedChildren` 模板的属性 `P`.

评估工作如下：

* 第一个非空 `cq:allowedTemplates` 在页面层次结构中以开始升序时发现属性 `P` 的路径匹配 `T`. 如果没有任何值匹配， `T` 被拒绝。

* 如果 `T` 具有非空 `allowedPaths` 属性，但没有值匹配路径 `P`， `T` 被拒绝。

* 如果以上属性为空或不存在， `T` 被拒绝，除非它属于与相同的应用程序 `P`. `T` 属于与相同的应用程序 `P` 当且仅当第二级路径的名称 `T` 与的路径的第二级名称相同 `P`. 例如，模板 `/apps/wknd/templates/foo` 属于与页面相同的应用程序 `/content/wknd`.

* 如果 `T` 具有非空 `allowedParents` 属性，但没有值匹配路径 `P`， `T` 被拒绝。

* 如果模板 `P` 具有非空 `allowedChildren` 属性，但没有值匹配路径 `T`， `T` 被拒绝。

* 在所有其他情况下， `T` 允许。

下图描述了模板评估流程：

![模板评估过程](assets/template-evaluation.png)

>[!CAUTION]
>
>AEM提供了多个属性来控制下允许的模板 **站点**. 但是，将它们组合在一起可能会导致非常复杂的规则，这些规则难以跟踪和管理。
>
>因此，Adobe建议您从定义以下内容开始：
>
>* 仅 `cq:allowedTemplates` 属性
>
>* 仅在站点根目录上
>
>有关示例，请参见 [wknd教程](/help/implementing/developing/introduction/develop-wknd-tutorial.md) 内容： `/content/wknd/jcr:content`
>
>属性 `allowedPaths`， `allowedParents`、和 `allowedChildren` 还可以放置在模板上以定义更复杂的规则。 但是，如果可能，它是 *很多* 更简单以进一步定义 `cq:allowedTemplates` 属性（如果需要进一步限制允许的模板）。
>
>另一个优势是 `cq:allowedTemplates` 作者可以在以下位置更新属性 **高级** 选项卡 **页面属性**. 无法使用（标准）UI更新其他模板属性，因此需要开发人员维护规则和每次更改的代码部署。

#### 限制子页面中使用的模板 {#limiting-templates-used-in-child-pages}

要限制哪些模板可用于在给定页面下创建子页面，请使用 `cq:allowedTemplates` 属性 `jcr:content` 页面的节点，用于指定允许作为子页面的模板列表。 例如，列表中的每个值都必须是允许的子页面模板的绝对路径 `/apps/wknd/templates/page-content`.

您可以使用 `cq:allowedTemplates` 模板的属性  `jcr:content` 节点，用于将此配置应用于使用此模板的所有新创建的页面。

如果要添加更多约束，例如关于模板层次结构的约束，您可以使用 `allowedParents/allowedChildren` 属性。 然后，您可以明确指定从模板T创建的页面必须是从模板T创建的页面的父项/子项。
