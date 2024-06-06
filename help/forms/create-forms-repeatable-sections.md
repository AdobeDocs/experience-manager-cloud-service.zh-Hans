---
title: 如何在自适应表单核心组件中创建可重复面板？
description: 了解如何在自适应表单中创建一个或多个可重复的部分。
role: Architect, Developer, Admin, User
feature: Adaptive Forms, Core Components
exl-id: 02521bf3-83c1-40a0-8fe6-23af240727e9
source-git-commit: d3c5adf0b5b2155308e0bf9f4459682f11b67780
workflow-type: tm+mt
source-wordcount: '1258'
ht-degree: 8%

---

# 创建包含可重复部分的表单（核心组件） {#repeat-panel}


| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/creating-forms-repeatable-sections.html?lang=en) |
| AEM as a Cloud Service | 本文 |

可重复部分是指可为同一数据的多个实例收集信息而重复或多次重复的表单的一部分。

例如，请看一个用于收集个人工作经验信息的表单。您可以设置一个可重复的分区，用于记录以前每份工作的详细信息。可重复分区通常包含公司名称、职位、就业日期和工作职责等字段。用户可以在可重复分区中添加多个实例，以输入有关他们所做过的每项工作的信息。

![重复性](/help/forms/assets/repeatable-adaptive-form-example.gif)

读完本文后，您将学会：

* 在自适应表单中创建可重复部分
* 设置自适应表单组件的最小或最大重复次数
* 使用规则编辑器为可重复部分配置添加或删除操作

您可以使用 [面板](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel-container.html)， [折叠](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion.html)， [水平选项卡](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/horizontal-tabs.html)， [垂直选项卡](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/vertical-tabs)  或 [向导](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard.html) 组件使自适应表单的部分可重复。 可将子组件添加到这些组件中，以在表单中创建可重复部分。


本文档中的示例基于 [面板](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel-container.html) 组件。 您可以执行相同的步骤，以使 [面板](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel-container.html)， [折叠](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion.html)， [水平选项卡](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/horizontal-tabs.html)， [垂直选项卡](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/vertical-tabs) 或 [向导](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard.html) 组件可重复。

## 添加或删除表单中的可重复部分 {#add-or-delete-repeatable-section-in-panel-container}

要在表单中重复面板或删除可重复面板，表单作者使用按钮组件添加或删除面板的实例。 在表单中添加或删除可重复部分（面板）：

* [使面板容器可重复](#make-panel-container-repeatable)
* [添加可重复部分](#add-repeatable-section-using-instance-manager-via-scripts)
* [删除可重复部分](#delete-repeatable-section-using-instance-manager-via-scripts)

### 使面板容器可重复 {#make-panel-container-repeatable}

![“辅助功能”选项卡](/help/forms/assets/repeat-panel.png)

要使面板可重复，请执行以下步骤：
1. 选择面板容器并选择 ![cmppr](/help/forms/assets/cmppr.png).
1. 单击 **重复面板** 并切换到 **使面板可重复**.
1. 设置 **最小重复次数** 根据最小可重复部分的要求，您可以设置 **最小重复次数** 零表示面板不重复，或移除重复的面板。 默认情况下，最小重复次数值为0。
1. 设置 **最大重复次数** 要重复面板所需的次数，该值默认为infinite。

   >[!NOTE]
   >
   > 
   > * 最小重复次数不能为 — ve值。
   > * 要创建不可重复的面板，请将最大和最小字段的值设置为1。

### 使用实例管理器（通过脚本）添加可重复部分 {#add-repeatable-section-using-instance-manager-via-scripts}

要重复的面板的父级应包含一个“添加”按钮来管理面板的重复实例。 执行以下步骤将按钮插入到父代，并在按钮上启用脚本：

1. 添加 **按钮组件** 到面板的父项。 在以下示例视频中，显示了一个带有标签名称的按钮组件 **添加** 和字段名称 **添加面板**，使用。 选择组件并选择 ![edit-rules](/help/forms/assets/edit-rules.png). 按钮组件的规则将在规则编辑器中打开。
1. 在规则编辑器窗口中，单击 **创建**.

   选择 **可视编辑器** 表单对象和函数行中的。

   1. 在规则区域的WHEN下，选择state **已单击**.
   1. 在THEN下，选择 **添加实例**，并使用拖放面板 ![切换侧面板](/help/forms/assets/toggle-side-panel.png) 或使用以下方式选择它 **拖放对象或在此选择。**

   选择 **代码编辑器** 表单对象和函数行中的。 单击 **编辑规则** 在代码区域中：

   * 要创建添加面板按钮，请指定 `this.panel.instanceManager.addInstance()`

   单击&#x200B;**完成**。

>[!VIDEO](https://video.tv.adobe.com/v/3421052/adaptive-forms-repeatable-sections-repeat-sections/?quality=12&learn=on)


### 使用实例管理器（通过脚本）删除可重复部分 {#delete-repeatable-section-using-instance-manager-via-scripts}

面板的父级应包含一个删除按钮，用于删除可重复面板的实例。 执行以下步骤以将按钮插入到父项，并在按钮上启用脚本以删除可重复的面板：

1. 添加 **按钮组件** 至面板的父面板，在下面的视频中，显示一个具有标签名称的按钮组件 **删除** 和字段名称 **DeletePanel** 已使用。 选择组件并选择 ![edit-rules](/help/forms/assets/edit-rules.png). 按钮组件的规则将在规则编辑器中打开。
1. 在规则编辑器窗口中，单击 **创建**.

   选择 **可视编辑器** 表单对象和函数行中的。

   1. 在规则区域中的WHEN下 **DeletePanel**，选择状态 **已单击**.
   1. 在THEN下，选择 **删除实例**，并使用拖放面板 ![切换侧面板](/help/forms/assets/toggle-side-panel.png) 或使用以下方式选择它 **拖放对象或在此选择。**

   选择 **代码编辑器** 表单对象和函数行中的。 单击 **编辑规则** 在代码区域中：

   * 要创建删除面板按钮，请指定 `this.panel.instanceManager.removeInstance(this.panel.instanceIndex)`

   单击&#x200B;**完成**。
>[!VIDEO](https://video.tv.adobe.com/v/3421620/adaptive-forms-repeatable-sections)

>[!NOTE]
>
>如果某个字段属于可重复面板，则无法在脚本中使用该字段名称直接访问该字段。 要访问字段，请使用指定字段所属的可重复实例 `instances` 中的API `InstanceManager`. 要使用的语法 `instances` 中的API `InstanceManager` 为：
>
>
>`<panelName>.instanceManager.instances[<instanceNumber>].<fieldname>`
>
>
>例如，创建一个带有文本框的可重复面板的自适应表单。 使用三个可重复的文本框预填表单时，您需要以下xml：
>
>
>`<panel1><textbox1>AA1</panel1></textbox1>`
>
>
>`<panel1><textbox1>AA2</panel1></textbox1>`
>
>
>`<panel1><textbox1>AA3</panel1></textbox1>`
>
>
>要读取AA1数据，请指定：
>
>
>`Panel1.instanceManager.instances[0].textbox.value`
>
>
>要读取AA2数据，请指定：
>
>
>`Panel1.instanceManager.instances[1].textbox.value`
>
>
>

<!-- 
>For more information, see: Class: InstanceManager#instances in [AEM Forms Java API reference](https://adobe.com/go/learn_aemforms_documentation_63).      
-->

>[!NOTE]
>
> 从自适应表单中删除面板的所有实例时，要添加已删除面板的实例，请使用_panelName语法捕获面板的实例管理器，并使用实例管理器的addInstance API添加已删除的实例。 例如，_panelName.addInstance()。 它会添加已删除面板的一个实例。

<!--
![panel-repeatability-video](/help/adaptive-forms/assets/panel-repeatability-video.mp4)
-->

<!--

## Using the accordion layout for the parent panel &nbsp; {#using-the-accordion-layout-for-the-parent-panel-nbsp}

A panel has various layouts options. The Layout for accordian design option has out of the box support for repeatable panels. Perform the following steps to repeatable panel with Layout for accordian design option:

1. On the parent of panel to be repeated, select ![cmppr](assets/cmppr.png). You can see the properties in the sidebar. In the **Layout** drop-down, select **Accordion**.
1. On a panel, which is to be repeated, select ![cmppr](assets/cmppr.png). You can see the panel properties in the sidebar. Enable the **Make Panel Repeatable** tab, and specify value for the **Maximum** and **Minimum** fields.

   Now, you can use the plus (+) and delete ( ![delete-panel](assets/delete-panel.png)) buttons to add and remove the panels.

-->

## 使用表单模板中的重复子表单(XDP/XSD) {#using-repeating-subforms-from-form-template-xdp-xsd}

可重复子表单类似于自适应Forms中的可重复面板。 在AEM Forms Designer中，执行以下步骤以创建重复的子表单：

1. 在层级调色板中，选择要重复的子表单的父子表单。
1. 在“对象”面板中，单击“子表单”选项卡，然后在“内容”列表中选择“流式”。
1. 选择要重复的子表单。
1. 在“对象”面板中，单击“子表单”选项卡，然后在“内容”列表中选择“已定位”或“已流动”。
1. 单击“绑定”选项卡，并为每个数据项选择“重复子表单”。
1. 要指定最小重复次数，请选择最小计数，然后在关联的框中键入一个数字。 如果将此选项设置为0，并且在数据合并时没有为子表单中的对象提供数据，则在呈现表单时不会放置子表单。
1. 要指定子表单重复的最大次数，请选择“最大”，然后在相关框中键入一个数字。 如果未在“最大值”框中指定值，则子表单的重复次数将无限制。
1. 要指定一组子表单重复次数，而不考虑数据量，请选择初始计数，然后在关联框中键入一个数字。 如果选择此选项，并且没有可用数据或存在的数据条目少于指定的初始计数值，则子表单的空实例仍会放置在表单上。
1. 在父子表单中添加两个按钮 — 一个用于添加实例，另一个用于删除可重复子表单的实例。 有关详细步骤，请参阅 [构建操作](https://help.adobe.com/en_US/AEMForms/6.1/DesignerHelp/WS107c29ade9134a2c74572b5612a87ca2b56-8000.2.html#WS107c29ade9134a2c-1f74d86012a87d4fe55-8000.2).
1. 现在，将表单模板链接到自适应表单。 有关详细步骤，请参阅 [基于模板创建自适应表单](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/creating-adaptive-form.html?lang=en#create-an-adaptive-form-based-on-an-xfa-form-template).
1. 使用在第9步中创建的按钮添加和删除子表单。

附加的.zip文件包含一个示例可重复的子表单。

[获取文件](/help/forms/assets/samplerepeatablesubform.zip)

## 使用XML架构(XSD)的重复设置 {#using-repeat-settings-of-an-xml-schema-xsd-br}

您可以从XML架构和任何复杂类型元素的minOccours和maxOccurs属性创建可重复面板。 有关XML架构的详细信息，请参见 [使用XML架构作为表单模型创建自适应表单](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/adaptive-form-xml-schema-form-model.html).

在以下代码中， `SampleType`面板使用minOccurs和maxOccurs属性。

```xml
<?xml version="1.0" encoding="utf-8" ?>
    <xs:schema targetNamespace="https://adobe.com/sample.xsd"
                    xmlns="https://adobe.com/sample.xsd"
                    xmlns:xs="https://www.w3.org/2001/XMLSchema"
                >

        <xs:element name="sample" type="SampleType"/>

        <xs:complexType name="SampleType">
            <xs:sequence>
                <xs:element name="leaderName" type="xs:string" default="Enter Name"/>
                <xs:element name="assignmentStartDate" type="xs:date"/>
                <xs:element name="gender" type="GenderEnum"/>
                <xs:element name="noOfProjectsAssigned" type="IntType"/>
                <xs:element name="assignmentDetails" type="AssignmentDetails"
                                            minOccurs="0" maxOccurs="10"/>
            </xs:sequence>
        </xs:complexType>

        <xs:complexType name="AssignmentDetails">
            <xs:attribute name="name" type="xs:string" use="required"/>
            <xs:attribute name="durationOfAssignment" type="xs:unsignedInt" use="required"/>
            <xs:attribute name="numberOfMentees" type="xs:unsignedInt" use="required"/>
             <xs:attribute name="descriptionOfAssignment" type="xs:string" use="required"/>
             <xs:attribute name="financeRelatedProject" type="xs:boolean"/>
       </xs:complexType>
  <xs:simpleType name="IntType">
            <xs:restriction base="xs:int">
            </xs:restriction>
        </xs:simpleType>
  <xs:simpleType name="GenderEnum">
            <xs:restriction base="xs:string">
                <xs:enumeration value="Female"/>
                <xs:enumeration value="Male"/>
            </xs:restriction>
        </xs:simpleType>
    </xs:schema>
```


## 另请参阅 {#see-also}

{{see-also}}

<!--

>[!MORELIKETHIS]
>
>* [Create an Adaptive Form](creating-adaptive-form-core-components.md)
>* [Create style or themes for your forms](using-themes-in-core-components.md)
>* [Add dynamic behavior to forms using the rule editor](rule-editor.md)
>* [Set layout of forms for different screen sizes and device types](/help/sites-cloud/authoring/features/console-layout.md)

-->