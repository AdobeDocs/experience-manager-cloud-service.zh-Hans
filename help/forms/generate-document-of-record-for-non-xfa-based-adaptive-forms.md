---
title: 为自适应Forms生成记录文档
description: 说明如何为自适应Forms的记录文档(DoR)生成模板。
exl-id: 15540644-c0c3-45ce-97d3-3bdaa16fb4b6
source-git-commit: 21db238b0808d6131c2a22de3d47ba7f7bd2f48b
workflow-type: tm+mt
source-wordcount: '3659'
ht-degree: 2%

---

# 为自适应Forms生成记录文档

## 概述 {#overview}

填写或提交表单后，您可以以打印或文档格式保留表单的记录。 此记录称为记录文档(DoR)。 它是已提交表单的打印友好副本。 您还可以参考客户在稍后日期填写的信息的记录文档，或使用记录文档以PDF格式将表单和内容一起存档。

![记录文档](assets/document-of-record.png)

要创建记录文档，将基于XFA或Acroform的模板与通过自适应表单收集的数据合并。 您可以自动或按需生成记录文档。
利用按需选项，可指定基于自定义XFA或Acroform的模板，以为记录文档提供自定义外观。

您可以：

* [生成基于XFA的记录文档](#generate-an-XFA-based-document-of-record)
* [生成基于Acroform(Acrobat表单PDF)的记录文档](#generate-an-Acroform-based-document-of-record)
* [自动生成记录文档](#auto-generate-a-document-of-record)

## 开始之前 {#components-to-automatically-generate-a-document-of-record}

在您开始学习并准备记录文档所需的资产之前：

**基本模板：** 在Forms Designer或Acrobat表单(AcroForm)中创建的XFA模板（XDP文件）。 [基本模板](#base-template-of-a-document-of-record) 用于为记录文档指定样式和品牌信息。 在之前，将XFA模板（XDP文件）上传到AEM Forms实例

**自适应表单：** 要为其生成记录文档的自适应表单。

## 生成基于XFA的记录文档 {#generate-an-XFA-based-document-of-record}

将XFA模板（XDP文件）上传到AEM Forms实例。 请执行以下步骤来配置自适应表单，以使用XFA模板（XDP文件）作为记录文档的模板：

1. 在Experience Manager创作实例中，单击 **[!UICONTROL Forms]** > **[!UICONTROL Forms和文档].**
1. 选择表单，然后单击 **[!UICONTROL 属性]**.
1. 在属性窗口中，点按 **[!UICONTROL 表单模型]**.
1. 在  **[!UICONTROL 表单模型]** 选项卡 **[!UICONTROL 选择自]** 下拉列表，选择 **[!UICONTROL 架构]** 或 **[!UICONTROL 无]**. 在创建表单时，您还可以选择表单模型。
1. 在“表单模型”选项卡的“记录模板配置文档”部分中，选择 **将表单模板关联为记录模板文档**. 选择此选项时，将显示您计算机上可用的所有XFA模板（XDP文件）。 选择相应的文件。 此外，还要确保对自适应表单和选定的XFA模板（XDP文件）使用相同的架构（数据架构）。
1. 单击 **[!UICONTROL 完成。]**

自适应表单现已配置为使用XDP文件作为记录文档的模板。 下一步是 [使用相应的模板字段绑定自适应表单组件](#bind-adaptive-form-components-with-template-fields).

## 生成基于Acroform的记录文档 {#generate-an-Acroform-based-document-of-record}

将Adobe AcrobatPDF(Acroform)上传到AEM Forms实例。 请执行以下步骤来配置自适应表单，以使用Adobe AcrobatPDF(Acroform)作为记录文档的模板：

1. 在Experience Manager创作实例中，单击 **[!UICONTROL Forms]** > **[!UICONTROL Forms和文档].**
1. 选择表单，然后单击 **[!UICONTROL 属性]**.
1. 在属性窗口中，点按 **[!UICONTROL 表单模型]**.
1. 在  **[!UICONTROL 表单模型]** 选项卡 **[!UICONTROL 选择自]** 下拉列表，选择 **[!UICONTROL 架构]** 或 **[!UICONTROL 无]**. 在创建表单时，您还可以选择表单模型。
1. 在“表单模型”选项卡的“记录模板配置文档”部分中，选择 **将表单模板关联为记录模板文档**. 选择此选项时，将显示您计算机上可用的所有AcrobatPDF(Acroform)。 选择相应的文件。
1. 单击 **[!UICONTROL 完成。]**

您的自适应表单现已配置为使用Acroform作为记录文档的模板。 下一步是 [使用相应的模板字段绑定自适应表单组件](#bind-adaptive-form-components-with-template-fields).

## 自动生成记录文档 {#auto-generate-a-document-of-record}

当自适应表单配置为自动生成记录文档时，每次更改表单时，其记录文档都会立即更新。 例如，如果从现有自适应表单中删除了字段，则相应的字段也会被删除，并且在记录文档中不可见。 自动生成记录文档还有许多其他优势。 : 

* 表单开发人员不必手动维护数据绑定。 自动生成的记录文档负责数据绑定相关更新。
* 表单开发人员不必手动隐藏标记为从记录文档中排除的字段。 自动生成的记录文档已预配置为排除此类字段。
* 自动生成的记录文档选项可节省为记录文档创建表单模板所需的时间。
* 自动生成的“记录文档”选项允许您使用不同的基本模板来使用不同的样式和外观。 它有助于为您的组织选择记录文档的最佳样式和外观。 如果未指定样式，则系统样式将设置为默认样式。
* 自动生成的记录文档可确保表单的任何更改立即反映在记录文档中。

执行以下步骤来配置自适应表单以自动生成记录文档：

1. 在Experience Manager创作实例中，单击 **[!UICONTROL Forms]** > **[!UICONTROL Forms和文档].**
1. 选择表单，然后单击 **[!UICONTROL 属性]**.
1. 在属性窗口中，点按 **[!UICONTROL 表单模型]**.
1. 在  **[!UICONTROL 表单模型]** 选项卡 **[!UICONTROL 选择自]** 下拉列表，选择 **[!UICONTROL 架构]** 或 **[!UICONTROL 无]**. 在创建表单时，您还可以选择表单模型。
1. 在“表单模型”选项卡的“记录模板配置文档”部分中，选择 **生成记录文档**.
1. 单击 **[!UICONTROL 完成。]**

## 使用模板字段绑定自适应表单组件 {#bind-adaptive-form-components-with-template-fields}

将自适应表单字段与模板字段绑定，以在相应的记录字段文档中显示捕获的表单数据。 要将自适应表单组件与记录模板字段的相应文档绑定，请执行以下操作：

1. 打开自适应表单，该表单配置为使用自定义表单模板进行编辑。

1. 选择自适应表单组件并单击打开配置 ![配置](assets/Smock_Wrench_18_N.svg) 图标。 它会打开属性浏览器。

1. 在属性浏览器中，浏览并选择一个字段。

   * （对于AcroForm模板） **[!UICONTROL 记录绑定引用字段的文档]** 属性。
   * （对于XFA模板） **[!UICONTROL 数据模型绑定参考]** 属性。

1. 单击“**[!UICONTROL 保存]**”。

<!-- 
In the following video Adaptive Form components are binded with corresponding Acroform template fields and the Document of Record is sent as an email attachment.
-->

您可以将“发送电子邮件”、“Experience Manager工作流”提交操作与 [记录文档步骤和其他提交操作](configuring-submit-actions.md) 接收记录文档。

## 记录文档模板的增量更新 {#document-of-record-template-incremental-updates}

自适应表单和相应的记录模板文档会随着时间的推移而变化。 您可以选择向自适应表单或记录文档模板添加、删除或修改字段。

当您更改记录文档模板并将更改的记录文档模板上传到AEM Forms时，自适应Forms编辑器会自动检测更改的绑定并通知您需要新绑定的自适应表单组件。 它允许您对记录文档模板进行增量更新。

例如，组织， *We.Retail*，具有基于AcroForm的记录文档模板， *we-retail-invoice.pdf*. 模板如下所示：

![原始模板](assets/we-retail-invoice.png)

在使用模板一段时间后，组织会决定重命名 `invoice-number` 字段 `bill-number` 字段和捕获购买者的电子邮件地址。 开发人员更新 `invoice-number` 字段，并向模板中添加电子邮件字段。 他还创建了一个新版本的模板，名为  *we-retail-invoice-v2.pdf*.

![更新的模板](assets/we-retail-new-invoice.png)

开发人员将更新的模板上传并应用到自适应表单。 自适应表单会自动检测并显示绑定已更改的字段列表。

![绑定错误](assets/we-retail-binding-error.png)

表单开发人员将自适应Forms字段与相应的记录文档模板绑定。
>[!VIDEO](assets/we-retail-binding.mp4)

现在，在提交自适应表单时，将创建更新的记录文档。

![更新了-](assets/we-retail-new-invoice-sent-to-customer.png)

## 使用记录文档时的主要注意事项 {#key-considerations-when-working-with-document-of-record}

处理自适应Forms的记录文档时，请记住以下注意事项和限制。

* 记录模板文档不支持富文本。 因此，静态自适应表单或最终用户填写的信息中的任何富文本都会在记录文档中显示为纯文本。
* 自适应表单中的文档片段不显示在记录文档中。 但是，支持自适应表单片段。
* 不支持为基于XML架构的自适应表单生成的记录文档中的内容绑定。
* 当用户请求渲染记录文档时，将根据区域设置的要求创建记录文档的本地化版本。 记录文档的本地化与自适应表单的本地化同步进行。 <!-- For more information on localization of Document of Record and Adaptive Forms see Using AEM translation workflow to localize Adaptive Forms and Document of Record.-->

<!-- ## Configure an adaptive form to generate  Document of Record {#adaptive-form-types-and-their-documents-of-record}

While creating an adaptive form, in the Form Model tab of Adaptive Form properties, select one the following option: 

* **None**
  Select the option to create an Adaptive Form without a form model. When the option is selected, the Document of Record is automatically generated for your Adaptive Form.

* **[Associate form template as a Document of Record template](creating-adaptive-form.md#create-an-adaptive-form-based-on-an-xfa-form-template)**
  
  Select the option to use an XFA Form as a template for Document of Record. 

* **[Generate Document of Record](creating-adaptive-form.md#create-an-adaptive-form-based-on-xml-or-json-schema)**
  Select the option to use an XFA Form as a template. When the option is selected, the Document of Record is automatically generated for your Adaptive Form. When you use an XML schema as a template for an Adaptive Form, ensure that the adaptive form and associated XFA Form use the same XML schema as your Adaptive Form
  

When you select a form model, configure Document of Record using options available under Document of Record Template Configuration. See [Document of Record Template Configuration](#document-of-record-template-configuration). -->

## 自适应表单元素的映射 {#mapping-of-adaptive-form-elements}

下表描述了自适应表单组件和相应的XFA组件，以及这些组件是否显示在记录文档中。

### 字段 {#fields}

<table>
 <tbody>
  <tr>
   <th>自适应表单组件</th>
   <th>相应的XFA组件</th>
   <th>默认情况下，是否包含在记录模板文档中？</th>
   <th>注释</th>
  </tr>
  <tr>
   <td>按钮</td>
   <td>按钮</td>
   <td>false</td>
   <td> </td>
  </tr>
  <tr>
   <td>复选框</td>
   <td>复选框</td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>日期选取器</td>
   <td>日期/时间字段</td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>下拉列表</td>
   <td>下拉列表</td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>潦草签名</td>
   <td>签名涂写</td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>数值框</td>
   <td>数值字段</td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>密码框</td>
   <td>密码字段</td>
   <td>false</td>
   <td> </td>
  </tr>
  <tr>
   <td>单选按钮</td>
   <td>单选按钮</td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>文本框</td>
   <td>文本字段</td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>“重置”按钮</td>
   <td>重置按钮</td>
   <td>false</td>
   <td> </td>
  </tr>
  <tr>
   <td>提交按钮</td>
   <td><p>“电子邮件提交”按钮</p> <p>HTTP提交按钮</p> </td>
   <td>false</td>
   <td> </td>
  </tr>
  <tr>
   <td>条款和条件</td>
   <td> </td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>文件附件</td>
   <td> </td>
   <td>false</td>
   <td>在记录文档模板中不可用。 仅在记录文档中通过附件可用。</td>
  </tr>
 </tbody>
</table>

### 容器 {#containers}

<table>
 <tbody>
  <tr>
   <th>自适应表单组件</th>
   <th>相应的XFA组件</th>
   <th>注释</th>
  </tr>
  <tr>
   <td>面板<br /> </td>
   <td>子表单<br /> </td>
   <td>可重复面板映射到可重复的子表单。</td>
  </tr>
 </tbody>
</table>

### 静态组件 {#static-components}

| 自适应表单组件 | 相应的XFA组件 | 注释 |
|---|---|---|
| 图像 | 图像 | 无论绑定还是未绑定的TextDraw和图像组件，都会始终显示在基于XSD的自适应表单的记录文档中，除非使用记录文档设置排除。 |
| 文本 | 文本 |

### 表 {#tables}

自适应Forms表组件（如页眉、页脚和行映射）映射到相应的XFA组件。 您可以将可重复面板映射到记录文档中的表。

## 记录文档的基本模板 {#base-template-of-a-document-of-record}

基本模板为记录文档提供样式和外观信息。 它允许您自定义自动生成的记录文档的默认外观。 例如，您可以使用基本模板在记录文档页脚的页眉和版权信息中添加公司徽标。

基本模板中的主控页用作记录文档模板的主控页。 主控页面可以包含可应用于记录文档的页眉、页脚和页码等信息。 您可以使用基本模板将此类信息应用到记录文档，以自动生成记录文档。 使用基本模板可更改字段的默认属性。

始终关注 [基本模板约定](#base-template-conventions) 设计基本模板时。

## 基本模板约定 {#base-template-conventions}

基本模板用于定义记录文档的页眉、页脚、样式和外观。 页眉和页脚可以包含公司徽标和版权文本等信息。 基本模板中的第一个主控页面将被复制并用作记录文档的主控页面，其中包含页眉、页脚、页码，或应显示在记录文档所有页面中的任何其他信息。 如果您使用的基本模板不符合基本模板惯例，则基本模板中的第一个主控页面仍会在记录文档模板中使用。 强烈建议您按照其惯例设计基本模板，并将其用于自动生成记录文档。

**主控页面惯例**

* 在基本模板中，将根子表单命名为 `AF_METATEMPLATE` 主控页面为 `AF_MASTERPAGE`.

* 具有名称的主控页面 `AF_MASTERPAGE` 位于 `AF_METATEMPLATE` 首选根子表单提取页眉、页脚和样式信息。

* 如果 `AF_MASTERPAGE` 不存在，则使用基础模板中存在的第一个主控页面。

**字段的样式约定**

* 要对“记录文档”中的字段应用样式，基本模板会提供位于 `AF_FIELDSSUBFORM` 从 `AF_METATEMPLATE` 根子表单。

* 这些字段的属性将应用于记录文档中的字段。 这些字段应跟在 `AF_<name of field in all caps>_XFO` 命名约定。 例如，复选框的字段名称应为 `AF_CHECKBOX_XFO`.

要创建基本模板，请在Forms Designer中执行以下操作。

1. 单击 **[!UICONTROL 文件]** > **[!UICONTROL 新建]**.
1. 选择 **[!UICONTROL 基于模板]** 选项。

1. 选择 **[!UICONTROL Forms — 记录文档]** 类别。
1. 选择 **[!UICONTROL DoR基模板]**.
1. 单击 **[!UICONTROL 下一个]** 并提供所需信息。

1. （可选）修改要应用于记录文档中字段的字段的样式和外观。
1. 保存表单。

现在，您可以将保存的表单用作记录文档的基本模板。 请勿修改或删除基本模板中存在的任何脚本。

**修改基本模板**

* 如果不对基本模板中的字段应用任何样式，则建议从基本模板中删除这些字段，以便自动选取对基本模板的任何升级。
* 修改基本模板时，请勿删除、添加或修改脚本。

严格按照上述惯例和说明设计基础模板。

## 自定义记录文档中的品牌信息 {#customize-the-branding-information-in-document-of-record}

在生成记录文档时，您可以在“记录文档”选项卡上更改记录文档的品牌信息。 “记录文档”选项卡包含徽标、外观、布局、页眉和页脚、免责声明，以及是否要包含未选中的复选框和单选按钮选项等选项。

要将您在“记录文档”选项卡中输入的品牌信息本地化，请确保已正确设置浏览器的区域设置。 要自定义记录文档的品牌信息，请执行以下步骤：

1. 在记录文档中选择一个面板（根面板），然后点按 ![配置](assets/configure.png).
1. 点按 ![多选项卡](assets/dortab.png). 将出现“记录文档”选项卡。
1. 选择默认模板或用于渲染记录文档的自定义模板。 如果选择默认模板，“记录文档”的缩略图预览将显示在“模板”下拉列表的下方。

   ![品牌模板](assets/brandingtemplate.png)

   如果选择自定义模板，请在 [!DNL AEM Forms] 服务器。 如果要使用的模板上尚未包含 [!DNL AEM Forms] 服务器中，您应该先将XDP上传到 [!DNL AEM Forms] 服务器。

1. 根据您是选择默认模板还是自定义模板，“记录文档”选项卡中将显示以下部分或全部属性。 请相应地指定以下选项：

   * **徽标图像**:您可以选择使用自适应表单中的徽标图像，从DAM中选择徽标图像，或从计算机上传徽标图像。
   * **表单标题**
   * **标题文本**
   * **免责声明标签**
   * **免责声明**
   * **免责声明文本**
   * **强调颜色**:在文档或记录PDF中呈现标题文本和分隔线的颜色
   * **字体系列**:记录文档中文本的字体系列PDF
   * **对于复选框和单选按钮组件，仅显示选定的值**
   * **用于多个选定值的分隔符**
   * **包括未绑定到数据模型的表单对象**
   * **从记录文档中排除隐藏字段**
   * **隐藏面板描述**

   >[!NOTE]
   >
   >如果您使用的自适应表单模板是使用6.3之前的Designer版本创建的，要使“强调颜色”和“字体系列”属性正常工作，请确保根子表单下的自适应表单模板中存在以下内容：

   ```xml
   <proto>
   <font typeface="Arial"/>
   <fill>
   <color value="4,166,203"/>
   </fill>
   <edge>
   <color value="4,166,203"/>
   </edge>
   </proto>
   ```

1. 要保存品牌策略更改，请点按完成。

## 记录文档中面板的表和列布局 {#table-and-column-layouts-for-panels-in-document-of-record}

您的自适应表单可能是一个包含多个表单字段的冗长表单。 您可能不希望将记录文档另存为自适应表单的确切副本。 现在，您可以选择表格或列布局，以在“记录文档”PDF中保存一个或多个“自适应表单”面板。

在生成记录文档之前，在面板的设置中，为该面板的记录文档选择“布局”(Layout For The Document For The Record)作为“表”或“列”。 面板中的字段在记录文档中进行相应的组织。

![在“记录文档”的表布局中呈现的面板中的字段](assets/dortablelayout.png)

在“记录文档”的表布局中呈现的面板中的字段

![在“记录文档”中以列布局呈现的面板中的字段](assets/dorcolumnlayout.png)

在“记录文档”中以列布局呈现的面板中的字段

## 记录文档设置 {#document-of-record-settings}

“记录文档”设置允许您选择要包含在“记录文档”中的选项。 例如，银行以表格接受姓名、年龄、社会保障号码和电话号码。 表单会生成银行帐号和分行详细信息。 您可以选择在记录单中仅显示名称、社会保险号、银行帐户和分行详细信息。

记录文档组件的设置可在其属性下找到。 要访问组件的属性，请选择该组件并单击 ![cppr](assets/cmppr.png) 在叠加图中。 侧栏中列出了这些属性，您可以在其中找到以下设置。

**字段级别设置**

* **从记录文档中排除**:将属性设置为true会从记录文档中排除该字段。 这是名为的可脚本属性 `excludeFromDoR`. 其行为取决于 **隐藏时从DoR中排除字段** 表单级别属性。

* **将面板显示为表格：** 如果面板中的字段少于6个，则设置属性会将面板显示为“记录文档”中的表。 仅适用于面板。
* **从记录文档中排除标题：** 设置属性会从记录文档中排除面板/表的标题。 仅适用于面板和表。
* **从记录文档中排除说明：** 设置属性时，“记录文档”中不包含面板/表的说明。 仅适用于面板和表。

**表单级别设置**

* **在DoR中包含未绑定字段：** 设置属性包括记录文档中基于架构的自适应表单中的未绑定字段。 默认情况下，为true。
* **隐藏时从DoR中排除字段：** 设置属性会覆盖“从记录文档中排除”字段级别属性（如果不为true）的行为。 如果字段在表单提交时处于隐藏状态，则如果该属性设置为true，则它们将从记录文档中排除，但前提是未设置“从记录文档排除”属性。 设置 [在服务器上重新验证](/help/forms/configuring-submit-actions.md#server-side-revalidation-in-adaptive-form-server-side-revalidation-in-adaptive-form) 属性为true可标识要从服务器端记录文档中排除的隐藏字段。

## 使用自定义XCI文件

XCI文件可帮助您设置文档的各种属性。 Formsas a Cloud Service有一个主控的XCI文件。 您可以使用自定义XCI文件覆盖在主控XCI文件中指定的一个或多个默认属性。 例如，您可以选择将字体嵌入文档或为所有文档启用标记属性。 下表指定了XCI选项：

| XCI选项 | 描述 |
|--- |--- |
| config/present/pdf/creator | 使用“文档信息”词典中的“创建者”条目标识文档创建者。 有关该词典的信息，请参阅 [PDF参考指南](https://opensource.adobe.com/dc-acrobat-sdk-docs/acrobatsdk/). |
| config/present/pdf/producer | 使用“文档信息”词典中的“制作者”条目标识文档制作者。 有关该词典的信息，请参阅 [PDF参考指南](https://opensource.adobe.com/dc-acrobat-sdk-docs/acrobatsdk/). |
| 配置/存在/布局 | 控制输出是单个面板还是分页。 |
| config/present/pdf/compression/level | 指定在生成PDF文档时要使用的压缩度。 |
| config/present/pdf/fontInfo/embed | 控制在输出文档中嵌入字体。 |
| config/present/pdf/scriptModel | 控制输出PDF文档中是否包含XFA特定信息。 |
| config/present/common/data/adjustData | 控制XFA应用程序是否在合并后调整数据。 |
| config/present/pdf/renderPolicy | 控制是在服务器上完成页面内容的生成，还是将其延迟到客户端。 |
| 配置/存在/常用/区域设置 | 指定输出文档中使用的默认区域设置。 |
| 配置/存在/目标 | 如果包含在当前元素中，则指定输出格式。 当包含在openAction元素中时，指定在交互式客户端中打开文档时要执行的操作。 |
| config/present/output/type | 指定要应用于文件的压缩类型或要生成的输出类型。 |
| config/present/common/temp/uri | 指定表单URI。 |
| config/present/common/template/base | 在表单设计中为URI提供基本位置。 当此元素缺失或为空时，将使用表单设计的位置作为基础。 |
| config/present/common/log/to | 控制写入日志数据或输出数据的位置。 |
| config/present/output/to | 控制写入日志数据或输出数据的位置。 |
| config/present/script/currentPage | 指定打开文档时的初始页面。 |
| config/present/script/exclude | 通知Formsas a Cloud Service要忽略的事件。 |
| config/present/pdf/linearized | 控制输出PDF文档是否被线性化。 |
| config/present/script/runScripts | 控制执行哪组脚本Formsas a Cloud Service。 |
| config/present/pdf/tagged | 控制在输出PDF文档中包含标记。 PDF中的标记是文档中包含的用于显示文档逻辑结构的附加信息。 标记有助于辅助辅助功能和重新设置格式。 例如，页码可以标记为项目，以便屏幕阅读器不会在文本的中间发音它。 尽管标记使文档更有用，但标记也会增加文档的大小和创建文档的处理时间。 |
| config/present/pdf/fontInfo/alwaysEmbed | 指定嵌入到输出文档中的字体。 |
| config/present/pdf/fontInfo/neverEmbed | 指定永远不能嵌入到输出文档中的字体。 |
| config/present/pdf/pdfa/part | 指定文档符合的PDF/A规范的版本号。 |
| config/present/pdf/pdfa/amd | 指定PDF/A规范的修正级别。 |
| config/present/pdf/pdfa/confrance | 指定与PDF/A规范的符合级别。 |
| config/present/pdf/version | 指定要生成的PDF文档的版本 |
| config/present/pdf/version/map | 指定文档的回退字体 |

### 在Formsas a Cloud Service环境中使用自定义XCI文件

1. 将自定义XCI文件添加到您的开发项目。
1. 指定以下内容 [内联属性](/help/implementing/deploying/configuring-osgi.md):

   ```JSON
    {
     "xciFilePath": "[path of XCI file]"
    }
   ```

   例如，

   ```JSON
    {
     "xciFilePath": "/content/dam/formsanddocuments/customMinionProBoldAndTagged.xci"
    }
   ```

1. 将项目部署到Cloud Service环境。

### 在本地Formsas a Cloud Service开发环境中使用自定义XCI文件

1. 将XCI文件上传到本地开发环境。
1. 打开Cloud ServiceSDK配置管理器。 默认URL为： <http://localhost:4502/system/console/configMgr>.
1. 找到并打开 **[!UICONTROL 自适应Forms和交互式通信Web渠道]** 配置。
1. 指定XCI文件的路径，然后单击 **[!UICONTROL 保存]**.
