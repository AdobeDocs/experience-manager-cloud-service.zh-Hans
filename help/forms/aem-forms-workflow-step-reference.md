---
title: '如何向其他用户分配工作流、发送电子邮件、在工作流中使用Adobe Sign? '
description: 以Forms为中心的工作流允许您快速构建基于Forms的自适应工作流。 您可以使用Adobe Sign对文档进行电子签名、创建基于表单的业务流程、检索数据并将其发送到多个数据源，以及发送电子邮件通知
exl-id: e1403ba6-8158-4961-98a4-2954b2e32e0d
source-git-commit: 211724e8031c6b83ca202739d2bc56007243d3d5
workflow-type: tm+mt
source-wordcount: '5467'
ht-degree: 1%

---

# 以Forms为中心的AEM工作流 — 步骤参考 {#forms-centric-workflow-on-osgi-step-reference}

您可以使用工作流模型将业务逻辑转换为自动重复流程。 模型可帮助您定义和执行一系列步骤。 您还可以定义模型属性，例如工作流是临时的还是使用多个资源。 您可以 [在模型中包含各种AEM工作流步骤以实现业务逻辑](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html?lang=en#extending-aem).

## 以Forms为中心的步骤 {#forms-workflow-steps}

以Forms为中心的工作流步骤可在AEM工作流中执行特定于AEM Forms的操作。 这些步骤允许您在OSGi上快速构建基于Forms的以Forms为中心的自适应工作流。 这些工作流可用于开发基本的审核和批准工作流、内部和跨防火墙的业务流程。 您还可以使用Forms Workflow步骤：

* 创建业务流程、提交后工作流和后端工作流以管理注册流程。

* 创建任务并将其分配给用户或组。

* 使用 [!DNL Adobe Sign] 在AEM工作流中发送要签名的文档。

* 按需或在提交表单时生成记录文档。

* 将工作流模型与各种数据源连接起来，以便轻松保存和检索数据。

* 使用电子邮件步骤，在完成操作并在工作流开始或完成时发送通知电子邮件和其他附件。

>[!NOTE]
>
>如果为外部存储标记了工作流模型，则对于所有Forms工作流步骤，您只能选择变量选项来存储或检索数据文件和附件。


## 分配任务步骤 {#assign-task-step}

分配任务步骤将创建一个工作项并将其分配给用户或组。 除了分配任务外，组件还为任务指定自适应表单或非交互式PDF。 需要自适应表单才能接受用户输入且非交互式PDF，或者只读自适应表单只能用于审阅工作流。

您还可以使用组件来控制任务的行为。 例如，创建自动记录文档、将任务分配给特定用户或组、指定提交数据的路径、指定要预填充的数据路径以及指定默认操作。 “分配任务”步骤具有以下属性：

* **[!UICONTROL 标题]**:任务的标题。 标题会显示在AEM收件箱中。
* **[!UICONTROL 描述]**:任务中正在执行的操作说明。 当您在共享开发环境中工作时，此信息对于其他流程开发人员非常有用。

* **[!UICONTROL 缩略图路径]**:任务缩略图的路径。 如果未指定路径，则会为自适应表单默认缩略图显示，为记录文档显示默认图标。
* **[!UICONTROL 工作流阶段]**:一个工作流可以具有多个阶段。 这些阶段会显示在AEM收件箱中。 您可以在模型的属性（Sidekick >页面>页面属性>阶段）中定义这些阶段。
* **[!UICONTROL 优先级]**:选定的优先级将显示在AEM收件箱中。 可用选项包括“高”、“中”和“低”。 默认值为“中”。
* **[!UICONTROL 到期日期]**:指定任务标记为逾期的天数或小时数。 如果您选择 **[!UICONTROL 关闭]**，则任务永远不会被标记为过期。 您还可以指定超时处理程序，以在任务过期后执行特定任务。

* **[!UICONTROL 天]**:任务完成前的天数。 在将任务分配给用户后，将计为天数。 如果任务未完成，并且跨越“天”字段中指定的天数，则如果选中，将在到期日期后触发超时处理程序。
* **[!UICONTROL 小时]**:任务完成前的小时数。 在将任务分配给用户后，将计为小时数。 如果任务未完成，并跨越“小时”字段中指定的小时数，则如果选中，则会在到期小时后触发超时处理程序。
* **[!UICONTROL 到期日期后超时]**:选择此选项可启用超时处理程序选择字段。
* **[!UICONTROL 超时处理程序]**:选择要在分配任务步骤跨越到期日期时执行的脚本。 放置在CRX存储库(位于 [应用程序]/fd/dashboard/scripts/timeoutHandler可供选择。 crx-repository中不存在指定的路径。 管理员在使用路径之前会创建该路径。
* **[!UICONTROL 在任务详细信息中突出显示最后一个任务中的操作和注释]**:选择此选项可显示上次执行的操作以及收到的对任务详细信息部分的评论。
* **[!UICONTROL 类型]**:选择启动工作流时要填写的文档类型。 您可以选择自适应表单、只读自适应表单、非交互式PDF文档。 <!-- , Interactive Communication Agent UI, or Interactive Communication Web Channel Document. -->
* **[!UICONTROL 使用自适应表单]**:指定定位输入自适应表单的方法。 如果从“类型”下拉列表中选择“自适应表单”或“只读自适应表单”，则此选项将可用。 您可以使用提交到工作流的自适应表单（在绝对路径上可用，或在变量的路径上可用）。 您可以使用字符串类型的变量指定路径。\
   您可以将多个自适应Forms与工作流相关联。 因此，您可以使用可用的输入方法在运行时指定自适应表单。

<!-- 
* **[!UICONTROL Use Interactive Communication]**: Specify the method to locate the input interactive communication. You can use the interactive communication submitted to the workflow, available at an absolute path, or available at a path in a variable. You can use a variable of type String to specify the path. This option is available if you select Interactive Communication Agent UI or Interactive Communication Web Channel Document from the Type drop-down list. 

> [!NOTE]
>
>You must have cm-agent-users and workflow-users group assignments to access Interactive Communications Agent UI in AEM inbox.  -->

* **[!UICONTROL 自适应表单路径]**:指定自适应表单的路径。<!--  or Interactive Communication.--> 您可以使用自适应表单 <!-- or interactive communication --> 提交到工作流的自适应表单（位于绝对路径中），或从字符串数据类型变量中存储的路径中检索自适应表单。
* **[!UICONTROL 使用选择输入PDF]**:指定非交互式PDF文档的路径。 在“类型”字段中选择非交互式PDF文档时，该字段将可用。 您可以使用相对于有效负荷的路径选择输入PDF，该路径保存在绝对路径中，或使用“文档”数据类型的变量。 例如， [Payload_Directory]/Workflow/PDF/credit-card.pdf。 crx-repository中不存在路径。 管理员在使用路径之前会创建该路径。 要使用“记录文档路径”选项，您需要启用“记录文档”选项，或者需要基于表单模板的自适应Forms来PDF。
* **[!UICONTROL 对于已完成的任务，将自适应表单渲染为]**:当任务标记完成时，您可以将自适应表单呈现为只读自适应表单或PDF文档。 您需要启用“记录文档”选项或基于表单模板的自适应Forms，才能将自适应表单渲染为记录文档。
* **[!UICONTROL 预填充]**:下面列出的字段用作任务的输入：

   * **[!UICONTROL 使用选择输入数据文件]**:输入数据文件（.json、.xml、.doc或表单数据模型）的路径。 您可以使用相对于有效负载的路径检索输入数据文件，或检索存储在Document、XML或JSON数据类型变量中的文件。 例如，文件包含通过AEM收件箱应用程序为表单提交的数据。 示例路径为 [Payload_Directory]/workflow/data.
   * **[!UICONTROL 使用]**:该位置可用的附件会附加到与任务关联的表单。 该路径可以相对于有效负荷，或检索存储在文档变量中的附件。 示例路径为 [Payload_Directory]/attachments/. 您可以指定相对于有效负载放置的附件，或使用文档类型（数组列表>文档）变量为自适应表单指定输入附件。

   <!-- * **[!UICONTROL Choose input JSON]**: Select an input JSON file using a path that is relative to payload or stored in a variable of Document, JSON, or Form Data Model data type. This option is available if you select Interactive Communication Agent UI or Interactive Communication Web Channel Document from the Type drop-down list.

    * **[!UICONTROL Choose a custom prefill service]**: Select the prefill service to retrieve the data and prefill the Interactive Communication Web channel document or the Agent UI.  
    
    * **[!UICONTROL Use the prefill service of the interactive communication selected above]**: Use this option to use the prefill service of the Interactive Communication defined in the Use Interactive Communication drop-down list. -->
   * **[!UICONTROL 请求属性映射]**:使用“请求属性映射”部分定义 [请求属性的名称和值](work-with-form-data-model.md#bindargument). 根据请求中指定的属性名称和值，从数据源检索详细信息。 您可以使用字面值或字符串数据类型的变量定义请求属性值。

   <!--  The prefill service and request attribute mapping options are available only if you select Interactive Communication Agent UI or Interactive Communication Web Channel Document from the Type drop-down list. -->

* **[!UICONTROL 提交的信息]**:下面列出的字段用作任务的输出位置：

   * **[!UICONTROL 使用保存输出数据文件]**:保存数据文件（.json、.xml、.doc或表单数据模型）。 数据文件包含通过关联表单提交的信息。 您可以使用相对于有效负载的路径保存输出数据文件，或将其存储在Document、XML或JSON数据类型的变量中。 例如， [Payload_Directory]/Workflow/data，其中数据是文件。
   * **[!UICONTROL 使用保存附件]**:保存任务中提供的表单附件。 您可以使用相对于有效负载的路径保存附件，或将其存储在“文档”数据类型数组列表的变量中。
   * **[!UICONTROL 使用保存记录文档]**:保存记录文档的路径。 例如， [Payload_Directory]/DocumentofRecord/credit-card.pdf。 您可以使用相对于有效负荷的路径保存记录文档，或将其存储在“文档”数据类型的变量中。 如果您选择 **[!UICONTROL 相对于有效负载]** 选项，则路径字段留空时不会生成记录文档。 仅当您从类型下拉列表中选择自适应表单时，此选项才可用。

   <!-- * **[!UICONTROL Save Web Channel data using]**: Save the Web Channel data file using a path that is relative to the payload or store it in a variable of Document, JSON, or Form Data Model data type. This option is available only if you select Interactive Communication Agent UI from the Type drop-down list. c
    * **[!UICONTROL Save PDF document using]**: Save the PDF document using a path that is relative to the payload or store it in a variable of Document data type. This option is available only if you select Interactive Communication Agent UI from the Type drop-down list.
    <!-- * **[!UICONTROL Save layout template using]**: Save the layout template using a path that is relative to the payload or store it in a variable of Document data type. The [layout template](layout-design-details.md) refers to an XDP file that you create using Forms Designer. This option is available only if you select Interactive Communication Agent UI from the Type drop-down list. -->

* **[!UICONTROL 被分派人]** > **[!UICONTROL 分配选项]**:指定将任务分配给用户的方法。 您可以使用“参与者选择器”脚本将任务动态分配给用户或组，或将任务分配给特定的AEM用户或组。
* **[!UICONTROL 参与者选择器]**:当 **[!UICONTROL 动态发送给用户或组]** 选项。 您可以使用ECMAScript或服务动态选择用户或组。 有关更多信息，请参阅 [动态地为用户分配工作流](https://helpx.adobe.com/experience-manager/kb/HowToAssignAWorkflowDynamicallyToParticipants.html) 和 [创建自定义Adobe Experience Manager动态参与者步骤。](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=en&amp;CID=RedirectAEMCommunityKautuk)

* **[!UICONTROL 参与者]**:当 **[!UICONTROL com.adobe.granite.workflow.core.process.RandomParticipantChooser]** 选项 **[!UICONTROL 参与者选择器]** 字段。 利用字段，可为RandomParticipantChooser选项选择用户或组。

* **[!UICONTROL 被分派人]**:当 **[!UICONTROL com.adobe.fd.workspace.step.service.VariableParticipantChooser]** 的 **[!UICONTROL 参与者选择器]** 字段。 利用字段，可选择字符串数据类型的变量以定义代理人。

* **[!UICONTROL 参数]**:当在“参与者选择器”字段中选择RandomParticiantChoose脚本以外的脚本时，该字段将可用。 利用字段，可为在“参与者选择器”字段中选择的脚本提供以逗号分隔的参数列表。

* **[!UICONTROL 用户或组]**:该任务被分配给选定的用户或组。 当 **[!UICONTROL 到特定用户或群组选项]** 的 **[!UICONTROL 分配选项]** 字段。 该字段列出了 [!DNL workflow-users] 群组。\
   的 **[!UICONTROL 用户或组]** 下拉菜单列出了登录用户有权访问的用户和组。 用户名的显示取决于您是否拥有 **[!UICONTROL 用户]** 该特定用户的crx-repository中的节点。

* **[!UICONTROL 发送通知电子邮件]**:选择此选项可向被分派人发送电子邮件通知。 在将任务分配给用户或组时，会发送这些通知。 您可以使用 **[!UICONTROL 收件人电子邮件地址]** 选项，以指定检索电子邮件地址的机制。

* **[!UICONTROL 收件人电子邮件地址]**:您可以在变量中存储电子邮件地址，使用文字指定永久电子邮件地址，或使用在被分派人配置文件中指定的被分派人的默认电子邮件地址。 您可以使用文字或变量指定组的电子邮件地址。 变量选项有助于动态检索和使用电子邮件地址。 的 **[!UICONTROL 使用被分派人的默认电子邮件地址]** 选项仅适用于单个代理人。 在这种情况下，会使用存储在受分配用户配置文件中的电子邮件地址。

* **[!UICONTROL HTML电子邮件模板]**:为通知电子邮件选择电子邮件模板。 要编辑模板，请修改crx-repository中位于/libs/fd/dashboard/templates/email/htmlEmailTemplate.txt的文件。
* **[!UICONTROL 允许委派到]**:AEM收件箱为已登录的用户提供了一个选项，用于将分配的工作流委派给其他用户。 允许您在同一组内委派给另一个组的工作流用户。 如果任务被分配给单个用户，并且 **[!UICONTROL 允许委派给受让人组成员]** 选项，则无法将任务委派给其他用户或组。
* **[!UICONTROL 共享设置]**:AEM收件箱提供用于与其他用户共享收件箱中单个或所有任务的选项：
   * 当 **[!UICONTROL 允许被分派人明确在收件箱中共享]** 选项时，用户可以在AEM收件箱中选择该任务，并将其与其他AEM用户共享。
   * 当 **[!UICONTROL 允许被分派人通过收件箱共享进行共享]** 选项，用户可共享其收件箱项目或允许其他用户访问其收件箱项目，则只会与其他用户共享启用之前所述选项的任务。
   * 当 **[!UICONTROL 允许被分派人使用“不在办公室”设置委派]** 中。 代理人可以启用选项，将任务连同其他“不在办公室”选项一起委派给其他用户。 分配给外出用户的任何新任务都会自动委派（分配）给出来设置中提到的用户。

   它允许其他用户在外出时选择受分配任务，无法处理分配的任务。

* **[!UICONTROL 操作]** > **[!UICONTROL 默认操作]**:现成可用的提交、保存和重置操作。 默认情况下，所有默认操作都处于启用状态。
* **[!UICONTROL 路由变量]**:路由变量的名称。 route变量可捕获用户在AEM收件箱中选择的自定义操作。
* **[!UICONTROL 路由]**:任务可以分支到不同的路由。 在AEM收件箱中选择该路由后，该路由将返回一个值，并根据选定的路由返回工作流分支。 您可以将路由存储在字符串数据类型数组的变量中，也可以选择 **[!UICONTROL 文字]** 手动添加路由。

* **[!UICONTROL 路由标题]**:指定路由的标题。 它显示在AEM收件箱中。
* **[!UICONTROL Coral图标]**:指定珊瑚图标的HTML属性。 AdobeCorelUI库提供了大量的触屏优先图标。 您可以选择并使用路由的图标。 它与标题一起显示在AEM收件箱中。 如果将路由存储在变量中，则路由将使用默认的“标记”珊瑚图标。
* **[!UICONTROL 允许被分派人添加评论]**:选择此选项可为任务启用注释。 任务提交时，被分派人可以从AEM收件箱中添加评论。
* **[!UICONTROL 在变量中保存注释]**:将注释保存在字符串数据类型的变量中。 仅当您选择 **[!UICONTROL 允许被分派人添加评论]** 复选框。

* **[!UICONTROL 允许被分派人向任务添加附件]**:选择此选项可为任务启用附件。 任务提交时，被分派人可以从AEM收件箱中添加附件。 您还可以限制最大大小 **[!UICONTROL （最大文件大小）]** 附件。 默认大小为2 MB。

* **[!UICONTROL 使用保存输出任务附件]**:指定附件文件夹的位置。 您可以使用相对于有效负荷的路径或文档数据类型数组的变量来保存输出任务附件。 仅当您选择 **[!UICONTROL 允许被分派人向任务添加附件]** 复选框和选择 **[!UICONTROL 自适应表单]**, **[!UICONTROL 只读自适应表单]**&#x200B;或 **[!UICONTROL 非交互式PDF文档]** 从 **[!UICONTROL 类型]** 下拉列表 **[!UICONTROL 表单/文档]** 选项卡。

* **[!UICONTROL 使用自定义元数据]**:选择此选项可启用自定义元数据字段。 自定义元数据在电子邮件模板中使用。
* **[!UICONTROL 自定义元数据]**:为电子邮件模板选择自定义元数据。 自定义元数据可在crx-repository中的apps/fd/dashboard/scripts/metadataScripts访问。 crx-repository中不存在指定的路径。 管理员在使用路径之前会创建该路径。 您还可以将服务用于自定义元数据。 您还可以扩展 `WorkitemUserMetadataService` 用于提供自定义元数据的界面。
* **[!UICONTROL 显示前一步骤的数据]**:选择此选项可使受分配人能够查看以前的受分配人、已对任务执行的操作、添加到任务的注释以及已完成任务的记录文档（如果可用）。
* **[!UICONTROL 显示后续步骤的数据]**:选择此选项可使当前代理人能够查看由后续代理人执行的操作和添加到任务的注释。 它还允许当前受让人查看已完成任务的记录文档（如果可用）。
* **[!UICONTROL 数据类型的可见性]**:默认情况下，代理人可以查看记录文档、受让人、已采取的操作以及先前和后续受让人已添加的注释。 使用数据类型的可见性选项限制受让人可见的数据类型。

>[!NOTE]
>
>在为外部数据存储配置AEM工作流模型时，将“分配任务”步骤另存为草稿并检索“分配任务”步骤历史记录的选项会被禁用。 此外，在收件箱中，用于保存的选项处于禁用状态。

## 发送电子邮件步骤 {#send-email-step}

使用电子邮件步骤发送电子邮件，例如，包含自适应表单记录文档的电子邮件链接 <!-- , link of an interactive communication-->，或附加PDF文档。 “发送电子邮件”步骤支持 [HTML电子邮件](https://en.wikipedia.org/wiki/HTML_email). HTML电子邮件是响应式的，可根据收件人的电子邮件客户端和屏幕大小进行调整。 您可以使用HTML电子邮件模板来定义电子邮件的外观、颜色方案和行为。

电子邮件步骤使用Day CQ Mail Service发送电子邮件。 在使用电子邮件步骤之前，请确保已配置电子邮件服务。 默认情况下，电子邮件仅支持HTTP和HTTP协议。 [联系支持团队](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html?lang=en#sending-email) 启用用于发送电子邮件的端口，并为环境启用SMTP协议。 此限制有助于提高平台的安全性。

电子邮件步骤具有以下属性：

**[!UICONTROL 标题]**:步骤的标题有助于在工作流编辑器中识别步骤。

**[!UICONTROL 描述]**:当您在共享开发环境中工作时，此说明对于其他流程开发人员非常有用。

**[!UICONTROL 电子邮件主题]**:主题可以从工作流元数据中检索（手动指定），或从变量中存储的值中检索。 从以下选项中进行选择：

* **[!UICONTROL 文字]** 手动指定主题。
* **[!UICONTROL 从工作流元数据中检索]**  — 从元数据属性中检索主题。
* **[!UICONTROL 变量]**  — 从字符串数据类型变量中存储的值检索主题。

**[!UICONTROL HTML电子邮件模板]**:HTML电子邮件模板。 您可以在电子邮件模板中指定变量。 电子邮件步骤会提取并显示模板中包含的所有变量以用于输入。

**[!UICONTROL 电子邮件模板元数据]**:电子邮件模板变量的值可以是用户指定的值、作者或发布服务器上资产的路径、图像或工作流元数据属性。

* **[!UICONTROL 文字]**:当您知道要指定的确切值时，请使用选项。 例如， [example@example.com](mailto:example@example.com).

* **[!UICONTROL 工作流元数据]**:将要使用的值保存在工作流元数据属性中时，请使用选项。 选择选项后，在工作流元数据选项下方的空文本框中输入元数据属性名称。 例如， emailAddress。

<!-- * **[!UICONTROL Asset URL]**: Use the option to embed a web link of an interactive communication to the email. After selecting the option, browse and choose the interactive communication to embed. The asset can reside on the author or the publish server. -->
* **[!UICONTROL 图像]**:使用选项将图像嵌入到电子邮件中。 选择选项后，浏览并选择图像。 图像选项仅适用于电子邮件模板中可用的图像标记(&lt;img src=&quot;*&quot; />)。

**[!UICONTROL 发件人/收件人的电子邮件地址]**:选择 **[!UICONTROL 文字]** 用于手动指定电子邮件地址或选择 **[!UICONTROL 从工作流元数据中检索]** 用于从元数据属性中检索电子邮件地址的选项。 您还可以为 **[!UICONTROL 从工作流元数据中检索]** 选项。 选择 **[!UICONTROL 变量]** 用于从字符串数据类型变量中存储的值检索电子邮件地址的选项。

* **[!UICONTROL 文件附件]**:指定位置的可用资产会附加到电子邮件中。 资产的路径可以是相对于有效负载的路径，也可以是绝对路径。 示例路径为 [Payload_Directory]/attachments/.

选择 **[!UICONTROL 变量]** 用于检索存储在文档、XML或JSON数据类型变量中的文件附件的选项。

**[!UICONTROL 文件名]**:电子邮件附件文件的名称。 电子邮件步骤将附件的原始文件名更改为指定的文件名。 可以手动指定或从工作流元数据属性或变量中检索名称。 使用 **[!UICONTROL 文字]** 选项。 使用 **[!UICONTROL 变量]** 用于从字符串数据类型变量中存储的值检索文件名的选项。 使用 **[!UICONTROL 从工作流元数据中检索]** 选项。

## 生成记录文档步骤 {#generate-document-of-record-step}

填写或提交表单后，您可以以打印或文档格式保留表单的记录。 此记录称为记录文档(DoR)。 您可以使用生成记录文档步骤创建自适应表单的只读或交互式PDF版本。 PDF版本包含填写到表单中的信息以及自适应表单的布局。

“记录文档”步骤具有以下属性：

**[!UICONTROL 使用自适应表单]**:指定定位输入自适应表单的方法。 您可以使用提交到工作流的自适应表单（在绝对路径上可用，或在变量的路径上可用）。 您可以使用字符串数据类型的变量在 **[!UICONTROL 选择要解析的变量]** 字段。\
您可以将多个自适应Forms与工作流相关联。 因此，您可以使用可用的输入方法在运行时指定自适应表单。

**[!UICONTROL 自适应表单路径]**:指定自适应表单的路径。 当您选择 **[!UICONTROL 在绝对路径下可用]** 选项 **[!UICONTROL 使用自适应表单]** 字段。

**[!UICONTROL 使用选择输入数据]**:自适应表单的输入数据路径。 您可以将数据保留在相对于有效负载的位置，指定数据的绝对路径，或检索存储在文档、JSON或XML数据类型变量中的数据。 输入数据将与自适应表单合并以创建记录文档。

**[!UICONTROL 使用]**:附件的路径。 这些附件包含在记录文档中。 您可以将附件保留在相对于有效负载的位置，指定附件的绝对路径，或检索存储在Document数据类型数组变量中的附件。

如果指定文件夹的路径（例如附件），则文件夹中直接可用的所有文件都将附加到记录文档。 如果任何文件在指定附件路径中直接可用的文件夹中可用，则这些文件将作为附件包含在记录文档中。 如果直接可用的文件夹中存在任何文件夹，则会跳过这些文件夹。

**[!UICONTROL 使用以下选项保存生成的记录文档]**:指定保留记录文档文件的位置。 您可以选择覆盖有效负荷文件夹，将记录文档放在有效负荷目录中的某个位置，或将记录文档存储在文档类型的变量中。

**[!UICONTROL 区域设置]**:指定记录文档的语言。 选择 **[!UICONTROL 文字]** 从下拉列表中选择区域设置或选择 **[!UICONTROL 变量]** 用于从字符串数据类型变量中存储的值检索区域设置。 在变量中存储区域设置值时，必须定义区域设置代码。 例如，指定 **en_US** (英语和 **fr_FR** 法语。

## 调用表单数据模型服务步骤 {#invoke-form-data-model-service-step}

您可以使用 [[!DNL AEM Forms] 数据集成](data-integration.md) 配置和连接到不同的数据源。 这些数据源可以是Web服务、REST服务、OData服务和CRM解决方案。 [!DNL AEM Forms] 数据集成允许您创建包含各种服务的表单数据模型，以对配置的数据库执行数据检索、添加和更新操作。 您可以使用 **[!UICONTROL 调用数据模型服务步骤]** 选择表单数据模型(FDM)，然后使用FDM的服务来检索、更新或将数据添加到不同的数据源。

为了说明步骤字段的输入，以下数据库表和JSON文件作为示例：

**[!UICONTROL CustomerDetails表示例]**

<table>
 <tbody> 
  <tr> 
   <td>属性</td> 
   <td>值<br /> </td> 
  </tr> 
  <tr> 
   <td>名字<br /> </td> 
   <td>莎拉<br /> </td> 
  </tr> 
  <tr> 
   <td>姓氏</td> 
   <td>罗斯</td> 
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

**[!UICONTROL JSON文件示例]**

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

“调用表单数据模型服务”步骤列出了以下字段，以便于执行表单数据模型操作：

* **[!UICONTROL 标题]**:步骤的标题。 它有助于在工作流编辑器中确定步骤。
* **[!UICONTROL 描述]**:当您在共享开发环境中工作时，此说明对其他流程开发人员非常有用。

* **[!UICONTROL 表单数据模型路径]**:浏览并选择服务器上存在的表单数据模型。

* **[!UICONTROL 错误和验证]**:利用选项，可捕获错误消息，并为检索到并发送到数据源的数据指定验证选项。 通过这些更改，您可以确保传递到调用表单数据模型服务步骤的数据符合数据源定义的数据约束。 有关更多详细信息，请参阅 [自动验证输入数据](work-with-form-data-model.md#automated-validation-of-input-data)

* **[!UICONTROL 验证级别]**:验证分为三类：基本、完整和关闭：

   * 完整：所有约束都经过验证。
   * 基本：仅必需和可为空的约束
   * 关闭：不进行验证。

* **[!UICONTROL 失败时终止工作流]**:当约束验证失败时，工作流将停止。

* **[!UICONTROL 在变量中存储错误代码]**:您可以在 [字符串类型变量](variable-in-aem-workflows.md).

* **[!UICONTROL 将错误消息存储在变量中]**:您可以在 [字符串类型变量](variable-in-aem-workflows.md).

* **[!UICONTROL 在变量中存储错误详细信息]**:您可以在 [JSON类型变量](variable-in-aem-workflows.md).

* **[!UICONTROL 服务]**:所选表单数据模型提供的服务列表。
* **[!UICONTROL 服务输入]** > **[!UICONTROL 使用文字、变量或工作流元数据和JSON文件提供输入数据]**:一个服务可以有多个参数。 选择选项，以从工作流元数据属性、JSON对象、变量获取服务参数的值，或直接在提供的文本框中输入值：

   * **[!UICONTROL 文字]**:当您知道要指定的确切值时，请使用选项。 例如， srose@we.info。
   * **[!UICONTROL 变量]**:使用选项检索存储在变量中的值。
   * **[!UICONTROL 从工作流元数据中检索]**:将要使用的值保存在工作流元数据属性中时，请使用选项。 例如， emailAddress。

   * **[!UICONTROL 相对于有效负载]**:使用选项检索保存在相对于有效负荷的路径上的文件附件。 选择选项并指定包含文件附件的文件夹名称，或在文本框中指定文件附件名称。

      例如，如果CRX存储库中的Relative to Payload文件夹在 `attachment\attachment-folder` 位置，指定 `attachment\attachment-folder` （在文本框中） **[!UICONTROL 相对于有效负载]** 选项。

   * **[!UICONTROL JSON点表示法]**:当要使用的值位于JSON文件中时，请使用选项。 例如， insurance.customerDetails.emailAddress。 仅当选择了来自输入JSON的映射输入字段选项时，“JSON点表示法”选项才可用。
   * **[!UICONTROL 映射来自输入JSON的输入字段]**:指定JSON文件的路径，以从JSON文件获取某些服务参数的输入值。 JSON文件的路径可以是相对于有效负载的路径、绝对路径，也可以是使用JSON或表单数据模型类型的变量选择输入JSON文档。

* **[!UICONTROL 服务输入]** > **[!UICONTROL 使用变量或JSON文件提供输入数据]**:选择选项，以从保存在绝对路径、相对于有效负载的路径或变量中的JSON文件获取所有参数的值。
* **[!UICONTROL 使用选择输入JSON文档]**:包含所有服务参数值的JSON文件。 JSON文件的路径可以是 **[!UICONTROL 相对于有效载荷]** 或 **[!UICONTROL 绝对路径]**. 您还可以使用JSON或表单数据模型数据类型的变量来检索输入JSON文档。

* **[!UICONTROL JSON点表示法]**:将字段留空，以使用指定JSON文件的所有对象作为服务参数的输入。 要从指定的JSON文件中读取特定JSON对象作为服务参数的输入，请为JSON对象指定点表示法，例如，如果您的JSON与部分开头列出的JSON类似，请指定insurance.customerDetails，以提供作为服务输入的客户的所有详细信息。
* **[!UICONTROL 服务输出]** > **[!UICONTROL 将输出值映射到变量或元数据]**:选择选项，将输出值另存为crx-repository中工作流实例元数据节点的属性。 指定元数据属性的名称并选择要映射为元数据属性的相应服务输出属性，例如，将输出服务返回的phone_number映射为工作流元数据的phone_number属性。 同样，您可以将输出存储在Long数据类型的变量中。 当您为 **[!UICONTROL 要映射的服务输出属性]** 选项，则只会为 **[!UICONTROL 将输出保存到]** 选项。

* **[!UICONTROL 服务输出]** > **[!UICONTROL 将输出保存到变量或JSON文件]**:选择选项，以在JSON文件中的绝对路径、相对于有效负载的路径或变量中保存输出值。
* **[!UICONTROL 使用以下选项保存输出JSON文档]**:保存输出JSON文件。 输出JSON文件的路径可以是相对于有效负载的路径，也可以是绝对路径。 您还可以使用JSON或表单数据模型数据类型的变量保存输出JSON文件。

## “签名文档”步骤 {#sign-document-step}

使用“签名文档”步骤，您可以使用 [!DNL Adobe Sign] 来签署文档。 在使用 [!DNL Adobe Sign] Workflow 步骤对自适应表单进行签名时，可以将表单逐个传送给签名者，也可以将表单同时发送给所有签名者，具体取决于工作流步骤的配置。仅在所有签名者完成签名过程后，[!DNL Adobe Sign] 支持的自适应表单才提交到 Experience Manager Forms Server。

默认情况下，[!DNL Adobe Sign] 调度程序服务每 24 小时检查（轮询）一次签名者响应。您可以 [更改环境的默认间隔](adobe-sign-integration-adaptive-forms.md##configure-adobe-sign-scheduler-to-sync-the-signing-status).

“签名文档”步骤具有以下属性：

* **[!UICONTROL 协议名称]**:指定协议的标题。 协议名称将成为发送给签名者的电子邮件的主题和正文文本的一部分。 您可以将名称存储在字符串数据类型的变量中，或选择 **[!UICONTROL 文字]** 手动添加名称。

* **[!UICONTROL 区域设置]**:指定电子邮件和验证选项的语言。 您可以将区域设置存储在字符串数据类型的变量中，也可以选择 **[!UICONTROL 文字]** 从可用选项列表中选择区域设置。 在变量中存储区域设置值时，必须定义区域设置代码。 例如，指定 **[!UICONTROL en_US]** (英语和 **[!UICONTROL fr_FR]** 法语。

* **[!UICONTROL Adobe Sign云配置]**:选择 [!DNL Adobe Sign] 云配置。 如果您尚未配置 [!DNL Adobe Sign] 表示 [!DNL AEM Forms]，请参阅 [将Adobe Sign与 [!DNL AEM Forms]](adobe-sign-integration-adaptive-forms.md).

* **[!UICONTROL 选择要使用签名的文档]**:您可以从相对于有效负荷的位置选择文档，使用有效负荷作为文档，指定文档的绝对路径，或检索存储在“文档”数据类型变量中的文档。
* **[!UICONTROL 截止时间前的天数]**:在中指定的天数内，任务上没有活动，则文档会标记为到期（已过期） **[!UICONTROL 截止时间前的天数]** 字段。 在将记录的分配给用户进行签名后，将计为天数。
* **[!UICONTROL 提醒电子邮件频度]**:您可以以每日或每周间隔发送提醒电子邮件。 该周将从记录的被分配给用户进行签名的当天开始计数。
* **[!UICONTROL 签名过程]**:您可以选择按顺序或并行顺序对文档进行签名。 按顺序，一个签名者每次接收文档以进行签名。 在第一个签名者完成对文档的签名后，将该文档发送给第二个签名者，依此类推。 同时，多个签名者可以一次对文档进行签名。
* **[!UICONTROL 重定向URL]**:指定重定向URL。 在文档签名后，您可以将代理人重定向到一个URL。 通常，此URL包含感谢信或进一步说明。
* **[!UICONTROL 工作流阶段]**:一个工作流可以具有多个阶段。 这些阶段会显示在AEM收件箱中。 可以在模型的属性中定义这些阶段( **[!UICONTROL Sidekick]** > **[!UICONTROL 页面]** > **[!UICONTROL 页面属性]** > **[!UICONTROL 阶段]**)。
* **[!UICONTROL 选择签名者]**:指定为文档选择签名者的方法。 您可以动态地将工作流分配给用户或组，或手动添加签名者的详细信息。
* **[!UICONTROL 用于选择签名者的脚本或服务]**:仅当在选择签名者字段中选择了动态选项时，该选项才可用。 您可以指定ECMAScript或服务来为文档选择签名者和验证选项。
* **[!UICONTROL 签名者详细信息]**:仅当在选择签名者字段中选择了手动选项时，该选项才可用。 指定电子邮件地址并选择可选的验证机制。 在选择两步验证机制之前，请确保为配置的 [!DNL Adobe Sign] 帐户。 您可以使用字符串数据类型的变量来定义电子邮件、国家/地区代码和电话号码字段的值。 仅当您从2步验证下拉列表中选择电话验证时，才会显示“国家/地区代码”和“电话号码”字段。

<!-- ## Document Services steps {#document-services-steps}

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
* **[!UICONTROL Indirect accessible printer]**: The printer that is installed on a print server is accessed from other computers. Technologies such as the common UNIX® printing system (CUPS) and the Line Printer Daemon (LPD) protocol are available to connect to a network printer. To access an indirect accessible printer, specify the print server’s IP or host name. Using this mechanism, you can send a document to an LPD URI when the network has an LPD running. The mechanism lets you route the document to any printer that is connected to the network that has an LPD running.

### Generate Printed Output Step {#generatePrintedOutput}

The step generates a PCL, PostScript, ZPL, IPL, TPCL, or DPL output given a form design and data file. The data file is merged with the form design and formatted for printing. The output generated by this step can be sent directly to a printer or saved as file. It is recommended that you use this step when you want to use form designs or data from an application. If your form designs or form designs are located on the network, local file system, or HTTP location, use the generatePrintedOutput operation operation.

For example, your application requires that you merge a form design with a data file. The data contains hundreds of records. In addition, it requires the output is sent to a printer that supports ZPL. The form design and your input data are located in an application. Use the generatePrintedOutput operation to merge each record with a form design and send the output to a printer that supports ZPL.

The Generate Printed Output step has the following properties:

**[!UICONTROL Input properties]**

* **[!UICONTROL Select template file using]**: Specify the path of the template file. You can select the template file using the path that is relative to the payload, saved at an absolute path, or using a variable of Document data type. For example, [Payload_Directory]/Workflow/data.xml. If the path does not exist in crx-repository, an administrator can create the path before using it. Moreover, you can also accept payload as the input data file.

* **[!UICONTROL Select data document using]**: Specify the path of a input data file. You can select the input data file using the path that is relative to the payload, saved at an absolute path, or using a variable of Document data type. For example, [Payload_Directory]/Workflow/data.xml. If the path does not exist in crx-repository, an administrator can create the path before using it.

* **[!UICONTROL Printer Format]**: A Print Format value that specifies the page description language to use, when an XDC file is not provided, to generate the output stream. If you provide a literal value, select one of these values:

  * **[!UICONTROL Custom PCL]**: Use the option to specify a custom XDC file for PCL.
  * **[!UICONTROL Custom PostScript]**: Use the option to specify a custom XDC file for PostScript.
  * **[!UICONTROL Custom ZPL]**: Use the option to specify a custom XDC file file for ZPL.
  * **[!UICONTROL Generic Color PCL (5c)]**: Use a generic color PCL (5c).
  * **[!UICONTROL Generic PostScript Level3]**: Use generic PostScript Level 3.
  * **[!UICONTROL ZPL 300 DPI]**: Use ZPL 300 DPI. The zpl300.xdc is used.
  * **[!UICONTROL ZPL 600 DPI]**: Use ZPL 600 DPI. The zpl600.xdc file is used.
  * **[!UICONTROL Custom IPL]**: Use the option to specify a custom XDC file for IPL.
  * **[!UICONTROL IPL 300 DPI]**: Use IPL 300 DPI. The ipl300.xdc is used.
  * **[!UICONTROL IPL 400 DPI]**: Use IPL 400 DPI. The ipl400.xdc file is used.
  * **[!UICONTROL Custom TPCL]**: Use the option to specify a custom XDC file for TPCL.
  * **[!UICONTROL TPCL 305 DPI]**: Use TPCL 300 DPI. The tpcl305.xdc file is used.
  * **[!UICONTROL PCL 600 DPI]**: Use TPCL 600 DPI. The tpcl600.xdc file is used.
  * **[!UICONTROL Custom DPL]**: Use the option to specify a custom XDC file DPL.
  * **[!UICONTROL DPL300DPI]**: Use DPL 300 DPI. The dpl300.xdc file is used.
  * **[!UICONTROL DPL406DPI]**: Use DPL 400 DPI. The dpl406.xdc is used.
  * **[!UICONTROL DPL600DPI]**: Use DPL 600 DPI. The dpl600.xdc is used.

**[!UICONTROL Output Properties]**

* **[!UICONTROL Save output document using]**: Specify the location to save the output file. You can save the output file at an location  which is relative to the payload, in a variable, or specify an absolute location to save the output file. If the path does not exist in crx-repository, an administrator can create the path before using it.

**[!UICONTROL Advanced Properties]**

* **[!UICONTROL Select Content Root location using]**: Content root is a string value that specifies the URI, absolute reference, or location in the repository to retrieve relative assets used by the form design. For example, if the form design references an image relatively, such as ../myImage.gif, myImage.gif must be located at repository://. The default value is repository://, which points to the root level of the repository.

  When you pick an asset from your application, the Content Root URI path must have the correct structure. For example, if a form is picked from an application named SampleApp, and is placed at SampleApp/1.0/forms/Test.xdp, the Content Root URI must be specified as repository://administrator@password/Applications/SampleApp/1.0/forms/, or repository:/Applications/SampleApp/1.0/forms/ (when authority is null). When the Content Root URI is specified this way, the paths of all of the referenced assets in the form will be resolved against this URI.

* **[!UICONTROL Select XCI file using]**: XCI files are used to describe fonts and other properties that are used for form design elements. You can keep an XCI file relative to the payload, at an absolute path, or using a variable of Document data type.

* **[!UICONTROL Locale]**: Specifies the language used for generating the PDF document. If you provide a literal value, select a language from the list or select one of these values:
  * **[!UICONTROL To use server default]**:
    (Default) Use the Locale setting configured on the [!DNL AEM Forms] Server. The Locale setting is configured using Administration Console. (See [Designer Help](http://www.adobe.com/go/learn_aemforms_designer_65).)

  * **[!UICONTROL To use custom value]**:
    Type the Locale code in the literal box or select a string variable containing the locale code. For a complete list of supported locale codes, see http://java.sun.com/j2se/1.5.0/docs/guide/intl/locale.doc.html.

* **[!UICONTROL Copies]**: An integer value that specifies the number of copies to generate for the output. The default value is 1.

* **[!UICONTROL Duplex Printing]**:  A Pagination value that specifies whether to use two-sided or single-sided printing. Printers that support PostScript and PCL use this value.If you provide a literal value, select one of these values:
    * **[!UICONTROL Duplex Long Edge]**: Use two-sided printing and print using long-edge pagination. 
    * **[!UICONTROL Duplex Short Edge]**: Use two-sided printing and print using short-edge pagination. 
    * **[!UICONTROL Simplex]**: Use single-sided printing.-->
