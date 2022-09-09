---
title: 自适应Forms创作简介
seo-title: Introduction to authoring Adaptive Forms
description: AEM Forms为创作自适应Forms提供了易于使用且功能强大的界面。 它提供了许多可用于构建表单的组件和工具。
seo-description: AEM Forms provide easy-to-use yet powerful interface for authoring Adaptive Forms. It provides a host of components and tools that you can use to build forms.
uuid: 3b150507-41b9-47c2-a94c-f85b903b2274
content-type: reference
topic-tags: author, introduction
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: ba70921e-db7e-43f6-902c-1065d3b13aef
docset: aem65
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '2317'
ht-degree: 4%

---


# 自适应Forms编辑器 {#introduction-to-authoring-adaptive-forms}

## 概述 {#overview}

自适应Forms让您能够创建有吸引力的响应式、动态且自适应的表单。 [!DNL AEM Forms] 提供了直观的用户界面和现成的组件，用于创建和使用自适应Forms。 您可以选择基于表单模型或架构创建自适应表单，也可以不使用表单模型创建自适应表单。 必须仔细选择不仅适合您的要求，而且扩展您现有的基础设施投资和资产的表单模式。 您可以从以下选项中进行选择，以创建自适应表单：

<!-- * **Using a form data model**
  [Data integration](data-integration.md) lets you integrate entities and services from disparate data sources in to a Form Data Model that you can use to create Adaptive Forms. Choose Form Data Model if the Adaptive Form you are creating involves fetching and write data from and to multiple data source. -->

* **使用XDP表单模板**
如果您在基于XFA或XDP的表单中进行了投资，则这是理想的表单模型。 它提供了一种将基于XFA的表单转换为自适应Forms的直接方法。 任何现有的XFA规则都将保留在关联的自适应Forms中。 生成的自适应Forms支持XFA构建，如验证、事件、属性和模式。

* **使用XML架构定义(XSD)或JSON架构**
XML和JSON架构表示组织内的后端系统生成或使用数据的结构。 您可以将架构与自适应表单相关联，并使用其元素向自适应表单添加动态内容。 创作自适应Forms时，架构的元素将可用在内容浏览器的“数据模型对象”选项卡中。

* **不使用表单模型或不使用表单模型**
使用此选项创建的自适应Forms不使用任何表单模型。 从这种表单生成的数据XML具有平坦结构，其中具有字段和相应的值。

<!--  For more information about creating an Adaptive Form, see [Creating an Adaptive Form](creating-adaptive-form.md). -->

## 自适应表单创作UI {#adaptive-form-authoring-ui}

用于创作自适应Forms的触屏优化UI非常直观，它提供：

* 拖放功能
* 标准表单组件
* 集成的资产存储库

创建新自适应表单或编辑现有自适应表单时，可使用以下UI元素：

* [侧栏](#sidebar)
* [页面工具栏](#page-toolbar)
* [组件工具栏](#component-toolbar)
* [自适应表单页面](#af-page)

<!-- ![Adaptive Form authoring UI](assets/formeditor.png)

**A.** Sidebar **B.** Page toolbar **C.** Adaptive Form page -->

### 侧栏 {#sidebar}

侧栏允许您

* 搜索、查看和使用AEM数字资产管理(DAM)存储库中的资产。
* 请参阅表单内容，如面板、组件、字段和布局。
* 在表单上添加组件。
* 编辑组件属性。

![侧栏](assets/sidebar-comps.png)

**A.** 内容浏览器 **B.** 属性浏览器 **C.** 资产浏览器 **D.** 组件浏览器

<!--Click to enlarge

](assets/sidebar-comps-1.png) -->

侧栏包含以下浏览器：

* **内容浏览器**
在内容浏览器中，您可以看到：

   * **表单对象**
显示表单的对象层次结构。 作者可以通过在表单对象树中点按特定表单组件来导航到该组件。 作者可以在此树中搜索并重新排列对象。

   * **数据模型对象**
用于查看表单模型层次结构。
它允许您在自适应表单上拖放表单模型元素。 添加的元素会自动转换为表单组件，同时保留其原始属性。 当您的表单使用XML架构、JSON架构或XDP模板时，您可以看到数据模型对象。

* **属性浏览器**

   允许您编辑组件的属性。 属性会根据组件而发生更改。 要查看自适应表单容器的属性，请执行以下操作：

   选择一个组件，然后点按 ![字段级别](assets/Smock_SelectContainer_18_N.svg) > **[!UICONTROL 自适应表单容器]**，然后点按 ![属性](assets/Smock_Wrench_18_N.svg).

* **资产浏览器**

   分隔不同类型的内容，如图像、文档、页面、电影等。

* **组件浏览器**

   包括可用于构建自适应表单的组件。 您可以将组件从拖动到自适应表单上以添加表单元素，并根据要求配置添加的元素。 下表介绍了组件浏览器中列出的组件。

<table>
 <tbody>
  <tr>
   <th><strong>组件</strong></th>
   <th><strong>功能</strong></th>
  </tr>
  <tr>
   <td>Adobe Sign Block</td>
   <td>为使用Adobe Sign进行签名时要填充的字段添加带占位符的文本块。</td>
  </tr>
  <tr>
   <td>按钮</td>
   <td>添加按钮，您可以将其配置为执行各种操作，例如保存、重置、转到下一步、转到上一步等。</td>
  </tr>
  <tr>
   <td>Captcha</td>
   <td>添加了使用Google reCAPTCHA服务的CAPTCHA验证。</td>
  </tr>
  <tr>
   <td>图表</td>
   <td>添加一个图表，可在自适应Forms和文档中使用该图表以在可重复面板和表行中直观地表示二维数据。</td>
  </tr>
  <tr>
   <td>复选框</td>
   <td>添加复选框。</td>
  </tr>
  <tr>
   <td>数据输入字段</td>
   <td>在您的表单中使用日期输入字段组件，让客户在三个框中分别填写日、月和年。 您可以自定义组件的外观，并更改日期格式。 例如，您可以让客户以YYYY/MM/DD或DD/MM/YYYY格式输入日期。</td>
  </tr>
  <tr>
   <td>日期选取器</td>
   <td>添加日历字段以选取日期。</td>
  </tr>
  <tr>
   <td>文档片段</td>
   <td>允许您添加通信的可重用组件。</td>
  </tr>
  <tr>
   <td>文档片段组</td>
   <td>允许您添加可在信件模板中用作单个单元的相关文档片段组。</td>
  </tr>
  <tr>
   <td>下拉列表</td>
   <td>添加下拉列表 — 单选或多选</td>
  </tr>
  <tr>
   <td>电子邮件</td>
   <td><p>添加用于捕获电子邮件地址的字段。 默认情况下，电子邮件组件会使用以下正则表达式来验证电子邮件地址。</p> <p><code>^[a-zA-Z0-9.!#$%&amp;’*+/=?^_`{|}~-]+@[a-zA-Z0-9-]+(?:.[a-zA-Z0-9-]+)*$</code></p> </td>
  </tr>
  <tr>
   <td>文件附件</td>
   <td><p>添加按钮，允许用户浏览支持文档并将其附加到表单。</p> <p><strong>注意： </strong>文件附件组件支持在为Adobe Sign启用的自适应Forms中预定义的一组文件格式。 有关更多信息，请参阅 <a href="https://helpx.adobe.com/document-cloud/help/supported-file-formats-fill-sign.html#main-pars_text">支持的文件格式</a>.</p> </td>
  </tr>
  <tr>
   <td>文件附件列表</td>
   <td>添加一个字段，其中列出了使用“文件附件”组件上传的所有附件。</td>
  </tr>
  <tr>
   <td>页脚<br /> </td>
   <td>添加页眉，该页眉通常包括公司徽标、表单标题和摘要。<br /> </td>
  </tr>
  <tr>
   <td>标题</td>
   <td>添加页脚，该页脚通常包含版权信息以及指向其他页面的链接。 </td>
  </tr>
  <tr>
   <td>图像</td>
   <td>允许插入图像。</td>
  </tr>
  <tr>
   <td>图像选择</td>
   <td>允许您的客户选择要提供信息的图像。 您可以使用该信息为客户提供个性化服务。</td>
  </tr>
  <tr>
   <td>“下一个”按钮</td>
   <td>添加按钮以导航到表单中的下一个面板。</td>
  </tr>
  <tr>
   <td>数值框</td>
   <td>添加用于捕获数值的字段</td>
  </tr>
  <tr>
   <td>数值步进器</td>
   <td>在表单中使用数字步进器，让客户输入一个数字值，他们可以根据预定义的步骤增加或减少该值。</td>
  </tr>
  <tr>
   <td>面板</td>
   <td><p>添加面板或子面板。</p> <p>您还可以使用 <span class="uicontrol">添加子面板</code> 按钮。 同样，您也可以使用 <span class="uicontrol">添加面板工具栏</code> 按钮。 您可以使用编辑面板对话框配置面板工具栏的位置。</code></code></p> </td>
  </tr>
  <tr>
   <td>密码框</td>
   <td>添加用于捕获密码的字段。</td>
  </tr>
  <tr>
   <td>“上一个”按钮</td>
   <td>添加用户需要返回上一页或面板的按钮。</td>
  </tr>
  <tr>
   <td>单选按钮</td>
   <td>添加单选按钮。</td>
  </tr>
  <tr>
   <td>“重置”按钮</td>
   <td>添加按钮以重置表单字段。</td>
  </tr>
  <tr>
   <td>保存按钮</td>
   <td>添加按钮以保存表单数据。</td>
  </tr>
  <tr>
   <td>连笔签名</td>
   <td>添加用于捕获潦草签名的字段。</td>
  </tr>
  <tr>
   <td>分隔符</td>
   <td>以您的形式启用面板的可视隔离。</td>
  </tr>
  <tr>
   <td>签名步骤</td>
   <td>显示表单中提供的信息以及用户验证和签署表单的签名字段。</td>
  </tr>
  <tr>
   <td>文本</td>
   <td>用于指定静态文本。</td>
  </tr>
  <tr>
   <td>提交按钮</td>
   <td>添加提交按钮以将表单提交到配置的提交操作。</td>
  </tr>
  <tr>
   <td>摘要步骤</td>
   <td>提交表单并显示作者在提交表单后指定的摘要文本。 </td>
  </tr>
  <tr>
   <td>切换</td>
   <td>添加执行切换或启用/禁用操作的开关。 不能在交换机组件中添加两个以上的选项。 由于交换机只能有两个值：“开”或“关”，“强制”不适用。 保存至少一个值，而不考虑用户输入。 <br /> </td>
  </tr>
  <tr>
   <td>表</td>
   <td>添加表格以便按行和列整理数据。 </td>
  </tr>
  <tr>
   <td>电话</td>
   <td><p>添加用于捕获电话号码的字段。 电话组件允许作者配置以下电话号码类型之一。 每种类型都与验证的默认正则表达式相关联。</p>
    <ul>
     <li>Type International由 <code>^[+][0-9]{0,14}$</code>.</li>
     <li>类型USPhoneNumber由 <code>{'+1 ('999') '999-9999}</code>.</li>
     <li>类型UKPhoneNumber将由验证 <code>text{'+'99 999 999 9999}</code>.</li>
     <li>类型自定义不提供默认验证模式。 它采用最后选定电话号码类型的值。 您还可以指定自己的自定义验证模式。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>条款和条件<br /> </td>
   <td>添加作者可用于指定用户在填写表单之前查看的条款和条件的字段。</td>
  </tr>
  <tr>
   <td>文本框 </td>
   <td><p>添加一个文本框，用户可在其中指定所需信息。 </p> <p>默认情况下，文本框组件仅接受纯文本。 您可以启用文本框组件以接受富文本。 启用富文本的文本组件提供了以下选项：添加标题、更改字符样式（粗体、斜体、为字符加下划线）、创建有序和无序列表、更改文本背景和文本颜色以及添加超链接。 要为文本框启用富文本，请启用<strong> 允许富文本</strong> 选项。</p> </td>
  </tr>
  <tr>
   <td>标题</td>
   <td>指定自适应表单的标题。</td>
  </tr>
  <tr>
   <td>验证步骤</td>
   <td><p>添加占位符以显示已填充的表单，以供用户验证。</p> <p><strong>注意</strong>:包含验证组件的自适应表单不支持匿名用户。 此外，不建议在自适应表单片段中使用验证组件。</p> </td>
  </tr>
 </tbody>
</table>

### 页面工具栏 {#page-toolbar}

顶部的页面工具栏提供了用于预览表单、更改表单属性和编辑表单布局的选项。 您可以在创作表单时进行预览，并相应地进行更改。 在页面工具栏中，您会看到：

* **切换侧面板** ![切换侧面板](assets/Smock_RailLeft_18_N.svg):允许您显示或隐藏侧栏。

* **页面信息** ![主题选项](assets/Smock_Properties_18_N.svg):允许您查看页面属性、发布/取消发布表单、启动表单工作流，以及在经典UI中打开表单。

* **模拟器** ![标尺](assets/Smock_Devices_18_N.svg):允许您针对平板电脑和手机等不同显示大小模拟表单的外观。

* **编辑**:允许您选择其他模式，例如： **[!UICONTROL 编辑]**, **[!UICONTROL 样式]**, **[!UICONTROL 开发人员]**&#x200B;和 **[!UICONTROL 设计]**.

   * **编辑**:允许您编辑表单及其组件的属性。 例如，添加组件、删除图像并指定必填字段。
   * **样式**:允许您设置表单组件外观的样式。 例如，在样式模式下，您可以选择面板并指定其背景颜色。

   * **开发人员**:允许开发人员：

      * 了解表单由哪些组成。
      * 调试在何处和何时发生的事件，这反过来有助于解决问题。

      * **Design**. 允许您启用或禁用自定义组件，或未在侧栏中列出的现成组件。

* **预览**:用于预览发布表单时的外观。

### 组件工具栏 {#component-toolbar}

![触屏UI中的组件工具栏](assets/component-toolbar.png)

选择组件时，您会看到一个允许您处理该组件的工具栏。 您可以选择剪切、粘贴、移动和指定组件的属性。 您的选项包括：

A.**配置**:点按 **[!UICONTROL 配置]**，则组件属性会显示在侧栏中。 通过配置这些属性，您可以自定义数据捕获体验。 您可以更改组件的元素名称，在组件的标题字段中指定标签文本。 元素名称允许您使用组件捕获用户输入的值。 在组件属性中，您可以指定组件的行为并管理用户输入。 在侧栏中配置属性以捕获用户数据并将其用于进一步处理。 自适应表单容器的属性允许您指定客户端库、布局、主题、记录文档设置、保存设置、提交设置和元数据设置。

B.**复制**:您可以使用复制选项复制组件并将其粘贴到表单中的其他位置。 粘贴组件时，粘贴的组件会获得新的元素名称，但会保留复制的组件的属性。

C.**剪切**:您可以使用剪切选项在自适应表单中将组件从一个位置移动到另一个位置。

D. **删除**:允许您从表单中删除组件。

E. **插入**:允许您在选定组件上方插入组件。

F. **粘贴**:允许您使用上述选项粘贴您剪切或复制的组件。

G. **编辑规则**:用于打开规则编辑器。 有关更多信息, <!-- see [Rule Editor](rule-editor.md). -->

H. **组**:如果要剪切、复制或粘贴多个组件，可让您选择多个组件。

我。 **父项**:允许您选择组件的父组件。 例如，文本字段位于位于某个部分中的子部分中。 部分位于指南根面板中，而自适应表单容器是指南根面板的父级。 对于组件，您可以看到所有选项，这些选项的层次结构从下而上排序。

例如，如果您点按 **[!UICONTROL 父项]** 对于文本框，您可以看到：

* 子部分
* 区域
* guideRootPanel
* 自适应表单容器

J. **其他**:提供更多用于处理选定组件的选项。

* 查看SOM表达式
* 将面板另存为片段（仅适用于面板）
* 添加子面板（仅适用于面板）
* 添加面板工具栏（仅适用于面板）
* 替换（不适用于面板）

### 自适应表单页面 {#af-page}

“自适应表单”页面是实际的表单。 与建模为WCM的任何其他WCM页面类似 `cq:Page` 组件。 下图显示了典型自适应表单的内容结构。

![自适应表单WCM页面的内容结构](assets/afstructure.png)

内容结构通常包含以下主要组件：

* **guideContainer**:自适应表单的根，标记为 **[!UICONTROL 自适应表单的开始]** 在自适应表单UI中。 在此组件中，您可以指定：

   * *自适应表单的移动布局*:定义表单在移动设备上的外观。
   * *感谢页面*:定义提交表单后用户被重定向的页面。
   * *提交操作*:定义用户提交表单后如何在服务器上处理表单。
   * *样式*:指定用于自定义表单外观的CSS文件的路径。

* **rootPanel:** 自适应表单的根面板。 它可以在项目节点下包含子面板。 包括根面板的每个面板都可以具有与其关联的布局。 面板的布局指示表单的布局方式。 例如，在折叠式布局中，其项目布局为折叠式步骤。

* **工具栏：** 自适应表单容器具有与表单全局关联的全局工具栏。 此工具栏可使用 **[!UICONTROL 添加工具栏]** 操作，该操作允许作者添加操作，例如提交、保存、重置等。

* **资产：** 此节点包含用于表单创作的其他信息。 例如，表单模型详细信息、本地化详细信息等。
