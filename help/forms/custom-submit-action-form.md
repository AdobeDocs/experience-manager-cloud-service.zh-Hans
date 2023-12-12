---
title: 如何为自适应表单创建自定义提交操作？
description: 了解如何为自适应Forms创建自定义提交操作，以便在将数据提交到Rest端点、保存到数据存储和执行其他自定义函数之前延迟提交和处理数据。
feature: Adaptive Forms, Foundation Components
role: User
level: Intermediate
exl-id: 77131cc2-9cb1-4a00-bbc4-65b1a66e76f5
source-git-commit: f419883d0e83b5d711e0f594a8e14a8f2133f4b1
workflow-type: tm+mt
source-wordcount: '1670'
ht-degree: 1%

---

# 创建自适应Forms的自定义提交操作 {#writing-custom-submit-action-for-adaptive-forms}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/forms/customize-aem-forms/custom-submit-action-form.html) |
| AEM as a Cloud Service | 本文 |

自适应表单提供多个现成的提交操作(OOTB)。 提交操作可指定要对通过自适应表单收集的数据执行的操作的详细信息。 例如，通过电子邮件发送数据。

您可以创建自定义提交操作以添加中未包含的功能 [现成提交操作](configuring-submit-actions.md) 或者不支持通过单个OOTB提交操作。 例如，将数据提交到工作流，将数据保存在数据存储中，向提交表单的人员发送电子邮件通知，并通过单个提交操作向负责处理已提交表单以供审批和拒绝的人员发送电子邮件。

## XML数据格式 {#xml-data-format}

使用将XML数据发送到servlet **`jcr:data`** 请求参数。 提交操作可以访问参数以处理数据。 以下代码描述了XML数据的格式。 绑定到表单模型的字段显示在 **`afBoundData`** 部分。 未绑定字段显示在 `afUnoundData`部分。 <!--For more information about the format of the `data.xml` file, see [Introduction to prepopulating Adaptive Form fields](prepopulate-adaptive-form-fields.md).-->

```xml
<?xml ?>
<afData>
<afUnboundData>
<data>
<field1>value</field2>
<repeatablePanel>
    <field2>value</field2>
</repeatablePanel>
<repeatablePanel>
    <field2>value</field2>
</repeatablePanel>
</data>
</afUnboundData>
<afBoundData>
<!-- xml corresponding to the Form Model /XML Schema -->
</afBoundData>
</afData>
```

### 操作字段 {#action-fields}

提交操作可以添加隐藏的输入字段(使用HTML) [输入](https://developer.mozilla.org/en/docs/Web/HTML/Element/Input) 标签)到渲染的表单HTML。 这些隐藏字段可以包含处理表单提交时所需的值。 在提交表单时，这些字段值作为请求参数回发，提交操作可在提交处理期间使用这些参数。 输入字段称为操作字段。

例如，如果提交操作还捕获填写表单所用的时间，则可以添加隐藏的输入字段 `startTime` 和 `endTime`.

脚本可以提供 `startTime` 和 `endTime` 表单渲染时和表单提交前的字段。 提交操作脚本 `post.jsp` 之后，可以使用请求参数访问这些字段，并计算填写表单所需的总时间。

### 文件附件 {#file-attachments}

“提交操作”还可以使用您通过“文件附件”组件上传的文件附件。 提交操作脚本可以使用sling访问这些文件 [RequestParameter API](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/request/RequestParameter.html). 此 [isFormField](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/request/RequestParameter.html#isFormField()) api的方法有助于识别请求参数是文件还是表单字段。 您可以在“提交操作”中对“请求”参数进行迭代，以确定“文件附件”参数。

以下示例代码标识请求中的文件附件。 接下来，它使用 [获取API](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/request/RequestParameter.html#get()). 最后，它会使用数据创建一个Document对象，并将其附加到列表中。

```java
RequestParameterMap requestParameterMap = slingRequest.getRequestParameterMap();
for (Map.Entry<String, RequestParameter[]> param : requestParameterMap.entrySet()) {
    RequestParameter rpm = param.getValue()[0];
    if(!rpm.isFormField()) {
        fileAttachments.add(new Document(rpm.get()));
    }
}
```

将文件附加到自适应表单时，服务器会在提交自适应表单后验证文件附件，并在以下情况下返回错误消息：

* 文件附件包括以(.)开头的文件名 字符，包含\ / ： * ？ “ &lt; > | ； % $个字符，或包含为Windows操作系统保留的特殊文件名，如 `nul`， `prn`， `con`， `lpt`，或 `com`.

* 文件附件的大小为0字节。

* 文件附件的格式未在 [支持的文件类型](https://helpx.adobe.com/cn/document-cloud/help/supported-file-formats-fill-sign.html#main-pars_text) 部分。

### 转发路径和重定向URL {#forward-path-and-redirect-url}

执行所需的操作后，提交servlet将请求转发到转发路径。 一个操作使用setForwardPath API在指南提交servlet中设置转发路径。

如果操作不提供转发路径，则提交Servlet将使用重定向URL重定向浏览器。 作者使用“自适应表单编辑”对话框中的“感谢页面”配置来配置重定向URL。 您还可以通过提交操作或指南提交servlet中的setRedirectUrl API配置重定向URL。 您还可以使用指南提交servlet中的setRedirectParameters API配置发送到重定向URL的请求参数。

>[!NOTE]
>
>作者提供了重定向URL（使用感谢页面配置）。 [OOTB提交操作](configuring-submit-actions.md) 使用重定向URL从转发路径引用的资源重定向浏览器。
>
>您可以编写自定义提交操作，将请求转发到资源或servlet。 Adobe建议在处理完成后，为转发路径执行资源处理的脚本将请求重定向到重定向URL。

## 提交操作 {#submit-action}

提交操作是一个sling：Folder，它包括以下内容：

* **addfields.jsp**：此脚本提供在呈现版本期间添加到HTML文件中的操作字段。 此脚本用于在post.context.jsp脚本中添加提交期间所需的POST输入参数。
* **dialog.xml**：此脚本类似于CQ组件对话框。 它提供作者自定义的配置信息。 选择提交操作后，这些字段显示在“自适应表单编辑”对话框的“提交操作”选项卡中。
* **post.POST.jsp**：提交servlet使用您提交的数据以及前面部分中的附加数据调用此脚本。 本页中有关运行操作的任何内容都表示运行post.post.jspPOST。 要在自适应Forms中注册提交操作以在“自适应表单编辑”对话框中显示，请将这些属性添加到sling:Folder:

   * **guideComponentType** 字符串和值的类型 **fd/af/components/guidesubmittype**
   * **guideDataModel** 类型字符串，指定提交操作适用的自适应表单的类型。 <!--**xfa** is supported for XFA-based Adaptive Forms while -->**xsd** 基于XSD的自适应Forms支持。 **基本** 对于不使用XDP或XSD的自适应Forms支持。 要在多种类型的自适应Forms上显示操作，请添加相应的字符串。 用逗号分隔每个字符串。 例如，要在以下位置显示操作： <!--XFA- and -->基于XSD的自适应Forms，指定值为 <!--**xfa** and--> **xsd**.

   * **jcr：description** 类型为String。 此属性的值显示在“自适应表单编辑”对话框的“提交操作”选项卡的“提交操作”列表中。 OOTB操作存在于该位置的CRX存储库中 **/libs/fd/af/components/guidesubmittype**.

   * **submittservice** 类型为String。 有关更多信息，请参阅 [为自定义操作计划自适应表单提交](#schedule-adaptive-form-submission).

## 创建自定义提交操作 {#creating-a-custom-submit-action}

执行以下步骤可创建自定义提交操作，将数据保存在CRX存储库中，并向您发送电子邮件。 自适应表单包含OOTB提交操作存储内容（已弃用），可将数据保存在CRX存储库中。 此外，AEM还提供 [邮件](https://www.adobe.io/experience-manager/reference-materials/6-5/javadoc/com/day/cq/mailer/package-summary.html) 可用于发送电子邮件的API。 在使用Mail API之前，通过系统控制台配置Day CQ Mail服务。 您可以重用“存储内容（已弃用）”操作将数据存储在存储库中。 在CRX存储库中的/libs/fd/af/components/guidesubmittype/store位置提供了“存储内容（已弃用）”操作。

1. 通过URL https://登录CRXDE Lite&lt;server>：&lt;port>/crx/de/index.jsp. 在/apps/custom_submit_action文件夹中创建具有属性sling：Folder并命名为store_and_mail的节点。 创建custom_submit_action文件夹（如果尚不存在）。

   ![描述使用属性sling：Folder创建节点的屏幕截图](assets/step1.png)

1. **提供必需的配置字段。**

   添加存储区操作所需的配置。 复制 **cq：dialog** 从/libs/fd/af/components/guidessubmittype/store到/apps/custom_submit_action/store_and_email操作文件夹的“存储”操作的节点。

   ![显示将对话框节点复制到操作文件夹的屏幕截图](assets/step2.png)

1. **提供配置字段以提示作者进行电子邮件配置。**

   自适应表单还提供向用户发送电子邮件的电子邮件操作。 根据您的要求自定义此操作。 导航到/libs/fd/af/components/guidessubmittype/email/dialog。 将cq：dialog节点中的节点复制到提交操作(/apps/custom_submit_action/store_and_email/dialog)的cq：dialog节点。

   ![自定义电子邮件操作](assets/step3.png)

1. **使操作在“自适应表单编辑”对话框中可用。**

   在store_and_email节点中添加以下属性：

   * **guideComponentType** 类型 **字符串** 和值 **fd/af/components/guidesubmittype**

   * **guideDataModel** 类型 **字符串** 和值 **<!--xfa, -->xsd，基本**

   * **jcr：description** 类型 **字符串** 和值 **存储和电子邮件操作**

   * **submittservice** 类型 **字符串** 和值 **商店和电子邮件**. 有关更多信息，请参阅 [为自定义操作计划自适应表单提交](#schedule-adaptive-form-submission).

1. 打开任意自适应表单。 单击 **编辑** 按钮旁边 **开始** 以打开 **编辑** 自适应表单容器的对话框。 新操作将显示在 **提交操作** 选项卡。 选择 **存储和电子邮件操作** 显示对话框节点中添加的配置。

   ![提交操作配置对话框](assets/store_and_email_submit_action_dialog.jpg)

1. **使用操作完成任务。**

   将post.jsp.jspPOST添加到您的操作中。 (/apps/custom_submit_action/store_and_mail/)。

   运行OOTB Store操作(post.store.jspPOST)。 使用 [FormsHelper.runAction](https://www.adobe.io/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/foundation/forms/FormsHelper.html#runAction-java.lang.String-java.lang.String-org.apache.sling.api.resource.Resource-org.apache.sling.api.SlingHttpServletRequest-org.apache.sling.api.SlingHttpServletResponse-)(java.lang.String， java.lang.String， org.apache.sling.api.resource.Resource， org.apache.sling.api.SlingHttpServletRequest， org.apache.sling.api.SlingHttpServletResponse) CQ在您的代码中提供的API，用于运行存储操作。 在JSP文件中添加以下代码：

   `FormsHelper.runAction("/libs/fd/af/components/guidesubmittype/store", "post", resource, slingRequest, slingResponse);`

   要发送电子邮件，代码会从配置中读取收件人的电子邮件地址。 要获取操作脚本中的配置值，请使用以下代码读取当前资源的属性。 同样，您可以读取其他配置文件。

   `ValueMap properties = ResourceUtil.getValueMap(resource);`

   `String mailTo = properties.get("mailTo");`

   最后，使用CQ Mail API发送电子邮件。 使用 [简单电子邮件](https://commons.apache.org/proper/commons-email/apidocs/org/apache/commons/mail/SimpleEmail.html) 类以创建电子邮件对象，如下所述：

   >[!NOTE]
   >
   >确保JSP文件的名称是post.pository.jspPOST。

   ```java
   <%@include file="/libs/fd/af/components/guidesglobal.jsp" %>
   <%@page import="com.day.cq.wcm.foundation.forms.FormsHelper,
          org.apache.sling.api.resource.ResourceUtil,
          org.apache.sling.api.resource.ValueMap,
                   com.day.cq.mailer.MessageGatewayService,
     com.day.cq.mailer.MessageGateway,
     org.apache.commons.mail.Email,
                   org.apache.commons.mail.SimpleEmail" %>
   <%@taglib prefix="sling"
                   uri="https://sling.apache.org/taglibs/sling/1.0" %>
   <%@taglib prefix="cq"
                   uri="https://www.day.com/taglibs/cq/1.0"
   %>
   <cq:defineObjects/>
   <sling:defineObjects/>
   <%
           String storeContent =
                       "/libs/fd/af/components/guidesubmittype/store";
           FormsHelper.runAction(storeContent, "post", resource,
                                   slingRequest, slingResponse);
    ValueMap props = ResourceUtil.getValueMap(resource);
    Email email = new SimpleEmail();
    String[] mailTo = props.get("mailto", new String[0]);
    email.setFrom((String)props.get("from"));
           for (String toAddr : mailTo) {
               email.addTo(toAddr);
      }
    email.setMsg((String)props.get("template"));
    email.setSubject((String)props.get("subject"));
    MessageGatewayService messageGatewayService =
                       sling.getService(MessageGatewayService.class);
    MessageGateway messageGateway =
                   messageGatewayService.getGateway(SimpleEmail.class);
    messageGateway.send(email);
   %>
   ```

   在自适应表单中选择操作。 该操作会发送电子邮件并存储数据。

## 将submitService属性用于自定义提交操作 {#submitservice-property}

设置自定义提交操作时，包括 `submitService` 属性，则表单会触发 [FormSubmittactionService](https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/aemds/guide/service/FormSubmitActionService.html) 提交时。 此 `FormSubmitActionService` 使用 `getServiceName` 用于检索值 `submitService` 属性。 根据 `submitService` 属性，则服务会调用相应的提交方法。 包括 `FormSubmitActionService` 至您上传到的自定义捆绑包 [!DNL AEM Forms] 服务器。

添加 `submitService` 字符串类型的属性 `sling:Folder` ，用于启用您的自定义提交操作 [!DNL Adobe Sign] 用于自适应表单。 您可以选择 **[!UICONTROL 启用Adobe Sign]** 中的选项 **[!UICONTROL 电子签名]** 设置值之后才可进行自适应表单容器属性的部分 `submitService` 自定义提交操作的属性。

<!--As a result of setting an appropriate value for the `submitService` property and enabling [!DNL Adobe Sign], you can schedule the submission of an Adaptive Form to ensure that all configured signers have taken an action on the form. [!DNL Adobe Sign] Configuration Service keeps polling [!DNL Adobe Sign] server at regular intervals to verify the status of signatures. If all the signers complete signing the form, the Submit Action service is started and the form is submitted.-->


![提交服务属性](assets/submit-service-property.png)

<!-- You can't do comments within comments, so I changed comment tags to <start-comment> <end-comment> -->

<!--
## Workflow for a Submit Action {#workflow-for-a-submit-action}

The flowchart depicts the workflow for a Submit Action that is triggered when you click the **[!UICONTROL Submit]** button in an Adaptive Form. The files in the File Attachment component are uploaded to the server, and the form data is updated with the URLs of the uploaded files. Within the client, the data is stored in the JSON format. The client sends an Ajax request to an internal servlet that massages the data you specified and returns it in the XML format. The client collates this data with action fields. It submits the data to the final servlet (Guide Submit servlet) through a Form Submit Action. Then, the servlet forwards the control to the Submit Action. The Submit Action can forward the request to a different sling resource or redirect the browser to another URL.

![Flowchart depicting the workflow for Submit Action](assets/diagram1.png)

### XML data format {#xml-data-format}

The XML data is sent to the servlet using the **`jcr:data`** request parameter. Submit Actions can access the parameter to process the data. The following code describes the format of the XML data. The fields that are bound to the Form model appear in the **`afBoundData`** section. Unbound fields appear in the `afUnoundData`section. For more information about the format of the `data.xml` file, see [Introduction to prepopulating Adaptive Form fields](prepopulate-adaptive-form-fields.md).

```xml
<?xml ?>
<afData>
<afUnboundData>
<data>
<field1>value</field2>
<repeatablePanel>
    <field2>value</field2>
</repeatablePanel>
<repeatablePanel>
    <field2>value</field2>
</repeatablePanel>
</data>
</afUnboundData>
<afBoundData>
<start comment> xml corresponding to the Form Model /XML Schema <end comment>
<start comment> </afBoundData> <end comment>
</afData>
```

### Action fields {#action-fields}

A Submit Action can add hidden input fields (using the HTML [input](https://developer.mozilla.org/en/docs/Web/HTML/Element/Input) tag) to the rendered form HTML. These hidden fields can contain values that it needs while processing form submission. When submitting the form, these field values are posted back as request parameters that the Submit Action can use during submission handling. The input fields are called action fields.

For example, a Submit Action that also captures the time taken to fill a form can add the hidden input fields `startTime` and `endTime`.

A script can supply the values of the `startTime` and `endTime` fields when the form renders and before form submission, respectively. The Submit Action script `post.jsp` can then access these fields using request parameters and compute the total time required to fill the form.

### File attachments {#file-attachments}

Submit Actions can also use the file attachments you upload using the File Attachment component. Submit Action scripts can access these files using the sling [RequestParameter API](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/request/RequestParameter.html). The [isFormField](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/request/RequestParameter.html#isFormField()) method of the API helps identify whether the request parameter is a file or a form field. You can iterate over the Request parameters in a Submit Action to identify File Attachment parameters.

The following sample code identifies the file attachments in the request. Next, it reads the data into the file using the [Get API](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/request/RequestParameter.html#get()). Finally, it creates a Document object using the data and appends it to a list.

```java
RequestParameterMap requestParameterMap = slingRequest.getRequestParameterMap();
for (Map.Entry<String, RequestParameter[]> param : requestParameterMap.entrySet()) {
    RequestParameter rpm = param.getValue()[0];
    if(!rpm.isFormField()) {
        fileAttachments.add(new Document(rpm.get()));
    }
}
```

### Forward path and Redirect URL {#forward-path-and-redirect-url}

After performing the required action, the Submit servlet forwards the request to the forward path. An action uses the setForwardPath API to set the forward path in the Guide Submit servlet.

If the action does not provide a forward path, the Submit servlet redirects the browser using the Redirect URL. The author configures the Redirect URL using the Thank You Page configuration in the Adaptive Form Edit dialog. You can also configure the Redirect URL through the Submit Action or the setRedirectUrl API in the Guide Submit servlet. You can also configure the Request parameters sent to the Redirect URL using the setRedirectParameters API in the Guide Submit servlet.

>[!NOTE]
>
>An author provides the Redirect URL (using the Thank You Page Configuration). [OOTB Submit Actions](configuring-submit-actions.md) use the Redirect URL to redirect the browser from the resource that the forward path references.
>
>You can write a custom Submit Action that forwards a request to a resource or servlet. Adobe recommends that the script that performs resource handling for the forward path redirect the request to the Redirect URL when the processing completes.

## Submit Action {#submit-action}

A Submit Action is a sling:Folder that includes the following:

* **addfields.jsp**: This script provides the action fields that are added to the HTML file during rendition. Use this script to add hidden input parameters required during submission in the post.POST.jsp script.
* **dialog.xml**: This script is similar to the CQ Component dialog. It provides configuration information that the author customizes. The fields are displayed in the Submit Actions Tab in the Adaptive Form Edit dialog when you select the Submit Action.
* **post.POST.jsp**: The Submit servlet calls this script with the data that you submit and the additional data in the previous sections. Any mention of running an action in this page implies running the post.POST.jsp script. To register the Submit Action with the Adaptive Forms to display in the Adaptive Form Edit dialog, add these properties to the sling:Folder:

    * **guideComponentType** of type String and value **fd/af/components/guidesubmittype**
    * **guideDataModel** of type String that specifies the type of Adaptive Form for which the Submit Action is applicable. **xfa** is supported for XFA-based Adaptive Forms while **xsd** is supported for XSD-based Adaptive Forms. **basic** is supported for Adaptive Forms that do not use XDP or XSD. To display the action on multiple types of Adaptive Forms, add the corresponding strings. Separate each string by a comma. For example, to make an action visible on XFA- and XSD-based Adaptive Forms, specify the values **xfa** and **xsd** respectively.

    * **jcr:description** of type String. The value of this property is displayed in the Submit Action list in the Submit Actions Tab of the Adaptive Form Edit dialog. The OOTB actions are present in the CRX repository at the location **/libs/fd/af/components/guidesubmittype**.

## Creating a custom Submit Action {#creating-a-custom-submit-action}

Perform the following steps to create a custom Submit Action that saves the data in the CRX repository and then sends you an email. The Adaptive Form contains the OOTB Submit Action Store Content (deprecated) that saves the data in the CRX repository. In addition, CQ provides a [Mail](https://www.adobe.io/experience-manager/reference-materials/6-5/javadoc/com/day/cq/mailer/package-summary.html) API that can be used to send emails. Before using the Mail API, configure the Day CQ Mail service through the system console. You can reuse the Store Content (deprecated) action to store the data in the repository. The Store Content (deprecated) action is available at the location /libs/fd/af/components/guidesubmittype/store in the CRX repository.

1. Log in to CRXDE Lite at the URL https://&lt;server&gt;:&lt;port&gt;/crx/de/index.jsp. Create a node with the property sling:Folder and name store_and_mail in the /apps/custom_submit_action folder. Create the custom_submit_action folder if it does not exist already.

   ![Screenshot depicting the creation of a node with the property sling:Folder](assets/step1.png)

1. **Provide the mandatory configuration fields.**

   Add the configuration the Store action requires. Copy the **cq:dialog** node of the Store action from /libs/fd/af/components/guidesubmittype/store to the action folder at /apps/custom_submit_action/store_and_email.

   ![Screenshot showing the copying of the dialog node to the action folder](assets/step2.png)

1. **Provide configuration fields to prompt the author for email configuration.**

   The Adaptive Form also provides an Email action that sends emails to users. Customize this action based on your requirements. Navigate to /libs/fd/af/components/guidesubmittype/email/dialog. Copy the nodes within the cq:dialog node to cq:dialog node of your Submit Action (/apps/custom_submit_action/store_and_email/dialog).

   ![Customizing the email action](assets/step3.png)

1. **Make the action available in the Adaptive Form Edit dialog.**

   Add the following properties in the store_and_email node:

    * **guideComponentType** of type **String** and value **fd/af/components/guidesubmittype**

    * **guideDataModel** of type **String** and value **xfa, xsd, basic**

    * **jcr:description** of type **String** and value **Store and Email Action**

1. Open any Adaptive Form. Click the **Edit** button next to **Start** to open the **Edit** dialog of the Adaptive Form container. The new action is displayed in the **Submit Actions** Tab. Selecting the **Store and Email Action** displays the configuration added in the dialog node.

   ![Submit Action configuration dialog](assets/store_and_email_submit_action_dialog.jpg)

1. **Use the action to complete a task.**

   Add the post.POST.jsp script to your action. (/apps/custom_submit_action/store_and_mail/).

   Run the OOTB Store action (post.POST.jsp script). Use the [FormsHelper.runAction](https://www.adobe.io/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/foundation/forms/FormsHelper.html#runAction-java.lang.String-java.lang.String-org.apache.sling.api.resource.Resource-org.apache.sling.api.SlingHttpServletRequest-org.apache.sling.api.SlingHttpServletResponse-(java.lang.String, java.lang.String, org.apache.sling.api.resource.Resource, org.apache.sling.api.SlingHttpServletRequest, org.apache.sling.api.SlingHttpServletResponse)) API that CQ provides in your code to run the Store action. Add the following code in your JSP file:

   `FormsHelper.runAction("/libs/fd/af/components/guidesubmittype/store", "post", resource, slingRequest, slingResponse);`

   To send the email, the code reads the recipient's email address from the configuration. To fetch the configuration value in the action's script, read the properties of the current resource using the following code. Similarly you can read the other configuration files.

   `ValueMap properties = ResourceUtil.getValueMap(resource);`

   `String mailTo = properties.get("mailTo");`

   Finally, use the CQ Mail API to send the email. Use the [SimpleEmail](https://commons.apache.org/proper/commons-email/apidocs/org/apache/commons/mail/SimpleEmail.html) class to create the Email Object as depicted below:

   >[!NOTE]
   >
   >Ensure that the JSP file has the name post.POST.jsp.

   ```java
   <%@include file="/libs/fd/af/components/guidesglobal.jsp" %>
   <%@page import="com.day.cq.wcm.foundation.forms.FormsHelper,
          org.apache.sling.api.resource.ResourceUtil,
          org.apache.sling.api.resource.ValueMap,
                   com.day.cq.mailer.MessageGatewayService,
     com.day.cq.mailer.MessageGateway,
     org.apache.commons.mail.Email,
                   org.apache.commons.mail.SimpleEmail" %>
   <%@taglib prefix="sling"
                   uri="https://sling.apache.org/taglibs/sling/1.0" %>
   <%@taglib prefix="cq"
                   uri="https://www.day.com/taglibs/cq/1.0"
   %>
   <cq:defineObjects/>
   <sling:defineObjects/>
   <%
           String storeContent =
                       "/libs/fd/af/components/guidesubmittype/store";
           FormsHelper.runAction(storeContent, "post", resource,
                                   slingRequest, slingResponse);
    ValueMap props = ResourceUtil.getValueMap(resource);
    Email email = new SimpleEmail();
    String[] mailTo = props.get("mailto", new String[0]);
    email.setFrom((String)props.get("from"));
           for (String toAddr : mailTo) {
               email.addTo(toAddr);
      }
    email.setMsg((String)props.get("template"));
    email.setSubject((String)props.get("subject"));
    MessageGatewayService messageGatewayService =
                       sling.getService(MessageGatewayService.class);
    MessageGateway messageGateway =
                   messageGatewayService.getGateway(SimpleEmail.class);
    messageGateway.send(email);
   %>
   ```

   Select the action in the Adaptive Form. The action sends an email and stores the data. 

-->

>[!MORELIKETHIS]
>
>* [为自适应表单配置提交操作](/help/forms/configure-submit-actions-core-components.md)