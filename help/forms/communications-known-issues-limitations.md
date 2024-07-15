---
title: AEM Forms中有哪些注意事项、已知问题和最佳实践？
description: 注意事项AEM Forms通信API的已知问题和最佳实践。
exl-id: e95615dd-e494-40cd-9cdf-6e9761ca3b3e
feature: Adaptive Forms
role: Admin, Developer, User
source-git-commit: 975f767e75a268a1638227ae20a533f82724c80a
workflow-type: tm+mt
source-wordcount: '1733'
ht-degree: 0%

---

# 注意事项、已知问题和最佳实践 {#best-practices-known-issues-and-limitations}

在开始使用通信API之前，请查看以下注意事项、已知问题和常见问题解答：

## 注意事项  {#considerations-for-communications-apis}

### 表单数据 {#form-data}

通信API接受通常在Designer中创建的表单设计和XML表单数据作为输入。 要使用数据填充文档，XML元素必须存在于要填充的每个表单字段的XML表单数据中。 XML元素名称必须与字段名称匹配。 如果XML元素与表单字段不对应，或者如果XML元素名称与字段名称不匹配，则忽略该元素。 无需匹配XML元素的显示顺序。 重要因素是XML元素是使用相应的值指定的。

请考虑以下示例贷款申请表：

![贷款申请表](assets/loanFormData.png)

要将数据合并到此表单设计，请创建与表单相对应的XML数据源。 以下XML表示与示例抵押应用程序表单相对应的XML数据源。

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

### 支持的文档类型 {#supported-document-types}

要完全访问Communications API的渲染功能，建议您使用XDP文件作为输入。 有时，可以使用PDF文件。 但是，使用PDF文件作为输入有以下限制：

不包含XFA流的PDF文档无法呈现为PostScript、PCL或ZPL。 通信API可以将具有XFA流(即在Designer中创建的表单)的PDF文档渲染为激光和标签格式。 如果PDF文档已经过签名、认证或包含使用权限(使用AEM FormsReader扩展服务应用)，则无法呈现这些打印格式。


### 可打印区域 {#printable-areas}

对于标签打印机，默认的0.25英寸不可打印的边距并不精确，并且会因打印机和标签大小而异，但是，建议保留0.25英寸的边距或减小它。 但是，建议不要增加不可打印的边距。 否则，在可打印区域中的信息无法正确打印。

务必确保为打印机使用正确的XDC文件。 例如，避免为300 dpi打印机选择XDC文件并将文档发送到200 dpi打印机。

### 仅适用于XFA表单(XDP/PDF)的脚本 {#scripts}

与Communications API一起使用的表单设计可以包含服务器上运行的脚本。 确保窗体设计不包含客户端上运行的脚本。 有关创建表单设计脚本的信息，请参阅[Designer帮助](use-forms-designer.md)。

<!-- #### Working with Fonts
 Document Considerations for Working with Fonts>> -->

### 字体映射 {#font-mapping}

要设计使用打印机驻留字体的表单，请在Designer中选择与打印机上可用字体匹配的字体名称。 PCL或PostScript支持的字体列表位于相应的设备配置文件（XDC文件）中。 或者，可以创建字体映射以将非打印机驻留的字体映射到具有不同字体名称的打印机驻留的字体。 例如，在PostScript场景中，对Arial®字体的引用可以映射到打印机驻留的Helvetica®字体。

如果某个字体安装在客户端计算机上，则它在Designer的下拉列表中可用。 如果未安装字体，则需要手动指定字体名称。 可以关闭Designer中的“永久替换不可用字体”选项。 否则，当XDP文件保存在Designer中时，替代字体名称将写入XDP文件。 这意味着不使用打印机驻留字体。

存在两种类型的OpenType®字体。 一种类型是PCL支持的TrueTypeOpenType®字体。 另一个是CFFOpenType®。 PDF和PostScript输出支持嵌入的Type-1、TrueType和OpenType®字体。 PCL输出支持嵌入的TrueType字体。

Type-1和OpenType®字体未嵌入到PCL输出中。 使用Type-1和OpenType®字体格式化的内容将被栅格化并生成为位图图像，该图像可能会大而慢，生成速度会比较慢。

在生成PostScript、PCL或PDF输出时，下载的字体或嵌入的字体会自动被替换。 这意味着生成的输出中只包括正确渲染生成的文档所需的字体字形子集。

### 使用设备配置文件（XDC文件） {#working-with-xdc-files}

设备配置文件（XDC文件）是XML格式的打印机说明文件。 此文件使Communications API能够以激光或标签打印机格式输出文档。 Communications API使用XDC文件，其中包括：

* hppcl5c.xdc

* hppcl5e.xdc

* ps_plain_level3.xdc

* ps_plain.xdc

* zpl300.xdc

* zpl600.xdc

* zpl300.xdc

* ipl300.xdc

* ipl400.xdc

* tpcl600.xdc

* dpl300.xdc

* dpl406.xdc

* dpl600.xdc

您可以使用提供的XDC文件生成打印文档，也可以根据需要对其进行修改。
<!-- It is not necessary to modify these files to create documents. However, you can modify them to meet your business requirements. -->

这些文件是支持特定打印机功能（如常驻字体、纸盒和装订器）的参考XDC文件。 这些参考的目的在于帮助您了解如何使用设备配置文件设置自己的打印机。 该参考也是同一产品线中类似打印机的起点。

### 使用XCI配置文件 {#working-with-xci-files}

通信API使用XCI配置文件执行任务，例如控制输出是单面板输出还是分页输出。 虽然此文件包含可以设置的设置，但通常不会修改此值。<!-- The default.xci file is located in the svcdata\XMLFormService folder. -->

您可以在使用Communications API时传递修改后的XCI文件。 在执行此操作时，请创建默认文件的副本，仅更改需要修改的值以满足您的业务要求，并使用修改后的XCI文件。

通信API以默认的XCI文件（或修改的文件）开头。 然后，它会应用使用通信API指定的值。 这些值将覆盖XCI设置。

下表指定了XCI选项。

| XCI选项 | 描述 |
| ------------------------------------| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| config/present/pdf/creator | 使用文档信息词典中的创建者条目标识文档创建者。 有关此词典的信息，请参阅《PDF参考指南》。 |
| config/present/pdf/producer | 使用文档信息词典中的制作者条目标识文档制作者。 有关此词典的信息，请参阅《PDF参考指南》。 |
| config/present/layout | 控制输出是单个面板还是分页。 |
| config/present/pdf/compression/level | 指定生成PDF文档时使用的压缩程度。 |
| config/present/pdf/scriptModel | 控制输出PDF文档中是否包含XFA特定的信息。 |
| config/present/common/data/adjustData | 控制XFA应用程序在合并后是否调整数据。 |
| config/present/pdf/renderPolicy | 控制页面内容的生成是在服务器上完成还是延迟到客户端。 |
| config/present/common/locale | 指定输出文档中使用的默认区域设置。 |
| config/present/destination | 当由当前元素包含时，指定输出格式。 当由openAction元素包含时，指定在交互式客户端中打开文档时要执行的操作。 |
| config/present/output/type | 指定要应用于文件的压缩类型或要生成的输出类型。 |
| config/present/common/temp/uri | 指定表单URI。 |
| config/present/common/template/base | 在表单设计中提供URI的基本位置。 当此元素不存在或为空时，将使用窗体设计的位置作为基础。 |
| config/present/common/log/to | 控制日志数据或输出数据写入的位置。 |
| config/present/output/to | 控制日志数据或输出数据写入的位置。 |
| config/present/script/currentPage | 指定文档打开时的初始页面。 |
| config/present/script/exclude | 告知AEM Forms服务器/通信API要忽略哪些事件。 |
| config/present/pdf/linearized | 控制输出PDF文档是否线性化。 |
| config/present/script/runScripts | 控制AEM Forms执行的脚本集。 |
| config/present/pdf/tagged | 控制标签在输出PDF文档中的包含。 在PDF上下文中，标记是文档中包含的其他信息，用于公开文档的逻辑结构。 标记有助于辅助功能和重新设置格式。 例如，页码可能会被标记为工件，这样屏幕阅读器就不会在文本中间朗读它。 虽然标记可以使文档更有用，但它们也会增加文档的大小以及创建文档所需的处理时间。 |
| config/present/pdf/version | 指定要生成的PDF文档的版本。 |


## 已知问题

* 在打印选项列表中，只能使用一次特定渲染类型(PDF、打印)。 例如，不能有两个PRINT选项，每个选项都指定PCL渲染类型。

* 对于批处理配置，只允许一个OutputType(PDF、打印)和RenderType(PostScript、PCL、IPL、ZPL等)值的组合实例。

* 对于异步API（批处理），默认记录级别设置为2。 您可以使用自定义XCI将记录级别更改为1。

* 配置默认XCI后，它将包含原始演绎版的路径。 例如，`/content/dam/formsanddocuments/default.xci/jcr:content/renditions/original`



## 最佳实践

* Adobe建议将数据文件blob容器存储托管在AEM Cloud Service使用的云区域中。

## 常见问题解答 {#faq}

**我是否可以使用观察文件夹或其他存储机制来存储输入和输出？**

目前，您可以使用Microsoft Azure Storage保存输入数据和生成的文档。 Microsoft Azure Storage提供了多种选项，用于[自动执行数据移动操作](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10)。

**Experience Manager FormsCloud Service许可证中是否包括Microsoft Azure Storage帐户？**

Microsoft Azure Storage帐户独立于Experience Manager FormsCloud Service许可证。

**通信API是否在Experience Manager FormsCloud Service服务器上存储数据？**

输入和输出数据仅保存在Microsoft Azure Storage上。

**通信API是否仅可用于Experience Manager FormsCloud Service？ 能否在内部部署环境中获得类似的功能？**

您可以使用AEM Forms Output服务将模板(XFA或PDF)与客户数据相结合，生成PDF、PS、PCL和ZPL格式的文档。

与内部部署环境相比，该Cloud Service提供了自动扩展和成本效益方面的更多优势。

<!--**Where is data processed?**

**Who has access to data?**

**Is data encrypted?**

**Where is data hosted?** -->

**我可以同时运行多个批处理操作吗？**
可以，您可以同时运行多个批操作。 请始终对每项操作使用不同的源文件夹和目标文件夹，以避免任何冲突。

>[!MORELIKETHIS]
>
>* [AEM Formsas a Cloud Service通信简介](/help/forms/aem-forms-cloud-service-communications-introduction.md)
>* 自适应AEM Forms和通信API的[Formsas a Cloud Service架构](/help/forms/aem-forms-cloud-service-architecture.md)
>* [通信处理 — 同步API](/help/forms/aem-forms-cloud-service-communications.md)
>* [通信处理 — 批处理API](/help/forms/aem-forms-cloud-service-communications-batch-processing.md)

