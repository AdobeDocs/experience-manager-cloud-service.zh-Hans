---
title: 使用元件的最佳作法
seo-title: Best practices for working with components
description: 使用最適化表單元件時應記住的一些最佳實務和要點
seo-description: Some best practices and key points to remember when working with Adaptive Form components
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 1%

---


# 使用元件的最佳作法{#best-practices-for-working-with-components}

使用最適化表單元件時，請謹記以下最佳作法和要點：

* 每個元件都有相關的屬性，這些屬性控制其外觀和功能。 若要設定元件的屬性，請點選元件並點選 ![屬性](assets/Smock_Wrench_18_N.svg) 以在「屬性」瀏覽器中開啟元件屬性。
* 元件以其元素名稱識別。 點選時 ![屬性](assets/Smock_Wrench_18_N.svg)，您可以透過變更元件名稱來變更元件 **[!UICONTROL 元素名稱]** 屬性瀏覽器中的欄位值。 「元素名稱」欄位僅接受字母、數字、連字型大小(-)和底線(_)。 不允許使用其他特殊字元，元素名稱應以字母開頭。

* 只要表單上有顯示標題，您就可以在表單編輯器中內嵌修改最適化表單元件的Title屬性，而無需開啟Properties瀏覽器。 若要這麼做：

   1. 點選以選取具有 **[!UICONTROL 標題]** 屬性及其 **[!UICONTROL 隱藏標題]** 屬性已停用。

   1. 點選 ![編輯圖示](assets/Smock_Edit_18_N.svg) 讓標題可編輯。

   1. 修改標題並點選Return鍵，或點選元件之外的任意位置以儲存變更。 點選Esc鍵以捨棄變更。

* 電子郵件和電話等部分最適化表單元件包含現成可用的驗證模式。 不過，您可以更新 **[!UICONTROL 驗證模式]** 元件屬性中「模式」摺疊式功能表下的欄位。 請參閱上表中的「元件說明」，以取得預設驗證的詳細資訊。

* 最適化Forms欄位（例如數值方塊和電子郵件）可以設定為包含專門的HTML5輸入型別。 當這些欄位成為行動裝置和平板電腦上的焦點時，鍵盤會預先顯示特定字母、數字和字元，這些通常用於欄位中的輸入資訊。 它可協助使用者快速輸入資訊，而不需在鍵盤上的字元組之間切換。 若要允許專門輸入元件，請啟用 **[!UICONTROL 使用HTML型別編號]** 核取方塊。

* 您可以启用文本框组件以接受富文本。若要為文字方塊啟用RTF文字，請啟用 **[!UICONTROL 允許RTF文字]** 元件屬性中的核取方塊。

* 您可以啟用「文字方塊」、「電子郵件」和「電話」元件，以自動填寫名稱、地址、信用卡、電話和電子郵件等欄位值，這些值來自瀏覽器自動填寫設定中儲存的資訊。 若要啟用此功能，請選取 **[!UICONTROL 啟用自動填寫]** 在元件屬性中並選取 **[!UICONTROL 自動填寫屬性]**. 當使用者填寫最適化表單時，會根據瀏覽器中自動填寫設定檔的值或使用者先前填寫的值來建議值。 請注意，如果使用者瀏覽器中的自動填寫設定已開啟，自動填寫即可運作。

* 指定選項按鈕和核取方塊專案的值 `{value}={text}` 元件屬性中的格式。
* 依預設，檔案附件元件僅允許使用者附加一個檔案。 不過，您可以設定元件屬性以支援多個附件。 此外，如果使用者使用相同的檔案名稱附加多個檔案，附件可能會導致一些問題。 因此，建議您在提交表單時，為每個已提交的附件建立唯一識別碼的關聯。 若要這麼做：

   1. 在您的 [!DNL AEM Forms] 伺服器，導覽至 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL 工具]** > **[!UICONTROL 作業]** > **[!UICONTROL 網頁主控台]**.
   1. 尋找並點選 **[!UICONTROL 最適化Forms設定服務]**.
   1. 在最適化Forms設定服務對話方塊中，啟用 **[!UICONTROL 將檔案名稱設為唯一]**. 預設為停用。

* 若要讓使用者能使用Safari瀏覽器附加PDF，請確定 **application/pdf** 會新增至「檔案」附件元件的「支援的檔案型別」屬性。 使用先前建立的最適化Forms [!DNL AEM Forms] 版本可能包含 **.pdf** 而非 **application/pdf** （在支援的檔案型別屬性中）。

>[!NOTE]
>
>最適化表單元件不支援由右至左(RTL)語言。 例如，希伯來文。