---
title: 级联元数据
description: 本文介绍了如何在资源视图中定义资源的级联元数据。
feature: Metadata
role: Admin, User
source-git-commit: 2bb309afc372fe18ce274a2813ed25cba22eb4de
workflow-type: tm+mt
source-wordcount: '1214'
ht-degree: 5%

---


# 级联元数据Assets视图{#cascading-metadata-assets-view}

在捕获资源的元数据信息时，用户在各种可用字段中提供信息。 您可以根据在其他字段中选择的选项，显示特定的元数据字段或字段值。 此类元数据的条件显示称为层叠元数据。 换言之，您可以在特定元数据字段/值与一个或多个字段和/或其值之间创建依赖关系。

使用元数据Forms定义用于显示层叠元数据的规则。 例如，如果您的元数据表单包含资产类型字段，则可以根据用户选择的资产类型定义要显示的相关字段集。

以下是您可以定义层叠元数据的一些用例：

* 在需要用户位置时，根据用户选择的国家和州显示相关城市名称。
* 根据用户选择的产品类别，在列表中加载相关品牌名称。
* 根据在另一个字段中指定的值切换特定字段的可见性。 例如，如果用户希望以不同的地址交付装运，则显示单独的装运地址字段。
* 根据在另一个字段中指定的值将某个字段指定为必填字段。
* 根据在另一个字段中指定的值更改为特定字段显示的选项。
* 根据在其他字段中指定的值在特定字段中设置默认元数据值。

>[!IMPORTANT]
>
>级联元数据功能作为有限可用性功能提供。 您可以[创建并提交 Adobe 客户支持案例](https://helpx.adobe.com/cn/enterprise/using/support-for-experience-cloud.html)，为您的部署启用该功能。

## 在[!DNL Experience Manager]中配置级联元数据 {#configure-cascading-metadata-in-aem}

考虑一个方案，其中您要根据所选资源的类型显示层叠元数据。 例如 — 

* 对于视频，显示适用的字段，例如格式、编解码器、持续时间等。
* 对于Word或PDF文档，显示字段，例如页数、作者等。

我们使用名为`Image`的下拉字段作为示例，根据文件的图像类型对文件进行分类。 下拉列表包含表示受支持的图像扩展的选项(例如JPG/JPEG、GIF等)。 为确保数据一致性并防止选择或处理不支持的格式，将对此字段应用验证规则。 该规则将评估所选的下拉值，并强制实施与接受的图像格式一致的约束。

>[!IMPORTANT]
>
>您只能基于下拉字段创建规则。

无论选择的资产类型如何，都会将版权信息显示为必填字段。 您可以使用[预定义的元数据组件](metadata-assets-view.md#property-components)和[将元数据分配给文件夹](metadata-assets-view.md#assign-metadata-form-folder)。

### 生成元数据Forms {#build-metadata-schema-forms}

请考虑执行以下步骤以创建新的元数据表单：

1. 选择[!DNL Experience Manager]徽标，然后转到&#x200B;**[!UICONTROL 设置]** > **[!UICONTROL 元数据Forms]** > **[!UICONTROL 创建]**。

1. 从&#x200B;**[!UICONTROL 类型]**&#x200B;下拉列表中，选择适当的表单类型：**[!UICONTROL 文件]**、**[!UICONTROL 文件夹]**&#x200B;或&#x200B;**[!UICONTROL 收藏集]**。

1. 在&#x200B;**[!UICONTROL 名称]**&#x200B;字段中指定元数据表单的标题。

1. 或者，从&#x200B;**[!UICONTROL 从现有表单模板选择]**&#x200B;下拉列表中选择现有元数据表单模板。

1. 出现一个空白的元数据表单。 添加新选项卡。

   ![元数据表单UI](assets/metadata-form-ui.png)

   * **A：**&#x200B;在[!UICONTROL 编辑]或[!UICONTROL 预览]之间切换
   * **B：** [元数据表单的组件](metadata-assets-view.md#property-components)
   * **C：**&#x200B;切换到其他元数据表单
   * **D：**&#x200B;添加新选项卡
   * **E：**&#x200B;画布
   * **F：**&#x200B;选定组件的常规设置
   * **G：**&#x200B;规则选项卡
   * **H：**&#x200B;组件属性

观看本视频以查看步骤顺序，[设置元数据Forms](https://video.tv.adobe.com/v/341275)。

### 修改现有元数据表单 {#modify-existing-metadata-form}

要修改现有元数据表单，请执行以下步骤：

1. 打开现有的元数据表单，然后导航到要添加到该表单中的[预定义组件](metadata-assets-view.md#property-components)，并将元素拖放到画布上。

   根据&#x200B;**图像**&#x200B;用例，添加下拉字段以定义图像资源类型。 在&#x200B;**设置**&#x200B;中指定名称和属性路径，并可以选择将该字段配置为&#x200B;**[!UICONTROL 只读]**&#x200B;或&#x200B;**[!UICONTROL 多项选择]**。

1. 通过手动输入键值选项、指定JSON路径或导入CSV文件，为下拉列表提供键值选项。

   * 要手动指定值，请选择&#x200B;**[!UICONTROL 选择]**&#x200B;下的&#x200B;**[!UICONTROL 手动添加]**，然后单击`Add`并指定选项标签和值。 例如，指定视频、PDF和图像资源类型。

     ![图像资源类型](assets/image-asset-type.png)

   * 要从JSON路径获取值，请选择&#x200B;**[!UICONTROL 通过JSON路径添加]**&#x200B;并指定JSON文件的路径。

     >[!NOTE]
     >
     >确保将JSON文件存储在所有DAM编辑器和作者都可访问的共享位置。

     ![通过JSON路径添加选项](assets/add-json-choices.png)

   * 要动态获取CSV中的值，请单击&#x200B;**[!UICONTROL 导入CSV]**&#x200B;并提供CSV文件的路径。 [!DNL Experience Manager]在将表单呈现给用户时实时获取键值对。

     ![通过CSV添加选项](assets/import-csv-choices.png)

   >[!NOTE]
   > 
   >您无法从CSV文件导入选项并手动编辑它们，因为这两个选项是互斥的。

1. 若要在“图像”字段和其他字段之间创建依赖关系，请选择依赖字段并打开&#x200B;**[!UICONTROL 规则]**&#x200B;选项卡。 每个组件都支持一组特定的规则。 对于此用例，可使用图像资源类型选项来定义规则逻辑。

   <!--![Image Asset Type Rule](assets/image-asset-type-rule.png)-->

   <!--![rule tab](assets/rule-tab.png)-->

1. 在&#x200B;**[!UICONTROL 必需]**&#x200B;下，根据新规则&#x200B;**[!UICONTROL 选项选择]**&#x200B;必需。 单击![加号图标](assets/do-not-localize/aem_assets_add_icon.png)以添加新规则。

   ![规则](assets/image-required-rule1.png)

   在当前用例中，当图像资源格式为JPG/JPEG、PNG、GIF、TIFF或WEBP时，需要资源类型字段。 此外，单击![编辑图标](assets/do-not-localize/edit.svg)以重新定义规则，或单击![删除图标](assets/do-not-localize/delete.svg)以删除定义的规则。

   ![规则](assets/image-required-rule2.png)

1. 在&#x200B;**[!UICONTROL 可见性]**&#x200B;下，根据新规则&#x200B;**[!UICONTROL 选项选择]**&#x200B;可见。 单击![加号图标](assets/do-not-localize/aem_assets_add_icon.png)以添加新规则。

   >[!NOTE]
   >
   >您可以应用&#x200B;**[!UICONTROL 要求]**&#x200B;条件和&#x200B;**[!UICONTROL 可见性]**&#x200B;条件，二者相互独立。

   ![规则](assets/image-visible-rule1.png)

   在当前用例中，当图像资源格式为JPG/JPEG、PNG或GIF时，资源类型字段可见。 此外，单击![编辑图标](assets/do-not-localize/edit.svg)以重新定义规则，或单击![删除图标](assets/do-not-localize/delete.svg)以删除定义的规则。

   ![规则](assets/image-visible-rule2.png)

1. 选择&#x200B;**[!UICONTROL 基于规则]**&#x200B;的选择以创建依赖项并定义规则。 单击![加号图标](assets/do-not-localize/aem_assets_add_icon.png)以添加新规则。

   ![规则](assets/image-choices-rule1.png)

   要为资源类型下拉列表配置基于规则的选择，请创建一个规则并将图像设置为依赖字段。 然后，通过为JPG/JPEG、PNG、GIF和TIFF选择“图像”，并为WEBP选择“视频”，定义每种图像格式的显示值，确保只检查每种格式的预期值以动态显示相关选项。 此外，单击![编辑图标](assets/do-not-localize/edit.svg)以重新定义规则，或单击![删除图标](assets/do-not-localize/delete.svg)以删除定义的规则。

   ![规则](assets/image-choices-rule2.png)

1. 同样，重复这些步骤以在[!UICONTROL Asset Type]字段中的其他资源(如PDF和Word)与字段（如[!UICONTROL Page Count]和[!UICONTROL Author]）之间建立依赖关系。

1. 单击&#x200B;**[!UICONTROL 保存]**。将元数据表单应用到文件夹。

1. 导航到将元数据表单应用到的文件夹，然后打开资源的属性页面。 根据您在“资产类型”字段中的选择，将显示相关的级联元数据字段。

   ![级联元数据表单输出](assets/cascading-metadata-form-output.png)

>[!NOTE]
> 
>若要提前访问Assets视图帐户上的层叠元数据，请[创建并提交Adobe客户支持案例](https://helpx.adobe.com/cn/enterprise/using/support-for-experience-cloud.html)。

## 后续步骤 {#next-steps}

* [观看视频，了解如何在Assets视图中管理元数据表单](https://experienceleague.adobe.com/docs/experience-manager-learn/assets-essentials/configuring/metadata-forms.html?lang=zh-Hans)

* 利用资源视图用户界面上的[!UICONTROL 反馈]选项提供产品反馈

* 通过右侧边栏中的[!UICONTROL 编辑此页面]![编辑页面](assets/do-not-localize/edit-page.png)或[!UICONTROL 记录问题]![创建 GitHub 问题](assets/do-not-localize/github-issue.png)来提供文档反馈

* 联系[客户关怀团队](https://experienceleague.adobe.com/zh-hans?support-solution=General#support)

