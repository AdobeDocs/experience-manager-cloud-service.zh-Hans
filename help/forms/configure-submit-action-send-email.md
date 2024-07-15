---
Title: How to send an email on submission of an Adaptive Form?
Description: Explore the process to set up email notifications when submitting an Adaptive Form.
keywords: 如何发送自适应表单的电子邮件、电子邮件提交操作、自适应表单电子邮件、表单提交电子邮件、发送电子邮件指南
feature: Adaptive Forms, Core Components
exl-id: 70386e57-345b-4edb-97f1-3fd52ea9ff4f
title: “如何为自适应表单配置提交操作？”
role: User, Developer
source-git-commit: 2b76f1be2dda99c8638deb9633055e71312fbf1e
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 25%

---

# 为自适应表单配置“发送电子邮件”提交操作

通过&#x200B;**[!UICONTROL 发送电子邮件]**&#x200B;提交操作，您可以在成功提交表单时向一个或多个收件人发送电子邮件。 通过此提交操作，可创建包含预定义格式的表单数据的电子邮件。 例如，考虑使用以下模板，其中从提交的表单数据中检索客户名称、配送地址、州名称和邮政编码：


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
1. 从&#x200B;**[!UICONTROL 提交操作]**&#x200B;下拉列表中选择&#x200B;**[!UICONTROL 发送电子邮件]**。

   发送电子邮件的![操作配置](/help/forms/assets/send-email-action-configuration.gif)
1. 在&#x200B;**[!UICONTROL 发件人]**&#x200B;文本框中指定发件人的电子邮件ID。
1. 在&#x200B;**[!UICONTROL To]**&#x200B;文本框中添加收件人的电子邮件ID。 您可以通过单击“**[!UICONTROL 添加]**”按钮添加多个收件人。
1. [可选]通过单击&#x200B;**[!UICONTROL 添加]**&#x200B;按钮添加CC和BCC收件人。
1. 在&#x200B;**[!UICONTROL 主题]**&#x200B;文本框中指定主题行。
1. 添加电子邮件模板以配置发送电子邮件提交操作。
   * 可以使用&#x200B;**[!UICONTROL 外部模板路径]**&#x200B;选项指定保存在AEM资源中的外部电子邮件模板的路径。
   * 您还可以在&#x200B;**[!UICONTROL 电子邮件模板]**&#x200B;文本框中为表单提交添加自定义电子邮件模板。
1. [可选] **[!UICONTROL 发送电子邮件]**&#x200B;提交操作提供了将附件和[记录文档(DoR)](generate-document-of-record-core-components.md)包含在电子邮件中的选项。
1. 单击&#x200B;**[!UICONTROL 完成]**。

## 最佳实践 {#best-practices}

* 建议保持电子邮件内容简洁明了。 用户应该了解电子邮件的用途以及他们需要执行的任何操作。
* 建议所有表单字段都具有唯一的元素名称，即使它们放置在自适应表单的不同面板上也是如此。
* 在使用 AEM as a Cloud Service 时，出站电子邮件需要进行加密。默认情况下，出站电子邮件功能处于禁用状态。要激活它，请向[请求访问](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html?lang=zh-Hans#sending-email)提交支持票证。


## 相关文章

{{af-submit-action}}
