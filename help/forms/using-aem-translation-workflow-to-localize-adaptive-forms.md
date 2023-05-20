---
title: 使用AEM翻譯工作流程將最適化Forms和記錄檔案本地化
seo-title: Using AEM translation workflow to localize Adaptive Forms and Document of Record
description: 瞭解如何使用AEM翻譯工作流程將Adaptive Forms和記錄檔案本地化。
seo-description: Learn to use AEM translation workflows to localize Adaptive Forms and Document of Record.
uuid: 6c87a283-0203-4cf7-989a-3770ddbbbd6e
content-type: reference
topic-tags: develop
discoiquuid: f5642571-9657-4ca1-93c5-4ae2eb91e967
noindex: true
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 1%

---


# 使用AEM翻譯工作流程將最適化Forms和記錄檔案本地化 {#using-aem-translation-workflow-to-localize-adaptive-forms-and-document-of-record}

本地化的表單可協助您跨地理區域提供更廣泛的受眾。 Adobe Experience Manager翻譯工作流程可協助您將Adaptive Forms及其記錄檔案本地化。 您可以使用 **機器翻譯** 或 **人工翻譯** 將最適化表單本地化。

本文說明搭配最適化Forms和記錄檔案使用AEM翻譯工作流程的流程。

## 使用機器翻譯將最適化表單和記錄檔案當地語系化 {#localizing-an-adaptive-form-and-document-of-record-using-machine-translation}

機器翻譯服務會立即翻譯最適化表單和記錄檔案中的內容。 [!DNL AEM Forms] 已預先設定為使用試用版 [!DNL Microsoft Translator] （機器翻譯）。 執行以下步驟來啟用最適化Forms和記錄檔案的機器翻譯：

1. 於 [!DNL AEM Forms] UI，選取表單，然後點選 **新增字典** 選項。
1. 在 **新增字典至翻譯專案** 熒幕中，選取 **建立新的翻譯專案** 或 **新增至現有翻譯專案** 選項。
1. 在 **專案標題** 欄位中，指定標題。 例如，`Government Reference Site - German locale.`
1. 在 **目標語言** 欄位，指定地區設定(例如， `German(de)`)，然後按一下 **完成**. 您可以指定多個地區設定。 表單已轉譯為 **目標語言** 欄位。
1. 在「新增的字典」對話方塊中，按一下 **開啟專案**. 在「專案」畫面中，開啟新建立的專案。
1. 按一下 **橢圓** 在底部 **翻譯摘要** 圖磚。 「翻譯摘要」畫面隨即開啟。
1. 按一下 **編輯** 圖示於 **翻譯摘要** 畫面。 開啟 **翻譯** 標籤並選取中的機器翻譯 **翻譯方法** 畫面。 選取適當的 **翻譯提供者** 和 **雲端設定**. 按一下 **完成** 圖示加以檢視。
1. 於 **翻譯工作** 圖磚，按一下 ![aem62forms_downarrow](assets/aem62forms_downarrow.png) 圖示，然後按一下 **開始**. 圖磚的狀態會變更為「草稿」。 翻譯完成後，狀態會變更為 **準備好審查**. 幾分鐘後重新整理頁面並驗證狀態。
1. 在狀態變更為 **準備好審查** 於 **翻譯工作** 圖磚，在瀏覽器視窗中開啟表單。 此時會顯示表單的當地語系化版本。

   >[!NOTE]
   >
   >* 在瀏覽器視窗中開啟表單的當地語系化版本之前，請確定瀏覽器的地區設定已設定為符合表單的地區設定。 例如，如果表單已翻譯成德文(de)語言，則將瀏覽器的地區設定設為德文(de)。
   >* 最適化表單元件不支援由右至左(RTL)語言。 例如，希伯來文。


   除了最適化表單之外，自動產生的記錄檔案也會翻譯。

   如需記錄檔案設定和組態的詳細資訊，請參閱：

[记录文档模板配置](generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-template-configuration-p)

[記錄檔案設定](generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-settings-p)

1. [自訂記錄檔案的品牌資訊](generate-document-of-record-for-non-xfa-based-adaptive-forms.md) 並確保瀏覽器地區設定與您使用機器語言將最適化表單本地化的語言設定相同。 瀏覽器地區設定有助於記錄檔案中的品牌資訊本地化。
1. 若要檢視當地語系化的記錄檔案，請點選「產生預覽」。 記錄檔案PDF會產生，並在瀏覽器的新索引標籤中開啟。

<!-- ## Localizing an Adaptive Form and its Document of Record using Human Translation {#localizing-an-adaptive-form-and-its-document-of-record-using-human-translation}

In Human translation the content is sent to a translation provider and translated by professional translators. When complete, the translated content is returned and imported into AEM. When your translation provider is integrated with AEM, content is automatically sent between AEM and the translation provider.

For translation, a dictionary containing files in XLIFF format is shared with the professional translators. The dictionary includes a separate XLIFF file for each locale. Each XLIFF file contains text that will be displayed to the end users and placeholders for the corresponding localized text.

Perform the following steps to localize a form and its Document of Record using Human Translators:

1. [Connect AEM with your translation service provider](/help/sites-administering/tc-tic.md) and [create translation integration framework configurations](/help/sites-administering/tc-tic.md).

1. [Associate the pages of your language master](/help/sites-administering/tc-tic.md) with the translation service and framework configurations.

1. [Identify the type of content](/help/sites-administering/tc-rules.md) to translate.

1. [Prepare the content for translation](/help/sites-administering/tc-prep.md) by authoring the language master and creating the root pages of language copies.

1. [Create translation projects](/help/sites-administering/tc-manage.md) to gather the content to translate and to prepare the translation process.

1. Use the translation projects to [manage the content translation process](/help/sites-administering/tc-manage.md).

>[!NOTE]
>
>* Adaptive Form components do not support right to left (RTL) languages. For example, Hebrew.
> -->

