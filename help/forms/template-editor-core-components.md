---
title: 如何基于核心组件创建自适应表单模板？
description: 使用模板编辑器基于核心组件创建自适应表单模板以定义基本结构和初始内容。
feature: Adaptive Forms, Core Components
Keywords: create adaptive form template, create adaptive form template based on core components, Use template to create adpative form.
exl-id: c1c050d3-953e-4e56-a96b-d84f2ec05e5e
source-git-commit: eaab351460363b83c7d3667e048235506cc71c41
workflow-type: tm+mt
source-wordcount: '1961'
ht-degree: 4%

---

# 创建基于核心组件的自适应表单模板 {#adaptive-form-templates}

在创作表单时，可在编辑器中添加字段和组件以定义表单结构、内容和操作。 您可以在 `guideRootPanel` 表单容器的。 使用模板编辑器，您可以创建一个模板，其中包含作者可用于创建表单的基本结构和初始内容。

例如，您希望所有表单作者在注册表单中都拥有某些文本框、导航按钮和提交按钮。 您可以创建一个模板，其中包含作者可用来创建与其他注册表单一致的表单的组件。 当作者使用模板创建自适应表单时，新表单会继承您在模板中指定的结构和组件。 通过模板编辑器，您可以：

* 在结构层中添加表单的页眉和页脚组件。
* 提供表单的初始内容。
* 指定主题“提交操作”。

<!--
You can download and install [!DNL AEM Forms] reference content package from [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html) portal to import reference themes and templates to your environment.
-->

## 先决条件

**为您的环境启用自适应Forms核心组件**：在创建项目时，已为您的环境启用自适应Forms核心组件。 如果您有一个表单as a Cloud Service环境，基于 [AEM Archetype 39或更早版本](https://github.com/adobe/aem-project-archetype)， [为您的环境启用自适应Forms核心组件](enable-adaptive-forms-core-components.md).

>[!NOTE]
>
> 在部署基于Archetype 45的Formsas a Cloud Service环境时， **自适应Forms（核心组件）** 模板和基于组件的核心主题会添加到您的环境中。

## 使用模板 {#working-with-templates}

您可以从“工具”菜单导航到，访问模板编辑器 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL 工具]** > **[!UICONTROL 常规]** > **[!UICONTROL 模板]**. 在此处，模板在启用可编辑模板的文件夹中进行组织。

>[!NOTE]
>
> 您可以在特定于核心组件的文件夹中找到基于核心组件的可编辑模板。

Experience Manager提供了一个全局文件夹来组织模板。 但是，默认情况下不启用此功能。 您可以请求管理员启用全局文件夹或创建模板文件夹。 有关如何创建文件夹的详细信息，请参阅 [模板文件夹](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/features/templates.html#editing-templates-template-authors).

## 创建模板 {#create-template}

创建文件夹后，打开该文件夹并执行以下步骤以创建模板：

1. 选择 **[!UICONTROL 创建]** 在您创建的文件夹内。
1. 在 **[!UICONTROL 选择模板类型]** 部分，选择 **[!UICONTROL 自适应表单（核心组件）模板]** 并选择 **[!UICONTROL 下一个]**.

1. 在 **[!UICONTROL 模板详细信息]** 部分，提供 **模板标题** 并选择 **[!UICONTROL 创建]**.
您还可以提供描述。

1. 选择 **[!UICONTROL 完成]** 以返回到控制台，或选择 **[!UICONTROL 打开]** 以在编辑器中打开模板。

## 模板编辑器用户界面 {#template-editor-ui}

在打开模板进行编辑时，您可以看到以下AEM Editor组件：

* **页面工具栏**
包含以下选项：

   * **切换侧面板**：用于显示或隐藏侧栏。
   * **页面信息**：用于指定发布/取消发布时间、缩略图、客户端库、页面策略和页面设计客户端库等信息。
     <!-- * **Emulator**: Lets you simulate and customize the look for different devices.-->
   * **模式选择器：** 允许您更改模式。 您可以选择 **[!UICONTROL 结构]** 模式， **[!UICONTROL 初始内容]**， **[!UICONTROL 布局控件]** 模式。 结构模式允许您添加和自定义页眉和页脚。 初始内容模式允许您自定义表单内容。
   * **预览：** 允许您预览发布模板时的外观。 您可以使用“图层选择器”和“预览”来切换编辑和预览模式。
* **侧栏：** 提供内容、属性、资源和组件浏览器。
* **组件工具栏：** 选择某个组件后，您将看到一个工具栏，其中允许您自定义该组件。
* **页面**：添加内容以创建模板的区域。

<!-- See [Introduction to authoring Adaptive Forms](introduction-forms-authoring.md) to understand the Touch UI editor. -->

## 编辑模板 {#editing-a-template}

选择和编辑模板的相应方面的不同模式包括：

* [结构](#structure)
* [初始内容](#initial-content)
* [布局](#layout)

图层选择器位于屏幕右上角的“预览”选项旁边。

### 结构 {#structure}

在模板编辑器中选择结构层时，它有助于预定义在创建与模板关联的自适应Forms时无法更改的内容。

<!-- you can see the layout containers above and below the Adaptive Form Container. Authors can use these layout containers for header and footer. -->


![在结构层中布局容器](/help/forms/assets/header-layer-selector-core-component.png)

<!--

**A. Layout container for Header component**
Drag-drop the Adaptive Form Header component in the layout container above the Adaptive Form Container. After you add the component, you can specify its properties that let you add a logo and provide its title.
**B. Adaptive Form Container component**
Drag-drop the Adaptive Form components in the Adaptive Form Container. You can specify the design and arrangement of fields and components in the template editor. After you add the components, you can specify its properties.
**C. Layout container for Footer component**
Similarly, when you drag-drop the footer component in the layout container below the Adaptive Form Container, you can provide the copyright information and company details. 
You can add, edit, or customize the header and footer. Drag-drop the Adaptive Form Header and Footer component to customize the template. Drag-drop the Adaptive Form components in the Adaptive Form Container. You can specify the design and arrangement of fields and components in the template editor. 


Header and footer are added in the Initial Content layer.
-->

#### 在结构层中锁定/解锁组件 {#locking-unlocking-components-in-the-structure-layer}

在选定结构层的情况下编辑模板时，可以解锁模板的页眉和页脚。 如果在模板中解锁了某个组件，则表单作者可以在使用该模板的自适应表单中编辑该组件。 锁定组件会阻止表单作者在自适应表单中进行编辑。 “锁定”选项在组件工具栏中可用。

例如，在模板中添加标题组件。 选择组件后，您会在组件工具栏中看到一个锁定选项。 通常，页眉包括公司名称和徽标，并且您不希望表单作者更改模板中的徽标和页眉。 在锁定标题组件且使用模板创建的自适应表单中，表单作者无法更改徽标和公司名称。

>[!NOTE]
>
>不建议单独锁定或解锁页眉组件中的图像或徽标。 您可以解锁标头组件。

### 初始内容 {#initial-content}

选择初始内容选项后，模板的自适应表单容器会像要编辑的自适应表单一样打开。 它允许您创建预定义内容，在创建与模板关联的自适应Forms时可以更改这些内容。 与创作自适应表单一样，您可以指定初始设置，例如选择主题和提交操作。

表单作者可将其用作创建表单的基础。 内容流结构在模板的初始内容层中指定。 要切换到编辑表单模板的初始内容，请在页面工具栏中的预览之前，选择 ![画布下拉列表](assets/canvas-drop-down.png) **>** **[!UICONTROL 初始内容]**.

![在初始内容层中添加了页眉和页脚](assets/header-and-footer.png)

在初始内容层中，创建作者用作基础的自适应表单模板。 创作模板与创作表单类似，只是使用侧栏中提供的选项。 侧栏提供内容、属性、资源和组件浏览器。

<!-- See [Sidebar](introduction-forms-authoring.md#sidebar). -->

>[!NOTE]
>
>选择“存储内容”或“存储PDF”作为“提交操作”时，您将获得一个用于指定存储路径的选项。 如果在模板中指定路径，则使用该模板创建的所有表单都具有相同的路径。 您可以指定正确的存储路径，或确保表单作者对其进行更新，以防止每个表单中的数据存储在同一位置。

### 布局 {#layout}

编辑模板时，您可以定义布局，这会使用标准响应式布局。 布局有助于根据设备宽度管理组件宽度，以促进响应式自适应表单设计。

![在结构层中布局容器](/help/forms/assets/layout-template-core-component.png)

请参阅文章 [了解响应式布局](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/page-authoring/responsive-layout-feature-video-understand.html?lang=en) 以了解其他信息。

## 启用模板 {#enabling-the-template}

创建模板时，模板会添加为草稿。 启用模板以将其用于创建自适应Forms。 要启用模板：

1. 导航到 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL 工具]** > **[!UICONTROL 模板]**，然后打开已在其中创建模板的文件夹。
您创建的模板将标记为草稿。
1. 选择模板并选择 **[!UICONTROL 启用]** 工具栏中。
在创建自适应表单时，如果要求您选择模板，则可以看到列出的模板。

## 导入或导出模板 {#importing-or-exporting-a-template}

表单可与其模板配合使用。 下载使用自定义模板创建的自适应表单时，不会下载该模板。 当您在不同页面上导入表单时 [!DNL AEM Forms] 例如，导入时没有使用模板。 如果表单已导入，但其模板不可用，则不会呈现表单。 您可以从以下位置打包自定义模板 `/conf` 中的节点 `https://<server>:<port>/crx/packmgr`，并将其移植到 [!DNL AEM Forms] 要上载表单的实例。 您还可以 [使用AEM原型创建模板并将其部署到Cloud Service实例](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/pages-templates.html#prerequisites).

>[!NOTE]
>
> * 您还可以配置 [!UICONTROL 记录文档] 直接从自适应表单编辑器或自适应表单模板编辑器中访问模板。 有关更多信息，请参阅 [为自适应Forms生成记录文档](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#document-of-record-support-in-adaptive-form-editor-dor-support-in-adaptiveform).

## 将表单数据模型架构关联到模板 {#associating-form-data-model-schema-in-template}

作者可以关联 [!UICONTROL 表单数据模型架构] 到模板编辑器中的自适应表单模板。 它允许作者从模板编辑器中选择架构。 在将架构与模板关联并且表单作者基于模板创建表单时，系统会为表单预先选择架构。 它有助于表单作者规范架构的使用，同时为表单作者节省时间。 要在模板编辑器中选择表单数据模型架构，请执行以下操作：

1. 选择 **[!UICONTROL 内容浏览器]** 位于左侧。
1. 转到表单容器 **[!UICONTROL 设置]**.
1. 选择 **[!UICONTROL 数据模型]**.
1. 通过以下方式选择您的表单数据模型 **[!UICONTROL 选择表单数据模型]** 并保存配置。

![Form-Data-Model-Association-in-Forms](/help/forms/assets/select-form-data-model-img-core-component.png)

<!--

## Creating an Adaptive Form template with tabs and panels {#creating-an-adaptive-form-template-with-tabs-and-panels-nbs}

For example, you want to create a template with the following tabs:

* General Information
* Professional Information

You have added a logo, provided a title, and added a footer in the structure layer. Lock the header and footer to stop form authors from editing them when they use the template to create forms.

Change the layer from **Structure** to **Initial Content**, and start adding content to the form. To create a tabbed structure, add a child Panel in the guideRootPanel of the Adaptive Form container. To add a panel:

* You can add a panel by tapping the **[!UICONTROL +]** button when you select the **[!UICONTROL Drag components here]** option.

* You can drag-drop the panel component from the components browser in the sidebar.
* You can add child panel of the `guideRootPanel` from the component toolbar.

To create the General Information and Professional Information tabs, add two panels in the child panel of the `guideRootPanel`. Select the panels and select ![cmppr](assets/configure-icon.svg) to open the properties in the sidebar. Change the element names as `general-info` and `professional-info`, and titles as General Information and Professional Information respectively. In the sidebar, select content to open the content browser. In the Form Objects tab, select `guideRootPanel`. In the editor, the guideRootPanel is selected. Select ![cmppr](assets/configure-icon.svg) in the component toolbar to open its properties. In the Panel Layout field, select **[!UICONTROL Tabs on Top]** and select **[!UICONTROL Done]**. The tabbed template structure is applied.

### Adding content in tabs {#adding-content-in-tabs}

After you add panels and structure them as tabs, you can add fields inside the tabs. When you select a tab in the editor, you can see the **[!UICONTROL Drag components here]** option. You can drag-drop components such as text-boxes, list items, and buttons. You can drag-drop components from the components browser in the sidebar.

Each component has properties that enhance data capturing and manipulation. For example, you can enable the **[!UICONTROL Required field]** property of a component. Your authors can specify a message that your customers see when they skip filling a required field. Specify the message in **[!UICONTROL Required Field Message]** property.

In the example template, Name, Phone number, and Date of birth fields are added in the General Information tab. In the Professional Information tab, Currently employed, employment type, Educational qualification fields are added.

After you have added fields, you can add buttons such as Submit and Reset.
-->

### 使用模板策略将自定义属性添加到自适应表单组件

通过自定义属性，您可使用表单模板将自定义属性（键值对）关联到自适应表单核心组件。自定义属性反映在 **[!UICONTROL 属性]** 组件的headless演绎版的部分。 它可让您创建根据自定义属性值进行调整的动态表单行为。例如，开发人员可以为移动、桌面或 Web 平台设计 Headless 表单组件的各种演绎版，从而大大提升各种设备上的用户体验。

将自定义属性添加到自适应表单核心组件字段的步骤如下：

1. [在模板编辑器的策略中添加自定义组名称](#add-a-custom-group-name)
1. [在自适应表单组件的“编辑”对话框中选择自定义组名称](#select-a-custom-group-name)

#### 在模板编辑器的策略中添加自定义组名称 {#add-a-custom-group-name}

1. 转到 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL 工具]** > **[!UICONTROL 常规]** > **[!UICONTROL 模板]**.
1. 选择基于核心组件的模板，并以编辑模式打开它。
1. 单击 **[!UICONTROL 策略]** ![策略](/help/forms/assets/Smock_FeedManagement_18_N.svg) 需要定义自定义属性的自适应表单核心组件字段的图标。 此 **[!UICONTROL 自适应表单字段]** 出现对话框。
1. 选择 **[!UICONTROL 自定义属性]** 选项卡。
1. 指定 **[!UICONTROL 策略标题]** 在 **[!UICONTROL 策略]** 部分。
1. 指定 **[!UICONTROL 组名称]** 和添加与特定组关联的键值对。 在组件的“编辑”对话框中，组名称对表单作者可见。 如果选择组名称，则每个关联的键值对都适用于组件。
1. 单击&#x200B;**[完成]**。

![在模板编辑器中添加自定义属性组名称](/help/forms/assets/custom-properties-core-component.png)

使用模板策略添加至少一个自定义属性组时， **[!UICONTROL 高级]** 选项卡在相应的核心组件的“编辑”对话框中变为可见。

#### 在核心组件的“编辑”对话框中选择自定义组名称 {#select-a-custom-group-name}

1. 在编辑模式下打开自适应表单。
1. 选择已在模板编辑器中为其定义了自定义属性的组件，然后选择 ![settings_icon](assets/configure-icon.svg) 以打开组件的“编辑”对话框。
1. 选择 **[!UICONTROL 高级]** 选项卡。
1. 从中选择自定义属性组名称 **[!UICONTROL 自定义属性选择]** 下拉菜单。 所有定义的自定义组名称将自动填充到下拉列表中。
1. 选择 **[!UICONTROL 完成]** 以保存属性。

![选择自定义属性组名称](/help/forms/assets/select-custom-properties-group-name.png)

>[!NOTE]
>
> * 此 **[!UICONTROL 其他自定义属性]** 复选框允许您动态添加特定于组件的自定义属性，以及模板策略中提供的属性。 当键名称值匹配时，特定组件的自定义属性优先于模板策略中设置的自定义属性。

## 使用模板创建自适应表单 {#creating-an-adaptive-form-using-the-template}

创建并启用模板后，在创建自适应表单时，表单管理器中会提供该模板。 要使用模板和创建自适应表单，请参阅 [基于核心组件创建自适应表单](/help/forms/creating-adaptive-form-core-components.md).
<!--
## Change display option of out of the box templates  {#change-display-option-of-out-of-the-box-templates}

You can create custom templates for Adaptive Forms to define basic structure and initial content. [!DNL AEM Forms] also provides a set of out of the box template for Adaptive Forms. You can choose to show or hide the templates.

Perform the following steps to show and hide templates:

1. Log in to [!DNL AEM Forms] author instance and navigate to **[!UICONTROL Tools]** &gt; **[!UICONTROL Operations]** &gt; **[!UICONTROL Web Console]**.

   >[!NOTE]
   >
   >The URL of AEM web console is https://'[server]:[port]'/system/console/configMgr

1. Locate and open the **FormsManager Configuration** settings:

    * To show or hide out of the box Adaptive Forms template, check or uncheck the **Include Out of the box AF and AD Templates** option.
    * To show or hide out of the box Adaptive Form templates that were added in AEM 6.0 Forms or AEM 6.1 Forms releases but are now deprecated, check or uncheck the **Include AEM 6.0 AF Templates** option. If this option is checked, and you want it to take effect, it requires the **Include Out of the box AF and AD Templates** configuration to be enabled.

1. Click **Save**. The display options for the out of the box templates are changed. 

## Save an Adaptive Form as a template {#saving-adaptive-form-as-template}

You can also save an Adaptive Form as a template for future use. To save a Adaptive Form as a template:

1. Select an Adaptive Form to save it as a template.
1. Click **[!UICONTROL Save as Template]**. A dialog box appears.
1. Specify **[!UICONTROL Title]** (mandatory field), **[!UICONTROL Location]** (mandatory field) and **[!UICONTROL Description]** (optional field) for the template. 
1. Click **[!UICONTROL Create]**.

   ![Save as Form as Template](/help/forms/assets/saveformastemplate.png)



>[!NOTE]
>
>To use the same container policy as of the source Adaptive Form, it is recommended to save the template in the same folder as of the source Adaptive Form. In case, the template is saved in any other folder, than the created template uses a default container policy.
-->

## 最佳实践 {#best-practices}

* 使用基于核心组件的组件创建模板，例如自适应表单文本、自适应表单容器等。 要获取有关自适应Forms核心组件的信息， [单击此处](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html).
* 限制模板的数量以匹配网站上提供的截然不同的表单类型
* 为模板中使用的自定义组件提供必要的灵活性和配置功能。

<!--
## See next

* [Create style or themes for your forms](using-themes-in-core-components.md)
* [Create an Adaptive Form (core components)](/help/forms/creating-adaptive-form-core-components.md)

-->

## 另请参阅 {#see-also}

{{see-also}}
* [为表单创建样式或主题](using-themes-in-core-components.md)
* [创建自适应表单（核心组件）](/help/forms/creating-adaptive-form-core-components.md)

