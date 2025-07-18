---
title: 如何编辑或添加元数据
description: 了解 [!DNL Experience Manager Assets] 中资源元数据的各种编辑方式。
contentOwner: AG
feature: Metadata
role: User, Admin
exl-id: 464a97ce-da3e-47b5-9879-fafaf2f2378c
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 9%

---

# 如何编辑或添加元数据 {#how-to-edit-or-add-metadata}

元数据是可搜索的资产的其他相关信息。 上传图像时，会自动提取该值。 您可以编辑现有元数据或向现有字段添加新元数据属性（例如，当元数据字段为空时）。

由于公司需要受控且可靠的元数据词汇，[!DNL Experience Manager Assets]不允许按需添加新元数据属性。 尽管作者无法为资产添加新元数据字段，但开发人员可以。 请参阅[为Assets创建新的元数据属性](meta-edit.md#editing-metadata-schema)。

## 编辑资源的元数据 {#editing-metadata-for-an-asset}

要编辑元数据，请执行以下操作：

1. 执行下列操作之一：

   * 从Assets UI中，选择资源，然后从工具栏中选择&#x200B;**[!UICONTROL 查看属性]**&#x200B;图标。
   * 从资产缩略图中，选择&#x200B;**[!UICONTROL 查看属性]**&#x200B;快速操作。
   * 在资源页面中，从工具栏中选择&#x200B;**[!UICONTROL 查看属性]**。

   资源页面显示资源的元数据。 此元数据在上传（引入）到Experience Manager Assets后会自动提取。

1. 根据需要，在各个选项卡下对元数据进行编辑，完成后，从工具栏中选择&#x200B;**[!UICONTROL 保存]**&#x200B;以保存更改。 选择&#x200B;**[!UICONTROL 关闭]**&#x200B;以返回到Assets Web界面。

   >[!NOTE]
   >
   >如果文本字段为空，则不存在现有的元数据集。 您可以在字段中输入值并将其保存以添加该元数据属性。

对资源元数据所做的任何更改都将作为其XMP数据的一部分写回原始二进制文件。 这是通过Experience Manager元数据回写工作流完成的。 对现有属性（如`dc:title`）所做的更改将被覆盖，创建的属性（包括自定义属性，如`cq:tags`）将与架构一起添加。

<!-- XMP write-back is supported and enabled for the platforms and file formats described in technical requirements. -->

## 编辑元数据架构 {#editing-metadata-schema}

有关如何编辑元数据架构的详细信息，请参阅[编辑元数据架构表单](metadata-schemas.md#edit-metadata-schema-forms)。

## 在Experience Manager中注册自定义命名空间 {#registering-a-custom-namespace-within-aem}

您可以在Experience Manager中添加自己的命名空间。 就像存在预定义的命名空间（如cq、jcr和sling）一样，您也可以具有用于存储库元数据和xml处理的命名空间。

1. 转到节点类型管理页面&#x200B;*https://&lt;主机>：&lt;端口>/crx/explorer/nodetypes/index.jsp*。
1. 选择页面顶部的&#x200B;**[!UICONTROL 命名空间]**。 命名空间管理页面将显示在窗口中。

1. 若要添加命名空间，请选择底部的&#x200B;**[!UICONTROL 新建]**。
1. 以XML命名空间惯例指定自定义命名空间（以URI形式指定ID并为ID指定关联的前缀），然后选择&#x200B;**[!UICONTROL 保存]**。

**另请参阅**

* [翻译资源](translate-assets.md)
* [Assets HTTP API](mac-api-assets.md)
* [资源支持的文件格式](file-format-support.md)
* [搜索资源](search-assets.md)
* [连接的资源](use-assets-across-connected-assets-instances.md)
* [资源报告](asset-reports.md)
* [元数据架构](metadata-schemas.md)
* [下载资源](download-assets-from-aem.md)
* [管理元数据](manage-metadata.md)
* [搜索 Facet](search-facets.md)
* [管理收藏集](manage-collections.md)
* [批量元数据导入](metadata-import-export.md)
* [发布资源到 AEM 和 Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)
