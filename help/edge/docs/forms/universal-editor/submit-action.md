---
title: 提交操作
description: 配置自适应表单的提交操作。
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: beee9be7-8215-496b-9fb9-61fba000a055
hide: true
hidefromToC: true
source-git-commit: 565336d96a718a46f23d0acfa6155a6fd78ad87d
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# 自适应表单提交操作

## 概述

表单提交是用户旅程中至关重要的最后一步——在此阶段，将会处理所收集的数据并触发相应操作。本文档提供了在通用编辑器中配置和管理自适应表单提交操作的完整指南。

### 您将了解的内容

阅读本文档后，您将掌握以下内容：

* 为表单配置不同类型的提交操作
* 设置 REST 端点提交，以实现与外部系统的集成
* 配置表单响应的电子邮件提交
* 实施针对特定业务需求的自定义提交操作
* 处理表单提交过程中的验证与出错场景

### 目标受众

本指南面向以下人群：

* 负责实施提交逻辑的&#x200B;**表单开发人员**
* 负责将表单与后端系统连接起来的&#x200B;**系统集成商**
* 负责定义表单工作流的&#x200B;**业务分析师**
* 负责设计表单提交流程的&#x200B;**技术架构师**

### 可用的提交操作

通用编辑器提供两种主要的提交操作类型：

1. **提交至 REST 端点** * 将表单数据发送至 API 端点
2. **发送电子邮件** * 通过电子邮件传递表单响应内容

### 先决条件

在配置提交操作之前，请确保您具有：

* 通用编辑器的访问权限
* 表单配置的相应权限
* 了解目标提交端点或电子邮件配置要求

提交操作指定了通过自适应表单所收集数据的目标。当用户单击表单上的&#x200B;**[!UICONTROL 提交]**&#x200B;按钮时，提交过程就开始了。AEM Forms 提供以下两种类型的提交操作，您可以创建和使用自定义提交操作，以满足您的特定需求。开箱即用的提交操作有：

<!--To define a Submit Action for an Adaptive Form, you use the Properties dialog of the **Adaptive Form block** in the **Editor**-->

* [提交到 REST 端点](#rest-endpoint-submission-ue)
* [发送电子邮件](#email-submission-ue)


### 提交到 REST 端点 {#rest-endpoint-submission-ue}

“提交到 REST 端点”操作用于将提交的表单数据发送到指定的 REST 端点。端点可以属于托管表单的内部服务器，也可以通过使用相对路径或绝对路径使其属于外部服务器。要将数据提交到托管表单的 AEM 服务器，请使用与 AEM 服务器的根路径对应的相对路径。例如，`/content/forms/af/SampleForm.html`。要将数据提交到任何其他服务器，请使用绝对路径。

<!--Configuring the Submit Action to REST Endpoint for Adaptive Forms offers several benefits such as:  
* It facilitates seamless integration of form data with external systems and services via RESTful APIs.  
* Offers flexibility in managing data submissions from Adaptive Forms, accommodating dynamic and complex data structures.  
* Allows dynamic mapping of form fields to parameters within the REST endpoint URL, enabling adaptable and customizable data submissions.
-->



要配置 REST 端点：

1. 在&#x200B;**[!UICONTROL 编辑器]**&#x200B;中打开自适应表单。
1. 选择 **[!UICONTROL Adaptive Form Block]**。
1. 单击属性![属性](/help/forms/assets/Smock_Properties_18_N.svg)图标。
1. 从&#x200B;**[!UICONTROL 提交操作]**&#x200B;下拉列表中选择&#x200B;**[!UICONTROL 提交到 REST 端点]**。
1. 指定 REST 端点 URL。
1. 您也可以&#x200B;**启用 POST 请求**&#x200B;并提供用于发布请求的 URL。

![通用编辑器属性面板截图，展示了用于配置 REST 端点的字段，包括 URL 输入框和用于启用 POST 请求的切换开关](/help/forms/assets/enable-post-request-ue.png)

>[!NOTE]
>
> * 要将数据发布到内部服务器，请提供资源的路径。数据将发布到资源的路径。例如，`/content/restEndPoint`。对于此类 POST 请求，将使用提交请求的身份验证信息。
> * 要将数据发布到外部服务器，请提供 URL。URL 的格式为 `https://host:port/path_to_rest_end_point`。确保配置以匿名方式处理 POST 请求的路径。

### 发送电子邮件 {#email-submission-ue}

通过“发送电子邮件”提交操作，您可以在成功提交表单后向一个或多个收件人发送电子邮件。发送电子邮件配置可帮助您创建可以包含预定义格式的表单数据的电子邮件。例如，考虑使用以下模板，其中的客户名称、配送地址、州名称和邮政编码从提交的表单数据中检索获得。[了解有关自适应表单中的电子邮件模板的更多信息](/help/forms/html-email-templates-in-adaptive-forms.md)。使用“发送电子邮件”提交操作配置自适应表单的一些优势如下：

1. 由于表单数据会直接发送给指定的电子邮件收件人，因此可以实现快速通信。
1. 直接将表单提交集成到电子邮件通知中，有助于简化工作流程。
1. 帮助组织自定义电子邮件内容，使其适合特定的通信需求。

![通用编辑器中的自适应表单属性](/help/forms/assets/submit-actions-ue.png)


将提交操作配置为表单提交的电子邮件：

1. 在&#x200B;**编辑器**&#x200B;中打开自适应表单。
1. 选择您的 **[!UICONTROL Adaptive Form Block]**。
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
      <td>指定电子邮件的主要收件人，可以添加多个电子邮件地址，用逗号分隔。</td>
    </tr>
    <tr>
      <td><b>抄送</td>
      <td>指定应收到电子邮件副本（CC）的收件人。</td>
    </tr>
    <tr>
      <td><b>BCC</td>
      <td>指定应收到电子邮件密件抄送（BCC）的收件人。</td>
    </tr>
    <tr>
      <td><b>主题</td>
      <td>指定电子邮件的主题行。</td>
    </tr>
    <tr>
      <td><b>使用外部模板</td>
      <td>允许使用外部电子邮件模板来确定电子邮件内容的格式。提供外部模板的 URL 或路径，以集成 AEM Assets 文件夹中保存的预先设计的电子邮件模板。</td>
    </tr>
    <tr>
      <td><b>包含附件</td>
      <td>指定提交的表单数据是否应包括电子邮件中通过表单提交的附件。支持的附件格式为 PDF、XML 和 JSON。</td>
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

    ![Screenshot of the Universal Editor email configuration panel showing fields for From, To, CC, BCC, Subject, and options for external templates and attachments](/help/forms/assets/email-config-ue.png)

-->

## 在自适应表单提交时显示一条自定义的感谢消息 {#submit-action-message-ue}

“提交时”选项可帮助您在自适应表单提交时配置“提交操作”消息。为表单配置“提交操作”消息：

1. 在&#x200B;**编辑器**&#x200B;中打开自适应表单。
1. 选择您的 **[!UICONTROL Adaptive Form Block]**。
1. 单击属性![属性](/help/forms/assets/Smock_Properties_18_N.svg)图标。
1. 单击后，您会看到以下选项：
   * **[!UICONTROL 提交时]**：“提交时”可帮助您自定义表单提交时要显示的信息。默认情况下，当表单成功提交时，会向用户显示一条自定义消息“感谢您提交表单”。
您还可以通过选择**[!UICONTROL 显示消息]**&#x200B;选项，然后在富文本&#x200B;**编辑器**&#x200B;中添加/编辑您的消息，从而在提交表单时自定义“感谢消息”。


## 另请参阅

{{universal-editor-see-also}}

