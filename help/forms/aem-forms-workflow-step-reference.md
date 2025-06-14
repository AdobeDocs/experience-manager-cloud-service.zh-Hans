---
title: 在AEM Forms Cloud Service上，哪些工作流步骤可用于创建工作流或用于业务流程自动化(BPM)？
description: 以Forms为中心的工作流允许您快速构建基于自适应Forms的工作流。 您可以使用Adobe Sign对文档进行电子签名，创建基于表单的业务流程，检索数据并将数据发送到多个数据源，以及发送电子邮件通知
exl-id: e1403ba6-8158-4961-98a4-2954b2e32e0d
google-site-verification: A1dSvxshSAiaZvk0yHu7-S3hJBb1THj0CZ2Uh8N_ck4
keywords: 使用AEM工作流，使用分配任务步骤，转换为PDF/A步骤，生成记录步骤的文档，使用工作流，签署文档步骤，生成打印输出步骤，生成非交互式PDF输出
feature: Adaptive Forms, Workflow
role: Admin, User
source-git-commit: fecbebde808c545a84889da5610a79c088f2f459
workflow-type: tm+mt
source-wordcount: '7370'
ht-degree: 0%

---


# 使用以Forms为中心的AEM Workflows — 步骤参考以自动化业务流程 {#forms-centric-workflow-on-osgi-step-reference}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/forms/workflows/aem-forms-workflow-step-reference.html?lang=zh-Hans) |
| AEM as a Cloud Service | 本文 |

您可以使用工作流模型。 模型可帮助您定义和执行一系列步骤。 您还可以定义模型属性，例如工作流是临时工作流还是使用多个资源。 您可以[在模型中包含各种AEM工作流步骤以实现业务逻辑](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html?lang=zh-Hans#extending-aem)。

## 以Forms为中心的步骤 {#forms-workflow-steps}

以Forms为中心的工作流步骤在AEM工作流中执行特定于AEM Forms的操作。 这些步骤允许您在OSGi上快速构建基于Adaptive Forms的以Forms为中心的工作流。 这些工作流可用于开发基本的审核和批准工作流、内部和跨防火墙业务流程。 您还可以使用Forms Workflow步骤执行以下操作：

* 创建业务流程、提交后工作流和后端工作流以管理注册流程。

* 创建任务并将其分配给用户或组。

* 在AEM工作流中使用[!DNL Adobe Sign]发送要签名的文档。

* 按需或提交表单时生成记录文档。

* 将工作流模型与各种数据源连接起来，以便轻松地保存和检索数据。

* 使用电子邮件步骤，在操作完成以及工作流开始或完成时发送通知电子邮件和其他附件。

>[!NOTE]
>
>如果将工作流模型标记为外部存储，则对于所有Forms Workflow步骤，您只能选择变量选项来存储或检索数据文件和附件。

## 分配任务步骤 {#assign-task-step}

分配任务步骤创建工作项并将其分配给用户或组。 在分配任务的同时，组件还为任务指定自适应表单或非交互式PDF。 从用户处接受输入需要自适应表单，非交互式PDF或只读自适应表单用于仅审阅工作流。

您还可以使用组件控制任务的行为。 例如，创建自动记录文档，将任务分配给特定用户或组，指定提交数据的路径，指定要预填充的数据路径，以及指定默认操作。 “分配任务”步骤具有以下属性：

* **[!UICONTROL 标题]**：任务的标题。 标题会显示在AEM收件箱中。
* **[!UICONTROL 描述]**：任务中正在执行的操作的说明。 当您在共享开发环境中工作时，此信息对于其他流程开发人员非常有用。

* **[!UICONTROL 缩略图路径]**：任务缩略图的路径。 如果未指定路径，则对于自适应表单，将显示默认缩略图；对于记录文档，将显示默认图标。
* **[!UICONTROL 工作流暂存]**：一个工作流可以有多个暂存。 这些阶段显示在AEM收件箱中。 您可以在模型的属性(Sidekick >页面>页面属性>阶段)中定义这些阶段。
* **[!UICONTROL 优先级]**：选定的优先级显示在AEM收件箱中。 可用的选项包括高、Medium和低。 默认值为Medium。
* **[!UICONTROL 到期日期]**：指定任务被标记为超期的天数或小时数。 如果您选择&#x200B;**[!UICONTROL 关闭]**，则不会将任务标记为过期。 您还可以指定超时处理程序，以便在任务过期后执行特定任务。

* **[!UICONTROL 天]**：任务完成的间隔天数。 将任务分配给用户后计算的天数。 如果任务未完成并超过在天数字段中指定的天数，则如果选择该任务，将在到期日期之后触发超时处理程序。
* **[!UICONTROL 小时]**：任务完成之前的小时数。 将任务分配给用户后计数小时数。 如果任务未完成并超过小时数字段中指定的小时数，则如果选择该任务，将在到期小时数后触发超时处理程序。
* **[!UICONTROL 到期日期之后超时]**：选择此选项可启用“超时处理程序”选择字段。
* **[!UICONTROL 超时处理程序]**：选择分配任务步骤超过到期日期时要执行的脚本。 放置在[apps]/fd/dashboard/scripts/timeoutHandler的CRX存储库中的脚本可供选择。 crx-repository中不存在指定的路径。 管理员在使用该路径之前先创建该路径。
* **[!UICONTROL 在任务详细信息中突出显示上一个任务的操作和注释]**：选择此选项可显示任务任务详细信息部分中执行的最后一个操作和收到的注释。
* **[!UICONTROL 类型]**：选择工作流启动时要填充的文档类型。 您可以选择自适应表单、只读自适应表单和非交互式PDF文档。

<!-- , Interactive Communication Agent UI, or Interactive Communication Web Channel Document. -->


* **[!UICONTROL 使用自适应表单]**：指定用于查找输入自适应表单的方法。 如果从“类型”下拉列表中选择“自适应表单”或“只读自适应表单”，则此选项可用。 您可以使用提交到工作流的自适应表单、在绝对路径上提供的自适应表单或变量中路径上提供的自适应表单。 您可以使用类型为“字符串”的变量来指定路径。\
  您可以将多个自适应Forms与一个工作流关联。 因此，您可以使用可用的输入方法在运行时指定自适应表单。

<!-- 

* **[!UICONTROL Use Interactive Communication]**: Specify the method to locate the input interactive communication. You can use the interactive communication submitted to the workflow, available at an absolute path, or available at a path in a variable. You can use a variable of type String to specify the path. This option is available if you select Interactive Communication Agent UI or Interactive Communication Web Channel Document from the Type drop-down list. 

> [!NOTE]
>
>You must have cm-agent-users and workflow-users group assignments to access Interactive Communications Agent UI in AEM inbox.  

-->

* **[!UICONTROL 自适应表单路径]**：指定自适应表单的路径。 您可以使用提交给工作流的自适应表单（在绝对路径上可用），或从字符串数据类型变量中存储的路径检索自适应表单。
* **[!UICONTROL 使用]**&#x200B;选择输入PDF：指定非交互式PDF文档的路径。 在类型字段中选择非交互式PDF文档时，该字段可用。 您可以使用相对于有效负荷的路径（以绝对路径保存）或使用Document数据类型的变量来选择输入PDF。 例如，[Payload_Directory]/Workflow/PDF/credit-card.pdf。 crx-repository中不存在路径。 管理员在使用该路径之前先创建该路径。 要使用“PDF路径”选项，您需要启用记录文档选项或基于表单模板的自适应Forms。
* **[!UICONTROL 对于已完成的任务，将自适应表单渲染为]**：当任务标记为完成时，可以将自适应表单渲染为只读自适应表单或PDF文档。 您需要启用记录文档选项或基于表单模板的自适应Forms才能将自适应表单渲染为记录文档。
* **[!UICONTROL 已预填充]**：下面列出的以下字段用作任务的输入：

   * **[!UICONTROL 使用]**&#x200B;选择输入数据文件：输入数据文件的路径(.json、.xml、.doc或表单数据模型(FDM))。 您可以使用相对于有效负荷的路径检索输入数据文件，或检索存储在Document、XML或JSON数据类型的变量中的文件。 例如，文件包含通过AEM收件箱应用程序为表单提交的数据。 示例路径为[Payload_Directory]/workflow/data。
   * **[!UICONTROL 使用]**&#x200B;选择输入附件：该位置可用的附件已附加到与任务关联的表单。 路径可以相对于有效负荷或检索存储在文档变量中的附件。 示例路径为[Payload_Directory]/attachments/。 您可以指定相对于有效负荷放置的附件，也可以使用文档类型（数组列表>文档）变量来指定自适应表单的输入附件。

  <!-- 
    
    * **[!UICONTROL Choose input JSON]**: Select an input JSON file using a path that is relative to payload or stored in a variable of Document, JSON, or Form Data Model (FDM) data type. This option is available if you select Interactive Communication Agent UI or Interactive Communication Web Channel Document from the Type drop-down list.

    * **[!UICONTROL Choose a custom prefill service]**: Select the prefill service to retrieve the data and prefill the Interactive Communication Web channel document or the Agent UI.  
    
    * **[!UICONTROL Use the prefill service of the interactive communication selected above]**: Use this option to use the prefill service of the Interactive Communication defined in the Use Interactive Communication drop-down list. 
    
    -->

   * **[!UICONTROL 请求属性映射]**：使用“请求属性映射”部分定义请求属性[&#128279;](work-with-form-data-model.md#bindargument)的名称和值。 根据请求中指定的属性名称和值从数据源检索详细信息。 您可以使用文本值或String数据类型的变量来定义请求属性值。

  <!--  
     
     The prefill service and request attribute mapping options are available only if you select Interactive Communication Agent UI or Interactive Communication Web Channel Document from the Type drop-down list. 
     
     -->

* **[!UICONTROL 提交的信息]**：下面列出的以下字段用作任务的输出位置：

   * **[!UICONTROL 使用]**&#x200B;保存输出数据文件：保存数据文件(.json、.xml、.doc或表单数据模型(FDM))。 数据文件包含通过关联表单提交的信息。 您可以使用相对于有效负荷的路径保存输出数据文件，或将其存储在Document、XML或JSON数据类型的变量中。 例如，[Payload_Directory]/Workflow/data，其中数据是文件。
   * **[!UICONTROL 使用]**&#x200B;保存附件：保存任务中提供的表单附件。 您可以使用相对于有效负荷的路径保存附件，或将其存储在Document数据类型的数组列表的变量中。
   * **[!UICONTROL 使用]**&#x200B;保存记录文档：保存记录文档文件的路径。 例如，[Payload_Directory]/DocumentofRecord/credit-card.pdf。 您可以使用相对于有效负荷的路径保存记录文档，或将其存储在文档数据类型的变量中。 如果选择&#x200B;**[!UICONTROL 相对于有效负载]**&#x200B;选项，如果路径字段留空，则不会生成记录文档。 仅当从“类型”下拉列表中选择“自适应表单”时，此选项才可用。

  <!-- 
    
    * **[!UICONTROL Save Web Channel data using]**: Save the Web Channel data file using a path that is relative to the payload or store it in a variable of Document, JSON, or Form Data Model (FDM) data type. This option is available only if you select Interactive Communication Agent UI from the Type drop-down list. c
    * **[!UICONTROL Save PDF document using]**: Save the PDF document using a path that is relative to the payload or store it in a variable of Document data type. This option is available only if you select Interactive Communication Agent UI from the Type drop-down list.
    <!-- * **[!UICONTROL Save layout template using]**: Save the layout template using a path that is relative to the payload or store it in a variable of Document data type. The [layout template](layout-design-details.md) refers to an XDP file that you create using Forms Designer. This option is available only if you select Interactive Communication Agent UI from the Type drop-down list. 
    
    -->

* **[!UICONTROL 代理人]** > **[!UICONTROL 分配选项]**：指定将任务分配给用户的方法。 您可以使用“参与者选择器”脚本将任务动态分配给用户或组，或者将任务分配给特定的AEM用户或组。
* **[!UICONTROL 参与者选择器]**：在“分配选项”字段中选择了&#x200B;**[!UICONTROL 动态到用户或组]**&#x200B;选项时，该选项可用。 您可以使用ECMAScript或服务来动态选择用户或组。 有关详细信息，请参阅[创建自定义Adobe Experience Manager动态参与者步骤](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=zh-Hans&CID=RedirectAEMCommunityKautuk)。

* **[!UICONTROL 参与者]**：在&#x200B;**[!UICONTROL 参与者选择器]**&#x200B;字段中选择&#x200B;**[!UICONTROL com.adobe.granite.workflow.core.process.RandomParticipantChooser]**&#x200B;选项时，该字段可用。 利用字段，可为RandomParticipantChooser选项选择用户或组。

* **[!UICONTROL 代理人]**：在&#x200B;**[!UICONTROL 参与者选择器]**&#x200B;字段中选择&#x200B;**[!UICONTROL com.adobe.fd.workspace.step.service.VariableParticipantChooser]**&#x200B;时，该字段可用。 利用字段，可选择String数据类型的变量来定义被分派人。

* **[!UICONTROL 参数]**：在“参与者选择器”字段中选择RandomParticipantChoose脚本以外的脚本时，该字段可用。 利用字段，可为“参与者选择器”字段中选择的脚本提供以逗号分隔的参数列表。

* **[!UICONTROL 用户或组]**：任务已分配给选定的用户或组。 在&#x200B;**[!UICONTROL 分配选项]**&#x200B;字段中选择&#x200B;**[!UICONTROL 到特定用户或组选项]**&#x200B;时，该选项可用。 该字段列出了[!DNL workflow-users]组的所有用户和组。\
  **[!UICONTROL 用户或组]**&#x200B;下拉菜单列出了登录用户有权访问的用户和组。 用户名显示取决于您是否对该特定用户的crx存储库中的&#x200B;**[!UICONTROL 用户]**&#x200B;节点具有访问权限。

* **[!UICONTROL 发送通知电子邮件]**：选择此选项可向被分派人发送电子邮件通知。 将任务分配给用户或组时会发送这些通知。 您可以使用&#x200B;**[!UICONTROL 收件人电子邮件地址]**&#x200B;选项指定检索电子邮件地址的机制。

* **[!UICONTROL 收件人电子邮件地址]**：您可以将电子邮件地址存储在变量中，使用文本指定永久电子邮件地址，或使用在受让人的配置文件中指定的受让人的默认电子邮件地址。 您可以使用文本或变量指定组的电子邮件地址。 变量选项有助于动态检索和使用电子邮件地址。 **[!UICONTROL 使用被分派人的默认电子邮件地址]**&#x200B;选项仅适用于单个被分派人。 在这种情况下，将使用存储在被分配人用户配置文件中的电子邮件地址。

* **[!UICONTROL HTML电子邮件模板]**：选择通知电子邮件的电子邮件模板。 要编辑模板，请在crx-repository中修改位于/libs/fd/dashboard/templates/email/htmlEmailTemplate.txt的文件。
* **[!UICONTROL 允许委派给]**： AEM收件箱为登录用户提供了一个将分配的工作流委派给其他用户的选项。 允许您在同一组内委派给另一个组的工作流用户。 如果任务被分配给单个用户，并且选择了&#x200B;**[!UICONTROL 允许委派给被分派人组]**&#x200B;的成员，则无法将任务委派给其他用户或组。
* **[!UICONTROL 共享设置]**： AEM收件箱提供了选项，用于与其他用户共享收件箱中的单个或所有任务：
   * 选择&#x200B;**[!UICONTROL 允许被分派人在收件箱]**&#x200B;中明确共享选项后，用户可以在AEM收件箱中选择该任务并将其与其他AEM用户共享。
   * 如果选择了&#x200B;**[!UICONTROL 允许被分派人通过收件箱共享进行共享]**&#x200B;选项，并且用户共享其收件箱项目或允许其他用户访问其收件箱项目时，只有之前提到的启用选项的任务才会与其他用户共享。
   * 选择&#x200B;**[!UICONTROL 允许被分派人使用“外出”设置]**&#x200B;进行委派时。 被分派人可以启用将任务委派给其他用户的选项以及其他外出选项。 任何分配给外出用户的新任务都会自动委派（分配）给外出设置中提到的用户。

  它允许其他用户在“不在办公室”且无法处理已分配任务时选择被分配人任务。

* **[!UICONTROL 操作]** > **[!UICONTROL 默认操作]**：现成可用的提交、保存和重置操作。 默认启用所有默认操作。
* **[!UICONTROL 路由变量]**：路由变量的名称。 路由变量会捕获用户在AEM收件箱中选择的自定义操作。
* **[!UICONTROL 路由]**：任务可以分支到不同的路由。 在AEM收件箱中选择后，该路由将返回一个值，并根据所选路由选择工作流分支。 您可以将路由存储在String数据类型的数组中，也可以选择&#x200B;**[!UICONTROL 文本]**&#x200B;来手动添加路由。

* **[!UICONTROL 路由标题]**：指定路由的标题。 它会显示在AEM收件箱中。
* **[!UICONTROL Coral图标]**：指定coral图标的HTML属性。 Adobe CorelUI库提供了一组大量的“触摸优先”图标。 您可以选择并使用路由的图标。 它会与标题一起显示在AEM收件箱中。 如果将路由存储在变量中，则路由会使用默认的“标记”珊瑚色图标。
* **[!UICONTROL 允许被分派人添加评论]**：选择此选项可启用该任务的评论。 被分派人可以在任务提交时从AEM收件箱中添加注释。
* **[!UICONTROL 在变量中保存注释]**：将注释保存在String数据类型的变量中。 仅当您选中&#x200B;**[!UICONTROL 允许被分派人添加评论]**&#x200B;复选框时，才会显示此选项。

* **[!UICONTROL 允许被分派人向任务添加附件]**：选择此选项可启用任务的附件。 被分派人可以在任务提交时从AEM收件箱中添加附件。 您还可以限制附件的最大大小&#x200B;**[!UICONTROL （最大文件大小）]**。 默认大小为2 MB。

* **[!UICONTROL 使用]**&#x200B;保存输出任务附件：指定附件文件夹的位置。 您可以使用相对于有效负荷的路径或在文档数据类型数组的变量中保存输出任务附件。 仅当您选中&#x200B;**[!UICONTROL 允许被分派人向任务添加附件]**&#x200B;复选框，并从&#x200B;**[!UICONTROL 表单/文档]**&#x200B;选项卡的&#x200B;**[!UICONTROL 类型]**&#x200B;下拉列表中选择&#x200B;**[!UICONTROL 自适应表单]**、**[!UICONTROL 只读自适应表单]**&#x200B;或&#x200B;**[!UICONTROL 非交互式PDF文档]**&#x200B;时，才会显示此选项。

* **[!UICONTROL 使用自定义元数据]**：选择此选项可启用自定义元数据字段。 电子邮件模板中使用自定义元数据。
* **[!UICONTROL 自定义元数据]**：为电子邮件模板选择自定义元数据。 自定义元数据位于crx-repository中的apps/fd/dashboard/scripts/metadataScripts。 crx-repository中不存在指定的路径。 管理员在使用该路径之前先创建该路径。 您还可以将服务用于自定义元数据。 您还可以扩展`WorkitemUserMetadataService`界面以提供自定义元数据。
* **[!UICONTROL 显示先前步骤的数据]**：选择此选项可让被分派人查看之前的被分派人、已对任务执行的操作、添加到任务的注释以及已完成任务的记录文档（如果可用）。
* **[!UICONTROL 显示后续步骤的数据]**：选择此选项可允许当前被分派人查看后续被分派人执行的操作和添加到任务的注释。 它还允许当前被分派人查看已完成任务的记录文档（如果可用）。
* **[!UICONTROL 数据类型的可见性]**：默认情况下，被分派人可以查看记录文档、被分派人、采取的操作以及之前和后续被分派人添加的注释。 使用“数据类型的可见性”选项限制被分派人可见的数据类型。

>[!NOTE]
>
>为外部数据存储配置AEM工作流模型时，将分配任务步骤另存为草稿和检索分配任务步骤历史记录的选项将被禁用。 此外，在收件箱中，将禁用保存选项。

## 转换为PDF/A步骤 {#convert-pdfa}

PDF/A是一种用于长期保存文档内容的存档格式，通过嵌入字体并解压缩文件来实现。 因此，PDF/A 文档通常比标准 PDF 文档大。您可以使用AEM工作流中的&#x200B;***转换为PDF/A***&#x200B;步骤将PDF文档转换为PDF/A格式。

转换为PDF/A步骤具有以下属性：

**[!UICONTROL 输入文档]**：输入文档可以相对于有效负荷，具有绝对路径，可以作为有效负荷提供，或存储在Document数据类型的变量中。

**[!UICONTROL 转换选项]**：使用此属性，指定了将PDF文档转换为PDF/A文档的设置。 此选项卡下可用的各种选项包括：
* **[!UICONTROL 符合性]**：指定输出PDF/A文档必须符合的标准。 它支持不同的PDF标准，例如PDF/A-1b、PDF/A-2b或PDF/A-3b。
* **[!UICONTROL 结果级别]**：将转换输出的结果级别指定为PassFail、Summary或Detailed。
* **[!UICONTROL 色彩空间]**：指定预定义的色彩空间，即S_RGB、COATED_FOGRA27、JAPAN_COLOR_COATED或SWOP，它们可用于输出PDF/A文件。
* **[!UICONTROL 可选内容]**：仅当满足指定的标准集时，才允许在输出PDF/A文档中显示特定图形对象和/或注释。

**[!UICONTROL 输出文档]**：指定保存输出文件的位置。 输出文件可以保存在有效负荷的相对位置，如果有效负荷是文件或是Document数据类型的变量，则覆盖有效负荷。


## 发送电子邮件步骤 {#send-email-step}

使用电子邮件步骤发送电子邮件，例如，包含记录文档、自适应表单<!-- , link of an interactive communication-->链接或附加的PDF文档的电子邮件。 发送电子邮件步骤支持[HTML电子邮件](https://en.wikipedia.org/wiki/HTML_email)。 HTML电子邮件具有响应性，可适应收件人的电子邮件客户端和屏幕大小。 您可以使用HTML电子邮件模板来定义电子邮件的外观、配色方案和行为。

电子邮件步骤使用Day CQ Mail Service发送电子邮件。 在使用电子邮件步骤之前，请确保已配置电子邮件服务。 默认情况下，电子邮件仅支持HTTP和HTTP协议。 [请与支持团队联系](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines.html?lang=zh-Hans#sending-email)以启用端口来发送电子邮件，并为您的环境启用SMTP协议。 该限制有助于提高平台的安全性。

电子邮件步骤具有以下属性：

**[!UICONTROL 标题]**：步骤的标题有助于在工作流编辑器中识别该步骤。

**[!UICONTROL 描述]**：当您在共享开发环境中工作时，说明对其他进程开发人员很有用。

**[!UICONTROL 电子邮件主题]**：可以从工作流元数据中检索主题、手动指定主题，也可以从变量中存储的值中检索主题。 从以下选项中选择：

* **[!UICONTROL 文本]**&#x200B;手动指定主题。
* **[!UICONTROL 从工作流元数据中检索]** — 从元数据属性中检索主题。
* **[!UICONTROL 变量]** — 从字符串数据类型的变量中存储的值检索主题。

**[!UICONTROL HTML电子邮件模板]**： HTML电子邮件模板。 您可以在电子邮件模板中指定变量。 电子邮件步骤可提取并显示模板中包含的所有变量以供输入。

**[!UICONTROL 电子邮件模板元数据]**：电子邮件模板变量的值可以是用户指定的值、创作或发布服务器上资源的路径、图像或工作流元数据属性。

* **[!UICONTROL 文本]**：知道要指定的确切值时使用选项。 例如，[example@example.com](mailto:example@example.com)。

* **[!UICONTROL 工作流元数据]**：在工作流元数据属性中保存要使用的值时使用选项。 选择该选项后，在工作流元数据选项下方的空文本框中输入元数据属性名称。 例如，emailAddress。

<!-- 

* **[!UICONTROL Asset URL]**: Use the option to embed a web link of an interactive communication to the email. After selecting the option, browse and choose the interactive communication to embed. The asset can reside on the author or the publish server. 

-->

* **[!UICONTROL 图像]**：使用选项将图像嵌入电子邮件。 选择该选项后，浏览并选择图像。 图像选项仅适用于电子邮件模板中可用的图像标记(&lt;img src=&quot;&#42;&quot;/>)。

**[!UICONTROL 发件人/收件人的电子邮件地址]**：选择&#x200B;**[!UICONTROL 文本]**&#x200B;选项以手动指定电子邮件地址，或选择&#x200B;**[!UICONTROL 从工作流元数据中检索]**&#x200B;选项以从元数据属性中检索电子邮件地址。 您还可以为&#x200B;**[!UICONTROL 从工作流元数据中检索]**&#x200B;选项指定元数据属性数组的列表。 选择&#x200B;**[!UICONTROL 变量]**&#x200B;选项，以从字符串数据类型的变量中存储的值检索电子邮件地址。

* **[!UICONTROL 文件附件]**：在指定位置可用的资产已附加到电子邮件。 资源的路径可以是相对于有效负荷的路径，也可以是绝对路径。 示例路径为[Payload_Directory]/attachments/。

选择&#x200B;**[!UICONTROL 变量]**&#x200B;选项以检索存储在文档、XML或JSON数据类型的变量中的文件附件。

**[!UICONTROL 文件名]**：电子邮件附件文件的名称。 电子邮件步骤将附件的原始文件名更改为指定的文件名。 可以手动指定名称，也可以从工作流元数据属性或变量中检索名称。 当您知道要指定的确切值时，请使用&#x200B;**[!UICONTROL 文本]**&#x200B;选项。 使用&#x200B;**[!UICONTROL 变量]**&#x200B;选项从字符串数据类型的变量中存储的值检索文件名。 在工作流元数据属性中保存要使用的值时，使用&#x200B;**[!UICONTROL 从工作流元数据中检索]**&#x200B;选项。

## 生成记录文档步骤 {#generate-document-of-record-step}

填写或提交表单时，您可以以打印或文档格式保留表单记录。 此记录称为记录文档(DoR)。 您可以使用“生成记录文档”步骤来创建自适应表单的只读或交互式PDF版本。 PDF版本包含填写到表单中的信息以及自适应表单的布局。

记录文档步骤具有以下属性：

**[!UICONTROL 使用自适应表单]**：指定用于查找输入自适应表单的方法。 您可以使用提交到工作流的自适应表单、在绝对路径上提供的自适应表单或变量中路径上提供的自适应表单。 可以使用String数据类型的变量在&#x200B;**[!UICONTROL 选择要解析的]**&#x200B;字段中选择路径。\
您可以将多个自适应Forms与一个工作流关联。 因此，您可以使用可用的输入方法在运行时指定自适应表单。

**[!UICONTROL 自适应表单路径]**：指定自适应表单的路径。 当您从&#x200B;**[!UICONTROL 使用自适应表单]**&#x200B;字段中选择&#x200B;**[!UICONTROL 在绝对路径上可用]**&#x200B;选项时，该字段可用。

**[!UICONTROL 使用]**&#x200B;选择输入数据：自适应表单的输入数据路径。 您可以将数据保留在相对于有效负载的位置，指定数据的绝对路径，或检索存储在Document、JSON或XML数据类型的变量中的数据。 输入数据将与自适应表单合并以创建记录文档。

**[!UICONTROL 使用]**&#x200B;选择输入附件路径：附件的路径。 这些附件包含在记录文档中。 您可以将附件保留在相对于有效负荷的位置，指定附件的绝对路径，或检索存储在Document数据类型数组中的附件。

如果指定文件夹的路径（例如，附件），则文件夹中直接可用的所有文件都将附加到记录文档。 如果任何文件在指定附件路径中直接可用的文件夹中可用，则这些文件将作为附件包含在记录文档中。 如果在直接可用的文件夹中有任何文件夹，则会跳过这些文件夹。

**[!UICONTROL 使用以下选项保存生成的记录文档]**：指定保存记录文档文件的位置。 您可以选择覆盖有效负载文件夹，将记录文档放在有效负载目录中的某个位置，或将记录文档存储在Document数据类型的变量中。

**[!UICONTROL 区域设置]**：指定记录文档的语言。 选择&#x200B;**[!UICONTROL 文本]**&#x200B;从下拉列表中选择区域设置，或者选择&#x200B;**[!UICONTROL 变量]**&#x200B;从字符串数据类型的变量中存储的值检索区域设置。 在变量中存储区域设置的值时定义区域设置代码。 例如，为英语指定&#x200B;**en_US**，为法语指定&#x200B;**fr_FR**。

## 调用DDX步骤 {#invokeddx}

文档描述XML (DDX)是一种声明性标记语言，其元素代表文档的构建块。 这些构建块包括 PDF 和 XDP 文档以及其他元素，例如注释、书签和样式文本。DDX定义了一组操作，这些操作可以应用于一个或多个输入文档，以生成一个或多个输出文档。 单个 DDX 可用于一系列源文档。您可以在AEM工作流中使用&#x200B;***调用DDX步骤***&#x200B;执行各种操作，如汇编和反汇编文档、创建和修改Acrobat和XFA Forms，以及[DDX参考文档](https://helpx.adobe.com/content/dam/help/en/experience-manager/forms-cloud-service/ddxRef.pdf)中描述的其他操作。

调用DDX步骤具有以下属性：

**[!UICONTROL 输入文档]**：用于设置输入文档的属性。 此选项卡下可用的各种选项包括：
* **[!UICONTROL 使用]**&#x200B;指定DDX：指定相对于有效负荷的输入文档、具有绝对路径、可以作为有效负荷提供，或存储在Document数据类型的变量中。
* **[!UICONTROL 从有效负荷创建映射]**：将有效负荷文件夹下的所有文档添加到输入文档的映射中，以便在Assembler中调用API。 每个文档的节点名称在映射中用作键。
* **[!UICONTROL 输入文档的映射]**：选项用于使用&#x200B;**[!UICONTROL ADD]**&#x200B;按钮添加多个条目。 每个条目表示映射中的文档键和文档的源。

**[!UICONTROL 环境选项]**：此选项用于设置调用API的处理设置。 此选项卡下可用的各种选项包括：
* **[!UICONTROL 仅验证]**：检查输入DDX文档的有效性。
* **[!UICONTROL 因错误]**&#x200B;而失败：布尔值，指示调用API服务是否失败（如果存在错误）。 默认情况下，其值设置为False。
* **[!UICONTROL First Bates编号]**：指定自动递增的编号。 此自动递增数字将自动显示在每个连续页面上。
* **[!UICONTROL 默认样式]**：设置输出文件的默认样式。

>[!NOTE]
>
>环境选项与HTTP API保持同步。

**[!UICONTROL 输出文档]**：指定保存输出文件的位置。 此选项卡下可用的各种选项包括：
* **[!UICONTROL 将输出保存在有效负荷中]**：将输出文档保存在有效负荷文件夹中，如果有效负荷是文件，则覆盖有效负荷。
* **[!UICONTROL 输出文档的映射]**：通过为每个文档添加一个条目，指定显式保存每个文档文件的位置。 每个条目表示文档以及保存文档的位置。 如果有多个输出文档，则使用此选项。

## 调用表单数据模型(FDM)服务步骤 {#invoke-form-data-model-service-step}

您可以使用[[!DNL AEM Forms] 数据集成](data-integration.md)来配置并连接到不同的数据源。 这些数据源可以是Web服务、REST服务、OData服务和CRM解决方案。 [!DNL AEM Forms]数据集成允许您创建包含各种服务的表单数据模型(FDM)，以对配置的数据库执行数据检索、添加、更新操作。 您可以使用&#x200B;**[!UICONTROL 调用数据模型服务步骤]**&#x200B;选择表单数据模型(FDM)，并使用FDM的服务检索、更新或向不同的数据源添加数据。

为说明该步骤的字段输入，使用了以下数据库表和JSON文件作为示例：

**[!UICONTROL 示例CustomerDetails表]**

<table>
 <tbody> 
  <tr> 
   <td>属性</td> 
   <td>值<br /> </td> 
  </tr> 
  <tr> 
   <td>名字<br /> </td> 
   <td>Sarah<br /> </td> 
  </tr> 
  <tr> 
   <td>姓氏</td> 
   <td>玫瑰</td> 
  </tr> 
  <tr> 
   <td>客户ID</td> 
   <td>1</td> 
  </tr> 
  <tr> 
   <td>电子邮件地址<br /> </td> 
   <td>srose@we.info</td> 
  </tr> 
 </tbody> 
</table>

**[!UICONTROL 示例JSON文件]**

```json
  { 
    customer: { 
     firstName: "Sarah", 
     lastName:"Rose", 
     customerId: "1", 
     emailAddress:"srose@we.info" 
   }, 
    insurance: {
     customerId: "1", 
    policyType: "Premium,
    policyNumber: "Premium-521499",
    customerDetails: { 
     firstName: "Sarah",
     lastName: "Rose",
     customerId: "1",
     emailAddress: "srose@we.info" 
    }
   }
  }
```

调用表单数据模型(FDM)服务步骤具有以下列出的字段，以方便表单数据模型(FDM)操作：

* **[!UICONTROL 标题]**：步骤的标题。 它有助于标识工作流编辑器中的步骤。
* **[!UICONTROL 描述]**：当您在共享开发环境中工作时，对其他进程开发人员有用的说明。

* **[!UICONTROL 表单数据模型路径]**：浏览并选择服务器上存在的表单数据模型(FDM)。

* **[!UICONTROL 错误和验证]**：选项允许您捕获错误消息，并为检索和发送到数据源的数据指定验证选项。 通过这些更改，您可以确保传递到调用表单数据模型(FDM)服务步骤的数据遵循数据源定义的数据约束。 有关详细信息，请参阅[自动验证输入数据](work-with-form-data-model.md#automated-validation-of-input-data)

* **[!UICONTROL 验证级别]**：验证分为三类： Basic、Full和OFF：

   * 完整：验证所有约束。
   * 基本：仅必需和可空的约束
   * OFF：不进行验证。

* **[!UICONTROL 失败时终止工作流]**：当约束验证失败时，工作流将停止。

* **[!UICONTROL 在变量]**&#x200B;中存储错误代码：您可以在[String类型变量](variable-in-aem-workflows.md)中存储错误代码。

* **[!UICONTROL 在变量]**&#x200B;中存储错误消息：您可以在[String类型变量](variable-in-aem-workflows.md)中存储错误消息。

* **[!UICONTROL 在变量]**&#x200B;中存储错误详细信息：您可以在[JSON类型变量](variable-in-aem-workflows.md)中存储错误详细信息。

* **[!UICONTROL 服务]**：所选表单数据模型(FDM)提供的服务列表。
* **[!UICONTROL 服务输入]** > **[!UICONTROL 使用文本值、变量或工作流元数据以及JSON文件提供输入数据]**：服务可以有多个参数。 选择选项以从工作流元数据属性、JSON对象、变量获取服务参数的值，或直接在提供的文本框中输入值：

   * **[!UICONTROL 文本]**：知道要指定的确切值时使用选项。 例如，srose@we.info。
   * **[!UICONTROL 变量]**：使用选项检索存储在变量中的值。
   * **[!UICONTROL 从工作流元数据中检索]**：在工作流元数据属性中保存要使用的值时使用选项。 例如，emailAddress。

   * **[!UICONTROL 相对于有效负载]**：使用选项检索在有效负载的相对路径中保存的文件附件。 选择选项并指定包含文件附件的文件夹名称，或在文本框中指定文件附件名称。

     例如，如果CRX存储库中的“相对于有效负荷”文件夹在`attachment\attachment-folder`位置包含文件附件，则在选择&#x200B;**[!UICONTROL 相对于有效负荷]**&#x200B;选项后，在文本框中指定`attachment\attachment-folder`。

   * **[!UICONTROL JSON点表示法]**：当要使用的值位于JSON文件中时，请使用选项。 例如，insurance.customerDetails.emailAddress。 “JSON点表示法”选项仅在从输入JSON选项中选择了映射输入字段时可用。
   * **[!UICONTROL 映射来自输入JSON的输入字段]**：指定JSON文件的路径，以从JSON文件中获取某些服务参数的输入值。 JSON文件的路径可以是相对于有效负载的相对路径，也可以是绝对路径，您也可以使用JSON或表单数据模型(FDM)类型的变量选择输入JSON文档。

* **[!UICONTROL 服务输入]** > **[!UICONTROL 使用变量或JSON文件提供输入数据]**：选择相应选项，以从在绝对路径、有效负荷的相对路径或变量中保存的JSON文件中获取所有参数的值。
* **[!UICONTROL 使用以下方式选择输入JSON文档]**：包含所有服务参数值的JSON文件。 JSON文件的路径可以是有效负载&#x200B;**的相对路径**&#x200B;或&#x200B;**[!UICONTROL 绝对路径]**。 您还可以使用JSON或表单数据模型(FDM)数据类型的变量检索输入JSON文档。

* **[!UICONTROL JSON点表示法]**：将该字段留空可使用指定JSON文件的所有对象作为服务参数的输入。 要从指定的JSON文件中读取特定JSON对象作为服务参数的输入，请为JSON对象指定点表示法，例如，如果您的JSON与部分开头列出的类似，请指定insurance.customerDetails以提供客户的所有详细信息作为服务的输入。
* **[!UICONTROL 服务输出]** > **[!UICONTROL 将输出值映射并写入变量或元数据]**：选择选项以将输出值保存为crx-repository中工作流实例元数据节点的属性。 指定元数据属性的名称，然后选择要与元数据属性映射的相应服务输出属性，例如，将输出服务返回的phone_number映射到工作流元数据的phone_number属性。 同样，可以将输出存储在Long数据类型的变量中。 为&#x200B;**[!UICONTROL 要映射的服务输出属性]**&#x200B;选项选择属性时，**[!UICONTROL 将输出保存到]**&#x200B;选项仅填充能够存储所选属性数据的变量。

* **[!UICONTROL 服务的输出]** > **[!UICONTROL 将输出保存到变量或JSON文件]**：选择相应选项以将输出值保存在JSON文件中的绝对路径、有效负荷的相对路径或变量中。
* **[!UICONTROL 使用以下选项保存输出JSON文档]**：保存输出JSON文件。 输出JSON文件的路径可以是相对于有效负载的相对路径，也可以是绝对路径。 还可使用JSON或表单数据模型(FDM)数据类型的变量保存输出JSON文件。



## 签名文档步骤 {#sign-document-step}

“签署文档”步骤允许您使用[!DNL Adobe Sign]签署文档。 在使用[!DNL Adobe Sign]工作流步骤对自适应表单进行签名时，可以将表单逐个传送给收件人，也可以将表单同时发送给所有收件人，具体取决于工作流步骤的配置。 仅在所有收件人完成签名过程后，才会将启用[!DNL Adobe Sign]的Adaptive Forms提交到Experience Manager Forms Server。

默认情况下，[!DNL Adobe Sign]计划程序服务每24小时检查（轮询）一次收件人响应。 您可以[更改环境的默认间隔](adobe-sign-integration-adaptive-forms.md#for-aem-workflows-only-configure-dnl-adobe-acrobat-sign-scheduler-to-sync-the-signing-status-configure-adobe-sign-scheduler-to-sync-the-signing-status)。

“签署文档”步骤具有以下属性：

* **[!UICONTROL 协议名称]**：指定协议的标题。 协议名称将成为发送给签名者的电子邮件的主题和正文的一部分。 您可以将该名称存储在String数据类型的变量中，也可以选择&#x200B;**[!UICONTROL 文本]**&#x200B;手动添加该名称。

* **[!UICONTROL 区域设置]**：指定电子邮件和验证选项的语言。 您可以将区域设置存储在String数据类型的变量中，也可以选择&#x200B;**[!UICONTROL 文本]**&#x200B;从可用选项列表中选择区域设置。 在变量中存储区域设置的值时，必须定义区域设置代码。 例如，为英语指定&#x200B;**[!UICONTROL en_US]**，为法语指定&#x200B;**[!UICONTROL fr_FR]**。

* **[!UICONTROL Adobe Sign云配置]**：选择[!DNL Adobe Sign]云配置。 如果您尚未为[!DNL AEM Forms]配置[!DNL Adobe Sign]，请参阅[将Adobe Sign与 [!DNL AEM Forms]](adobe-sign-integration-adaptive-forms.md)集成。

* **[!UICONTROL 使用选择要签名的文档]**：您可以从有效负荷的相对位置选择文档，使用有效负荷作为文档，指定文档的绝对路径，或检索存储在Document数据类型变量中的文档。
* 截止日期&#x200B;**[!UICONTROL 天]**：在截止日期&#x200B;**[!UICONTROL 天]**&#x200B;字段中指定的天数内任务没有活动后，文档被标记为到期（已超过截止日期）。 在将文档分配给用户进行签名后，计算天数。
* **[!UICONTROL 提醒电子邮件频率]**：您可以按每日或每周间隔发送提醒电子邮件。 从文档分配给用户进行签名的当天开始计算周数。
* **[!UICONTROL 签名流程]**：您可以选择按顺序或并行顺序对文档进行签名。 按顺序依次依次接收文档，以供签名者每次签名。 在第一签名者完成文档签名后，文档被发送给第二签名者，依此类推。 多个签名者可以同时以并行顺序对文档进行签名。
* **[!UICONTROL 重定向URL]**：指定重定向URL。 在签署文档后，您可以将受分派人重定向到URL。 通常，此URL包含感谢消息或进一步说明。
* **[!UICONTROL 工作流暂存]**：一个工作流可以有多个暂存。 这些阶段显示在AEM收件箱中。 您可以在模型的属性(**[!UICONTROL Sidekick]** > **[!UICONTROL 页面]** > **[!UICONTROL 页面属性]** > **[!UICONTROL 阶段]**)中定义这些阶段。
* **[!UICONTROL 选择收件人]**：指定选择文档收件人的方法。 您可以动态地将工作流分配给用户或组，或手动添加收件人的详细信息。 在下拉列表中选择手动后，您会添加收件人详细信息，例如电子邮件、角色和身份验证方法。

  >[!NOTE]
  >
  >* 在“角色”部分，您可以将收件人角色指定为签名者、批准者、接受者、已认证收件人、表单填写者和委托人。
  >* 如果在“角色”选项中选择“委托人”，则委托人可以将该签名任务分配给其他收件人。
  >* 如果已为[!DNL Adobe Sign]配置了身份验证方法，则根据您的配置，请选择身份验证方法，例如基于电话的身份验证、基于社交身份的身份验证、基于知识的身份验证、基于政府身份的身份验证。

* **[!UICONTROL 用于选择收件人的脚本或服务]**：仅当您在“选择收件人”字段中选择“动态”选项时，该选项才可用。 您可以指定ECMAScript或服务来选择文档的签名者和验证选项。
* **[!UICONTROL 收件人详细信息]**：只有在“选择收件人”字段中选择了“手动”选项时，该选项才可用。 指定电子邮件地址并选择可选的验证机制。 在选择两步验证机制之前，请确保为配置的[!DNL Adobe Sign]帐户启用相应的验证选项。 您可以使用String数据类型的变量来定义电子邮件、国家/地区代码和电话号码字段的值。 仅当您从两步验证下拉列表中选择“电话验证”时，才会显示“国家/地区代码”和“电话号码”字段。
* **[!UICONTROL 已签署文档]**：您可以将已签署文档的状态保存到变量。 要为已签署文档添加电子签名审核跟踪，以提高安全性和合法性，您可以包括审核报表。 您可以使用变量或有效负荷文件夹保存签名文档。

  >[!NOTE]
  >
  > 审计报告将附加到已签署文档的最后一页。

<!--
## Document Services steps {#document-services-steps}

AEM Document services are a set of services for creating, assembling, and securing PDF Documents. [!DNL AEM Forms] provides a separate AEM Workflow step for each document service.

Similar to other [!DNL AEM Forms] workflow steps, such as Assign Task, Send Email, and Sign Document, you can use variables in all AEM Document services steps. For more information on creating and managing variables, see [Variables in AEM workflows](variable-in-aem-workflows.md).
 
### Apply Document Time Stamp step {#apply-document-time-stamp-step}

Add time stamp to a document. You provide document details such as input document path, input document name, location to store exported data. You may choose to overwrite existing payload file, choose a different file name to store data in a different file under payload folder, provide an absolute path to the data, or store data in a variable of Document data type.

### Convert to image step {#convert-to-image-step}

Converts a PDF document to list of images. Supported image formats are JPEG, JPEG2000, PNG, and TIFF. The following information applies to conversions to TIFF images:

* A multi-page TIFF file is generated.
* Some annotations are not included in TIFF images. Annotations that require Acrobat to generate their appearance are not included.

### Convert to PDF/A step {#convert-to-pdf-a-step}

Converts a PDF document to PDF/A format using the options provided. The PDF/A version of Portable Document Format (PDF) is specialized for archiving and long-term preservation of documents.

### Convert to PS step {#convert-to-ps-step}

Convert PDF documents to PostScript. When converting to PostScript, you can use the conversion operation to specify the source document and whether to convert to PostScript level 2 or 3. The PDF document you convert to a PostScript file must be non-interactive.

### Create PDF from specified type step {#create-pdf-from-specified-type-step}

Generate a PDF document from an input file. The input document can be relative to the payload, have an absolute path, can be payload itself, or stored in a variable of Document data type.

### Create PDF from URL/HTML/ZIP step {#create-pdf-from-url-html-zip-step}

Generates a PDF document from supplied URL, HTML, and ZIP file.

### Export Data step {#export-data-step}

Exports data from a PDF forms or XDP file. It requires you to enter the file path of Input Document and the Export Data Format. The options for Export Data Format are Auto, XDP and XmlData.

### Export PDF to specified type step {#export-pdf-to-specified-type-step}

Converts a PDF document to a selected format.

### Generate Non-Interactive PDF step {#generatenoninteractive}

Generate a Non-Interactive PDF. It provides various customization options.

>[!NOTE]
>
>You can use variables to specify the template file for input documents. Store the path of the template file in a variable of String data type.

### Import Data step {#import-data-step}

Merges form data into a PDF form. You can import form data into a PDF form.

### Invoke DDX step {#invokeddx}

Executes the DDX file on the specified map of input documents and returns the manipulated PDF documents.

>[!NOTE]
>
>You can use variables to specify the DDX file for input documents. Store the DDX file in a variable of Document or XML data type.

### Optimize PDF step {#optimize-pdf-step}

Optimizes PDF files by reducing their size. The result of this conversion is PDF files that may be smaller than their original versions. This operation also converts PDF documents to the PDF version specified in the optimization parameters.

Optimization settings specify how files are optimized. Here are example settings:

* Target PDF version
* Discarding objects such as JavaScript actions and embedded page thumbnails
* Discarding user data such as comments and file attachments
* Discarding invalid or unused settings
* Compressing uncompressed data or using more efficient compression algorithms
* Removing embedded fonts
* Setting transparency values

### Render PDF Form step {#renderpdf}

Renders a form created in Form Designer (XDP) to a PDF form.

>[!NOTE]
>
>You can use variables to specify the template file for input documents. Store the path of the template file in a variable of String data type.

### Secure Document step {#secure-document-step}

Encrypt, Sign, and certify a document. [!DNL AEM Forms] supports both password based and certificate base encryption. You can also choose between various algorithms for signing documents. For example, SHA-256 and SH-512. You can also use the workflow step to reader extend PDF documents. The workflow step provides option to enable barcode decoding, digital signatures, import and export of PDF data, and other options.

### Send to Printer step {#send-to-printer-step}

Send a document directly to a printer. It supports the following printing access mechanisms:

* **[!UICONTROL Direct accessible printer]**: A printer that is installed on the same computer is called a direct accessible printer, and the computer is named printer host. This type of printer can be a local printer that is connected to the computer directly.
* **[!UICONTROL Indirect accessible printer]**: The printer that is installed on a print server is accessed from other computers. Technologies such as the common UNIX&reg; printing system (CUPS) and the Line Printer Daemon (LPD) protocol are available to connect to a network printer. To access an indirect accessible printer, specify the print server's IP or host name. Using this mechanism, you can send a document to an LPD URI when the network has an LPD running. The mechanism lets you route the document to any printer that is connected to the network that has an LPD running.
    -->

## 生成打印的输出步骤 {#generatePrintedOutput}

该步骤会生成给定表单设计和数据文件的PCL、PostScript、ZPL、IPL、TPCL或DPL输出。 数据文件将与窗体设计合并并设置格式以供打印。 此步骤生成的输出可以直接发送到打印机或另存为文件。 当您想要使用表单设计或应用程序中的数据时，建议您使用此步骤。 如果您的表单设计位于网络、本地文件系统或HTTP位置，请使用generatePrintedOutput操作。

例如，您的应用程序要求您将表单设计与数据文件合并。 数据包含数百条记录。 此外，它要求将输出发送到支持ZPL的打印机。 表单设计和您的输入数据都在应用程序中。 使用generatePrintedOutput操作将每个记录与表单设计合并，并将输出发送到支持ZPL的打印机。

“生成打印输出”步骤具有以下属性：

**[!UICONTROL 输入属性]**

* **[!UICONTROL 使用]**&#x200B;选择模板文件：指定模板文件的路径。 您可以使用相对于有效负荷的路径、以绝对路径保存或者使用Document数据类型的变量来选择模板文件。 例如，[Payload_Directory]/Workflow/data.xml。 如果crx-repository中不存在该路径，则管理员可以在使用该路径之前创建该路径。 此外，您还可以接受有效负荷作为输入数据文件。

* **[!UICONTROL 使用以下方式选择数据文档]**：指定输入数据文件的路径。 您可以使用相对于有效负荷的路径（以绝对路径保存）或使用Document数据类型的变量来选择输入数据文件。 例如，[Payload_Directory]/Workflow/data.xml。 如果crx-repository中不存在该路径，则管理员可以在使用该路径之前创建该路径。

* **[!UICONTROL 打印机格式]**：指定在未提供XDC文件时用于生成输出流的页面描述语言的打印格式值。 如果提供文本值，请选择以下值之一：

   * **[!UICONTROL 颜色PCL]**：使用选项为PCL指定XDC文件。
   * **[!UICONTROL 通用PostScript]**：使用选项为PostScript指定通用XDC文件。
   * **[!UICONTROL ZPL 300 DPI]**：使用ZPL 300 DPI。 使用zpl300.xdc。
   * **[!UICONTROL ZPL 600 DPI]**：使用ZPL 600 DPI。 使用zpl600.xdc文件。
   * **[!UICONTROL IPL 300 DPI]**：使用IPL 300 DPI。 使用ipl300.xdc。
   * **[!UICONTROL IPL 400 DPI]**：使用IPL 400 DPI。 使用ipl400.xdc文件。
   * **[!UICONTROL TPCL 600 DPI]**：使用TPCL 600 DPI。 使用tpcl600.xdc文件。
   * **[!UICONTROL PostScript Plain]**：使用选项为PostScript指定纯文本XDC文件。
   * **[!UICONTROL DPL300DPI]**：使用DPL 300 DPI。 使用dpl300.xdc。
   * **[!UICONTROL DPL400DPI]**：使用DPL 400 DPI。 使用dpl400.xdc。
   * **[!UICONTROL DPL600DPI]**：使用DPL 600 DPI。 使用dpl600.xdc。
   * **[!UICONTROL HP_PCL_5e]**：使用选项支持多个Canon设备。


**[!UICONTROL 输出属性]**

* **[!UICONTROL 使用]**&#x200B;保存输出文档：指定保存输出文件的位置。 可将输出文件保存在相对于有效负荷的位置、变量中，或指定绝对位置以保存输出文件。 如果crx-repository中不存在该路径，则管理员可以在使用该路径之前创建该路径。

**[!UICONTROL 高级属性]**

* **[!UICONTROL 使用以下方式选择内容根位置]**：内容根是一个字符串值，它指定存储库中的URI、绝对引用或位置以检索表单设计使用的相对资源。 例如，如果窗体设计相对引用了一个图像，如`../myImage.gif`，`myImage.gif`必须位于`repository://`。 默认值为`repository://`，它指向存储库的根级别。

  从应用程序中选择资源时，内容根URI路径必须具有正确的结构。 例如，如果从名为SampleApp的应用程序中挑选了一个表单，并将其放置在`SampleApp/1.0/forms/Test.xdp`上，则内容根URI必须指定为`repository://administrator@password/Applications/SampleApp/1.0/forms/`或`repository:/Applications/SampleApp/1.0/forms/`（当授权为null时）。 以这种方式指定内容根URI时，表单中所有引用资源的路径都将针对此URI解析。

* **[!UICONTROL 使用]**&#x200B;选择XCI文件： XCI文件用于描述用于窗体设计元素的字体和其他属性。 您可以将XCI文件相对于有效负荷保留在绝对路径上，或者使用Document数据类型的变量。

* **[!UICONTROL 区域设置]**：指定用于生成PDF文档的语言。 如果提供文本值，请从列表中选择一种语言或选择以下值之一：
   * **[!UICONTROL 要使用服务器默认值]**：
（默认）使用[!DNL AEM Forms]服务器上配置的区域设置。 “区域设置”设置是使用“管理控制台”配置的。 (请参阅[Designer帮助](https://helpx.adobe.com/cn/content/dam/help/en/experience-manager/6-5/forms/pdf/using-designer.pdf)。)

   * **[!UICONTROL 要使用自定义值]**：
在文本框中键入区域设置代码，或选择包含区域设置代码的字符串变量。 有关支持的区域设置代码的完整列表，请参阅https://docs.oracle.com/javase/1.5.0/docs/guide/intl/locale.doc.html。

* **[!UICONTROL 副本]**：一个整数值，它指定要为输出生成的副本数。 默认值为 1。

* **[!UICONTROL 双面打印]**：指定使用双面打印还是单面打印的“分页”值。 支持PostScript和PCL的打印机使用此值。 如果提供文本值，请选择以下值之一：
   * **[!UICONTROL 双面长Edge]**：使用双面打印并使用长边分页进行打印。
   * **[!UICONTROL 双面短Edge]**：使用双面打印并使用短边分页进行打印。
   * **[!UICONTROL 单面]**：使用单面打印。

## 生成非交互式PDF输出步骤   {#generatePDFdocuments}

1. 在Sidekick中，将生成非交互式PDF输出工作流拖动到Forms Workflow选项卡下。
1. 双击添加的工作流步骤以编辑组件。
1. 在“编辑组件”对话框中，配置输入文档、输出文档和其他参数，然后单击&#x200B;**[!UICONTROL 确定]**。

### 输入文档 {#input-documents-3}

* **模板文件**：指定XDP模板的位置。 它是必填字段。

* **数据文档**：指定必须与模板合并的数据xml的位置。

### 输出文档 {#output-document}

**输出文档**：指定生成的PDF表单的名称。

### 其他参数 {#additional-parameters-1}

* **内容根**：指定存储输入XDP模板中使用的片段或图像的存储库中的文件夹的路径。
* **区域设置**：指定生成的PDF表单的默认区域设置。
* **Acrobat版本**：为生成的PDF表单指定目标Acrobat版本。
* **线性化PDF**：指定是否优化生成的PDF以进行Web查看。
* **标记的PDF**：指定是否使生成的PDF可访问。
* **XCI文档**：指定XCI文件的路径。

## 另请参阅 {#see-also}

* [以Forms为中心的AEM工作流中的变量](/help/forms/variable-in-aem-workflows.md)
* [配置外出设置](/help/forms/configure-out-of-office-settings.md)

<!--

>[!MORELIKETHIS]
>
>* [Forms-centric workflow on OSGi](/help/forms/aem-forms-workflow.md)
>* [Use AEM translation workflow to localize Adaptive Forms and Document of Record](/help/forms/using-aem-translation-workflow-to-localize-adaptive-forms.md)

-->