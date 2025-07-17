---
title: HTML5 Forms与PDF forms的功能差异
description: 了解HTML5 Forms和PDF forms之间的功能差异。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
docset: aem65
feature: HTML5 Forms,Mobile Forms
exl-id: 3150f95f-7150-4eee-b5a9-121422dec2a1
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 22aeedaaf4171ad295199a989e659b6bf5ce9834
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 2%

---

# HTML5 Forms与PDF forms的功能差异 {#feature-differentiation-between-html-forms-and-pdf-forms}

<span class="preview"> HTML5 Forms功能作为提前访问计划的一部分提供。 要请求访问，请将您的官方（工作）电子邮件ID通过电子邮件发送到aem-forms-ea@adobe.com。
</span>

下表指定了为HTML5 Forms和PDF forms提供的功能支持：

<table>
 <tbody>
  <tr>
   <th>功能</th>
   <th>HTML5 表单</th>
   <th>PDF</th>
  </tr>
  <tr>
   <td>条形码<br /> </td>
   <td>在用户界面级别不可用。 </td>
   <td>支持</td>
  </tr>
  <tr>
   <td>签名字段<br /> </td>
   <td>不支持<strong>数字签名</strong>，但是为类似纸张的签名添加了新的<strong>涂写签名</strong>字段。 可以使用<strong>涂写签名</strong>字段在表单上涂写签名。 签名将作为图像保存在表单上。 您可以在<strong>涂写签名</strong>字段中保存地理位置信息。</td>
   <td>可用于<strong>数字签名</strong>的签名字段。</td>
  </tr>
  <tr>
   <td>数据合并</td>
   <td>支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>图像</td>
   <td>数据URI方案用于显示图像。 所有新版本的浏览器都支持此方案，但每个浏览器支持的图像格式范围存在差异。<br /> </td>
   <td>支持.gif、.png、.jpeg、.bmp和.tiff格式。</td>
  </tr>
  <tr>
   <td>分页<br /> </td>
   <td><p>HTML5窗体分为多个面板和框，以便其外观类似于PDF forms。 页面大小会动态计算。 如果HTML5表单中页面的所有内容被删除或标记为隐藏，则空白页面将被隐藏。 空白页的上方和下方的页面之间不显示空格（空格）。</p> <p>如果数据合并或脚本向页面添加内容，则页面长度将展开以容纳新添加的内容。 表单中不会添加任何新页面，以适应新添加的内容。 </p> <p><strong>注意：</strong>当HTML5表单中某个页面的所有内容被删除或标记为隐藏时，空白页面（空格）在第一页和第二页之间保持可见，但在任何其他页面之间保持可见。</p> </td>
   <td>PDF中的分页取决于合并的数据内容或用户内容，并且页面计数会因此而增加/减少。</td>
  </tr>
  <tr>
   <td>页眉/页脚 </td>
   <td>支持。 <br /> <br />由于HTML5移动表单不支持分页符，因此页眉和页脚只显示一次。 但是，您可以将它们设置为在移动设备表单预览中的多个位置显示。<br /> </td>
   <td>支持。</td>
  </tr>
  <tr>
   <td>自定义构件</td>
   <td>可以自定义小组件以增强移动设备上的用户体验。<br /> </td>
   <td>已锁定所有小组件，无法插入自定义小组件。<br /> </td>
  </tr>
  <tr>
   <td>XFA脚本API</td>
   <td>支持最常用的XFA脚本结构。 有关支持的构造的详细列表，请参阅<a href="/help/forms/scripting-support.md">脚本支持</a>。</td>
   <td>支持所有XFA脚本结构。</td>
  </tr>
  <tr>
   <td>Acrobat脚本API </td>
   <td>HTML5 forms支持最常用的API。 有关详细信息，请参阅<a href="/help/forms/scripting-support.md">脚本支持</a>。</td>
   <td>如果在Acrobat或Reader中打开PDF文件，则它还支持Acrobat提供的所有脚本API。</td>
  </tr>
  <tr>
   <td>支持从右至左的语言 </td>
   <td>支持</td>
   <td>支持</td>
  </tr>
 </tbody>
</table>

<!--Follow the best practices to enable a form template for HTML5 renditions and ensure that the behavior and appearance of HTML5 forms and XFA-based PDF is consistent. For detailed list of best practices, see [Best practices to design an HTML5 form.](/help/forms/using/best-practices-design-html5-forms.md)-->
