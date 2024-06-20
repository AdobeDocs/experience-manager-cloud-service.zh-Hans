---
title: 翻译和本地化 AEM Forms Edge Delivery ServicesForm
description: 翻译和本地化 AEM Forms Edge Delivery ServicesForm
feature: Edge Delivery Services
hide: true
hidefromtoc: true
exl-id: 8a0c826f-8acc-4a00-bd84-7b0df9a82457
role: Admin, Architect, Developer
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 100%

---


# 翻译和本地化 AEM Forms Edge Delivery ServicesForm

在 Edge Delivery Services 中，表格翻译涉及将表格内容从一种语言转换为另一种语言，重点关注准确性、清晰度和一致性。翻译或本地化的形式能够覆盖不同地理位置的更广泛受众，从而提升用户体验并促进不同语言偏好之间的更好沟通。


在本文结束时，您将学会：

* [在 Google Drive 内翻译表格](#translate-form-google-drive)
* [在 SharePoint Site 内翻译表格](#translate-form-sharepoint)

## 在 Google Drive 内翻译表格 {#translate-form-google-drive}

Google 表单的 `GOOGLETRANSLATE` 功能通过利用内置翻译工具来翻译表格，直接在 Google 工作表中将文本从一种语言更改为另一种语言。在 Google Drive 内翻译表格：

1. 转到 Google Drive 上的 AEM Project 文件夹并打开 Google 表。
2. 将现有工作表（`shared-default`）重命名为 `shared-en`。
3. 添加一个名为 `shared-default`的工作表。`shared-default` 表包含本地化为特定语言的内容。
4. 使用 `shared-default` 函数在 `GOOGLETRANSLATE` 工作表中添加本地化内容。
您可以使用公式将 `shared-en` 工作表中单元格 D2 的内容翻译为 `shared-default` 工作表中的法语。以下是使用的公式：
   `=GOOGLETRANSLATE('shared-en'!D2,"en","fr")`

   ![Enquiry Translate 电子表格](/help/forms/assets/translate-enquiry-spreadsheet.png)

5. 使用 [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content)预览和发布工作表。

您可以参考 [电子表格](/help/forms/assets/enquirytranslate.xlsx)，其中包含 `enquiry` 从英语翻译成法语的表单定义。

![Enquiry Translated Form](/help/forms/assets/translate-form-french.png)

请参阅下面的 URL，您可以在那里查看带有法语翻译的表格：
https://main--portal--wkndforms.hlx.live/enquirytranslate

## 在 SharePoint Site 内翻译表格{#translate-form-sharepoint}

要翻译 Microsoft® SharePoint 网站上的表格，您需要使用任何翻译服务手动更改字段的标签。在 SharePoint Site 内翻译表格：

1. 转到 Microsoft® SharePoint 上的 AEM Project 文件夹并打开电子表格。
2. 将现有工作表（`shared-default`）重命名为 `shared-en`。
3. 添加一个名为 `shared-default`的工作表。`shared-default` 表包含本地化为特定语言的内容。
4. 手动在 `shared-default` 表中添加本地化内容。

   ![Enquiry Translate 电子表格](/help/forms/assets/translate-enquiry-sp-spreadsheet.png)

5. 使用 [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content)预览和发布工作表。

请参考包含 `enquiry` 从英语翻译成法语的表单定义的 [电子表格](/help/forms/assets/enquirytranslate-sp.xlsx)。

![Enquiry Translated Form](/help/forms/assets/translate-form-french.png)

请参阅下面的 URL，您可以在那里查看带有法语翻译的表格：
https://main--wefinance--wkndforms.hlx.live/enquirytranslate

## 已知问题 {#known-issues}

* 表单的标签被翻译成 `shared-default` 表中指定的本地化语言，但错误消息以浏览器的默认语言显示。

  ![错误消息](/help/forms/assets/translate-error-message.png)

* 当您打开日程表时，日程表下拉菜单会以浏览器的默认语言显示。

  ![错误消息](/help/forms/assets/translate-calender-display.png)


## 常见问题解答 {#faq}

**问**：如何在表单中输入指定的本地化语言？

**答**：要以特定的本地化语言输入文本，请调整设备上的键盘设置。请参阅以下链接以获取有关如何操作的说明：

* [设置你的 Mac 以接受其他语言的输入](https://support.apple.com/en-in/guide/mac-help/mchlp1406/mac)
* [设置你的 Windows 以接受其他语言的输入](https://support.microsoft.com/en-us/windows/manage-the-input-and-display-language-settings-in-windows-12a10cb4-8626-9b77-0ccb-5013e0c7c7a2#:~:text=选%20择%20开始%20%3E%20设置%20%3E%20想要的%20时间，%2C%20然后%20选择%20选项)
* [设置你的 Android 或 iPhone/iPad 以接受其他语言的输入](https://support.google.com/gboard/answer/7068494?hl=en&amp;co=GENIE.Platform%3DAndroid)


**问**：如何检索 `GOOGLETRANSLATE` 函数中使用的区域设置列表

**答**：您可以参考 [ Google 的官方文档](https://cloud.google.com/translate/docs/languages) 获得 GOOGLETRANSLATE 中使用的语言环境的完整列表。

## 另请参阅

{{see-more-forms-eds}}

