---
title: 翻译和本地化 AEM Forms Edge Delivery ServicesForm
description: 翻译和本地化 AEM Forms Edge Delivery ServicesForm
feature: Edge Delivery Services
hide: true
hidefromtoc: true
exl-id: 8a0c826f-8acc-4a00-bd84-7b0df9a82457
source-git-commit: eadfc3d448bd2fadce08864ab65da273103a6212
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 6%

---


# 翻译和本地化 AEM Forms Edge Delivery ServicesForm

在Edge Delivery Services中，表单翻译涉及将表单内容从一种语言转换为另一种语言，侧重于准确性、清晰度和一致性。 翻译或本地化的表单使不同地理位置的受众覆盖面更广，从而增强用户体验并促进不同语言偏好之间的更好沟通。


在文章结束时，您将学习：

* [在Google Drive中翻译表单](#translate-form-google-drive)
* [在SharePoint站点中翻译表单](#translate-form-sharepoint)

## 在Google Drive中翻译表单 {#translate-form-google-drive}

此 `GOOGLETRANSLATE` Google工作表中的功能通过点按内置翻译工具来翻译表单，并直接在Google工作表中将文本从一种语言更改为另一种语言。 要在Google Drive中翻译表单，请执行以下操作：

1. 转到Google驱动器上的AEM项目文件夹，然后打开Google工作表。
2. 重命名现有工作表(`shared-default`)到 `shared-en`.
3. 添加名为的工作表 `shared-default`. 此 `shared-default` 工作表包含用于本地化为特定语言的内容。
4. 在中添加本地化的内容 `shared-default` 工作表使用 `GOOGLETRANSLATE` 函数。
您可以使用公式从以下位置翻译单元格D2的内容 `shared-en` 在中转换为法语 `shared-default` 工作表。 以下是要使用的公式：
   `=GOOGLETRANSLATE('shared-en'!D2,"en","fr")`

   ![Enquiry Translate电子表格](/help/forms/assets/translate-enquiry-spreadsheet.png)

5. 预览和发布工作表，使用 [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content).

您可参阅 [电子表格](/help/forms/assets/enquirytranslate.xlsx) 包含的表单定义 `enquiry` 表单已从英语翻译为法语。

![查询已翻译表单](/help/forms/assets/translate-form-french.png)

请参阅以下URL，您可以在其中查看带有法语翻译的表单：https://main--portal--wkndforms.hlx.live/enquirytranslate

## 在SharePoint站点中翻译表单{#translate-form-sharepoint}

要翻译Microsoft® SharePoint网站上的表单，您需要使用任何翻译服务手动更改字段的标签。 要在SharePoint站点中翻译表单，请执行以下操作：

1. 转到Microsoft® SharePoint上的AEM项目文件夹，然后打开电子表格。
2. 重命名现有工作表(`shared-default`)到 `shared-en`.
3. 添加名为的工作表 `shared-default`. 此 `shared-default` 工作表包含用于本地化为特定语言的内容。
4. 在中添加本地化的内容 `shared-default` 手动工作表。

   ![Enquiry Translate电子表格](/help/forms/assets/translate-enquiry-sp-spreadsheet.png)

5. 预览和发布工作表，使用 [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content).

请参阅 [电子表格](/help/forms/assets/enquirytranslate-sp.xlsx) 包含的表单定义 `enquiry` 表单已从英语翻译为法语。

![查询已翻译表单](/help/forms/assets/translate-form-french.png)

请参阅以下URL，您可以在其中查看带有法语翻译的表单：https://main--wefinance--wkndforms.hlx.live/enquirytranslate

## 已知问题 {#known-issues}

* 表单的标签将翻译为 `shared-default` 工作表中，但错误消息以浏览器的默认语言显示。

  ![错误消息](/help/forms/assets/translate-error-message.png)

* 打开日历时，日历下拉列表将以浏览器的默认语言显示。

  ![错误消息](/help/forms/assets/translate-calender-display.png)


## 常见问题解答 {#faq}

**Q**：如何在表单中以指定的本地化语言键入输入？

**A**：要使用特定的本地化语言输入文本，请调整设备上的键盘设置。 有关如何执行此操作的说明，请参阅以下链接：

* [设置您的Mac以使用其他语言进行输入](https://support.apple.com/en-in/guide/mac-help/mchlp1406/mac)
* [设置Windows以使用其他语言进行输入](https://support.microsoft.com/en-us/windows/manage-the-input-and-display-language-settings-in-windows-12a10cb4-8626-9b77-0ccb-5013e0c7c7a2#:~:text=Select%20the%20Start%20%3E%20Settings%20%3E%20Time,you%20want%2C%20then%20select%20Options)
* [设置Android或iPhone/iPad以使用其他语言进行输入](https://support.google.com/gboard/answer/7068494?hl=en&amp;co=GENIE.Platform%3DAndroid)


**Q**：如何检索中使用的区域设置列表 `GOOGLETRANSLATE` 函数？

**A**：您可以参阅 [Google的官方文档](https://cloud.google.com/translate/docs/languages) 获取GOOGLE TRANSLATE中使用的区域设置的完整列表。

## 另请参阅

{{see-more-forms-eds}}

