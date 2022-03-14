---
title: 在 [!DNL Adobe Experience Manager]
description: 了解如何在 [!DNL Adobe Experience Manager] ，以及如何使用搜索中显示的资产。
contentOwner: AG
mini-toc-levels: 1
feature: Search,Metadata,Asset Distribution
role: User,Admin
exl-id: 68bdaf25-cbd4-47b3-8e19-547c32555730
source-git-commit: d37193833d784f3f470780b8f28e53b473fd4e10
workflow-type: tm+mt
source-wordcount: '4897'
ht-degree: 7%

---

# 在中搜索资产 [!DNL Adobe Experience Manager] {#search-assets-in-aem}

[!DNL Adobe Experience Manager Assets] 提供了强大的资产发现方法，可帮助您实现更高的内容速度。 您的团队可以使用现成的功能和自定义方法，通过无缝、智能的搜索体验缩短上市时间。 搜索资产是使用数字资产管理系统的核心 — 无论是供创意人员进一步使用，还是由业务用户和营销人员对资产进行稳健管理，还是由DAM管理员进行管理。 简单、高级和自定义的搜索，您可以通过执行这些搜索 [!DNL Assets] 用户界面或其他应用程序和界面可帮助完成这些用例。

[!DNL Experience Manager Assets] 支持以下用例，本文介绍了这些用例的使用、概念、配置、限制和疑难解答。

| 搜索资产 | 配置和管理搜索功能 | 处理搜索结果 |
|---|---|---|
| [基本搜索](#searchbasics) | [搜索索引](#searchindex) | [排序结果](#sort) |
| [了解搜索UI](#searchui) | [文本提取](#extracttextupload) | [检查资产的属性和元数据](#checkinfo) |
| [搜索建议](#searchsuggestions) | [必需元数据](#mandatorymetadata) | [下载](#download) |
| [了解搜索结果和行为](#searchbehavior) | [修改搜索彩块化](#searchfacets) | [批量元数据更新](#metadata-updates) |
| [搜索排名和提升](#searchrank) | [自定义谓词](#custompredicates) | [智能收藏集](#collections) |
| [高级搜索：筛选和搜索范围](#scope) |  | [了解意外结果并排除其故障](#unexpected-results) |
| [从其他解决方案和应用程序中搜索](#search-assets-other-surfaces):<ul><li>[Adobe Asset Link](#aal)</li><li>[Brand Portal](#brand-portal)</li><li>[Experience Manager桌面应用程序](#desktop-app)</li><li>[Adobe Stock图像](#adobe-stock)</li><li>[Dynamic Media资产](#search-dynamic-media-assets)</li></ul> |  |  |
| [资产选择器](#asset-picker) |  |  |
| [限制](#limitations) 和 [提示](#tips) |  |  |
| [示例](#samples) |  |  |

使用 [!DNL Experience Manager] web界面。 转到 **[!UICONTROL 资产]** > **[!UICONTROL 文件]** in [!DNL Experience Manager]，单击 ![search_icon](assets/do-not-localize/search_icon.png) 在顶部栏中，输入搜索关键词，然后选择 `Return`. 或者，使用关键词快捷键 `/` （正斜杠）以打开Omnisearch字段。 `Location:Assets` 已预选以限制对DAM资产的搜索。 [!DNL Experience Manager] 在您开始键入搜索关键词时提供建议。

使用 **[!UICONTROL 过滤器]** 面板来搜索资产、文件夹、标记和元数据。 您可以根据各种选项（谓词）筛选搜索结果，例如文件类型、文件大小、上次修改日期、资产状态、分析数据和Adobe Stock许可。 您可以自定义“过滤器”面板，并使用 [搜索彩块化](/help/assets/search-facets.md). 的 [!UICONTROL 文件类型] 过滤器 [!UICONTROL 过滤器] 面板具有混合状态复选框。 因此，除非选择所有嵌套谓词（或格式），否则会部分选中第一级复选框。

[!DNL Experience Manager] 搜索功能支持搜索收藏集和搜索收藏集中的资产。 请参阅 [搜索收藏集](/help/assets/manage-collections.md).

## 了解搜索界面 {#searchui}

熟悉搜索界面和可用的操作。

![了解Experience Manager Assets搜索结果界面](assets/aem_search_results.png)

*图：了解 [!DNL Experience Manager Assets] 搜索结果界面。*

**A.** 将搜索另存为智能收藏集。 **B.** 过滤或谓词以缩小搜索结果。 **C.** 显示文件、文件夹或两者。 **D.** 单击“过滤器”以打开或关闭左边栏。**E.** 搜索位置为 DAM。**F.** 包含用户提供的搜索关键词的Omnisearch字段。 **G.** 选择加载的搜索结果。 **H.** 显示的搜索结果占总搜索结果的数量。 **我。** 关闭搜索。 **J.** 在卡片视图和列表视图之间切换。

### 动态搜索彩块化 {#dynamicfacets}

您可以使用搜索彩块化中动态更新的预期搜索结果数，更快地从搜索结果页面中发现所需的资产。 预期的资产数量会在应用搜索过滤器之前进行更新。 通过过滤器查看预期计数有助于您快速高效地浏览搜索结果。

![在搜索彩块化中，查看不筛选搜索结果的资产大致数量。](assets/asset_search_results_in_facets_filters.png)

*图：在搜索彩块化中，查看不筛选搜索结果的资产大致数量。*

## 在键入时搜索建议 {#searchsuggestions}

开始键入关键词时，Experience Manager会建议可能的搜索关键词或短语。 建议基于Experience Manager中的资产。 Experience Manager为所有元数据字段编入索引，以帮助进行搜索。 为了提供搜索建议，系统使用以下几个元数据字段的值。 要提供搜索建议，请考虑使用适当的关键字填充以下字段：

* 资产标记。 (映射到 `jcr:content/metadata/cq:tags`)
* 资产标题。 (映射到 `jcr:content/metadata/dc:title`)
* 资产描述。 (映射到 `jcr:content/metadata/dc:description`)
* JCR存储库中的标题。 该值可能会映射到资产标题。 (映射到 `jcr:content/jcr:title`)
* JCR存储库中的描述。 该值可能会映射到资产描述。 (映射到 `jcr:content/jcr:description`)

## 了解搜索结果和行为 {#searchbehavior}

### 基本搜索词和结果 {#searchbasics}

您可以从OmniSearch字段运行关键词搜索。 关键字搜索不区分大小写，并且是全文搜索（跨常用元数据字段）。 如果使用多个关键词， `AND` 是关键词之间的默认运算符。

结果按相关性排序，从最接近的匹配开始。 对于多个关键字，更相关的结果是元数据中同时包含这两个术语的资产。 在元数据中，显示为智能标记的关键词的排名高于其他元数据字段中显示的关键词。 [!DNL Experience Manager] 允许为特定搜索词赋予更高的权重。 此外， [提升排名](#searchrank) 特定搜索词的几个目标资产。

为了快速找到相关资产，富界面提供了过滤、排序和选择机制。 您可以根据多个条件筛选结果，并查看针对各种筛选条件搜索的资产数量。 或者，您也可以通过更改Omnisearch字段中的查询来重新运行搜索。 当您更改搜索词或过滤器时，仍会应用其他过滤器以保留搜索的上下文。

当结果为多个资产时， [!DNL Experience Manager] 在卡片视图中显示前100个，在列表视图中显示200个。 用户滚动时，会加载更多资产。 这是为了提高性能。 观看 [显示的资产数量](https://www.youtube.com/watch?v=LcrGPDLDf4o).

有时，您可能会在搜索结果中看到一些意外的资产。 有关更多信息，请参阅 [意外结果](#unexpected-results).

[!DNL Experience Manager] 可以搜索多种文件格式，并且可以自定义搜索过滤器以满足您的业务要求。 请与管理员联系，以了解哪些搜索选项可用于您的DAM存储库，以及您的帐户具有哪些限制。

<!-- 
### Results with and without enhanced Smart Tags {#withsmarttags}

By default, [!DNL Experience Manager] search combines the search terms with an AND clause. For example, consider searching for keywords woman running. Only the assets with both woman and running keywords in the metadata appear in the search results by default. The same behavior is retained when special characters (periods, underscores, or dashes) are used with the keywords. The following search queries return the same results:

* `woman running`
* `woman.running`
* `woman-running`

However, the query `woman -running` returns assets without `running` in their metadata.
Using Smart Tags adds an extra `OR` clause to find any of the search terms as the applied smart tags. An asset tagged with either `woman` or `running` using Smart Tags also appear in such a search query. So the search results are a combination of,

* Assets with `woman` and `running` keywords in the metadata (default behavior).

* Assets smart tagged with either of the keywords (Smart Tags behavior).
-->

### 搜索排名和提升 {#searchrank}

首先显示与元数据字段中的所有搜索词匹配的搜索结果，然后显示与智能标记中的任意搜索词匹配的搜索结果。 在上例中，搜索结果的显示大致顺序为：

1. 匹配 `woman running` 在各种元数据字段中。
1. 匹配 `woman running` 在智能标记中。
1. 匹配 `woman` 或 `running` 在智能标记中。

您可以提高特定资产的关键词相关性，以帮助根据关键词提高搜索量。 换言之，在您基于这些关键词进行搜索时，向其促销特定关键词的图像会显示在搜索结果的顶部。

1. 从 [!DNL Assets] 用户界面中，打开资产的属性页面。 单击 **[!UICONTROL 高级]** 单击 **[!UICONTROL 添加]** 在 **[!UICONTROL 提升搜索关键词]**.
1. 在 **[!UICONTROL Search Promote]** 框中，指定要增加图像搜索的关键词，然后单击 **[!UICONTROL 添加]**. 您可以以相同方式指定多个关键词。
1. 单击&#x200B;**[!UICONTROL 保存并关闭]**。您为此关键词促销的资产会显示在热门搜索结果中。

您可以通过提升目标关键字的搜索结果中某些资产的排名，来使用此功能。 请观看下面的视频示例。 有关详细信息，请参阅 [搜索 [!DNL Experience Manager]](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/search-and-discovery/search-boost.html).

>[!VIDEO](https://video.tv.adobe.com/v/16766/?quality=6)

*视频：了解搜索结果的排名方式以及排名如何受到影响。*

## 高级搜索 {#scope}

[!DNL Experience Manager] 提供了各种方法，如应用于搜索的资产的过滤器，以帮助您更快地找到所需的资产。 下面介绍了一些常用的方法。 部分 [示例](#samples) 共享。

**搜索文件或文件夹**:在搜索结果中，查看文件、文件夹或两者。 从 **[!UICONTROL 过滤器]** 面板时，您可以选择相应的选项。 请参阅 [搜索界面](#searchui).

**在文件夹中搜索资产**:您可以将搜索限制为特定文件夹。 在 **[!UICONTROL 过滤器]** 面板，添加文件夹的路径。 一次只能选择一个文件夹。

![通过在“筛选器”面板中添加文件夹路径，将搜索结果限制为文件夹](assets/search_folder_select.gif)

*图：通过在“筛选器”面板中添加文件夹路径，将搜索结果限制为文件夹。*

### 查找类似图像 {#visualsearch}

要查找与用户选择的图像视觉上相似的图像，请从图像的卡片视图或工具栏中单击&#x200B;**[!UICONTROL 查找类似]**&#x200B;选项。[!DNL Experience Manager] 显示 DAM 存储库中与用户所选图像相似的智能标记图像。

![使用卡片视图中的选项查找类似图像](assets/search_find_similar.png)

*图：使用卡片视图中的选项查找类似图像。*

### Adobe Stock图像 {#adobe-stock}

从 [!DNL Experience Manager] 用户界面，用户可搜索 [Adobe Stock资产](/help/assets/aem-assets-adobe-stock.md) 并授权所需资产。 添加 `Location: Adobe Stock` 中。 您还可以使用过滤器面板来查找所有授权或未授权的资产，或使用Adobe Stock文件号搜索特定资产。

### Dynamic Media资产 {#dmassets}

您可以通过选择&#x200B;**[!UICONTROL 过滤器]**&#x200B;面板中的 **[!UICONTROL Dynamic Media]** > **[!UICONTROL 集]**&#x200B;来过滤 Dynamic Media 图像。该操作可过滤并显示图像集、轮播集、混合媒体集和旋转集等资产。

### 使用元数据字段中的特定值进行GQL搜索 {#gql-search}

您可以根据元数据字段的确切值（如标题、描述和创建者）来搜索资产。 GQL全文搜索功能仅获取其元数据值与您的搜索查询完全匹配的资产。 属性的名称（创建者、标题等）和值区分大小写。

| 元数据字段 | Facet值和用法 |
|---|---|
| 标题 | title:John |
| 创建者 | creator:John |
| 位置 | 位置：NA |
| 描述 | description:&quot;Sample Image&quot; |
| 创建者工具 | creatortool:&quot;Adobe Photoshop&quot; |
| 版权所有者 | copyrightowner:&quot;Adobe Systems&quot; |
| 参与者 | contributor:John |
| 使用条款 | usageterms:&quot;CopyRights Reserved&quot; |
| 创建时间 | created:YYYY-MM-DDTHH |
| 过期日期 | expires:YYYY-MM-DDTHH |
| 开始时间 | ontime:YYYY-MM-DDTHH |
| 结束时间 | offtime:YYYY-MM-DDTHH |
| 时间范围（过期日期、开始时间、结束时间） | facet字段：下限……上限 |
| 路径 | /content/dam/&lt;folder name> |
| PDF 标题 | pdftitle:&quot;Adobe Document&quot; |
| 主题 | subject:&quot;Training&quot; |
| 标记 | tags:&quot;Location And Travel&quot; |
| 类型 | type:&quot;image\png&quot; |
| 图像宽度 | width:lowerbound..上限 |
| 图像高度 | height:lowerbound..上限 |
| 人员 | person:John |

属性 `path`, `limit`, `size`和 `orderby` 不能使用 `OR` 运算符。

<!-- TBD: Where are the limit, size, orderby properties defined?
-->

用户生成属性的关键字是其属性编辑器中的字段标签（以小写形式显示），并删除空格。

以下是复杂查询的一些搜索格式示例：

* 要显示具有多个Facet字段的所有资产(例如：title=John Doe and creator tool = Adobe Photoshop): `title:"John Doe" creatortool:Adobe*`
* 当Facet值不是单个词而是句子时，显示所有资产(例如：title=Scott Reynolds): `title:"Scott Reynolds"`
* 要显示具有单个属性的多个值的资产(例如：title=Scott Reynolds或John Doe): `title:"Scott Reynolds" OR "John Doe"`
* 要显示属性值以特定字符串开头的资产(例如：标题是Scott Reynolds): `title:Scott*`
* 要显示属性值以特定字符串结尾的资产(例如：标题是Scott Reynolds): `title:*Reynolds`
* 要显示包含属性值且其中包含特定字符串的资产(例如：title =巴塞尔会议室): `title:*Meeting*`
* 要显示包含特定字符串且具有特定属性值的资产(例如：在标题为John Doe的资产中搜索字符串Adobe): `*Adobe* title:"John Doe"`

## 从其他资产中搜索资产 [!DNL Experience Manager] 产品或界面 {#search-assets-other-surfaces}

[!DNL Adobe Experience Manager] 将DAM存储库连接到其他各种 [!DNL Experience Manager] 解决方案，以便更快地访问数字资产并简化创意工作流程。 任何资产发现都以浏览或搜索开头。 在各种曲面和解决方案中，搜索行为基本保持不变。 某些搜索方法会随着目标受众、用例和用户界面的不同而发生更改， [!DNL Experience Manager] 解决方案。 下面的链接中介绍了各个解决方案的具体方法。 本文介绍了普遍适用的提示和行为。

### 从Adobe资产链接面板搜索资产 {#aal}

使用Adobe资产链接，创意专业人士现在可以访问 [!DNL Experience Manager Assets]，而无需离开支持的Adobe Creative Cloud应用程序。 创意人员可以使用 [!DNL Adobe Creative Cloud] 应用程序： [!DNL Adobe Photoshop], [!DNL Adobe Illustrator]和 [!DNL Adobe InDesign]. 资产链接还允许用户搜索视觉上相似的结果。 可视搜索显示结果由Adobe Sensei的机器学习算法提供支持，并帮助用户找到在美学上相似的图像。 请参阅 [搜索和浏览资产](https://helpx.adobe.com/cn/enterprise/using/manage-assets-using-adobe-asset-link.html#UseAdobeAssetLink) 使用Adobe资产链接。

### 在中搜索资产 [!DNL Experience Manager] 桌面应用程序 {#desktop-app}

创意专业人士使用桌面应用程序 [!DNL Experience Manager Assets] 可轻松搜索并在其本地桌面(Win或Mac)上提供。 创意人员可以轻松地在Mac Finder或Windows资源管理器中显示所需的资产，在桌面应用程序中打开并在本地更改 — 更改将保存回 [!DNL Experience Manager] 在存储库中创建了新版本。 应用程序支持使用一个或多个关键字进行基本搜索， `*` 和 `?` 通配符和 `AND` 运算符。 请参阅 [浏览、搜索和预览资产](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#browse-search-preview-assets) 在桌面应用程序中。

### 在中搜索资产 [!DNL Brand Portal] {#brand-portal}

业务线用户和营销人员使用Brand Portal，与其扩展的内部团队、合作伙伴和经销商高效、安全地共享已批准的数字资产。 请参阅 [在Brand Portal中搜索资产](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/search-capabilities/brand-portal-searching.html).

### 搜索 [!DNL Adobe Stock] 图像 {#adobe-stock1}

从 [!DNL Experience Manager] 用户界面中，用户可以搜索Adobe Stock资产并授权所需的资产。 添加 `Location: Adobe Stock` 在Omnisearch字段中。 您还可以使用 **[!UICONTROL 过滤器]** 面板，以查找所有授权或未授权的资产，或使用Adobe Stock文件号搜索特定资产。 请参阅 [管理 [!DNL Adobe Stock] 图像 [!DNL Experience Manager]](/help/assets/aem-assets-adobe-stock.md#usemanage).

### 搜索 [!DNL Dynamic Media] 资产 {#search-dynamic-media-assets}

您可以通过选择&#x200B;**[!UICONTROL 过滤器]**&#x200B;面板中的 **[!UICONTROL Dynamic Media]** > **[!UICONTROL 集]**&#x200B;来过滤 Dynamic Media 图像。该操作可过滤并显示图像集、轮播集、混合媒体集和旋转集等资产。在创作网页时，作者可以在内容查找器中搜索集。弹出菜单中提供集的过滤器。

### 创作网页时在内容查找器中搜索资产 {#content-finder}

作者可以使用内容查找器搜索DAM存储库中的相关资产，并在他们创建的网页中使用资产。 作者还可以使用“连接的资产”功能搜索远程设备上可用的资产 [!DNL Experience Manager] 部署。 然后，作者可以在本地的网页中使用这些资产 [!DNL Experience Manager] 部署。 请参阅 [使用远程资产](/help/assets/use-assets-across-connected-assets-instances.md#use-remote-assets).

### 搜索收藏集 {#collections}

[!DNL Experience Manager] 搜索功能支持搜索收藏集和搜索收藏集中的资产。 请参阅 [搜索收藏集](/help/assets/manage-collections.md).

## 资产选择器 {#asset-picker}

资产选择器(在以前版本的 [!DNL Adobe Experience Manager])允许您以特殊方式搜索、筛选和浏览DAM资产。 资产选择器位于 `https://[aem_server]:[port]/aem/assetpicker.html`. 您可以使用资产选择器获取您选择的资产的元数据。 您可以使用支持的请求参数来启动它，例如资产类型（图像、视频、文本）和选择模式（单个或多个选择）。 这些参数为特定搜索实例设置资产选择器的上下文，并在整个选择过程中保持不变。

资产选择器使用HTML5 `Window.postMessage` 消息，以将选定资产的数据发送给收件人。 它仅在浏览模式下工作，并且仅在Omnisearch结果页面中工作。

在URL中传递以下请求参数，以在特定上下文中启动资产选择器：

| 名称 | 值 | 示例 | 用途 |
|---|---|---|---|
| 资源后缀(B) | 作为URL中资源后缀的文件夹路径： [https://localhost:4502/aem/assetpicker.html/&lt;folder_path>](https://localhost:4502/aem/assetpicker.html) | 要启动资产选择器并选择特定文件夹，例如文件夹 `/content/dam/we-retail/en/activities` ，则URL应为以下形式： `https://localhost:4502/aem/assetpicker.html/content/dam/we-retail/en/activities?assettype=images` | 如果在启动资产选择器时需要选择特定文件夹，则会将其作为资源后缀传递。 |
| `mode` | 单个，多个 | <ul><li>`https://localhost:4502/aem/assetpicker.html?mode=single`</li><li>`https://localhost:4502/aem/assetpicker.html?mode=multiple`</li></ul> | 在多个模式下，您可以使用资产选择器同时选择多个资产。 |
| `dialog` | true，false | [https://localhost:4502/aem/assetpicker.html?dialog=true](https://localhost:4502/aem/assetpicker.html?dialog=true) | 使用这些参数以Granite对话框的形式打开资产选择器。 仅当您通过Granite路径字段启动资产选择器，并将其配置为pickerSrc URL时，此选项才适用。 |
| `root` | &lt;folder_path> | `https://localhost:4502/aem/assetpicker.html?assettype=images&root=/content/dam/we-retail/en/activities` | 使用此选项可为资产选择器指定根文件夹。 在这种情况下，资产选择器允许您仅选择根文件夹下的子资产（直接/间接）。 |
| `viewmode` | 搜索 |  | 要在搜索模式下启动资产选择器，请使用 `assettype` 和 `mimetype` 参数。 |
| `assettype` | 图像、文档、多媒体、存档。 | <ul><li>`https://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=images`</li><li> `https://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=documents` </li><li> `https://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=multimedia` </li><li> `https://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=archives` </li></ul> | 使用选项可根据提供的值筛选资产类型。 |
| `mimetype` | MIME类型(`/jcr:content/metadata/dc:format`)（也支持通配符）。 | <ul><li>`https://localhost:4502/aem/assetpicker.html?mimetype=image/png`</li><li>`https://localhost:4502/aem/assetpicker.html?mimetype=*png`</li><li>`https://localhost:4502/aem/assetpicker.html?mimetype=*presentation`</li><li>`https://localhost:4502/aem/assetpicker.html?mimetype=*presentation&mimetype=*png`</li></ul> | 可使用它根据MIME类型筛选资产。 |

要访问资产选择器界面，请转到 `https://[aem_server]:[port]/aem/assetpicker`. 导航到所需的文件夹，然后选择一个或多个资产。 或者，从Omnisearch框中搜索所需的资产，根据需要应用过滤器，然后选择该资产。

![在资产选择器中浏览并选择资产](assets/assetpicker.png)

*图：在资产选择器中浏览并选择资产。*

## 限制 {#limitations}

中的搜索功能 [!DNL Experience Manager Assets] 具有以下限制：

* 请勿在搜索查询中输入前导空格，否则搜索将不起作用。
* [!DNL Experience Manager] 在您从搜索的结果中选择资产的属性，然后取消搜索后，可能会继续显示搜索词。 <!-- (CQ-4273540) -->
* 在搜索文件夹或文件和文件夹时，无法按任何参数对搜索结果进行排序。
* 如果您选择 `Return` 无需在Omnisearch栏中键入内容， [!DNL Experience Manager] 返回仅包含文件而非文件夹的列表。 如果您在不使用关键字的情况下专门搜索文件夹， [!DNL Experience Manager] 不返回任何结果。
* 您可以对文件夹执行全文搜索。 指定搜索词以使搜索正常工作。

可视搜索或相似度搜索具有以下限制：

* 可视化搜索最适合于大型存储库。 尽管没有获得良好结果所需的最少图像数，但与一些图像的匹配质量不如大型存储库中的匹配质量好。
* 不能更改模型或训练 [!DNL Experience Manager] 查找类似图像。 例如，向少数资产添加或删除智能标记不会更改模型。 资产会从视觉上相似的搜索结果中排除。

在以下情况下，搜索功能可能会存在性能限制：

* 与显示搜索结果的列表视图相比，卡片视图的加载时间更快。

## 搜索提示 {#tips}

* 在监控资产的审核状态时，请使用相应的选项来查找已批准的资产或待批准的资产。
* 使用“分析”谓词，可根据从各种创意应用程序获取的资产使用情况统计信息来搜索受支持的资产。 使用情况数据按资产显示类别的使用情况得分、展示次数、点击次数和媒体渠道进行分组。
* 使用 **[!UICONTROL 全选]** 复选框以选择搜索的资产。 [!DNL Experience Manager] 最初在卡片视图中显示100个资产，在列表视图中显示200个资产。 滚动搜索结果时会加载更多资产。 您可以选择的资产比加载的资产多。 选定资产的计数显示在搜索结果页面的右上角。 您可以对所选内容进行操作，例如下载选定的资产、批量更新选定资产的元数据属性，或将选定的资产添加到收藏集。 选择的资产多于显示的资产时，会对所有选定的资产应用一项操作，或者出现一个对话框，显示所应用的资产数量。 要对未加载的资产应用操作，请确保明确选择了所有资产。
* 要搜索不包含必需元数据的资产，请参阅 [必需元数据](#mandatorymetadata).
* 搜索使用所有元数据字段。 一般搜索（如搜索12）通常会返回许多结果。 为获得更好的结果，请使用双引号（而非单引号）或确保数字与没有特殊字符的单词相连(例如， `shoe12`)。
* 全文搜索支持运算符，例如 `-` 和 `^`. 要将这些字母作为字符串文字搜索，请用双引号将搜索表达式引住。 例如，使用 `"Notebook - Beauty"` 而不是 `Notebook - Beauty`.
* 如果搜索结果过多，请限制 [搜索范围](#scope) ，以便在所需的资产上插入。 当您对如何更好地查找所需资产（例如，特定文件类型、特定位置、特定元数据等）有一些想法时，效果会最佳。

* **标记**:标记可帮助您对能够更高效地浏览和搜索的资产进行分类。 标记有助于将相应的分类推广到其他用户和工作流。 [!DNL Experience Manager] 提供了使用Adobe Sensei人为智能服务自动标记资产的方法，这些方法可不断通过使用和培训更好地标记资产。 在搜索资产时，会考虑智能标记。 它与内置搜索功能结合使用。 请参阅 [搜索行为](#searchbehavior). 要优化搜索结果的显示顺序，您可以 [提升搜索排名](#searchrank) 中的“隐藏主体”。

* **索引**:搜索结果中只返回已索引的元数据和资产。 为获得更好的覆盖面和性能，请确保正确索引并遵循最佳实践。 请参阅 [索引](#searchindex).

## 一些说明搜索的示例 {#samples}

使用关键词周围的双引号，以按用户指定的准确顺序查找包含确切短语的资产。

![带引号和不带引号的搜索行为](assets/search_with_quotes.gif)

*图：搜索行为（包含引号和不包含引号）。*

**使用星号通配符搜索**:要扩大搜索范围，请在搜索词之前或之后使用星号来匹配任意数量的字符。 例如，搜索不带星号的运行不会返回包含单词任何变体（包括在元数据中）的资产。 星号用于替换任意数量的字符。 例如，

* `run` 返回具有完全运行关键字的资产
* `run*` 返回带有 `running`, `run`, `runaway`，等等。
* `*run` 返回带有 `outrun`, `rerun`，等等。
* `*run*` 返回所有可能的组合。

![通过示例说明在资产搜索中使用星号通配符](assets/search_with_asterisk_run.gif)

*图：通过示例，说明了如何在资产搜索中使用星号通配符。*

**使用问号通配符搜索**:要扩大搜索范围，请使用一个或多个“？” 字符以匹配精确的字符数。 例如，在下图中，

* `run???` 查询与任何资产均不匹配。

* `run????` 查询与单词匹配 `running` 后面有四个字符 `run`.

* `??run` 查询与单词匹配 `rerun` 之前两个字符 `run`.

![通过一个示例说明在资产搜索中使用问号通配符的方法](assets/search_with_questionmark_run.gif)

*图：通过示例说明了如何在资产搜索中使用问号通配符。*

**排除关键词**:使用短划线搜索不包含关键字的资产。 例如， `running -shoe` 查询会返回包含 `running`，但不是 `shoe`. 同样， `camp -night` 查询会返回包含 `camp` 但不是 `night`. 查询 `camp-night` 返回同时包含这两个资产 `camp` 和 `night`.

![使用短划线搜索不包含排除的关键词的资产](assets/search_dash_exclude_keyword.gif)

*图：使用短划线搜索不包含排除的关键词的资产。*

<!--
## Configuration and administration tasks related to search functionality {#configadmin}

### Search index configurations {#searchindex}

Asset discovery relies on indexing of DAM contents, including the metadata. Faster and accurate asset discovery relies on optimized indexing and appropriate configurations. See [indexing](/help/operations/indexing.md).
-->

<!--
### Visual or similarity search {#configvisualsearch}

Visual search uses Smart Tags. After configuring smart tagging functionality, follow these steps.

1. In [!DNL Experience Manager] CRXDE, in `/oak:index/lucene` node, add the following properties and values and save the changes.

    * `costPerEntry` property of type `Double` with the value `10`.

    * `costPerExecution` property of type `Double` with the value `2`.

    * `refresh` property of type `Boolean` with the value `true`.

   This configuration allows searches from the appropriate index.

1. To create Lucene index, in CRXDE, at `/oak:index/damAssetLucene/indexRules/dam:Asset/properties`, create node named `imageFeatures` of type `nt-unstructured`. In `imageFeatures` node,

    * Add `name` property of type `String` with the value `jcr:content/metadata/imageFeatures/haystack0`.

    * Add `nodeScopeIndex` property of type `Boolean` with the value of `true`.

    * Add `propertyIndex` property of type `Boolean` with the value of `true`.

    * Add `useInSimilarity` property of type `Boolean` with the value `true`.

   Save the changes.

1. Access `/oak:index/damAssetLucene/indexRules/dam:Asset/properties/predictedTags` and add `similarityTags` property of type `Boolean` with the value of `true`.
1. Apply Smart Tags to the assets in your [!DNL Experience Manager] repository. See [how to configure smart tags](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/configuring/tagging.html#configuring).
1. In CRXDE, in `/oak-index/damAssetLucene` node, set the `reindex` property to `true`. Save the changes.
1. (Optional) If you have customized search form then copy the `/libs/settings/dam/search/facets/assets/jcr%3Acontent/items/similaritysearch` node to `/conf/global/settings/dam/search/facets/assets/jcr:content/items`. Save the changes.

For related information, see [understand smart tags in Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/metadata/image-smart-tags.html) and [how to manage smart tags](/help/assets/smart-tags.md).
-->

<!--
### Mandatory metadata {#mandatorymetadata}

Business users, administrators, or DAM librarians can define some metadata as mandatory metadata that is a must for the business processes to work. For various reasons, some assets may be missing this metadata, such as legacy assets or assets migrated in bulk. Assets with missing or invalid metadata are detected and reported based on the indexed metadata property. To configure it, see [mandatory metadata](/help/assets/metadata-schemas.md#defining-mandatory-metadata).

### Modify search facets {#searchfacets}

To improve the speed of discovery, [!DNL Experience Manager Assets] offers search facets using which you can filter the search results. The Filters panel includes a few standard facets by default. Administrators can customize the Filters panel to modify the default facets using the in-built predicates. [!DNL Experience Manager] provides a good collection of in-built predicates and an editor to customize the facets. See [search facets](/help/assets/search-facets.md).

### Extract text when uploading assets {#extracttextupload}

You can configure [!DNL Experience Manager] to extract the text from the assets when users upload assets, such as PSD or PDF files. [!DNL Experience Manager] indexes the extracted text and helps users search these assets based on the extracted text. See [upload assets](/help/assets/manage-digital-assets.md#uploading-assets).
-->

### 用于筛选搜索结果的自定义谓词 {#custompredicates}

谓词用于创建Facet。 管理员可以使用预配置的谓词，在“过滤器”面板中自定义搜索彩块化。 可以使用叠加图自定义这些谓词。 请参阅 [创建自定义谓词](/help/assets/search-facets.md).

您可以根据以下一个或多个属性搜索数字资产。 默认情况下，对其中某些属性应用的过滤器可用，并且可以自定义创建某些其他过滤器以应用于其他属性。

| 搜索字段 | 搜索属性值 |
|-----------------|----------------------------------------------------------------------------------------------------------------------------------------|
| MIME 类型 | 图像、文档、多媒体、存档或其他。 |
| 上次修改时间 | “小时”、“天”、“周”、“月”或“年”。 |
| 文件大小 | “小”、“中”或“大”。 |
| 发布状态 | “已发布”或“已取消发布”。 |
| 批准状态 | “已批准”或“已拒绝”。 |
| 方向 | “水平”、“垂直”或“正方形”。 |
| 样式 | “彩色”或“黑白”。 |
| 视屏高度 | 指定为最小值和最大值。 值仅存储在视频演绎版的元数据中。 |
| 视频宽度 | 指定为最小值和最大值。 值仅存储在视频演绎版的元数据中。 |
| 视频格式 | DVI、Flash、MPEG4、MPEG、OGG Theora、QuickTime、Windows Media。 值会存储在源视频及任何演绎版的元数据中。 |
| 视频编解码器 | x264。 值仅存储在视频演绎版的元数据中。 |
| 视频比特率 | 指定为最小值和最大值。 值仅存储在视频演绎版的元数据中。 |
| 音频编解码器 | Libvorbis、Lame MP3、AAC编码。 值仅存储在视频演绎版的元数据中。 |
| 音频比特率 | 指定为最小值和最大值。 值仅存储在视频演绎版的元数据中。 |

## 使用资产搜索结果 {#aftersearch}

您可以对搜索的资产执行以下操作 [!DNL Experience Manager]:

* 查看元数据属性和其他信息。
* 下载一个或多个资产。
* 可使用桌面操作在桌面应用程序中打开这些资产。
* 创建智能收藏集。

### 对搜索结果排序 {#sort}

对搜索结果排序，以更快地发现所需的资产。 您可以在列表视图中对搜索结果进行排序，并且仅在选择 **[[!UICONTROL 文件]](#searchui)** 从 **[!UICONTROL 过滤器]** 的上界。 [!DNL Assets] 使用服务器端排序来快速对文件夹或搜索查询结果中的所有资产（无论数量多少）进行排序。 与客户端排序相比，服务器端排序提供更快、更准确的结果。

在列表视图中，您可以对搜索结果进行排序，就像对任意文件夹中的资产进行排序一样。 排序适用于这些列 — 名称、标题、状态、Dimension、大小、评级、使用情况、创建日期、修改日期、发布日期、工作流和签出。

有关排序功能的限制，请参阅 [限制](#limitations).

### 检查资产的详细信息 {#checkinfo}

您可以从搜索结果页面查看已搜索资产的详细信息。

要查看资产的所有元数据，请选择资产，然后单击 **[!UICONTROL 属性]** 中。

要检查对资产或资产版本历史记录的注释，请单击资产以打开大型预览。 打开左边栏中的时间轴，然后选择“ **[!UICONTROL 注释]** ”或“ **[!UICONTROL 版本]**”。 您还可以按时间顺序对时间轴活动（如注释或版本）进行排序。

![对搜索资产的时间轴条目进行排序](assets/sort_timeline_search_results.gif)

*图：对搜索资产的时间轴条目进行排序。*

### 下载搜索的资产 {#download}

您可以像从文件夹下载常规资产一样下载搜索的资产及其演绎版。 从搜索结果中选择一个或多个资产，然后单击 **[!UICONTROL 下载]** 中。

### 批量更新元数据属性 {#metadata-updates}

可以批量更新多个资产的常用元数据字段。 从搜索结果中，选择一个或多个资产。 单击 **[!UICONTROL 属性]** ，然后根据需要更新元数据。 单击 **[!UICONTROL 保存并关闭]** 完成时。 更新字段中以前存在的元数据将被覆盖。

对于单个文件夹或收藏集中可用的资产， [批量更新元数据](/help/assets/manage-metadata.md#manage-assets-metadata) ，而无需使用搜索功能。 对于跨文件夹提供的资产或符合常用条件的资产，通过搜索批量更新元数据会更快。

### 智能收藏集 {#smart-collections}

收藏集是一组有序的资产，这些资产可以包含来自不同位置的资产，因为收藏集仅包含对这些资产的引用。 收藏集有以下两种类型：

* 资产、文件夹和其他收藏集的静态引用列表。
* 动态列表（智能收藏集），可根据搜索条件填充收藏集中的资产。

您可以根据搜索条件创建智能收藏集。从&#x200B;**[!UICONTROL 过滤器]**&#x200B;面板中，选择&#x200B;**[!UICONTROL 文件]**，然后单击&#x200B;**[!UICONTROL 保存智能收藏集]**。请参阅[管理收藏集](/help/assets/manage-collections.md)。

## 意外的搜索结果和问题 {#unexpected-results}

<!--
**Partially related or unrelated search results**: Experience Manager may display seemingly partially related or unrelated assets, alongside the desired assets in the search results. If you enable Enhanced Smart Tags, the search behavior changes slightly. See how it changes [after smart tagging](#withsmarttags).
-->

| 错误、问题、症状 | 可能的原因 | 可能的问题修复或了解 |
|---|---|---|
| 搜索缺少元数据的资产时，结果不正确。 | 搜索缺少必需元数据的资产时， [!DNL Experience Manager] 可能会显示一些具有有效元数据的资产。 结果基于索引的元数据属性。 | 更新元数据后，需要重新编制索引，以反映资产元数据的正确状态。 请参阅 [必需元数据](metadata-schemas.md#define-mandatory-metadata). |
| 搜索结果过多。 | 广泛搜索参数。 | 考虑限制 [搜索范围](#scope). 使用智能标记可能会提供比预期更多的搜索结果。 请参阅 [使用智能标记搜索行为](#withsmarttags). |
| 无关或部分相关的搜索结果。 | 搜索行为会随智能标记而发生更改。 | 了解 [智能标记后的搜索更改](#withsmarttags). |
| 没有自动完成有关资产的建议。 | 尚未对新上传的资产建立索引。 当您开始在Omnisearch栏中键入搜索关键词时，元数据并非立即可用，因为提供了建议。 | [!DNL Experience Manager] 会等到超时时段（默认为一小时）到期，然后运行后台作业以索引所有新上传或更新的资产的元数据，然后将该元数据添加到建议列表中。 |
| 无搜索结果. | <ul><li>与查询匹配的资产不存在。 </li><li> 在搜索查询之前添加了空格。 </li><li> 不支持的元数据字段包含您搜索的关键词。</li><li> 在资产的非工作时间内进行搜索。 </li></ul> | <ul><li>使用其他关键词进行搜索。 或者，使用智能标记或相似度搜索来改进搜索结果。 </li><li>[已知限制](#limitations).</li><li>所有元数据字段均不考虑进行搜索。 请参阅 [范围](#scope).</li><li>稍后搜索或修改所需资产的按时和按时。</li></ul> |
| 搜索筛选器或谓词不可用。 | <ul><li>未配置搜索过滤器。</li><li>无法用于登录。</li><li>（不太可能）未在您使用的部署中自定义搜索选项。</li></ul> | <ul><li>请联系管理员以检查搜索自定义是否可用。</li><li>请联系管理员以检查您的帐户是否具有使用自定义设置的权限。</li><li>联系管理员并检查 [!DNL Assets] 正在使用的部署。</li></ul> |
| 在搜索视觉上相似的图像时，缺少预期的图像。 | <ul><li>图像在 [!DNL Experience Manager].</li><li>图像未编入索引。 通常，在最近上传时。</li><li>图像未智能标记。</li></ul> | <ul><li>将图像添加到 [!DNL Assets].</li><li>请与管理员联系以重新编入存储库索引。 此外，请确保您使用了相应的索引。</li><li>请联系您的管理员以智能标记相关资产。</li></ul> |
| 在搜索视觉上相似的图像时，会显示不相关的图像。 | 可视搜索行为。 | [!DNL Experience Manager] 显示尽可能多的潜在相关资产。 相关性较差的图像（如果有）会添加到结果中，但搜索排名会较低。 当您向下滚动搜索结果时，匹配项的质量和搜索资产的相关性会降低。 |
| 选择并运行搜索结果时，所有搜索的资产都不会运行。 | 的 [!UICONTROL 全选] 选项仅选择卡片视图中的前100个搜索结果和列表视图中的前200个搜索结果。 |  |

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 搜索实施指南](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/developing/search-tutorial-develop.html)
>* [用于提升搜索结果的高级配置](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/search-and-discovery/search-boost.html)
>* [配置智能翻译搜索](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/translation/smart-translation-search-technical-video-setup.html)

