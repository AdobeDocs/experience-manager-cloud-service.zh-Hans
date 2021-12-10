---
title: AEM Formsas a Cloud Service — 通信
description: 自动将数据与XDP和PDF模板合并，或以PCL、ZPL和PostScript格式生成输出
exl-id: 9fa9959e-b4f2-43ac-9015-07f57485699f
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '2372'
ht-degree: 0%

---


# 使用AEM Formsas a Cloud Service通信API {#frequently-asked-questions}

**“通信”功能处于测试阶段。**

通信API可帮助您将XDP模板、基于XDP的PDF文档以及Acrobat Forms(AcroForm)与XML数据结合使用，以生成各种格式的打印文档，并使您能够创建应用程序，以便：

- 使用XML数据填充模板文件，以生成文档。

- 以各种格式生成表单，包括非交互式PDF打印流。

- 从XFA表单PDF中生成打印PDF。

- 通过将多组数据与源模板合并，批量生成PDF、 PostScript、PCL和ZPL文档。

假设您有一个或多个模板以及每个模板的多个XML数据记录。 您可以使用通信API为每个记录生成打印文档。 <!-- You can also combine the records into a single document. --> 结果会生成一个非交互式PDF文档。 非交互式PDF文档不允许用户在其字段中输入数据。

的 [API参考文档](https://documentcloud.adobe.com/link/track?uri=urn:aaid:scds:US:b1223732-ae0f-4921-bdc0-c31e48b56044) 提供有关API提供的所有API、参数、身份验证方法和各种服务的详细信息。 API引用文档也提供.yaml格式。 您可以下载 [批量API](assets/batch-api.yaml) 或 [非批量API.yaml](assets/non-batch-api.yaml) 文件并将其上传到postman，以检查API的功能。

>[!VIDEO](https://video.tv.adobe.com/v/335771)

将通信API .yaml文件上传到Postman以检查API的功能。

>[!NOTE]
>
>只有表单用户组的成员才能访问通信API。

## 启用通信

要为Formsas a Cloud Service环境启用通信，请执行以下操作：

1. 登录到Cloud Manager并打开AEM Formsas a Cloud Service实例。

1. 打开编辑程序选项，转到解决方案和加载项选项卡，然后选择 **[!UICONTROL Forms — 通信]** 选项。

   <!-- ![Communications](assets\communications.png)

    If you have already enabled the **[!UICONTROL Forms - Digital Enrollment]** option, then select the **[!UICONTROL Forms - Communications Add-On]** option.  

    <!-- ![Addon](assets\add-on.png) -->

1. 单击 **[!UICONTROL 更新]**.

1. 运行生成管道。

构建配置成功后，将为您的环境启用通信API。

## 使用通信API {#workflows}

通常，您使用 [Designer](use-forms-designer.md) 和使用通信API:

- 将这些模板转换为各种格式，包括PDF、PostScript、ZPL和PCL。
- 将XML表单数据与表单设计合并，以生成文档。
- 生成文档，而不将XML表单数据合并到文档中。 但是，主工作流将数据合并到文档中。

然后，将输出文档存储到文件中。 您可以设计自定义工作流，以将文件发送到网络打印机、本地打印机或存储系统进行存档。 典型的开箱即用工作流和自定义工作流如下所示：

![通信工作流](assets/communicaions-workflow.png)

### 创建PDF文档 {#create-pdf-documents}

您可以使用 _generatePDFOutput_ 用于创建基于表单设计和XML表单数据的PDF文档的API。 输出是非交互式PDF文档。 即用户无法输入或修改表单数据。 基本的工作流程是将XML表单数据与表单设计合并，以创建PDF文档。 下图显示了表单设计和XML表单数据的合并，以生成PDF文档。

![创建PDF文档](assets/outPutPDF_popup.png)

### 创建PostScript(PS)、打印机命令语言(PCL)、Zebra打印语言(ZPL)文档 {#create-PS-PCL-ZPL-documents}

您可以使用通信API创建基于XDP表单设计或PDF文档的PostScript(PS)、打印机命令语言(PCL)和Zebra打印语言(ZPL)文档。 的 _generatePrintedOutput_ API将表单设计与表单数据合并以生成文档。 您可以将文档保存到文件并开发一个自定义流程以将其发送到打印机。

<!-- ### Processing batch data to create multiple documents

Communications APIs can create separate documents for each record within an XML batch data source. The APIs can also create a single document that contains all records (this functionality is the default). Assume that an XML data source contains ten records and you instruct the APIs to create a separate document for each record (for example, PDF documents). As a result, the APIs generate ten PDF documents.

The following illustration also shows Communications APIs processing an XML data file that contains multiple records. However, assume that you instruct the APIs to create a single PDF document that contains all data records. In this situation, the APIs generate one document that contains all of the records.

The following illustration shows Communications APIs processing an XML data file that contains multiple records. Assume that you instruct the Communications APIs to create a separate PDF document for each data record. In this situation, the APIs generates a separate PDF document for each data record.

 -->

### 处理批量数据以创建多个文档 {#processing-batch-data-to-create-multiple-documents}

您可以为XML批量数据源中的每个记录创建单独的文档。 您可以在批量和异步模式下生成文档。 您可以为转换配置各种参数，然后启动批处理。 <!-- You can can also create a single document that contains all records (this functionality is the default).  Assume that an XML data source contains ten records and you have a requirement to create a separate document for each record (for example, PDF documents). You can use the Communication APIs to generate ten PDF documents. -->

<!-- The following illustration shows the Communication APIs processing an XML data file that contains multiple records. However, assume that you instruct the Communication APIs to create a single PDF document that contains all data records. In this situation, the Communication APIs generate one document that contains all of the records.

![Create PDF Documents](assets/ou_OutputBatchSingle_popup.png)

The following illustration shows the Communication APIs processing an XML data file that contains multiple records. Assume that you instruct the Communication APIs to create a separate PDF document for each data record. In this situation, the Communication APIs generates a separate PDF document for each data record.

![Create PDF Documents](assets/ou_OutputBatchMany_popup.png)

For detailed information on using Batch APIs, see Communication APIs: Processing batch data to create multiple documents. -->

### 扁平化交互式PDF文档 {#flatten-interactive-pdf-documents}

您可以使用通信API将交互式PDF文档（例如，表单）转换为非交互式PDF文档。 交互式PDF文档允许用户输入或修改位于PDF文档字段中的数据。 将交互式PDF文档转换为非交互式PDF文档的过程称为拼合。 对PDF文档进行扁平化处理后，用户无法修改位于文档字段中的数据。 扁平化PDF文档的一个原因是要确保数据无法修改。

您可以拼合以下类型的PDF文档：

- 在Designer中创建的交互式PDF文档（包含XFA流）。

- AcrobatPDF forms

如果尝试扁平化非交互式PDF文档，则会出现异常。

### 保留表单状态 {#retain-form-state}

交互式PDF文档包含构成表单的各种元素。 这些元素可能包括字段（用于接受或显示数据）、按钮（用于触发事件）和脚本（用于执行特定操作的命令）。 单击按钮可能会触发更改字段状态的事件。 例如，选择性别选项可能会更改字段的颜色或表单的外观。 这是导致表单状态更改的手动事件示例。

如果使用通信API对此类交互式PDF文档进行扁平化处理，则不会保留表单的状态。 要确保即使对表单进行扁平化处理后仍保留表单状态，请设置布尔值 _retainFormState_ 设置为True可保存并保留表单的状态。

### 有关通信API的注意事项 {#considerations-for-communications-apis}

#### 表单数据 {#form-data}

通信API接受通常在Designer中创建的表单设计和作为输入的XML表单数据。 要使用数据填充文档，每个要填充的表单字段的XML表单数据中必须存在XML元素。 XML元素名称必须与字段名称匹配。 如果XML元素与表单字段不对应，或XML元素名称与字段名称不匹配，则忽略该元素。 不必与XML元素的显示顺序匹配。 重要因素是XML元素是使用相应值指定的。

请考虑以下贷款申请表示例：

![贷款申请表](assets/loanFormData.png)

要将数据合并到此表单设计中，请创建与表单对应的XML数据源。 以下XML表示与示例抵押申请表单对应的XML数据源。

```XML
<?xml version="1.0" encoding="UTF-8" ?>
- <xfa:datasets xmlns:xfa="http://www.xfa.org/schema/xfa-data/1.0/">
- <xfa:data>
- <data>
    - <Layer>
        <closeDate>1/26/2007</closeDate>
        <lastName>Johnson</lastName>
        <firstName>Jerry</firstName>
        <mailingAddress>JJohnson@NoMailServer.com</mailingAddress>
        <city>New York</city>
        <zipCode>00501</zipCode>
        <state>NY</state>
        <dateBirth>26/08/1973</dateBirth>
        <middleInitials>D</middleInitials>
        <socialSecurityNumber>(555) 555-5555</socialSecurityNumber>
        <phoneNumber>5555550000</phoneNumber>
    </Layer>
    - <Mortgage>
        <mortgageAmount>295000.00</mortgageAmount>
        <monthlyMortgagePayment>1724.54</monthlyMortgagePayment>
        <purchasePrice>300000</purchasePrice>
        <downPayment>5000</downPayment>
        <term>25</term>
        <interestRate>5.00</interestRate>
    </Mortgage>
</data>
</xfa:data>
</xfa:datasets>
```

#### 支持的文档类型 {#supported-document-types}

要完全访问通信API的渲染功能，建议使用XDP文件作为输入。 在某些情况下，可以使用PDF文件。 但是，使用PDF文件作为输入具有以下限制：

- 不包含XFA流的PDF文档无法呈现为PostScript、PCL或ZPL。 通信API可以将具有XFA流（即在Designer中创建的表单）的PDF文档渲染为激光和标签格式。 如果PDF文档已签名、已认证或包含使用权限(使用AEM FormsReader扩展服务应用)，则无法将其呈现为这些打印格式。

<!-- * Run-time options such as PDF version and tagged PDF are not supported for Acrobat forms. They are valid for PDF forms that contain XFA streams; however, these forms cannot be signed or certified. 

#### Email support {#email-support}

For email functionality, you can create a process in AEM Workflows that uses the Email Step. A workflow represents a business process that you are automating. -->

#### 可打印区域 {#printable-areas}

默认的0.25英寸不可打印边距对于标签打印机不精确，因而会因打印机和打印机以及标签大小和标签大小而异。 建议您保持0.25英寸的边距或减小它。 但是，建议不要增加不可打印的边距。 否则，可打印区域中的信息无法正确打印。

始终确保为打印机使用正确的XDC文件。 例如，避免为300 dpi打印机选择XDC文件，并将文档发送到200 dpi打印机。

#### 脚本 {#scripts}

与通信API一起使用的表单设计可以包含在服务器上运行的脚本。 确保表单设计不包含在客户端上运行的脚本。 有关创建表单设计脚本的信息，请参阅设计器帮助。

<!-- #### Working with Fonts
 Document Considerations for Working with Fonts>> -->

#### 字体映射 {#font-mapping}

如果字体安装在客户端计算机上，则该字体会显示在Designer的下拉列表中。 如果未安装字体，则需要手动指定字体名称。 Designer中的“永久替换不可用字体”选项可能会关闭。 否则，在Designer中保存XDP文件时，替换字体名称将写入XDP文件。 这表示不使用打印机驻留字体。

要设计使用打印机驻留字体的表单，请在Designer中选择与打印机上可用字体匹配的字体名称。 PCL或PostScript支持的字体列表位于相应的设备配置文件（XDC文件）中。 或者，可以创建字体映射以将非打印机驻留字体映射到不同字体名称的打印机驻留字体。 例如，在PostScript方案中，对Arial®字体的引用可以映射到打印机驻留的Helvetica®字体。

存在两种类型的OpenType®字体。 一种是PCL支持的TrueTypeOpenType®字体。 另一个是CFFOpenType®。 PDF和PostScript输出支持嵌入的Type-1、TrueType和OpenType®字体。 PCL输出支持嵌入的TrueType字体。

Type-1和OpenType®字体未嵌入到PCL输出中。 使用Type-1和Adobe Analytics®字体格式化的内容将作为位图图像进行光栅化和生成，该图像可以大而慢，因此可以生成。

在生成PostScript、PCL或PDF输出时，下载或嵌入的字体会自动替换。 这意味着，在生成的输出中只包含正确呈现生成的文档所需的字体字形子集。

#### 使用设备配置文件（XDC文件） {#working-with-xdc-files}

设备配置文件（XDC文件）是XML格式的打印机描述文件。 此文件允许通信API将文档输出为激光打印机格式或标记打印机格式。 通信API使用XDC文件，包括：

- hppcl5c.xdc

- hppcl5e.xdc

- ps_plain_level3.xdc

- ps_plain.xdc

- zpl300.xdc

- zpl600.xdc

- zpl300.xdc

- ipl300.xdc

- ipl400.xdc

- tpcl600.xdc

- dpl300.xdc

- dpl406.xdc

- dpl600.xdc

无需修改这些文件即可创建文档。 但是，您可以修改它们以满足您的业务需求。

这些文件是支持特定打印机功能的示例XDC文件，如驻留字体、纸盘和订书机。 这些示例旨在帮助您了解如何使用设备配置文件来设置您自己的打印机。 这些示例也是同一产品线中类似打印机的起点。

#### 使用XCI配置文件 {#working-with-xci-files}

通信API使用XCI配置文件来执行任务，例如控制输出是单个面板还是分页。 尽管此文件包含可设置的设置，但修改此值并不是典型操作。 <!-- The default.xci file is located in the svcdata\XMLFormService folder. -->

您可以在使用通信API时传递修改的XCI文件。 这样做时，请创建默认文件的副本，仅更改需要修改以满足业务要求的值，然后使用修改后的XCI文件。

通信API以默认XCI文件（或修改后的文件）开头。 然后，它会应用使用通信API指定的值。 这些值会覆盖XCI设置。

下表指定了XCI选项。

| XCI选项 | 描述 |
| ------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| config/present/pdf/creator | 使用“文档信息”词典中的“创建者”条目标识文档创建者。 有关该词典的信息，请参阅PDF参考指南。 |
| config/present/pdf/producer | 使用“文档信息”词典中的“制作者”条目标识文档制作者。 有关该词典的信息，请参阅PDF参考指南。 |
| 配置/存在/布局 | 控制输出是单个面板还是分页。 |
| config/present/pdf/compression/level | 指定在生成PDF文档时要使用的压缩度。 |
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
| config/present/script/exclude | 通知AEM Forms服务器/通信API要忽略的事件。 |
| config/present/pdf/linearized | 控制输出PDF文档是否被线性化。 |
| config/present/script/runScripts | 控制执行哪组脚本AEM Forms。 |
| config/present/pdf/tagged | 控制在输出PDF文档中包含标记。 PDF中的标记是文档中包含的用于显示文档逻辑结构的附加信息。 标记有助于辅助辅助功能和重新设置格式。 例如，页码可以标记为项目，以便屏幕阅读器不会在文本的中间发音它。 尽管标记使文档更有用，但标记也会增加文档的大小和创建文档的处理时间。 |
| config/present/pdf/version | 指定要生成的PDF文档的版本。 |

### 已知问题

- 确保模板和XCI配置文件的大小大于16KB。

- 确保数据xml文件不包含XML声明标头。 例如, `<?xml version="1.0" encoding="UTF-8"?>`

- 对于批量配置，只有OutputType(PDF、打印)和RenderType（PostScript、PCL、IPL、ZPL等）值组合的一个实例 中的“禁止页面加载闪烁”。

- 在运行批处理时，请勿修改批处理配置中使用的数据源USC配置/Azure云配置。 即使在执行后，如果需要进行任何更新，也应创建配置副本，而不是更新现有批量配置中使用的配置副本。

### 最佳实践

- Adobe建议将数据文件blob容器存储托管在AEM Cloud Service使用的云区域中。

<!-- Using API

 There are two main Communications APIs. The _generatePDFOutput_ generates PDFs, while the _generatePrintedOutput_ generates PostScript, ZPL, and PCL formats. These APIs are available as HTTP endpoints on your environment, both on author and publish instances. Since the publish instances are configured to scale faster than the author instances, it is recommended use these APIs via publish instances.

The first parameter of both the operations accept the path and name of the template file (for example ExpenseClaim.xdp). You can specify a fully qualified path, reference path of your AEM Repository, or path of a binary file. The second parameter accepts an XML document that is merged with the template while generating the output document. -->


