---
title: 如何创建自适应表单模板？
description: 使用模板编辑器创建自适应表单模板以定义基本结构和初始内容。
exl-id: a882cba2-c621-4ff7-a972-c504641b5639
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '2018'
ht-degree: 1%

---

# 创建自适应表单模板 {#adaptive-form-templates}

在创作表单时，可在编辑器中添加字段和组件以定义表单结构、内容和操作。 您可以在 `guideRootPanel` 表单容器的。 使用模板编辑器，您可以创建一个模板，其中包含作者可用于创建表单的基本结构和初始内容。

例如，您希望所有表单作者在注册表单中都拥有特定的文本框、导航按钮和提交按钮。 您可以创建一个模板，其中包含作者可用来创建与其他注册表单一致的表单的组件。 当作者使用模板创建自适应表单时，新表单会继承您在模板中指定的结构和组件。 通过模板编辑器，您可以：

* 在结构层中添加表单的页眉和页脚组件。
* 提供表单的初始内容。
* 指定主题“提交操作”。

您可以下载并安装 [!DNL AEM Forms] 引用内容包来自 [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html) 门户，用于将引用主题和模板导入到您的环境。

## 使用模板 {#working-with-templates}

您可以从“工具”菜单导航到，访问模板编辑器 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL 工具]** > **[!UICONTROL 常规]** > **[!UICONTROL 模板]**. 在此，模板在启用可编辑模板的文件夹中进行组织。

Experience Manager提供了一个全局文件夹来组织模板。 但是，默认情况下不启用它。 您可以请求管理员启用全局文件夹或为模板创建文件夹。 有关如何创建文件夹的详细信息，请参阅 [模板文件夹](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/features/templates.html#editing-templates-template-authors).

### 创建模板 {#create-template}

创建文件夹后，打开该文件夹并执行以下步骤以创建模板：

1. 点按 **[!UICONTROL 创建]** 在您创建的文件夹内。
1. 在“选择模板类型”部分中，选择 **[!UICONTROL 自适应表单模板]** 并点按 **[!UICONTROL 下一个]**.

1. 在模板详细信息部分，提供模板标题并点按 **[!UICONTROL 创建]**.
您还可以提供描述。

1. 点按 **[!UICONTROL 完成]** 以返回到控制台，或点按 **[!UICONTROL 打开]** 以在编辑器中打开模板。

### 模板编辑器用户界面 {#template-editor-ui}

在打开模板进行编辑时，您可以看到以下AEM Editor组件：

* **页面工具栏**
包含以下选项：

   * **切换侧面板**：用于显示或隐藏侧栏。
   * **页面信息**：用于指定发布/取消发布时间、缩略图、客户端库、页面策略和页面设计客户端库等信息。
     <!-- * **Emulator**: Lets you simulate and customize the look for different devices.-->
   * **模式选择器：** 允许您更改模式。您可以选择 **[!UICONTROL 结构]** 模式， **[!UICONTROL 初始内容]**， **[!UICONTROL 布局控件]** 模式。 “结构”模式允许您添加和自定义页眉和页脚。 初始内容模式允许您自定义表单内容。
   * **预览：** 允许您预览模板在发布时的外观。 您可以使用“图层选择器”和“预览”来切换编辑和预览模式。
* **侧栏：** 提供“内容”、“属性”、“资产”和“组件”浏览器。
* **组件工具栏：** 选择某个组件后，您将看到一个工具栏，通过该工具栏可自定义该组件。
* **页面**：添加内容以创建模板的区域。

<!-- See [Introduction to authoring Adaptive Forms](introduction-forms-authoring.md) to understand the Touch UI editor. -->

### 编辑模板 {#editing-a-template}

自适应表单模板使用两层创建：

* 结构
* 初始内容

图层选择器位于屏幕右上角的“预览”选项旁边。

### 结构 {#structure}

在模板编辑器中选择结构层时，您可以看到自适应表单容器的上方和下方的布局容器。 作者可以将这些布局容器用于页眉和页脚。 您可以添加、编辑或自定义页眉和页脚。 将自适应表单标题组件拖放到自适应表单容器上方的布局容器中，以自定义模板标题。 将自适应表单页脚组件拖放到自适应表单容器下的布局容器中，以自定义模板页脚。

![结构层中的布局容器](assets/header-layer-selector.png)

结构层中的布局容器

**答：** 标题组件的布局容器 **B.** 页脚组件的布局容器

将自适应表单标题组件拖放到自适应表单容器上方的布局容器中。 添加组件后，您可以指定其属性，以便添加徽标并提供其标题。

同样，将页脚组件拖放到自适应表单容器下方的布局容器中时，您可以提供版权信息和公司详细信息。

![在结构层中添加了页眉和页脚](assets/header-and-footer.png)

在结构层中添加了页眉和页脚

#### 结构层中的锁定/解锁组件 {#locking-unlocking-components-in-the-structure-layer}

在选定结构层的情况下编辑模板时，可以解锁模板的页眉和页脚。 如果在模板中解锁了组件，则表单作者可以在使用该模板的自适应表单中编辑该组件。 锁定组件会阻止表单作者在自适应表单中进行编辑。 “锁定”选项在组件工具栏中可用。

例如，在模板中添加标题组件。 选择组件后，您会在组件工具栏中看到一个锁定选项。 通常，页眉包括公司名称和徽标，并且您不希望表单作者更改模板中的徽标和页眉。 在标题组件被锁定且使用模板创建的自适应表单中，表单作者无法更改徽标和公司名称。

>[!NOTE]
>
>不建议单独锁定或解锁页眉组件中的图像或徽标。 您可以解锁标头组件。

### 初始内容 {#initial-content}

选择“初始内容”选项后，模板的自适应表单容器会像要编辑的自适应表单一样打开。 与创作自适应表单一样，您可以指定初始设置，例如选择主题和提交操作。

表单作者可将其用作创建表单的基础。 内容流结构在模板的“初始内容”层中指定。 要切换到编辑表单模板的初始内容，请在页面工具栏中的预览之前，点按 ![画布下拉列表](assets/canvas-drop-down.png) **>** **[!UICONTROL 初始内容]**.


在初始内容层中，创建作者用作基础的自适应表单模板。 创作模板与创作表单类似，只是使用侧栏中提供的选项。 侧栏提供内容、属性、资源和组件浏览器。

<!-- See [Sidebar](introduction-forms-authoring.md#sidebar). -->

>[!NOTE]
>
>选择“存储内容”或“存储PDF”作为“提交操作”时，您将获得一个用于指定存储路径的选项。 如果在模板中指定路径，则使用该模板创建的所有表单都具有相同的路径。 您可以指定正确的存储路径，或确保表单作者对其进行更新，以防止每个表单中的数据存储在同一位置。

#### 创建具有选项卡和面板的自适应表单模板 {#creating-an-adaptive-form-template-with-tabs-and-panels-nbsp}

例如，要创建具有以下选项卡的模板：

* 常规信息
* 专业信息

您已添加徽标、提供标题，并在结构图层中添加了页脚。 锁定页眉和页脚，以阻止表单作者在使用模板创建表单时编辑它们。

将图层从“结构”更改为“初始内容”，然后开始将内容添加到表单中。 要创建选项卡式结构，请在自适应表单容器的guideRootPanel中添加一个子面板。 要添加面板，请执行以下操作：

* 您可以通过点按 **[!UICONTROL +]** 按钮 **[!UICONTROL 将组件拖动到此处]** 选项。

* 您可以从组件浏览器中将面板组件拖放到侧栏中。
* 您可以添加的子面板 `guideRootPanel` （从组件工具栏）。

要创建“常规信息”和“专业信息”选项卡，请在的子面板中添加两个面板 `guideRootPanel`. 选择面板并点按 ![cmppr](assets/configure-icon.svg) 以打开侧栏中的属性。 将元素名称更改为 `general-info` 和 `professional-info`和职称分别作为“一般信息”和“专业信息”。 在侧栏中，点按内容以打开内容浏览器。 在表单对象选项卡中，选择 `guideRootPanel`. 在编辑器中，选择guideRootPanel。 点按 ![cmppr](assets/configure-icon.svg) 以打开其属性。 在“面板布局”字段中，选择 **[!UICONTROL 顶部选项卡]** 并点按 **[!UICONTROL 完成]**. 应用选项卡式模板结构。

#### 在选项卡中添加内容 {#adding-content-in-tabs}

在添加面板并将其结构为选项卡后，您可以在选项卡内添加字段。 在编辑器中选择选项卡时，您会看到 **[!UICONTROL 将组件拖动到此处]** 选项。 您可以拖放组件，例如文本框、列表项和按钮。 您可以从侧栏中的组件浏览器拖放组件。

每个组件都具有可增强数据捕获和处理的属性。 例如，您可以启用 **[!UICONTROL 必填字段]** 组件的属性。 您的作者可以指定客户在跳过填写必填字段时看到的消息。 在中指定消息 **[!UICONTROL 必填字段消息]** 属性。

在示例模板中，“姓名”、“电话号码”和“出生日期”字段添加到“一般信息”选项卡中。 在“专业信息”选项卡中，添加了“当前雇用”、“雇佣类型”、“教育资格”字段。

添加字段后，您可以添加“提交”和“重置”等按钮。

### 启用模板 {#enabling-the-template}

创建模板时，模板会添加为草稿。 启用模板以将其用于创建自适应Forms。 启用模板：

1. 导航到 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL 工具]** > **[!UICONTROL 模板]**，然后打开已在其中创建模板的文件夹。

1. 您创建的模板将标记为草稿。
1. 选择模板并点按 **[!UICONTROL 启用]** 工具栏中。
创建自适应表单时，如果系统要求您选择模板，您会看到模板已列出。

## 导入或导出模板 {#importing-or-exporting-a-template}

表单可与其模板配合使用。 下载使用自定义模板创建的自适应表单时，不会下载该模板。 当您在不同页面上导入表单时 [!DNL AEM Forms] 实例时，导入时不含其模板。 如果表单已导入，但其模板不可用，则不会呈现表单。 您可以从以下位置打包自定义模板 `/conf` 中的节点 `https://<server>:<port>/crx/packmgr`，并将其移植到 [!DNL AEM Forms] 要上载表单的实例。 您还可以 [使用AEM Archype创建模板并将其部署到Cloud Services实例](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/pages-templates.html#prerequisites).

>[!NOTE]
>
> * 您还可以配置 [!UICONTROL 记录文档] 自适应表单编辑器或自适应表单模板编辑器中的模板。 有关更多信息，请参阅 [为自适应Forms生成记录文档](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#document-of-record-support-in-adaptive-form-editor-dor-support-in-adaptiveform).


## 将表单数据模型架构关联到模板 {#associating-form-data-model-schema-in-template}

作者可以关联 [!UICONTROL 表单数据模型架构] 模板编辑器中的自适应表单模板。 它允许作者从模板编辑器中选择架构。 将架构与模板关联并且表单作者根据模板创建表单时，会为表单预先选择架构。 它有助于表单作者规范架构的使用，并节省表单作者的时间。 要在模板编辑器中选择表单数据模型架构，请执行以下操作：

1. 点按 **[!UICONTROL 内容浏览器]** 位于左侧。
1. 转到表单容器 **[!UICONTROL 设置]**.
1. 选择 **[!UICONTROL 数据模型]**.
1. 通过以下方式选择您的表单数据模型 **[!UICONTROL 选择表单数据模型]** 并保存配置。

![Form-Data-Model-Association-in-Forms](/help/forms/assets/select-form-data-model-img.png)



## 使用模板创建自适应表单 {#creating-an-adaptive-form-using-the-template}

创建并启用模板后，创建自适应表单时可在表单管理器中找到该模板。 要使用模板和创建自适应表单，请参阅 [创建自适应表单](creating-adaptive-form.md).


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

1. Click **Save**. The display options for the out of the box templates are changed. -->

## 将自适应表单另存为模板 {#saving-adaptive-form-as-template}

您还可以将自适应表单另存为模板以供将来使用。 要将自适应表单另存为模板，请执行以下操作：

1. 选择自适应表单以将其另存为模板。
1. 单击 **[!UICONTROL 另存为模板]**. 将显示一个对话框。
1. 指定 **[!UICONTROL 标题]** （必填字段）， **[!UICONTROL 位置]** （必填字段）和 **[!UICONTROL 描述]** （可选字段）。
1. 单击&#x200B;**[!UICONTROL 创建]**。

   ![另存为表单为模板](/help/forms/assets/saveformastemplate.png)



>[!NOTE]
>
>要使用与源自适应表单相同的容器策略，建议将模板保存在与源自适应表单相同的文件夹中。 如果模板保存在任何其他文件夹中，则创建的模板不会使用默认容器策略。

## 推荐 {#recommendations}

* 在模板编辑器中修改表单的属性时，请勿使用BindReference属性。
* 如果要添加断点，请在创作自适应表单模板时创建断点。
有关断点的详细信息，请参见 [响应式布局](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/features/responsive-layout.html#authoring).
