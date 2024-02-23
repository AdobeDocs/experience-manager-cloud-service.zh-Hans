---
title: 配置搜索表单
description: 为Adobe Experience Manager as a Cloud Service配置搜索Forms 。
exl-id: b06649c4-cc91-44e3-8699-00e90140b90d
source-git-commit: 1a4c5e618adaef99d82a00e1118d1a0f8536fc14
workflow-type: tm+mt
source-wordcount: '2036'
ht-degree: 9%

---

# 配置搜索表单 {#configuring-search-forms}

Adobe Experience Manager as a Cloud Service随附功能强大的功能 [Search](/help/sites-cloud/authoring/search.md) 机制。

此外，还有一组预定义选项，可帮助您筛选内容。 这些保留预定义的Facet，例如 **修改日期**， **发布状态**，或 **活动副本状态** 帮助您快速深入了解所需的资源。

![搜索和筛选使用情况](assets/csf-usage.png)

这些目标共同帮助您从以下位置快速轻松地找到内容：

* [搜索和筛选](/help/sites-cloud/authoring/search.md#search-and-filter)
* [边栏选择器](/help/sites-cloud/authoring/basic-handling.md#rail-selector)
* 该 [资产浏览器](/help/sites-cloud/authoring/page-editor/editor-side-panel.md#assets-browser) （编辑页面时）

>[!NOTE]
>
>您可以配置基础 [内容搜索和索引](/help/operations/indexing.md) 服务。

使用 **搜索Forms**&#x200B;中，您可以根据特定需求自定义和扩展这些面板。

此 **搜索Forms** 提供开箱即用的选择 [谓词](#predicates-and-their-settings) 进行组合和定义。 此 [用于配置这些表单的对话框](#configuring-your-search-forms) 可以通过以下方式访问：

* **工具**
   * **常规**
      * **搜索Forms**

## 默认Forms {#default-forms}

当您首次访问 **搜索Forms** 控制台您可以看到所有配置都有一个挂锁符号。 这表示相应的配置是默认（现成）配置 — 无法删除。 自定义并保存配置后，锁定将消失。 当您 [删除自定义配置](#deleting-a-configuration-to-reinstate-the-default)，则恢复默认设置（以及挂锁指示器）。

![配置搜索表单概述](assets/csf-overview.png)

可用的默认配置（按字母顺序列出）包括：

* **资产管理搜索边栏**
* **页面编辑器（文档搜索）**
* **页面编辑器（体验片段搜索）**
* **页面编辑器（图像搜索）**
* **页面编辑器（手稿搜索）**
* **页面编辑器（页面搜索）**
* **页面编辑器（段落搜索）**
* **页面编辑器（产品搜索）**
* **页面编辑器(Scene7搜索)**
* **页面编辑器（视频搜索）**
* **项目管理员搜索边栏**
* **项目翻译搜索边栏**
* **站点管理员搜索边栏**
* **代码片段管理员搜索边栏**
* **Stock管理员搜索边栏**
* **内容片段模型搜索边栏**
* **项目管理员搜索边栏**
* **项目翻译搜索边栏**

>[!NOTE]
>
>有关资产相关搜索表单的更多详细信息，请参阅 [资产 — 搜索Facet](/help/assets/search-facets.md).


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
   <td>显示Analytics提供的数据时，站点浏览器中的搜索/过滤功能。 Analytics搜索筛选器将加载，以匹配映射的自定义分析列。</td>
   <td>
    <ul>
     <li>字段标签</li>
     <li>描述</li>
    </ul> </td>
  </tr>
  <tr>
   <td>审批状态</td>
   <td>根据审批状态搜索。</td>
   <td>
    <ul>
     <li>字段标签</li>
     <li>属性名称*</li>
     <li>描述</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>创作</td>
   <td>根据作者搜索。</td>
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
   <td>搜索由特定用户签出的资源。</td>
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
   <td>搜索具有特定签出状态的资源。</td>
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
   <td>允许作者搜索/筛选包含特定组件的页面。 例如，图像库。<br /> </td>
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
   <td>搜索在指定范围内为日期属性创建的资源。 在“搜索”面板中，您可以指定开始日期和结束日期。</td>
   <td>
    <ul>
     <li>字段标签</li>
     <li>占位符</li>
     <li>属性名称*</li>
     <li>范围文本（自）*</li>
     <li>范围文本（至）*</li>
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
   <td>根据文件/MIME类型搜索资源。</td>
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
   <td>全文搜索的搜索谓词。 用jcr：contains运算符对其进行映射。</td>
   <td>
    <ul>
     <li>占位符</li>
     <li>属性名称</li>
     <li>描述</li>
    </ul> </td>
  </tr>
  <tr>
   <td>组</td>
   <td>组的搜索谓词（仅用于分析谓词中）。</td>
   <td>
    <ul>
     <li>字段标签</li>
     <li>描述</li>
    </ul> </td>
  </tr>
  <tr>
   <td>隐藏的筛选器</td>
   <td>属性和值的筛选器，用户不可见。</td>
   <td>
    <ul>
     <li>属性名称*</li>
     <li>属性值*</li>
     <li>描述</li>
    </ul> </td>
  </tr>
  <tr>
   <td>见解</td>
   <td>根据选择的分析参数进行搜索。</td>
   <td>这是一个由多个谓词组成的复杂谓词：
    <ul>
     <li>组</li>
     <li>范围</li>
     <li>选项</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>收藏集成员</td>
   <td>搜索属于收藏集成员的资源</td>
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
   <td><p>选项是由用户创建的内容节点。</p> <p>请参阅 <a href="#addinganoptionspredicate">添加选项谓词</a> 以了解更多信息。</p> </td>
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
   <td>Options属性</td>
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
   <td>页面状态</td>
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
   <td>根据特定路径进行筛选。 您可以将多个路径指定为选项。</td>
   <td>
    <ul>
     <li>字段标签</li>
     <li>添加搜索路径</li>
     <li>描述</li>
    </ul> </td>
  </tr>
  <tr>
   <td>路径浏览器</td>
   <td>提供路径浏览器以在预定义的根路径下搜索。</td>
   <td>
    <ul>
     <li>占位符</li>
     <li>根路径</li>
     <li>描述</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>隐藏的路径</td>
   <td>路径上的过滤器，用户不可见。</td>
   <td>
    <ul>
     <li>属性名称(“path”)</li>
     <li>属性值('/content/dam')</li>
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
   <td>搜索指定范围内的资源。 在“搜索”面板中，可以指定范围的最小值和最大值。</td>
   <td>
    <ul>
     <li>字段标签</li>
     <li>属性名称*</li>
     <li>描述</li>
    </ul> </td>
  </tr>
  <tr>
   <td>评分</td>
   <td>根据资源的平均评分搜索资源。<br /> </td>
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
   <td>根据资源的相对创建日期筛选资源。 例如，1周前、1个月前。</td>
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
   <td>使用滑块功能扩展范围谓词的常用搜索谓词。 搜索属性的值必须介于滑块限制之间。</td>
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
   <td>根据审批和签出状态搜索。</td>
   <td>这是一个由多个谓词组成的复杂谓词：
    <ul>
     <li>审批状态</li>
     <li>签出状态</li>
    </ul> 
   </td>
  </tr>
  <tr>
   <td>标记</td>
   <td>基于标记进行搜索。</td>
   <td>
    <ul>
     <li>字段lavel</li>
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
   <td>根据翻译状态搜索。</td>
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
>常见的搜索谓词定义于：
>  `/libs/cq/gui/components/common/admin/customsearch/searchpredicates`
>
>此信息仅供参考，不得更改 `/libs`.

<!--
>* Search predicates related only to siteadmin (classic UI) are located under:
> `/libs/cq/gui/components/siteadmin/admin/searchpanel/searchpredicates`
>   * These are deprecated and only available for backward compatibility.
>
-->

### 谓词设置 {#predicate-settings}

根据谓词，可以配置一系列设置，包括：

* **字段标签**

  将显示为可折叠标题或谓词字段标签的标签。

* **描述**

  用户的描述性详细信息。

* **占位符**

  空文本或谓词的占位符（如果未输入过滤文本）。

* **属性名称**

  要搜索的属性。 它使用相对路径和通配符 `*/*/*` 指定相对于的属性深度 `jcr:content` 节点（每个星号代表一个节点级别）。

  如果只想在资源的第一级子节点上搜索，该资源具有 `x` 上的属性 `jcr:content` 节点使用 `*/jcr:content/x`

* **属性深度**

  在资源中搜索该属性的最大深度。 因此，可以对该属性进行资源搜索并递归子项，直到子项的级别等于指定的深度。

* **属性值**

  作为绝对字符串或表达式语言的属性值；例如， `cq:Page` 或

  `${empty requestPathInfo.suffix ? "/content" : requestPathInfo.suffix}`。

* **范围文本**

  中范围字段的标签 **日期范围** 谓词。

* **选项路径**

  用户可以使用谓词设置选项卡中的路径浏览器选择路径。 选择 **+** 图标用于将所选内容添加到有效选项列表中(然后 **-** 图标以删除（如有必要）。

  这些选项是由用户创建的内容节点，具有以下结构：

  `(jcr:primaryType = nt:unstructured, value (String), jcr:title (String))`

* **选项节点路径**
实际上与 **选项路径**，只有公用谓词字段中有此变量，其他变量专用于资产。

* **单选**
如果选中，这些选项将呈现为仅允许单个选择的复选框。 如果错误地选中此复选框，则可取消选中此复选框。

* **发布和Live Copy属性名称**
站点特定谓词的发布和Live Copy复选框的标签。

* 中的字段标签上的&amp;ast； **设置** 制表符表示这些字段为必填项，如果留空，将显示错误消息。

## 配置搜索Forms {#configuring-your-search-forms}

### 创建/打开自定义配置 {#creating-opening-a-customized-configuration}

1. 导航到 **工具**， **常规**， **搜索Forms**.

1. 选择要自定义的配置。
1. 使用 **编辑** 图标以打开配置以进行更新。
1. 如果进行了新的自定义，则您可能需要 [添加新谓词字段并定义设置](#add-edit-a-predicate-field-and-define-field-settings) 根据需要。 如果存在自定义项，您可以选择现有字段并 [更新设置](#add-edit-a-predicate-field-and-define-field-settings).
1. 选择 **完成** 以保存配置。 下次使用该配置时即可看到您所做的更改。

   >[!NOTE]
   >
   >自定义配置存储（根据需要）在下：
   >
   >* `/apps/cq/gui/content/facets/<option>`
   >* `/apps/commerce/gui/content/facets/<option>`

### 添加/编辑谓词字段并定义字段设置 {#add-edit-a-predicate-field-and-define-field-settings}

您可以添加或编辑字段并定义/更新其设置：

1. [打开自定义配置](#creating-opening-a-customized-configuration) 以进行更新。
1. 如果要添加新字段，请打开 **选择谓词** 制表符并将所需的谓词拖到所需的位置。 例如， **日期范围谓词**：

   ![添加谓词](assets/csf-add-predicate.png)

1. 取决于是否：

   * 您正在添加新字段：

     添加谓词后， **设置** 选项卡将打开并显示可以定义的属性。

   * 要更新现有的谓词：

     选择谓词字段（位于右侧），然后打开 **设置** 选项卡。

   例如， **日期范围谓词**：

   ![修改谓词](assets/csf-modify-predicate.png)

1. 根据需要进行更改并通过进行确认 **完成**. 下次使用该配置时即可看到您所做的更改。

### 预览搜索配置 {#previewing-the-search-configuration}

1. 选择预览图标：

   ![预览图标](assets/csf-preview-icon.png)

1. 显示搜索表单（完全展开）在相应控制台的“搜索”列中的显示方式。

   ![预览表单](assets/csf-preview-form.png)

1. **关闭** 预览以返回并完成配置。

### 删除谓词字段 {#deleting-a-predicate-field}

1. [打开自定义配置](#creating-opening-a-customized-configuration) 以进行更新。
1. 选择谓词字段（位于右侧），打开 **设置** 选项卡，然后选择 **删除** 图标（左下方）。

   ![删除图标](assets/csf-delete-icon.png)

1. 此时将显示一个对话框，要求确认删除操作。

1. 通过确认此更改和任何其他更改 **完成**.

### 删除配置（恢复默认设置） {#deleting-a-configuration-to-reinstate-the-default}

自定义配置后，这将覆盖默认值。 您可以通过删除自定义配置来重新声明默认配置。

>[!NOTE]
>
>您无法删除默认配置。

从控制台中删除自定义配置已完成：

1. 选择所需的配置(例如， **页面编辑器（段落搜索）**)，然后 **删除** 工具栏中的图标：

   ![恢复默认值](assets/csf-restore-default.png)

1. 自定义配置将被删除，默认配置将恢复（控制台中挂锁符号的重新显示即表示这一点）。

### 添加选项谓词 {#adding-options-predicates}

选项谓词（选项、选项属性）允许您配置要搜索的项目。 属性通常用于直接在页面下搜索某些内容；例如，页面节点上的属性。

以下示例（根据用于创建页面的模板进行搜索）说明了所涉及的步骤：

1. 创建定义要搜索的属性的节点。

   您需要一个根节点，其中包含可供用户使用的各个选项的定义。

   单个选项的节点需要以下属性：

   * `jcr:title`  — 要在搜索边栏中显示的字段标签
   * `value`  — 要搜索的属性值

   ![谓词定义](assets/csf-options-predicate-01.png)

   >[!NOTE]
   >
   >您 ***必须*** 不会更改中的任何内容 `/libs` 路径。
   >
   >这是因为 `/libs` 下次升级实例时将被覆盖（在应用修补程序或功能包时很可能会被覆盖）。
   >
   >建议用于配置和其他更改的方法是：
   >
   >1. 重新创建所需的项目，因为它存在于中 `/libs`，下 `/apps`. 在本例中，来自：
   >1. `/libs/cq/gui/content/common/options/predicates`
   >1. 在中进行任何更改 `/apps.`

1. 打开 **搜索Forms** 控制台并选择要更新的配置。 例如， **站点管理员搜索边栏**. 然后选择 **编辑**.

1. 根据配置，添加 **选项** 或 **Options属性** 到配置。
1. 更新这些字段，特别是：

   * **属性名称**

     指定要在目标节点上搜索的节点属性。 例如：

     `jcr:content/cq:template`

   * **选项节点路径**

     选择保留选项的路径。 例如：

     `/apps/cq/gui/content/common/options/predicates/templatetype`

   ![选项谓词](assets/csf-options-predicate-02.png)

1. 选择 **完成** 以保存您的配置。
1. 导航到相应的控制台(在本例中， **站点**)并打开 **搜索 — 筛选器** 边栏。 新定义的搜索表单以及各种选项均可见。 选择所需的选项以查看搜索结果。

   ![正在使用的选项](assets/csf-options-usage.png)


## 用户权限 {#user-permissions}

下表列出了对搜索表单执行编辑、删除和预览操作所需的权限。

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
   <td>对的读、写权限 <code>/apps </code>节点。</td>
  </tr>
  <tr>
   <td>删除</td>
   <td>对的读、写、删除权限 <code>/apps</code> 节点</td>
  </tr>
  <tr>
   <td>预览</td>
   <td>对的读、写、删除权限 <code>/var/dam/content</code> 节点。<br /> 对的读、写权限 <code>/apps</code> 节点。</td>
  </tr>
 </tbody>
</table>
