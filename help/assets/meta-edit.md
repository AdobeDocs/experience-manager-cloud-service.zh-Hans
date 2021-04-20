---
title: 如何编辑或添加元数据
description: 通过 [!DNL Experience Manager Assets] 了解资产元数据，通过各种方式编辑资产元数据。
contentOwner: AG
feature: Metadata
role: Business Practitioner,Administrator
translation-type: tm+mt
source-git-commit: 8093f6cec446223af58515fd8c91afa5940f9402
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 9%

---


# 如何编辑或添加元数据{#how-to-edit-or-add-metadata}

元数据是有关可搜索的资产的其他信息。 在您上传图像时，系统会自动提取该图像。 您可以编辑现有元数据或向现有字段添加新的元数据属性（例如，当元数据字段为空时）。

由于公司需要可控和可靠的元数据词汇表，[!DNL Experience Manager Assets]不允许临时添加新的元数据属性。 尽管作者无法为资产添加新的元数据字段，但开发人员可以。 请参阅[为资产创建新元数据属性](meta-edit.md#editing-metadata-schema)。

## 编辑资产{#editing-metadata-for-an-asset}的元数据

要编辑元数据：

1. 执行下列操作之一：

   * 在资产UI中，选择资产，然后单击/点按工具栏中的&#x200B;**[!UICONTROL 视图属性]**&#x200B;图标。
   * 从资产缩略图中，选择&#x200B;**[!UICONTROL 视图属性]**&#x200B;快速操作。
   * 在资产页面中，单击/点按工具栏中的&#x200B;**[!UICONTROL 视图属性]**。

   资产页面会显示资产的所有元数据。 此元数据在上传（摄入）到AEM Assets时会自动提取。

1. 根据需要，在各个选项卡下对元数据进行编辑，完成后，单击／点按工具栏中的 **[!UICONTROL 保存]** ，以保存更改。 单击／点 **[!UICONTROL 按关闭]** ，以返回到资产Web界面。

   >[!NOTE]
   >
   >如果文本字段为空，则没有现有的元数据集。 您可以在字段中输入一个值并保存它以添加该元数据属性。

对资产元数据所做的任何更改都会作为其XMP数据的一部分写回原始二进制文件。 这是通过AEM元数据回写工作流完成的。 对现有属性（如`dc:title`）所做的更改会被覆盖，新创建的属性（包括`cq:tags`等自定义属性）会与模式一起添加。

<!-- XMP write-back is supported and enabled for the platforms and file formats described in technical requirements. -->

## 编辑元数据模式{#editing-metadata-schema}

有关如何编辑元数据模式的详细信息，请参阅[编辑元数据模式表单](metadata-schemas.md#edit-metadata-schema-forms)。

## 在AEM {#registering-a-custom-namespace-within-aem}中注册自定义命名空间

您可以在AEM中添加您自己的命名空间。 正如有预定义的命名空间（如cq、jcr和sling）一样，您也可以对存储库元数据和xml处理进行命名空间。

1. 转到节点类型管理页&#x200B;*https://&lt;host>:&lt;port>/crx/explorer/nodetypes/index.jsp*。
1. 单击或点按页面顶部的&#x200B;**[!UICONTROL 命名空间]**。 命名空间管理页显示在窗口中。

1. 要添加命名空间，请单击或点按底部的&#x200B;**[!UICONTROL 新建]**。
1. 在XML命名空间约定中指定自定义命名空间（以URI形式指定ID以及ID的关联前缀），然后单击或点按&#x200B;**[!UICONTROL 保存]**。
