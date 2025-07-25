---
title: 在AEM中引入用于数字资产管理的Assets as a Cloud Service
description: 在AEM中引入用于数字资产管理的Assets as a Cloud Service
source-git-commit: 707c2125b3a5401cd5b0ebe19f3bc9c46302b697
workflow-type: tm+mt
source-wordcount: '5032'
ht-degree: 29%

---


# 在AEM中引入用于数字资产管理的Assets as a Cloud Service {#assets-as-cloud-service-digital-asset-management-aem}

Adobe Experience Manager Assets as a Cloud Service 为企业提供了云原生的 PaaS 解决方案，不仅可用于快速执行其数字资源管理和 Dynamic Media 运营来实现影响力，而且还可在始终最新、始终可用和不断学习的系统中使用新一代智能功能，例如 AI/ML。

Adobe 为您提供强大的数字资源管理（DAM）解决方案，让您能够充分利用数字资源。 Adobe Experience Manager Assets具有两种单独的体验，它们使用相同的Cloud Services存储库来满足您的要求。 有关AEM Assets基于角色的体验的信息，请参阅[数字资产管理可用的基于角色的体验](#persona-based-experiences)。

有关AEM Assets Ultimate和AEM Assets Prime产品的信息，请参阅[Assets as a Cloud Service Ultimate](/help/assets/assets-ultimate-overview.md)和[Assets as a Cloud Service Prime](/help/assets/assets-prime.md)。

Adobe的数字资产管理的一些主要功能包括：

![添加标记](assets/aem-assets-features-landing-page.png)


>[!BEGINTABS]

>[!TAB 资源引入]

## 资源引入 {#asset-ingestion}

使用批量导入功能将大量资源直接从数据源(如Azure、AWS、Google Cloud、Dropbox和OneDrive)导入Assets as a Cloud Service。

您可以使用管理员视图或Assets视图执行批量导入操作。 与管理员视图相比，Assets视图提供了更多数据源选项。

除了Web浏览器用户界面外，Experience Manager还支持桌面上的其他客户端。 它们还提供了上传体验，无需转至Web浏览器。

* Adobe Asset Link允许从Adobe Photoshop、Adobe Illustrator和Adobe InDesign桌面应用程序中的Experience Manager访问资源。 您可以从这些桌面应用程序中直接从Experience Manager Asset Link用户界面将当前打开的文档上传到Adobe。

* Experience Manager桌面应用程序可简化在桌面上使用资产的过程，而与资产的文件类型或处理这些资产的本机应用程序无关。 从本地文件系统上传嵌套文件夹层次结构中的文件很有用，因为浏览器上传仅支持上传平面文件列表。

使用这些链接可访问有关这些资产摄取工具的详细文档：

<table>
<td>
   <a href="/help/assets/bulk-import-assets-view.md">
   <img alt="批量导入工具" src="./assets/bulk-images.jpeg" />
   </a>
   <div>
      <a href="/help/assets/bulk-import-assets-view.md">
      <strong>使用批量导入工具</strong>
      </a>
   </div>
   <p>
      <em>了解如何直接从数据源导入大量资源</em>
   </p>
</td>


<td>
   <a href="https://experienceleague.adobe.com/zh-hans/docs/experience-manager-desktop-app/using/using">
   <img alt="使用AEM桌面应用程序" src="./assets/desktop-app-upload.jpeg" />
   </a>
   <div>
      <a href="https://experienceleague.adobe.com/zh-hans/docs/experience-manager-desktop-app/using/using">
      <strong>使用AEM桌面应用程序</strong>
      </a>
   </div>
   <p>
      <em>了解如何使用AEM桌面应用程序从本地文件系统上传嵌套文件夹层次结构中的文件。</em>
   </p>
</td>
<td>
   <a href="https://helpx.adobe.com/cn/enterprise/using/adobe-asset-link.html">
   <img alt="使用 Adobe Asset Link" src="./assets/adobe-asset-link.jpeg" />
   </a>
   <div>
      <a href="https://helpx.adobe.com/cn/enterprise/using/adobe-asset-link.html">
      <strong>使用Adobe Asset Link</strong>
      </a>
   </div>
   <p>
      <em>了解如何使用Creative Cloud应用程序将资源上传到Experience Manager。</em>
   </p>
</td>
</table>

>[!TAB AI支持的功能]

**智能标记**：智能标记使用Adobe Sensei的人工智能框架根据您的标记结构和业务分类培训其图像识别算法。 然后，此内容智能可用于将相关标记应用到其他资产集。 默认情况下，AEM会自动将智能标记应用于上传的资源。

**基于颜色的智能标记和搜索**： AEM Assets使用Adobe Sensei AI功能区分图像中的颜色，并在摄取时自动将这些颜色作为标记应用。 这些标记可根据图像颜色组合来增强搜索体验。

**AI生成的元数据**： AEM Assets使用AI自动生成元数据，包括标题、描述和关键字。 这些由 AI 生成的字段提高了元数据的准确性，使资产更易于搜索、分类和推荐。这种方法不仅通过消除手动标记来提高效率，而且确保了大量数字内容之间的一致性和可扩展性。

**AI支持的资源批量重命名**： [Assets视图允许您使用人工智能](/help/assets/bulk-rename-assets-view.md)同时重命名多个资源。 您可以同时选择多个文件并将它们重命名在一起。 一些示例会话重命名提示包括&#x200B;*将所有文件更改为“my-file”并附加递增数字*&#x200B;和&#x200B;*为文件添加001、002等前缀。 并将它翻译成英文*。

<table>
<td>
   <a href="/help/assets/smart-tags.md">
   <img alt="AEM Assets中的智能标记" src="./assets/smart-tags-ai.jpeg" />
   </a>
   <div>
      <a href="/help/assets/smart-tags.md">
      <strong>将AI智能标记添加到资源</strong>
      </a>
   </div>
   <p>
      <em>了解如何将智能标记自动应用于上传的资产。</em>
   </p>
</td>


<td>
   <a href="/help/assets/color-tag-images.md">
   <img alt="添加基于颜色的智能标记" src="./assets/color-tags.jpg" />
   </a>
   <div>
      <a href="/help/assets/manage-notifications-assets-view.md">
      <strong>添加基于颜色的智能标记</strong>
      </a>
   </div>
   <p>
      <em>了解如何在摄取时自动应用基于颜色的标记。</em>
   </p>
</td>
<td>
   <a href="/help/assets/metadata-assets-view.md">
   <img alt="AI生成的元数据" src="./assets/ai-generated-metadata-landing.jpg" />
   </a>
   <div>
      <a href="/help/assets/metadata-assets-view.md">
      <strong>AI生成的元数据</strong>
      </a>
   </div>
   <p>
      <em>使用AI生成资源元数据，如标题和描述。</em>
   </p>
</td>
</table>

**上下文搜索**： AEM Assets允许您通过定义文本提示来搜索存储库中可用的资源。 Experience Manager Assets 会自动将这些文本提示转换为搜索过滤器，并显示搜索结果。您可以使用“筛选器”窗格查看和修改自动筛选器，以进一步缩小搜索结果。 一些对话式文本提示示例包括&#x200B;*高度至少为200px、宽度至少为100px的图像（带沙滩和晴天）*&#x200B;和&#x200B;*我需要高度为1500和2500像素的蓝天图像（在上个月创建，未过期且已批准）*。

**在AEM中使用Adobe Firefly生成资源**：如果您的搜索查询未返回任何结果，AEM Assets允许您实时使用Adobe Firefly生成资源。 然后，您还可以通过AEM Assets在AEM Assets用户界面中将生成的图像上传到AEM Assets存储库。

**与Adobe Express集成**： AEM Assets与Adobe Express本机集成，这使您能够从Adobe Express用户界面中直接访问AEM Assets中存储的资源。 您还可以使用Express中的Adobe Firefly Artifical Intelligence通过简单的文本提示生成图像，并将其放置在Express画布上。 然后，您可以将新内容或编辑的内容保存到AEM Assets存储库中。

<table>
<td>
   <a href="/help/assets/search-assets-view.md#contextual-search">
   <img alt="上下文搜索" src="./assets/ai-based-search.jpg" />
   </a>
   <div>
      <a href="/help/assets/search-assets-view.md#contextual-search">
      <strong>上下文搜索</strong>
      </a>
   </div>
   <p>
      <em>了解如何使用简单的文本提示搜索资源。</em>
   </p>
</td>


<td>
   <a href="/help/assets/search-assets-view.md#search-firefly">
   <img alt="使用Adobe Firefly生成资源" src="./assets/adobe-firefly.jpg" />
   </a>
   <div>
      <a href="/help/assets/search-assets-view.md#search-firefly">
      <strong>使用Adobe Firefly生成资源</strong>
      </a>
   </div>
   <p>
      <em>使用Adobe Firefly实时生成资源。</em>
   </p>
</td>
<td>
   <a href="/help/assets/native-integration-adobe-express.md">
   <img alt="与 Adobe Express 集成" src="./assets/content-hub-express.jpeg" />
   </a>
   <div>
      <a href="/help/assets/native-integration-adobe-express.md">
      <strong>与Adobe Express集成</strong>
      </a>
   </div>
   <p>
      <em>在AEM Assets用户界面中使用Adobe Express AI功能。</em>
   </p>
</td>
</table>

**智能成像**：智能成像根据客户的浏览器功能自动优化图像的格式和文件大小，从而提供更好的图像资产投放性能。 它可与您现有的图像预设配合使用，并在投放时使用智能。 这种智能根据浏览器和网络连接速度进一步减小图像文件大小。

**智能裁切**：一种Adobe Sensei AI功能，可自动检测任何图像或视频中的焦点，并裁切以对其进行维护。 它可捕获目标兴趣点，而不管屏幕大小如何，从而消除繁琐的手动任务，并提供在任何设备或屏幕上看起来都良好的高质量、快速加载的图像和视频。

**AI生成的视频字幕**： Adobe Dynamic Media中的AI生成的视频字幕使用人工智能自动为视频内容生成字幕。 此功能旨在通过提供准确的字幕来提高视频的可观看性，并增强用户体验。字幕从原始音频生成，任何附加的音频曲目或额外的字幕在视频属性页面的`Captions and Audio`选项卡中提供。 支持超过 60 种语言，可以在发布视频之前查看和预览字幕。
<table>
<td>
   <a href="/help/assets/dynamic-media/imaging-faq.md">
   <img alt="智能成像" src="./assets/smart-imaging.jpg" />
   </a>
   <div>
      <a href="/help/assets/dynamic-media/imaging-faq.md">
      <strong>智能成像</strong>
      </a>
   </div>
   <p>
      <em>根据用户的浏览器功能和网络速度优化图像的格式和文件大小。</em>
   </p>
</td>


<td>
   <a href="https://experienceleague.adobe.com/en/docs/experience-manager-learn/assets/dynamic-media/images/smart-crop-feature-video-use.html">
   <img alt="智能裁切" src="./assets/smart-cropping.jpg" />
   </a>
   <div>
      <a href="https://experienceleague.adobe.com/en/docs/experience-manager-learn/assets/dynamic-media/images/smart-crop-feature-video-use.html">
      <strong>智能裁切</strong>
      </a>
   </div>
   <p>
      <em>使用AI自动检测任何图像或视频中的焦点，并裁切以保持该焦点</em>
   </p>
</td>
<td>
   <a href="/help/assets/dynamic-media/video.md">
   <img alt="人工智能生成的视频字幕" src="./assets/videos-with-captions.jpg" />
   </a>
   <div>
      <a href="/help/assets/dynamic-media/video.md">
      <strong>AI生成的视频字幕</strong>
      </a>
   </div>
   <p>
      <em>使用人工智能为视频内容自动生成字幕。</em>
   </p>
</td>
</table>

>[!TAB 资源发现]

## 资源发现 {#asset-discovery}

在将您的资源导入AEM Assets后，要从如此庞大的收藏集中快速找到合适的资源是一项挑战。

AEM Assets提供的功能可帮助您快速访问正确的资源，例如AI生成的标记（智能标记）、自定义元数据，以及可提升您搜索体验的功能。

**元数据管理**：元数据是开始资源管理历程时最重要的方面。 将资源分配给用户后，管理元数据将完全脱离管理员的控制。 有效的资产元数据可确保更好的搜索，这是任何DAM工具的最终目标。


**元数据Forms**： Assets as a Cloud Service默认提供了许多标准元数据字段。 如果您有其他元数据需求，并且需要更多元数据字段来添加特定于业务的元数据。 通过元数据表单，可将自定义元数据字段添加到资产的“详细信息”页面。业务特有的元数据改善对其资产的治理和发现。您可以从头开始创建表单，也可以重新利用现有表单。

<table>
<td>
   <a href="/help/assets/metadata-assets-view.md">
   <img alt="管理元数据Assets视图" src="./assets/manage-metadata-assets-view.jpeg" />
   </a>
   <div>
      <a href="/help/assets/metadata-assets-view.md">
      <strong>在Assets视图中管理元数据</strong>
      </a>
   </div>
   <p>
      <em>了解如何使用Assets视图管理元数据和元数据表单。</em>
   </p>
</td>


<td>
   <a href="https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager-blogs/how-to-manage-metadata-before-and-after-migrating-to-aem-assets/ba-p/744298">
   <img alt="元数据管理最佳实践" src="./assets/metadata-best-practices.jpeg" />
   </a>
   <div>
      <a href="https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager-blogs/how-to-manage-metadata-before-and-after-migrating-to-aem-assets/ba-p/744298">
      <strong>元数据管理最佳实践</strong>
      </a>
   </div>
   <p>
      <em>了解如何将资源迁移到AEM之前和之后管理元数据。</em>
   </p>
</td>
<td>
   <a href="/help/assets/manage-metadata.md">
   <img alt="使用 Adobe Asset Link" src="./assets/metadata-management-admin-view.jpeg" />
   </a>
   <div>
      <a href="/help/assets/manage-metadata.md">
      <strong>在管理员视图中管理元数据</strong>
      </a>
   </div>
   <p>
      <em>了解如何使用管理员视图管理元数据和元数据表单。</em>
   </p>
</td>
</table>

**智能标记**：智能标记使用Adobe Sensei的人工智能框架根据您的标记结构和业务分类培训其图像识别算法。 然后，此内容智能可用于将相关标记应用到其他资产集。 默认情况下，AEM会自动将智能标记应用于上传的资源。

**搜索资源**：准备好正确的元数据后，AEM Assets允许您使用各种运算符、通配符、高级查询和自定义筛选条件进行搜索。

**上下文搜索**：AEM Assets还提供了上下文搜索功能，该功能允许您通过定义文本提示来搜索存储库中可用的资源。 Experience Manager Assets 会自动将这些文本提示转换为搜索过滤器，并显示搜索结果。您可以使用“过滤器窗格”查看和修改自动过滤器，进一步缩小搜索结果。

<table>
<td>
   <a href="/help/assets/smart-tags.md">
   <img alt="AEM Assets中的智能标记" src="./assets/smart-tags-ai.jpeg" />
   </a>
   <div>
      <a href="/help/assets/smart-tags.md">
      <strong>将智能标记添加到资源</strong>
      </a>
   </div>
   <p>
      <em>了解如何将智能标记自动应用于上传的资产。</em>
   </p>
</td>


<td>
   <a href="/help/assets/search-assets-view.md">
   <img alt="搜索Assets视图" src="./assets/search-assets-view-landing.jpeg" />
   </a>
   <div>
      <a href="/help/assets/search-assets-view.md">
      <strong>在Assets视图中搜索资源</strong>
      </a>
   </div>
   <p>
      <em>了解如何在Assets视图中有效地使用上下文搜索和其他搜索功能。</em>
   </p>
</td>
<td>
   <a href="/help/assets/search-best-practices.md">
   <img alt="搜索最佳实践" src="./assets/search-best-practices.jpeg" />
   </a>
   <div>
      <a href="/help/assets/search-best-practices.md">
      <strong>搜索最佳实践</strong>
      </a>
   </div>
   <p>
      <em>描述各种方案，以帮助AEM用户执行从基础到高级的搜索。</em>
   </p>
</td>
</table>

>[!TAB 资产管理]

## 资产管理和治理 {#asset-management-governance}

在将资源上传到AEM Assets并设置其元数据以提高可发现性后，您可以使用Assets视图的用户友好界面执行各种数字资源管理任务。

**资产管理任务**：一些基本任务包括搜索、下载、移动、复制、重命名、删除、更新和编辑操作。

您还可以维护资产版本、设置资产状态和设置资产到期。

**我的Workspace**： Assets视图还包括可自定义的工作区，该工作区提供了小部件，以便您轻松访问Assets用户界面的关键区域以及与您最相关的信息。 此页面充当一个综合解决方案以提供您工作项的概述，并且通过它可快速地访问关键工作流。

**Content Credentials**： AEM Assets支持的另一个强大功能是Content Credentials。 各品牌比以往任何时候都更关注内容透明度、人工智能披露，以及防止资产被篡改。 Adobe的Content Authenticity Initiative (CAI)构建了与Coalition for Content Provenance and Authenticity (C2PA)技术标准兼容的工具。 Content Credentials是一种新型加密的、易于篡改的元数据，可帮助查看者了解内容的谱系并确保品牌资产的完整性。 它们可以包含范围广泛的来源数据，可将insight纳入数字资源的历史记录中。

<table>
<td>
   <a href="/help/assets/manage-organize-assets-view.md">
   <img alt="资产管理任务" src="./assets/asset-management.jpeg" />
   </a>
   <div>
      <a href="/help/assets/manage-organize-assets-view.md">
      <strong>资源管理任务</strong>
      </a>
   </div>
   <p>
      <em>了解如何执行一些基本和高级资源管理任务。</em>
   </p>
</td>


<td>
   <a href="/help/assets/my-workspace-assets-view.md">
   <img alt="Mt Workspace" src="./assets/my-workspace.jpeg" />
   </a>
   <div>
      <a href="/help/assets/my-workspace-assets-view.md">
      <strong>我的Workspace</strong>
      </a>
   </div>
   <p>
      <em>了解如何使用My Workspace快速访问Assets用户界面的关键区域。</em>
   </p>
</td>
<td>
   <a href="/help/assets/content-credentials.md">
   <img alt="Content Credentials" src="./assets/content-credentials.jpeg" />
   </a>
   <div>
      <a href="/help/assets/content-credentials.md">
      <strong>Content Credentials</strong>
      </a>
   </div>
   <p>
      <em>使用Content Credentials深入了解数字资源的历史记录。</em>
   </p>
</td>
</table>

**收藏集**：通过AEM Assets，还可以将资源整理为收藏集。 收藏集是Adobe Experience Manager Assets视图中的一组资源、文件夹或其他收藏集。 使用收藏集可在用户之间共享资源。收藏集与文件夹的不同之处是可包含来自不同位置的资源。您可以与一个用户共享多个收藏集。每个收藏集都包含对资源的引用。收藏集中会保持资源的引用完整性。

**通知**： Assets查看通知允许您监视对存储库中可用的资源、文件夹或收藏集执行的操作。 需要选择并订阅将向您发送其通知的内容。还可配置向您发送其通知的类别。

**检测重复资源**： AEM Assets还支持检测重复资源。 如果DAM用户上传一个或多个已存在于存储库中的资源，Experience Manager会检测重复并通知用户。



<table>
<td>
   <a href="/help/assets/manage-collections-assets-view.md">
   <img alt="管理收藏集" src="./assets/manage-collections.jpeg" />
   </a>
   <div>
      <a href="/help/assets/manage-collections-assets-view.md">
      <strong>管理收藏集</strong>
      </a>
   </div>
   <p>
      <em>了解如何将资源组织为收藏集，以便有效共享资源。</em>
   </p>
</td>


<td>
   <a href="/help/assets/manage-notifications-assets-view.md">
   <img alt="设置通知" src="./assets/manage-notifications.jpeg" />
   </a>
   <div>
      <a href="/help/assets/manage-notifications-assets-view.md">
      <strong>设置通知</strong>
      </a>
   </div>
   <p>
      <em>了解如何设置通知以监视对资源、文件夹或收藏集执行的操作。</em>
   </p>
</td>
<td>
   <a href="/help/assets/detect-duplicate-assets.md">
   <img alt="检测重复的资产" src="./assets/duplicate-assets.jpeg" />
   </a>
   <div>
      <a href="/help/assets/detect-duplicate-assets.md">
      <strong>检测重复的资源</strong>
      </a>
   </div>
   <p>
      <em>检测上传到AEM Assets的重复资源并通知用户。</em>
   </p>
</td>
</table>

>[!TAB 集成]

## 与Adobe和非Adobe应用程序集成 {#integration-adobe-non-adode-apps}

AEM Assets可与各种Adobe和非Adobe应用程序无缝集成。 以下是可用集成的概要视图：

+++**与Adobe和非Adobe应用程序的集成**

* **具有OpenAPI功能的Dynamic Media**： [具有OpenAPI功能的Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md)提供了一组[搜索](/help/assets/search-assets-api.md)和[投放](/help/assets/deliver-assets-apis.md) API。 它允许开发人员轻松地将资产交付与其应用程序集成。 这些应用程序包括 Adobe 以及第三方应用程序。它提供了一个微型前端资产选择器用户界面，用于搜索和选择批准的资产。 该选择器可以轻松地与基于 JavaScript 框架（如 React JS、Angular JS 和 Vanilla JS）的任何应用程序集成。

* **微前端资源选择器**：微前端资源选择器提供了一个用户界面，该界面可与Experience Manager Assets存储库轻松集成，因此您可以浏览或搜索存储库中可用的数字资源，并在应用程序创作体验中使用这些资源。
您可以将资源选择器与Adobe或非Adobe应用程序集成。

<table>
<td>
   <a href="/help/assets/dynamic-media-open-apis-overview.md">
   <img alt="具有OpenAPI功能的Dynamic Media概述" src="./assets/dm-openapi-uses.jpeg" />
   </a>
   <div>
      <a href="/help/assets/dynamic-media-open-apis-overview.md">
      <strong>具有OpenAPI功能的Dynamic Media概述</strong>
      </a>
   </div>
   <p>
      <em>了解主要优势以及如何启用它。</em>
   </p>
</td>


<td>
   <a href="/help/assets/restrict-assets-delivery.md">
   <img alt="限制对 Experience Manager 中的资产的访问" src="./assets/restrict-assets.jpeg" />
   </a>
   <div>
      <a href="/help/assets/restrict-assets-delivery.md">
      <strong>限制对 Experience Manager 中的资产的访问</strong>
      </a>
   </div>
   <p>
      <em>配置角色以限制对已批准资源的访问。</em>
   </p>
</td>
<td>
   <a href="/help/assets/overview-asset-selector.md">
   <img alt="资源选择器" src="./assets/integration-asset-selector.jpeg" />
   </a>
   <div>
      <a href="/help/assets/overview-asset-selector.md">
      <strong>微型前端资产选择器</strong>
      </a>
   </div>
   <p>
      <em>了解如何将微型前端资产选择器与Adobe或非Adobe应用程序集成。</em>
   </p>
</td>
</table>

+++

+++**与Adobe应用程序的本机集成**

* **与Adobe Workfront集成**： [!DNL Adobe Workfront]是一个工作管理应用程序，可帮助您在一个地方管理整个工作生命周期。 [!DNL Workfront]和[!DNL Adobe Experience Manager Assets]之间的集成使组织能够通过将工作和数字资产管理内在地连接起来，提高内容速度和上市时间。 在Workfront中管理其工作的情况下，用户有权访问所需的文档和图像。

  Adobe选件与[集成 [!DNL Workfront] 和 [!DNL Adobe Experience Manager Assets] 本机](https://experienceleague.adobe.com/docs/workfront/using/documents/wf-aem-integrations/wf-aem-essentials/aem-asset-integrations.html?lang=zh-Hans)。

* **与Figma集成**： AEM Assets与Figma原生集成，这允许设计人员从Figma用户界面中直接访问AEM Assets中存储的资源。 可将在 AEM Assets 中管理的内容放入 Figma 画布，然后将新内容或经过编辑的内容保存在 AEM Assets 存储库中。要访问 Figma 社区页面上提供的 AEM Assets 连接器，请单击[此处](https://www.figma.com/community/plugin/1512561378275712210/adobe-experience-manager-aem-assets-connector)。

* **与Adobe Express的本机集成**： AEM Assets与Adobe Express本机集成，这使您能够从Adobe Express用户界面中直接访问AEM Assets中存储的资源。 可将在 AEM Assets 中管理的内容放入 Express 画布，然后将新内容或经过编辑的内容保存在 AEM Assets 存储库中。

* **将AEM Assets连接到Creative Cloud**： Experience Manager Assets能够连接到已为其他IMS组织设置的Creative Cloud权利，以便轻松地使用AEM Assets中的最新Creative Cloud集成，包括Express和Creative Cloud Libraries。 如果您的 Creative Cloud 产品和 AEM Assets 预配给单独的 IMS 组织，则您可连接到其他 Creative Cloud 组织，以便可在这两个解决方案之间执行集成的工作流程。

<table>
<td>
   <a href="/help/assets/workfront-integrations.md">
   <img alt="与 Adobe Workfront 集成" src="./assets/integration-adobe-workfront.jpeg" />
   </a>
   <div>
      <a href="/help/assets/workfront-integrations.md">
      <strong>与Adobe Workfront集成</strong>
      </a>
   </div>
   <p>
      <em>与Adobe Workfront集成以在一个位置管理整个工作生命周期。</em>
   </p>
</td>
<td>
   <a href="/help/assets/manage-collections-assets-view.md">
   <img alt="与 Figma 集成" src="./assets/integration-commerce.jpeg" />
   </a>
   <div>
      <a href="/help/assets/manage-collections-assets-view.md">
      <strong>与Figma集成</strong>
      </a>
   </div>
   <p>
      <em>从Figma用户界面中访问AEM Assets中存储的资源</em>
   </p>
</td>
<td>
   <a href="/help/assets/native-integration-adobe-express.md">
   <img alt="与Adobe Express的本机集成" src="./assets/integration-adobe-express.jpeg" />
   </a>
   <div>
      <a href="/help/assets/native-integration-adobe-express.md">
      <strong>与Adobe Express的本机集成</strong>
      </a>
   </div>
   <p>
      <em>将AEM Assets中可用的资源放在Express画布上，并将更新的资源保存到AEM。</em>
   </p>
</td>


</table>


* **与Adobe Journey Optimizer集成**：使用Adobe Experience Manager Assets将营销和创意工作流程结合使用。 与Adobe Journey Optimizer本机集成，访问Assets as a Cloud Service以存储、管理、发现和分发数字资源。 它提供了单一集中式资源存储库，您可以使用它填充消息。

* **与Commerce的集成**： Adobe Experience Manager (AEM) Assets与Commerce的集成将AEM as a Digital Asset Management (DAM)系统的强大功能与Adobe Commerce相结合，以增强电子商务体验。 要提供这些功能，需要将Commerce项目连接到AEM强大的资产管理环境，以便提供一种无缝、可扩展且高效的方式来跨商业商店管理和交付资产。
* **将AEM Assets与Edge Delivery Services的基于文档的创作流集成**：当[!DNL AEM Assets]与您的基于文档的创作工具（如[!DNL Microsoft Word]或[!DNL Google Docs]）集成时，它在您的创作工具中提供资源选择器。 使用此资产选择器访问[!DNL AEM Assets]，并将批准的资产插入您的内容。
如果您已经拥有[!DNL Edge Delivery Services]网站，请参阅[[!DNL AEM Assets] 插件](https://github.com/adobe-rnd/aem-assets-plugin/blob/main/README.md)文档，以了解如何将[!DNL AEM Assets]与您现有的[!DNL AEM]项目集成。

* **将[!DNL AEM Assets]与[!DNL Universal Editor]的基于[!DNL Edge Delivery Services]**&#x200B;的创作流集成：将[!DNL Universal Editor]设置为与[!DNL AEM Assets]集成。 此集成允许您使用[!DNL Dynamic Media with OpenAPI capabilities]交付资产。

   * 查看[站点 [!DNL Edge Delivery] 中的](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/#configuration-in-edge-delivery-site)配置，了解如何在[!DNL Universal Editor]中添加自定义资产选取器函数。 自定义资产选取器允许您将资产直接插入到[!DNL Universal Editor]内容中。
   * 请参阅[扩展概述](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/#extension-overview)，了解如何在[!DNL AEM Assets]中创作时访问[!DNL Universal Editor]并插入资产。

<table>
<td>
   <a href="https://experienceleague.adobe.com/zh-hans/docs/journey-optimizer/using/content-management/combine/assets">
   <img alt="与 Adobe Journey Optimizer 集成" src="./assets/integration-figma.jpeg" />
   </a>
   <div>
      <a href="https://experienceleague.adobe.com/zh-hans/docs/journey-optimizer/using/content-management/combine/assets">
      <strong>与Adobe Journey Optimizer集成</strong>
      </a>
   </div>
   <p>
      <em>使用与AJO的集成，将营销和创意工作流程结合使用</em>
   </p>
</td>
<td>
   <a href="https://experienceleague.adobe.com/zh-hans/docs/commerce-admin/content-design/aem-asset-management/aem-assets-integration">
   <img alt="与Commerce集成" src="./assets/integration-ajo.jpeg" />
   </a>
   <div>
      <a href="https://experienceleague.adobe.com/zh-hans/docs/commerce-admin/content-design/aem-asset-management/aem-assets-integration">
      <strong>与Commerce集成</strong>
      </a>
   </div>
   <p>
      <em>将AEM Assets与Commerce集成以增强电子商务体验。</em>
   </p>
</td>
<td>
   <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md">
   <img alt="将AEM Assets与EDS集成" src="./assets/integrate-ue-assets.jpeg" />
   </a>
   <div>
      <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md">
      <strong>将AEM Assets与EDS集成</strong>
      </a>
   </div>
   <p>
      <em>将AEM Assets与基于文档和通用编辑器的创作流集成。</em>
   </p>
</td>
</table>

+++

>[!TAB 资产激活]

## 资产激活 {#asset-activation}

使用Content Hub到Dynamic Media（包括强大的OpenAPI功能），通过AEM Assets释放数字资源的全部潜力。 AEM Assets提供了一整套解决方案，旨在简化资产转换并优化各种渠道的交付。

+++**Content Hub**

Content Hub 是 Experience Manager Assets as a Cloud Service 的一部分，旨在为组织及其业务合作伙伴提供对品牌内容的普及化访问。它侧重于大规模分发资产以进行激活，并创建品牌内容变体，以提高营销敏捷度。

Content Hub 具有以下主要优势：

* **在一个直观的门户中查找并共享所有品牌批准的资源**：AEM Assets作为单一的真实来源，所有批准的资源在Content Hub中以平面层次结构自动提供，以改善搜索体验。

* **可配置的用户界面**： Content Hub中最常见的属性（如搜索筛选器）、添加或导入资源时可用的字段、资源属性、品牌推广的横幅内容，这些属性均可配置，管理员可以根据自己的要求轻松配置Content Hub用户界面。

* **让非创意人员能够编辑和混合内容，同时不离开品牌**：通过Content Hub，您可以使用Adobe Express创建新内容(如果您拥有Adobe Express权限)。 您可以使用易于使用的工具编辑现有内容，使用模板和品牌元素制作品牌变体，并使用 Adobe Firefly 的最新 GenAI功 能创建新内容。

* **深入了解如何跨团队使用内容**： [!DNL Content Hub]提供了有关资产的宝贵见解，从而解决了营销利益相关者经常遇到的共同难题 — 营销活动、渠道和不同区域中使用的资产使用情况统计数据。 通过清楚地了解资产的性能和受欢迎程度，它提供了对增强用户体验至关重要的可操作见解。

<table>
<td>
   <a href="/help/assets/product-overview.md">
   <img alt="Content Hub 概述" src="./assets/content-hub-overview.jpeg" />
   </a>
   <div>
      <a href="/help/assets/product-overview.md">
      <strong>Content Hub概述</strong>
      </a>
   </div>
   <p>
      <em>进一步了解Content Hub、其主要优势以及如何访问它。</em>
   </p>
</td>


<td>
   <a href="/help/assets/configure-content-hub-ui-options.md">
   <img alt="配置Content Hub用户界面" src="./assets/content-hub-configuration.jpeg" />
   </a>
   <div>
      <a href="/help/assets/configure-content-hub-ui-options.md">
      <strong>配置Content Hub用户界面</strong>
      </a>
   </div>
   <p>
      <em>了解如何在Content Hub用户界面上配置可用选项。</em>
   </p>
</td>
<td>
   <a href="/help/assets/edit-images-content-hub.md">
   <img alt="使用Adobe Express编辑" src="./assets/content-hub-express.jpeg" />
   </a>
   <div>
      <a href="/help/assets/edit-images-content-hub.md">
      <strong>使用Adobe Express编辑</strong>
      </a>
   </div>
   <p>
      <em>了解如何使用Adobe Express在Content Hub中编辑图像。</em>
   </p>
</td>
</table>

+++

+++**Dynamic Media**

Dynamic Media可帮助您按需提供丰富的可视化推销和营销资产。 它还帮助您创建并提供交互式查看体验，包括缩放、360度旋转和视频。 您的资产会动态缩放以用于Web、移动和社交网站。 使用一组主要源资产（如图像、视频和3D ），Dynamic Media通过其可扩展、性能优化的全局CDN（内容交付网络）实时生成和交付此丰富内容的多种变体。

Dynamic Media提供以下主要功能：

* **智能成像**：智能成像根据客户的浏览器功能自动优化图像的格式和文件大小，从而提供更好的图像资产投放性能。 它可与您现有的图像预设配合使用，并在投放时使用智能。 这种智能根据浏览器和网络连接速度进一步减小图像文件大小。

* **自适应视频集**：自适应视频集对以不同比特率和格式编码的相同视频的版本进行分组。 首先从您上传到系统中的原始主视频开始。 Dynamic Media会自动调整该视频的大小，或将其转码为多个视频。 然后，在交付时，它会智能地确定要使用哪种视频屏幕、哪种质量和哪种格式，并将其交付到手机、平板电脑或台式计算机。

* **智能裁切**：一种Adobe Sensei AI功能，可自动检测任何图像或视频中的焦点，并裁切以对其进行维护。 它可捕获目标兴趣点，而不管屏幕大小如何，从而消除繁琐的手动任务，并提供在任何设备或屏幕上看起来都良好的高质量、快速加载的图像和视频。

* **Dynamic Media模板**：使用Dynamic Media模板、WYSIWYG模板编辑器，为您的横幅和传单创建实时可自定义的模板。 发布Dynamic Media模板并将其用于下游应用程序。 Dynamic Media模板包括图像和文本图层。 向模板的图像和文本图层添加参数，并使用Dynamic Media URL重新定位和调整图层大小并实时更新其内容。

* **多音频和字幕**：向主视频添加多个字幕和多个音轨。 此功能意味着全球观众都能看懂您的视频。只需自定义一个主视频，即可发布到多种语言的全球观众，并遵循不同地区的辅助功能准则。此外，作者从用户界面中的一个选项卡即可管理字幕和音轨。

* **支持HTTP (DASH)的Dynamic Adaptive Streaming**： Dynamic Media支持Dynamic Media视频交付中的Adaptive streaming（启用了CMAF），从而确保获得更好的视频用户查看体验。 DASH是自适应视频流的国际标准协议，在业界得到广泛应用。

* **AI生成的视频字幕**： Adobe Dynamic Media中的AI生成的视频字幕使用人工智能自动为视频内容生成字幕。 支持超过 60 种语言，可以在发布视频之前查看和预览字幕。

有关可用的Dynamic Media产品的信息，请参阅[Dynamic Media Prime和Ultimate](/help/assets/dynamic-media/dm-prime-ultimate.md)。



<table>
<td>
   <a href="/help/assets/dynamic-media/dynamic-media.md">
   <img alt="使用 Dynamic Media" src="./assets/work-with-dynamic-media.jpeg" />
   </a>
   <div>
      <a href="/help/assets/dynamic-media/dynamic-media.md">
      <strong>使用Dynamic Media</strong>
      </a>
   </div>
   <p>
      <em>了解如何投放资源以供在Web、移动和社交网站上使用。</em>
   </p>
</td>


<td>
   <a href="/help/assets/dynamic-media/dm-journey-part1.md">
   <img alt="Dynamic Media历程" src="./assets/dm-journey.jpeg" />
   </a>
   <div>
      <a href="/help/assets/dynamic-media/dm-journey-part1.md">
      <strong>Dynamic Media历程</strong>
      </a>
   </div>
   <p>
      <em>了解Dynamic Media如何为您的工作带来价值。</em>
   </p>
</td>
<td>
   <a href="/help/assets/dynamic-media/dm-best-practices.md">
   <img alt="将 AEM Assets 连接到 Creative Cloud" src="./assets/dm-best-practices.jpeg" />
   </a>
   <div>
      <a href="/help/assets/dynamic-media/dm-best-practices.md">
      <strong>Dynamic Media最佳做法</strong>
      </a>
   </div>
   <p>
      <em>处理图像、视频和查看者时的最佳实践。</em>
   </p>
</td>
</table>

+++

+++**具有 OpenAPI 功能的 Dynamic Media**

在当今快节奏的数字世界中，充分释放品牌数字资产的潜力对于保持竞争优势至关重要。全面的数字资产管理 (DAM) 解决方案有助于资产治理、促进品牌一致性、加速内容传递，同时确保品牌完整性和卓越的客户体验。

具有 OpenAPI 功能的 Dynamic Media 将 DAM 置于敏捷高效的内容供应链生态系统的核心，以确保资产治理和传递。

具有OpenAPI功能的Dynamic Media提供以下主要优势：

* **无缝集成**：具有 OpenAPI 功能的 Dynamic Media 提供了一套全面的搜索和传递 API。它有助于开发人员轻松地[将资产传递与其应用程序集成](/help/assets/integrate-dynamic-media-open-apis.md)。这些应用程序包括 Adobe 以及第三方应用程序。它提供了一个[微前端资产选择器用户界面](/help/assets/overview-asset-selector.md)，用于搜索和选择已批准的资产。该选择器可以轻松地与基于 JavaScript 框架（如 React JS、Angular JS 和 Vanilla JS）的任何应用程序集成。

* **集中管理数字资产**：DAM 是所有数字资产的单一数据源。您的数字资产在 AEM Assets 中进行集中管理，并通过使用传递 URL 进行引用，无需复制资产二进制文件，即可传递给消费应用程序。

* **实时更新**：对 DAM 中已批准资产所做的任何更改（包括版本更新和元数据修改）都会自动反映在传递 URL 中。通过内容传递网络为具有 OpenAPI 功能的 Dynamic Media 配置了一个较短的生存时间 (TTL) 值，即 10 分钟，这样，在不到 10 分钟的时间内，更新就会在所有创作和发布的界面上显示出来。

* **品牌一致性**：只有[经过品牌批准的资产](/help/assets/approve-assets.md)才会暴露给下游应用程序。[品牌经理和营销人员对品牌资产保持严格控制](/help/assets/restrict-assets-delivery.md)。只有经过批准的最新版本资产可供使用，以确保所有渠道和应用程序的品牌一致性。

* **针对网络优化的传递**：数字资产以针对网络优化的格式传递，以提升您的数字体验的核心网页关键指标。这包括支持图像的 WebP 演绎版、通过 HLS 或 DASH 协议实现视频的自适应流式处理，以及文档的原始演绎版。

* **动态资产转换**：我们的系统允许使用称为图像修改器的 URL 参数进行即时图像转换。[例如宽度、高度、旋转、翻转、质量、裁切、格式和智能裁剪](/help/assets/deliver-assets-apis.md)。转换后的演绎版是动态生成的，并通过内容传递网络无缝传递。

* **安全传递资产**：具有 OpenAPI 功能的 Dynamic Media 提供了一种控制访问您的数字资产的机制。您可以将用户角色或组指定为要保护的资产的元数据，并设置预定义的时间范围，在此期间[只有授权用户才能访问这些资产](/help/assets/restrict-assets-delivery.md)。在限制期内，未经授权的用户无法解析受保护资产的传递 URL。

有关可用的Dynamic Media产品的信息，请参阅[Dynamic Media Prime和Ultimate](/help/assets/dynamic-media/dm-prime-ultimate.md)。

<table>
<td>
   <a href="/help/assets/dynamic-media-open-apis-overview.md">
   <img alt="具有OpenAPI功能的Dynamic Media概述" src="./assets/dm-openapi-uses.jpeg" />
   </a>
   <div>
      <a href="/help/assets/dynamic-media-open-apis-overview.md">
      <strong>具有OpenAPI功能的Dynamic Media概述</strong>
      </a>
   </div>
   <p>
      <em>了解主要优势以及如何启用它。</em>
   </p>
</td>


<td>
   <a href="/help/assets/restrict-assets-delivery.md">
   <img alt="限制对 Experience Manager 中的资产的访问" src="./assets/restrict-assets.jpeg" />
   </a>
   <div>
      <a href="/help/assets/restrict-assets-delivery.md">
      <strong>限制对 Experience Manager 中的资产的访问</strong>
      </a>
   </div>
   <p>
      <em>配置角色以限制对已批准资源的访问。</em>
   </p>
</td>
<td>
   <a href="/help/assets/integrate-remote-approved-assets-with-sites.md">
   <img alt="将远程 AEM Assets 与 AEM Sites 集成" src="./assets/integration-aem-sites.jpeg" />
   </a>
   <div>
      <a href="/help/assets/integrate-remote-approved-assets-with-sites.md">
      <strong>将远程 AEM Assets 与 AEM Sites 集成</strong>
      </a>
   </div>
   <p>
      <em>将远程AEM Assets与AEM Sites环境集成。</em>
   </p>
</td>
</table>

+++

>[!TAB 见解]

## 资产分析 {#asset-insights}

通过资源报表，管理员可了解Adobe Experience Manager Assets视图环境的活动。 这些数据提供关于用户如何与内容和产品进行交互的有用信息。所有用户都可以访问 Insights 仪表板，分配给管理员产品配置文件的用户可以创建用户定义的报告。

您可以生成各种类型的报表，例如上传、下载和Dynamic Media交付。

* Assets视图中的&#x200B;**分析**： Assets视图允许您使用分析仪表板查看Assets视图环境的实时数据。 可以查看过去30天或过去12个月的实时事件量度。 这些事件包括下载、上传、存储使用情况、热门搜索、按大小划分的资源计数以及按资源类型划分的资源计数。

* 在管理员视图中&#x200B;**Adobe Analytics集成**： Assets Insights功能允许您跟踪第三方网站、营销活动和Adobe创意解决方案中使用的图像的用户评级和使用情况统计数据。 它有助于提供有关图像的性能和常用程度的洞察。 Assets Insights会捕获用户活动详细信息，例如对图像进行评级、单击的次数和展示次数（图像加载到网站上的次数）。 它根据这些统计数据为图像分配分数。 您可以使用得分和性能统计信息选择热门图像以将其包含在目录、营销活动等中。 您甚至可以根据这些统计数据制定存档和许可证更新策略。 要让Assets Insights显示资源的使用情况统计数据，请首先配置该功能以从Adobe Analytics获取报表数据。

* **Content Hub Insights**：Content Hub提供了有关资产的宝贵见解，解决了营销利益相关者经常遇到的共同挑战 — 营销活动、渠道和其他区域中使用的资产使用情况统计数据。 通过清楚地了解资产的性能和受欢迎程度，它提供了对增强用户体验至关重要的可操作见解。

<table>
<td>
   <a href="/help/assets/manage-reports-assets-view.md">
   <img alt="在“资源”视图中管理报告" src="./assets/assets-insights-assets-view.jpeg" />
   </a>
   <div>
      <a href="/help/assets/manage-reports-assets-view.md">
      <strong>在Assets视图中管理报告</strong>
      </a>
   </div>
   <p>
      <em>使用Assets视图获取有关关键成功指标的见解。</em>
   </p>
</td>


<td>
   <a href="/help/assets/asset-reports.md">
   <img alt="在“管理员”视图中管理报表" src="./assets/assets-insights-admin-view.jpeg" />
   </a>
   <div>
      <a href="/help/assets/asset-reports.md">
      <strong>以管理员视图管理报告</strong>
      </a>
   </div>
   <p>
      <em>了解如何在管理员视图中管理Adobe Analytics集成的报告。</em>
   </p>
</td>
<td>
   <a href="/help/assets/insights-content-hub.md">
   <img alt="Content Hub中的Assets分析" src="./assets/asset-insights-content-hub.jpeg" />
   </a>
   <div>
      <a href="/help/assets/insights-content-hub.md">
      在Content Hub中<strong>Assets分析</strong>
      </a>
   </div>
   <p>
      <em>了解如何在Content Hub中查看资源分析。</em>
   </p>
</td>
</table>

>[!ENDTABS]

## 基于角色的数字资产管理可用体验 {#persona-based-experiences}

Adobe 为您提供强大的数字资源管理（DAM）解决方案，让您能够充分利用数字资源。 Adobe Experience Manager Assets 具有两种使用相同 Cloud Service 存储库的独立体验：

* **管理视图**：现有资源作为 Cloud Service 用户界面。使用管理视图实现所有高级数字资产管理功能，包括集成、工作流程、内容自动化、发布等。

* **资产视图**：Adobe 的轻量级资源管理体验，用于存储、管理、发现和使用数字资产。简化的用户界面包含基本的数字资产管理功能。专为轻量级 DAM 用户设计，专注于上传、元数据管理、搜索、下载和共享。

![添加标记](assets/newui-overview.svg)

有权访问管理视图的用户也可以访问资源视图。资源视图提供简化的用户界面，使您可以轻松管理、探索和分发数字资源。 来自不同职能部门（包括创意团队、营销团队和业务线团队）的广泛用户可以就资源进行协作，并在需要时随时随地访问正确的、经批准的资源。许多临时 DAM 用户更喜欢资源视图，因为它只包含一部分功能。该体验面向创意人员、只读资源消费者和轻量级 DAM 用户。

DAM 库管理员、开发人员和超级用户可以继续使用管理视图，或根据需要在这些用户界面之间切换。您可以选择最适合您角色的体验。

有关如何访问资源视图及其通过“管理”视图提供的一些简化功能的信息，请参阅[资源视图简介。](/help/assets/assets-view-introduction.md)


