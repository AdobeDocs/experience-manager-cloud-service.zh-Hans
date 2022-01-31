---
title: '已知问题 '
description: 通信最佳实践、已知问题和限制
source-git-commit: 06da7d2a5063e163aa1534bedbc79ae50ef27515
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 2%

---


# 常见问题解答、最佳实践、已知问题和限制 {#best-practices-known-issues-and-limitations}

在开始使用通信API之前，请查看以下已知问题和限制：

## 已知问题

- 在打印选项列表中，您只能使用一次特定渲染类型(PDF、打印)。 例如，您不能有两个PRINT选项，每个选项指定PCL呈现类型。

- 对于批量配置，只有OutputType(PDF、打印)和RenderType（PostScript、PCL、IPL、ZPL等）值组合的一个实例 中的“禁止页面加载闪烁”。

## 最佳实践

- Adobe建议将数据文件blob容器存储托管在AEM Cloud Service使用的云区域中。

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
