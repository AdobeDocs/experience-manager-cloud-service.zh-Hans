---
title: 为HTML5表单创建CSS样式
description: 了解如何通过修改与HTML表单元素关联的CSS类来更改HTML5表单的外观。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: a8d986ab-2a4c-488b-957e-4606f7391bd3
feature: HTML5 Forms,Mobile Forms
exl-id: 8cc90ff7-284e-41cd-bfda-7fa09371e270
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 22aeedaaf4171ad295199a989e659b6bf5ce9834
workflow-type: tm+mt
source-wordcount: '838'
ht-degree: 3%

---

# 为HTML5表单创建CSS样式 {#creating-css-styles-for-html-forms}

<span class="preview"> HTML5 Forms功能作为提前访问计划的一部分提供。 要请求访问，请将您的官方（工作）电子邮件ID通过电子邮件发送到aem-forms-ea@adobe.com。
</span>

基于XFA的表单模板的HTML5演绎版包含多个HTML元素。 这些元素按顺序排列。 每个元素都有明确定义的CSS类。 您可以使用这些CSS类选择和更改元素的外观。

>[!NOTE]
>
>在CSS类中，请勿更改width、height、border-thickness、top、left、right、bottom、padding、margin以及其他位置和大小属性的值。 位置和大小属性的任何更改都会使表单的布局发生变化。

## CSS类  用于元素  {#css-classes-nbsp-for-elements-nbsp}

每个元素都包含明确定义的CSS类。 可以修改这些类以更改元素的外观。 每个元素（字段和绘制元素除外）都有两个CSS类 — Type类和Name类。

* **Type类**&#x200B;表示XFA字段的类型。 您可以覆盖`type`类以修改特定类型的所有元素的样式。

* **Name类**&#x200B;对应于XFA字段的名称。 您可以覆盖`name`类以修改自定义样式并将其应用于元素。

>[!NOTE]
>
>某些XFA元素没有名称。 要更改此类组件的样式，请修改该特定类型的所有组件。

对于AEM Forms Designer中未命名的页面，HTML5表单中的页面将按其数量的递增顺序进行命名。 例如，对于具有两个页面的HTML5表单，这些页面将命名为Page1、Page2。

## 字段元素 {#field-element}

字段元素包含两个嵌套元素：小部件和标题。

**小组件元素**

构件元素包含用于与用户交互的用户界面元素。 它有三个CSS类：

* **小组件**：每个小组件都有此类。
* **name**： AEM随附的所有构件都包含构件名称类。 对于自定义构件，构件开发人员提供构件名称类。
* **类型**：每个小组件都有一个用户界面元素。 此类定义用户界面元素的类型。

```xml
<!--field with caption-->
<div class="field numericfield NumericField3 ">
     <div class="caption">
        caption content
     </div>
     <div class="widget numericfieldwidget numericInput">
       widget content
     </div>
</div>

<!--field without caption-->
<div class="widget numericfieldwidget numericInput">
   widget content
</div>
```

除了类型和名称类之外，字段组件还包含一个名为&#x200B;**子类型**&#x200B;的附加CSS类。 子类型标识它的字段类型，例如NumericField、DateField、TextField。 可以覆盖子类型类来修改所有类型、子类型字段的样式。

## 不同组件的CSS类 {#css-classes-for-different-components}

<table>
 <tbody>
  <tr>
   <td><strong>组件</strong></td>
   <td><strong>类型</strong></td>
   <td><strong>名称</strong></td>
  </tr>
  <tr>
   <td>页面</td>
   <td>页面</td>
   <td>用户定义的名称<br />或<br /> Page&lt;pageNumber&gt;（默认）</td>
  </tr>
  <tr>
   <td>内容区域</td>
   <td>contentarea</td>
   <td>用户定义的名称</td>
  </tr>
  <tr>
   <td>子表单</td>
   <td>子表单</td>
   <td>用户定义的名称</td>
  </tr>
  <tr>
   <td>排除组</td>
   <td>排除组</td>
   <td>用户定义的名称</td>
  </tr>
  <tr>
   <td>Draw</td>
   <td>draw</td>
   <td>用户定义的名称</td>
  </tr>
  <tr>
   <td>字段</td>
   <td>字段</td>
   <td>用户定义的名称</td>
  </tr>
  <tr>
   <td>题注</td>
   <td>题注</td>
   <td>NA</td>
  </tr>
  <tr>
   <td>小组件</td>
   <td>构件</td>
   <td>构件开发人员定义它（对于用户定义的构件，请参阅下节中的表）</td>
  </tr>
 </tbody>
</table>

## 不同字段的CSS类 {#css-classes-for-different-fields}

AEM Forms Designer支持表单中各种类型的字段，如NumericField、DecimalField和Date Field。 HTML中的所有这些字段都包含上述CSS类。 它们还包含一些额外的类，具体取决于字段类型。

每个字段都有一个表示UI元素的关联构件。 下面列出了每个字段的类以及与每个字段关联的构件。

<table>
 <tbody>
  <tr>
   <td><strong>字段类型</strong></td>
   <td><strong>子类型</strong></td>
   <td><strong>构件名称</strong></td>
   <td><strong>构件类型</strong></td>
   <td><strong>HTML UI标记</strong></td>
  </tr>
  <tr>
   <td>按钮<br type="_moz" /> </td>
   <td>NA</td>
   <td>xfaButton<br type="_moz" /> </td>
   <td>buttonfieldwidget<br type="_moz" /> </td>
   <td>输入类型=按钮<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>CheckButton<br type="_moz" /> </td>
   <td>checkboxfield<br /> </td>
   <td>XfaCheckBox<br type="_moz" /> </td>
   <td>checkboxfieldwidget<br type="_moz" /> </td>
   <td>输入类型=复选框<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>日期字段<br type="_moz" /> </td>
   <td>datefield<br type="_moz" /> </td>
   <td>日期字段<br type="_moz" /> </td>
   <td>datefieldwidget<br type="_moz" /> </td>
   <td>输入类型=文本<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>日期时间字段<br type="_moz" /> </td>
   <td>textfield<br type="_moz" /> </td>
   <td>textField<br type="_moz" /> </td>
   <td>文本字段小组件</td>
   <td>输入类型=文本<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>DecimalField<br type="_moz" /> </td>
   <td>numericfield<br type="_moz" /> </td>
   <td>numericInput<br type="_moz" /> </td>
   <td>numericfieldwidget<br type="_moz" /> </td>
   <td>输入类型=文本<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>下拉列表<br type="_moz" /> </td>
   <td>choicelist<br type="_moz" /> </td>
   <td>dropDownListWidget<br type="_moz" /> </td>
   <td>choicelistwidget<br type="_moz" /> </td>
   <td>选择</td>
  </tr>
  <tr>
   <td>列表框<br type="_moz" /> </td>
   <td>choicelist<br type="_moz" /> </td>
   <td>listBoxWidget<br type="_moz" /> </td>
   <td>choicelistwidget<br type="_moz" /> </td>
   <td>ol</td>
  </tr>
  <tr>
   <td>NumericField<br type="_moz" /> </td>
   <td>numericfield<br type="_moz" /> </td>
   <td>numericInput<br type="_moz" /> </td>
   <td>numericfieldwidget<br type="_moz" /> </td>
   <td>输入类型=文本<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>密码字段<br type="_moz" /> </td>
   <td>密码字段<br type="_moz" /> </td>
   <td>defaultWidget<br type="_moz" /> </td>
   <td>passwordfieldwidget<br type="_moz" /> </td>
   <td>输入类型=密码<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>单选按钮<br type="_moz" /> </td>
   <td>无线电场<br type="_moz" /> </td>
   <td>XfaCheckBox<br type="_moz" /> </td>
   <td>radiofieldwidget<br type="_moz" /> </td>
   <td>输入类型=radio<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>TextField<br type="_moz" /> </td>
   <td>textfield<br type="_moz" /> </td>
   <td>textField<br type="_moz" /> </td>
   <td>textfieldwidget<br type="_moz" /> </td>
   <td>输入类型=文本<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>时间字段<br type="_moz" /> </td>
   <td>textfield<br type="_moz" /> </td>
   <td>textField<br type="_moz" /> </td>
   <td>textfieldwidget<br type="_moz" /> </td>
   <td>输入类型=文本<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

## 不同绘制元素的CSS类 {#css-classes-for-different-draw-elements}

您可以使用AEM Forms Designer插入静态绘制元素，如文本和图像。 对于每个绘制元素，单独的CSS类与该元素关联。 绘制元素的CSS类列表如下所列。 每个绘制元素都有一个与之关联的绘制类。

| **绘制类型** | **CSS类** |
|---|---|
| 文本 | text |
| 图像 | 图像 |
| 矩形 | 矩形 |
| 线形图 | 折线图 |

## 设置窗体其他部分的样式 {#styling-other-parts-of-the-form}

除了HTML表单中UI组件的外观之外，您还可以更改元素的样式，如内联错误、内联警告和有验证错误的字段。

`Styling Inline Errors`

如果字段的验证导致错误，则字段处于活动状态时会显示内联错误。 要更改内联错误的样式，请覆盖CSS ID **error-msg**。

`Styling Inline Warnings`

当字段的验证导致警告时，如果字段处于活动状态，则显示内联警告。 若要更改这些内联警告的样式，请覆盖CSS ID **warning-msg**。

`Styling Fields with Validation Errors`

当字段验证失败时，小组件的样式会更改。 此样式更改通过在构件组件上应用CSS类&#x200B;**widgetError**&#x200B;来完成。 要修改默认样式，请覆盖&#x200B;**widgetError**&#x200B;类。
