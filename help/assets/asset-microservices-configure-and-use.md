---
title: 配置和使用资源微服务
description: 配置并使用云原生资源微服务大规模处理资源。
contentOwner: AG
feature: Asset Compute Microservices, Asset Processing, Asset Management
role: Architect, Admin
exl-id: 7e01ee39-416c-4e6f-8c29-72f5f063e428
source-git-commit: 55ee7f866bcfc4ecc2e203102872af9752240019
workflow-type: tm+mt
source-wordcount: '2909'
ht-degree: 3%

---

# 使用资产微服务和处理配置文件 {#get-started-using-asset-microservices}

| [搜索最佳实践](/help/assets/search-best-practices.md) | [元数据最佳实践](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | [具有 OpenAPI 功能的 Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets 开发人员文档](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

资产微服务提供使用云原生应用程序（也称为工作程序）进行可扩展和弹性资产处理。 Adobe管理服务以优化处理各种资源类型和处理选项。

资产微服务允许您处理[多种文件类型](/help/assets/file-format-support.md)，这些类型涵盖的现成格式比以前版本的[!DNL Experience Manager]可能具有的格式更多。 例如，现在可以提取PSD和PSB格式的缩略图，但以前需要第三方解决方案，如[!DNL ImageMagick]。

资源处理依赖于&#x200B;**[!UICONTROL 处理配置文件]**&#x200B;中的配置。 Experience Manager提供了基本的默认设置，并允许管理员添加更具体的资源处理配置。 管理员创建、维护和修改后处理工作流的配置，包括可选自定义。 通过自定义工作流，开发人员可以扩展默认产品。

<!-- Proposed DRAFT diagram for asset microservices flow - see section "asset-microservices-flow.png (asset-microservices-configure-and-use.md)" in the PPTX deck

https://adobe-my.sharepoint.com/personal/gklebus_adobe_com/_layouts/15/guestaccess.aspx?guestaccesstoken=jexDC5ZnepXSt6dTPciH66TzckS1BPEfdaZuSgHugL8%3D&docid=2_1ec37f0bd4cc74354b4f481cd420e07fc&rev=1&e=CdgElS
-->

![资产处理的高级视图](assets/asset-microservices-flow.png "资产处理的高级视图")

>[!NOTE]
>
>此处描述的资产处理过程替换了[!DNL Experience Manager]早期版本中存在的`DAM Update Asset`工作流模型。 资产微服务处理取代了大多数标准演绎版生成和元数据相关步骤，并且后处理工作流配置可以替换剩余步骤（如果有）。

## 了解资源处理选项 {#get-started}

[!DNL Experience Manager]允许进行以下级别的处理。

| 选项 | 描述 | 涵盖的用例 |
|---|---|---|
| [默认配置](#default-config) | 它按原样可用，无法修改。 此配置提供基本的演绎版生成功能。 | <ul> <li>[!DNL Assets]用户界面使用的标准缩略图（48、140和319像素） </li> <li> 大型预览（Web呈现版本 — 1280像素） </li><li> 元数据和文本提取。</li></ul> |
| [自定义配置](#standard-config) | 由管理员通过用户界面配置。 通过扩展默认选项，为生成演绎版提供了更多选项。 扩展现成选项以提供不同的格式和演绎版。 | <ul><li>FPO（仅用于置入）演绎版。 </li> <li>更改图像的文件格式和分辨率</li> <li> 有条件地应用于配置的文件类型。 </li> </ul> |
| [自定义配置文件](#custom-config) | 管理员通过用户界面配置通过自定义应用程序使用自定义代码来调用[Asset compute服务](https://experienceleague.adobe.com/en/docs/asset-compute/using/introduction)。 以云原生的可伸缩方法支持更复杂的需求。 | 查看[允许的用例](#custom-config)。 |

<!-- To create custom processing profiles specific to your custom requirements, say to integrate with other systems, see [post-processing workflows](#post-processing-workflows).
-->

## 支持的文件格式 {#supported-file-formats}

资源微服务为处理、生成演绎版或提取元数据等多种文件格式提供支持。 有关MIME类型的完整列表以及每种类型支持的功能，请参阅[支持的文件格式](file-format-support.md)。

## 默认配置 {#default-config}

预配置了某些默认值，以确保Experience Manager中所需的默认呈现版本可用。 默认配置还可确保元数据提取和文本提取操作可用。 用户可以立即开始上传或更新资产，默认情况下可以进行基本处理。

使用默认配置时，仅配置最基本的处理配置文件。 此类处理配置文件在用户界面中不可见，您无法对其进行修改。 它始终执行以处理上传的资产。 此类默认处理配置文件可确保在所有资源上完成[!DNL Experience Manager]所需的基本处理。

<!-- ![processing-profiles-standard](assets/processing-profiles-standard.png)
-->

## 标准配置 {#standard-config}

[!DNL Experience Manager]提供了根据用户的需要为常用格式生成更具体的呈现版本的功能。 管理员可以创建其他[!UICONTROL 处理配置文件]来促进此类演绎版的创建。 然后，用户将一个或多个可用配置文件分配给特定文件夹，以完成其他处理。 例如，附加处理可以为Web、移动设备和平板电脑生成演绎版。 以下视频说明如何创建和应用[!UICONTROL 处理配置文件]，以及如何访问创建的演绎版。

* **演绎版宽度和高度**：演绎版宽度和高度规范提供了所生成输出图像的最大大小。 资源微服务会尝试生成可能的最大演绎版，其宽度和高度分别不大于指定的宽度和高度。 纵横比保持不变，与原始纵横比相同。 空值意味着资产处理会假定原始资产的像素尺寸。

* **MIME类型包含规则**：在处理具有特定MIME类型的资源时，将首先根据演绎版规范的排除MIME类型值检查MIME类型。 如果与该列表匹配，则不会为资源(阻止列表)生成此特定演绎版。 否则，将针对包含的MIME类型检查MIME类型，如果它与列表匹配，则生成演绎版(允许列表)。

* **特殊FPO演绎版**：将来自[!DNL Experience Manager]的大型资源放入[!DNL Adobe InDesign]文档时，创意专业人士会在[放置资源](https://helpx.adobe.com/indesign/using/placing-graphics.html)后等待相当长的时间。 同时，用户被阻止使用[!DNL InDesign]。 这会中断创作流并对用户体验产生负面影响。 Adobe功能允许首先在[!DNL InDesign]文档中临时放置小型演绎版，稍后可按需使用全分辨率资源替换小型演绎版。 [!DNL Experience Manager]提供仅用于放置的演绎版。 这些FPO呈现版本的文件大小较小，但纵横比相同。

处理配置文件可以包含FPO（仅用于放置）演绎版。 请参阅[!DNL Adobe Asset Link] [文档](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html)以了解是否需要为处理配置文件启用它。 有关详细信息，请参阅[AdobeAsset Link完整文档](https://helpx.adobe.com/cn/enterprise/using/adobe-asset-link.html)。

### 创建标准配置文件 {#create-standard-profile}

1. 管理员可访问&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 处理配置文件]**。 单击&#x200B;**[!UICONTROL 创建]**。
1. 提供一个名称，帮助您在应用到文件夹时唯一地标识配置文件。
1. 要生成FPO呈现版本，请在&#x200B;**[!UICONTROL 图像]**&#x200B;选项卡上启用&#x200B;**[!UICONTROL 创建FPO呈现版本]**。 输入1-100之间的&#x200B;**[!UICONTROL 质量]**&#x200B;值。
1. 要生成其他演绎版，请单击&#x200B;**[!UICONTROL 新增]**&#x200B;并提供以下信息：

   * 每个演绎版的文件名。
   * 每个演绎版的文件格式(PNG、JPEG、GIF或WebP)。
   * 每个演绎版的宽度和高度（以像素为单位）。 如果未指定这些值，则使用原始图像的完整像素大小。
   * 每个JPEG和WebP演绎版的质量（百分比）。
   * 包含和排除MIME类型以定义用户档案的适用性。

   ![processing-profiles-adding](assets/processing-profiles-image.png)

1. 单击&#x200B;**[!UICONTROL 保存]**。

<!-- TBD: Update the video link when a new video is available from Tech Marketing.

The following video demonstrates the usefulness and usage of standard profile.

>[!VIDEO](https://video.tv.adobe.com/v/29832?quality=9)
-->

<!-- This image was removed per cqdoc-15624, as requested by engineering.
 ![processing-profiles-list](assets/processing-profiles-list.png) 
 -->

## 自定义用户档案和用例 {#custom-config}

[!DNL Asset Compute Service]支持各种用例，包括默认处理和处理Adobe特定的格式，如Photoshop文件。 它还允许实施自定义或特定于组织的处理。 以前所需的DAM更新资产工作流自定义可自动处理，或通过处理用户档案配置的方式处理。 如果这些处理选项无法满足您的业务需求，Adobe建议开发和使用[!DNL Asset Compute Service]来扩展默认功能。 有关概述，请参阅[了解可扩展性和何时使用它](https://experienceleague.adobe.com/en/docs/asset-compute/using/extend/understand-extensibility)。

>[!NOTE]
>
>Adobe建议仅在无法使用默认配置或标准配置文件满足业务需求时才使用自定义应用程序。

它可以将图像、视频、文档和其他文件格式转换为不同的呈现形式，包括缩略图、提取的文本和元数据以及存档。

开发人员可以使用[!DNL Asset Compute Service]到[为支持的用例创建自定义应用程序](https://experienceleague.adobe.com/en/docs/asset-compute/using/extend/develop-custom-application)。 [!DNL Experience Manager]可以使用管理员配置的自定义配置文件从用户界面调用这些自定义应用程序。 [!DNL Asset Compute Service]支持以下调用外部服务的用例：

* 使用[!DNL Adobe Photoshop]的[ImageCutout API](https://developer.adobe.com/photoshop/photoshop-api-docs/)并将结果保存为演绎版。
* 调用第三方系统以进行更改，例如PIM系统。
* 使用[!DNL Photoshop] API根据Photoshop模板生成各种演绎版。
* 使用[Adobe Lightroom API](https://developer.adobe.com/photoshop/photoshop-api-docs/)优化摄取的资源并将其另存为演绎版。

>[!NOTE]
>
>无法使用自定义应用程序编辑标准元数据。 您只能修改自定义元数据。

### 创建自定义配置文件 {#create-custom-profile}

1. 管理员可访问&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 处理配置文件]** > **[!UICONTROL 创建]**。
1. 在处理配置文件页面上，单击&#x200B;**[!UICONTROL 自定义]**&#x200B;选项卡，然后单击&#x200B;**[!UICONTROL 新增]**。
1. 在“名称”文本字段中，键入所需的格式副本文件名，然后提供以下信息。

   * 每个演绎版的文件名和支持的文件扩展名。
   * App Builder自定义应用的[端点URL](https://experienceleague.adobe.com/en/docs/asset-compute/using/extend/deploy-custom-application)。 应用程序必须来自Experience Manager帐户所在的相同组织。
   * 将服务参数添加到[可将额外信息或参数传递给自定义应用程序](https://experienceleague.adobe.com/en/docs/asset-compute/using/extend/develop-custom-application#extend)。
   * 包含和排除的MIME类型可将处理限制为几种特定的文件格式。

1. 在页面的右上角附近，单击&#x200B;**[!UICONTROL 保存]**。

自定义应用程序是Headless [Project App Builder](https://developer.adobe.com/app-builder/docs/overview/)应用程序。 如果您的自定义应用程序获取所有提供的文件（如果已使用处理配置文件进行设置）。 应用程序必须筛选文件。

>[!CAUTION]
>
>如果App Builder应用程序和[!DNL Experience Manager]帐户不是来自同一组织，则集成无法正常工作。

### 自定义用户档案的示例 {#custom-profile-example}

为了说明自定义用户档案的使用情况，我们考虑一个用例，将一些自定义文本应用到Campaign图像。 您可以创建使用Photoshop API编辑图像的处理配置文件。

asset compute服务集成允许Experience Manager使用[!UICONTROL 服务参数]字段将这些参数传递到自定义应用程序。 然后，自定义应用程序调用Photoshop API并将这些值传递到API。 例如，您可以传递字体名称、文本颜色、文本粗细和文本大小，以将自定义文本添加到促销活动图像。

<!-- TBD: Check screenshot against the interface. -->

![自定义处理配置文件](assets/custom-processing-profile.png)

*图：使用[!UICONTROL 服务参数]字段将添加的信息传递到自定义应用程序中的预定义参数。 在此示例中，在上传促销活动图像时，将使用`Arial-BoldMT`字体中的`Jumanji`文本更新图像。*

## 使用处理配置文件处理资产 {#use-profiles}

创建其他自定义处理配置文件并将其应用到特定文件夹。 此工作流允许Experience Manager处理上传到这些文件夹或在这些文件夹中更新的资源。 默认的内置标准处理配置文件始终执行，但在用户界面中不可见。 如果您添加自定义配置文件，则两个配置文件都会用于处理上传的资产。

使用以下方法之一将处理配置文件应用到文件夹：

* 管理员可以在&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 处理配置文件]**&#x200B;中选择处理配置文件定义，并使用&#x200B;**[!UICONTROL 将配置文件应用到文件夹]**&#x200B;操作。 该操作将打开一个内容浏览器，允许您导航到特定文件夹并选择它们，然后确认配置文件的应用程序。
* 用户可以在Assets用户界面中选择文件夹，并使用&#x200B;**[!UICONTROL 属性]**&#x200B;操作打开文件夹属性屏幕。 在&#x200B;**[!UICONTROL 资产处理]**&#x200B;选项卡上，他们可以从[!UICONTROL 处理配置文件]列表中选择该文件夹的相应处理配置文件。 要保存更改，请单击&#x200B;**[!UICONTROL “保存并关闭”]**。
  ![从“资产属性”选项卡将处理配置文件应用到文件夹](assets/folder-properties-processing-profile.png)

* 用户可以在Assets用户界面中选择文件夹或特定资源以应用处理配置文件，然后从顶部可用的选项中选择![资源重新处理图标](assets/do-not-localize/reprocess-assets-icon.png) **[!UICONTROL 重新处理Assets]**&#x200B;选项。

>[!TIP]
>
>一个文件夹只能应用一个处理配置文件。 要生成更多演绎版，请向现有处理配置文件添加更多演绎版定义。

在处理配置文件应用于文件夹后，该文件夹或其任何子文件夹中上传（或更新）的所有新资产都将使用配置的其他处理配置文件进行处理。 这种处理是在标准默认配置文件之外进行的。

>[!NOTE]
>
>应用于文件夹的处理配置文件适用于整个树，但可以用应用于子文件夹的其他配置文件来覆盖。 将资源上传到文件夹后，Experience Manager会检查包含文件夹的属性以确定处理配置文件。 如果未应用任何配置文件，则会检查层级中的父文件夹以确定要应用的处理配置文件。

要验证是否已处理资源，请在左边栏的[!UICONTROL 呈现版本]视图中预览生成的呈现版本。 打开资源预览并打开左边栏以访问&#x200B;**[!UICONTROL 呈现版本]**&#x200B;视图。 处理配置文件中的特定演绎版（其特定资产的类型与MIME类型包含规则匹配）应当可见且可访问。

![其他节目](assets/renditions-additional-renditions.png)

*图：由应用于父文件夹的处理配置文件生成的两个其他呈现形式的示例。*

## 后处理工作流 {#post-processing-workflows}

对于需要使用处理配置文件无法实现的额外资产处理情况，可以向配置添加额外的后处理工作流。 后处理允许您在使用资产微服务的可配置处理之上添加完全自定义的处理。

在微服务处理完成后，[!DNL Experience Manager]自动运行后处理工作流，或者[自动启动工作流](https://experienceleague.adobe.com/en/docs/experience-manager-learn/assets/configuring/auto-start-workflows)（如果已配置）。 无需手动添加工作流启动器即可触发工作流。 示例包括：

* 用于处理资产的自定义工作流步骤。
* 集成以将元数据或属性从外部系统添加到资源，例如产品或流程信息。
* 其他处理由外部服务完成。

要将后处理工作流配置添加到[!DNL Experience Manager]，请执行以下步骤：

* 创建一个或多个工作流模型。 在本文档中，这些自定义模型称为&#x200B;*后处理工作流模型*。 它们是常规的[!DNL Experience Manager]工作流模型。
* 将所需的工作流步骤添加到这些模型中。 查看默认工作流的步骤，并将所有必需的默认步骤添加到自定义工作流中。 这些步骤基于工作流模型配置在资产上运行。 例如，如果您希望在上传资产时自动进行智能标记，请将步骤添加到自定义后处理工作流模型中。
* 在末尾添加[!UICONTROL DAM更新资产工作流已完成流程]步骤。 添加此步骤可确保Experience Manager知道处理何时结束，并且可以将该资源标记为已处理，即&#x200B;*New*&#x200B;显示在资源上。
* 创建自定义工作流运行器服务的配置，通过该配置，可通过路径（文件夹位置）或正则表达式配置后处理工作流模型的执行。

有关可在后处理工作流中使用的标准工作流步骤的详细信息，请参阅developer reference中的后处理工作流中的[工作流步骤](developer-reference-material-apis.md#post-processing-workflows-steps)。

### 创建后处理工作流模型 {#create-post-processing-workflow-models}

后处理工作流模型是常规的[!DNL Experience Manager]工作流模型。 如果您需要对不同的存储库位置或资源类型进行不同的处理，请创建不同的模型。

根据需要添加处理步骤。 您可以使用可用的受支持步骤以及任何自定义实施的工作流步骤。

确保每个后处理工作流的最后一步为`DAM Update Asset Workflow Completed Process`。 最后一步是确保Experience Manager在资源处理完成时进行识别。

### 配置后处理工作流执行 {#configure-post-processing-workflow-execution}

在资产微服务完成对上传资产的处理之后，您可以定义后处理工作流以进一步处理资产。 要使用工作流模型配置后处理，您可以执行以下操作之一：

* [在文件夹“属性”](#apply-workflow-model-to-folder)中应用工作流模型。
* [配置自定义工作流运行器服务](#configure-custom-workflow-runner-service)。

#### 将工作流模型应用到文件夹 {#apply-workflow-model-to-folder}

对于典型的后处理用例，考虑使用方法将工作流应用到文件夹。 要在文件夹[!UICONTROL 属性]中应用工作流模型，请执行以下步骤：

1. 创建工作流模型。
1. 选择一个文件夹，单击工具栏中的&#x200B;**[!UICONTROL 属性]**，然后单击&#x200B;**[!UICONTROL Assets处理]**&#x200B;选项卡。
1. 在&#x200B;**[!UICONTROL 自动启动工作流]**&#x200B;下，选择所需的工作流，提供工作流的标题，然后保存更改。

   ![将后处理工作流应用于其属性中的文件夹](assets/post-processing-profile-workflow-for-folders.png)

#### 配置自定义工作流运行器服务 {#configure-custom-workflow-runner-service}

您可以为高级配置配置配置自定义工作流运行器服务，这些配置无法通过将工作流应用到文件夹来轻松完成。 例如，使用正则表达式的工作流。 Adobe CQ DAM自定义工作流运行器(`com.adobe.cq.dam.processor.nui.impl.workflow.CustomDamWorkflowRunnerImpl`)是OSGi服务。 它提供了以下两个配置选项：

* 按路径(`postProcWorkflowsByPath`)后处理工作流：可以根据不同的存储库路径列出多个工作流模型。 使用冒号分隔路径和模型。 支持简单的存储库路径。 将它们映射到`/var`路径中的工作流模型。 例如：`/content/dam/my-brand:/var/workflow/models/my-workflow`。
* 按表达式(`postProcWorkflowsByExpression`)后处理工作流：可根据不同的正则表达式列出多个工作流模型。 使用冒号分隔表达式和模型。 将正则表达式直接指向资产节点，而不是某个演绎版或文件。 例如：`/content/dam(/.*/)(marketing/seasonal)(/.*):/var/workflow/models/my-workflow`。

要了解如何部署OSGi配置，请参阅[部署到 [!DNL Experience Manager]](/help/implementing/deploying/overview.md)。

#### 禁用后处理工作流执行

当不需要后期处理时，在&#x200B;**自动启动工作流**&#x200B;选择中创建并使用“空”工作流模型。

##### 创建禁用的自动启动工作流模型

1. 导航到&#x200B;**工具** > **工作流** > **模型**。
1. 从顶部操作栏中单击&#x200B;**创建** > **创建模型**。
1. 提供新工作流模型的标题和名称，例如：
   * Title：禁用自动启动工作流
   * 名称：disable-auto-start-workflow
1. 单击&#x200B;**完成**&#x200B;以创建工作流模型。
1. 选择并编辑创建的工作流模型
1. 在工作流模型编辑器中，单击模型定义中的&#x200B;**步骤1**&#x200B;并删除它。
1. 从侧面板中，单击&#x200B;**步骤**。
1. 将&#x200B;**DAM更新资产工作流已完成**&#x200B;步骤拖动到模型定义中。
1. 单击&#x200B;**页面信息**（在&#x200B;**侧面板**&#x200B;切换旁边），然后单击&#x200B;**打开属性**。
1. 在“基本”选项卡下，单击&#x200B;**临时工作流**。
1. 在顶部操作栏中，单击&#x200B;**保存并关闭**。
1. 在顶部操作栏中，单击&#x200B;**同步**。
1. 关闭工作流模型编辑器。

##### 应用禁用的自动启动工作流模型

按照[中概述的步骤将工作流模型应用到文件夹](#apply-workflow-model-to-folder)，并将&#x200B;**禁用自动启动工作流**&#x200B;设置为不需要资产后处理的文件夹的&#x200B;**自动启动工作流**。

## 最佳实践和限制 {#best-practices-limitations-tips}

* 在设计工作流时，请考虑您对所有类型的演绎版的需求。 如果您预计将来不需要节目，请从工作流中删除其创建步骤。 之后无法批量删除节目。 长时间使用[!DNL Experience Manager]后，不需要的演绎版可能会占用大量存储空间。 对于单个资源，您可以从用户界面手动删除演绎版。 对于多个资源，您可以自定义[!DNL Experience Manager]以删除特定演绎版，或删除这些资源并重新上传。
* 目前，支持仅限于生成演绎版。 不支持生成新资产。
* 目前，元数据提取的文件大小限制约为15 GB。 上传非常大的资源时，元数据提取操作有时会失败。

**另请参阅**

* [翻译资源](translate-assets.md)
* [Assets HTTP API](mac-api-assets.md)
* [资源支持的文件格式](file-format-support.md)
* [搜索资源](search-assets.md)
* [连接的资源](use-assets-across-connected-assets-instances.md)
* [资源报告](asset-reports.md)
* [元数据架构](metadata-schemas.md)
* [下载资源](download-assets-from-aem.md)
* [管理元数据](manage-metadata.md)
* [搜索 Facet](search-facets.md)
* [管理收藏集](manage-collections.md)
* [批量元数据导入](metadata-import-export.md)
* [发布资源到 AEM 和 Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)

>[!MORELIKETHIS]
>
>* [Asset compute服务简介](https://experienceleague.adobe.com/en/docs/asset-compute/using/introduction)。
>* [了解可扩展性以及何时使用它](https://experienceleague.adobe.com/en/docs/asset-compute/using/extend/understand-extensibility)。
>* [如何创建自定义应用程序](https://experienceleague.adobe.com/en/docs/asset-compute/using/extend/develop-custom-application)。
>* [各种用例支持的MIME类型](/help/assets/file-format-support.md)。

<!-- TBD: 
* How/where can admins check what's already configured and provisioned.
* How/where to request for new provisioning/purchase.
-->
