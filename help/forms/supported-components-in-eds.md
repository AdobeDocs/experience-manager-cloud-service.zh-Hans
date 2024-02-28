---
title: AEM Forms Edge Delivery Service表单组件
description: AEM Forms Edge交付服务专为实现卓越性能而打造，使您能够预见简化数据收集和用户参与的未来。 本文列出了可用于EDD表单的所有现成表单组件。
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: 1dc4915f0b149ef67dfa22c8d4c6be7538170d38
workflow-type: tm+mt
source-wordcount: '871'
ht-degree: 5%

---




# 表单块边缘交付中支持的HTML组件

AEM Forms Edge交付包含一个表单块。 表单块可帮助您轻松创建表单，以捕获和存储捕获的数据。

表单块支持HTML5组件，例如文本、电子邮件、数字、日期等。 它还支持文本区域、select和fieldset元素，并包括HTML-5固有的输入验证功能。 表单块为所有字段类型和容器创建统一的HTML结构，以确保一致性。 您也可以 [设置字段类型的样式](https://adobe-rnd.github.io/form-block/customization/styling_form) 使用 `form.css` 文件。

## 表单块中支持的HTML5输入类型

表单块支持一系列HTML5输入类型，它还无缝呈现使用AEM核心组件创建的表单。

下表概述了核心组件如何与Edge交付中的五个HTML输入类型相对应：

<table>
 <tbody>
  <tr>
   <td><b>核心组件</b> </td>
   <td><b>HTML5输入类型</b> </td>
   <td><b>详细信息</b></td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/form-container.html">表单容器</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#form">表单 </td>
   <td> 创建表单以捕获用户输入。
   </td>
  </tr>
  <tr>
   <td><a herf="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/text-input.html">文本输入</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/text">text</a></td>
   <td> 定义单行文本输入字段。 </td>
  </tr>
  <tr>
   <td><a href = "https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/number-input.html">数字输入</a></td>
   <td><a href = "https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/number">数字</a></td>
   <td>允许用户输入数字。 您还可以添加内置验证以拒绝非数字输入。 允许用户输入数字。 您还可以添加内置验证以拒绝非数字输入。 最初，输入字段显示为数字输入。 如果用户应用显示模式，它会更改为文本以允许作者应用数字格式，因为HTML5不支持显示模式。 但是，当用户单击它时，它会返回键入数字。</td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/date-picker.html">日期选取器</a></td>
   <td><a href = "https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/date">日期 </a></td>
   <td> 创建输入字段以输入日期。 您可以选择通过文本框（用于验证输入）或专用日期选取器界面输入日期。 最初，显示本机日期输入字段。 如果用户应用显示模式，它会更改为文本以允许用户应用格式，因为HTML5不支持显示模式。 但是，当用户单击它时，它会返回键入日期。</td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/file-attachment.html">文件附件</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/file">文件</a></td>
   <td> 允许用户从设备存储中选择一个或多个文件。 它支持增强的文件输入验证，例如接受的文件类型、文件大小限制和最小/最大文件选择限制。 </td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/drop-down.html"> 下拉列表</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select">选择</a></td>
   <td> 允许用户从预定义选项列表中选择一个或多个选项。 这些选项可以是字符串、数字或布尔类型。</td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/checkbox-group.html">复选框组</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/checkbox">多个复选框</a></td>
   <td> 允许用户从列表中选择一个或多个选项。 将生成多个名称相同的复选框，每个复选框均与枚举中的一个项目相对应。 </td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/radio-button.html">单选按钮群组</td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/radio">多收音机</a></td>
   <td> 允许用户从一组相关选项中选择一个选项。 生成多个名称相同的单选按钮，每个单选按钮均与枚举中的一个项目相对应。</td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/button.html">按钮</td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/button">按钮</a></td>
   <td>允许用户在单击时触发操作的UI元素。 </td>
  </tr>
  <tr>
   <td><a href="" https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel-container.html">面板</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset">带图例的字段集</a></td>
   <td> 对表单中的节进行分组，其中嵌套*legend*元素为表单添加标题。</td>
  </tr>
   <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard.html">向导</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset">字段集</a></td>
   <td>对表单中相关节进行分组。 它还控制排列，支持用于将其定位在顶部或左侧的显示选项。 </td>
  </tr>
    <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/text.html">文本</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/p">p</a></td>
   <td>p标记标记段落。 在可视内容中，段落是以空白行或缩进第一行分隔的文本块</td>
  </tr>
     <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/submit-button.html">“提交”按钮</td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/submit">提交</a></td>
   <td> 一个UI元素，它允许用户在单击时将表单提交到服务器。 如果用户将提交规则添加到按钮，则其功能相当于提交按钮。 </td>
  </tr>
     <tr>
   <td><a href = "https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/reset-button.html">“重置”按钮</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/reset">重置</a></td>
   <td>单击时重置表单的UI元素。 如果用户向按钮添加重置规则，则该规则将用作重置按钮。 </td>
  </tr>
    <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/email-input.html">电子邮件输入</td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/email">电子邮件</a></td>
   <td> 允许用户输入和编辑电子邮件地址。 如果用户添加多个属性，则可以添加或编辑电子邮件地址列表。</td>
  </tr>
   <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/telephone-input.html">电话输入</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/tel">电话</a></td>
   <td>允许用户输入和编辑电话号码。</td>
  </tr>
   <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/header.html">页眉</td>
   <td><a href = "https://developer.mozilla.org/en-US/docs/Web/HTML/Element/header"> 标题</a></td>
   <td>它包括介绍性内容，通常是一组介绍性或导航辅助工具。 它在表单容器之外受支持。 </td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/footer.html">页脚</td>
   <td><a href = "https://developer.mozilla.org/en-US/docs/Web/HTML/Element/footer">页脚</a></td>
   <td> 包含信息，例如版权数据或相关文档的链接。 它在表单容器之外受支持。</td>
  </tr>
  <tr>
   <td><a href = "https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion.html">可折叠项<a></td>
   <td><i>表单块中尚不受支持</i></td>
   <td> 允许用户在表单中创建可展开和可折叠的部分。 </td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/horizontal-tabs.html">水平选项卡</a></td>
   <td><i>表单块中尚不受支持</i></td>
   <td>将表单的多个部分组织为单独的选项卡，这些选项卡水平显示。</td>
  </tr>
  <tr>
   <td><a href = "https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/image.html">图像</a></td>
   <td><i>表单块中尚不受支持</i></td>
   <td> 允许用户在表单中包含图像。</td>
  </tr><tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/title.html">标题</a></td>
   <td><i>表单块中尚不受支持</i></td>
   <td> 指显示在表单顶部的文本。 </td>
  </tr>
  <tr>
   <td><a href = "https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/submit-button.html">开关</td>
   <td><i>表单块中尚不受支持</i></td>
   <td> 一种双状态切换，允许用户在两个状态之间进行选择，例如启用或禁用功能、设置或功能。</td>
  </tr>
 </tbody>
</table>


