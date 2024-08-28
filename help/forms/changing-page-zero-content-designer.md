---
title: 如何在Designer中更改零页面内容？
description: 更改在非Adobe PDF查看器的XFAPDF的第0页上显示的消息。
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
feature: Adaptive Forms
role: User
source-git-commit: 937bd4653e454beea3111cfc7ef7b4bbc1ace193
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 0%

---


# 在Designer中更改零页内容 {#changing-page-zero-content-in-designer}

如果非Adobe PDF查看器(如[!DNL Chrome]或[!DNL Firefox]中的默认PDF查看器)无法读取PDF/XFA表单的内容，则默认显示“零页”内容。 默认的Page Zero消息如下所示。

![defaultpage0message](assets/defaultpage0message.png)

[!DNL AEM Forms]版本的Designer允许您更改在第0页上显示的消息。 要更改Page Zero消息，请执行以下步骤：

1. 确保您已安装[!DNL AEM Forms]版本的Designer。 您可以从设计器的“关于”屏幕中检查版本。

1. 打开要为其更改“页面零”内容的表单。

1. 单击&#x200B;**[!UICONTROL 文件]** > **[!UICONTROL 表单属性]**。

1. 在[!UICONTROL 表单属性]对话框中，单击![加号](assets/plus.png)（加号图标）以添加自定义属性。

1. 将&#x200B;**_pagezerocontent**&#x200B;指定为属性的名称。
1. 以富文本格式添加新的“页面零”消息作为值。 例如：


   `<body xmlns="https://www.w3.org/1999/xhtml" xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/"><p style="font-family:'Times';font-size:12pt;letter-spacing:0in"><span style="xfa-spacerun:yes"> </code></p><p style="font-family:'Times';font-size:12pt;letter-spacing:0in">You are seeing this message maybe because you are using a non Adobe PDF Viewer or an Old version of Adobe Reader. You can upgrade to the latest version of Adobe Reader for Windows, Mac, or Linux by visiting <span style="xfa-spacerun:yes"> </code>https://www.adobe.com/go/reader_download.</p><p style="font-family:'Times';font-size:12pt;letter-spacing:0in"><span style="xfa-spacerun:yes"> </code></p><p style="font-family:'Times';font-size:12pt;letter-spacing:0in">For more assistance with Adobe Reader visit <span style="xfa-spacerun:yes"> </code>https://www.adobe.com/go/acrreader.</p></body>`

1. 将表单另存为PDF。

1. 在浏览器中查看PDF表单，确认消息已更新。 上面的示例值如下所示：

   ![changedmessage](assets/changedmessage.png)

>[!NOTE]
>
>重新打开表单时，您创建的自定义属性可能无法正确显示在表单属性对话框中。 但是，它可正常使用，并且表单会显示更新的零页消息。

>[!MORELIKETHIS]
>
>* [下载并安装Forms Designer以创建记录文档模板](/help/forms/installing-configuring-designer.md)
>* [使用Forms Designer创建记录文档(DoR)模板和表单片段？](/help/forms/use-forms-designer.md)
