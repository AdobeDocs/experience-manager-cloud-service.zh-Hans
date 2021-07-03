---
title: 如何编辑或添加元数据
description: 了解 [!DNL Experience Manager Assets] 中的资产元数据，以及编辑资产元数据的各种方式。
contentOwner: AG
feature: 元数据
role: User,Admin
exl-id: 464a97ce-da3e-47b5-9879-fafaf2f2378c
source-git-commit: a2c2a1f4ef4a8f0cf1afbba001d24782a6a2a24e
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 9%

---

# 如何编辑或添加元数据 {#how-to-edit-or-add-metadata}

元数据是有关可搜索资产的其他信息。 在您上传图像时，系统会自动提取该图像。 您可以编辑现有元数据或向现有字段添加新元数据属性（例如，当元数据字段为空时）。

由于公司需要可控且可靠的元数据词汇，因此[!DNL Experience Manager Assets]不允许临时添加新的元数据属性。 尽管作者无法为资产添加新的元数据字段，但开发人员可以。 请参阅[为资产创建新元数据属性](meta-edit.md#editing-metadata-schema)。

## 编辑资产的元数据 {#editing-metadata-for-an-asset}

要编辑元数据，请执行以下操作：

1. 执行下列操作之一：

   * 从资产UI中，选择资产，然后单击/点按工具栏中的&#x200B;**[!UICONTROL 查看属性]**&#x200B;图标。
   * 从资产缩略图中，选择&#x200B;**[!UICONTROL 查看属性]**&#x200B;快速操作。
   * 在资产页面中，单击/点按工具栏中的&#x200B;**[!UICONTROL 查看属性]** 。

   资产页面会显示资产的所有元数据。 此元数据在上传（摄取）到AEM Assets后会自动提取。

1. 根据需要，在各个选项卡下对元数据进行编辑，完成后，单击／点按工具栏中的 **[!UICONTROL 保存]** ，以保存更改。 单击／点 **[!UICONTROL 按关闭]** ，以返回到资产Web界面。

   >[!NOTE]
   >
   >如果文本字段为空，则不存在现有的元数据集。 您可以在字段中输入一个值，然后进行保存以添加该元数据属性。

对资产元数据所做的任何更改都会作为资产数据的一部分写回原始二进制文件。 这是通过AEM元数据回写工作流完成的。 对现有属性（如`dc:title`）所做的更改会被覆盖，新创建的属性（包括自定义属性，如`cq:tags`）会与架构一起添加。

<!-- XMP write-back is supported and enabled for the platforms and file formats described in technical requirements. -->

## 编辑元数据架构 {#editing-metadata-schema}

有关如何编辑元数据架构的详细信息，请参阅[编辑元数据架构表单](metadata-schemas.md#edit-metadata-schema-forms)。

## 在AEM中注册自定义命名空间 {#registering-a-custom-namespace-within-aem}

您可以在AEM中添加自己的命名空间。 正如存在预定义的命名空间（如cq、jcr和sling）一样，您也可以拥有用于存储库元数据和xml处理的命名空间。

1. 转到节点类型管理页面&#x200B;*https://&lt;host>:&lt;port>/crx/explorer/nodetypes/index.jsp*。
1. 单击或点按页面顶部的&#x200B;**[!UICONTROL 命名空间]**。 命名空间管理页面显示在窗口中。

1. 要添加命名空间，请单击或点按底部的&#x200B;**[!UICONTROL New]**。
1. 在XML命名空间约定中指定自定义命名空间（以URI的形式指定ID以及该ID的关联前缀），然后单击或点按&#x200B;**[!UICONTROL Save]**。
