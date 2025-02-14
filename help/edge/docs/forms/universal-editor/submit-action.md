---
title: 提交操作
description: 为自适应表单配置提交操作。
feature: Edge Delivery Services
role: Admin, Architect, Developer
hide: true
hidefromtoc: true
exl-id: beee9be7-8215-496b-9fb9-61fba000a055
source-git-commit: ba38294710553145a670ea42dd2b7571fa4eba7b
workflow-type: tm+mt
source-wordcount: '733'
ht-degree: 12%

---

# 自适应表单提交操作

提交操作可指定通过自适应表单收集的数据的目标。 提交过程在用户单击表单上的&#x200B;**[!UICONTROL 提交]**&#x200B;按钮时开始。 AEM Forms提供以下所述的两种类型的提交操作，并允许您创建和使用自定义提交操作以满足特定需求。 现成的提交操作包括：

<!--To define a Submit Action for an Adaptive Form, you use the Properties dialog of the **Adaptive Form block** in the **Editor**-->

* [提交到 REST 端点](#rest-endpoint-submission-ue)
* [发送电子邮件](#email-submission-ue)


### 提交到 REST 端点 {#rest-endpoint-submission-ue}

“提交到REST端点”操作用于将提交的表单数据发送到指定的REST端点。 端点可以属于承载表单的内部服务器，也可以使用相对路径或绝对路径属于外部服务器。 要将数据提交到托管表单的 AEM 服务器，请使用与 AEM 服务器的根路径对应的相对路径。例如，`/content/forms/af/SampleForm.html`。要将数据提交到任何其他服务器，请使用绝对路径。

<!--Configuring the Submit Action to REST Endpoint for Adaptive Forms offers several benefits such as:  
* It facilitates seamless integration of form data with external systems and services via RESTful APIs.  
* Offers flexibility in managing data submissions from Adaptive Forms, accommodating dynamic and complex data structures.  
* Allows dynamic mapping of form fields to parameters within the REST endpoint URL, enabling adaptable and customizable data submissions.
-->



要配置REST端点，请执行以下操作：

1. 在&#x200B;**[!UICONTROL 编辑器]**&#x200B;中打开您的自适应表单。
1. 选择&#x200B;**[!UICONTROL 自适应表单块]**。
1. 单击属性![属性](/help/forms/assets/Smock_Properties_18_N.svg)图标。
1. 从&#x200B;**[!UICONTROL 提交操作]**&#x200B;下拉列表中选择&#x200B;**[!UICONTROL 提交到REST终结点]**。
1. 指定REST端点URL。
1. 您还可以&#x200B;**启用POST请求**，并提供一个URL以发布该请求。

![为自适应表单启用POST请求](/help/forms/assets/enable-post-request-ue.png)

>[!NOTE]
>
> * 要将数据发布到内部服务器，请提供资源的路径。 数据将发布到资源的路径。 例如，`/content/restEndPoint`。对于此类 POST 请求，将使用提交请求的身份验证信息。
> * 要将数据发布到外部服务器，请提供 URL。URL 的格式为 `https://host:port/path_to_rest_end_point`。确保配置以匿名方式处理 POST 请求的路径。

### 发送电子邮件 {#email-submission-ue}

“发送电子邮件提交操作”允许您在成功提交表单后向一个或多个收件人发送电子邮件。 “发送电子邮件”配置可帮助您创建电子邮件，以便以预定义格式包含表单数据。 例如，请考虑以下模板，其中从提交的表单数据中检索客户名称、送货地址、州名和邮政编码。 [在自适应Forms中了解有关电子邮件模板的更多信息](/help/forms/html-email-templates-in-adaptive-forms.md)。 使用“发送电子邮件”提交操作配置自适应表单的一些优点包括：

1. 它支持快速通信，因为表单数据会直接发送给指定的电子邮件收件人。
1. 它有助于通过将表单提交直接集成到电子邮件通知中来简化工作流。
1. 它有助于组织自定义电子邮件内容，使其适合特定的通信需求。

通用编辑器中的![自适应表单属性](/help/forms/assets/submit-actions-ue.png)


要将提交操作配置为表单提交的电子邮件，请执行以下操作：

1. 在&#x200B;**编辑器**&#x200B;中打开您的自适应表单。
1. 选择您的&#x200B;**[!UICONTROL 自适应表单块]**。
1. 单击属性![属性](/help/forms/assets/Smock_Properties_18_N.svg)图标。
1. 从&#x200B;**[!UICONTROL 提交操作]**&#x200B;下拉列表中选择&#x200B;**[!UICONTROL 发送电子邮件]**&#x200B;选项。
1. 选择发送电子邮件选项后，您可以配置以下属性，如下图所示。

<table>
  <thead>
    <tr>
      <th>图像</th>
      <th>属性</th>
      <th>描述</th>
    </tr>
  </thead>
  <tbody>
    <tr>
    <td rowspan="7"><img src="/help/forms/assets/email-config-ue.png" alt="电子邮件配置"></td> 
    <td><b>发件人</td>
    <td>指定发件人的电子邮件地址。</td>
    </tr>
    <tr>
      <td><b>收件人</td>
      <td>指定电子邮件的主要收件人，可添加多个电子邮件地址（用逗号分隔）。</td>
    </tr>
    <tr>
      <td><b>抄送</td>
      <td>指定应接收电子邮件副本(CC)的收件人。</td>
    </tr>
    <tr>
      <td><b>BCC</td>
      <td>指定应接收电子邮件的密件抄送(BCC)的收件人。</td>
    </tr>
    <tr>
      <td><b>主题</td>
      <td>指定电子邮件的主题行。</td>
    </tr>
    <tr>
      <td><b>使用外部模板</td>
      <td>允许使用外部电子邮件模板来格式化电子邮件内容。 提供外部模板的URL或路径，以集成托管在AEM Assets文件夹中的预设计电子邮件模板。</td>
    </tr>
    <tr>
      <td><b>包括附件</td>
      <td>指定提交的表单数据是否应包括通过电子邮件中的表单提交的附件。 支持的附件格式为PDF、XML和JSON。</td>
    </tr>
  </tbody>
</table>






<!--
        
        * **From**: The email address of the sender.
        * **To**: Specify the primary recipients of the email, multiple email addresses can be added, separated by commas.
        * **CC**: Specify the recipients who should receive a carbon copy (CC) of the email.
        * **BCC**: Specify the recipients who should receive a blind carbon copy (BCC) of the email.
        * **Subject**: Specify the subject line of the email.
        * **Use External Template**: Enables the use of an external email template for formatting the email content. Provide the URL or path to the External template path to integrate a pre-designed email template hosted in your AEM Assets folder.
        * **Include Attachment**: Specifies whether the submitted form data should include an attachment submitted through the form in the email.

    {width=50%,height=50%}![Enable post request for adaptive forms](/help/forms/assets/email-config-ue.png)

-->

## 在自适应表单提交时显示自定义感谢消息 {#submit-action-message-ue}

“在提交时”选项可帮助您在自适应表单提交时配置提交操作消息。要为表单配置提交操作消息：

1. 在&#x200B;**编辑器**&#x200B;中打开您的自适应表单。
1. 选择您的&#x200B;**[!UICONTROL 自适应表单块]**。
1. 单击属性![属性](/help/forms/assets/Smock_Properties_18_N.svg)图标。
1. 单击后，您会看到以下选项：
   * **[!UICONTROL 在提交时]**：在提交时，可帮助您自定义在提交表单时要显示的消息。 默认情况下，成功提交表单后，会向用户显示自定义消息“感谢您提交表单”。
您还可以通过选择**[!UICONTROL 显示消息]**&#x200B;的选项自定义表单提交的“感谢您”消息，并在富文本&#x200B;**编辑器**&#x200B;中添加/编辑您的消息。
