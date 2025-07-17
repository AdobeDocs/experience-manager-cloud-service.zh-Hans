---
title: 在HTML5表单中创建自定义外观
description: 您可以将自定义构件插入到Mobile Forms。 您可以扩展现有的jQuery构件或开发自己的自定义构件。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
docset: aem65
feature: HTML5 Forms,Mobile Forms
exl-id: 76bd1e2d-9e65-452c-8cef-123d28886a62
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 22aeedaaf4171ad295199a989e659b6bf5ce9834
workflow-type: tm+mt
source-wordcount: '662'
ht-degree: 0%

---

# 在HTML5表单中创建自定义外观{#create-custom-appearances-in-html-forms}

<span class="preview"> HTML5 Forms功能作为提前访问计划的一部分提供。 要请求访问，请将您的官方（工作）电子邮件ID通过电子邮件发送到aem-forms-ea@adobe.com。
</span>

您可以将自定义构件插入到Mobile Forms。 您可以扩展现有的jQuery小组件，也可以使用外观框架开发自己的自定义小组件。 XFA引擎使用各种小组件，有关详细信息，请参阅自适应表单和HTML5表单的[外观框架](/help/forms/custom-widgets.md)。

![默认和自定义构件的示例](assets/custom-widgets.jpg)

默认小部件和自定义小部件的示例

## 将自定义构件与HTML5 Forms集成 {#integrating-custom-widgets-with-html-forms}

### 创建用户档案  {#create-a-profile-nbsp}

您可以创建配置文件或选择现有配置文件以添加自定义构件。 有关创建配置文件的详细信息，请参阅[创建自定义配置文件](/help/forms/custom-profile.md)。

### 创建构件 {#create-a-widget}

HTML5 forms提供了一个构件框架实现，可以对该框架进行扩展以创建新构件。 该实现是一个jQuery小组件&#x200B;*abstractWidget*，可以扩展它以编写新的小组件。 只有通过扩展/覆盖以下提及的函数，才能使新构件正常工作。

<table>
 <tbody>
  <tr>
   <td>函数/类</td>
   <td>描述</td>
  </tr>
  <tr>
   <td>渲染</td>
   <td>渲染函数为小组件的默认HTML元素返回jQuery对象。 默认的HTML元素应为可聚焦类型。 例如，&lt;a&gt;、&lt;input&gt;和&lt;li&gt;。 返回的元素用作$userControl。 如果$userControl指定上述约束，则AbstractWidget类的函数将按预期工作，否则，某些常用API（集中、单击）需要更改。 </td>
  </tr>
  <tr>
   <td>getEventMap</td>
   <td>返回将HTML事件转换为XFA事件的映射。 <br /> {<br /> blur： XFA_EXIT_EVENT，<br /> }<br />此示例显示该blur是一个HTML事件，而XFA_EXIT_EVENT是相应的XFA事件。 </td>
  </tr>
  <tr>
   <td>getOptionsMap</td>
   <td>返回一个映射，该映射提供更改选项时要执行的操作的详细信息。 这些键是提供给构件的选项，值是每当检测到该选项发生更改时调用的函数。 小组件为所有常用选项（value和displayValue除外）提供处理程序</td>
  </tr>
  <tr>
   <td>getcommitvalue</td>
   <td>每当小部件的值保存在XFAModel中（例如，在textField的退出事件中）时，Widget框架就会加载函数。 该实施应返回保存在小组件中的值。 将为处理程序提供选项的新值。</td>
  </tr>
  <tr>
   <td>show值</td>
   <td>默认情况下，在XFA输入事件中，显示该字段的rawValue。 调用此函数是为了向用户显示rawValue。 </td>
  </tr>
  <tr>
   <td>showdisplayvalue</td>
   <td>默认情况下，在退出事件的XFA中，显示该字段的formattedValue 。 调用此函数是为了向用户显示formattedValue。 </td>
  </tr>
 </tbody>
</table>

要创建自己的小组件，请在上面创建的配置文件中，包含JavaScript文件的引用，该文件包含被覆盖的函数和新添加的函数。 例如，*sliderNumericFieldWidget*&#x200B;是数值字段的小部件。 要在用户档案中的标题部分中使用构件，请包括以下行：

```javascript
window.formBridge.registerConfig("widgetConfig" , widgetConfigObject);
```

### 向XFA脚本引擎注册自定义构件  {#register-custom-widget-with-xfa-scripting-engine-nbsp}

当自定义构件代码准备就绪时，请使用适用于`registerConfig`表单Bridge[的](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-65/content/forms/developer-reference/form-bridge-apis)API在脚本引擎中注册该构件。 它将widgetConfigObject作为输入。

```javascript
window.formBridge.registerConfig("widgetConfig",
        {
        ".<field-identifier>":"<name-of-the-widget>"
        }
    );
```

#### widgetConfigObject {#widgetconfigobject}

构件配置作为JSON对象（键值对的集合）提供，其中键标识字段，值表示用于这些字段的构件。 示例配置如下所示：

```
*{*

*"identifier1" : "customwidgetname",
"identifier2" : "customwidgetname2",
..
}*
```

其中，“identifier”是一个jQuery CSS选择器，它表示特定字段、特定类型的一组字段或所有字段。 下面列出了标识符在不同情况下的值：

| 标识符类型 | 标识符 | 描述 |
|---|---|---|
| 名为fieldname的特定字段 | 标识符：&quot;div.fieldname&quot; | 所有名为“fieldname”的字段都使用小组件渲染。 |
| &#39;type&#39;类型的所有字段（其中，类型为NumericField、DateField等）:  | 标识符： &quot;div.type&quot; | 对于Timefield和DateTimeField，类型为textfield，因为这些字段不受支持。 |
| 所有字段 | 标识符： &quot;div.field&quot; |  |
