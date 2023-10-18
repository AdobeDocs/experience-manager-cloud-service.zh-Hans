---
title: 如何翻译基于核心组件的自适应表单？
description: 了解如何在AEM Forms中创建表单数据模型，使用示例数据和服务测试该模型，以及为模型配置各种选项。
feature: Adaptive Forms
exl-id: ad46bf0f-e6ec-4c52-9695-5768a9968e16
source-git-commit: 57e421a865b664c0adb7af93b33bd4b6b32049ab
workflow-type: tm+mt
source-wordcount: '896'
ht-degree: 4%

---

# 使用机器翻译或人工翻译来翻译基于核心组件的自适应表单 {#using-aem-translation-workflow-to-localize-adaptive-forms-and-document-of-record}

本地化的表单可帮助您跨地域提供更广泛的受众。 Adobe Experience Manager翻译工作流可帮助您本地化自适应Forms及其记录文档。 您可以使用 **机器翻译** 或 **人工翻译** 本地化自适应表单。

## 使用机器翻译翻译翻译自适应表单和记录文档 {#localizing-an-adaptive-form-and-document-of-record-using-machine-translation}

机器翻译服务会立即在自适应表单中翻译您的内容并 [记录文档](/help/forms/generate-document-of-record-core-components.md). AEM Formsas a Cloud Service已预配置为使用Microsoft Translator的试用版进行机器翻译。 执行以下步骤以启用自适应Forms和记录文档的机器翻译：

1. 在AEM Forms UI中，选择一个表单，然后点按 **[!UICONTROL 添加字典]** 选项。
1. 在“将字典添加到翻译项目”屏幕中，对于 **[!UICONTROL 项目]** option

   * 要创建翻译项目，请选择 **[!UICONTROL 创建新翻译项目]** 选项和 **项目标题** 字段中，指定标题。 例如，`Government Reference Site - German locale.`
   * 要向现有翻译项目添加新词典，请选择 **[!UICONTROL 添加到现有翻译项目]** 选项并选择 **[!UICONTROL 现有翻译项目]**.
1. 在 **目标语言** 字段，指定区域设置(例如， `German(de)`)。 您可以指定多个区域设置。 该表单将转换为 **目标语言** 字段。 单击&#x200B;**完成**。
1. 在“添加的词典”对话框中，单击 **打开项目**.
1. 在“项目”屏幕中，单击新创建的项目。 例如，单击 **政府参考站点 — 德语区域设置** 磁贴。
1. 在 **翻译作业** 图块，单击 ![aem62forms_downarrow](assets/aem62forms_downarrow.png) 图标，然后单击 **开始**. 图块的状态将更改为“草稿”。 翻译完成后，状态将更改为 **已批准**. 几分钟后刷新页面并验证状态。

   ![开始翻译](/help/forms/assets/adaptive-forms-core-components-start-translation.png)
1. 在状态更改为后 **已批准** 在 **翻译作业** 图块，单击 ![aem62forms_downarrow](assets/aem62forms_downarrow.png) 图标，然后单击 **完成**.

1. 要预览本地化表单，请在AEM Forms UI中选择本地化表单。 单击 **[!UICONTROL 预览]** >**[!UICONTROL HTML预览]**. 在添加 `afAcceptLang=<locale code>` 到表单的URL。 例如，添加 `afAcceptLang=de`以打开德语版窗体。


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
1. To view the localized document of record, tap Generate Preview. The document of record PDF is generated and opened in a new tab in your browser.

-->

## 使用人工翻译本地化自适应表单及其记录文档 {#localizing-an-adaptive-form-and-its-document-of-record-using-human-translation}

在人工翻译中，内容将发送给翻译提供商并由专业翻译人员进行翻译。 完成后，将返回翻译的内容并将其导入 AEM。当您的翻译提供商与 AEM 集成时，内容会在 AEM 和翻译提供商之间自动发送。

对于翻译，包含XLIFF格式文件的词典将与专业翻译人员共享。 该词典包括适用于每种区域设置的单独的XLIFF文件。 每个XLIFF文件都包含向最终用户显示的文本，以及相应本地化文本的占位符。

执行以下步骤以使用人工翻译员本地化表单及其记录文档：

1. 在AEM Forms UI中，选择一个表单，然后点按 **[!UICONTROL 添加字典]** 选项。
1. 在“将字典添加到翻译项目”屏幕中，对于 **[!UICONTROL 项目]** option

   * 要创建翻译项目，请选择 **[!UICONTROL 创建新翻译项目]** 选项和 **项目标题** 字段中，指定标题。 例如，`Government Reference Site - German locale.`
   * 要向现有翻译项目添加新词典，请选择 **[!UICONTROL 添加到现有翻译项目]** 选项并选择 **[!UICONTROL 现有翻译项目]**.
1. 在 **目标语言** 字段，指定区域设置(例如， `German(de)`)。 您可以指定多个区域设置。 该表单将转换为 **目标语言** 字段。 单击&#x200B;**完成**。
1. 在“添加的词典”对话框中，单击 **打开项目**.
1. 在“项目”屏幕中，单击新创建的项目。 例如，单击 **政府参考站点 — 德语区域设置** 磁贴。
1. 在底部 **摘要** 图块，单击 **椭圆**. 这将打开翻译项目属性屏幕。
1. 打开 **[!UICONTROL 高级]** 选项卡顶部的 **翻译项目属性** 屏幕。 对于 **[!UICONTROL 翻译字段]**，选择 **[!UICONTROL 人工翻译]**. 单击 **保存并关闭** 在屏幕顶部。
1. 在 **翻译作业** 图块，单击 ![aem62forms_downarrow](assets/aem62forms_downarrow.png) 图标，然后单击 **导出**. 在导出对话框中，单击下载导出的文件选项。 它下载一个.zip文件。
   ![导出翻译文件](/help/forms/assets/adaptive-forms-core-components-start-translation-export.png)
1. 解压缩下载的.zip文件。 提取的文件夹有两个文件：
   * translation_export_summary.xml
   * [form-files-file].xml.
1. 打开 [form-files-file].xml进行编辑。 为表单字段添加本地化的字符串和消息。 保存并关闭该文件。
1. 将translation_export_summary.xml和 [form-files-file].xml.
1. 在 **翻译作业** 图块，单击 ![aem62forms_downarrow](assets/aem62forms_downarrow.png) 图标，然后单击 **导入**. 选择包含的档案 [form-files-file].xml. 表单字段的本地化字符串和消息。

   ![导入翻译文件](/help/forms/assets/adaptive-forms-core-components-start-translation-import.png)

1. 要预览本地化表单，请在AEM Forms UI中选择本地化表单。 单击 **[!UICONTROL 预览]** >**[!UICONTROL HTML预览]**. 在添加 `afAcceptLang=<locale code>` 到表单的URL。 例如，添加 `afAcceptLang=de`以打开德语版窗体。

## 另请参阅 {#see-also}

{{see-also}}