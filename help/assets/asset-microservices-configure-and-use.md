---
title: 配置和使用资产微服务进行资产处理
description: 了解如何配置和使用云本机资产微服务大规模处理资产。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 45810a3bc5bb333b03d63d56e170388f0a1c082e

---


# 开始使用资产微服务 {#get-started-using-asset-microservices}

<!--

* Current capabilities of asset microservices offered. If workers have names then list the names and give a one-liner description. (The feature-set is limited for now and continues to grow. So will this article continue to be updated.)
* How to access the microservices. UI. API. Is extending possible right now?
* Detailed list of what file formats and what processing is supported by which workflows/workers process.
* How/where can admins check what's already configured and provisioned.
* How to create new config or request for new provisioning/purchase.

* [DO NOT COVER?] Exceptions or limitations or link back to lack of parity with AEM 6.5.

-->

资产微型服务使用云服务提供可伸缩的、具有弹性的资产处理，这些服务由Adobe管理，以优化处理不同的资产类型和处理选项。

资产处理是根据处理配置文件中的配 **[!UICONTROL 置进行的]**，处理配置文件提供了默认设置，并允许管理员添加更具体的资产处理配置。 为了实现可扩展性和完全自定义，资产处理允许对后处理工作流进行可选配置，然后由管理员创建和维护这些工作流。

以下为Experience Manager中的云服务资产处理流程概述。

<!-- Proposed DRAFT diagram for asset microservices flow - see section "asset-microservices-flow.png (asset-microservices-configure-and-use.md)" in the PPTX deck

https://adobe-my.sharepoint.com/personal/gklebus_adobe_com/_layouts/15/guestaccess.aspx?guestaccesstoken=jexDC5ZnepXSt6dTPciH66TzckS1BPEfdaZuSgHugL8%3D&docid=2_1ec37f0bd4cc74354b4f481cd420e07fc&rev=1&e=CdgElS
-->

![资产微服务流](assets/asset-microservices-flow.png)

>[!NOTE]
>
> 对于从Experience Manager的先前版本更新的客户——本节中介绍的资产处理将替换以前用于资产获取处理的“DAM更新资产”工作流模型。 大多数标准再现生成和元数据相关步骤都由资产Microservices处理取代，其余步骤（如果有）可由后处理工作流配置替换。

## 资产处理入门 {#get-started}

资产微服务的资产处理已通过默认配置预配置，从而确保系统所需的默认演绎版可用。 它还可以确保元数据提取和文本提取操作可用。 用户可以立即开始上传或更新资产，并且基本处理在默认情况下可用。

对于特定的再现生成或资产处理要求，AEM管理员可以创建其他处理配 [!UICONTROL 置文件]。 用户可以将一个或多个可用配置文件分配到特定文件夹，以完成其他处理。 例如，生成Web、移动和平板电脑特定的再现。 以下视频说明了如何创建和应用处理配 [!UICONTROL 置文件] ，以及如何访问创建的再现。

>[!VIDEO](https://video.tv.adobe.com/v/29832?quality=9)

要更改现有配置文件，请参 [阅资产Microsoft服务的配置](#configure-asset-microservices)。
要创建特定于您的自定义要求的自定义处理配置文件，例如与其他系统集成，请参 [阅后期处理工作流](#post-processing-workflows)。

## 资产微服务配置 {#configure-asset-microservices}

要配置资产微型服务，管理员可以在工具>资产>处理配 **[!UICONTROL 置文件下使用配置用户界面]**。

### 默认配置 {#default-config}

使用默认配置时，只配置标准处理配置文件。 标准处理配置文件在用户界面上不可见，您无法对其进行修改。 它始终执行以处理上传的资产。 标准处理配置文件可确保Experience Manager所需的所有基本处理均已完成。

<!-- ![processing-profiles-standard](assets/processing-profiles-standard.png) -->

标准处理配置文件提供以下处理配置：

* 资产用户界面使用的标准缩略图（48、140和319像素）
* 大预览（Web再现- 1280 px）
* 元数据提取
* 文本提取

### 支持的文件格式 {#supported-file-formats}

Asset Microservices在生成演绎版或提取元数据的能力方面支持各种文件格式。 有关 [完整列表](file-format-support.md) ，请参阅支持的文件格式。

### 添加其他处理配置文件 {#processing-profiles}

使用“创建”(Create **[!UICONTROL )操作可以添加其他处理配]** 置文件。

每个处理配置文件配置都包括一个演绎版列表。 对于每个再现，您可以指定以下内容：

* 演绎名
* 再现格式（支持JPEG、PNG或GIF）
* 再现宽度和高度（以像素为单位）（如果未指定，则假定原始图像的完全像素大小）
* 以百分比表示的再现质量（对于JPEG）
* 包含和排除的MIME类型定义了处理配置文件应用于的资产类型

![处理配置文件——添加](assets/processing-profiles-adding.png)

保存新的处理配置文件后，该配置文件会添加到已配置的处理配置文件列表中。 然后，这些处理配置文件可以应用到文件夹层次结构中的文件夹，以使它们对上传资产和在此处完成的资产有效。

![processing-profiles-list](assets/processing-profiles-list.png)

#### 再现宽度和高度 {#rendition-width-height}

演绎版宽度和高度规范提供了生成的输出图像的最大大小。 Asset Microservice会尝试生成最大可能的再现，其宽度和高度分别不大于指定的宽度和高度。 将保留宽高比，即与原始图像相同。

空值表示资产处理采用原始图像的像素尺寸。

#### MIME类型包含规则 {#mime-type-inclusion-rules}

处理具有特定MIME类型的资产时，首先会针对演绎版规范的已排除MIME类型值检查MIME类型。 如果它与该列表匹配，则不会为资产生成此特定再现（“黑名单”）。

否则，将针对包含的MIME类型检查MIME类型，如果该类型与列表匹配，则会生成演绎版（“白名单”）。

#### 特殊FPO再现 {#special-fpo-rendition}

将AEM中的大型资产放入Adobe InDesign文档时，创意专业人士在放置资产后必须等待很 [长时间](https://helpx.adobe.com/indesign/using/placing-graphics.html)。 同时，用户无法使用InDesign。 这会中断创作流程，并对用户体验造成负面影响。 Adobe允许将小型再现临时置入InDesign文档中，以后可以用全分辨率资产按需替换。 Experience Manager提供仅用于放置(FPO)的再现。 这些FPO再现的文件大小较小，但长宽比相同。

处理配置文件可以包括FPO（仅用于放置）再现。 请参阅Adobe Asset Link [文档](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html) ，了解您是否需要为处理配置文件打开它。 有关详细信息，请参 [阅Adobe Asset Link完整文档](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html)。

## 使用资产微服务处理资产 {#use-asset-microservices}

为Experience Manager创建附加的自定义处理配置文件并将其应用到特定文件夹，以便处理上传到这些文件夹或更新到这些文件夹的资产。 默认的内置标准处理配置文件始终执行，但在用户界面上不可见。 如果您添加自定义配置文件，则这两个配置文件将用于处理上传的资产。

有两种方法可将处理配置文件应用到文件夹：

* 管理员可以在工具>资产>处理配置 **[!UICONTROL 文件中选择处理配置文件定义]**，然后使用 **[!UICONTROL 将配置文件应用到文件夹操作]** 。 它会打开一个内容浏览器，允许您导航到特定文件夹，选择这些文件夹并确认配置文件的应用程序。
* 用户可以在 Assets 用户界面中选择文件夹，使用&#x200B;**[!UICONTROL 属性]**&#x200B;操作打开文件夹属性屏幕，单击&#x200B;**[!UICONTROL 处理配置文件]**&#x200B;选项卡，然后在下拉菜单中，选择该文件夹的正确处理配置文件。在“保存并关闭”操作 **[!UICONTROL 后，将保存选择]** 。

>[!NOTE]
>
>只能将一个处理配置文件应用到特定文件夹。 如果需要生成更多再现，则可以向处理配置文件中添加更多再现定义。

在将处理配置文件应用到文件夹后，此文件夹或其任何子文件夹中上传（或更新）的所有新资产都将使用配置的其他处理配置文件进行处理。 此附加处理是在标准默认配置文件之外进行的。 如果您将多个配置文件应用到一个文件夹，则系统会使用每个配置文件处理上传或更新的资产。

>[!NOTE]
>
>将资产上传到文件夹后，Experience Manager会检查包含文件夹的属性以查找处理配置文件。 如果未应用任何配置文件，则会在文件夹树中向上移动，直到找到已应用的处理配置文件并将其用于资产。 这意味着应用于文件夹的处理配置文件适用于整个树，但可能与应用于子文件夹的其他配置文件重叠。

用户可以通过打开处理已完成的新上传资产、打开资产预览并单击左边栏的演绎版视图来检查处理是否实际 **[!UICONTROL 进行]** 。 处理配置文件中特定的演绎版（其特定资产的类型与MIME类型包含规则匹配）应可见且可访问。

![附加再现](assets/renditions-additional-renditions.png)*图：由应用于父文件夹的处理配置文件生成的两个其他演绎版示例*

## 后处理工作流程 {#post-processing-workflows}

对于需要使用处理配置文件无法完成的额外资产处理的情况，可以向配置添加其他后期处理工作流。 这允许在使用资产微服务的可配置处理的基础上添加完全自定义的处理。

后期处理工作流（如果已配置）由AEM在Microservices处理完成后自动执行。 无需手动添加工作流启动器来触发它们。

示例包括：

* 用于处理资产的自定义工作流步骤，例如，使用Java代码从专有文件格式生成演绎版。
* 集成，将元数据或属性从外部系统添加到资产，例如产品或流程信息。
* 外部服务完成的附加处理

将后处理工作流配置添加到Experience Manager由以下步骤组成：

* 创建一个或多个工作流模型。 我们将它们称为“后处理工作流模型”，但它们是常规AEM工作流模型。
* 向这些模型添加特定的工作流步骤。 这些步骤将基于工作流模型配置对资产执行。
* 这种模型的最后一步必须是这 `DAM Update Asset Workflow Completed Process` 一步。 这是确保AEM知道处理已结束且资产可以标记为已处理（“新”）所必需的
* 为自定义工作流运行器服务创建配置，该配置允许按路径（文件夹位置）或正则表达式配置后处理工作流模型的执行

### 创建后处理工作流模型 {#create-post-processing-workflow-models}

后处理工作流模型是常规的AEM工作流模型。 如果您需要对不同存储库位置或资产类型进行不同的处理，请创建不同的模型。

应根据需要添加处理步骤。 您可以使用任何支持的步骤以及任何自定义实现的工作流步骤。

确保每个后处理工作流程的最后一步是 `DAM Update Asset Workflow Completed Process`。 最后一步有助于确保Experience Manager了解资产处理何时完成。

### 配置后处理工作流执行 {#configure-post-processing-workflow-execution}

要配置在资产微型服务处理完成后为系统中上传或更新的资产执行的后处理工作流模型，需要配置自定义工作流运行器服务。

自定义工作流运行器服`com.adobe.cq.dam.processor.nui.impl.workflow.CustomDamWorkflowRunnerImpl`务()是OSGi服务，它提供两个配置选项：

* 按路径(`postProcWorkflowsByPath`)的后处理工作流：可以根据不同的存储库路径列出多个工作流模型。 路径和模型应以冒号分隔。 支持简单的存储库路径，并且应该映射到路径中的工作流 `/var` 模型。 For example: `/content/dam/my-brand:/var/workflow/models/my-workflow`.
* 按表达式列出的后处理工作流(`postProcWorkflowsByExpression`):可以根据不同的正则表达式列出多个工作流模型。 表达式和模型应用冒号分隔。 正则表达式应直接指向“资产”节点，而不是指向某个演绎版或文件。 For example: `/content/dam(/.*/)(marketing/seasonal)(/.*):/var/workflow/models/my-workflow`.

>[!NOTE]
>
>自定义工作流运行器的配置是OSGi服务的配置。 有关 [如何部署OSGi配置的信息，请参阅部署到Experience Manager](/help/implementing/deploying/overview.md) 。
> 与AEM的内部部署和托管服务部署不同，OSGi Web控制台不直接在云服务部署中可用。

有关在后处理工作流中可以使用哪个标准工作流步骤的详细信息，请参阅开发 [人员参考中的后处理工作流中的工作流步骤](developer-reference-material-apis.md#post-processing-workflows-steps) 。
