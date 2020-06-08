---
title: 如何编辑或添加元数据
description: 了解AEM资产中的资产元数据以及编辑资产元数据的各种方式。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 991d4900862c92684ed92c1afc081f3e2d76c7ff
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 9%

---


# 如何编辑或添加元数据 {#how-to-edit-or-add-metadata}

元数据是有关可搜索资产的其他信息。 上传图像时会自动提取图像。 您可以编辑现有元数据或向现有字段添加新的元数据属性（例如，当元数据字段为空时）。

由于公司需要可控且可靠的元数据词汇，因此AEM资产不允许临时添加新元数据属性。 尽管作者无法为资产添加新的元数据字段，但开发人员可以。 请参 [阅为资产创建新的元数据属性](meta-edit.md#editing-metadata-schema)。

## 编辑资产的元数据 {#editing-metadata-for-an-asset}

要编辑元数据，请执行以下操作：

1. 执行下列操作之一：

   * 在资产UI中，选择资产，然后单击／点按工 **[!UICONTROL 具栏中的视图]** 属性图标。
   * 从资产缩略图中，选择 **[!UICONTROL 视图属性]** 快速操作。
   * 在资产页面中，单击／点按工 **[!UICONTROL 具栏中的]** 视图属性。

   资产页面会显示资产的所有元数据。 此元数据在上传（摄取）到AEM资产时会自动提取。

1. 根据需要，在各个选项卡下对元数据进行编辑，完成后，单击／点按工具栏中的 **[!UICONTROL 保存]** ，以保存更改。 单击／点 **[!UICONTROL 按关闭]** ，以返回到资产Web界面。

   >[!NOTE]
   >
   >如果文本字段为空，则没有现有元数据集。 您可以在字段中输入一个值并保存它以添加该元数据属性。

对资产元数据所做的任何更改都会作为其XMP数据的一部分写回原始二进制文件。 这是通过AEM元数据回写工作流来完成的。 对现有属性（如）所做的更 `dc:title`改会被覆盖，新创建的属性(包括自定义属 `cq:tags`性等)会与模式一起添加。

<!-- XMP write-back is supported and enabled for the platforms and file formats described in technical requirements. -->

## 编辑元数据模式 {#editing-metadata-schema}

有关如何编辑元数据模式的详细信息，请参 [阅编辑元数据模式表单](metadata-schemas.md#edit-metadata-schema-forms)。

## 在AEM中注册自定义命名空间 {#registering-a-custom-namespace-within-aem}

您可以在AEM中添加您自己的命名空间。 正如存在预定义的命名空间（如cq、jcr和sling）一样，您也可以对存储库元数据和xml处理进行命名空间。

1. 转到节点类型管 *理页https://&lt;host>:&lt;port>/crx/explorer/nodetypes/index.jsp*。
1. 单击或点 **[!UICONTROL 按]** 页面顶部的命名空间。 命名空间管理页面显示在窗口中。

1. 要添加命名空间，请单击或点 **[!UICONTROL 按]** 底部的“新建”。
1. 在XML命名空间约定中指定自定义命名空间（以URI形式指定id并为id指定关联前缀），然后单击或点按保 **[!UICONTROL 存]**。
