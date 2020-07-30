---
title: 配置和使用资产微服务进行资产处理
description: 了解如何配置和使用云本机资产微服务大规模处理资产。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 253231d2c9bafbba72696db36e9ed46b8011c9b3
workflow-type: tm+mt
source-wordcount: '2246'
ht-degree: 1%

---


# 使用资产微服务和处理用户档案 {#get-started-using-asset-microservices}

<!--
* Current capabilities of asset microservices offered. If workers have names then list the names and give a one-liner description. (The feature-set is limited for now and continues to grow. So will this article continue to be updated.)
* How to access the microservices. UI. API. Is extending possible right now?
* Detailed list of what file formats and what processing is supported by which workflows/workers process.
* How/where can admins check what's already configured and provisioned.
* How to create new config or request for new provisioning/purchase.

* [DO NOT COVER?] Exceptions or limitations or link back to lack of parity with AEM 6.5.
-->

资产微型服务为使用云服务的资产提供可扩展且具有弹性的处理。 Adobe管理服务以优化处理不同的资产类型和处理选项。

资产处理取决于处理用户档案 **[!UICONTROL 中的配置]**，该配置提供了默认设置，并允许管理员添加更具体的资产处理配置。 管理员可以创建和维护后处理工作流的配置，包括可选自定义。 自定义工作流允许可扩展性和完全自定义。

Asset microservices允许您处 [理各种文件类型](/help/assets/file-format-support.md) ，这些类型的现成格式比先前版本的Experience Manager所能处理的格式更多。 例如，PSD和PSB格式的缩览图提取现在可能是之前需要的第三方解决方案，如ImageMagick。

<!-- Proposed DRAFT diagram for asset microservices flow - see section "asset-microservices-flow.png (asset-microservices-configure-and-use.md)" in the PPTX deck

https://adobe-my.sharepoint.com/personal/gklebus_adobe_com/_layouts/15/guestaccess.aspx?guestaccesstoken=jexDC5ZnepXSt6dTPciH66TzckS1BPEfdaZuSgHugL8%3D&docid=2_1ec37f0bd4cc74354b4f481cd420e07fc&rev=1&e=CdgElS
-->

![资产处理的高级视图](assets/asset-microservices-flow.png "资产处理的高级视图")

>[!NOTE]
>
>此处介绍的资产处理将替 `DAM Update Asset` 换先前版本中存在的工作流模型 [!DNL Experience Manager]。 大多数标准演绎版生成和元数据相关步骤都由资产microservices处理取代，其余步骤（如果有）可由后处理工作流配置替换。

## 了解资产处理选项 {#get-started}

Experience Manager允许以下级别的处理。

| 配置 | 描述 | 涵盖的使用案例 |
|---|---|---|
| [默认配置](#default-config) | 它按原样可用，无法修改。 此配置提供了非常基本的再现生成功能。 | 用户界面使 [!DNL Assets] 用的标准缩略图（48、140和319 px）; 大预览（Web再现- 1280 px）; 元数据和文本提取。 |
| [标准配置](#standard-config) | 仅由管理员通过用户界面进行配置。 提供的再现生成选项比上述默认配置更多。 | 更改图像的格式和分辨率； 生成FPO再现。 |
| [自定义配置](#custom-config) | 由管理员通过用户界面进行配置，以调用支持更复杂要求的自定义Worker。 利用云本机 [!DNL Asset Compute Service]。 | 请参阅 [允许的使用案例](#custom-config)。 |

要创建特定于您的自定义要求的自定义处理用户档案，例如与其他系统集成，请参 [阅后处理工作流](#post-processing-workflows)。

## 支持的文件格式 {#supported-file-formats}

Asset microservices在生成演绎版或提取元数据方面支持各种文件格式。 有关 [完整列表](file-format-support.md) ，请参阅支持的文件格式。

## 默认配置 {#default-config}

已预配置一些默认设置，以确保Experience Manager中所需的默认演绎版可用。 默认配置还确保元数据提取和文本提取操作可用。 用户可以立即开始上传或更新资产，并且基本处理默认可用。

使用默认配置，只配置最基本的处理用户档案。 此类处理用户档案在用户界面上不可见，您无法修改它。 它始终执行以处理上传的资产。 此默认处理用户档案可确保对所有资产完成所 [!DNL Experience Manager] 需的基本处理。

<!-- ![processing-profiles-standard](assets/processing-profiles-standard.png)
-->

## 标准用户档案 {#standard-config}

[!DNL Experience Manager] 根据用户的需要，提供为通用格式生成更多特定再现的功能。 管理员可以创建其 [!UICONTROL 他处理用户档案] ，以便创建此类再现。 然后，用户将一个或多个可用用户档案分配给特定文件夹以完成附加处理。 例如，附加处理可以为Web、移动设备和平板电脑生成再现。 以下视频说明了如何创建和应用处 [!UICONTROL 理用户档案] ，以及如何访问创建的演绎版。

* **演绎版宽度和高度**: 演绎版宽度和高度规范提供了生成的输出图像的最大大小。 资产微型服务会尝试生成最大可能的再现，其宽度和高度分别不大于指定的宽度和高度。 将保留宽高比，即与原始宽高比相同。 空值表示资产处理采用原始图像的像素尺寸。

* **MIME类型包含规则**: 当处理具有特定MIME类型的资产时，会首先根据演绎版规范的已排除MIME类型值检查MIME类型。 如果它与该列表匹配，则不会为资产(阻止列表)生成此特定再现。 否则，将根据包含的MIME类型检查MIME类型，如果它与列表匹配，则会生成演绎版(允许列表)。

* **特殊FPO再现**: 当将大型资产从文档 [!DNL Experience Manager] 置入 [!DNL Adobe InDesign] 时，创意专业人士在置入资产后会等 [待相当长时间](https://helpx.adobe.com/indesign/using/placing-graphics.html)。 同时，用户被阻止使用 [!DNL InDesign]。 这会中断创意流程，并对用户体验造成负面影响。 Adobe允许将小型演绎版临时放 [!DNL InDesign] 置到文档中，以后可以用全分辨率资产按需替换。 [!DNL Experience Manager] 提供仅用于放置(FPO)的再现。 这些FPO再现文件大小较小，但长宽比相同。

处理用户档案可以包括FPO（仅用于放置）再现。 查看 [!DNL Adobe Asset Link] 文 [档](https://helpx.adobe.com/cn/enterprise/using/manage-assets-using-adobe-asset-link.html) ，了解您是否需要为处理用户档案打开它。 有关详细信息，请参阅 [Adobe资产链接完整文档](https://helpx.adobe.com/cn/enterprise/using/adobe-asset-link.html)。

### 创建标准用户档案 {#create-standard-profile}

要创建标准处理用户档案，请执行以下步骤：

1. 管理员访 **[!UICONTROL 问工具]** >资 **[!UICONTROL 产]** >处 **[!UICONTROL 理用户档案]**。 单击&#x200B;**[!UICONTROL 创建]**。
1. 提供一个名称，帮助您在应用到文件夹时唯一标识用户档案。
1. 要生成FPO演绎版，请在“标 **[!UICONTROL 准]** ”选项卡上 **[!UICONTROL 启用创建FPO演绎版]**。 输入一个 **[!UICONTROL 介于]** 1和100之间的“质量”值。
1. 要生成其他演绎版，请单 **[!UICONTROL 击“添加新]** ”并提供以下信息：

   * 每个再现的文件名。
   * 每个再现的文件格式（PNG、JPEG或GIF）。
   * 每个演绎版的宽度和高度（以像素为单位）。 如果未指定这些值，则使用原始图像的完整像素大小。
   * 质量（以每个JPEG再现的百分比表示）。
   * 包含和排除的MIME类型，用于定义用户档案的适用性。

![处理用户档案-添加](assets/processing-profiles-adding.png)

1. 单击&#x200B;**[!UICONTROL 保存]**。

以下视频演示了标准用户档案的有用性和用法。

>[!VIDEO](https://video.tv.adobe.com/v/29832?quality=9)

<!-- Removed per cqdoc-15624 request by engineering.
 ![processing-profiles-list](assets/processing-profiles-list.png) 
 -->

## 自定义用户档案和用例 {#custom-config}

**待定项目**:

* 与可扩展性内容的整体交叉链接。
* 提及如何获取工作人员的URL。 开发、舞台和产品环境的工作URL。
* 提及服务参数的映射。 指向计算服务文章的链接。
* 从Jira票证中共享的流透视进行审阅。

由于组织的需求各不相同，因此无法使用默认配置完成某些复杂的资产处理用例。 Adobe [!DNL Asset Compute Service] 优惠。 它是一种可扩展的可扩展服务，用于处理数字资产。 它可以将图像、视频、文档和其他文件格式转换为不同的再现，包括缩略图、提取的文本和元数据以及存档。

开发人员可以使用资产计算服务来创建专门的自定义工作程序，它们适合预定义、复杂的用例。 [!DNL Experience Manager] 可以使用管理员配置的自定义用户档案从用户界面调用这些自定义Worker。 [!DNL Asset Compute Service] 支持以下用例：

* 使用Adobe Sensei为数字资产生成自定义增强的智能标签。
* 使用Adobe Sensei生成主题的裁剪面具。
* 从PIM系统检索产品元数据信息，并在获取资产期间将元数据部分用于资产的二进制。
* 使用API更改透明图像的背景 [!DNL Adobe Photoshop] 颜色。
* 使用API润饰 [!DNL Photoshop] 图像。
* 使用API拉直 [!DNL Adobe Lightroom] 图像。

>[!NOTE]
>
>不能使用自定义Worker编辑标准元数据。 您只能修改自定义元数据。

### 创建自定义用户档案 {#create-custom-profile}

要创建自定义用户档案，请执行以下步骤：

1. 管理员可 **[!UICONTROL 以访问工具>资产>处理用户档案]**。 单击&#x200B;**[!UICONTROL 创建]**。
1. Click on **[!UICONTROL Custom]** tab. 单击 **[!UICONTROL 添加新]**。 提供再现所需的文件名。
1. 提供以下信息，然后单击“ **[!UICONTROL 保存]**”。

   * 每个再现的文件名和支持的文件扩展名。
   * Firefly自定义应用程序的端点URL。 应用程序必须与Experience Manager帐户来自同一组织。
   * 根据需要添加服务参数。
   * 包含和排除的MIME类型，用于定义用户档案的适用性。

![自定义处理用户档案](assets/custom-processing-profile.png)

>[!CAUTION]
>
>如果Firefly应用程序 [!DNL Experience Manager] 和帐户不来自同一组织，则集成将不起作用。

## 使用处理用户档案处理资产 {#use-profiles}

创建附加的自定义处理用户档案并将其应用到特定文件夹，以便Experience Manager处理上传到这些文件夹或在这些文件夹中更新的资产。 默认的内置标准处理用户档案始终执行，但在用户界面上不可见。 如果您添加自定义用户档案，则两个用户档案均用于处理上传的资产。

使用以下方法之一将处理用户档案应用到文件夹：

* 管理员可以在工具>资产>处 **[!UICONTROL 理用户档案中选择处理用户档案定义]**，然后使 **[!UICONTROL 用将用户档案应用到文件夹操作]** 。 它会打开一个内容浏览器，允许您导航到特定文件夹，选择这些文件夹并确认该用户档案的应用程序。
* Users can select a folder in the Assets user interface, use **[!UICONTROL Properties]** action to open folder properties screen, click on the **[!UICONTROL Processing Profiles]** tab, and in the popup list, select the correct processing profile for that folder. 要保存更改，请单击“保 **[!UICONTROL 存并关闭”]**。

>[!NOTE]
>
>只能将一个处理用户档案应用于特定文件夹。 要生成更多再现，请向现有处理用户档案添加更多再现定义。

在将处理用户档案应用到文件夹后，会使用配置的附加处理用户档案处理此文件夹或其任何子文件夹中上传（或更新）的所有新资产。 此处理是在标准默认用户档案之外添加的。 如果您对一个文件夹应用多个用户档案，则系统会使用其中每个用户档案处理已上传或更新的资产。

>[!NOTE]
>
>应用于文件夹的处理用户档案适用于整个树，但可能与应用于子文件夹的其他用户档案重叠。 资产上传到文件夹后，Experience Manager会检查包含文件夹的属性以查找处理用户档案。 如果未应用任何文件夹，则会检查层次结构中的父文件夹以查找要应用的处理用户档案。

用户可以通过打开处理已完成的新上传资产、打开资产预览并单击左边栏的演绎版视图，检查处理是否实际 **[!UICONTROL 进行]** 。 处理用户档案中的特定演绎版（其特定资产的类型与MIME类型包含规则匹配）应可见且可访问。

![其他演绎版](assets/renditions-additional-renditions.png)

*图： 由应用于父文件夹的处理用户档案生成的两个其他演绎版的示例。*

## 后处理工作流 {#post-processing-workflows}

在需要对无法使用处理用户档案进行的资产进行额外处理的情况下，可以向配置中添加其他后处理工作流。 这允许在使用资产微服务的可配置处理的基础上添加完全自定义的处理。

后处理工作流（如果配置）由AEM在微服务处理完成后自动执行。 无需手动添加工作流启动器来触发它们。 示例包括：

* 处理资产的自定义工作流步骤。
* 集成功能，可将元数据或属性从外部系统添加到资产，例如产品或流程信息。
* 外部服务完成的附加处理。

将后处理工作流配置添加到Experience Manager包含以下步骤：

* 创建一个或多个工作流模型。 文档将其称为后 *处理工作流模型*，但这些是常规Experience Manager工作流模型。
* 为这些模型添加特定的工作流步骤。 这些步骤将基于工作流模型配置对资产执行。
* 在最 [!UICONTROL 后添加DAM更新资产工作流完成] 的流程步骤。 添加此步骤可确保Experience Manager知道处理何时结束，并且资产可以标记为已处理，即 *新* （在资产上显示）。
* 为自定义工作流运行服务创建配置，允许通过路径（文件夹位置）或常规表达式配置后处理工作流模型的执行。

### 创建后处理工作流模型 {#create-post-processing-workflow-models}

后处理工作流模型是常规的AEM工作流模型。 如果您需要针对不同的存储库位置或资产类型进行不同的处理，请创建不同的模型。

应根据需要添加处理步骤。 您可以使用任何支持的步骤以及任何自定义实现的工作流步骤。

确保每个后处理工作流的最后一步是 `DAM Update Asset Workflow Completed Process`。 最后一步有助于确保Experience Manager知道资产处理何时完成。

### 配置后处理工作流执行 {#configure-post-processing-workflow-execution}

要配置在资产微型服务处理完成后，为系统中上传或更新的资产执行后处理工作流模型，需要配置自定义工作流运行器服务。

自定义工作流运行`com.adobe.cq.dam.processor.nui.impl.workflow.CustomDamWorkflowRunnerImpl`器服务()是OSGi服务，提供两个配置选项：

* 按路径()分类的后处理工作流`postProcWorkflowsByPath`: 可以根据不同的存储库路径列出多个工作流模型。 路径和模型应以冒号分隔。 支持简单的存储库路径，并应映射到路径中的工作流 `/var` 模型。 For example: `/content/dam/my-brand:/var/workflow/models/my-workflow`.
* 后处理工作流(按表达式`postProcWorkflowsByExpression`): 可以根据不同的常规表达式列出多个工作流模型。 表达式和模型应用冒号分隔。 常规表达式应直接指向“资产”节点，而不是指向某个演绎版或文件。 For example: `/content/dam(/.*/)(marketing/seasonal)(/.*):/var/workflow/models/my-workflow`.

>[!NOTE]
>
>自定义工作流运行器的配置是OSGi服务的配置。 有 [关如何部署OSGi配置](/help/implementing/deploying/overview.md) ，请参阅部署到Experience Manager。
>与AEM的内部部署和托管服务部署不同，OSGi Web控制台在云服务部署中不直接可用。

有关在后处理工作流中可以使用哪个标准工作流步骤的详细信息，请参 [阅开发人员参考中的后处理工作流中](developer-reference-material-apis.md#post-processing-workflows-steps) 的工作流步骤。

## 最佳实践和限制 {#best-practices-limitations-tips}

* 设计工作流时，请考虑您对所有类型再现的需求。 如果您不认为将来需要再现，请从工作流中删除其创建步骤。 之后无法批量删除演绎版。 长期使用后，不需要的再现可能占用大量存储空间 [!DNL Experience Manager]。 对于单个资产，您可以从用户界面手动删除演绎版。 对于多个资产，您可以自定 [!DNL Experience Manager] 义删除特定演绎版，也可以删除资产，然后再次上传这些资产。
