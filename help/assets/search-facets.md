---
title: 搜索 Facet.
description: 本文介绍如何在AEM中创建、修改和使用搜索彩块化。
translation-type: tm+mt
source-git-commit: 9c5dd93be316417014fc665cc813a0d83c3fac6f
workflow-type: tm+mt
source-wordcount: '2371'
ht-degree: 34%

---


# 搜索 Facet {#search-facets}

Adobe Experience Manager(AEM)资产在企业范围内进行部署，能够存储许多资产。 有时，如果您仅使用AEM的通用搜索功能，则查找正确的资产可能既困难又耗时。

使用“过滤器”面板中的搜索彩块化，为您的搜索体验添加更多粒度，并使搜索功能更高效、用途更广。 搜索彩块化可添加多个维度（谓词），使您能够执行更复杂的搜索。 过滤器面板包括一些标准彩块化。 您还可以添加自定义搜索彩块化。

总之，搜索彩块化允许您以多种方式而非按单一、预先确定的分类顺序搜索资产。 您可以轻松地向下展开到所需的详细级别，以便进行更集中的搜索。

例如，如果您要查找图像，则可以选择要位图还是矢量图像。 您可以通过为图像指定MIME类型进一步缩小搜索范围。 同样，在搜索文档时，可以指定格式，例如PDF或MS Word。

## 添加谓词 {#adding-a-predicate}

在过滤器面板中显示的搜索彩块化在基础搜索表单中使用谓词进行定义。 要显示更多或不同的彩块化，您可以向默认表单添加谓词，或使用包含您选择的彩块化的自定义表单。

对于全文搜索，请将谓 `Fulltext` 词添加到表单。 使用属性谓词可搜索与您指定的单个属性匹配的资产。 使用“选项”谓词，可搜索与特定属性的一个或多个值匹配的资产。 添加日期范围谓词，以搜索在指定日期范围内创建的资产。

1. 点按/单击 AEM 徽标，然后转到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 常规]** > **[!UICONTROL 搜索表单]**。
1. From the Search Forms page, select **[!UICONTROL Assets Admin Search Rail]**, then tap  **Edit** ![aemassets_edit](assets/aemassets_edit.png).

   ![找到并选择资产管理搜索边栏](assets/assets_admin_searchrail.png)

1. In the Edit Search Forms page, drag a predicate from the **[!UICONTROL Select Predicate]** tab to the main pane. For example, drag **[!UICONTROL Property Predicate]**.

   ![按并移动谓词以自定义搜索过滤器](assets/drag_predicate.png)

   *图： 按并移动谓词以自定义搜索过滤器。*

1. 在设置选项卡中，输入谓词的字段标签、占位符文本和说明。 为要与谓词关联的元数据属性指定有效名称。 设置选项卡中的标题标签标识所选谓词的类型。

   ![使用设置选项卡提供谓词的所需选项](assets/settings.png)

   *图： 使用设置选项卡提供谓词的所需选项。*

1. 在&#x200B;**[!UICONTROL 属性名称]**&#x200B;字段中，为要与谓词关联的元数据属性指定有效名称。该名称是执行搜索时所依据的名称。例如，输入 `jcr:content/metadata/dc:description` 或 `./jcr:content/metadata/dc:description`。也可以从选择对话框中选择现有节点。

   ![将元数据属性与属性名称字段中的谓词关联](assets/property_settings.png)

   *图： 将元数据属性与属性名称字段中的谓词关联。*

1. Click the **[!UICONTROL Preview]** ![preview](assets/preview.png) to generate a preview of the Filters panel as it appears after you add the predicate.
1. 在“预览”模式下查看谓词的布局。

   ![预览搜索表单，然后提交更改](assets/preview-1.png)

   预览搜索表单，然后提交更改

1. To close the preview, click the **[!UICONTROL Close]** ![close](assets/do-not-localize/close_icon.png) on the upper-right corner of the preview.
1. Tap **[!UICONTROL Done]** to save the settings.
1. 导航到资产用户界面中的搜索面板。 属性谓词已添加到该面板。
1. 在文本框中输入对要搜索的资产的描述。例如，输入“Adobe”。执行搜索时，其描述与“Adobe”匹配的资产便会列在搜索结果中。

## 添加“选项”谓词 {#adding-an-options-predicate}

“选项”谓词允许您在“过滤器”面板中添加多个搜索选项。 您可以在“过滤器”面板中选择一个或多个这些选项以搜索资产。 例如，要根据文件类型搜索资产，请在搜索表单中配置选项，如“图像”、“多媒体”、“文档”和“存档”。 配置这些选项后，当您在“过滤器”面板中选择“图像”选项时，将对GIF、JPEG、PNG等类型的资产执行搜索。

要将选项映射到相应的属性，请为选项创建节点结构，并在“选项”谓词的“属性名称”属性中提供父节点的路径。 The parent node should be of type `sling`: `OrderedFolder`. The options should be of type `nt:unstructured`. The option nodes should have the properties `jcr:title` and `value` configured.

The `jcr:title` property is a user-friendly name for the option that is displayed on the Filters panel. `value` 字段会用在查询中以匹配指定的属性。

当您选择一个选项时，会根据该选项节点及其子节点（如果有）的 `value` 属性来执行搜索。系统会遍历该选项节点下的整个树，并通过使用 OR 运算将每个子节点的 `value` 属性组合到一起，以构成搜索查询。

例如，如果您为文件类型选择“图像”，则资产的搜索查询将通过使用 OR 操作组合 `value` 属性来构建。For example, the search query for images is built by combining the results matched for *image/jpeg*, *image/gif*, *image/png*, *image/pjpeg*, and *image/tiff* for the property `jcr:content/metadata/dc:format` using an OR operation.

文件类型的值属性（如CRXDE中所示）用于搜索查询

您不必为 CRX 存储库中的选项手动创建节点结构，而是可以通过指定相应的键值对在 JSON 文件中定义选项。在&#x200B;**[!UICONTROL 属性名称]**&#x200B;字段中指定 JSON 文件的路径。例如，您可以定义键值对、`image/bmp`、`image/gif`、`image/jpeg` 和 `image/png`，并指定它们的值，如以下示例 JSON 文件中所示。在&#x200B;**[!UICONTROL 属性名称]**&#x200B;字段中，可以指定此文件的 CRX 路径。

```json
{
    "options" :
 [
          {"value" : "image/bmp","text" : "BMP"},
          {"value" : "image/gif","text" : "GIF"},
          {"value" : "image/jpeg","text" : "JPEG"},
          {"value" : "image/png","text" : "PNG"}
 ]
}
```

如果要使用现有节点，请使用选择对话框指定它。

>[!NOTE]
>
>“选项”谓词是一个自定义包装器，其中包含用于演示所描述行为的属性谓词。 目前，没有 REST 端点可在本机支持该功能。

1. Tap the AEM logo, and then go to **[!UICONTROL Tools > General > Search Forms]**.
1. 在“搜索 **[!UICONTROL 表单]** ”页面中，选择 **[!UICONTROL 资产管理员搜索边栏]**，然后点按编辑图标。
1. 在“编 **[!UICONTROL 辑搜索表单]** ”页中，将“选 **[!UICONTROL 项谓词]** ”从“选 **** 择谓词”选项卡拖至主窗格。
1. 在&#x200B;**[!UICONTROL 设置]**&#x200B;选项卡中，输入属性的标签和名称。例如，要根据资产的格式搜索资产，请为标签指定用户友好名称，例如&#x200B;**[!UICONTROL 文件类型]**。在属性字段中指定执行搜索时所依据的属性，例如 `jcr:content/metadata/dc:format.`
1. 执行下列操作之一：

   * In the **[!UICONTROL Property Name]** field, mention the path of the JSON file where you define the nodes for the options and specify corresponding key-value pairs.
   * 点 ![](assets/do-not-localize/aem_assets_add_icon.png) 按“选项”字段旁的，以指定要在“过滤器”面板中提供的选项的显示文本和值。 要添加其他选项，请点按／单 ![](assets/do-not-localize/aem_assets_add_icon.png) 击并重复该步骤。

1. 确保取消选中&#x200B;**[!UICONTROL 单选]**，以允许用户一次为文件类型选择多个选项（例如，“图像”、“文档”、“多媒体”和“存档”）。如果选中&#x200B;**[!UICONTROL 单选]**，则用户一次只能为文件类型选择一个选项。

   ![“选项”谓词中的可用字段](assets/options_predicate.png)

   “选项”谓词中的可用字段

1. 在&#x200B;**描述**&#x200B;字段中，输入可选描述，然后单击&#x200B;**[!UICONTROL 完成]**。
1. 导航到“搜索”面板。 “选项”谓词已添加到“搜 **索** ”面板。 “文件类型 **[!UICONTROL ”的选项]** 将显示为复选框。

## 添加多值属性谓词 {#adding-a-multi-value-property-predicate}

此谓 `Multi Value Property` 词允许您搜索多个值的资产。 请考虑一种情况，即您在AEM Assets中拥有多个产品的图像，并且每个图像的元数据包括与产品关联的SKU编号。 您可以使用此谓词根据多个SKU编号搜索产品图像。

1. 单击 AEM 徽标，然后转到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 常规]** > **[!UICONTROL 搜索表单]**。
1. 在“搜索表单”页面上，选 **[!UICONTROL 择资产管理搜索边栏]**，然后点 **按** 编 ![辑aemassets_edit](assets/aemassets_edit.png)。
1. 在“编辑搜索表单”页中，将&#x200B;**[!UICONTROL 多值属性谓词]**&#x200B;从&#x200B;**[!UICONTROL 选择谓词]**&#x200B;选项卡拖到主窗格。
1. In the **[!UICONTROL Settings]** tab, enter a label and placeholder text for the predicate. Specify the property name based on which the search is to be performed in the property field, for example `jcr:content/metadata/dc:value`. 您还可以使用选择对话框选择节点。
1. 确保选中&#x200B;**[!UICONTROL 分隔符支持]**。在&#x200B;**[!UICONTROL 输入分隔符]**&#x200B;字段中，指定要用于分隔各个值的分隔符。默认情况下，指定逗号为分隔符。您可以指定其他分隔符。
1. In the **Description** field, enter an optional description and then tap **[!UICONTROL Done]**.
1. 导航到 Assets 用户界面中的“过滤器”面板。**[!UICONTROL 多值属性]**&#x200B;谓词已添加到面板。
1. 在由分隔符分隔的“多值”字段中指定多个值并执行搜索。 此谓词将获取与您指定的值完全匹配的文本。

## 添加“标记”谓词 {#adding-a-tags-predicate}

此谓 `Tags` 词允许您对资产执行基于标记的搜索。 默认情况下，AEM Assets会根据您指定的标记搜索资产中的一个或多个标记匹配项。 换言之，搜索查询使用指定标记执行OR操作。 但是，您可以使用“匹配所有标记”选项来搜索包含您指定的所有标记的资产。

1. 单击 AEM 徽标，然后转到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 常规]** > **[!UICONTROL 搜索表单]**。
1. 在“搜索表单”页面中，选 **[!UICONTROL 择资产管理搜索边栏]** ，然后点 **按** 编 ![辑aemassets_edit](assets/aemassets_edit.png)。
1. In the Edit Search Form page, drag **[!UICONTROL Tags Predicate]** from the Select Predicate tab to the main pane.
1. 在设置选项卡中，输入谓词的占位符文本。 Specify the property name based on which the search is to be performed in the property field, for example `jcr:content/metadata/cq:tags`. 或者，也可以从选择对话框中选择CRXDE中的节点。
1. 配置此谓词的根标记路径属性，以在标记列表中填充各种标记。
1. 选择&#x200B;**[!UICONTROL 显示“匹配所有标记”选项]**，以搜索包含您指定的所有标记的资产。

   ![“标记”谓词的典型设置](assets/tags_predicate.png)

1. In the **[!UICONTROL Description]** field, enter an optional description and then click/tap **[!UICONTROL Done]**.
1. 导航到“搜索”面板。 The **[!UICONTROL Tags]** predicate is added to the Search panel.
1. 指定要根据其搜索资产或从建议列表中进行选择的标记。
1. Select **[!UICONTROL Match all]** to search for matches that include all tags that you specify.

## 添加其他谓词 {#adding-other-predicates}

按照与添加“属性”谓词或“选项”谓词相似的方法，您还可以将以下谓词添加到“搜索”面板：

<table>
 <tbody>
  <tr>
   <td><p><strong>谓词名称</strong></p> </td>
   <td><p><strong>描述</strong></p> </td>
   <td><p><strong>属性</strong></p> </td>
  </tr>
  <tr>
   <td><p>全文</p> </td>
   <td>此搜索谓词用于对整个资产节点执行全文搜索。 它映射为 <code>jcr</code>:<code>contains</code> 运算符。 如果要对资产节点的特定部分执行全文搜索，可以指定相对路径。</td>
   <td>
    <ul>
     <li>标签</li>
     <li>占位符</li>
     <li>属性名称</li>
     <li>描述</li>
    </ul> </td>
  </tr>
  <tr>
   <td>路径浏览器</td>
   <td>此搜索谓词用于在预配置的根路径中搜索文件夹和子文件夹中的资产</td>
   <td>
    <ul>
     <li>占位符</li>
     <li>根路径</li>
     <li>描述</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>路径</p> </td>
   <td><p>使用它按位置筛选结果。 可以指定不同的路径作为选项。</p> </td>
   <td>
    <ul>
     <li>标签</li>
     <li>路径</li>
     <li>描述</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>发布状态</p> </td>
   <td><p>此搜索谓词用于根据资产的发布状态搜索资产</p> </td>
   <td>
    <ul>
     <li>标签</li>
     <li>属性名称</li>
     <li>描述</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>相对日期</p> </td>
   <td><p>此搜索谓词用于根据创建资产的相对日期搜索资产. 例如，您可以配置选项，如2个月前、3周前等。 </p> </td>
   <td>
    <ul>
     <li>标签</li>
     <li>属性名称</li>
     <li>相对日期</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>范围</p> </td>
   <td><p>此搜索谓词用于搜索特定范围内的资产。在“搜索”面板中，可以指定范围的最小值和最大值。</p> </td>
   <td>
    <ul>
     <li>标签</li>
     <li>属性名称</li>
     <li>描述</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>日期范围</p> </td>
   <td><p>此搜索谓词用于搜索在日期属性的指定范围内创建的资产。在“搜索”面板中，您可以使用日期选择器指定开始和结束日期。</p> </td>
   <td>
    <ul>
     <li>标签</li>
     <li>占位符</li>
     <li>属性名称</li>
     <li>范围文本（始于）</li>
     <li>范围文本（止于）</li>
     <li>描述</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>日期</p> </td>
   <td><p>此搜索谓词用于根据日期属性进行基于滑块的资产搜索。</p> </td>
   <td>
    <ul>
     <li>标签</li>
     <li>属性名称</li>
     <li>描述</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>文件大小</p> </td>
   <td><p>此搜索谓词用于根据资产的大小搜索资产. 它是基于滑块的谓词，您可以从可配置节点中选择滑块选项。 默认选项在CRX存储库中的/libs/dam/options/predicates/filesize中定义。 文件大小以字节为单位提供。</p> </td>
   <td>
    <ul>
     <li>标签</li>
     <li>属性名称</li>
     <li>路径</li>
     <li>描述</li>
    </ul> </td>
  </tr>
  <tr>
   <td>上次修改的资源</td>
   <td>此搜索谓词用于搜索最近修改的资产 </td>
   <td>
    <ul>
     <li>属性名称</li>
     <li>属性值</li>
     <li>描述</li>
    </ul> </td>
  </tr>
  <tr>
   <td>发布状态</td>
   <td>此搜索谓词用于根据资产的发布状态搜索资产 </td>
   <td>
    <ul>
     <li>标签</li>
     <li>属性名称</li>
     <li>描述</li>
    </ul> </td>
  </tr>
  <tr>
   <td>评级</td>
   <td>此搜索谓词用于根据资产的平均评级搜索资产 </td>
   <td>
    <ul>
     <li>标签</li>
     <li>属性名称</li>
     <li>选项路径</li>
     <li>描述</li>
    </ul> </td>
  </tr>
  <tr>
   <td>到期状态</td>
   <td>此搜索谓词用于根据资产的到期状态搜索资产 </td>
   <td>
    <ul>
     <li>标签</li>
     <li>属性名称</li>
     <li>描述</li>
    </ul> </td>
  </tr>
  <tr>
   <td>隐藏</td>
   <td>此搜索谓词用于定义用于搜索资产的隐藏字段属性</td>
   <td>
    <ul>
     <li>属性名称</li>
     <li>属性值</li>
     <li>描述</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## 恢复默认搜索彩块化 {#restoring-default-search-facets}

默认情况下，“搜索表单”页面的“资 **[!UICONTROL 产管理员搜索边栏]** ”前会 **[!UICONTROL 显示一个锁图标]** 。 如果您向该表单中添加搜索彩块化，该锁图标便会消失，以指示默认表单已被修改。

“搜索表单”页面上某个选项的锁图标表示默认设置保持不变且未进行自定义。

要恢复默认搜索彩块化，请执行以下步骤：

1. 在“搜 **[!UICONTROL 索表单”页面中]** ，选择 **[!UICONTROL “资产管理员]** ”。
1. 点按 **[!UICONTROL 工]** 具栏 ![](assets/do-not-localize/deleteoutline.png) 中的删除图标。
1. 在确认对话框中，点按 **[!UICONTROL 删除]** ，以删除自定义更改。

   在删除对搜索彩块化的自定义更改后，“搜索表单”页面中的“资 **[!UICONTROL 产管理员搜索边栏]** ”前会重 **[!UICONTROL 新显示锁图标]** 。

## 用户权限 {#user-permissions}

如果您没有分配管理员角色，则您需要执行编辑、删除和预览操作（涉及搜索彩块化）的列表权限。

| 操作 | 权限 |
|---|---|
| 编辑 | Read and write permissions on the `/apps` node in CRX. |
| 删除 | Read, write, and delete permissions on the `/apps` node in CRX. |
| 预览 | Read, write, and delete permissions on the `/var/dam/content` node in CRX. Also, Read and write permissions on `/apps` node. |

>[!MORELIKETHIS]
>
>* [搜索数字资产](search-assets.md)。

