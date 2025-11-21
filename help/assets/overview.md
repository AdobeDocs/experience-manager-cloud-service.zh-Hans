---
title: 在 AEM 中引入用于数字资产管理的 Assets as a Cloud Service
description: 在 AEM 中引入用于数字资产管理的 Assets as a Cloud Service
exl-id: 4437f214-d058-4975-8b8f-869a12c8103b
source-git-commit: f72f72e87dabe89cafc0a56feb35f58ae1a97dfb
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# 在 AEM 中引入用于数字资产管理的 Assets as a Cloud Service {#assets-as-cloud-service-digital-asset-management-aem}

AEM Assets as a Cloud Service 为企业提供了一个云原生 PaaS 解决方案，不仅可以执行企业的数字资产管理和动态媒体操作，还可以使用 AI/ML 等新一代智能功能。所有这些都来自一个始终保持最新状态、始终可用、始终不断学习的系统。

Adobe 提供强大的数字资产管理（DAM）解决方案，助您充分发挥数字资产的价值。Adobe Experience Manager Assets 提供两种独立的使用体验，共享同一 Cloud Services 存储库，以满足您的不同需求。关于 AEM Assets 中基于用户画像的体验，请参阅《[适用于数字资产管理的基于用户画像的体验](#persona-based-experiences)》。

关于 AEM Assets Ultimate 和 AEM Assets Prime 的相关信息，请参阅 [Assets as a Cloud Service Ultimate](/help/assets/assets-ultimate-overview.md) 和 [Assets as a Cloud Service Prime](/help/assets/assets-prime.md)。

Adobe 数字资产管理的部分核心功能包括：

![add-tags](assets/aem-assets-features-landing-page.png)


>[!BEGINTABS]

>[!TAB 资产摄取]

## 资产摄取 {#asset-ingestion}

使用批量导入功能可将大量资产直接从数据源（如 Azure、AWS、Google Cloud、Dropbox 和 OneDrive）导入 Assets as a Cloud Service。

您可以通过“管理员视图”或“资产视图”执行批量导入操作。与“管理员视图”相比，“资产视图”提供了更多数据源选项。

除了网页浏览器用户界面外，Experience Manager 还支持其他的桌面设备客户端。这些客户端也提供无需网页浏览器的上传体验。

* Adobe Asset Link 可在 Adobe Photoshop、Adobe Illustrator 和 Adobe InDesign 桌面应用程序中访问 Experience Manager 中的资产。您可以将打开的文档上传至 Experience Manager。您可以直接通过这些桌面应用程序中的 Adobe Asset Link 界面上传。

* 无论是哪种文件类型的资产或者用哪种原生应用程序处理资产，Experience Manager 桌面应用程序都可简化在桌面设备上处理资产的流程。该应用程序适用于从本地文件系统上传包含嵌套文件夹结构的文件，因为浏览器上传仅支持上传扁平的文件列表。

请通过以下链接访问这些资产摄取工具的详细文档：

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
      <em>了解如何直接从数据源导入大量资产</em>
   </p>
</td>


<td>
   <a href="https://experienceleague.adobe.com/zh-hans/docs/experience-manager-desktop-app/using/get-started">
   <img alt="使用 AEM 桌面应用程序" src="./assets/desktop-app-upload.jpeg" />
   </a>
   <div>
      <a href="https://experienceleague.adobe.com/zh-hans/docs/experience-manager-desktop-app/using/get-started">
      <strong>使用 AEM 桌面应用程序</strong>
      </a>
   </div>
   <p>
      <em>了解如何使用 AEM 桌面应用程序从您的本地文件系统上传位于嵌套文件夹结构中的文件。</em>
   </p>
</td>
<td>
   <a href="https://helpx.adobe.com/cn/enterprise/using/adobe-asset-link.html">
   <img alt="使用 Adobe Asset Link" src="./assets/adobe-asset-link.jpeg" />
   </a>
   <div>
      <a href="https://helpx.adobe.com/cn/enterprise/using/adobe-asset-link.html">
      <strong>使用 Adobe Asset Link</strong>
      </a>
   </div>
   <p>
      <em>了解如何通过 Creative Cloud 应用程序将资产上传至 Experience Manager。</em>
   </p>
</td>
</table>

>[!TAB AI 驱动的功能]

**智能标记**：智能标记借助 Adobe Sensei 的人工智能框架，基于您的标记结构和业务分类法训练图像识别算法。随后，该内容智能可用于为另一组资产自动应用相关标记。AEM 默认会自动为上传的资产应用智能标记。

**基于颜色的智能标记与搜索**：AEM Assets 使用 Adobe Sensei 的 AI 功能区分图像中的颜色，并在摄取时自动将这些特征应用为标记。这些标记可基于图像的颜色构成提供更优的搜索体验。

**AI 生成的元数据**：AEM Assets 使用 AI 自动生成元数据，包括标题、描述和关键词。这些由 AI 生成的字段提高了元数据的准确性，使资产更易于搜索、分类和推荐。这种方法不仅通过消除手动标记来提高效率，而且确保了大量数字内容之间的一致性和可扩展性。

**AI 驱动的资产批量重命名**：[通过“资产视图”可借助人工智能一次性重命名多个资产](/help/assets/bulk-rename-assets-view.md)。您可以一次选择多个文件，并统一进行重命名。一些示例对话式重命名提示包括：*将所有文件更名为“my-file”并追加递增编号* 和 *为文件添加 001、002 等前缀并翻译为英文*。

<table>
<td>
   <a href="/help/assets/smart-tags.md">
   <img alt="AEM Assets 中的智能标记" src="./assets/smart-tags-ai.jpeg" />
   </a>
   <div>
      <a href="/help/assets/smart-tags.md">
      <strong>为资产添加 AI 智能标记</strong>
      </a>
   </div>
   <p>
      <em>了解如何为上传的资产自动应用智能标记。</em>
   </p>
</td>


<td>
   <a href="/help/assets/color-tag-images.md">
   <img alt="添加智能基于颜色的标记" src="./assets/color-tags.jpg" />
   </a>
   <div>
      <a href="/help/assets/manage-notifications-assets-view.md">
      <strong>添加智能基于颜色的标记</strong>
      </a>
   </div>
   <p>
      <em>了解如何在导入过程中自动应用基于颜色的标记。</em>
   </p>
</td>
<td>
   <a href="/help/assets/metadata-assets-view.md">
   <img alt="AI 生成的元数据" src="./assets/ai-generated-metadata-landing.jpg" />
   </a>
   <div>
      <a href="/help/assets/metadata-assets-view.md">
      <strong>AI 生成的元数据</strong>
      </a>
   </div>
   <p>
      <em>使用 AI 自动生成资产元数据，如标题和描述。</em>
   </p>
</td>
</table>

**上下文搜索**：使用 AEM Assets 您可以通过定义文本提示词在存储库中搜索可用资产。Experience Manager Assets 会自动将这些文本提示词转换为搜索过滤器，并显示搜索结果。您可以通过“过滤器窗格”查看并更改自动过滤器，以进一步缩小搜索结果范围。以下是一些对话式文本提示词示例：

* *图像高度至少为 200 像素，宽度至少为 100 像素，内容为海滩和晴朗的天空*，
* *我需要上个月创建的高度为 1500 至 2500 像素的蓝天图像，并且图像未过期且已经获得批准*。

**在 AEM 中通过 Adobe Firefly 生成资产**：如果您的搜索查询未返回任何结果，您可以在 AEM Assets 中使用 Adobe Firefly 实时生成资产。AEM Assets 还支持您直接在 AEM Assets 用户界面中将生成的图像上传至 AEM Assets 存储库。

**与 Adobe Express 集成**：AEM Assets 以原生方式与 Adobe Express 集成，使您能够在 Adobe Express 用户界面中直接访问 AEM Assets 中存储的资产。您还可以在 Adobe Express 中使用 Adobe Firefly 人工智能，通过简单的文本提示词生成图像，并将其添加到 Express 画布中。随后，您可以将新建或编辑的内容保存至 AEM Assets 存储库中。

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
      <em>了解如何使用简单的文本提示词搜索资产。</em>
   </p>
</td>


<td>
   <a href="/help/assets/search-assets-view.md#search-firefly">
   <img alt="使用 Adobe Firefly 生成资产" src="./assets/adobe-firefly.jpg" />
   </a>
   <div>
      <a href="/help/assets/search-assets-view.md#search-firefly">
      <strong>使用 Adobe Firefly 生成资产</strong>
      </a>
   </div>
   <p>
      <em>使用 Adobe Firefly 实时生成资产。</em>
   </p>
</td>
<td>
   <a href="/help/assets/native-integration-adobe-express.md">
   <img alt="与 Adobe Express 集成" src="./assets/content-hub-express.jpeg" />
   </a>
   <div>
      <a href="/help/assets/native-integration-adobe-express.md">
      <strong>与 Adobe Express 集成</strong>
      </a>
   </div>
   <p>
      <em>在 AEM Assets 用户界面中使用 Adobe Express 的 AI 功能。</em>
   </p>
</td>
</table>

**智能图像处理**：智能图像处理可根据用户浏览器的能力，自动优化图像格式和文件大小，从而显著提升图像资产的交付性能。该功能可与您现有的图像预设配合使用，并在交付时智能优化图像内容。该智能机制还会根据浏览器类型和网络连接速度，进一步压缩图像文件大小。

**智能裁剪**：这是 Adobe Sensei 的 AI 功能，可自动识别图像或视频中的焦点，并在裁剪时保持该焦点不变。该功能可在不同屏幕尺寸下准确保留图像或视频中的目标焦点，从而省去繁琐的手动操作，提供高质量、加载迅速的图像和视频内容，确保在任何设备或屏幕上均呈现良好效果。

**AI 生成的视频字幕**：Adobe Dynamic Media 利用人工智能自动为视频内容生成字幕。此功能旨在通过提供精准字幕，提高内容的可访问性并优化用户体验。字幕可根据原始音频生成，也可以通过视频属性页面中的 `Captions and Audio` 选项卡添加额外音轨或字幕内容。支持 60 多种语言，字幕可在发布视频前进行审核与预览。
<table>
<td>
   <a href="/help/assets/dynamic-media/imaging-faq.md">
   <img alt="智能图像处理" src="./assets/smart-imaging.jpg" />
   </a>
   <div>
      <a href="/help/assets/dynamic-media/imaging-faq.md">
      <strong>智能图像处理</strong>
      </a>
   </div>
   <p>
      <em>根据用户的浏览器能力和网络速度优化图像格式和文件大小。</em>
   </p>
</td>


<td>
   <a href="https://experienceleague.adobe.com/zh-hans/docs/experience-manager-learn/assets/dynamic-media/video/dynamic-media-smart-crop-video">
   <img alt="智能裁剪" src="./assets/smart-cropping.jpg" />
   </a>
   <div>
      <a href="https://experienceleague.adobe.com/zh-hans/docs/experience-manager-learn/assets/dynamic-media/video/dynamic-media-smart-crop-video">
      <strong>智能裁剪</strong>
      </a>
   </div>
   <p>
      <em>使用 AI 自动识别图像或视频中的焦点，并在裁剪时保持该焦点</em>
   </p>
</td>
<td>
   <a href="/help/assets/dynamic-media/video.md">
   <img alt=" AI 生成的视频字幕" src="./assets/videos-with-captions.jpg" />
   </a>
   <div>
      <a href="/help/assets/dynamic-media/video.md">
      <strong>AI 生成的视频字幕</strong>
      </a>
   </div>
   <p>
      <em>使用人工智能为视频内容自动生成字幕。</em>
   </p>
</td>
</table>

>[!TAB 资产发现]

## 资产发现 {#asset-discovery}

将资产导入 AEM Assets 后，如何从如此庞大的收藏集中快速找到合适的资产是一大挑战。

AEM Assets 提供的功能可帮助您快速找到合适的资产。这些功能包括 AI 生成的标记（智能标记）、自定义元数据和增强的搜索功能。

**元数据管理**：在开启资产管理工作时，元数据是最关键的组成部分。一旦资产分发给用户，元数据的管理就会完全脱离管理员的掌控。高质量的资产元数据能够显著提升搜索效果，而这正是任何数字资产管理（DAM）工具的最终目标。


**元数据表单**：Assets as a Cloud Service 默认提供众多标准元数据字段。如果您有额外的元数据需求，希望有更多的元数据字段来添加与业务相关的元数据。元数据表单允许企业在资产的“详细信息”页面中添加自定义元数据字段。业务特有的元数据改善对其资产的治理和发现。您可以从头开始创建表单，也可以重新利用现有表单。

<table>
<td>
   <a href="/help/assets/metadata-assets-view.md">
   <img alt="管理元数据资产视图" src="./assets/manage-metadata-assets-view.jpeg" />
   </a>
   <div>
      <a href="/help/assets/metadata-assets-view.md">
      <strong>在资产视图中管理元数据</strong>
      </a>
   </div>
   <p>
      <em>了解如何使用资产视图管理元数据及元数据表单。</em>
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
      <em>了解在将资产迁移至 AEM 之前和之后如何进行元数据管理。</em>
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
      <em>了解如何使用管理员视图管理元数据及元数据表单。</em>
   </p>
</td>
</table>

**智能标记**：智能标记借助 Adobe Sensei 的人工智能框架，基于您的标记结构和业务分类法训练图像识别算法。随后，该内容智能可用于为另一组资产自动应用相关标记。AEM 默认会自动为上传的资产应用智能标记。

**搜索资产**：一旦配置了合适的元数据，AEM Assets 便可支持使用多种运算符、通配符、高级查询和自定义筛选器进行搜索。

**上下文搜索**：AEM Assets 还提供上下文搜索功能，您可通过输入文本提示词，在资产库中搜索相关资产。Experience Manager Assets 会自动将这些文本提示词转换为搜索过滤器，并显示搜索结果。您可以通过“过滤器窗格”查看并更改自动过滤器，以进一步缩小搜索结果范围。

<table>
<td>
   <a href="/help/assets/smart-tags.md">
   <img alt="AEM Assets 中的智能标记" src="./assets/smart-tags-ai.jpeg" />
   </a>
   <div>
      <a href="/help/assets/smart-tags.md">
      <strong>为资产添加 AI 智能标记</strong>
      </a>
   </div>
   <p>
      <em>了解如何为上传的资产自动应用智能标记。</em>
   </p>
</td>


<td>
   <a href="/help/assets/search-assets-view.md">
   <img alt="搜索资产视图" src="./assets/search-assets-view-landing.jpeg" />
   </a>
   <div>
      <a href="/help/assets/search-assets-view.md">
      <strong>在资产视图中搜索资产</strong>
      </a>
   </div>
   <p>
      <em>了解如何在资产视图中有效使用上下文搜索及其他搜索功能。</em>
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
      <em>了解多种场景，帮助 AEM 用户执行从基本到高级的不同等级的搜索。</em>
   </p>
</td>
</table>

>[!TAB 资产治理]

## 资产管理和治理 {#asset-management-governance}

将资产上传至 AEM Assets 并设置好元数据以提升可发现性后，您即可通过资产视图的用户友好界面，执行多项数字资产管理任务。

**资产管理任务**：基本任务包括搜索、下载、移动、复制、重命名、删除、更新和编辑等操作。

您还可以管理资产版本、设置资产状态以及配置资产过期时间。

**我的工作区**：资产视图还包括一个提供各种小部件的可自定义工作区。通过这些小部件，您可以方便地访问 Assets 用户界面的关键区域以及与您最相关的信息。此页面作为一站式解决方案，可概览您的工作项，并快速访问关键工作流。

**Content Credentials**：AEM Assets 支持的另一项强大功能是 Content Credentials。品牌对内容透明度、AI 来源披露以及防止资产被篡改的关注程度空前提高。Adobe 发起的 Content Authenticity Initiative（简称 CAI）致力于构建符合内容出处与真实性联盟（Coalition for Content Provenance and Authenticity，C2PA）技术标准的工具。Content Credentials 是一种全新的加密且可防篡改的元数据，有助于帮助查看者了解内容的来源与演变，并保障品牌资产的完整性。Content Credentials 可包含多种溯源数据，深入呈现数字资产的历史信息。

<table>
<td>
   <a href="/help/assets/manage-organize-assets-view.md">
   <img alt="资产管理任务" src="./assets/asset-management.jpeg" />
   </a>
   <div>
      <a href="/help/assets/manage-organize-assets-view.md">
      <strong>资产管理任务</strong>
      </a>
   </div>
   <p>
      <em>了解如何执行基础及高级的资产管理任务。</em>
   </p>
</td>


<td>
   <a href="/help/assets/my-workspace-assets-view.md">
   <img alt="我的工作区" src="./assets/my-workspace.jpeg" />
   </a>
   <div>
      <a href="/help/assets/my-workspace-assets-view.md">
      <strong>我的工作区</strong>
      </a>
   </div>
   <p>
      <em>了解如何使用“我的工作区”，快速访问 Assets 用户界面的关键区域。</em>
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
      <em>通过 Content Credentials 洞察数字资产的历史信息。</em>
   </p>
</td>
</table>

**收藏集**：AEM Assets 还支持将资产组织到收藏集中进行管理。收藏集是 Adobe Experience Manager Assets 视图中的一组资产、文件夹或其他收藏集。使用收藏集可在用户之间共享资产。收藏集与文件夹的不同之处是可包含来自不同位置的资产。您可以与一个用户共享多个收藏集。每个收藏集都包含对资产的引用。收藏集中会保持资产的引用完整性。

**通知**：资产视图中的通知功能可帮助您监控存储库中对资产、文件夹或收藏集执行的各类操作。需要选择并订阅将向您发送其通知的内容。还可配置向您发送其通知的类别。

**检测重复资产**：AEM Assets 还支持检测重复资产。如果 DAM 用户上传的一个或多个资产已存在于存储库中，Experience Manager 将自动检测到重复项并通知用户。



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
      <em>了解如何将资产整理为收藏集，以实现高效的资产共享。</em>
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
      <em>了解如何设置通知，以监控对资产、文件夹或收藏集执行的各项操作。</em>
   </p>
</td>
<td>
   <a href="/help/assets/detect-duplicate-assets.md">
   <img alt="检测重复的资产" src="./assets/duplicate-assets.jpeg" />
   </a>
   <div>
      <a href="/help/assets/detect-duplicate-assets.md">
      <strong>检测重复的资产</strong>
      </a>
   </div>
   <p>
      <em>检测上传至 AEM Assets 的重复资产并向用户发出通知。</em>
   </p>
</td>
</table>

>[!TAB 集成]

## 与 Adobe 及非 Adobe 应用程序的集成 {#integration-adobe-non-adode-apps}

AEM Assets 可与多种 Adobe 及非 Adobe 应用程序实现无缝集成。以下是可用集成方式的概览：

+++**与 Adobe 及非 Adobe 应用程序的集成**

* **具有 OpenAPI 功能的 Dynamic Media**： [具有 OpenAPI 功能的 Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) 提供一整套完整的[搜索](/help/assets/search-assets-api.md)和[交付](/help/assets/deliver-assets-apis.md) API。它可帮助开发人员轻松地将资产交付与他们的应用程序集成。这些应用程序既包括 Adobe 应用，也包括第三方应用。它提供了微前端资产选择器用户界面，用于搜索并选择已审核的资产。该选择器可轻松集成到基于 JavaScript 框架（如 React JS、Angular JS 和 Vanilla JS）的任何应用程序中。

* **微前端资产选择器**：微前端资产选择器提供一个用户界面，它可与 Experience Manager Assets 存储库集成，让您能够浏览或搜索存储库中可用的数字资产。
然后您可以在应用程序创作体验中使用它们。
您可以将资产选择器集成至 Adobe 应用程序或非 Adobe 应用程序中。

<table>
<td>
   <a href="/help/assets/dynamic-media-open-apis-overview.md">
   <img alt="具有 OpenAPI 功能的 Dynamic Media 概述" src="./assets/dm-openapi-uses.jpeg" />
   </a>
   <div>
      <a href="/help/assets/dynamic-media-open-apis-overview.md">
      <strong>具有 OpenAPI 功能的 Dynamic Media 概述</strong>
      </a>
   </div>
   <p>
      <em>了解主要优势及如何启用。</em>
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
      <em> 配置角色以限制对已审核资产的访问权限。</em>
   </p>
</td>
<td>
   <a href="/help/assets/overview-asset-selector.md">
   <img alt="资产选择器" src="./assets/integration-asset-selector.jpeg" />
   </a>
   <div>
      <a href="/help/assets/overview-asset-selector.md">
      <strong>微前端资产选择器</strong>
      </a>
   </div>
   <p>
      <em>了解如何将微前端资产选择器集成至 Adobe 或非 Adobe 应用程序中。</em>
   </p>
</td>
</table>

+++

+++**与 Adobe 应用程序的原生集成**

* **与 Adobe Workfront 集成**：[!DNL Adobe Workfront] 是一款工作管理应用程序，帮助您在一个平台中统一管理工作全流程。[!DNL Workfront] 和 [!DNL Adobe Experience Manager Assets] 的集成，通过将工作管理与数字资产管理深度融合，帮助组织提升内容产出效率并加快产品上市速度。在 Workfront 的工作管理环境中，用户可以访问所需的文档和图像。

  Adobe 提供原生方式[将 [!DNL Workfront] 和 [!DNL Adobe Experience Manager Assets] 集成](https://experienceleague.adobe.com/zh-hans/docs/workfront/using/documents/wf-aem-integrations/wf-aem-essentials/aem-asset-integrations)。

* **与 Figma 集成**：AEM Assets 可以与 Figma 原生集成，使设计人员能够直接在 Figma 用户界面中访问 AEM Assets 中存储的资产。您可以将 AEM Assets 中管理的内容放入 Figma 画布，然后将新内容或编辑过的内容保存在 AEM Assets 存储库中。要访问 Figma 社区页面上提供的 AEM Assets 连接器，请单击[此处](https://www.figma.com/community/plugin/1512561378275712210/adobe-experience-manager-aem-assets-connector)。

* **与 Adobe Express 原生集成**：AEM Assets 与 Adobe Express 原生集成，使您能够直接在 Adobe Express 用户界面中访问 AEM Assets 中存储的资产。您可以将 AEM Assets 中管理的内容放入 Express 画布中，并将新建或编辑的内容保存回 AEM Assets 存储库。

* **将 AEM Assets 与 Creative Cloud 连接**：Experience Manager Assets 可以与另一个 IMS 组织中配置的 Creative Cloud 使用权限连接。此功能可让您使用 AEM Assets 中的最新 Creative Cloud 集成，包括 Express 和 Creative Cloud Libraries。如果您的 Creative Cloud 产品与 AEM Assets 分别配置在不同的 IMS 组织中，您可以连接至其他 Creative Cloud 组织，从而在这两个解决方案之间执行集成工作流。

<table>
<td>
   <a href="/help/assets/workfront-integrations.md">
   <img alt="与 Adobe Workfront 集成" src="./assets/integration-adobe-workfront.jpeg" />
   </a>
   <div>
      <a href="/help/assets/workfront-integrations.md">
      <strong>与 Adobe Workfront 集成</strong>
      </a>
   </div>
   <p>
      <em>集成 Adobe Workfront，实现工作全生命周期的一体化管理。</em>
   </p>
</td>
<td>
   <a href="/help/assets/manage-collections-assets-view.md">
   <img alt="与 Figma 集成" src="./assets/integration-commerce.jpeg" />
   </a>
   <div>
      <a href="/help/assets/manage-collections-assets-view.md">
      <strong>与 Figma 集成</strong>
      </a>
   </div>
   <p>
      <em>在 Figma 用户界面中访问存储于 AEM Assets 的资产</em>
   </p>
</td>
<td>
   <a href="/help/assets/native-integration-adobe-express.md">
   <img alt="与 Adobe Express 的原生集成" src="./assets/integration-adobe-express.jpeg" />
   </a>
   <div>
      <a href="/help/assets/native-integration-adobe-express.md">
      <strong>与 Adobe Express 的原生集成</strong>
      </a>
   </div>
   <p>
      <em>将 AEM Assets 中的资产置入 Express 画布，并将更新后的资产保存至 AEM。</em>
   </p>
</td>


</table>


* **与 Adobe Journey Optimizer 集成**：通过 Adobe Experience Manager Assets 将营销与创意工作流融合在一起。通过与 Adobe Journey Optimizer 的原生集成，您可访问 Assets as a Cloud Service 来存储、管理、查找及分发数字资产。它提供一个统一的集中式存储库，便于您在创建消息内容时直接调用所需资产。

* **与 Commerce 集成**：Adobe Experience Manager (AEM) Assets 的 Commerce 集成功能将 AEM 强大的数字资产管理（DAM）能力与 Adobe Commerce 相结合，全面提升电商体验。通过将 Commerce 项目连接至 AEM 强大的资产管理环境，这些能力得以实现，从而为管理和交付电商前端资产提供无缝、可扩展且高效的解决方案。
* **将 AEM Assets 与用于 Edge Delivery Services 的基于文档的创作流程集成**：如果 [!DNL AEM Assets] 与您的基于文档的创作工具（如 [!DNL Microsoft Word] 或 [!DNL Google Docs]）集成，您的创作工具中就会提供一个资产选择器。使用此资产选择器可访问 [!DNL AEM Assets]，并将已批准的资产插入到您的内容中。
如果您已有一个 [!DNL Edge Delivery Services] 网站，请参阅 [[!DNL AEM Assets] 插件](https://github.com/adobe-rnd/aem-assets-plugin/blob/main/README.md) 文档，了解如何将 [!DNL AEM Assets] 集成到您现有的 [!DNL AEM] 项目中。

* **将 [!DNL AEM Assets] 集成至基于 [!DNL Universal Editor] 的[!DNL Edge Delivery Services]** 创作流程中：配置 [!DNL Universal Editor] 以实现与 [!DNL AEM Assets] 的集成。通过此集成，您可以借助具备 OpenAPI 功能的 [!DNL Dynamic Media with OpenAPI capabilities] 交付资产。

   * 请参阅[在  [!DNL Edge Delivery]  站点](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/#configuration-in-edge-delivery-site)中进行配置，了解如何在 [!DNL Universal Editor] 中添加自定义资产选择器功能。自定义资产选择器可让您将资产直接插入至 [!DNL Universal Editor] 内容中。
   * 请参阅[扩展概述](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/#extension-overview)，了解如何在 [!DNL Universal Editor] 中创作内容时访问 [!DNL AEM Assets] 并插入资产。

<table>
<td>
   <a href="https://experienceleague.adobe.com/zh-hans/docs/journey-optimizer/using/content-management/combine/assets">
   <img alt="与 Adobe Journey Optimizer 集成" src="./assets/integration-figma.jpeg" />
   </a>
   <div>
      <a href="https://experienceleague.adobe.com/zh-hans/docs/journey-optimizer/using/content-management/combine/assets">
      <strong>与 Adobe Journey Optimizer 集成</strong>
      </a>
   </div>
   <p>
      <em>通过与 AJO 的集成，将营销与创意工作流程无缝融合</em>
   </p>
</td>
<td>
   <a href="https://experienceleague.adobe.com/zh-hans/docs/commerce/aem-assets-integration/overview">
   <img alt="与 Commerce 的集成" src="./assets/integration-ajo.jpeg" />
   </a>
   <div>
      <a href="https://experienceleague.adobe.com/zh-hans/docs/commerce/aem-assets-integration/overview">
      <strong>与 Commerce 的集成</strong>
      </a>
   </div>
   <p>
      <em>将 AEM Assets 与 Commerce 集成，提升电商体验。</em>
   </p>
</td>
<td>
   <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md">
   <img alt="将 AEM Assets 与 EDS 集成" src="./assets/integrate-ue-assets.jpeg" />
   </a>
   <div>
      <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md">
      <strong>将 AEM Assets 与 EDS 集成</strong>
      </a>
   </div>
   <p>
      <em>将 AEM Assets 集成至基于文档和 Universal Editor 的创作流程中。</em>
   </p>
</td>
</table>

+++

>[!TAB 资产激活]

## 资产激活 {#asset-activation}

使用 AEM Assets，通过从 Content Hub 到 Dynamic Media 的集成——包括强大的 OpenAPI 功能——充分释放数字资产的全部潜能。AEM Assets 提供一整套全面的解决方案，旨在简化资产转换流程，并优化跨多个渠道的投放效率。

+++**Content Hub**

Content Hub 是 Experience Manager Assets as a Cloud Service 的一部分，旨在为组织及其业务合作伙伴实现对品牌内容访问的民主化。它侧重于大规模分发资产以进行激活，并创建品牌内容变体，以提高营销敏捷度。

Content Hub 具有以下主要优势：

* **在直观的门户中查找并共享所有品牌批准的资产**：AEM Assets 作为统一可信的数据源，所有经批准的资产将自动以扁平化层级结构呈现在 Content Hub 中，从而提升搜索体验。

* **可配置的用户界面**：Content Hub 中最常用的属性（如搜索筛选器、添加或导入资产时可用的字段、资产属性以及品牌横幅内容）均支持配置，管理员可根据需求轻松自定义 Content Hub 的用户界面。

* **使非创意人员在保持品牌一致性的前提下编辑与重混内容**：Content Hub 支持使用 Adobe Express 创建新内容（需具备 Adobe Express 授权）。您可以使用易于使用的工具编辑现有内容，使用模板和品牌元素制作品牌变体，并使用 Adobe Firefly 的最新 GenAI功 能创建新内容。

* **深入了解内容在各团队中的使用情况**：[!DNL Content Hub] 提供有关资产的宝贵洞察，解决营销相关方常见的难题——即资产在营销活动、渠道和不同地区的使用情况统计数据。通过清楚地了解资产的性能和受欢迎程度，它提供了对增强用户体验至关重要的可操作洞察。

<table>
<td>
   <a href="/help/assets/product-overview.md">
   <img alt="Content Hub 概述" src="./assets/content-hub-overview.jpeg" />
   </a>
   <div>
      <a href="/help/assets/product-overview.md">
      <strong>Content Hub 概述</strong>
      </a>
   </div>
   <p>
      <em>深入了解 Content Hub 的主要优势及访问方式。</em>
   </p>
</td>


<td>
   <a href="/help/assets/configure-content-hub-ui-options.md">
   <img alt="配置 Content Hub 用户界面" src="./assets/content-hub-configuration.jpeg" />
   </a>
   <div>
      <a href="/help/assets/configure-content-hub-ui-options.md">
      <strong>配置 Content Hub 用户界面</strong>
      </a>
   </div>
   <p>
      <em>了解如何配置 Content Hub 用户界面中提供的各种选项。</em>
   </p>
</td>
<td>
   <a href="/help/assets/edit-images-content-hub.md">
   <img alt="使用 Adobe Express 进行编辑" src="./assets/content-hub-express.jpeg" />
   </a>
   <div>
      <a href="/help/assets/edit-images-content-hub.md">
      <strong>使用 Adobe Express 进行编辑</strong>
      </a>
   </div>
   <p>
      <em>了解如何使用 Adobe Express 在 Content Hub 中编辑图像。</em>
   </p>
</td>
</table>

+++

+++**Dynamic Media**

Dynamic Media 可帮助您按需交付丰富的视觉营销和推广资产。它还能帮助您创建并呈现互动式浏览体验，包括缩放、360 度旋转以及视频内容。您的资产会根据需求动态缩放，以适配网页、移动端和社交平台的展示。通过一组主要源资产（如图像、视频和 3D 文件），Dynamic Media 能够实时生成并分发多种内容变体，并借助其全球化、可扩展且性能优化的内容分发网络（CDN）进行高效交付。

Dynamic Media 提供以下关键功能：

* **智能图像处理**：智能图像处理可根据用户浏览器的能力，自动优化图像格式和文件大小，从而显著提升图像资产的交付性能。该功能可与您现有的图像预设配合使用，并在交付时智能优化图像内容。该智能机制还会根据浏览器类型和网络连接速度，进一步压缩图像文件大小。

* **自适应视频集**：自适应视频集将同一视频的多个版本（以不同码率和格式编码）进行分组管理。您首先上传原始主视频至系统，作为创建自适应视频集的起点。Dynamic Media 会自动对该视频进行调整尺寸或转码，生成多个不同版本的视频。在内容投放时，Dynamic Media 会智能判断应使用的视频尺寸、质量和格式，并将最合适的版本传递至手机、平板或桌面设备。

* **智能裁剪**：借助 Adobe Sensei 的 AI 能力，自动识别图像或视频中的焦点，并在裁剪时保持该焦点不变。该功能可在不同屏幕尺寸下准确保留图像或视频中的目标焦点，从而省去繁琐的手动操作，提供高质量、加载迅速的图像和视频内容，确保在任何设备或屏幕上均呈现良好效果。

* **Dynamic Media 模板**：使用 Dynamic Media 模板这一所见即所得的模板编辑器，为横幅和宣传单创建可实时自定义的模板。发布您的 Dynamic Media 模板，并在下游应用程序中使用该模板。Dynamic Media 模板包含图像图层和文本图层。为模板中的图像图层和文本图层添加参数，并通过 Dynamic Media URL 实现图层的实时重定位、调整尺寸及内容更新。

* **多音轨与字幕**：为主视频添加多个字幕和多条音轨。此功能意味着全球观众都能看懂您的视频。只需自定义一个主视频，即可发布到多种语言的全球观众，并遵循不同地区的辅助功能准则。此外，作者从用户界面中的一个选项卡即可管理字幕和音轨。

* **支持通过 HTTP (DASH) 的动态自适应流媒体传输**：Dynamic Media 支持（在启用 CMAF 的情况下）在 Dynamic Media 视频传递时的自适应流媒体传输，为用户带来更佳的视频观看体验。DASH 是自适应视频流的国际标准协议，已在业界被广泛采用。

* **AI 生成的视频字幕**：Adobe Dynamic Media 利用人工智能自动为视频内容生成字幕。支持超过 60 种语言，可以在发布视频之前查看和预览字幕。

有关可用的 Dynamic Media 产品信息，请参阅 [Dynamic Media Prime 和 Ultimate](/help/assets/dynamic-media/dm-prime-ultimate.md)。



<table>
<td>
   <a href="/help/assets/dynamic-media/dynamic-media.md">
   <img alt="使用 Dynamic Media" src="./assets/work-with-dynamic-media.jpeg" />
   </a>
   <div>
      <a href="/help/assets/dynamic-media/dynamic-media.md">
      <strong>使用 Dynamic Media</strong>
      </a>
   </div>
   <p>
      <em>了解如何投放资产，以适配网页、移动端和社交平台的使用需求。</em>
   </p>
</td>


<td>
   <a href="/help/assets/dynamic-media/dm-journey-part1.md">
   <img alt="Dynamic Media 历程" src="./assets/dm-journey.jpeg" />
   </a>
   <div>
      <a href="/help/assets/dynamic-media/dm-journey-part1.md">
      <strong>Dynamic Media 历程</strong>
      </a>
   </div>
   <p>
      <em>了解 Dynamic Media 如何为您的工作带来价值。</em>
   </p>
</td>
<td>
   <a href="/help/assets/dynamic-media/dm-best-practices.md">
   <img alt="将 AEM Assets 连接到 Creative Cloud" src="./assets/dm-best-practices.jpeg" />
   </a>
   <div>
      <a href="/help/assets/dynamic-media/dm-best-practices.md">
      <strong>Dynamic Media 最佳实践</strong>
      </a>
   </div>
   <p>
      <em>处理图像、视频和查看器时的最佳实践。</em>
   </p>
</td>
</table>

+++

+++**具有 OpenAPI 功能的 Dynamic Media**

在当今快节奏的数字世界中，充分释放品牌数字资产的潜力对于保持竞争优势至关重要。全面的数字资产管理 (DAM) 解决方案有助于资产治理、促进品牌一致性、加速内容传递，同时确保品牌完整性和卓越的客户体验。

具有 OpenAPI 功能的 Dynamic Media 将 DAM 置于敏捷高效的内容供应链生态系统的核心，以确保资产治理和传递。

具有 OpenAPI 功能的 Dynamic Media 提供以下关键优势：

* **无缝集成**：具有 OpenAPI 功能的 Dynamic Media 提供了一套全面的搜索和传递 API。它有助于开发人员轻松地[将资产传递与其应用程序集成](/help/assets/integrate-dynamic-media-open-apis.md)。这些应用程序包括 Adobe 以及第三方应用程序。它提供了一个[微前端资产选择器用户界面](/help/assets/overview-asset-selector.md)，用于搜索和选择已批准的资产。该选择器可以轻松地与基于 JavaScript 框架（如 React JS、Angular JS 和 Vanilla JS）的任何应用程序集成。

* **集中管理数字资产**：DAM 是所有数字资产的单一数据源。您的数字资产在 AEM Assets 中进行集中管理，并通过使用传递 URL 进行引用，无需复制资产二进制文件，即可传递给消费应用程序。

* **实时更新**：对 DAM 中已批准资产所做的任何更改（包括版本更新和元数据修改）都会自动反映在传递 URL 中。通过内容传递网络为具有 OpenAPI 功能的 Dynamic Media 配置了一个较短的生存时间 (TTL) 值，即 10 分钟，这样，在不到 10 分钟的时间内，更新就会在所有创作和发布的界面上显示出来。

* **品牌一致性**：只有[经过品牌批准的资产](/help/assets/approve-assets.md)才会暴露给下游应用程序。[品牌经理和营销人员对品牌资产保持严格控制](/help/assets/restrict-assets-delivery.md)。只有经过批准的最新版本资产可供使用，以确保所有渠道和应用程序的品牌一致性。

* **网页优化的传递方式**：数字资产以网页优化的方式传递，以提升您的数字体验的核心网页指标。这个优化包括支持图像的 WebP 演绎版、通过 HLS 或 DASH 协议实现视频的自适应流媒体传输，以及文档的原始演绎版。

* **动态资产转换**：该系统允许您使用称作“图像修改器”的 URL 参数进行即时图像转换。[例如宽度、高度、旋转、翻转、质量、裁切、格式和智能裁剪](/help/assets/deliver-assets-apis.md)。转换后的演绎版是动态生成的，并通过内容传递网络无缝传递。

* **安全传递资产**：具有 OpenAPI 功能的 Dynamic Media 提供了一种控制访问您的数字资产的机制。您可以将用户角色或组指定为要保护的资产的元数据，并设置预定义的时间范围，在此期间[只有授权用户才能访问这些资产](/help/assets/restrict-assets-delivery.md)。在限制期内，未经授权的用户无法解析受保护资产的传递 URL。

有关可用的 Dynamic Media 产品信息，请参阅 [Dynamic Media Prime 和 Ultimate](/help/assets/dynamic-media/dm-prime-ultimate.md)。

<table>
<td>
   <a href="/help/assets/dynamic-media-open-apis-overview.md">
   <img alt="具有 OpenAPI 功能的 Dynamic Media 概述" src="./assets/dm-openapi-uses.jpeg" />
   </a>
   <div>
      <a href="/help/assets/dynamic-media-open-apis-overview.md">
      <strong>具有 OpenAPI 功能的 Dynamic Media 概述</strong>
      </a>
   </div>
   <p>
      <em>了解主要优势及如何启用。</em>
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
      <em> 配置角色以限制对已审核资产的访问权限。</em>
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
      <em>将远程 AEM Assets 集成至 AEM Sites 环境中。</em>
   </p>
</td>
</table>

+++

>[!TAB 洞察]

## 资产洞察 {#asset-insights}

资产报告使管理员能够全面了解 Adobe Experience Manager Assets View 环境中的各类活动。这些数据可提供有关用户如何与内容及产品交互的有价值信息。所有用户都可以访问 Insights 仪表板，被分配给管理员产品配置文件的用户可以创建用户定义的报告。

您可以生成多种类型的报告，例如上传、下载以及 Dynamic Media 投放报告。

* **资产视图中的洞察功能**：资产视图支持通过 Insights 仪表板查看 Assets 视图环境的实时数据。可查看过去 30 天或过去 12 个月的实时事件指标。这些事件包括下载、上传、存储使用情况、热门搜索、按资产大小分类的资产数量，以及按资产类型分类的资产数量。

* **管理员视图中的 Adobe Analytics 集成**：Assets Insights 功能可用于追踪图像在第三方网站、营销活动以及 Adobe 创意解决方案中的用户评分和使用统计数据。此功能有助于洞察图像的效果和受欢迎程度。Assets Insights 可捕获用户活动的详细信息，例如图像被评分的次数、点击次数，以及曝光量（即图像在网站上的加载次数）。系统会根据这些统计数据为图像分配评分。您可以利用这些评分和性能统计数据，挑选热门图像用于产品目录、营销活动等用途。您甚至可以根据这些统计数据制定资产归档和许可续订策略。若要让 Assets Insights 显示资产的使用统计数据，需先配置该功能，以便从 Adobe Analytics 获取报告数据。

* **Content Hub 洞察功能**：Content Hub 提供有关资产的宝贵洞察，解决营销相关方常见的难题——即资产在营销活动、各渠道及不同地区中的使用统计问题。通过清楚地了解资产的性能和受欢迎程度，它提供了对增强用户体验至关重要的可操作洞察。

<table>
<td>
   <a href="/help/assets/manage-reports-assets-view.md">
   <img alt="在资产视图中管理报告" src="./assets/assets-insights-assets-view.jpeg" />
   </a>
   <div>
      <a href="/help/assets/manage-reports-assets-view.md">
      <strong>在资产视图中管理报告</strong>
      </a>
   </div>
   <p>
      <em>通过资产视图获取关键成功指标的洞察。</em>
   </p>
</td>


<td>
   <a href="/help/assets/asset-reports.md">
   <img alt="在管理员视图中管理报告" src="./assets/assets-insights-admin-view.jpeg" />
   </a>
   <div>
      <a href="/help/assets/asset-reports.md">
      <strong>在管理员视图中管理报告</strong>
      </a>
   </div>
   <p>
      <em>了解如何在管理员视图中管理与 Adobe Analytics 集成的报告。</em>
   </p>
</td>
<td>
   <a href="/help/assets/insights-content-hub.md">
   <img alt="Content Hub 中的资产洞察" src="./assets/asset-insights-content-hub.jpeg" />
   </a>
   <div>
      <a href="/help/assets/insights-content-hub.md">
      <strong>Content Hub 中的资产洞察</strong>
      </a>
   </div>
   <p>
      <em>了解如何在 Content Hub 中查看资产洞察信息。</em>
   </p>
</td>
</table>

>[!ENDTABS]

## 可用的基于角色的数字资产管理体验 {#persona-based-experiences}

Adobe 为您提供强大的数字资产管理（DAM）解决方案，让您能够充分利用数字资产。Adobe Experience Manager Assets 具有两种使用相同 Cloud Service 存储库的独立体验：

* **管理视图**：现有资产作为 Cloud Service 用户界面。通过管理员视图使用所有高级数字资产管理功能，包括集成、工作流、内容自动化、发布等。

* **资产视图**：Adobe 的轻量级资产管理体验，用于存储、管理、发现和使用数字资产。简化的用户界面包含基本的数字资产管理功能。专为轻量级 DAM 用户设计，重点支持上传、元数据管理、搜索、下载与共享等功能。

![add-tags](assets/newui-overview.svg)

有权访问管理视图的用户也可以访问资产视图。资产视图提供了一个简化的用户界面，使您可以轻松管理、探索和分发您的数字资产。 来自不同职能部门（包括创意团队、营销团队和业务线团队）的广泛用户群体可以在资产方面协作工作，在需要时随时随地访问合适的且经过批准的资产。许多临时 DAM 用户更喜欢资产视图，因为它只包含一部分功能。该体验面向创意人员、只读资产消费者和轻量级 DAM 用户。

DAM 库管理员、开发人员和超级用户可以继续使用管理视图，或根据需要在这些用户界面之间切换。您可以选择最适合您角色的体验。

关于如何访问资产视图以及通过管理员视图提供的一些简化方法的信息，请参阅[资产视图简介](/help/assets/assets-view-introduction.md)。

## AEM 中的 AI 助手

对于已[满足先决条件](/help/implementing/cloud-manager/ai-assistant-in-aem.md#get-access)的客户，AEM 中的 AI 助手可供其组织的用户使用。参见 [AEM 中的 AI 助手](/help/implementing/cloud-manager/ai-assistant-in-aem.md)。
