---
Title: How to send an email on submission of an Adaptive Form?
Description: Explore the process to set up email notifications when submitting an Adaptive Form.
keywords: 如何发送自适应表单的电子邮件、电子邮件提交操作、自适应表单电子邮件、表单提交电子邮件、发送电子邮件指南
feature: Adaptive Forms, Core Components
source-git-commit: f1db04e6cd1f78c1530aefd29f5f036ca5e70873
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 24%

---


# 为自适应表单配置“发送电子邮件提交”操作

此 **[!UICONTROL 发送电子邮件]** 提交操作允许您在成功提交表单后向一个或多个收件人发送电子邮件。 通过此提交操作，可创建包含预定义格式的表单数据的电子邮件。 例如，考虑使用以下模板，其中从提交的表单数据中检索客户名称、配送地址、州名称和邮政编码：


    ```
    ${customer_Name}，您好！
    
    以下内容设定为您的默认配送地址：
    ${customer_Name}，
    ${customer_Shipping_Address}，
    ${customer_State}，
    ${customer_ZIPCode}
    
    此致，
    WKND
    
    ```


## 优点

使用“发送电子邮件”提交操作配置自适应表单的一些优点包括：

* 它支持快速通信，因为表单数据会直接发送到指定的电子邮件收件人。
* 它有助于通过将表单提交直接集成到电子邮件通知中来简化工作流。
* 它有助于组织自定义电子邮件内容，使其适合特定的通信需求。

## 配置发送电子邮件提交操作 {#steps-to-configure-send-email-submit-action}

要配置提交操作：

1. 打开内容浏览器，然后选择自适应表单的&#x200B;**[!UICONTROL 指南容器]**&#x200B;组件。
1. 单击指南容器属性![指南属性](/help/forms/assets/configure-icon.svg)图标。这将打开“自适应表单容器”对话框。
1. 单击&#x200B;**[!UICONTROL 提交]**&#x200B;选项卡。
1. 从 **[!UICONTROL 提交操作]** 下拉列表，选择 **[!UICONTROL 发送电子邮件]**.

   ![发送电子邮件的操作配置](/help/forms/assets/send-email-action-configuration.gif)
1. 在中指定发件人的电子邮件ID **[!UICONTROL 从]** 文本框。
1. 在中添加收件人的电子邮件ID **[!UICONTROL 至]** 文本框。 您可以通过单击 **[!UICONTROL 添加]** 按钮。
1. [可选] 通过单击 **[!UICONTROL 添加]** 按钮。
1. 在中指定主题行 **[!UICONTROL 主题]** 文本框。
1. 添加电子邮件模板以配置发送电子邮件提交操作。
   * 您可以使用来指定保存在AEM资源中的外部电子邮件模板的路径 **[!UICONTROL 外部模板路径]** 选项。
   * 您还可以在以下位置为表单提交添加自定义电子邮件模板 **[!UICONTROL 电子邮件模板]** 文本框。
1. [可选] 此 **[!UICONTROL 发送电子邮件]** 提交操作提供包括附件和 [记录文档(DoR)](generate-document-of-record-core-components.md) 使用电子邮件。
1. 单击&#x200B;**[!UICONTROL 完成]**。

## 最佳实践 {#best-practices}

* 建议保持电子邮件内容简洁明了。 用户应该了解电子邮件的用途以及他们需要执行的任何操作。
* 建议所有表单字段都具有唯一的元素名称，即使它们放置在自适应表单的不同面板上也是如此。
* 在使用 AEM as a Cloud Service 时，出站电子邮件需要进行加密。默认情况下，出站电子邮件功能处于禁用状态。要激活它，请将支持票证提交到 [请求访问](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html?lang=zh-Hans#sending-email).


## 相关文章

{{af-submit-action}}


