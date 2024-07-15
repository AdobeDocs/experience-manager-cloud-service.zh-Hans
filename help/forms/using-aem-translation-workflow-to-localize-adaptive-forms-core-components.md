---
title: 如何翻译基于核心组件的自适应表单？
description: 了解如何在AEM Forms中创建表单数据模型(FDM)、使用示例数据和服务测试模型以及为模型配置各种选项。
feature: Adaptive Forms, Core Components
exl-id: ad46bf0f-e6ec-4c52-9695-5768a9968e16
role: User, Developer
source-git-commit: 2b76f1be2dda99c8638deb9633055e71312fbf1e
workflow-type: tm+mt
source-wordcount: '885'
ht-degree: 4%

---

# 使用机器翻译或人工翻译来翻译基于核心组件的自适应表单 {#using-aem-translation-workflow-to-localize-adaptive-forms-and-document-of-record}

本地化的表单可帮助您跨地域提供更广泛的受众。 Adobe Experience Manager翻译工作流可帮助您本地化自适应Forms及其记录文档。 您可以使用&#x200B;**机器翻译**&#x200B;或&#x200B;**人工翻译员**&#x200B;本地化自适应表单。

## 使用机器翻译翻译翻译自适应表单和记录文档 {#localizing-an-adaptive-form-and-document-of-record-using-machine-translation}

机器翻译服务立即翻译自适应表单和[记录文档](/help/forms/generate-document-of-record-core-components.md)中的内容。 AEM Forms as a Cloud Service已预配置为使用Microsoft Translator的试用版进行机器翻译。 执行以下步骤以启用自适应Forms和记录文档的机器翻译：

1. 在AEM Forms UI上，选择一个表单，然后选择&#x200B;**[!UICONTROL 添加词典]**&#x200B;选项。
1. 在“将字典添加到翻译项目”屏幕中，对于&#x200B;**[!UICONTROL 项目]**&#x200B;选项

   * 要创建翻译项目，请选择&#x200B;**[!UICONTROL 新建翻译项目]**&#x200B;选项，然后在&#x200B;**项目标题**&#x200B;字段中指定标题。 例如，`Government Reference Site - German locale.`
   * 要向现有翻译项目添加新词典，请选择&#x200B;**[!UICONTROL 添加到现有翻译项目]**&#x200B;选项，然后选择&#x200B;**[!UICONTROL 现有翻译项目]**。
1. 在&#x200B;**目标语言**&#x200B;字段中，指定区域设置（例如，`German(de)`）。 您可以指定多个区域设置。 表单已翻译为&#x200B;**目标语言**&#x200B;字段中指定的所有区域设置。 单击&#x200B;**完成**。
1. 在“添加的词典”对话框中，单击&#x200B;**打开项目**。
1. 在“项目”屏幕中，单击已创建的项目。 例如，单击&#x200B;**政府参考站点 — 德语区域设置**&#x200B;拼贴。
1. 在&#x200B;**翻译作业**&#x200B;拼贴上，单击![aem62forms_downarrow](assets/aem62forms_downarrow.png)图标，然后单击&#x200B;**开始**。 图块的状态将更改为“草稿”。 翻译完成后，状态将更改为&#x200B;**已批准**。 几分钟后刷新页面并验证状态。

   ![开始翻译](/help/forms/assets/adaptive-forms-core-components-start-translation.png)
1. 在&#x200B;**翻译作业**&#x200B;拼贴上的状态更改为&#x200B;**已批准**&#x200B;后，单击![aem62forms_downarrow](assets/aem62forms_downarrow.png)图标，然后单击&#x200B;**完成**。

1. 要预览本地化表单，请在AEM Forms UI中选择本地化表单。 单击&#x200B;**[!UICONTROL 预览]** >**[!UICONTROL 预览为HTML]**。 将`afAcceptLang=<locale code>`添加到表单的URL后重新打开表单。 例如，添加`afAcceptLang=de`以打开表单的德语版本。


   >[!NOTE]
   >
   >* 在浏览器窗口中打开本地化的表单版本之前，请确保将浏览器的区域设置设置为与表单的区域设置相匹配。 例如，如果表单转换为德语(de)语言，则将浏览器的区域设置设置为德语(de)。
   >* 自适应表单组件不支持从右至左(RTL)语言。 例如，希伯来语。

<!-- 
   Along with the Adaptive form, the auto-generated document of record is also localized.

   For more information on Document of Record settings and configuration, see:

   [Document of Record Template](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-template-configuration-p)

   [Document of Record settings](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-settings-p)

1. [Customize the branding information of the document of record](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md) and ensure that the browser locale is set to the same language to which you have localized the Adaptive Form using machine language. The browser locale helps localize the branding information in the document of record.
1. To view the localized document of record, select Generate Preview. The document of record PDF is generated and opened in a new tab in your browser.

-->

## 使用人工翻译本地化自适应表单及其记录文档 {#localizing-an-adaptive-form-and-its-document-of-record-using-human-translation}

在人工翻译中，内容将发送给翻译提供商并由专业翻译人员进行翻译。 完成后，将返回翻译的内容并将其导入 AEM。当您的翻译提供商与 AEM 集成时，内容会在 AEM 和翻译提供商之间自动发送。

对于翻译，包含XLIFF格式文件的词典将与专业翻译人员共享。 该词典包括适用于每种区域设置的单独的XLIFF文件。 每个XLIFF文件都包含向最终用户显示的文本，以及相应本地化文本的占位符。

执行以下步骤以使用人工翻译员本地化表单及其记录文档：

1. 在AEM Forms UI上，选择一个表单，然后选择&#x200B;**[!UICONTROL 添加词典]**&#x200B;选项。
1. 在“将字典添加到翻译项目”屏幕中，对于&#x200B;**[!UICONTROL 项目]**&#x200B;选项

   * 要创建翻译项目，请选择&#x200B;**[!UICONTROL 新建翻译项目]**&#x200B;选项，然后在&#x200B;**项目标题**&#x200B;字段中指定标题。 例如，`Government Reference Site - German locale.`
   * 要向现有翻译项目添加新词典，请选择&#x200B;**[!UICONTROL 添加到现有翻译项目]**&#x200B;选项，然后选择&#x200B;**[!UICONTROL 现有翻译项目]**。
1. 在&#x200B;**目标语言**&#x200B;字段中，指定区域设置（例如，`German(de)`）。 您可以指定多个区域设置。 表单已翻译为&#x200B;**目标语言**&#x200B;字段中指定的所有区域设置。 单击&#x200B;**完成**。
1. 在“添加的词典”对话框中，单击&#x200B;**打开项目**。
1. 在“项目”屏幕中，单击已创建的项目。 例如，单击&#x200B;**政府参考站点 — 德语区域设置**&#x200B;拼贴。
1. 在&#x200B;**摘要**&#x200B;拼贴的底部，单击&#x200B;**省略号**。 这将打开翻译项目属性屏幕。
1. 打开&#x200B;**翻译项目属性**&#x200B;屏幕顶部的&#x200B;**[!UICONTROL 高级]**&#x200B;选项卡。 对于&#x200B;**[!UICONTROL 翻译字段]**，请选择&#x200B;**[!UICONTROL 人工翻译]**。 单击屏幕顶部的&#x200B;**保存并关闭**。
1. 在&#x200B;**翻译作业**&#x200B;拼贴上，单击![aem62forms_downarrow](assets/aem62forms_downarrow.png)图标，然后单击&#x200B;**导出**。 在导出对话框中，单击下载导出的文件选项。 它下载一个.zip文件。
   ![导出翻译文件](/help/forms/assets/adaptive-forms-core-components-start-translation-export.png)
1. 解压缩下载的.zip文件。 提取的文件夹有两个文件：
   * translation_export_summary.xml
   * [form-fields-file].xml。
1. 打开[form-fields-file].xml进行编辑。 为表单字段添加本地化的字符串和消息。 保存并关闭该文件。
1. 将translation_export_summary.xml和[form-fields-file].xml压缩文件。
1. 在&#x200B;**翻译作业**&#x200B;拼贴上，单击![aem62forms_downarrow](assets/aem62forms_downarrow.png)图标，然后单击&#x200B;**导入**。 选择包含[form-fields-file].xml的存档。 表单字段的本地化字符串和消息。

   ![导入翻译文件](/help/forms/assets/adaptive-forms-core-components-start-translation-import.png)

1. 要预览本地化表单，请在AEM Forms UI中选择本地化表单。 单击&#x200B;**[!UICONTROL 预览]** >**[!UICONTROL 预览为HTML]**。 将`afAcceptLang=<locale code>`添加到表单的URL后重新打开表单。 例如，添加`afAcceptLang=de`以打开表单的德语版本。

## 另请参阅 {#see-also}

{{see-also}}