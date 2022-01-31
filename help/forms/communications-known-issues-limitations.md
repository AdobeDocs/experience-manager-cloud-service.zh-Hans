---
title: '已知问题 '
description: 通信最佳实践、已知问题和限制
source-git-commit: c38a34519822449ff2577a9474b1294d5d45d3ae
workflow-type: tm+mt
source-wordcount: '1666'
ht-degree: 0%

---


# 已知问题的注意事项和最佳实践 {#best-practices-known-issues-and-limitations}

在开始使用通信API之前，请查看以下注意事项、已知问题和常见问题：

## 注意事项  {#considerations-for-communications-apis}

### 表单数据 {#form-data}

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

### 支持的文档类型 {#supported-document-types}

要完全访问通信API的渲染功能，建议使用XDP文件作为输入。 有时，可以使用PDF文件。 但是，使用PDF文件作为输入具有以下限制：

不包含XFA流的PDF文档无法呈现为PostScript、PCL或ZPL。 通信API可以将具有XFA流（即在Designer中创建的表单）的PDF文档渲染为激光和标签格式。 如果PDF文档已签名、已认证或包含使用权限(使用AEM FormsReader扩展服务应用)，则无法将其呈现为这些打印格式。


### 可打印区域 {#printable-areas}

默认的0.25英寸不可打印边距对于标签打印机不精确，因而会因打印机和打印机的不同而异，从标签大小到标签大小，但建议保留0.25英寸边距或将其减小。 但是，建议不要增加不可打印的边距。 否则，可打印区域中的信息无法正确打印。

始终确保为打印机使用正确的XDC文件。 例如，避免为300 dpi打印机选择XDC文件，并将文档发送到200 dpi打印机。

### XFA表单的脚本(仅限XDP/PDF) {#scripts}

与通信API一起使用的表单设计可以包含在服务器上运行的脚本。 确保表单设计不包含在客户端上运行的脚本。 有关创建表单设计脚本的信息，请参阅 [Designer帮助](use-forms-designer.md).

<!-- #### Working with Fonts
 Document Considerations for Working with Fonts>> -->

### 字体映射 {#font-mapping}

要设计使用打印机驻留字体的表单，请在Designer中选择与打印机上可用字体匹配的字体名称。 PCL或PostScript支持的字体列表位于相应的设备配置文件（XDC文件）中。 或者，可以创建字体映射以将非打印机驻留字体映射到不同字体名称的打印机驻留字体。 例如，在PostScript方案中，对Arial®字体的引用可以映射到打印机驻留的Helvetica®字体。

如果字体安装在客户端计算机上，则该字体会显示在Designer的下拉列表中。 如果未安装字体，则需要手动指定字体名称。 Designer中的“永久替换不可用字体”选项可能会关闭。 否则，在Designer中保存XDP文件时，替换字体名称将写入XDP文件。 这意味着不使用打印机驻留字体。

存在两种类型的OpenType®字体。 一种是PCL支持的TrueTypeOpenType®字体。 另一个是CFFOpenType®。 PDF和PostScript输出支持嵌入的Type-1、TrueType和OpenType®字体。 PCL输出支持嵌入的TrueType字体。

Type-1和OpenType®字体未嵌入到PCL输出中。 使用Type-1和Adobe Analytics®字体格式化的内容将作为位图图像进行光栅化和生成，该图像可以大而慢，因此可以生成。

在生成PostScript、PCL或PDF输出时，下载或嵌入的字体会自动替换。 这意味着，在生成的输出中只包含正确呈现生成的文档所需的字体字形子集。

### 使用设备配置文件（XDC文件） {#working-with-xdc-files}

设备配置文件（XDC文件）是XML格式的打印机描述文件。 此文件允许通信API将文档输出为激光打印机格式或标记打印机格式。 通信API使用XDC文件，其中包括：

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

您可以使用提供的XDC文件来生成打印文档或根据您的要求对其进行修改。
<!-- It is not necessary to modify these files to create documents. However, you can modify them to meet your business requirements. -->

这些文件是支持特定打印机功能（如驻留字体、纸盘和订书机）的引用XDC文件。 这些参考旨在帮助您了解如何使用设备配置文件来设置您自己的打印机。 参考也是同一产品线中类似打印机的起点。

### 使用XCI配置文件 {#working-with-xci-files}

通信API使用XCI配置文件来执行任务，例如控制输出是单个面板还是分页。 尽管此文件包含可设置的设置，但修改此值并不是典型操作。 <!-- The default.xci file is located in the svcdata\XMLFormService folder. -->

您可以在使用通信API时传递修改的XCI文件。 这样做时，请创建默认文件的副本，仅更改需要修改以满足业务要求的值，然后使用修改后的XCI文件。

通信API以默认XCI文件（或修改后的文件）开头。 然后，它会应用使用通信API指定的值。 这些值会覆盖XCI设置。

下表指定了XCI选项。

| XCI选项 | 描述 |
| ------------------------------------| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
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


## 已知问题

* 在打印选项列表中，您只能使用一次特定渲染类型(PDF、打印)。 例如，您不能有两个PRINT选项，每个选项指定PCL呈现类型。

* 对于批量配置，只有OutputType(PDF、打印)和RenderType（PostScript、PCL、IPL、ZPL等）值组合的一个实例 中的“禁止页面加载闪烁”。

## 最佳实践

* Adobe建议将数据文件blob容器存储托管在AEM Cloud Service使用的云区域中。

## 常见问题 {#faq}

**我是否可以使用监视文件夹或其他存储机制来存储输入和输出？**

目前，您可以使用Microsoft Azure Storage保存输入数据和生成的文档。 Microsoft Azure存储提供了多种 [自动化数据移动操作](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10).

**Experience Manager FormsCloud Service许可证中是否包含Microsoft Azure存储帐户？**

Microsoft Azure存储帐户独立于Experience Manager FormsCloud Service许可证。

**通信API是否在Experience Manager FormsCloud Service服务器上存储数据？**

输入和输出数据仅保存在Microsoft Azure存储中。

**通信API是否仅可用于Experience Manager FormsCloud Service? 我能否在内部部署环境中获得类似的功能？**

您可以使用AEM Forms输出服务将模板(XFA或PDF)与客户数据结合，以生成PDF、PS、PCL和ZPL格式的文档。

与内部部署环境相比，本Cloud Service提供了自动扩展和成本效益的额外优势。

<!--**Where is data processed?**

**Who has access to data?**

**Is data encrypted?**

**Where is data hosted?** -->

**我是否可以同时运行多个批处理操作？**
是，您可以简单地运行多个批处理操作。 请始终对每个操作使用不同的源文件夹和目标文件夹，以避免任何冲突。
