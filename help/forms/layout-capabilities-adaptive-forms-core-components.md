---
title: 基于核心组件的自适应Forms的布局功能是什么？
description: 自适应Forms在各种设备上的布局和外观受布局设置控制。 了解各种布局及其应用方式。
feature: Adaptive Forms, Core Components
keywords: 基于核心组件的自适应表单布局、表单的不同布局、动态表单布局AEM、AEM Cloud Service表单布局、AEM核心组件中的表单布局类型、自适应表单布局
role: User, Developer, Admin
source-git-commit: b06d86ffc620327a744f53733e3bf84fe8c03f2f
workflow-type: tm+mt
source-wordcount: '2107'
ht-degree: 1%

---


# 基于核心组件的自适应Forms的布局功能


| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/layout-capabilities-adaptive-forms.html) |
| AEM as a Cloud Service（基础组件） | [单击此处](/help/forms/layout-capabilities-adaptive-forms.md) |
| AEM as a Cloud Service（核心组件） | 本文 |

自适应Forms提供一流的组件，可高效地布局和设计表单。 布局控制组件在表单中的显示方式。 自适应Forms支持各种布局：面板、向导、折叠面板、位于顶部/水平选项卡的选项卡以及位于左侧/垂直选项卡的选项卡。

![布局类型](/help/forms/assets/generic-layout-hero-image.png){align="center"}

## 先决条件

在浏览布局的各种功能之前，请确保为环境启用了核心组件。 有关如何为您的环境启用核心组件的详细说明，请[单击此处](/help/forms/enable-adaptive-forms-core-components.md)。

## 自适应Forms布局类型

基于核心组件的自适应表单支持以下类型的布局：
* **面板布局**
* **向导布局**
* **垂直布局**
* **水平布局**
* **折叠布局**

>[!BEGINTABS]

>[!TAB 面板布局]

面板布局有助于以更便于导航和查找相应内容的方式组织相关字段。 面板布局将表单组件排列在自适应表单的不同部分或面板中。

![面板布局](/help/forms/assets/panel-layout.png){width="250" align="center"}

面板布局

您可以使用[面板组件](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel)在表单中添加面板布局。 有关如何配置面板组件的各种属性的详细说明，请参阅[面板组件](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel)文章。

>[!TAB 向导布局]

向导布局通过将复杂表单划分为不同的步骤来帮助简化该表单。 每个步骤代表流程的不同部分，用户按顺序浏览这些步骤，通常使用&#x200B;**下一个**&#x200B;和&#x200B;**上一个**&#x200B;按钮。 您可以使用向导布局创建包含多个部分或步骤的表单。

![向导布局](/help/forms/assets/wizard-layout-compare.gif){width="250" align="center"}

向导布局

您可以使用[向导组件](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard)在表单中添加向导布局。 有关如何配置向导组件的各种属性的详细说明，请参阅[向导组件](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard)一文。

>[!TAB 垂直制表符布局]

垂直选项卡布局也称为左侧布局中的选项卡。 垂直选项卡布局沿表单左侧组织面板或区域。 这是一种表单的常见布局，其中面板/部分垂直栈叠以方便阅读和导航。

![垂直布局](/help/forms/assets/vertical-tab.gif){width="250" align="center"}

垂直选项卡布局

您可以使用[垂直制表符组件](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/vertical-tabs)在表单中添加垂直制表符布局。 有关如何配置垂直选项卡组件的各种属性的详细说明，请参阅[垂直选项卡组件](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/vertical-tabs)文章。


>[!TAB 水平选项卡布局]

水平选项卡布局也称为顶部布局中的选项卡。 水平选项卡布局将面板或区域并排排列。 此布局以线性方式跨窗体或面板的宽度显示窗体部分。


![水平布局](/help/forms/assets/horizontal-layout.gif){width="250" align="center"}

水平选项卡布局

您可以使用[水平选项卡组件](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/horizontal-tabs)在表单中添加水平选项卡布局。 有关如何配置水平选项卡组件的各种属性的详细说明，请参阅[水平选项卡组件](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/horizontal-tabs)文章。


>[!TAB 折叠布局]

折叠布局在自适应表单中以可折叠部分或面板显示内容。 展开某个部分时，会在其中显示内容，而其他部分仍保持折叠状态。 此布局非常适用于以紧凑形式显示大量信息。

![折叠布局](/help/forms/assets/accordion-layout-compare.gif){width="250" align="center"}

可折叠项布局

您可以使用[折叠组件](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion)在表单中添加折叠布局。 有关如何配置折叠组件的各种属性的详细说明，请参阅[折叠组件](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion)文章。

>[!ENDTABS]

要了解如何插入布局并向其中添加表单组件，请参阅标题为[如何插入布局并向其中添加表单组件？](#how-to-insert-a-layout-and-add-form-components-to-it)

### 如何选择正确的自适应表单布局？

选择正确的自适应表单布局以优化用户体验和表单功能很重要。 该表可帮助您了解可用的各种布局选项，并指导您根据特定需求和用例选择最合适的布局：

| 专题 | 面板布局 | 向导布局 | 选项卡在顶部/垂直选项卡布局中 | 选项卡位于左侧选项卡/水平选项卡布局 | 可折叠项布局 |
|--------------------------|-----------------------------------------------------|----------------------------------------------------|-----------------------------------------------------|--------------------------------------------------------|--------|
| **目的** | 将相关内容分组为不同的部分 | 指导用户完成多步骤流程或表单 | 允许在同一页面上的各个部分/视图之间切换 | 与顶部选项卡类似，但在左侧垂直排列 | 将内容整理到可折叠部分中 |
| **结构** | 不同的部分 | 连续步骤/页面 | 顶部的水平选项卡 | 左侧垂直选项卡 | 可折叠面板/区域 |
| **导航** | 单击面板标题以进行导航 |  — 前进：“下一步”按钮<br> — 后退：“后退”按钮<br> — 可选跳过步骤 | 单击选项卡以切换节 | 单击选项卡以切换节 | 单击标题可展开/折叠部分 |
| **用户体验** | 以可管理的方式组织大量内容 | 逐步指导，减少负担 | 清晰、可访问的视图间切换 | 有效利用垂直空间，始终显示选项卡 | 具有展开/折叠部分的紧凑视图 |
| **用例** | 具有已分类分区的复杂表单 | 设置流程，复杂表单 | 组织设置或内容类别 | 仪表板、复杂数据视图 | 常见问题解答、设置菜单、详细内容部分 |


## 如何插入布局并向其中添加表单组件？

下图显示了将布局插入表单并将表单组件添加到表单的步骤：

![用于添加布局和表单组件的工作流](/help/forms/assets/workflow-to-add-component-to-a-layout.png)

考虑在[自适应Forms布局类型](#adaptive-forms-layout-types)部分中显示的&#x200B;**IT请求表单**。 该表单从遇到网络或笔记本电脑相关技术问题的员工那里收集信息。 它包括三个面板：

* **员工详细信息**：该面板收集有关该员工的信息，并包含三个标有“姓名”、“电子邮件ID”和“部门”的文本框。

* **问题详细信息**：面板捕获有关问题的详细信息。 它包括一个用于问题类别的复选框，带有三个选项：“网络”、“计算机”或“其他”。 它还具有两个标有“请指定”和“注释”的文本框。

* **附件**：该面板允许用户上载与问题相关的支持文档。

让我们来探索插入布局并向其中添加组件的分步流程。 在此示例中，水平制表符布局插入到表单中。

### 1.在表单中插入布局组件

1. 登录到您的[!DNL Experience Manager Forms]实例。
1. 选择左上角的&#x200B;**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms和文档]**。
1. 在编辑模式下打开现有的自适应表单（如果已经创建）。

   ![打开自适应表单](/help/forms/assets/insert-layout.png){width="250" align="center"}

   或者，您也可以[创建新的自适应表单](/help/forms/creating-adaptive-form-core-components.md)。

1. 在表单编辑器中找到用于添加布局的部分。

   ![表单编辑器](/help/forms/assets/form-editor.png){width="200" align="center"}
1. 单击&#x200B;**添加**&#x200B;图标。 图标是一个加号(+)，表示添加新组件的选项。

   ![插入布局](/help/forms/assets/insert-layout-add-icon.png){width="200" align="center"}

   单击&#x200B;**添加**&#x200B;图标会显示&#x200B;**插入新组件**&#x200B;对话框，其中显示了要插入的各种组件。

   >[!NOTE]
   >
   > 或者，您也可以[拖放布局组件](#extra-bytes)。

1. 浏览对话框中的可用组件，并从列表中选择所需的布局。 在本例中，我们选择“水平选项卡”组件来插入水平选项卡布局。

   ![选择水平制表符](/help/forms/assets/select-horizontal-tab.png){width="200" align="center"}

   将水平选项卡组件添加到表单时，它最初由两个空面板组成，默认情况下分别名为Item1和Item2。 您需要手动将表单组件添加到这些面板。

   ![水平选项卡](/help/forms/assets/insert-tabs-on-top.png){width="200" align="center"}

1. 打开水平选项卡组件的属性，并指定组件的名称。
例如，在本例中，我们将水平选项卡组件的名称添加为IT请求表单。

   ![添加水平选项卡的名称](/help/forms/assets/change-name-of-horizontal-tabs.png){width="200" align="center"}

1. 单击&#x200B;**完成**。

   ![水平选项卡](/help/forms/assets/tabs-on-top-rename-component.png){width="200" align="center"}

在表单中添加布局组件后，根据需要修改面板数量。

### 2.将面板添加到布局中

将新面板添加到水平选项卡组件：

1. 打开水平选项卡组件属性，然后单击&#x200B;**项目**&#x200B;选项卡。

   水平选项卡的![项选项卡](/help/forms/assets/tabs-on-top-items-tab.png){width="200" align="center"}

2. 单击&#x200B;**添加**&#x200B;图标以添加新面板。

   ![添加新面板](/help/forms/assets/tabs-on-top-add-panel.png){width="200" align="center"}

   单击&#x200B;**添加**&#x200B;图标时，将显示&#x200B;**插入新组件**&#x200B;对话框。

3. 选择面板组件。

   ![添加新面板](/help/forms/assets/tabs-on-top-new-panel.png){width="200" align="center"}

   选择面板组件后，新面板将添加到水平布局中。

   ![添加新面板](/help/forms/assets/tabs-on-top-add-new-panel.png){width="200" align="center"}

   为新面板提供一个名称；否则，无法保存水平选项卡组件的属性。

4. 指定面板的名称，如下图所示：

   ![面板名称](/help/forms/assets/tabs-on-tops-panel-name.png){width="200" align="center"}

5. 单击&#x200B;**完成**。

   单击&#x200B;**完成**&#x200B;后，三个面板会并排显示。 面板名称显示为每个面板的标题，您可以将表单组件添加到每个面板。

   ![面板名称](/help/forms/assets/tabs-on-top-initial-view.png){width="200" align="center"}

   您可以配置面板组件的属性。 例如，IT请求表单不包括面板标题，以下是配置面板组件属性的步骤。

6. 打开第一个面板的属性。

   ![面板1属性](/help/forms/assets/tabs-on-tops-panel1-properties.png){width="200" align="center"}

7. 从&#x200B;**Basic**&#x200B;选项卡中选择&#x200B;**隐藏标题**&#x200B;复选框。

   ![隐藏标题](/help/forms/assets/tabs-on-top-hide-panel.png){width="200" align="center"}

8. 单击&#x200B;**完成**。

同样，也可以隐藏其他两个面板的标题。 完成后，您可以继续将表单组件添加到每个面板。

### 3.将表单组件添加到面板

<!-- You can employ one of the following method to add form components to the panel:
* [Add components to a layout's panel using the Add icon](#add-components-to-a-layouts-panel-using-the-add-icon)
* [Drag and drop components into a layout's panel](#drag-and-drop-components-into-a-layouts-panel) -->

1. 在允许您添加组件的面板中查找部分。
1. 单击&#x200B;**添加**图标。 图标是一个加号(+)，表示添加新组件的选项。
   ![插入布局](/help/forms/assets/tabs-on-top-add-component.png){width="200" align="center"}

   单击&#x200B;**添加**&#x200B;图标会显示&#x200B;**插入新组件**&#x200B;对话框，其中显示了要插入的各种组件。

   ![插入新组件对话框](/help/forms/assets/insert-new-component.png){width="200" align="center"}

1. 浏览出现的对话框中的可用组件，然后选择所需的组件。 在本例中，选择文本框组件。
1. 打开所添加组件的属性并指定其名称。 允许编辑已添加文本框组件的属性并指定其名称。
   ![插入布局](/help/forms/assets/tabs-on-top-textbox-component.png){width="200" align="center"}
1. 同样，添加另外两个文本框组件，名称将这两个组件添加为电子邮件ID和部门。\
   ![第一个面板](/help/forms/assets/tabs-on-tops-first-panel.png){width="200" align="center"}

   现在，第一个面板中的组件已添加，您可以继续将组件添加到第二个面板。

1. 若要切换面板，请单击工具栏中的&#x200B;**选择面板**。

   ![切换面板](/help/forms/assets/tabs-on-top-select-panel.png){width="200" align="center"}

   单击&#x200B;**选择面板**&#x200B;时，水平选项卡组件中已添加面板的列表即会显示。

   ![切换面板](/help/forms/assets/tabs-on-tops-panel2.png){width="200" align="center"}

1. 从面板列表中选择&#x200B;**2面板**，视图将从第一个面板更改为第二个面板。

   ![第二个面板](/help/forms/assets/tabs-on-top-panel2-component.png){width="200" align="center"}

1. 重复步骤2到步骤4中所述的步骤，在面板2中添加所需的组件，如下图所示：

   ![第二个面板组件](/help/forms/assets/panel-2-components.png){width="200" align="center"}

1. 按照步骤6和步骤7中所述的步骤切换到&#x200B;**3面板**。

1. 重复步骤2到步骤4中列出的步骤，在面板3中添加所需的组件：

   ![第三面板组件](/help/forms/assets/panel-3-component.png){width="200" align="center"}

1. 单击创作环境右上角的&#x200B;**[!UICONTROL 预览]**。

   ![水平布局](/help/forms/assets/horizontal-layout.gif){width="250" align="center"}

您也可以[拖放组件](#extra-bytes)以将表单组件添加到每个面板。


<!-- #### Drag and drop components into a layout's panel 

1. Locate the section within the panel that allows you to add components. 
2. Navigate to the left panel within your authoring environment and click **Components**.

    ![Component Panel](/help/forms/assets/add-new-component.png){width="200" align="center"}

    When you click the **Components** option, the list of the available components appears.   

    ![Component Panel](/help/forms/assets/add-new-component2.png){width="200" align="center"}

3. Browse the available components and select the Text Box component.

4. Drag the component by clicking and holding the selected component, then drag it over to the panel area to place it.

5. Drop the component into the panel by releasing the mouse. 

6. Open the properties of the added Text Box component and specify its name as Name.
    ![Insert layout](/help/forms/assets/tabs-on-top-textbox-component.png){width="200" align="center"}
7. Similarly, add two more Text Box components and name added the components as Email ID and Department.   
    ![First Panel](/help/forms/assets/tabs-on-tops-first-panel.png){width="200" align="center"}

    Now that the components in the first panel have been added, you can proceed with adding the components to the second panel. 

8. To switch the panel, click **Select Panel** from the toolbar. 

    ![Switch Panel](/help/forms/assets/tabs-on-top-select-panel.png){width="200" align="center"}

    When you click the **Select Panel**, the list of the added panels in the Horizontal Tabs component appears.

    ![Switch Panel](/help/forms/assets/tabs-on-tops-panel2.png){width="200" align="center"}

9. Select **2 Panel** from the panel list and the view changes from the first panel to the second panel.

    ![Second Panel](/help/forms/assets/tabs-on-top-panel2-component.png){width="200" align="center"}

10. Repeat the steps outlined from Step 2 to Step 6 for adding the desired components in panel 2 as shown in the below figure:   

     ![Second Panel components](/help/forms/assets/panel-2-components.png){width="200" align="center"}

11. Switch to the **3 Panel** by following the steps outlined in Step 8 and Step 9.

12. Repeat the steps outlined from Step 2 to Step 6 for adding the desired component in panel 3:

    ![Third Panel components](/help/forms/assets/panel-3-component.png){width="200" align="center"} 

    -->



您还可以使用![删除图标](/help/forms/assets/Smock_Delete_18_N.svg)图标从面板中删除表单组件。

![删除组件](/help/forms/assets/delete-component.png){width="200" align="center"}

您还可以根据需要为组件添加所需的验证。

## 如何使用新布局替换现有布局？

您可以使用新布局替换表单的布局，其中涉及修改组件在表单中的排列和显示方式。



执行以下步骤以替换表单的现有布局：

1. 单击布局组件工具栏中的替换图标，此时将显示&#x200B;**[!UICONTROL 替换组件]**&#x200B;对话框。

   ![替换布局](/help/forms/assets/replace-layout.png){width="200" align="center"}

1. 从&#x200B;**[!UICONTROL 替换组件]**&#x200B;对话框中选择所需的布局。

   ![替换组件对话框](/help/forms/assets/replace-component.png){width="200" align="center"}

   选择布局后，布局中组件的排列方式会相应发生变化。 例如，从&#x200B;**[!UICONTROL 替换组件]**&#x200B;对话框中选择垂直选项卡组件；面板的排列方式将更改为左侧的选项卡：

   ![垂直布局](/help/forms/assets/vertical-tab.gif){width="250" align="center"}

## 额外字节

要将组件拖放到表单编辑器中，请执行以下步骤：

1. 找到用于添加组件的部分。
1. 导航到创作环境中的左侧面板，然后单击&#x200B;**组件**。

   ![组件面板](/help/forms/assets/add-new-component.png){width="200" align="center"}

   单击&#x200B;**组件**&#x200B;选项时，将显示可用组件列表。

   ![组件面板](/help/forms/assets/add-new-component2.png){width="200" align="center"}

1. 浏览可用的组件并选择所需的组件。

1. 单击并按住选定的组件以拖动该组件，然后将其拖动到面板区域以放置它。

1. 释放鼠标将组件放入面板中。

## 后续步骤

在熟悉基于核心组件的自适应表单的各种布局功能后，您可以继续后续步骤：

* [根据核心组件创建您的第一个自适应表单](/help/forms/creating-adaptive-form-core-components.md)
* [创建和使用自适应表单主题](/help/forms/using-themes-in-core-components.md)



## 另请参阅

{{see-also}}