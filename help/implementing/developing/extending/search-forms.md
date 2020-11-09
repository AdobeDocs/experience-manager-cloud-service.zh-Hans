---
title: 配置搜索表单
description: 将搜索Forms作为Cloud Service。
translation-type: tm+mt
source-git-commit: 23349f3350631f61f80b54b69104e5a19841272f
workflow-type: tm+mt
source-wordcount: '2030'
ht-degree: 15%

---


# 配置搜索表单 {#configuring-search-forms}

Adobe Experience Manager作为Cloud Service，拥有强大的 [搜索](/help/sites-cloud/authoring/getting-started/search.md) 机制。

此外，还有一组预定义选项可帮助您筛选内容。 这些方面包含预定义 **的彩块化**，如 **修改日期**、发布状态 **或Live Copy状态** ，以帮助您快速细化到所需的资源。

![搜索和筛选使用情况](assets/csf-usage.png)

这些目标是帮助您快速轻松地从以下位置找到内容：

* [搜索和筛选](/help/sites-cloud/authoring/getting-started/search.md#search-and-filter)
* [边栏选择器](/help/sites-cloud/authoring/getting-started/basic-handling.md#rail-selector)
* 资产 [浏览器](/help/sites-cloud/authoring/fundamentals/environment-tools.md#assets-browser) （编辑页面时）

>[!NOTE]
>
>您可以配置基础内 [容搜索和索引服务](/help/operations/indexing.md) 。

使用 **搜索Forms**，您可以根据您的特定需求自定义和扩展这些面板。

搜 **索Forms** (Search Section Medias [)提供现成的谓词选](#predicates-and-their-settings) 项，您可以组合和定义。 配置 [这些表单的对话框](#configuring-your-search-forms) ，可通过以下方式访问：

* **工具**

   * **常规**

      * **搜索表单**

## 默认Forms {#default-forms}

首次访问“搜索 **Forms** ”控制台时，您可以看到所有配置都有挂锁符号。 这表示相应的配置是默认（现成）配置——无法删除。 在您自定义并保存后，锁定将消失。 删除自定义配 [置时，它将重新](#deleting-a-configuration-to-reinstate-the-default)显示，此时将恢复默认配置（和挂锁指示符）。

![配置搜索表单概述](assets/csf-overview.png)

可用的默认配置（按字母顺序列出）包括：

* **资产管理员搜索边栏:**

* **页面编辑器(文档搜索):**

* **页面编辑器（体验片段搜索）:**

* **页面编辑器（图像搜索）:**

* **页面编辑器（手稿搜索）:**

* **页面编辑器（页面搜索）:**

* **页面编辑器（段落搜索）:**

* **页面编辑器（产品搜索）:**

* **页面编辑器(Scene7搜索**):

* **页面编辑器（视频搜索）**:

* **项目管理员搜索边栏:**

* **项目翻译搜索边栏:**

* **站点管理员搜索边栏**:

* **代码片段管理员搜索边栏**:

* **Stock 管理员搜索边栏**:

>[!NOTE]
>
>有关与资产相关的搜索表单的更多详细信息，请 [参阅资产——搜索彩块化](/help/assets/search-facets.md)


## 谓词及其设置 {#predicates-and-their-settings}

### 谓词 {#predicates}

以下谓词可用，具体取决于配置：

<table>
 <tbody>
  <tr>
   <th>谓词</th>
   <th>用途</th>
   <th>设置</th>
  </tr>
  <tr>
   <td>分析</td>
   <td>显示以分析为后盾的数据时，站点浏览器中的搜索／过滤功能。 分析搜索过滤器加载以匹配映射的自定义分析列。</td>
   <td>
    <ul>
     <li>字段标签</li>
     <li>描述</li>
    </ul> </td>
  </tr>
  <tr>
   <td>批准状态</td>
   <td>根据批准状态进行搜索。</td>
   <td>
    <ul>
     <li>字段标签</li>
     <li>属性名称*</li>
     <li>描述</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>作者</td>
   <td>根据作者进行搜索。</td>
   <td>
    <ul>
     <li>占位符</li>
     <li>属性名称*</li>
     <li>描述</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>签出方</td>
   <td>搜索特定用户签出的资产。</td>
   <td>
    <ul>
     <li>字段标签</li>
     <li>占位符</li>
     <li>描述</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>签出状态</td>
   <td>搜索具有特定结帐状态的资产。</td>
   <td>
    <ul>
     <li>字段标签</li>
     <li>属性名称*</li>
     <li>描述</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>组件</td>
   <td>允许作者搜索／筛选具有特定组件的页面。 For example an image gallery.<br /> </td>
   <td>
    <ul>
     <li>占位符</li>
     <li>属性名称*</li>
     <li>属性深度</li>
     <li>描述</li>
    </ul> </td>
  </tr>
  <tr>
   <td>日期范围</td>
   <td>搜索在日期属性的指定范围内创建的资源。 在“搜索”面板中，可以指定开始日期和结束日期。</td>
   <td>
    <ul>
     <li>字段标签</li>
     <li>占位符</li>
     <li>属性名称*</li>
     <li>范围文本（自）*</li>
     <li>范围文本（收件人）*</li>
     <li>描述</li>
    </ul> </td>
  </tr>
  <tr>
   <td>到期状态</td>
   <td>根据到期状态搜索资源。</td>
   <td>
    <ul>
     <li>字段标签</li>
     <li>属性名称*</li>
     <li>描述</li>
    </ul> </td>
  </tr>
  <tr>
   <td>文件大小</td>
   <td>根据资源的大小筛选资源。</td>
   <td>
    <ul>
     <li>字段标签</li>
     <li>属性名称*</li>
     <li>选项路径</li>
     <li>描述</li>
    </ul> </td>
  </tr>
  <tr>
   <td>文件类型</td>
   <td>根据文件/MIME类型搜索资产。</td>
   <td>
    <ul>
     <li>字段标签</li> 
     <li>属性名称*</li>
     <li>Mime 类型路径</li>
     <li>描述</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>全文</td>
   <td>此搜索谓词用于进行全文搜索. 它映射为“jcr:contains´”运算符。</td>
   <td>
    <ul>
     <li>占位符</li>
     <li>属性名称</li>
     <li>描述</li>
    </ul> </td>
  </tr>
  <tr>
   <td>组</td>
   <td>组的搜索谓词（仅在“分析谓词”中使用）。</td>
   <td>
    <ul>
     <li>字段标签</li>
     <li>描述</li>
    </ul> </td>
  </tr>
  <tr>
   <td>隐藏的筛选器</td>
   <td>属性和值的过滤器，用户不可见。</td>
   <td>
    <ul>
     <li>属性名称*</li>
     <li>属性值*</li>
     <li>描述</li>
    </ul> </td>
  </tr>
  <tr>
   <td>分析</td>
   <td>根据一系列Insights参数进行搜索。</td>
   <td>这是一个由多个谓词组成的复杂谓词：
    <ul>
     <li>组</li>
     <li>范围</li>
     <li>选项</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>集合成员</td>
   <td>搜索属于收藏集成员的资产</td>
   <td>
    <ul>
     <li>描述</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>多值属性</td>
   <td>搜索指定属性的多个值。</td>
   <td>
    <ul>
     <li>字段标签</li>
     <li>占位符</li>
     <li>属性名称*</li>
     <li>分隔符支持</li>
     <li>输入分隔符</li>
     <li>忽略大小写</li>
     <li>描述</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>选项</td>
   <td><p>这些选项是用户创建的内容节点。</p> <p>有关 <a href="#addinganoptionspredicate">详细信息，请参阅</a> “添加选项谓词”。</p> </td>
   <td>
    <ul>
     <li>字段标签</li>
     <li>属性名称*</li>
     <li>单选</li>
     <li>添加选项</li>
     <li>手动</li>
     <li>描述</li>
    </ul> </td>
  </tr>
  <tr>
   <td>选项属性</td>
   <td>搜索选项的一个或多个属性。</td>
   <td>
    <ul>
     <li>字段标签</li>
     <li>属性名称*</li>
     <li>选项节点路径</li>
     <li>属性深度</li>
     <li>单选</li>
     <li>描述</li>
    </ul> </td>
  </tr>
  <tr>
   <td>页面 状态</td>
   <td>根据页面状态筛选页面。</td>
   <td>
    <ul>
     <li>字段标签</li>
     <li>发布属性名称*</li>
     <li>锁定的页面属性名称*</li>
     <li>描述</li>
    </ul> </td>
  </tr>
  <tr>
   <td>路径</td>
   <td>根据特定路径进行筛选。 可以指定多个路径作为选项。</td>
   <td>
    <ul>
     <li>字段标签</li>
     <li>添加搜索路径</li>
     <li>描述</li>
    </ul> </td>
  </tr>
  <tr>
   <td>路径浏览器</td>
   <td>提供一个路径浏览器以在预定义的根路径下进行搜索。</td>
   <td>
    <ul>
     <li>占位符</li>
     <li>根路径</li>
     <li>描述</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>隐藏路径</td>
   <td>路径上的过滤器，用户不可见。</td>
   <td>
    <ul>
     <li>属性名称(`path`)</li>
     <li>属性值(`/content/dam`)</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>属性</td>
   <td>搜索指定的属性。</td>
   <td>
    <ul>
     <li>字段标签</li>
     <li>占位符</li>
     <li>属性名称</li>
     <li>部分搜索</li>
     <li>忽略大小写</li>
     <li>描述</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>发布状态</td>
   <td>根据资源的发布状态筛选资源。</td>
   <td>
    <ul>
     <li>字段标签</li>
     <li>属性名称*</li>
     <li>描述</li>
    </ul> </td>
  </tr>
  <tr>
   <td>范围</td>
   <td>搜索位于指定范围内的资源。 在“搜索”面板中，可以指定范围的最小值和最大值。</td>
   <td>
    <ul>
     <li>字段标签</li>
     <li>属性名称*</li>
     <li>描述</li>
    </ul> </td>
  </tr>
  <tr>
   <td>评级</td>
   <td>根据资源的平均等级搜索资源。<br /> </td>
   <td>
    <ul>
     <li>字段标签</li>
     <li>属性名称*</li>
     <li>选项路径</li>
     <li>描述</li>
    </ul> </td>
  </tr>
  <tr>
   <td>相对日期</td>
   <td>根据资源创建的相对日期筛选资源。 例如，1周前，1个月前。</td>
   <td>
    <ul>
     <li>字段标签</li>
     <li>属性名称*</li>
     <li>相对日期</li>
     <li>描述</li>
    </ul> </td>
  </tr>
  <tr>
   <td>滑块范围</td>
   <td>使用滑块功能扩展范围谓词的通用搜索谓词。 搜索的属性的值必须介于滑块限制之间。</td>
   <td>
    <ul>
     <li>字段标签</li>
     <li>属性名称*</li>
     <li>选项节点路径</li>
     <li>描述</li>
    </ul> </td>
  </tr>
  <tr>
   <td>状态</td>
   <td>根据批准和结帐状态进行搜索。</td>
   <td>这是一个由多个谓词组成的复杂谓词：
    <ul>
     <li>批准状态</li>
     <li>签出状态</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>标记</td>
   <td>根据标记进行搜索。</td>
   <td>
    <ul>
     <li>Field Lavel</li>
     <li>占位符</li>
     <li>属性名称*</li>
     <li>显示匹配所有标记选项</li>
     <li>根标记路径</li>
     <li>描述</li>
    </ul> </td>
  </tr>
  <tr>
   <td>模板</td>
   <td>根据所选模板进行搜索。</td>
   <td>
    <ul>
     <li>占位符</li>
     <li>属性名称*</li>
     <li>描述</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>翻译状态</td>
   <td>根据翻译状态进行搜索。</td>
   <td>
    <ul>
     <li>字段标签</li>
    </ul> 
   </td>
  </tr>
 </tbody>
</table>

<!--
  <tr>
   <td>Date ???</td>
   <td>Slider-based search of assets based on a date property.</td>
   <td>
    <ul>
     <li>Field Label</li>
     <li>Property Name*</li>
     <li>Description</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Asset Last Modified ?????</td>
   <td>Date the asset was last modified.<br /> </td>
   <td>A customized predicate, based on the Date Predicate.</td>
  </tr>
  <tr>
   <td>Range Options ???</td>
   <td>A specific search predicate for Assets and the same as common Slider Predicate. Is still available due to backward compatibilty issues.</td>
   <td>
    <ul>
     <li>Field Label</li>
     <li>Property Name*</li>
     <li>Option Path</li>
     <li>Description</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Tag </td>
   <td>Search assets based on tags. You can configure the Path property to populate various tags in the Tags list.</td>
   <td>
    <ul>
     <li>Field Label</li>
     <li>Property Name*</li>
     <li>Option Path</li>
     <li>Description</li>
    </ul> </td>
  </tr>
-->

>[!NOTE]
>
>常用搜索谓词在以下位置进行定义：
>  `/libs/cq/gui/components/common/admin/customsearch/searchpredicates`
>
>此信息仅供参考，您不得对进行更改 `/libs`。

<!--
>* Search predicates related only to siteadmin (classic UI) are located under:
> `/libs/cq/gui/components/siteadmin/admin/searchpanel/searchpredicates`
>   * These are deprecated and only available for backward compatibility.
>
-->

### 谓词设置 {#predicate-settings}

根据谓词，可以选择一些设置进行配置，包括：

* **字段标签**

   将显示为可折叠标题或谓词字段标签的标签。

* **描述**

   用户的描述性详细信息。

* **占位符**

   如果未输入过滤文本，则为空文本或谓词的占位符。

* **属性名称**

   要搜索的属性。 它使用相对路径，通配符 `*/*/*` 指定属性相对于节点的深度(每个星 `jcr:content` 号表示一个节点级别)。

   如果只想在具有该节点上的属性的资源的一级子节点 `x` 上进行搜 `jcr:content` 索，则 `*/jcr:content/x`

* **属性深度**

   在资源中搜索该属性的最大深度。 因此，可以对资源和递归子项执行对该属性的搜索，直到子项的级别等于指定的深度。

* **属性值**

   属性值作为绝对字符串或作为表达式语言；例如， `cq:Page` 或

   `${empty requestPathInfo.suffix ? "/content" : requestPathInfo.suffix}`。

* **范围文本**

   “日期范围”谓词中的范围字 **段的标签** 。

* **选项路径**

   用户可以使用谓词设置选项卡中的路径浏览器选择路径。 选择+图 **标后** ，将选择添加到有效选项的列表中(然后 **使用——图标根据需要** 删除)。

   这些选项是用户创建的内容节点，其结构如下：

   `(jcr:primaryType = nt:unstructured, value (String), jcr:title (String))`

* **选项节点路**&#x200B;径与 
**选项路径**，只有此路径位于通用谓词字段中，而另一个路径则特定于资产。

* **单选**&#x200B;如果选中，选项将呈现为复选框，仅允许单选。 如果错误地选中了复选框，则可取消选中该复选框。

* **发布和Live Copy属性名称特**&#x200B;定站点谓词的发布和Live Copy复选框的标签。

* &amp;ast;在“设置”选项卡的 **字段** 标签中，表示字段为必填字段，如果留空，则将显示错误消息。

## 配置搜索Forms {#configuring-your-search-forms}

### 创建／打开自定义配置 {#creating-opening-a-customized-configuration}

1. 导航到 **工具**、 **常规**、搜 **索Forms**。

1. 选择要自定义的配置。
1. 使用编 **辑** 图标打开要更新的配置。
1. 如果是新的自定义，您可能想要 [添加新的谓词字段并根据需要](#add-edit-a-predicate-field-and-define-field-settings) 定义设置。 如果是现有自定义，则可以选择现有字段并 [更新设置](#add-edit-a-predicate-field-and-define-field-settings)。
1. Select **Done** to save the configuration. 您的更改可以在下次使用配置时看到。

   >[!NOTE]
   >
   >自定义配置存储在（视情况而定）下：
   >
   >* `/apps/cq/gui/content/facets/<option>`
   >* `/apps/commerce/gui/content/facets/<option>`


### 添加／编辑谓词字段和定义字段设置 {#add-edit-a-predicate-field-and-define-field-settings}

您可以添加或编辑字段，并定义／更新其设置：

1. [打开要更新的自定](#creating-opening-a-customized-configuration) 义配置。
1. 如果要添加新字段，请打开“选 **择谓词** ”选项卡，并将所需的谓词拖动到所需位置。 例如，日期 **范围谓词**:

   ![添加谓词](assets/csf-add-predicate.png)

1. 取决于：

   * 您正在添加新字段：

      添加谓词后，将 **打开** “设置”选项卡并显示可定义的属性。

   * 您要更新现有谓词：

      选择谓词字段（在右侧），然后打开“设 **置** ”选项卡。
   例如，日期范围谓词 **的设置**:

   ![修改谓词](assets/csf-modify-predicate.png)

1. 根据需要进行更改，然后单击“完 **成”**。 您的更改可以在下次使用配置时看到。

### 预览搜索配置 {#previewing-the-search-configuration}

1. 选择预览图标：

   ![预览图标](assets/csf-preview-icon.png)

1. 这将显示搜索表单，就像在相应控制台的“搜索”列中显示（完全展开）这些表单一样。

   ![预览表单](assets/csf-preview-form.png)

1. **关闭** 预览以返回并完成配置。

### 删除谓词字段 {#deleting-a-predicate-field}

1. [打开要更新的自定](#creating-opening-a-customized-configuration) 义配置。
1. 选择谓词字段（在右侧），打开“设 **置** ”选项卡，然后选择 **删除** 图标（左下方）。

   ![删除图标](assets/csf-delete-icon.png)

1. 对话框将请求确认删除操作。

1. 使用完成确认此更改和任何其他 **更改**。

### 删除配置（恢复默认配置） {#deleting-a-configuration-to-reinstate-the-default}

自定义配置后，这将覆盖默认值。 您可以通过删除自定义配置来重新声明默认配置。

>[!NOTE]
>
>无法删除默认配置。

从控制台中删除自定义配置：

1. 选择所需的配置(例如，页 **面编辑器(段落搜索**))，然后 **在工具栏中** 选择“删除”图标：

   ![恢复默认](assets/csf-restore-default.png)

1. 将删除自定义配置并恢复默认配置（在控制台中重新显示挂锁符号表示）。

### 添加选项谓词 {#adding-options-predicates}

选项谓词（选项、选项属性）允许您配置要搜索的项目。 它们通常用于直接搜索页面下的内容；例如，页面节点上的属性。

以下示例（根据用于创建页面的模板进行搜索）说明了所涉及的步骤：

1. 创建定义要搜索的属性的节点。

   您需要一个根节点，其中包含单个选项的定义才能提供给用户。

   单个选项的节点需要属性：

   * `jcr:title` -要在搜索边栏中显示的字段标签
   * `value` -要搜索的属性值

   ![谓词定义](assets/csf-options-predicate-01.png)

   >[!NOTE]
   >
   >您 ***不得*** 更改路径中的任 `/libs` 何内容。
   >
   >这是因为下次升级实 `/libs` 例时，内容会被覆盖（而应用修补程序或功能包时，内容很可能会被覆盖）。
   >
   >建议的配置和其他更改方法是：
   >
   >1. 在下重新创建所需的项(它 `/libs`存在于 `/apps`)。 在本例中，来源：
   >1. `/libs/cq/gui/content/common/options/predicates`
   >1. 在 `/apps.`


1. 打开搜 **索Forms** (Search Segation)控制台，选择要更新的配置。 例如，“站 **点管理员搜索边栏**”。 然后选择 **编辑**。

1. 根据配置，向配 **置添加****“选项** ”或“选项”属性。
1. 更新字段，特别是：

   * **属性名称**

      在目标节点上指定要搜索的节点属性。 例如：

      `jcr:content/cq:template`

   * **选项节点路径**

      选择保留选项的路径。 例如：

      `/apps/cq/gui/content/common/options/predicates/templatetype`
   ![选项谓词](assets/csf-options-predicate-02.png)

1. Select **Done** to save your configuration.
1. 导航到相应的控制台(在本例中 **为站点**)并打开“ **搜索-过滤器** ”边栏。 新定义的搜索表单以及各种选项将可见。 选择所需的选项可查看搜索结果。

   ![使用的选项](assets/csf-options-usage.png)


## 用户权限 {#user-permissions}

下表列表了对搜索表单执行编辑、删除和预览操作所需的权限。

<table>
 <thead>
  <tr>
   <td><strong>操作</strong></td>
   <td><strong>权限</strong></td>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td>编辑 </td>
   <td>节点的读取、写入 <code>/apps </code>权限。</td>
  </tr>
  <tr>
   <td>删除</td>
   <td>节点上的读取、写入和删除权 <code>/apps</code> 限</td>
  </tr>
  <tr>
   <td>预览</td>
   <td>节点上的读取、写入和删除 <code>/var/dam/content</code> 权限。<br /> 节点上的读取、写入 <code>/apps</code> 权限。</td>
  </tr>
 </tbody>
</table>
