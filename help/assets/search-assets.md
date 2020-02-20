---
title: 在AEM中搜索数字资产和图像
description: 了解如何使用“筛选器”面板在AEM中查找所需的资产，以及如何使用在搜索中显示的资产。
contentOwner: AG
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 7141e42f53c556c0ac21def6085182ef400f5a71

---


# 在AEM中搜索资产 {#search-assets-in-aem}

使用Experience Manager中用户友好的资产发现选项，您可以提高内容速度。 您的团队可以使用开箱即用的功能和自定义方法，通过无缝、智能的搜索体验缩短上市时间。 搜索资产是数字资产管理系统使用的核心——无论是供创意人员进一步使用、供商业用户和营销人员对资产进行可靠管理还是供DAM管理员管理。 您可以通过AEM资产用户界面或其他应用程序和界面执行的简单、高级和自定义搜索功能有助于完成这些使用案例。

AEM支持以下用例，本文介绍了这些用例的用法、概念、配置、限制和疑难解答。

| 搜索资产 | 配置和管理 | 处理搜索结果 |
|--- |--- |--- |
| [基本搜索](#searchbasics) | [搜索索引](#searchindex) | [排序结果](#sort) |
| [了解搜索UI](#searchui) |  | [检查资产的属性和元数据](#checkinfo) |
| [搜索建议](#searchsuggestions) | [强制元数据](#mandatorymetadata) | [下载](#download) |
| [了解搜索结果和行为](#searchbehavior) | [修改搜索彩块化](#searchfacets) | [批量元数据更新](#metadataupdates) |
| [搜索排名和提升](#searchrank) | [文本提取](#extracttextupload) | [智能收藏集](#collections) |
| [高级搜索：筛选和搜索范围](#scope) | [自定义谓词](#custompredicates) | [了解意外结果](#unexpectedresults) ，并进行疑难 [解答](#troubleshoot) |
| [从其他解决方案和应用程序中搜索](#beyondomnisearch):资 <br />产链 [接](#aal)<br />[接桌面应用程序](#desktopapp)<br />     [Adobe Stock图像](#adobestock)<br />     Dynamic [Media资产](#dynamicmedia) |  |  |
| [资产选择器／选取器](#assetselector) |  |  |
| [限制](#tips) 和提 [示](#limitations) |  |  |
| [插图示例](#samples) |  |  |

使用AEM web界面顶部的Omnisearch字段搜索资产。 转到 **[!UICONTROL AEM中的“资产]** ”>“文件”，单击顶 **[!UICONTROL 栏中的search_icon]**![](assets/do-not-localize/search_icon.png) ，输入search关键字，然后按回车键。 或者，使用关键字快 `/` 捷键（正斜杠）打开Omnisearch字段。 `Location:Assets` 已预选以将搜索限制为DAM资产。 您可以执行高级搜索以增加或限 [制搜索范围](#scope)。

使用“ **[!UICONTROL 筛选器]** ”面板搜索资产、文件夹、标记和元数据。 您可以根据各种选项（谓词）筛选搜索结果，如文件类型、文件大小、上次修改日期、资产状态、洞察数据和Adobe Stock许可。 您可以自定义“筛选器”面板，并使用搜索彩块化添加／删 [除搜索谓词](/help/assets/search-facets.md)。

AEM搜索功能支持搜索集合和搜索集合中的资产。 请参阅 [搜索集合](/help/assets/manage-collections.md)。

## 了解搜索界面 {#searchui}

熟悉搜索界面和可用的操作。

![](assets/aem_search_results.png) 了解资产搜索结果界面的各部分&#x200B;**&#x200B;图：了解资产搜索结果界面的各个部分

**** 答：将搜索另存为智能收藏集。 **** B.筛选器（谓词）以缩小搜索结果。 **C.在搜索结果中显示文件** 、文件夹或两者。 **** D.单击“过滤器”以打开或关闭左边栏。 **** E.搜索位置为DAM。 ************ F.包含用户提供的搜索关键字 **G的Omnisearch字段。选中此复选框可选择所有搜索**&#x200B;结果H。在总搜索结果 **I中显示的搜索结果数。关闭搜索** J。在卡片视图和列表视图之间切换

### 动态搜索彩块化 {#dynamicfacets}

您可以使用搜索彩块化中动态更新的预期搜索结果数量，从搜索结果页面更快地发现所需的资产。 预期的资产数量会在应用搜索筛选器之前进行更新。 查看筛选器的预期计数可帮助您快速、高效地浏览搜索结果。 有关详细信息，请参 [阅在AEM中搜索资产](/help/assets/search-assets.md)。

![无需筛选搜索彩块化中的搜索结果，即可查看资产的大致数量。](assets/asset_search_results_in_facets_filters.png)

无需筛选搜索彩块化中的搜索结果，即可查看资产的大致数量。

## Search suggestions as you type {#searchsuggestions}

开始键入关键字时，AEM会建议可能的搜索关键字或短语。 建议基于AEM中的资产。 AEM为所有元数据字段编制索引以帮助搜索。 为了提供搜索建议，系统使用以下几个元数据字段的值。 要提供搜索建议，请考虑使用适当的关键字填充以下字段：

* 资产标记。 (映射到 `jcr:content/metadata/cq:tags`)
* 资产标题。 (映射到 `jcr:content/metadata/dc:title`)
* 资产描述。 (映射到 `jcr:content/metadata/dc:description`)
* JCR存储库中的标题。 该值可能会映射到资产标题。 (映射到 `jcr:content/jcr:title`)
* JCR存储库中的说明。 该值可能会映射到资产描述。 (映射到 `jcr:content/jcr:description`)

## 了解搜索结果和行为 {#searchbehavior}

### 基本搜索词和结果 {#searchbasics}

您可以从OmniSearch字段运行关键字搜索。 关键字搜索不区分大小写，并且是全文搜索（跨常用元数据字段）。 如果使用了多个关键字，则 `AND` 是关键字之间的默认运算符。 结果按相关性排序，以最接近的匹配项开始。 对于多个关键字，更具相关性的结果是在元数据中包含这两个术语的资产。 在元数据中，显示为智能标记的关键字的排名高于其他元数据字段中显示的关键字。

AEM允许为特定搜索词赋予更高的权重。 此外，还可以提升特定搜索词的少数目标资产的排名。 AEM管理员可以按如下所述执行这些配置。

为了快速找到相关资产，富界面提供了筛选、排序和选择机制。 您可以根据多个条件筛选结果，并查看为各种筛选器搜索的资产数量。 或者，您也可以通过在“Omnisearch”（搜索）字段中更改查询来重新运行搜索。 当您更改搜索词或筛选器时，其他筛选器仍会被应用，以保留搜索的上下文。

有时，您可能会在搜索结果中看到一些意外的资产。 有关详细信息，请参阅 [意外的结果](#unexpectedresults)。

AEM可以搜索多种文件格式，并且可以自定义搜索筛选器以满足您的业务需求。 请与管理员联系，了解DAM存储库中有哪些可用的搜索选项以及登录可能受到哪些限制。

<!-- 
### Results with and without Enhanced Smart Tags {#withsmarttags}

By default, AEM search combines the search terms with an AND clause. For example, consider searching for keywords woman running. Only the assets with both woman and running keywords in the metadata appear in the search results by default. The same behavior is retained when special characters (periods, underscores, or dashes) are used with the keywords. The following search queries return the same results:

* `woman running`
* `woman.running`
* `woman-running`

However, the query `woman -running` returns assets without `running` in their metadata.
Using smart tags adds an extra `OR` clause to find any of the search terms as the applied smart tags. An asset tagged with either `woman` or `running` using Smart Tags also appear in such a search query. So the search results are a combination of,

* Assets with `woman` and `running` keywords in the metadata (default behavior).

* Assets smart tagged with either of the keywords (Smart Tags behavior).
-->

### 搜索排名和提升 {#searchrank}

首先显示与元数据字段中的所有搜索词匹配的搜索结果，然后显示与智能标记中的任意搜索词匹配的搜索结果。 在上例中，搜索结果的显示大致顺序为：

1. 各个元 `woman running` 数据字段中的匹配项。
1. 智能标 `woman running` 记中的匹配项。
1. 智能标 `woman` 记的匹 `running` 配项或匹配项。

您可以提高特定资产的关键字的相关性，以帮助根据关键字提升搜索。 换句话说，当您基于这些关键字进行搜索时，您为其提升特定关键字的图像将显示在搜索结果顶部。

1. 从资产用户界面中，打开资产的属性页面。 单击 **[!UICONTROL 高级]** ，然后单击／点按Elevate下 **[!UICONTROL 的]****[!UICONTROL 添加以获取搜索关键字]**。
1. 在“搜 **[!UICONTROL 索提升]** ”框中，指定要提升图像搜索的关键字，然后单击／点按添 **[!UICONTROL 加]**。 可以以相同的方式指定多个关键字。
1. 单击／点按保 **[!UICONTROL 存并关闭]**。 您为此关键字提升的资产会显示在顶级搜索结果中。

您可以通过提升目标关键字的搜索结果中某些资产的排名来利用此功能。 请观看以下视频示例。 有关详细信息，请参 [阅在AEM中搜索](https://helpx.adobe.com/experience-manager/kt/help/assets/search-feature-video-use.html)。

>[!VIDEO](https://video.tv.adobe.com/v/16766/?quality=6)

*了解搜索结果的排名方式以及排名如何受到影响。*

## Advanced search {#scope}

AEM提供了各种方法，如应用于已搜索资产的筛选器，以帮助您更快地找到所需的资产。 下面介绍了一些常用的方法。 下面 [分享了一些图示](#samples) 。

**搜索文件或文件夹**:在搜索结果中，可查看文件、文件夹或两者。 从“ **[!UICONTROL 滤镜]** ”面板中，可以选择相应的选项。 请参阅 [搜索界面](#searchui)。

**在文件夹内搜索资产**:您可以将搜索限制为特定文件夹。 在“筛 **[!UICONTROL 选器]** ”面板中，添加文件夹的路径。 一次只能选择一个文件夹。

![通过在“筛选器”面板中添加文件夹路径，将搜索结果限制在文件夹中](assets/search_folder_select.gif)

通过在“筛选器”面板中添加文件夹路径，将搜索结果限制在文件夹中

<!--
### Find similar images {#visualsearch}

To find images that are visually similar to a user-selected image, click **[!UICONTROL Find Similar]** option from the card view of an image or from the toolbar. AEM displays the smart tagged images from the DAM repository that are similar to a user-selected image. See [how to configure similarity search](#configvisualsearch).

![Find similar images using the option in the card view](assets/search_find_similar.png)
*Figure: Find similar images using the option in the card view*
-->

### Adobe Stock图像 {#adobestock}

在AEM用户界面中，用户可以搜索 [Adobe Stock资产](/help/assets/aem-assets-adobe-stock.md) ，并许可所需的资产。 添加 `Location: Adobe Stock` 到Omnisearch栏中。 您还可以使用“筛选器”面板查找所有授权或未授权的资源，或使用Adobe Stock文件号搜索特定资源。

### Dynamic media资产 {#dmassets}

可以通过从“滤镜”面板中选择“Dynamic Media” **[!UICONTROL >“集”]** ，对Dynamic media图像进 **[!UICONTROL 行筛选]** 。 它过滤和显示图像集、轮盘、混合媒体集和旋转集等资产。

### 使用元数据字段中的特定值进行搜索 {#gqlsearch}

您可以根据特定元数据字段的确切值（如标题、说明和作者）来对资产进行处理。 GQL全文搜索功能只获取其元数据值与您的搜索查询完全匹配的资产。 属性的名称（例如，作者、标题等）和值区分大小写。

| 元数据字段 | Facet值和用法 |
|---|---|
| 标题 | title:John |
| 创建者 | creator:John |
| 位置 | 位置：NA |
| 描述 | description:&quot;Sample Image&quot; |
| 创建程序工具 | creatortool:“Adobe Photoshop CC 2015” |
| 版权所有者 | copyrightowner:&quot;Adobe Systems&quot; |
| 参与者 | contributor:John |
| 使用条款 | usageterms:&quot;CopyRights Reserved&quot; |
| 创建时间 | created:YYYY-MM-DDTHH |
| 过期日期 | expires:YYYY-MM-DDTHH |
| 开始时间 | ontime:YYYY-MM-DDTHH |
| 结束时间 | offtime:YYYY-MM-DDTHH |
| 时间范围（过期日期、开始时间、结束时间） | facet字段：下界……上界 |
| 路径 | /content/dam/&lt;folder name> |
| PDF 标题 | pdftitle:&quot;Adobe Document&quot; |
| 主题 | subject:&quot;Training&quot; |
| 标记 | tags:&quot;Location And Travel&quot; |
| 类型 | type:&quot;image\png&quot; |
| 图像宽度 | width:lowerbound..上界 |
| 图像高度 | height:lowerbound..上界 |
| 人员 | person:John |

属性路径、限制、大小和排序依据不能与任何其他属性一起使用。

用户生成的属性的关键字是属性编辑器中的字段标签（以小写形式），并删除了空格。

以下是复杂查询的一些搜索格式示例：

* To display all assets with multiple facets fields (for example: title=John Doe and creator tool = Adobe Photoshop): `title:"John Doe" creatortool : Adobe*`
* To display all assets when the facets value is not a single word but a sentence (for example: title=Scott Reynolds): `title:"Scott Reynolds"`
* To display assets with multiple values of a single property (for example: title=Scott Reynolds or John Doe): `title:"Scott Reynolds" OR "John Doe"`
* To display assets with property values starting with a specific string (for example: title is Scott Reynolds): `title:Scott*`
* To display assets with property values ending with a specific string (for example: title is Scott Reynolds): `title:*Reynolds`
* To display assets with a property value that contains a specific string (for example: title = Basel Meeting Room): `title:*Meeting*`
* To display assets that contain a particular string and have a specific property value (for example: search for string Adobe in assets having title=John Doe): `*Adobe* title:"John Doe"`

## 从其他AEM产品或界面搜索资产 {#beyondomnisearch}

Adobe Experience Manager(AEM)将DAM存储库连接到各种其他AEM解决方案，以便更快地访问数字资产并简化创意工作流程。 任何资产搜索都以浏览或搜索开始。 搜索行为在不同的表面和解决方案上基本保持不变。 某些搜索方法会随目标受众、用例和用户界面的不同而改变，这些方法会因AEM解决方案而异。 下面的链接介绍了各个解决方案的具体方法。 本文介绍了普遍适用的提示和行为。

### 从Adobe Asset link面板搜索资产 {#aal}

使用Adobe Asset Link，创意专业人士现在可以访问存储在AEM资产中的内容，而无需离开受支持的Adobe Creative cloud应用程序。 创意人员可以使用Creative cloud应用程序中的应用程序内面板无缝地浏览、搜索、注销和登记资产：Photoshop、Illustrator和InDesign。 资产链接还允许用户搜索视觉效果相似的结果。 视觉搜索显示结果由Adobe Sensei的机器学习算法提供支持，并帮助用户查找美学上相似的图像。 请参 [阅使用Adobe资产链接搜索](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html#UseAdobeAssetLink) 和浏览资产。

### 在AEM桌面应用程序中搜索资产 {#desktopapp}

创意专业人士使用桌面应用程序使AEM资产可轻松搜索并在其本地桌面（Win或Mac）上可用。 创意人员可以在Mac finder或Windows资源管理器中轻松显示所需的资产，在桌面应用程序中打开并在本地更改——这些更改将保存回AEM并在存储库中创建了新版本。 应用程序支持使用一个或多个关键字*和？进行基本搜索 通配符和AND运算符。 请参 [阅在桌面应用程序中浏览、搜索和预览](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html#browse-search-preview-assets) 资源。

### Search assets in Brand Portal {#brandportal}

业务线用户和营销人员使用Brand Portal与其扩展的内部团队、合作伙伴和经销商高效、安全地共享获准的数字资产。 See [search assets on Brand Portal](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/search-capabilities/brand-portal-searching.html).

### 搜索Adobe Stock图像 {#adobestock-1}

从AEM用户界面中，用户可以搜索Adobe Stock资产并许可所需的资产。 添加 `Location: Adobe Stock` 到Omnisearch字段。 您还可以使用“ **[!UICONTROL 筛选器]** ”面板查找所有授权或未授权的资源，或使用Adobe Stock文件号搜索特定资源。 请参 [阅在AEM中管理Adobe Stock图像](/help/assets/aem-assets-adobe-stock.md#usemanage)。

### 搜索Dynamic media资产 {#dynamicmedia}

您可以通过从“滤镜”面板中选择“Dynamic Media **[!UICONTROL ”>“集”来筛选Dynamic Media]** 图像 **[!UICONTROL ，以]** 便对其进 **[!UICONTROL 行筛选]** 。 它过滤和显示图像集、轮盘、混合媒体集和旋转集等资产。 在创作网页时，作者可以在内容查找器中搜索集。 弹出菜单中提供集的过滤器。

### 在创作网页时在内容查找器中搜索资产 {#contentfinder}

作者可以使用内容查找器在DAM存储库中搜索相关资产，并在他们创建的网页中使用资产。

<!-- Authors can also use the Connected Assets functionality to search for assets that are available on a remote AEM deployment. Authors can then use these assets in web pages on a local AEM deployment. See [use remote assets](use-assets-across-connected-assets-instances.md#use-remote-assets).
-->

### 搜索集合 {#collections}

AEM搜索功能支持搜索集合和搜索集合中的资产。 请参阅 [搜索集合](/help/assets/manage-collections.md)。

## Asset selector {#assetselector}

资产选择器允许您以特殊方式搜索、筛选和浏览DAM资产。 资产选择器在上可用 `https://[aem_server]:[port]/aem/assetpicker.html`。 您可以使用资产选择器提取您选择的资产的元数据。 您可以使用支持的请求参数启动它，例如资产类型（图像、视频、文本）和选择模式（单选或多选）。 这些参数为特定搜索实例设置资产选择器的上下文，并在整个选择过程中保持不变。

资产选择器使用HTML5消 `Window.postMessage` 息将选定资产的数据发送给收件人。 资产选择器基于Granite的基础选取器词汇。 默认情况下，资产选择器在浏览模式下操作。

您可以在URL中传递以下请求参数，以在特定上下文中启动资产选择器：

| 名称 | 值 | 示例 | 用途 |
|---|---|---|---|
| 资源后缀(B) | 作为URL中资源后缀的文件夹路径：[https://localhost:4502/aem/assetpicker.html/&lt;folder_path>](https://localhost:4502/aem/assetpicker.html) | 要启动资产选择器并选择特定文件夹（例如，选择了文件夹/content/dam/we-retail/cn/activities）,URL应为以下格式： [https://localhost:4502/aem/assetpicker.html/content/dam/we-retail/en/activities?assettype=images](https://localhost:4502/aem/assetpicker.html/content/dam/we-retail/en/activities?assettype=images) | 如果在启动资产选择器时需要选择某个特定文件夹，请将其作为资源后缀进行传递。 |
| 模式 | 单个，多个 | [https://localhost:4502/aem/assetpicker.html?mode=multiplehttps://localhost:4502/aem/assetpicker.html?mode=single](https://localhost:4502/aem/assetpicker.html?mode=multiplehttps://localhost:4502/aem/assetpicker.html?mode=single) | 在多个模式中，您可以使用资产选择器同时选择多个资产。 |
| mimetype | 资产的mimetype(s)(`/jcr:content/metadata/dc:format`)（也支持通配符） | <ul><li>[https://localhost:4502/aem/assetpicker.html?mimetype=image/png](https://localhost:4502/aem/assetpicker.html?mimetype=image/png)</li><li>[https://localhost:4502/aem/assetpicker.html?mimetype=*png](https://localhost:4502/aem/assetpicker.html?mimetype=*png)</li><li>[https://localhost:4502/aem/assetpicker.html?mimetype=*presentation](https://localhost:4502/aem/assetpicker.html?mimetype=*presentation)</li><li>[https://localhost:4502/aem/assetpicker.html?mimetype=*presentation&amp;mimetype=*png](https://localhost:4502/aem/assetpicker.html?mimetype=*presentation&mimetype=*png)</li></ul> | 使用它根据MIME类型筛选资产 |
| 对话框 | true,false | [https://localhost:4502/aem/assetpicker.html?dialog=true](https://localhost:4502/aem/assetpicker.html?dialog=true) | 使用这些参数以Granite对话框的形式打开资产选择器。 仅当您通过Granite路径字段启动资产选择器并将其配置为pickerSrc URL时，此选项才适用。 |
| assettype(S) | 图像，文档，多媒体，存档 | <ul><li>[https://localhost:4502/aem/assetpicker.html?assettype=images](https://localhost:4502/aem/assetpicker.html?assettype=images)</li><li>[https://localhost:4502/aem/assetpicker.html?assettype=documents](https://localhost:4502/aem/assetpicker.html?assettype=documents)</li><li>[https://localhost:4502/aem/assetpicker.html?assettype=multimedia](https://localhost:4502/aem/assetpicker.html?assettype=multimedia)</li><li>[https://localhost:4502/aem/assetpicker.html?assettype=archives](https://localhost:4502/aem/assetpicker.html?assettype=archives)</li></ul> | 使用此选项可根据传递的值筛选资产类型。 |
| 根 | &lt;folder_path> | [https://localhost:4502/aem/assetpicker.html?assettype=images&amp;root=/content/dam/we-retail/en/activities](https://localhost:4502/aem/assetpicker.html?assettype=images&root=/content/dam/we-retail/en/activities) | 使用此选项可指定资产选择器的根文件夹。 在这种情况下，资产选择器允许您仅选择根文件夹下的子资产（直接／间接）。 |

要访问资产选择器界面，请转到 `https://[AEM server]:[port]/aem/assetpicker`。 导航到所需的文件夹，然后选择一个或多个资产。 或者，从Omnisearch框中搜索所需的资产，根据需要应用筛选器，然后选择它。

![在资产选取器中浏览并选择资产](assets/assetpicker.png)

在资产选取器中浏览并选择资产

## 限制 {#limitations}

AEM资产中的搜索功能有以下限制：

* 请勿在搜索查询中输入前导空间，否则搜索不起作用。
* 在您从搜索结果中选择资产的属性，然后取消搜索后，AEM可能会继续显示搜索词(CQ-4273540)。
* 搜索文件夹或文件和文件夹时，无法对任何参数对搜索结果进行排序。
* 如果按回车键时未关联Omnisearch栏中的任何内容，AEM将返回仅包含文件而非文件夹的列表。 如果您在不使用关键字的情况下专门搜索文件夹，则AEM不会返回任何结果。

视觉搜索或相似性搜索具有以下限制：

* 视觉搜索最适合于较大的存储库。 虽然没有达到最佳效果所需的最少图像数，但与一些图像匹配的质量可能不如来自大型存储库的匹配质量好。
* 您无法更改模型或培训AEM以查找类似图像。 例如，向一些资产添加或删除智能标记不会更改模型。 资产确实会从视觉上相似的搜索结果中排除。

## 搜索提示 {#tips}

* 在监视资产的审核状态时，请使用相应的选项来查找已批准的资产或待批准的资产。
* 使用“分析”谓词，根据从各种Creative应用程序获取的资产使用情况统计信息搜索受支持的资产。 使用情况数据按使用情况得分、印象、点击量和资产显示类别的媒体渠道进行分组。
* 使用复选框选择所有搜索结果或筛选的搜索结果，以便对选定内容进行操作。 无论当前用户视图中显示的资产数量如何，系统会选择所有已搜索的资产。 例如，您可以下载所有选定的资产，批量更新所有选定资产的元数据属性，或将选定的资产添加到收藏集。
* 要搜索不包含强制元数据的资产，请参阅强制 [元数据](#mandatorymetadata)。
* 搜索使用所有元数据字段。 通常，搜索12等通用搜索会返回许多结果。 为获得更好的效果，请使用双引号（非单引号）或确保数字与没有特殊字符的单词相邻(例如 *shoe12*)。
* 全文搜索支持-、^等运算符。 要将这些字母作为字符串文本搜索，请将搜索表达式括在双引号中。 例如，使用“Notebook - Beauty”（笔记本——美容）而不是“Notebook - Beauty”（笔记本——美容）。
* 如果搜索结果过多，请将所 [需资产的搜索范围](#scope) 限制为零。 当您了解如何更好地查找所需的资产（例如，特定文件类型、特定位置、特定元数据等）时，它最适合使用。

* **标记**:标记可帮助您对可以更高效地浏览和搜索的资产进行分类。 标记有助于将相应的分类传播到其他用户和工作流。 AEM提供了使用Adobe Sensei的人工智能服务自动标记资产的方法，这些方法通过使用和培训不断改进对资产的标记功能。 在搜索资产时，如果帐户中启用了该功能，则智能标记会被纳入其中。 它与内置的搜索功能一起使用。 请参阅 [搜索行为](#searchbehavior)。 要优化搜索结果的显示顺序，您可以提 [升几个选定资产的](#searchrank) 搜索排名。

* **索引**:搜索结果中只返回已索引的元数据和资产。 为获得更好的覆盖面和性能，请确保正确的索引并遵循最佳做法。 请参阅 [索引](#searchindex)。

## 说明搜索的一些示例 {#samples}

在关键字周围使用双引号，以按用户指定的确切顺序查找包含确切短语的资产。

![带引号和不带引号的搜索行为](assets/search_with_quotes.gif)

带引号和不带引号的搜索行为

**使用星号通配符搜索**:要扩大搜索范围，请在搜索单词前后使用星号来匹配任意数量的字符。 例如，搜索不带星号的运行不会返回包含该单词任何变体（包括在元数据中）的资产。 星号可替代任意数量的字符。 例如，

* `run` 返回具有精确运行关键字的资产
* `run*` 返回资产，包括运行、运行、失控等。
* `*run` 返回结束、重新运行等。
* `*run*` 返回所有可能的组合。

![使用示例说明在资产搜索中使用星号通配符](assets/search_with_asterisk_run.gif)

使用示例说明在资产搜索中使用星号通配符

**使用问号通配符搜索**:要扩大搜索范围，请使用一个或多个“?” 字符以匹配字符数。 例如，在下图中，

* `run???` 查询与任何资产均不匹配。

* `run????` query将单词与后 `running` 面四个字符匹配 `run`。

* `??run` query匹配前面带 `rerun` 有两个字符的单词 `run`。

![通过示例说明在资产搜索中使用问号通配符的方法](assets/search_with_questionmark_run.gif)

通过示例说明在资产搜索中使用问号通配符的方法

**排除关键字**:使用虚线搜索不包含关键字的资产。 例如，查 `running -shoe` 询会返回包含但不 `running`包含的资产 `shoe`。 同样， `camp -night` 查询也会返回包含但不 `camp` 包含的资 `night`产。 请注意， `camp-night` 查询将返回同时包含和的 `camp` 资产 `night`。

![使用虚线搜索不包含被排除关键字的资产](assets/search_dash_exclude_keyword.gif)*图：使用虚线搜索不包含被排除关键字的资产*

<!--
## Configuration and administration tasks related to search functionality {#configadmin}

### Search index configurations {#searchindex}

Asset discovery relies on indexing of DAM contents, including the metadata. Faster and accurate asset discovery relies on optimized indexing and appropriate configurations. See [indexing](/help/operations/indexing.md).

### Sort on Name column {#sortbyname}

In list view, you can sort the search results just as you can sort assets in any folder. Sorting does not work on the `Name` column by default. To sort by the `Name` column, overlay `/libs/dam/gui/content/commons/availablecolumns` and change the value of sortable to `True`.

<!--
### Visual or similarity search {#configvisualsearch}

Visual search uses smart tagging and requires AEM 6.5.2.0 or later. After configuring smart tagging functionality, follow these steps.

1. In AEM CRXDE, in `/oak:index/lucene` node, add the following properties and values and save the changes.

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
1. Apply Smart Tags to the assets in your AEM repository. See [how to configure smart tags](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/metadata/smart-tags-technical-video-setup.html).
1. In CRXDE, in `/oak-index/damAssetLucene` node, set the `reindex` property to `true`. Save the changes.
1. (Optional) If you have customized search form then copy the `/libs/settings/dam/search/facets/assets/jcr%3Acontent/items/similaritysearch` node to `/conf/global/settings/dam/search/facets/assets/jcr:content/items`. Save all the changes.

For related information, see [understand smart tags in AEM](https://helpx.adobe.com/experience-manager/kt/help/assets/smart-tags-feature-video-understand.html) and [how to manage smart tags](/help/assets/smart-tags.md).

-->
<!--

### Mandatory metadata {#mandatorymetadata}

Business users, administrators, or DAM librarians can define some metadata as mandatory metadata that is a must for the business processes to work. For various reasons, some assets may be missing this metadata, such as legacy assets or assets migrated in bulk. Assets with missing or invalid metadata are detected and reported based on the indexed metadata property. To configure it, see [mandatory metadata](/help/assets/metadata-schemas.md#defining-mandatory-metadata).

### Modify search facets {#searchfacets}

To improve the speed of discovery, AEM Assets offers search facets using which you can filter the search results. The Filters panel includes a few standard facets by default. Administrators can customize the Filters panel to modify the default facets using the in-built predicates. AEM provides a good collection of in-built predicates and an editor to customize the facets. See [search facets](/help/assets/search-facets.md).

### Extract text when uploading assets {#extracttextupload}

You can configure AEM to extract the text from the assets when users upload assets, such as PSD or PDF files. AEM indexes the extracted text and helps users search these assets based on the extracted text. See [upload assets](/help/assets/manage-digital-assets.md#uploading-assets).

<!-- Check with gklebus if this customization is possible in Cloud Service now

### Custom predicates to filter search results {#custompredicates}

Predicates are used to create facets. Administrators can customize the search facets in the Filters panel using pre-configured predicates. These predicates can be customized using overlays. See [create custom predicates](/help/assets/searchx.md).

You can search for digital assets based on one or more of the following properties. Filters that apply on some of these properties are available by default and some other filters can be custom-created to apply on the other properties.

| Search field | Search property values |
|---|---|
| MIME Types | Images, Documents, Multimedia, Archives, or Other. |
| Last Modified | Hour, Day, Week, Month, or Year. |
| File Size | Small, Medium, or Large. |
| Publish Status | Published or Unpublished. |
| Approved Status | Approved or Rejected. |
| Orientation | Horizontal, Vertical, or Square. |
| Style | Color, or Black & White. |
| Video Height | Specified as a minimum and maximum value. Value is stored in the metadata of video renditions only. |
| Video Width | Specified as a minimum and maximum value. Value is stored in the metadata of video renditions only. |
| Video Format | DVI, Flash, MPEG4, MPEG, OGG Theora, QuickTime, Windows Media. Value is stored in the metadata of the source video and any renditions. |
| Video Codec | x264. Value is stored in the metadata of video renditions only. |
| Video Bitrate | Specified as a minimum and maximum value. Value is stored in the metadata of video renditions only. |
| Audio Codec | Libvorbis, Lame MP3, AAC Encoding. Value is stored in the metadata of video renditions only. |
| Audio Bitrate | Specified as a minimum and maximum value. Value is stored in the metadata of video renditions only. |

-->

## 使用资产搜索结果 {#aftersearch}

当您看到一些已搜索的资产符合您的条件时，您可以执行以下典型任务，或对这些搜索结果执行以下操作：

* 查看元数据属性和其他信息。
* 下载一个或多个资源。
* 使用“桌面操作”在桌面应用程序中打开这些资产。
* 创建智能收藏集。

### 对搜索结果进行排序 {#sort}

对搜索结果排序可帮助您更快地发现所需的资产。 对搜索结果排序仅在列表视图中有效，并且仅在您从“筛选器 **[!UICONTROL [”面板](#searchui)]**中选择“**[!UICONTROL &#x200B;文件&#x200B;]**”时有效。 AEM资产使用服务器端排序来快速对某个文件夹或搜索查询结果中的所有资产（无论数量多少）进行排序。 与客户端排序相比，服务器端排序提供更快、更准确的结果。

在列表视图中，您可以像对任意文件夹中的资产进行排序一样对搜索结果进行排序。 排序适用于这些列——标题、状态、维度、大小、等级、使用情况、（修改日期）、（发布日期）、工作流和签出。

请参 [阅配置“名称”列的排序](#sortbyname)。 有关排序功能的限制，请参 [阅限制](#limitations)。

### 检查资产的详细信息 {#checkinfo}

您可以从搜索结果页面检查已搜索资产的详细信息。

要查看资产的所有元数据，请选择资产，然后单击工 **[!UICONTROL 具栏中]** 的属性。

要检查对资产或资产版本历史记录的注释，请单击资产以打开大型预览。 打开左边栏中的时间轴，然后选择“ **[!UICONTROL 注释]** ”或“ **[!UICONTROL 版本]**”。 您还可以按时间顺序对时间轴活动（如注释或版本）进行排序。

![对搜索资产的时间轴条目进行排序](assets/sort_timeline_search_results.gif)

对搜索资产的时间轴条目进行排序

### 下载搜索的资源 {#download}

您可以像从文件夹下载常规资产一样下载搜索的资产及其演绎版。 从搜索结果中选择一个或多个资产，然后单击工 **[!UICONTROL 具栏中]** 的下载。

### 批量更新元数据属性 {#metadataupdates}

可以批量更新多个资产的公用元数据字段。 从搜索结果中，选择一个或多个资产。 单击 **[!UICONTROL 工具栏中]** “属性”，然后根据需要更新元数据。 完成 **[!UICONTROL 后，单击“保存并关闭]** ”。 更新的字段中以前存在的元数据将被覆盖。

对于单个文件夹或集合中可用的资产，可更轻松地批 [量更新元数据](/help/assets/manage-metadata.md#manage-assets-metadata)。 对于跨文件夹可用或符合通用标准的资产，通过搜索批量更新元数据会更快。

### 智能收藏集 {#collections-1}

收藏集是一组有序的资产，可以包含来自不同位置的资产，因为收藏集只包含对这些资产的引用。 集合有以下两种类型：

* 资产、文件夹和其他收藏集的静态引用列表。
* 一个动态列表（智能收藏集），它根据搜索条件填充收藏集中的资产。

您可以根据搜索条件创建智能收藏集。 从“滤 **[!UICONTROL 镜]** ”面板中，选择“ **[!UICONTROL 文件]** ” **[!UICONTROL ，然后单击“]**&#x200B;保存智能收藏集”。 请参阅 [管理集合](/help/assets/manage-collections.md)。

## 意外的搜索结果 {#unexpectedresults}

**搜索缺少的元数据**:在搜索缺少必需元数据的资产时，AEM可能会显示一些具有有效元数据的资产。 会根据索引元数据属性检测并报告缺失的元数据。 即使资产元数据已修复，但在重新构建索引之前，它仍会继续显示为缺失的元数据。 请参阅 [必填元数据](/help/assets/metadata-schemas.md#defining-mandatory-metadata)。

**搜索结果过多**:为避免搜索结果过多，请考虑限制搜索结果。 例如，要在DAM中搜索资产，请在Omnisearch栏中 `Location:Assets` 进行选择。 有关更多搜索筛选器，请参 [阅搜索范围](#scope)。

<!-- Another reason to get more than expected search results can be use of smarts tags. See [search behavior with smart tags](#withsmarttags). 
-->

<!--
**Partially related or unrelated search results**: AEM may display seemingly partially related or unrelated assets, alongside the desired assets in the search results. If you enable Enhanced Smart Tags, the search behavior changes slightly. See how it changes [after smart tagging](#withsmarttags).
-->

**对于新上传的资产，没有自动完成建议**:当您开始在Omnisearch栏中键入搜索关键字时，最近上传的资产的元数据（标题、标记等）不会立即作为建议可用。 AEM资产会等到超时期（默认为一小时）到期后再运行后台作业，为所有新上传或更新的资产索引元数据，然后将元数据添加到建议列表。

**无搜索结果**:如果AEM显示空页面用于搜索查询，则以下可能是原因：

* 不存在与您的查询匹配的资产。
* 在搜索查询前添加空白。 这是已知 [的限制](#limitations)。

* 不支持的元数据字段包含您搜索的关键字。 并非所有元数据字段都会用于搜索。 请参阅 [范围](#scope)。
* 为资产配置了开启时间和结束时间，并在资产的结束时间内进行搜索。

**搜索筛选器／谓词不可用**:如果用户界面上没有搜索筛选器的预期自定义功能，请与管理员联系以检查是否已针对所有作者以及在所使用的生产服务器上实现自定义功能。 可能配置不正确。

## 搜索相关问题疑难解答 {#troubleshoot}

请参阅以下问题和可能的操作过程：

* 如果未显示预期的搜索筛选器／谓词，请与您的管理员联系。
* 在搜索视觉上相似的图像时，有时搜索结果中可能缺少预期的图像。 检查此类资产是否已编制索引并添加智能标记。
* 在搜索视觉上相似的图像时，有时在搜索结果中可能显示看似无关的图像。 AEM会显示尽可能多的潜在相关资产。 相关性较差的图像（如果有）会添加到结果中，但搜索级别较低。 当您向下滚动搜索结果时，搜索资产的匹配质量和相关性会降低。
