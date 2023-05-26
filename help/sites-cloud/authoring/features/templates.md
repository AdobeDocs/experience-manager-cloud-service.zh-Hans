---
title: 创建页面模板
description: 模板定义了结果页面的结构，并且使用模板编辑器，创建和维护模板不再只是开发人员的任务
exl-id: 4c9dbf26-5852-45ab-b521-9f051c153b2e
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '4596'
ht-degree: 61%

---

# 创建页面模板 {#creating-page-templates}

创建页面时，您必须选择一个模板，该模板将用作创建新页面的基础。 模板定义了生成页面的结构、任何初始内容以及可以使用的组件。

使用模 **板编辑器**，创建和维护模板不再只是开发人员的任务。 高级用户(称为模板作者 **)也可能**。 开发人员仍需要设置环境、创建客户端库和创建要使用的组件，但是，在这些基础知识到位后，模板作者就可以灵活地创建和配置模板，而无需开发项目。 ****

此 **模板控制台** 允许模板作者：

* 创建新模板，或复制现有模板。
* 管理模板的生命周期。

此 **模板编辑器** 允许模板作者：

* 将组件添加到模板并将它们放置在响应式网格上。
* 预先配置组件。
* 定义在使用模板创建的页面上可以编辑哪些组件。

本文档说明如何 **模板作者** 可以使用“模板”控制台和编辑器创建和管理可编辑模板。

有关如何在技术层面使用可编辑模板的详细信息，请参阅开发人员文档[页面模板](/help/implementing/developing/components/templates.md)以了解更多信息。

>[!NOTE]
>
>模板 **** 编辑器不支持直接在模板级别进行定位。 可以定位基于可编辑模板创建的页面，但不能定位模板本身。

## 开始之前 {#before-you-start}

>[!NOTE]
>
>管理员必须在&#x200B;**配置浏览器**&#x200B;中配置一个模板文件夹，并应用适当的权限，之后模板作者才能在该文件夹中创建模板。

在开始之前，请务必考虑到创建新模板需要多方协作。因此，为每项任务指明了对应的[角色](#roles)。这并不会影响您使用模板来创建页面的实际操作方式，但却会影响页面与模板之间的关系。

### 角色 {#roles}

使用&#x200B;**“模板”控制台**&#x200B;和&#x200B;**模板编辑器**&#x200B;创建新模板需要以下角色之间的协作：

* **管理员**:
   * 创建新的模板文件夹需要 `admin` 权限。
   * 此类任务通常也可以由开发人员完成
* **开发人员**:
   * 专注于技术/内部详细信息
   * 需要具有开发环境方面的经验。
   * 为模板作者提供必要信息。
* **模板作者**：
   * 特定的作者，`template-authors` 组中的一个成员。
      * 可分配所需的权限和许可。
   * 可以配置组件的使用和其他高级详细信息，这些详细信息需要：
      * 一些技术知识
         * 例如，在定义路径时使用模式。
      * 由开发人员提供的技术信息。

由于某些任务（如创建文件夹）的性质，需要开发环境，而这需要知识/经验。

本文档中详细列出的任务以及负责执行这些任务的角色。

## 创建和管理模板 {#creating-and-managing-templates}

在创建新的可编辑模板时，您可以：

* 使用 **模板** 控制台。 此页面位于 **常规** 部分 **工具** 控制台。
   * 或直接从以下网站进行访问：`https://<host>:<port>/libs/wcm/core/content/sites/templates.html/conf`
* 如有必要，可以[创建模板文件夹](#creating-a-template-folder-admin)
* [创建新模板](#creating-a-new-template-template-author)，新模板最初是空的
* [定义其他属性](#defining-template-properties-template-author) 模板（如果需要）
* [编辑模板](#editing-templates-template-authors) 要定义，请执行以下操作：
   * [结构](#editing-a-template-structure-template-author) - 不能在使用该模板创建的页面上更改的预定义内容。
   * [初始内容](#editing-a-template-initial-content-author) - 能够在使用该模板创建的页面上更改的预定义内容。
   * [布局](#editing-a-template-layout-template-author) - 针对各种设备。
   * [样式](/help/sites-cloud/authoring/features/style-system.md) - 定义要用于该模板及其组件的样式。
* [启用模板](#enabling-a-template-template-author) 创建页面时使用
* [允许模板](#allowing-a-template-author) 所需的页面或网站分支
* [发布模板](#publishing-a-template-template-author) 以使其在发布环境中可用

>[!NOTE]
>
>通常，在最初设置您的网站时便会预定义&#x200B;**允许的模板**。

>[!TIP]
>
>切勿在模板中输入任何需要国际化的信息。<!-- Never enter any information that needs to be [internationalized](/help/sites-developing/i18n.md) into a template.-->
>
>对于必须本地化的模板元素（如页眉和页脚），请利用[核心组件的本地化功能。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/localization.html)

### 创建模板文件夹 – 管理员 {#creating-a-template-folder-admin}

您应该为项目创建模板文件夹，以保存特定于项目的模板。这是一项管理员任务，在[页面模板](/help/implementing/developing/components/templates.md#template-folders)文档中有相关说明。-->

### 创建新模板 – 模板作者 {#creating-a-new-template-template-author}

1. 打开&#x200B;**“模板”控制台**（通过&#x200B;**工具** -> **常规**），然后导航到所需的文件夹。

   >[!NOTE]
   >
   >在标准 AEM 实例中，“模板”控制台中已存在&#x200B;**全局**&#x200B;文件夹。此文件夹会保存默认模板，如果在当前文件夹中没有找到策略和/或模板类型，则此文件夹可以充当备用。
   >
   >建议最好使用 [为您的项目创建的模板文件夹](/help/implementing/developing/components/templates.md#template-folders).

1. 选择&#x200B;**创建**，然后选择&#x200B;**创建模板**&#x200B;以打开向导。

1. 选取 **模板类型**，然后选择 **下一个**.

   >[!NOTE]
   >
   >模板类型是预定义的模板布局，可以将其视为模板的模板。 这些权限由开发人员或系统管理员预定义。 要获取更多信息，请参阅开发人员文档[页面模板](/help/implementing/developing/components/templates.md#template-type)。-->

1. 完成 **模板详细信息**：

   * **模板名称**
   * **描述**

1. 选择&#x200B;**创建**。随即会显示确认对话框，选择&#x200B;**打开**&#x200B;以开始编辑模板，或选择&#x200B;**完成**&#x200B;以返回到“模板”控制台。

   >[!NOTE]
   >
   >创建新模板后，会在控制台中将其标记为&#x200B;**草稿**，这表示页面作者还不能使用此模板。

>[!NOTE]
>
>模板是简化页面创建工作流的强大工具。不过，太多的模板会让作者不知所措，并使页面创建变得混乱。一个好的经验法则是将模板的数量保持在 100 个以内。
>
>由于潜在的性能影响，Adobe 建议不要使用超过 1000 个模板。

### 定义模板属性 — 模板作者 {#defining-template-properties-template-author}

模板可以具有以下属性：

* 图像
   * 要用作的图像 [模板的缩略图](#template-thumbnail-image) 以帮助进行选择，例如在“创建页面”向导中选择。
      * 可以上传
      * 可以基于模板内容生成
* 标题
   * 用于标识模板的标题，例如 **创建页面** 向导。
* 描述
   * 可选描述，用于提供更多有关模板及其用法的信息，例如&#x200B;**创建页面**&#x200B;向导中显示的描述。

要查看和/或编辑属性，请执行以下操作：

1. 在&#x200B;**模板控制台**&#x200B;中，选择相应的模板。
1. 从工具栏或快速选项中选择&#x200B;**查看属性**&#x200B;以打开对话框。
1. 此时您可以查看或编辑模板属性。

>[!NOTE]
>
>控制台中会指示模板的状态（“草稿”、“已启用”或“已禁用”）。

#### 模板缩略图图像 {#template-thumbnail-image}

要定义模板缩略图，请执行以下操作：

1. 编辑模板属性。
1. 选择要上传缩略图还是从模板内容生成缩略图。
   * 如果要上传缩略图，请单击或点按 **上传图像**
   * 如果要生成缩略图，请单击或点按 **生成预览**
1. 对于这两种方法，将显示缩略图预览。
   * 如果不满意，请单击或点按 **清除** 上传其他图像或重新生成缩略图。
1. 如果您对缩略图满意，请单击或点按 **保存并关闭**.

### 启用和允许模板 — 模板作者 {#enabling-and-allowing-a-template-template-author}

为了能够在创建页面时使用模板，您需要执行以下操作：

* [启用模板](#enabling-a-template-template-author)以使其可在创建页面时使用。
* [允许模板](#allowing-a-template-author)以指定可以使用模板的内容分支。

#### 启用模板 – 模板作者 {#enabling-a-template-template-author}

可以启用或禁用模板，使其在 **创建页面** 向导。

>[!CAUTION]
>
>启用模板后，当模板作者开始进一步更新模板时，将显示警告。 这是为了告知用户可能会引用该模板，因此任何更改都可能影响引用该模板的页面。

1. 在&#x200B;**模板控制台**&#x200B;中，选择相应的模板。
1. 从工具栏中选择&#x200B;**启用**&#x200B;或&#x200B;**禁用**，然后在确认对话框中再次选择“启用”或“禁用”。
1. 现在，您便能够在[创建新页面](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#creating-a-new-page)时使用模板，不过您可能想要根据自己的需求[编辑模板](#editing-templates-template-authors)。

>[!NOTE]
>
>控制台中会指示模板的状态（“草稿”、“已启用”或“已禁用”）。

#### 允许模板 – 作者 {#allowing-a-template-author}

可以使模板可用于或不可用于某些页面分支。

1. 对于希望可在其中使用模板的分支，打开其根页面的[页面属性](/help/sites-cloud/authoring/fundamentals/page-properties.md)。
1. 打开&#x200B;**高级**&#x200B;选项卡。
1. 在&#x200B;**模板设置**&#x200B;下方，使用&#x200B;**添加字段**&#x200B;指定模板的路径。

   路径可以是显式路径或使用模式。 例如：

   `/conf/<your-folder>/settings/wcm/templates/.*`

   路径的顺序无关，将扫描所有路径并检索任何模板。

   >[!NOTE]
   >
   >如果 **允许的模板** 列表留空，树将提升，直到找到值/列表。
   >
   >
   >请参阅[模板可用性](/help/implementing/developing/components/templates.md#template-availability) – 对允许的模板适用的原则与此相同。

1. 单击&#x200B;**保存**，以保存对页面属性所做的更改。

>[!NOTE]
>
>通常，在设置您的网站时便会为整个网站预定义允许的模板。

### 发布模板 – 模板作者 {#publishing-a-template-template-author}

由于渲染页面时会引用模板，因此模板在完全配置后需要进行发布，才能用于发布环境。

1. 在&#x200B;**模板控制台**&#x200B;中，选择相应的模板。
1. 从工具栏中选择&#x200B;**发布**&#x200B;以打开向导。
1. 选择要一同发布的&#x200B;**内容策略**。
1. 选择 **Publish** ，以完成操作。

## 编辑模板 — 模板作者 {#editing-templates-template-authors}

创建或编辑模板时，您可以定义多个方面。 编辑模板与页面创作类似。

使用工具栏中的&#x200B;**模式**&#x200B;选择器，可以选择并编辑模板的相应方面：

* [结构](#editing-a-template-structure-template-author)
* [初始内容](#editing-a-template-initial-content-author)
* [布局](#editing-a-template-layout-template-author)

![模板编辑器模式选择器](/help/sites-cloud/authoring/assets/templates-mode.png)

而使用&#x200B;**页面信息**&#x200B;菜单中的&#x200B;**页面策略**&#x200B;选项，可以[选择所需的页面策略](#page-policies)：

![模板编辑器页面信息](/help/sites-cloud/authoring/assets/templates-page-information.png)

>[!CAUTION]
>
>如果作者开始编辑已启用的模板，将显示警告。 这是为了告知用户可能会引用该模板，因此任何更改都可能影响引用该模板的页面。

### 模板属性 {#template-attributes}

可以编辑模板的以下属性：

#### 结构 {#template-structure}

页面作者不能从生成页面中移动/删除添加到[结构](#editing-a-template-structure-template-author)的组件。如果您希望页面作者能够在生成页面中添加和删除组件，则需要将段落系统添加到模板。

锁定组件后，您可以添加页面作者无法编辑的内容。 您可以解锁组件，以便定义 [初始内容](#editing-a-template-initial-content-author).

>[!NOTE]
>
>在结构模式下，任何作为已解锁元件的父元件的元件均无法移动、剪切或删除。

#### 初始内容 {#template-initial-content}

解锁组件后，您可以定义要复制到生成页面（使用模板创建）的[初始内容](#editing-a-template-initial-content-author)。可以在生成页面上编辑这些已解锁的组件。

>[!NOTE]
>
>在&#x200B;**初始内容**&#x200B;模式下以及在生成页面上，可以删除任何具有可访问父项的已解锁组件（即，布局容器内的组件）。

#### 布局 {#template-layout}

通过[布局](#editing-a-template-layout-template-author)，您可以预定义所需设备格式的模板布局。模板创作的&#x200B;**布局**&#x200B;模式与&#x200B;[**页面创作的布局**&#x200B;模式](/help/sites-cloud/authoring/features/responsive-layout.md#defining-layouts-layout-mode)具有相同的功能。

#### 页面策略 {#template-page-policies}

[页面策略](#page-policies)可以将预定义的页面策略关联到页面。这些页面策略可定义各种设计配置。

#### 样式 {#template-styles}

[样式系统](/help/sites-cloud/authoring/features/style-system.md)允许模板作者在组件的内容策略中定义样式类，以便内容作者在页面上编辑组件时能够选择这些类。这些样式可以作为组件的替代可视化变量，从而使组件变得更加灵活。

有关更多信息，请参阅[样式系统文档](/help/sites-cloud/authoring/features/style-system.md)。

### 编辑模板 – 结构 – 模板作者 {#editing-a-template-structure-template-author}

在&#x200B;**结构**&#x200B;模式下，您可以为模板定义组件和内容，并为模板及其组件定义策略。

* 不能在生成的页面上移动模板结构中定义的组件，也不能从任何生成的页面中删除这些组件。
* 如果您希望页面作者能够添加和删除组件，请向模板中添加一个段落系统。
* 可以解锁组件，然后再将其锁定，以便定义[初始内容](#editing-a-template-initial-content-author)。
* 可为组件和页面定义设计策略。

![模板编辑器页面结构](/help/sites-cloud/authoring/assets/templates-page-structure.png)

您可以在模板编辑器的&#x200B;**结构**&#x200B;模式中执行许多操作，并且有许多功能可协助您执行操作：

#### 添加组件 {#add-components}

向模板中添加组件有多种机制：

* 从 **组件** 浏览器中。
* 使用模板中现有组件的工具栏上的&#x200B;**插入组件**&#x200B;选项，或使用&#x200B;**将组件拖动到此处**&#x200B;框。
* 通过拖动资产(从 **资产** 浏览器中)直接加载到模板上以就地生成相应的组件。

添加后，每个组件都标有：

* 边框
* 用于显示组件类型的标记
* 解锁组件时显示的标记

>[!NOTE]
>
>将现成的&#x200B;**标题**&#x200B;组件添加到模板后，该组件会包含默认的文本&#x200B;**结构**。
>
>如果更改此文本，并添加自己的文本，则在使用该模板创建页面时，将会使用更新的文本。
>
>如果您保留默认文本（“结构”），则标题会默认使用后续生成页面的名称。

>[!NOTE]
>
>将组件和资产添加到模板的操作与在[页面创作](/help/sites-cloud/authoring/fundamentals/editing-content.md)时执行的类似操作虽然并不完全相同，但也存在许多相似之处。

#### 组件操作 {#component-actions}

将组件添加到模板后，对组件执行操作。 每个实例都有一个用于访问可用操作的工具栏，该工具栏取决于组件类型。

![模板组件的操作工具栏](/help/sites-cloud/authoring/assets/templates-component-actions.png)

显示的工具栏还会取决于执行的操作，例如将策略与组件关联后，便会显示设计配置图标。

#### 编辑和配置 {#edit-and-configure}

通过这两项操作，您可以在组件中添加内容。

#### 指示结构的边框 {#border-to-indicate-structure}

在中工作时 **结构** 模式橙色边框表示当前选择的组件。 虚线还指示父组件。

#### 策略和属性（常规） {#policy-and-properties-general}

内容（或设计）策略定义组件的设计属性。 例如，可用元件或最小/最大尺寸。 这些选项适用于模板（以及使用模板创建的页面）。

可为组件创建内容策略或选择现有策略。

![“内容策略”按钮](/help/sites-cloud/authoring/assets/templates-content-policy-button.png)

这允许您定义设计详细信息。

![内容策略](/help/sites-cloud/authoring/assets/template-content-policy.png)

配置窗口分为两个部分。

* 在对话框左侧的&#x200B;**策略**&#x200B;下方，您能够创建新策略或选择现有策略。
* 在对话框右侧的&#x200B;**属性**&#x200B;下方，您可以设置特定于组件类型的属性。

可用的属性取决于所选的组件。 例如，对于文本组件，属性定义了复制和粘贴选项、格式设置选项以及段落样式等选项。

##### 策略 {#policy}

内容（或设计）策略定义组件的设计属性。 例如，可用元件或最小/最大尺寸。 这些选项适用于模板（以及使用模板创建的页面）。

在&#x200B;**策略**&#x200B;下方，您可以通过下拉列表选择要应用于组件的现有策略。

![选择策略](/help/sites-cloud/authoring/assets/templates-policy-selector.png)

此外，也可以通过选择&#x200B;**选择策略**&#x200B;下拉列表旁边的“添加”按钮，来添加新策略。然后，应该在&#x200B;**策略标题**&#x200B;字段中输入一个新标题。

![“添加策略”按钮](/help/sites-cloud/authoring/assets/templates-add-policy-button.png)

使用&#x200B;**选择策略**&#x200B;下拉列表旁边的“复制”按钮，可复制在此下拉列表中选定的现有策略以将其作为新策略。然后，应该在&#x200B;**策略标题**&#x200B;字段中输入一个新标题。默认情况下，复制的策略的标题将为 **X 的副本**，其中 X 是被复制的策略的标题。

![“复制策略”按钮](/help/sites-cloud/authoring/assets/templates-copy-policy-button.png)

**策略说明**&#x200B;字段中的策略说明是可选的。

在&#x200B;**同时使用该选定策略的其他模板**&#x200B;部分中，您可以轻松地查看同时也使用了&#x200B;**选择策略**&#x200B;下拉列表中的选定策略的其他模板。

![使用现有策略](/help/sites-cloud/authoring/assets/templates-policy-use.png)

>[!NOTE]
>
>如果将同一类型的多个组件添加为初始内容，则同一策略适用于所有这些组件。

##### 属性 {#properties}

在 **属性** 标题可定义组件的设置。 标题包含两个选项卡：

* 主要
* 功能

###### 主要 {#main}

在 **主要** 选项卡中，定义了组件最重要的设置。

例如，对于图像组件，可以定义允许的宽度并启用延迟加载。

如果某个设置允许多项配置，请单击或点按 **添加** 按钮以添加其他配置。

![“添加”按钮](/help/sites-cloud/authoring/assets/templates-add-button.png)

要删除配置，请单击或点按位于配置右侧的&#x200B;**删除**&#x200B;按钮。

要删除配置，请单击或点按&#x200B;**删除**&#x200B;按钮。

![“删除”按钮](/help/sites-cloud/authoring/assets/templates-delete-button.png)

###### 功能 {#features}

此 **功能** 选项卡允许您启用或禁用组件的其他功能。

例如，对于图像组件，您可以定义裁剪比例、允许的图像方向以及允许上载的情况。

![“功能”选项卡](/help/sites-cloud/authoring/assets/templates-features-tab.png)

>[!CAUTION]
>
>请注意，在 AEM 中，裁剪比例被定义为&#x200B;**高宽比**。这与常见的宽高比的定义不同，这样做是出于对旧版兼容性的考虑。只要您清楚地定义&#x200B;**名称**，页面创作用户便不会察觉到任何差异，因为您定义的名称才是 UI 中显示的内容。

>[!NOTE]
>
>[](/help/implementing/developing/extending/rich-text-editor.md)只能为 RTE 通过其 UI 设置提供的选项定义用于实施富文本编辑器的组件的内容策略。

#### 策略和属性（布局容器） {#policy-and-properties-layout-container}

布局容器的策略和属性设置与常规用法相似，但存在一些差异。

>[!NOTE]
>
>对于容器组件而言，必须配置策略，因为它允许您定义将在容器中可用的组件。

配置窗口分为两部分，就像在窗口的常规用法中一样。

##### 策略 {#policy-layout}

内容（或设计）策略定义组件的设计属性。 例如，可用元件或最小/最大尺寸。 这些选项适用于模板（以及使用模板创建的页面）。

在&#x200B;**策略**&#x200B;下方，您可以通过下拉列表选择要应用于组件的现有策略。此操作方式与该窗口的常规用法相同。

##### 属性 {#properties-layout}

在 **属性** 标题您可以选择可用于布局容器的组件并定义其设置。 标题有三个选项卡：

* 允许的组件
* 默认组件
* 响应式设置

###### 允许的组件 {#allowed-components}

在 **允许的组件** 选项卡中，您可以定义哪些组件可用于布局容器。

* 组件按其组件组进行分组，这些组件组可展开和折叠。
* 通过选中组名可选择整个组，通过取消选中可取消选择所有组。
* 减号表示至少选择了一个项目，但并非选择组中的所有项目。
* 搜索可用于按名称筛选组件。
* 无论是否应用了过滤器，组件组名称右侧列出的数字都表示这些组中选定组件的总数。

![允许的组件选项卡](/help/sites-cloud/authoring/assets/templates-allowed-components-tab.png)

###### 默认组件 {#default-components}

在 **默认组件** 选项卡，您可以定义哪些组件自动与给定媒体类型关联，以便作者从资产浏览器拖动资产时，AEM知道要将资产与哪个组件关联。 请注意，只有具有拖放区域的组件才可用于此类配置。

单击或点按 **添加映射** 添加全新的组件和MIME类型映射。

在列表中选择一个组件，然后单击或点按 **添加类型** ，以向已映射的组件添加其他MIME类型。 单击&#x200B;**删除**&#x200B;图标可删除 MIME 类型。

![“默认组件”选项卡](/help/sites-cloud/authoring/assets/templates-default-components-tab.png)

###### 响应式设置 {#responsive-settings}

在&#x200B;**响应式设置**&#x200B;选项卡上，您可以配置布局容器的生成网格中的列数。

#### 解锁和锁定组件 {#unlock-and-lock-components}

您可以解锁/锁定组件，以定义内容是否可用于更改 **初始内容** 模式。

解锁组件后：

* 打开的挂锁指示器显示在边框中。
* 相应地对组件工具栏进行调整。
* 任何已输入的内容将不再显示于 **结构** 模式。
   * 已输入的内容会被视为初始内容，因此仅在&#x200B;**初始内容**&#x200B;模式下可见。
* 无法移动、剪切或删除已解锁组件的父组件。

![“锁定组件”按钮](/help/sites-cloud/authoring/assets/templates-unlock-component.png)

这包括解锁容器组件，以便在初始内容模式或生成的页面 **中添加其他组件** 。 如果在解锁容器之前已将组件／内容添加到容器，则这些组件／内容在结构模式下不再显示，但将以初始内容模式 **显示****** 。 在&#x200B;**“结构”模式**&#x200B;下，只会显示容器组件本身，及其&#x200B;**允许的组件**&#x200B;列表。

![允许的组件](/help/sites-cloud/authoring/assets/templates-allowed-components.png)

为了节省空间，布局容器不会扩大来容纳允许的组件列表。相反，容器会变成一个可滚动的列表。

可配置的组件会显示一个 **策略图标**，单击或点按该图标可编辑该组件的策略和属性。

![“可配置组件”图标](/help/sites-cloud/authoring/assets/templates-configurable-component.png)

#### 与现有页面的关系 {#relationship-to-existing-pages}

如果在基于模板创建页面后更新了模板的结构，则这些页面会反映对模板所做的更改。工具栏中会显示一条警告消息，提醒您这一事实，同时还会显示确认对话框。

![正在使用模板的横幅警告](/help/sites-cloud/authoring/assets/templates-in-use-banner.png)

### 编辑模板 – 初始内容 – 作者 {#editing-a-template-initial-content-author}

**初始内容** 模式用于定义首次根据模板创建页面时显示的内容。 随后，页面作者可以编辑初始内容。

虽然在&#x200B;**结构**&#x200B;模式下创建的所有内容在&#x200B;**初始内容**&#x200B;模式下均可见，但只能选择和编辑已解锁的组件。

>[!NOTE]
>
>可以将&#x200B;**初始内容**&#x200B;模式视为使用模板创建的页面的编辑模式。因此，策略不是在&#x200B;**初始内容**&#x200B;模式下定义的，而是在&#x200B;[**结构**&#x200B;模式](#editing-a-template-structure-template-author)下定义的。

* 可编辑的已解锁组件将被标记。 选中后，它们具有蓝色边框：

   ![初始内容模式](/help/sites-cloud/authoring/assets/templates-initial-content-mode.png)

* 已解锁组件的工具栏允许您编辑和配置内容：

   ![已解锁的组件](/help/sites-cloud/authoring/assets/templates-unlocked-components.png)

* 如果已将某个容器组件解锁（在&#x200B;**结构**&#x200B;模式下），则您可以将新组件添加到该容器（在&#x200B;**初始内容**&#x200B;模式下）。可以在生成页面上移动或删除在&#x200B;**初始内容**&#x200B;模式下添加的组件。

   您可以通过以下两种方式添加组件：使用&#x200B;**将组件拖动到此处**&#x200B;区域，或使用相应容器工具栏中的&#x200B;**插入新组件**&#x200B;选项。

   ![添加组件](/help/sites-cloud/authoring/assets/templates-add-component.png)
   ![添加组件](/help/sites-cloud/authoring/assets/templates-add-component-dialog.png)

* 如果在基于模板创建页面后更新了模板的初始内容，则对模板的初始内容所做的更改不会影响这些页面。

>[!NOTE]
>
>初始内容用于准备用作创建内容起点的组件和页面布局。 它不是将保持原样的实际内容。 因此，无法翻译初始内容。
>
>如果需要在模板中包括可翻译文本（如在页眉或页脚中），则可以使用[核心组件的本地化功能](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/localization.html)。

### 编辑模板 – 布局 – 模板作者 {#editing-a-template-layout-template-author}

您可以为各种设备定义模板布局。模板的[响应式布局](/help/sites-cloud/authoring/features/responsive-layout.md)与页面创作时的响应式布局功能相同。

>[!NOTE]
>
>**初始内容**&#x200B;模式会反映布局更改，而&#x200B;**结构**&#x200B;模式则不会反映任何布局更改。

![编辑模板布局](/help/sites-cloud/authoring/assets/templates-edit-layout.png)

### 编辑模板 – 页面策略 – 模板作者/开发人员 {#editing-a-template-page-policy-template-author-developer}

将在&#x200B;**页面信息**&#x200B;菜单的&#x200B;**页面策略**&#x200B;选项下维护包含所需客户端库的页面策略。

要访问&#x200B;**页面策略**&#x200B;对话框，请执行以下操作：

1. 在&#x200B;**模板编辑器**&#x200B;中，从工具栏中选择&#x200B;**页面信息**，然后选择&#x200B;**页面策略**&#x200B;以打开相应的对话框。
1. 随即会打开&#x200B;**页面策略**&#x200B;对话框，该对话框分成两个部分：

   * 左半部分定义 [页面策略](#page-policies)
   * 右半部分定义 [页面属性](#page-properties)

   ![页面设计](/help/sites-cloud/authoring/assets/templates-page-design.png)

#### 页面策略 {#page-policies}

您可以将内容策略应用于模板或生成页面。这会为页面上的主要段落系统定义内容策略。

![页面策略](/help/sites-cloud/authoring/assets/templates-page-policy.png)

* 您可以从&#x200B;**选择策略**&#x200B;下拉列表中为页面选择现有策略。

   ![策略选择器](/help/sites-cloud/authoring/assets/templates-policy-selector.png)

   此外，也可以通过选择&#x200B;**选择策略**&#x200B;下拉列表旁边的“添加”按钮，来添加新策略。然后，应该在&#x200B;**策略标题**&#x200B;字段中输入一个新标题。

   ![“添加策略”按钮](/help/sites-cloud/authoring/assets/templates-add-policy-button.png)

   使用&#x200B;**选择策略**&#x200B;下拉列表旁边的“复制”按钮，可复制在此下拉列表中选定的现有策略以将其作为新策略。然后，应该在&#x200B;**策略标题**&#x200B;字段中输入一个新标题。默认情况下，复制的策略的标题将为 **X 的副本**，其中 X 是被复制的策略的标题。

   ![“复制策略”按钮](/help/sites-cloud/authoring/assets/templates-copy-policy-button.png)

* 在&#x200B;**策略标题**&#x200B;字段中定义策略的标题。策略需要具有标题，以便能够轻松地在&#x200B;**选择策略**&#x200B;下拉列表中对其进行选择。

   ![策略标题](/help/sites-cloud/authoring/assets/templates-policy-title.png)

* **策略说明**&#x200B;字段中的策略说明是可选的。
* 在&#x200B;**同时使用该选定策略的其他模板**&#x200B;部分中，您可以轻松地查看同时也使用了&#x200B;**选择策略**&#x200B;下拉列表中的选定策略的其他模板。

   ![策略使用情况](/help/sites-cloud/authoring/assets/templates-policy-use.png)

#### 页面属性 {#page-properties}

使用&#x200B;**页面设计**&#x200B;对话框中的页面属性，您可以定义所需的客户端库。这些客户端库包含要与模板以及使用该模板创建的页面一起加载的样式表和 JavaScript。

![页面属性](/help/sites-cloud/authoring/assets/templates-page-properties.png)

* 指定要应用于使用此模板创建的页面的客户端库。 在的文本字段中输入库的名称 **客户端库** 部分。

   ![客户端库](/help/sites-cloud/authoring/assets/templates-client-side-libraries.png)

* 如果需要多个库，请单击“添加”按钮，以添加更多用于填写库名称的文本字段。

   ![“添加”按钮](/help/sites-cloud/authoring/assets/templates-add-button.png)

   为您的客户端库添加所需数量的文本字段。

* 通过使用拖动手柄拖动字段，根据需要定义库的相对位置。

   ![拖动手柄](/help/sites-cloud/authoring/assets/templates-drag-handle.png)

>[!NOTE]
>
>虽然模板作者可以在模板上指定页面策略，但是他们需要从开发人员处获取相应客户端库的详细信息。

### 编辑模板 – 初始页面属性 – 作者 {#editing-a-template-initial-page-properties-author}

使用&#x200B;**初始页面属性**&#x200B;选项，您可以定义要在创建生成页面时使用的初始[页面属性](/help/sites-cloud/authoring/fundamentals/page-properties.md)。

1. 在模板编辑器中，从工具栏中选择&#x200B;**页面信息**，然后选择&#x200B;**初始页面属性**&#x200B;以打开相应的对话框。

1. 在该对话框中，您可以定义要对使用此模板创建的页面应用的属性。

   ![模板初始页面属性](/help/sites-cloud/authoring/assets/templates-initial-properties.png)

1. 通过以下方式确认您的定义 **完成**.

## 最佳实践 {#best-practices}

在创建模板时，您应该考虑：

1. 从模板创建页面后对模板进行更改的影响。

   下面列出了对模板可能执行的不同操作，以及这些操作对根据这些操作创建的页面有何影响：

   * 对结构的更改：

      * 这些操作会立即应用于生成的页面。
      * 访客仍需要发布更改的模板，才能看到所做的更改。
   * 对内容策略和设计配置的更改：

      * 这些规则将立即应用于生成页面。
      * 访客需要发布更改才能查看更改。
   * 对初始内容的更改：

      * 这些选项仅适用于对模板进行更改后创建的页面。
   * 布局更改取决于修改的组件是否属于以下组件：

      * 仅结构 — 立即应用
      * 包含初始内容 — 仅在更改后创建的页面上

   在下列情况下，请特别注意：

   * 在启用的模板上锁定或解锁组件。
   * 这会带来一些副作用，因为现有页面已可以使用该功能。 通常：

      * 现有页面上将缺少解锁组件（已锁定）的功能。
      * 锁定组件（可编辑）会隐藏该内容，使其无法在页面上显示。

   >[!NOTE]
   >
   >在不再是草稿的模板上更改组件的锁定状态时，AEM会给出显式警告。

1. [创建您自己的文件夹](#creating-a-template-folder-admin) 特定站点模板的位置。
1. [发布模板](#publishing-a-template-template-author) 从 **模板** 控制台。
