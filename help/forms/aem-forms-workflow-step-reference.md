---
title: 如何将工作流分配给其他用户、发送电子邮件、在工作流中使用Adobe Sign？
description: 以Forms为中心的工作流允许您快速构建基于Forms的自适应工作流。 您可以使用Adobe Sign对文档进行电子签名、创建基于表单的业务流程、检索数据并将数据发送到多个数据源以及发送电子邮件通知
exl-id: e1403ba6-8158-4961-98a4-2954b2e32e0d
google-site-verification: A1dSvxshSAiaZvk0yHu7-S3hJBb1THj0CZ2Uh8N_ck4
source-git-commit: 3c8035e4db5729f58bae29136a32a0b9944d6a2f
workflow-type: tm+mt
source-wordcount: '7190'
ht-degree: 1%

---

# 以Forms为中心的AEM工作流 — 步骤参考 {#forms-centric-workflow-on-osgi-step-reference}

您可以使用工作流模型将业务逻辑转换为自动重复流程。 模型可帮助您定义和执行一系列步骤。 您还可以定义模型属性，例如工作流是瞬态的还是使用多个资源。 您可以 [在模型中包括各种AEM Workflow步骤以实现业务逻辑](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html?lang=en#extending-aem).

## 以Forms为中心的步骤 {#forms-workflow-steps}

以Forms为中心的工作流步骤在AEM Workflow中执行特定于AEM Forms的操作。 这些步骤允许您在OSGi上快速构建基于Adaptive Forms的以Forms为中心的工作流。 这些工作流可用于开发基本的审核和批准工作流、内部和跨防火墙业务流程。 您还可以使用Forms Workflow步骤执行以下操作：

* 创建业务流程、提交后工作流和后端工作流以管理注册流程。

* 创建任务并将其分配给用户或组。

* 使用 [!DNL Adobe Sign] 在AEM Workflow中发送要签名的文档。

* 按需或提交表单时生成记录文档。

* 将工作流模型与各种数据源连接起来，以便轻松保存和检索数据。

* 使用电子邮件步骤可在操作完成以及工作流开始或完成时发送通知电子邮件和其他附件。

>[!NOTE]
>
>如果将工作流模型标记为外部存储，则对于所有Forms工作流步骤，您只能选择变量选项来存储或检索数据文件和附件。


## 分配任务步骤 {#assign-task-step}

分配任务步骤创建一个工作项并将其分配给用户或组。 在分配任务的同时，组件还会为任务指定自适应表单或非交互式PDF。 自适应表单需要接受来自用户的输入且非交互式PDF，或只读自适应表单用于仅审阅工作流。

您还可以使用组件控制任务的行为。 例如，创建自动记录文档，将任务分配给特定用户或组，指定提交数据的路径，指定要预填充的数据路径，以及指定默认操作。 “分配任务”步骤具有以下属性：

* **[!UICONTROL 标题]**：任务的标题。 标题显示在AEM收件箱中。
* **[!UICONTROL 描述]**：任务中执行的操作说明。 当您在共享开发环境中工作时，此信息对于其他流程开发人员非常有用。

* **[!UICONTROL 缩略图路径]**：任务缩略图的路径。 如果未指定路径，则会为自适应表单显示默认缩略图，为记录文档显示默认图标。
* **[!UICONTROL 工作流暂存]**：一个工作流可以有多个阶段。 这些阶段显示在AEM收件箱中。 您可以在模型的属性（Sidekick >页面>页面属性>阶段）中定义这些阶段。
* **[!UICONTROL 优先级]**：选定的优先级显示在AEM收件箱中。 可用的选项包括“高”、“中”和“低”。 默认值为Medium。
* **[!UICONTROL 到期日期]**：指定任务被标记为超期的天数或小时数。 如果您选择 **[!UICONTROL 关闭]**，则任务永远不会标记为过期。 您还可以指定超时处理程序，以便在任务过期后执行特定任务。

* **[!UICONTROL 天]**：任务完成的间隔天数。 将任务分配给用户后计算天数。 如果任务未完成，并且超过了“天数”字段中指定的天数，则在选中时，将在到期日期之后触发超时处理程序。
* **[!UICONTROL 小时]**：完成任务之前的小时数。 将任务分配给用户后计算小时数。 如果任务未完成并超过小时数字段中指定的小时数，则在选择时，将在到期小时数后触发超时处理程序。
* **[!UICONTROL 到期日期后超时]**：选择此选项可启用超时处理程序选择字段。
* **[!UICONTROL 超时处理程序]**：选择分配任务步骤超过到期日期时要执行的脚本。 放置在CRX存储库中的脚本 [应用程序]/fd/dashboard/scripts/timeoutHandler可供选择。 crx-repository中不存在指定的路径。 管理员在使用路径之前创建该路径。
* **[!UICONTROL 在任务详细信息中突出显示上一个任务的操作和注释]**：选择此选项可显示任务的“任务详细信息”部分中执行的上一个操作以及收到的评论。
* **[!UICONTROL 类型]**：选择工作流启动时要填写的文档类型。 您可以选择自适应表单、只读自适应表单和非交互式PDF文档。

<!-- , Interactive Communication Agent UI, or Interactive Communication Web Channel Document. -->


* **[!UICONTROL 使用自适应表单]**：指定定位输入自适应表单的方法。 如果从“类型”下拉列表中选择“自适应表单”或“只读自适应表单”，则此选项可用。 您可以使用提交到工作流的自适应表单、在绝对路径上提供的自适应表单或变量中路径上提供的自适应表单。 您可以使用字符串类型的变量来指定路径。\
   您可以将多个自适应Forms与一个工作流关联。 因此，您可以使用可用的输入方法在运行时指定自适应表单。

<!-- 

* **[!UICONTROL Use Interactive Communication]**: Specify the method to locate the input interactive communication. You can use the interactive communication submitted to the workflow, available at an absolute path, or available at a path in a variable. You can use a variable of type String to specify the path. This option is available if you select Interactive Communication Agent UI or Interactive Communication Web Channel Document from the Type drop-down list. 

> [!NOTE]
>
>You must have cm-agent-users and workflow-users group assignments to access Interactive Communications Agent UI in AEM inbox.  

-->

* **[!UICONTROL 自适应表单路径]**：指定自适应表单的路径。 您可以使用提交给工作流的自适应表单（在绝对路径上可用），也可以从字符串数据类型变量中存储的路径检索自适应表单。
* **[!UICONTROL 使用以下方式选择输入PDF]**：指定非交互式PDF文档的路径。 在“类型”字段中选择非交互式PDF时，该字段可用。 您可以使用相对于有效负荷的路径（以绝对路径保存）或使用Document数据类型的变量来选择输入PDF。 例如， [Payload_Directory]/Workflow/PDF/credit-card.pdf. crx-repository中不存在该路径。 管理员在使用路径之前创建该路径。 要使用“PDF路径”选项，您需要启用记录文档选项或基于表单模板的自适应Forms。
* **[!UICONTROL 对于已完成的任务，将自适应表单渲染为]**：将任务标记为完成时，您可以将自适应表单渲染为只读自适应表单或PDF文档。 您需要启用记录文档选项或基于表单模板的自适应Forms才能将自适应表单渲染为记录文档。
* **[!UICONTROL 预填充]**：下面列出的以下字段用作任务的输入：

   * **[!UICONTROL 使用以下方式选择输入数据文件]**：输入数据文件（.json、.xml、.doc或表单数据模型）的路径。 您可以使用相对于有效负荷的路径检索输入数据文件，或检索存储在Document、XML或JSON数据类型的变量中的文件。 例如，文件包含通过AEM收件箱应用程序为表单提交的数据。 示例路径为 [Payload_Directory]/workflow/data.
   * **[!UICONTROL 使用以下方式选择输入附件]**：该位置可用的附件会附加到与任务关联的表单。 路径可以相对于有效负荷，也可以检索存储在文档变量中的附件。 示例路径为 [Payload_Directory]/attachments/. 您可以指定相对于有效负荷放置的附件，也可以使用文档类型（“数组列表”>“文档”）变量来指定自适应表单的输入附件。

   <!-- 
    
    * **[!UICONTROL Choose input JSON]**: Select an input JSON file using a path that is relative to payload or stored in a variable of Document, JSON, or Form Data Model data type. This option is available if you select Interactive Communication Agent UI or Interactive Communication Web Channel Document from the Type drop-down list.

    * **[!UICONTROL Choose a custom prefill service]**: Select the prefill service to retrieve the data and prefill the Interactive Communication Web channel document or the Agent UI.  
    
    * **[!UICONTROL Use the prefill service of the interactive communication selected above]**: Use this option to use the prefill service of the Interactive Communication defined in the Use Interactive Communication drop-down list. 
    
    -->

   * **[!UICONTROL 请求属性映射]**：使用“请求属性映射”部分定义 [请求属性的名称和值](work-with-form-data-model.md#bindargument). 根据请求中指定的属性名称和值从数据源检索详细信息。 您可以使用文本值或String数据类型的变量来定义请求属性值。

   <!--  
     
     The prefill service and request attribute mapping options are available only if you select Interactive Communication Agent UI or Interactive Communication Web Channel Document from the Type drop-down list. 
     
     -->

* **[!UICONTROL 提交的信息]**：下面列出的以下字段用作任务的输出位置：

   * **[!UICONTROL 保存输出数据文件，使用]**：保存数据文件（.json、.xml、.doc或表单数据模型）。 数据文件包含通过关联表单提交的信息。 您可以使用相对于有效负载的路径保存输出数据文件，或将其存储在Document、XML或JSON数据类型的变量中。 例如， [Payload_Directory]/Workflow/data，其中数据是文件。
   * **[!UICONTROL 保存附件，使用]**：保存任务中提供的表单附件。 您可以使用相对于有效负荷的路径保存附件，或将其存储在Document数据类型的数组列表的变量中。
   * **[!UICONTROL 保存记录文档，使用]**：保存记录文档文件的路径。 例如， [Payload_Directory]/DocumentofRecord/credit-card.pdf. 您可以使用相对于有效负荷的路径保存记录文档，或将其存储到文档数据类型的变量中。 如果您选择 **[!UICONTROL 相对于有效负荷]** 选项，如果路径字段留空，则不生成记录文档。 仅当从“类型”下拉列表中选择“自适应表单”时，此选项才可用。

   <!-- 
    
    * **[!UICONTROL Save Web Channel data using]**: Save the Web Channel data file using a path that is relative to the payload or store it in a variable of Document, JSON, or Form Data Model data type. This option is available only if you select Interactive Communication Agent UI from the Type drop-down list. c
    * **[!UICONTROL Save PDF document using]**: Save the PDF document using a path that is relative to the payload or store it in a variable of Document data type. This option is available only if you select Interactive Communication Agent UI from the Type drop-down list.
    <!-- * **[!UICONTROL Save layout template using]**: Save the layout template using a path that is relative to the payload or store it in a variable of Document data type. The [layout template](layout-design-details.md) refers to an XDP file that you create using Forms Designer. This option is available only if you select Interactive Communication Agent UI from the Type drop-down list. 
    
    -->

* **[!UICONTROL 被分派人]** > **[!UICONTROL 分配选项]**：指定将任务分配给用户的方法。 您可以使用“参与者选择器”脚本将任务动态分配给用户或组，或者将任务分配给特定的AEM用户或组。
* **[!UICONTROL 参与者选择器]**：在以下情况下，该选项可用： **[!UICONTROL 动态分配给用户或组]** 选项时，该复选框才会被选中。 您可以使用ECMAScript或服务来动态选择用户或组。 有关更多信息，请参阅 [向用户动态分配工作流](https://helpx.adobe.com/experience-manager/kb/HowToAssignAWorkflowDynamicallyToParticipants.html) 和 [创建自定义Adobe Experience Manager动态参与者步骤。](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=en&amp;CID=RedirectAEMCommunityKautuk)

* **[!UICONTROL 参与者]**：在以下情况下，该字段可用： **[!UICONTROL com.adobe.granite.workflow.core.process.RandomParticipantChooser]** 选项已选中 **[!UICONTROL 参与者选择器]** 字段。 利用字段，可为RandomParticipantChooser选项选择用户或组。

* **[!UICONTROL 被分派人]**：在以下情况下，该字段可用： **[!UICONTROL com.adobe.fd.workspace.step.service.VariableParticipantChooser]** 已选中 **[!UICONTROL 参与者选择器]** 字段。 利用字段，可选择String数据类型的变量来定义被分派人。

* **[!UICONTROL 参数]**：在“参与者选择器”字段中选择RandomParticipantChoose脚本以外的脚本时，该字段可用。 利用字段，可为“参与者选择器”字段中选择的脚本提供逗号分隔参数的列表。

* **[!UICONTROL 用户或组]**：任务已分配给选定的用户或组。 当满足以下条件时，该选项可用： **[!UICONTROL 至特定用户或组选项]** 已选中 **[!UICONTROL 分配选项]** 字段。 该字段列出了 [!DNL workflow-users] 组。\
   此 **[!UICONTROL 用户或组]** 下拉菜单列出了登录用户有权访问的用户和组。 用户名显示取决于您是否拥有 **[!UICONTROL 用户]** crx-repository中用于特定用户的节点。

* **[!UICONTROL 发送通知电子邮件]**：选择此选项可向被分派人发送电子邮件通知。 当任务分配给用户或组时，将发送这些通知。 您可以使用 **[!UICONTROL 收件人电子邮件地址]** 用于指定检索电子邮件地址的机制的选项。

* **[!UICONTROL 收件人电子邮件地址]**：您可以将电子邮件地址存储在变量中，使用文本可指定永久电子邮件地址，或者使用被分配人配置文件中指定的被分配人的默认电子邮件地址。 您可以使用文本或变量指定组的电子邮件地址。 变量选项有助于动态检索和使用电子邮件地址。 此 **[!UICONTROL 使用被分派人的默认电子邮件地址]** 选项仅适用于单个被分配人。 在这种情况下，将使用存储在被分派人用户配置文件中的电子邮件地址。

* **[!UICONTROL HTML电子邮件模板]**：为通知电子邮件选择电子邮件模板。 要编辑模板，请修改位于crx-repository中/libs/fd/dashboard/templates/email/htmlEmailTemplate.txt的文件。
* **[!UICONTROL 允许委派至]**：AEM收件箱为登录用户提供了一个选项，用于将分配的工作流委派给其他用户。 允许您在同一组内委派给另一个组的工作流用户。 如果任务分配给单个用户，并且 **[!UICONTROL 允许委派给被分派人组成员]** 选项，则无法将任务委派给其他用户或组。
* **[!UICONTROL 共享设置]**：AEM收件箱提供了选项，用于与其他用户共享收件箱中的单个或所有任务：
   * 当 **[!UICONTROL 允许被分派人在收件箱中明确共享]** 选项，则用户可以在AEM收件箱中选择任务并将其与其他AEM用户共享。
   * 当 **[!UICONTROL 允许被分派人通过收件箱共享进行共享]** 选项，并且用户共享其收件箱项目或允许其他用户访问其收件箱项目，只有之前提到的启用选项的任务才会与其他用户共享。
   * 当 **[!UICONTROL 允许被分派人使用“外出”设置进行委派]** 已选中。 被分派人可以启用将任务委派给其他用户的选项以及其他外出选项。 任何分配给休假用户的新任务都会自动委派（分配）给休假设置中提到的用户。

   它允许其他用户在外出时选择被分派人任务，并且无法处理被分派的任务。

* **[!UICONTROL 操作]** > **[!UICONTROL 默认操作]**：现成可用的提交、保存和重置操作。 默认启用所有默认操作。
* **[!UICONTROL 路由变量]**：路由变量的名称。 route变量可捕获用户在AEM收件箱中选择的自定义操作。
* **[!UICONTROL 路由]**：任务可以分支到不同的路由。 在AEM收件箱中选择后，该路由会返回一个值，并根据所选路由选择工作流分支。 您可以将路由存储在String数据类型的数组变量中，也可以选择 **[!UICONTROL 文本]** 以手动添加路由。

* **[!UICONTROL 路由标题]**：指定路由的标题。 它显示在AEM收件箱中。
* **[!UICONTROL Coral图标]**：指定coral图标的HTML属性。 AdobeCorelUI库提供了一组数量庞大的“触摸优先”图标。 您可以选择并使用路由的图标。 它与AEM收件箱中的标题一起显示。 如果将路由存储在变量中，则这些路由使用默认的“标记”珊瑚图标。
* **[!UICONTROL 允许被分派人添加评论]**：选择此选项可启用任务的注释。 被分派人可以在任务提交时从AEM收件箱中添加注释。
* **[!UICONTROL 在变量中保存注释]**：将评论保存在String数据类型的变量中。 仅当您选择 **[!UICONTROL 允许被分派人添加评论]** 复选框。

* **[!UICONTROL 允许被分派人向任务添加附件]**：选择此选项可启用任务的附件。 被分派人可以在提交任务时从AEM收件箱中添加附件。 您还可以限制最大大小 **[!UICONTROL （最大文件大小）]** 附件的URL。 默认大小为2 MB。

* **[!UICONTROL 保存输出任务附件，使用]**：指定附件文件夹的位置。 可以使用相对于有效负荷的路径或在文档数据类型数组的变量中保存输出任务附件。 仅当您选择 **[!UICONTROL 允许被分派人向任务添加附件]** 复选框，然后选择 **[!UICONTROL 自适应表单]**， **[!UICONTROL 只读自适应表单]**，或 **[!UICONTROL 非交互式PDF文档]** 从 **[!UICONTROL 类型]** 中的下拉列表 **[!UICONTROL 表单/文档]** 选项卡。

* **[!UICONTROL 使用自定义元数据]**：选择此选项可启用自定义元数据字段。 自定义元数据在电子邮件模板中使用。
* **[!UICONTROL 自定义元数据]**：为电子邮件模板选择自定义元数据。 自定义元数据位于crx-repository中的apps/fd/dashboard/scripts/metadataScripts。 crx-repository中不存在指定的路径。 管理员在使用路径之前创建该路径。 您还可以将服务用于自定义元数据。 您还可以扩展 `WorkitemUserMetadataService` 用于提供自定义元数据的界面。
* **[!UICONTROL 显示之前步骤的数据]**：选择此选项可让被分派人查看以前的被分派人、已对任务执行的操作、添加到任务的注释以及已完成任务的记录文档（如果可用）。
* **[!UICONTROL 显示后续步骤的数据]**：选择此选项可允许当前被分派人查看后续被分派人执行的操作和添加到任务的注释。 它还允许当前被分派人查看已完成任务的记录文档（如果可用）。
* **[!UICONTROL 数据类型可见性]**：默认情况下，被分配人可以查看记录文档、被分配人、采取的操作以及之前和后续被分配人添加的备注。 使用“数据类型可见性”选项可限制被分配人可见的数据类型。

>[!NOTE]
>
>为外部数据存储配置AEM Workflow模型时，将分配任务步骤另存为草稿和检索分配任务步骤的历史记录的选项被禁用。 此外，在收件箱中，将禁用保存的选项。

## 转换为PDF/A步骤 {#convert-pdfa}

PDF/A是一种用于长期保存文档内容的存档格式，通过嵌入字体并解压缩文件来实现。 因此，PDF/A 文档通常比标准 PDF 文档大。您可以使用 ***转换为PDF/音频*** 在AEM Workflow中将PDF文档转换为PDF/A格式的步骤。

转换为PDF/A步骤具有以下属性：

**[!UICONTROL 输入文档]**：输入文档可以相对于有效负荷，具有绝对路径，可以作为有效负荷提供，或存储在Document数据类型的变量中。

**[!UICONTROL 转换选项]**：使用此属性可指定将PDF文档转换为PDF/A文档的设置。 此选项卡下可用的各种选项包括：
* **[!UICONTROL 合规性]**：指定输出PDF/A文档必须符合的标准。 它支持不同的PDF标准，如PDF/A-1b、PDF/A-2b或PDF/A-3b。
* **[!UICONTROL 结果级别]**：将转换输出的结果级别指定为PassFail、Summary或Detailed。
* **[!UICONTROL 色彩空间]**：将预定义的色彩空间指定为S_COLOR、COATED_FOGRA27、JAPAN_COLOR_COATED或SWOP，它们可用于输出PDF/ARGB。
* **[!UICONTROL 可选内容]**：仅当满足指定的标准集时，才允许特定图形对象和/或注释在输出PDF/A文档中可见。

**[!UICONTROL 输出文档]**：指定保存输出文件的位置。 输出文件可以保存在相对于有效负荷的位置，如果有效负荷是文件或是Document数据类型的变量，则覆盖有效负荷。


## 发送电子邮件步骤 {#send-email-step}

使用电子邮件步骤发送电子邮件，例如包含记录文档、自适应表单链接的电子邮件 <!-- , link of an interactive communication-->，或者具有附加的PDF文档。 “发送电子邮件”步骤支持 [HTML电子邮件](https://en.wikipedia.org/wiki/HTML_email). HTML电子邮件具有响应性，可适应收件人的电子邮件客户端和屏幕大小。 您可以使用HTML电子邮件模板来定义电子邮件的外观、颜色方案和行为。

电子邮件步骤使用Day CQ邮件服务发送电子邮件。 在使用电子邮件步骤之前，请确保已配置电子邮件服务。 默认情况下，电子邮件仅支持HTTP和HTTP协议。 [联系支持团队](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines.html?lang=en#sending-email) 启用发送电子邮件的端口并为环境启用SMTP协议。 该限制有助于提高平台的安全性。

电子邮件步骤具有以下属性：

**[!UICONTROL 标题]**：步骤的标题有助于在工作流编辑器中标识该步骤。

**[!UICONTROL 描述]**：当您在共享开发环境中工作时，此说明对于其他流程开发人员非常有用。

**[!UICONTROL 电子邮件主题]**：可以从工作流元数据中检索主题、手动指定主题，也可以从变量中存储的值中检索主题。 从以下选项中选择：

* **[!UICONTROL 文本]** 手动指定主题。
* **[!UICONTROL 从工作流元数据中检索]**  — 从元数据属性检索主题。
* **[!UICONTROL 变量]**  — 从字符串数据类型变量中存储的值检索主题。

**[!UICONTROL HTML电子邮件模板]**：电子邮件的HTML模板。 您可以在电子邮件模板中指定变量。 电子邮件步骤可提取并显示模板中包含的所有变量以进行输入。

**[!UICONTROL 电子邮件模板元数据]**：电子邮件模板变量的值可以是用户指定的值、创作或发布服务器上资源的路径、图像或工作流元数据属性。

* **[!UICONTROL 文本]**：当您知道要指定的确切值时，请使用选项。 例如， [example@example.com](mailto:example@example.com).

* **[!UICONTROL 工作流元数据]**：当要使用的值保存在工作流元数据属性中时，使用选项。 选择该选项后，在工作流元数据选项下方的空文本框中输入元数据属性名称。 例如，emailAddress。

<!-- 

* **[!UICONTROL Asset URL]**: Use the option to embed a web link of an interactive communication to the email. After selecting the option, browse and choose the interactive communication to embed. The asset can reside on the author or the publish server. 

-->

* **[!UICONTROL 图像]**：使用选项将图像嵌入电子邮件。 选择该选项后，浏览并选择图像。 图像选项仅适用于电子邮件模板中可用的图像标记(&lt;img src=&quot;&lt;span id=&quot; translate=&quot;no&quot; />“/>”)。&#42;

**[!UICONTROL 发件人/收件人的电子邮件地址]**：选择 **[!UICONTROL 文本]** 用于手动指定电子邮件地址或选择 **[!UICONTROL 从工作流元数据中检索]** 选项，用于从元数据属性检索电子邮件地址。 您还可以为以下项指定元数据属性数组的列表： **[!UICONTROL 从工作流元数据中检索]** 选项。 选择 **[!UICONTROL 变量]** 选项，用于从字符串数据类型变量中存储的值检索电子邮件地址。

* **[!UICONTROL 文件附件]**：在指定位置可用的资源已附加到电子邮件。 资源的路径可以是相对于有效负荷的路径，也可以是绝对路径。 示例路径为 [Payload_Directory]/attachments/.

选择 **[!UICONTROL 变量]** 用于检索存储在Document、XML或JSON数据类型的变量中的文件附件的选项。

**[!UICONTROL 文件名]**：电子邮件附件文件的名称。 电子邮件步骤会将附件的原始文件名更改为指定的文件名。 可以手动指定名称，也可以从工作流元数据属性或变量中检索名称。 使用 **[!UICONTROL 文本]** 选项。 使用 **[!UICONTROL 变量]** 选项，用于从存储在字符串数据类型变量中的值检索文件名。 使用 **[!UICONTROL 检索工作流元数据]** 选项。

## 生成记录文档步骤 {#generate-document-of-record-step}

填写或提交表单时，您可以以打印或文档格式保留表单记录。 此记录称为记录文档(DoR)。 您可以使用“生成记录文档”步骤创建自适应表单的只读或交互式PDF版本。 PDF版本包含填写到表单中的信息以及自适应表单的布局。

记录文档步骤具有以下属性：

**[!UICONTROL 使用自适应表单]**：指定定位输入自适应表单的方法。 您可以使用提交到工作流的自适应表单、在绝对路径上提供的自适应表单或变量中路径上提供的自适应表单。 您可以使用String数据类型的变量在 **[!UICONTROL 选择要解析的变量]** 字段。\
您可以将多个自适应Forms与一个工作流关联。 因此，您可以使用可用的输入方法在运行时指定自适应表单。

**[!UICONTROL 自适应表单路径]**：指定自适应表单的路径。 当您选择时，该字段可用 **[!UICONTROL 在绝对路径上可用]** 选项来自 **[!UICONTROL 使用自适应表单]** 字段。

**[!UICONTROL 使用以下方式选择输入数据]**：自适应表单的输入数据的路径。 您可以将数据保留在相对于有效负载的位置，指定数据的绝对路径，或检索存储在Document、JSON或XML数据类型的变量中的数据。 输入数据与自适应表单合并以创建记录文档。

**[!UICONTROL 使用以下方式选择输入附件路径]**：附件的路径。 这些附件包含在记录文档中。 您可以将附件保留在相对于有效负荷的位置，指定附件的绝对路径，或检索存储在“文档”数据类型数组中的附件。

如果您指定文件夹的路径（例如，附件），则文件夹中直接可用的所有文件都会附加到记录文档。 如果任何文件在指定附件路径中直接可用的文件夹中可用，则这些文件将作为附件包含在记录文档中。 如果在直接可用的文件夹中有任何文件夹，则会跳过这些文件夹。

**[!UICONTROL 使用以下选项保存生成的记录文档]**：指定保留记录文档文件的位置。 您可以选择覆盖有效负载文件夹，将记录文档放在有效负载目录中的某个位置，或将记录文档存储在Document数据类型的变量中。

**[!UICONTROL 区域设置]**：指定记录文档的语言。 选择 **[!UICONTROL 文本]** 从下拉列表中选择区域设置，或选择 **[!UICONTROL 变量]** 从字符串数据类型变量中存储的值检索区域设置。 在变量中存储区域设置的值时定义区域设置代码。 例如，指定 **en_US** （英语）和 **fr_FR** 法文版。

## 调用DDX步骤 {#invokeddx}

文档描述XML (DDX)是一种声明性标记语言，其元素代表文档的构建块。 这些构建块包括 PDF 和 XDP 文档以及其他元素，例如注释、书签和样式文本。DDX定义了一组操作，这些操作可以应用于一个或多个输入文档，以生成一个或多个输出文档。 单个 DDX 可用于一系列源文档。您可以使用 ***调用DDX步骤*** 在AEM Workflow中执行各种操作，如汇编和反汇编文档、创建和修改Acrobat和XFA Forms，以及中描述的其他操作。 [DDX参考文档](https://helpx.adobe.com/content/dam/help/en/experience-manager/forms-cloud-service/ddxRef.pdf).

调用DDX步骤具有以下属性：

**[!UICONTROL 输入文档]**：用于设置输入文档的属性。 此选项卡下可用的各种选项包括：
* **[!UICONTROL 使用以下方式指定DDX]**：指定相对于有效负荷的输入文档、具有绝对路径、可以作为有效负荷提供，或存储在Document数据类型的变量中。
* **[!UICONTROL 从有效负载创建映射]**：将有效负荷文件夹下的所有文档添加到输入文档的映射中，以供汇编程序中的调用API使用。 每个文档的节点名称在映射中用作键。
* **[!UICONTROL 输入文档的映射]**：选项用于添加多个条目，使用 **[!UICONTROL 添加]** 按钮。 每个条目表示映射中的文档键和文档的源。

**[!UICONTROL 环境选项]**：此选项用于设置调用API的处理设置。 此选项卡下可用的各种选项包括：
* **[!UICONTROL 仅验证]**：检查输入DDX文档的有效性。
* **[!UICONTROL 出错时失败]**：布尔值，指示调用API服务是否失败（如果存在错误）。 默认情况下，其值设置为False。
* **[!UICONTROL 第一个Bates编号]**：指定自动递增的数字。 此自动递增数字将自动显示在每个连续页面上。
* **[!UICONTROL 默认样式]**：设置输出文件的默认样式。

>[!NOTE]
>
>环境选项与HTTP API保持同步。

**[!UICONTROL 输出文档]**：指定保存输出文件的位置。 此选项卡下可用的各种选项包括：
* **[!UICONTROL 将输出保存在有效负荷中]**：将输出文档保存在有效负荷文件夹下，或者覆盖有效负荷，以防有效负荷是文件。
* **[!UICONTROL 输出文档的映射]**：通过为每个文档添加一个条目，指定显式保存每个文档文件的位置。 每个条目表示文档以及保存文档的位置。 如果有多个输出文档，则使用此选项。

## 调用表单数据模型服务步骤 {#invoke-form-data-model-service-step}

您可以使用 [[!DNL AEM Forms] 数据集成](data-integration.md) 配置并连接到不同的数据源。 这些数据源可以是Web服务、REST服务、OData服务和CRM解决方案。 [!DNL AEM Forms] 数据集成允许您创建包含各种服务的表单数据模型，以对配置的数据库执行数据检索、添加、更新操作。 您可以使用 **[!UICONTROL 调用数据模型服务步骤]** 以选择表单数据模型(FDM)并使用FDM的服务来检索、更新或向不同的数据源添加数据。

为了说明该步骤的字段输入，以下数据库表和JSON文件用作示例：

**[!UICONTROL 示例CustomerDetails表]**

<table>
 <tbody> 
  <tr> 
   <td>属性</td> 
   <td>价值<br /> </td> 
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

调用表单数据模型服务步骤包含以下字段，以方便表单数据模型操作：

* **[!UICONTROL 标题]**：步骤的标题。 它有助于标识工作流编辑器中的步骤。
* **[!UICONTROL 描述]**：当您在共享开发环境中工作时，此说明对于其他流程开发人员非常有用。

* **[!UICONTROL 表单数据模型路径]**：浏览并选择服务器上存在的表单数据模型。

* **[!UICONTROL 错误和验证]**：利用选项，可捕获错误消息并为检索和发送到数据源的数据指定验证选项。 通过这些更改，您可以确保传递到“调用表单数据模型服务”步骤的数据遵守数据源定义的数据约束。 有关更多详细信息，请参阅 [自动验证输入数据](work-with-form-data-model.md#automated-validation-of-input-data)

* **[!UICONTROL 验证级别]**：验证分为三类：基本、完全和关闭：

   * 完整：所有约束均已验证。
   * 基本：仅必需和可空的约束
   * OFF：不进行验证。

* **[!UICONTROL 失败时终止工作流]**：当约束验证失败时，工作流将停止。

* **[!UICONTROL 将错误代码存储在变量中]**：您可以将错误代码存储在 [字符串类型变量](variable-in-aem-workflows.md).

* **[!UICONTROL 在变量中存储错误消息]**：您可以将错误消息存储在 [字符串类型变量](variable-in-aem-workflows.md).

* **[!UICONTROL 在变量中存储错误详细信息]**：您可以将错误详细信息存储在 [JSON类型变量](variable-in-aem-workflows.md).

* **[!UICONTROL 服务]**：所选表单数据模型提供的服务的列表。
* **[!UICONTROL 服务输入]** > **[!UICONTROL 提供使用文本、变量或工作流元数据的输入数据以及JSON文件]**：一个服务可以有多个参数。 选择选项以从工作流元数据属性、JSON对象、变量获取服务参数的值，或者在提供的文本框中直接输入值：

   * **[!UICONTROL 文本]**：当您知道要指定的确切值时，请使用选项。 例如，srose@we.info。
   * **[!UICONTROL 变量]**：使用选项检索存储在变量中的值。
   * **[!UICONTROL 检索工作流元数据]**：当要使用的值保存在工作流元数据属性中时，使用选项。 例如，emailAddress。

   * **[!UICONTROL 相对于有效负荷]**：使用选项可检索保存在相对于有效负荷的路径中的文件附件。 选择选项并指定包含文件附件的文件夹名称，或在文本框中指定文件附件名称。

      例如，如果CRX存储库中的相对于有效负荷文件夹在 `attachment\attachment-folder` 位置，指定 `attachment\attachment-folder` 在文本框中，选择 **[!UICONTROL 相对于有效负荷]** 选项。

   * **[!UICONTROL JSON点表示法]**：当要使用的值位于JSON文件中时，使用选项。 例如，insurance.customerDetails.emailAddress。 “JSON点表示法”选项仅在选择了“映射来自输入JSON的输入字段”选项时可用。
   * **[!UICONTROL 从输入JSON映射输入字段]**：指定JSON文件的路径，以从JSON文件中获取某些服务参数的输入值。 JSON文件的路径可以是相对于有效负载的路径、绝对路径，也可以使用JSON或表单数据模型类型的变量选择输入JSON文档。

* **[!UICONTROL 服务输入]** > **[!UICONTROL 使用变量或JSON文件提供输入数据]**：选择相应选项，以从在绝对路径、有效负荷的相对路径或变量中保存的JSON文件中获取所有参数的值。
* **[!UICONTROL 使用以下方式选择输入JSON文档]**：包含所有服务参数的值的JSON文件。 JSON文件的路径可以是 **[!UICONTROL 相对于有效负荷]** 或 **[!UICONTROL 绝对路径]**. 您还可以使用JSON或表单数据模型数据类型的变量检索输入JSON文档。

* **[!UICONTROL JSON点表示法]**：将字段留空可使用指定JSON文件的所有对象作为服务参数的输入。 要从指定的JSON文件中读取特定的JSON对象作为服务参数的输入，请为JSON对象指定点表示法。例如，如果您的JSON与在部分开头列出的JSON相似，请指定insurance.customerDetails以提供客户的所有详细信息作为服务的输入。
* **[!UICONTROL 服务输出]** > **[!UICONTROL 将输出值映射并写入变量或元数据]**：选择选项以将输出值另存为crx-repository中工作流实例元数据节点的属性。 指定元数据属性的名称，然后选择要与元数据属性映射的相应服务输出属性，例如，将输出服务返回的phone_number映射到工作流元数据的phone_number属性。 同样，您可以将输出存储在Long数据类型的变量中。 当您为选择属性时 **[!UICONTROL 要映射的服务输出属性]** 选项，则只会为填充能够存储选定属性的数据的变量 **[!UICONTROL 将输出保存到]** 选项。

* **[!UICONTROL 服务输出]** > **[!UICONTROL 将输出保存到变量或JSON文件]**：选择相应选项以将输出值保存在JSON文件中的绝对路径、有效负荷的相对路径或变量中。
* **[!UICONTROL 使用以下选项保存输出JSON文档]**：保存输出JSON文件。 输出JSON文件的路径可以是相对于有效负载的路径，也可以是绝对路径。 您还可以使用JSON或表单数据模型数据类型的变量保存输出JSON文件。

## 签署文档步骤 {#sign-document-step}

“签署文档”步骤允许您使用 [!DNL Adobe Sign] 以签署文档。 在使用 [!DNL Adobe Sign] Workflow 步骤对自适应表单进行签名时，可以将表单逐个传送给签名者，也可以将表单同时发送给所有签名者，具体取决于工作流步骤的配置。仅在所有签名者完成签名过程后，[!DNL Adobe Sign] 支持的自适应表单才提交到 Experience Manager Forms Server。

默认情况下，[!DNL Adobe Sign] 调度程序服务每 24 小时检查（轮询）一次签名者响应。您可以 [更改环境的默认间隔](adobe-sign-integration-adaptive-forms.md##configure-adobe-sign-scheduler-to-sync-the-signing-status).

“签署文档”步骤具有以下属性：

* **[!UICONTROL 协议名称]**：指定协议的标题。 协议名称将成为发送给签名者的电子邮件的主题和正文的一部分。 您可以将名称存储在String数据类型的变量中，也可以选择 **[!UICONTROL 文本]** 以手动添加名称。

* **[!UICONTROL 区域设置]**：指定电子邮件和验证选项的语言。 您可以将区域设置存储在String数据类型的变量中，也可以选择 **[!UICONTROL 文本]** 从可用选项列表中选择区域设置。 在变量中存储区域设置的值时，必须定义区域设置代码。 例如，指定 **[!UICONTROL en_US]** （英语）和 **[!UICONTROL fr_FR]** 法文版。

* **[!UICONTROL Adobe Sign云配置]**：选择一个 [!DNL Adobe Sign] 云配置。 如果您尚未配置 [!DNL Adobe Sign] 对象 [!DNL AEM Forms]，请参见 [将Adobe Sign与集成 [!DNL AEM Forms]](adobe-sign-integration-adaptive-forms.md).

* **[!UICONTROL 使用以下方式选择待签署文档]**：您可以从相对于有效负载的位置选择文档，使用有效负载作为文档，指定文档的绝对路径，或检索存储在Document数据类型变量中的文档。
* **[!UICONTROL 到截止日期前的天数]**：当任务中没有符合中指定的天数的活动后，文档被标记为到期（已超过截止日期）。 **[!UICONTROL 到截止日期前的天数]** 字段。 在将文档分配给用户进行签名后计算天数。
* **[!UICONTROL 提醒电子邮件频率]**：您可以按每日或每周间隔发送提醒电子邮件。 从将记录的周分配给用户进行签名的当天开始计算周数。
* **[!UICONTROL 签名过程]**：您可以选择按顺序或并行顺序对文档进行签名。 按顺序排列，一个签名者一次接收文档以进行签名。 第一个签名者完成文档签名后，文档将发送给第二个签名者，依此类推。 多个签名者可以按并行顺序一次签名一个文档。
* **[!UICONTROL 重定向URL]**：指定重定向URL。 在文档签名后，您可以将被分派人重定向到URL。 通常，此URL包含感谢消息或进一步说明。
* **[!UICONTROL 工作流暂存]**：一个工作流可以有多个阶段。 这些阶段显示在AEM收件箱中。 您可以在模型的属性中定义这些阶段( **[!UICONTROL Sidekick]** > **[!UICONTROL 页面]** > **[!UICONTROL 页面属性]** > **[!UICONTROL 暂存]**)。
* **[!UICONTROL 选择签名者]**：指定选择文档签名者的方法。 您可以将工作流动态分配给用户或组，或手动添加签名者的详细信息。
* **[!UICONTROL 用于选择签名者的脚本或服务]**：仅当在选择签名者字段中选择了动态选项时，该选项才可用。 您可以指定ECMAScript或服务来选择文档的签名者和验证选项。
* **[!UICONTROL 签名者详细信息]**：仅当在选择签名者字段中选择了手动选项时，该选项才可用。 指定电子邮件地址并选择可选的验证机制。 在选择两步验证机制之前，请确保为配置的启用了相应的验证选项 [!DNL Adobe Sign] 帐户。 您可以使用String数据类型的变量来定义“电子邮件”、“国家/地区代码”和“电话号码”字段的值。 仅当您从两步验证下拉列表中选择“电话验证”时，才会显示“国家/地区代码”和“电话号码”字段。

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

该步骤会生成给定表单设计和数据文件的PCL、PostScript、ZPL、IPL、TPCL或DPL输出。 数据文件将与表单设计合并，并设置格式以进行打印。 此步骤生成的输出可以直接发送到打印机或另存为文件。 当您想要使用表单设计或来自应用程序的数据时，建议您使用此步骤。 如果您的表单设计位于网络、本地文件系统或HTTP位置，请使用generatePrintedOutput操作。

例如，您的应用程序要求您将表单设计与数据文件合并。 数据包含数百条记录。 此外，它要求将输出发送到支持ZPL的打印机。 表单设计和输入数据在应用程序中。 使用generatePrintedOutput操作将每个记录与表单设计合并，并将输出发送到支持ZPL的打印机。

“生成打印输出”步骤具有以下属性：

**[!UICONTROL 输入属性]**

* **[!UICONTROL 使用以下方式选择模板文件]**：指定模板文件的路径。 您可以使用相对于有效负荷的路径、以绝对路径保存的路径或使用Document数据类型的变量来选择模板文件。 例如， [Payload_Directory]/Workflow/data.xml. 如果crx-repository中不存在该路径，则管理员可以在使用该路径之前创建该路径。 此外，您还可以接受有效负荷作为输入数据文件。

* **[!UICONTROL 使用以下方式选择数据文档]**：指定输入数据文件的路径。 您可以使用相对于有效负荷的路径（保存在绝对路径中）或使用Document数据类型的变量来选择输入数据文件。 例如， [Payload_Directory]/Workflow/data.xml. 如果crx-repository中不存在该路径，则管理员可以在使用该路径之前创建该路径。

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

* **[!UICONTROL 保存输出文档，使用]**：指定保存输出文件的位置。 可将输出文件保存在相对于有效负荷的位置、变量中，或指定绝对位置来保存输出文件。 如果crx-repository中不存在该路径，则管理员可以在使用该路径之前创建该路径。

**[!UICONTROL 高级属性]**

* **[!UICONTROL 使用以下方式选择内容根位置]**：内容根是一个字符串值，它指定存储库中的URI、绝对引用或位置以检索表单设计使用的相对资源。 例如，如果窗体设计相对引用图像，例如 `../myImage.gif`， `myImage.gif` 必须位于 `repository://`. 默认值为 `repository://`，指向存储库的根级别。

   从应用程序中选择资源时，内容根URI路径必须具有正确的结构。 例如，如果从名为SampleApp的应用程序中挑选表单，并将其放在 `SampleApp/1.0/forms/Test.xdp`，必须将内容根URI指定为 `repository://administrator@password/Applications/SampleApp/1.0/forms/`，或 `repository:/Applications/SampleApp/1.0/forms/` （当授权为空）。 以这种方式指定内容根URI时，表单中所有引用资产的路径都将针对此URI解析。

* **[!UICONTROL 使用以下方式选择XCI文件]**：XCI文件用于描述用于表单设计元素的字体和其他属性。 您可以将XCI文件相对于有效负荷保留在绝对路径上，或者使用Document数据类型的变量。

* **[!UICONTROL 区域设置]**：指定用于生成PDF文档的语言。 如果提供文本值，请从列表中选择一种语言或选择以下值之一：
   * **[!UICONTROL 使用服务器默认值]**：（默认）使用在 [!DNL AEM Forms] 服务器。 区域设置是使用Administration Console配置的。 (请参阅 [Designer帮助](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/using-designer.pdf).)

   * **[!UICONTROL 使用自定义值]**：在文本框中键入区域设置代码，或选择包含区域设置代码的字符串变量。 有关支持的区域设置代码的完整列表，请参阅https://docs.oracle.com/javase/1.5.0/docs/guide/intl/locale.doc.html。

* **[!UICONTROL 副本]**：一个整数值，它指定要为输出生成的副本数。 默认值为 1。

* **[!UICONTROL 双面打印]**：指定使用双面打印还是单面打印的“分页”值。 支持PostScript和PCL的打印机使用此值。 如果提供文本值，请选择以下值之一：
   * **[!UICONTROL 双面长边]**：使用双面打印和使用长边分页进行打印。
   * **[!UICONTROL 双面短边]**：使用双面打印和使用短边分页进行打印。
   * **[!UICONTROL 单面]**：使用单面打印。

## 生成非交互式PDF输出步骤   {#generatePDFdocuments}

1. 将“生成非交互式PDF输出”工作流拖动到Sidekick的“Forms Workflow”选项卡下。
1. 双击添加的工作流步骤以编辑组件。
1. 在“编辑组件”对话框中，配置输入文档、输出文档和其他参数，然后单击 **[!UICONTROL 确定]**.

### 输入文档 {#input-documents-3}

* **模板文件**：指定XDP模板的位置。 它是必填字段。

* **数据文档**：指定需要与模板合并的数据xml的位置。

### 输出文档 {#output-document}

**输出文档**：指定生成的PDF表单的名称。

### 其他参数 {#additional-parameters-1}

* **内容根**：指定存储库中用于存储输入XDP模板中使用的片段或图像的文件夹的路径。
* **区域设置**：指定生成的PDF表单的默认区域设置。
* **Acrobat版本**：为生成的PDF表单指定目标Acrobat版本。
* **线性PDF**：指定是否优化生成的PDF以进行Web查看。
* **已标记的PDF**：指定是否使生成的PDF可访问。
* **XCI文档**：指定XCI文件的路径。
