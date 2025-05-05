---
title: 如何使用AEM Forms实现业务流程自动化(BPM)？
seo-title: Rapidly build Adaptive Forms-based processes, automate document services operations, and use Adobe Sign with AEM workflows
description: 使用AEM Forms Workflow自动化并快速构建业务流程工作流。 例如，审阅和批准、PDF生成、Adobe Sign工作流程。
uuid: 797ba0f7-a378-45ac-9f82-fa9a952027be
topic-tags: publish, document_services
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: f0fec4a9-b214-4931-bf09-5898b082481e
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '2335'
ht-degree: 1%

---

# OSGi上以Forms为中心的工作流 {#forms-centric-workflow-on-osgi}

![主页图像](do-not-localize/header.png)

企业从成千上万个表单、各种后端系统以及在线或离线数据源中收集数据。 他们还拥有一组动态的用户来对数据做出决策，其中涉及反复的审核和批准流程。

除了针对内部和外部受众的审查和审批工作流之外，大型组织和企业还有重复性的任务。 例如，将PDF文档转换为另一种格式。 手动完成这些任务会占用很多时间和资源。 企业还有对文档进行数字签名并将表单数据存档以便以后以预定义格式使用的法律要求。

## OSGi上以Forms为中心的工作流简介 {#introduction-to-forms-centric-workflow-on-osgi}

您可以使用AEM Workflows快速构建基于Forms的自适应工作流。 这些工作流可用于审阅和批准、业务流程流、启动文档服务、与Adobe Sign签名工作流集成以及类似操作。 例如，信用卡申请处理、员工休假审批工作流、将表单另存为PDF文档。 此外，这些工作流还可以在组织内或跨网络防火墙使用。

借助OSGi上以Forms为中心的工作流，您可以在OSGi栈栈上快速构建和部署用于各种任务的工作流，而无需在JEE栈栈上安装完整的流程管理功能。 工作流的开发和管理使用熟悉的AEM Workflow和AEM Inbox功能。 工作流构成了跨多个软件系统、网络、部门甚至组织的真实业务流程自动化的基础。

设置后，可以手动触发这些工作流以完成定义的流程，或在用户提交表单<!-- or [correspondence management](cm-overview.md) letter-->时以编程方式运行。<!-- With this enhanced AEM Workflow capabilities, [!DNL AEM Forms] offers two distinct, yet similar, capabilities. As part of your deployment strategy, you need to decide which one works for you. See a [comparison](capabilities-osgi-jee-workflows.md) of the Forms-centric AEM Workflows on OSGi and Process Management on JEE. Moreover, for the deployment topology see, [Architecture and deployment topologies for [!DNL AEM Forms]]((aem-forms-architecture-deployment.md). -->

OSGi上以Forms为中心的工作流扩展了[AEM收件箱](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/getting-started/inbox.html#authoring)，并为AEM Workflow编辑器提供了额外的组件（步骤），以添加对以[!DNL AEM Forms]为中心的工作流的支持。<!-- The extended AEM Inbox has functionalities similar to [[!DNL AEM Forms] Workspace](introduction-html-workspace.md). Along with managing human-centric workflows (Approval, Review, and so on), you can use AEM workflows to automate [document services](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-step-ref.html#extending-aem)-related operations (for example, Generate PDF) and electronically signing (Adobe Sign) documents. -->

所有[!DNL AEM Forms]工作流步骤都支持使用变量。 变量使工作流步骤能够在运行时跨步骤保留和传递元数据。 您可以创建不同类型的变量以存储不同类型的数据。 您还可以创建变量集合（数组），用于存储相关同类型数据的多个实例。 通常，当您需要根据其持有的值做出决策时，或者需要存储稍后在流程中需要的信息时，可以使用变量或变量集合。 有关在这些以Forms为中心的工作流组件（步骤）中使用变量的更多信息，请参阅OSGi上的[以Forms为中心的工作流 — 步骤参考](aem-forms-workflow-step-reference.md)。 有关创建和管理变量的信息，请参阅AEM工作流中的[变量](variable-in-aem-workflows.md)。

下图描述了在OSGi上创建、运行和监控以Forms为中心的工作流的端到端过程。

![introduction-to-aem-forms-workflow](assets/introduction-to-aem-forms-workflow.jpg)

## 开始之前 {#before-you-start}

* 工作流是真实业务过程的一种表现形式。 让您的实际业务流程和业务流程参与者的列表做好准备。 此外，在开始创建工作流之前，应准备好宣传材料(自适应Forms、PDF文档等)。
* 一个工作流可以有多个阶段。 这些阶段显示在AEM收件箱中，并帮助报告工作流的进度。 将业务流程划分为逻辑阶段。
* 您可以配置AEM Workflows的分配任务步骤，以向用户或受分配人发送电子邮件通知。 因此，[启用电子邮件通知](#configure-email-service)。
* 工作流还可以使用Adobe签名进行数字签名。 如果计划在工作流中使用Adobe Sign，则在工作流中使用[为 [!DNL AEM Forms]](adobe-sign-integration-adaptive-forms.md)配置Adobe Sign之前。

## 创建工作流模型 {#create-a-workflow-model}

工作流模型由业务流程的逻辑和流程组成。 它由一系列步骤组成。 这些步骤是AEM组件。 您可以使用参数和脚本扩展工作流步骤，以根据需要提供更多功能和控制。 除了开箱即用的AEM步骤外，[!DNL AEM Forms]还提供了一些步骤。 有关AEM和[!DNL AEM Forms]步骤的详细列表，请参阅[AEM工作流步骤参考](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-step-ref.html#extending-aem)和[OSGi上以Forms为中心的工作流 — 步骤参考](aem-forms-workflow.md)。

AEM提供了一个直观的用户界面，用于使用提供的工作流步骤创建工作流模型。 有关创建工作流模型的分步说明，请参阅[创建工作流模型](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/workflows/overview.html#workflows)。 以下示例提供了为审批和审阅工作流创建工作流模型的分步说明：

>[!NOTE]
>
>您必须是工作流编辑器组的成员才能创建或编辑工作流模型。

### 为审批和审核工作流创建模型 {#create-a-model-for-an-approval-and-review-workflow}

审批和审核工作流适用于需要人工干预才能做出决定的任务。 以下示例为前台银行代理填写的抵押贷款申请创建工作流模型。 填写申请后，将发送该申请以供审批。 随后，经批准的申请将通过Adobe Sign发送给申请人电子签名。

该示例以如下附加的软件包形式提供。 使用包管理器导入并安装示例。 您还可以执行以下步骤来手动创建应用程序的工作流模型：

此示例创建一个工作流模型，用于创建一个由前台银行代理填写的抵押贷款申请。 填写完毕后，将发送申请以供审批。 稍后，将批准的申请发送给客户，以使用Adobe Sign进行电子签名。 您可以使用包管理器导入并安装示例。

[获取文件](assets/example-mortgage-loan-application.zip)

1. 打开工作流模型控制台。 默认URL为`https://[server]:[port]/libs/cq/workflow/admin/console/content/models.html/etc/workflow/models`
1. 选择&#x200B;**创建**，然后选择&#x200B;**创建模型**。 此时将显示“添加工作流模型”对话框。
1. 输入&#x200B;**标题**&#x200B;和&#x200B;**名称**（可选）。 例如，抵押贷款申请。 选择&#x200B;**完成**。
1. 选择已创建的工作流模型并选择&#x200B;**编辑**。 现在，您可以添加工作流步骤来构建业务逻辑。 首次创建工作流模型时，它包含：

   * 步骤：流程开始和流程结束。 这些步骤表示工作流的开始和结束。 这些步骤是必需的，无法编辑或删除。
   * 名为步骤1的参与者步骤示例。 此步骤配置为将工作项分配给管理员用户。 删除此步骤。

1. 启用电子邮件通知。 您可以在OSGi上配置以Forms为中心的工作流，以向用户或受分配人发送电子邮件通知。 执行以下配置以启用电子邮件通知：

   1. 前往`https://[server]:[port]/system/console/configMgr`处的AEM配置管理器。
   1. 打开&#x200B;**[!UICONTROL 天CQ邮件服务]**&#x200B;配置。 指定&#x200B;**[!UICONTROL SMTP服务器主机名]**、**[!UICONTROL SMTP服务器端口]**&#x200B;和&#x200B;**[!UICONTROL “发件人”地址]**&#x200B;字段的值。 单击&#x200B;**[!UICONTROL 保存]**。
   1. 打开&#x200B;**[!UICONTROL Day CQ Link Externalizer]**&#x200B;配置。 在&#x200B;**[!UICONTROL 域]**&#x200B;字段中，为本地、作者和发布实例指定实际的主机名/IP地址和端口号。 单击&#x200B;**[!UICONTROL 保存]**。

1. 创建工作流暂存。 一个工作流可以有多个阶段。 这些阶段显示在AEM收件箱中并报告工作流的进度。

   要定义阶段，请选择![信息圆圈](assets/info-circle.png)图标以打开工作流模型属性，打开&#x200B;**阶段**&#x200B;选项卡，为工作流模型添加阶段，然后选择&#x200B;**保存并关闭**。 例如，抵押贷款申请，创建阶段：贷款请求、贷款请求状态、要签名的文档、以及签名的贷款文档。

1. 将&#x200B;**分配任务**&#x200B;步骤浏览器拖放到工作流模型中。 使其成为模型的第一步。

   分配任务组件将工作流创建的任务分配给用户或组。 在分配任务时，您可以使用组件为该任务指定自适应表单或非交互式PDF。 接受来自用户的输入且非交互式PDF需要自适应表单，或者只读自适应表单用于仅审阅工作流。

   您还可以使用该步骤控制任务的行为。 例如，创建自动记录文档，将任务分配给特定用户或组，提交数据的路径，要预填充的数据路径以及默认操作。 有关分配任务步骤选项的详细信息，请参阅OSGi上的[以Forms为中心的工作流 — 步骤参考](aem-forms-workflow.md)文档。

   ![工作流编辑器](assets/workflow-editor.png)

   对于抵押贷款应用程序示例，将分配任务步骤配置为使用只读自适应表单并在任务完成后显示PDF文档。 此外，选择以允许审批贷款请求的用户组。 在&#x200B;**操作**&#x200B;选项卡上，禁用&#x200B;**提交**&#x200B;选项。 创建String数据类型的&#x200B;**actionTaken**&#x200B;变量，并将该变量指定为&#x200B;**路由变量**。 例如，actionTaken。 另外，添加批准路由和拒绝路由。 路由在AEM收件箱中显示为单独的操作（按钮）。 工作流会根据用户点击的操作（按钮）选择分支。

   您可以为配置的分配任务步骤的所有字段（例如，抵押应用程序）的完整值集导入示例包（可在部分开头下载）。

1. 将OR拆分组件从步骤浏览器拖放到工作流模型中。 OR拆分在工作流中创建拆分，之后只有一个分支处于活动状态。 此步骤允许您将条件处理路径引入工作流。 您可以根据需要向每个分支添加工作流步骤。

   您可以使用规则定义、ECMA脚本或外部脚本为分支定义路由表达式。

   使用表达式编辑器为Branch 1和Branch 2创建路由选择表达式。 这些路由表达式有助于根据AEM收件箱中的用户操作选择分支。

   分支1 **的**&#x200B;路由表达式

   当用户在AEM收件箱中点按&#x200B;**批准**&#x200B;时，分支1处于激活状态。

   ![OR拆分示例](assets/orsplit_branch1_active_new.png)

   分支2 **的**&#x200B;路由表达式

   当用户在AEM收件箱中点按&#x200B;**拒绝**&#x200B;时，分支2被激活。

   ![OR拆分示例](assets/orsplit_branch2_active_new.png)

   有关使用变量创建路由表达式的信息，请参阅 [!DNL AEM Forms] 工作流[&#128279;](variable-in-aem-workflows.md)中的变量。

1. 添加其他工作流步骤以构建业务逻辑。

   对于抵押示例，添加一个生成记录文档、两个分配任务步骤和一个签名文档步骤到模型的分支1，如下图所示。 一个分配任务步骤是显示&#x200B;**要签名的贷款文档并发送给申请人**，另一个分配任务组件是&#x200B;**以显示已签名的文档**。 另外，添加一个任务组件到分支2。 当用户点按AEM收件箱中的拒绝时，它会激活。

   对于配置的分配任务步骤、记录文档步骤和签名文档步骤（例如，抵押应用程序）的所有字段的完整值集，导入示例包，可在本节开头下载。

   工作流模型已准备就绪。 您可以通过各种方法启动工作流。 有关详细信息，请参阅[在OSGi上启动以Forms为中心的工作流](#launch)。

   ![workflow-editor-mortage](assets/workflow-editor-mortgage.png)

## 创建以Forms为中心的工作流应用程序 {#create-a-forms-centric-workflow-application}

应用程序是与工作流关联的自适应表单。 通过收件箱提交应用程序时，它会启动关联的工作流。 要使Forms工作流可用作AEM收件箱和[!DNL AEM Forms]应用程序中的应用程序，请执行以下操作以创建工作流应用程序：

>[!NOTE]
>
>您必须是fd-administrator组的成员才能创建和管理工作流应用程序。

1. 在您的AEM创作实例上，转到![tools-1](assets/tools-1.png) > **[!UICONTROL Forms]** > **[!UICONTROL 管理工作流应用程序]**，并点按&#x200B;**[!UICONTROL Create]**。
1. 在“创建工作流应用程序”窗口中，为以下字段提供输入，并点按&#x200B;**创建**。 将创建一个新应用程序，该应用程序将在Workflow Applications屏幕中列出。

<table>
 <tbody>
  <tr>
   <td>字段</td>
   <td>描述</td>
  </tr>
  <tr>
   <td>标题</td>
   <td>标题显示在AEM收件箱中，并帮助用户选择应用程序。 保持描述性。 例如，储蓄帐户开户申请。<br /> </td>
  </tr>
  <tr>
   <td>名称 </td>
   <td>指定应用程序的名称。 除字母、数字、连字符和下划线之外的所有字符都将替换为连字符。 </td>
  </tr>
  <tr>
   <td>描述</td>
   <td>该描述将显示在AEM收件箱中。 在描述字段中提供应用程序的详细信息。 例如，应用程序的用途。<br /> </td>
  </tr>
  <tr>
   <td>自适应表单</td>
   <td><p>指定自适应表单的路径。 当用户启动应用程序时，将显示指定的自适应表单。</p> <p><strong>注意</strong>：工作流应用程序不支持超过一页或需要在Apple iPad上滚动的表单和PDF文档。 在Apple iPad上打开应用程序，并且自适应表单或PDF文档长度超过一页时，第二页的表单字段和内容丢失。</p> </td>
  </tr>
  <tr>
   <td>访问组</td>
   <td><p>选择一个组。 该应用程序在AEM收件箱中仅对选定组的成员可见。 访问组选项使[!DNL workflow-users]组的所有组都可供选择。 </p> <br /> </td>
  </tr>
  <tr>
   <td>预填服务</td>
   <td>为自适应表单选择<a href="prepopulate-adaptive-form-fields.md#aem-forms-custom-prefill-service" target="_blank">预填充服务</a>。<br /> </td>
  </tr>
  <tr>
   <td>工作流模型</td>
   <td>为应用程序选择<a href="aem-forms-workflow.md#create-a-workflow-model">工作流模型</a>。 工作流模型是由业务过程的逻辑和流程组成的。 </td>
  </tr>
  <tr>
   <td>数据文件路径</td>
   <td>指定crx-repository中数据文件的路径。 路径是自适应表单有效负载的相对路径，包含数据文件的名称。 始终包括文件的完整名称，包括扩展名（如果适用）。 例如，[payload]/data.xml。 </td>
  </tr>
  <tr>
   <td>附件路径</td>
   <td>指定crx-repository中附件文件夹的路径。 附件路径相对于有效负荷位置。 例如，[payload]/data.xml。 </td>
  </tr>
  <tr>
   <td>记录文档路径</td>
   <td>指定crx-repository中记录文档文件的路径。 路径相对于自适应表单有效负荷位置。 始终包括文件的完整名称，包括扩展名（如果适用）。 例如，[payload]/DOR/creditcard.pdf。</td>
  </tr>
 </tbody>
</table>

## 在OSGi上启动以Forms为中心的工作流 {#launch}

您可以通过以下方式启动或触发以Forms为中心的工作流：

* [从AEM收件箱提交应用程序](#inbox)
* [从 [!DNL AEM Forms] 应用程序提交应用程序](#afa)

* [提交自适应表单](#af)
* [使用观察文件夹](#watched)

* [提交交互式通信或信件](#letter)

### 从AEM收件箱提交应用程序 {#inbox}

您创建的工作流应用程序可用作收件箱中的应用程序。 属于[!DNL workflow-users]组成员的用户可以填写并提交触发相关工作流的应用程序。

<!-- ### Submitting an application from [!DNL AEM Forms] App {#afa}

The [!DNL AEM Forms] app syncs with an [!DNL AEM Forms] server and lets you change the form data, tasks, workflow applications, and saved information (drafts/templates) in your account. For more information, see [[!DNL AEM Forms] app]((aem-forms-app.md) and related articles.-->

### 提交自适应表单 {#af}

您可以配置自适应表单的提交操作，以在提交自适应表单时启动工作流。 自适应Forms提供&#x200B;**调用AEM Workflow**&#x200B;提交操作以在提交自适应表单时启动工作流。 有关提交操作的详细信息，请参阅[配置提交操作](configuring-submit-actions.md)。 要通过[!DNL AEM Forms]应用程序提交自适应表单，请在自适应表单属性中启用“与[!DNL AEM Forms]应用程序同步”。

<!-- You can configure an Adaptive Form to sync, submit, and trigger a workflow from [!DNL AEM Forms] app. For details, see [working with a form]((working-with-form.md). -->

<!-- ### Using a watched folder {#watched}

An administrator (a member of fd-administrators group) can configure a network folder to run a pre-configured workflow when a user places a file (such as a PDF file) in the folder. After the workflow completes, it can save the result file to a specified output folder. Such a folder is known as [Watched Folder](watched-folder-in-aem-forms.md). Perform the following procedure to configure a watched folder to launch a workflow:

1. On your AEM author instance, go to ![tools-1](assets/tools-1.png) > **[!UICONTROL Forms]** > **[!UICONTROL Configure Watched Folder]**. A list of already configured watched folders is displayed.
1. Select **[!UICONTROL New]**. A list of fields is displayed. Specify a value for the following fields to configure a Watched Folder for a workflow:

<table>
 <tbody>
  <tr>
   <td>Field</td>
   <td>Description</td>
  </tr>
  <tr>
   <td><span class="uicontrol">Name</code></td>
   <td>Specify the name of the Watched Folder. This field support only alphanumeric.</td>
  </tr>
  <tr>
   <td><span class="uicontrol">Path</code></td>
   <td>Specify the physical location of the Watched Folder. In a clustered environment, use a shared network folder that is accessible from AEM cluster node.</td>
  </tr>
  <tr>
   <td><span class="uicontrol">Process Files Using</code></td>
   <td>Select the <span class="uicontrol">Workflow </code>option. </td>
  </tr>
  <tr>
   <td><span class="uicontrol">Workflow Model</code></td>
   <td>Select a workflow model.<br /> </td>
  </tr>
  <tr>
   <td><span class="uicontrol">Output File Pattern</code></td>
   <td>Specify the directory structure for output files and directories. </a>.</td>
  </tr>
 </tbody>
</table>

1. Select **Advanced**. Specify a value for the following field and taps **Create**. The Watched Folder is configured to launch a workflow. Now, whenever a file is placed in the input directory of the Watched Folder, the specified workflow is triggered.

   | Field |Description |
   |---|---|
   | Payload Mapper Filter |When you create a watched folder, it creates a folder structure in the crx-repository. The folder structure can serve as a payload to the workflow. You can write a script to map an AEM Workflow to accept inputs from the watched folder structure. An out of the box implementation is available and listed in the Payload Mapper Filter. If you do not have a custom implementation, select the default implementation. |

   The Advanced tab contains more fields. Most of these fields contain a default value. To learn about all the fields, see the [Create or Configure a watched folder]((admin-help/configuring-watched-folder-endpoints.md) article. -->

<!-- ### Submitting an interactive communication or a letter {#letter}

You can associate and execute a Forms-centric workflow on OSGi on submission of an interactive communication or a letter. In correspondence management workflows are used for post processing interactive communications and letters. For example, emailing, printing, faxing, or archiving final letters. For detailed steps, see [Post processing of interactive communications and letters](submit-letter-topostprocess.md).

## Additional Configurations {#additional-configurations}

### Configure email service {#configure-email-service}

You can use the Assign Task and Send Email steps of AEM Workflows to send an email. Perform the following steps to specify email servers and other configurations required to send email:

1. Go to AEM configuration manager at `https://[server]:[port]/system/console/configMgr`.
1. Open the **[!UICONTROL Day CQ Mail Service]** configuration. Specify a value for the **[!UICONTROL SMTP server host name]**, **[!UICONTROL SMTP server port]**, and **[!UICONTROL "From" address]** fields. Click **[!UICONTROL Save]**.
1. Open the **[!UICONTROL Day CQ Link Externalizer]** configuration. In the **[!UICONTROL Domains]** field, specify the actual hostname/IP address and port number for local, author, and publish instances. Click **[!UICONTROL Save]**. -->

### 清除工作流实例 {#purge-workflow-instances}

最大限度地减少工作流实例的数量可以提高工作流引擎的性能，因此您可以定期从存储库中清除已完成或正在运行的工作流实例。 有关详细信息，请参阅[定期清除工作流实例](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/maintenance.html?lang=zh-Hans)清除工作流实例
