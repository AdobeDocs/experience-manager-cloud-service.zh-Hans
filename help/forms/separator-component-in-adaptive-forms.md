---
title: Adaptive Forms中的分隔符號元件
seo-title: Separator component in Adaptive Forms
description: 您可以使用分隔符號元件以視覺化方式分隔表單的區段。
seo-description: You can use the separator component to visually segregate sections of a form.
uuid: f8d2aed3-52aa-437f-bfe3-0c8779e7986c
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: a8aa77fe-5880-4c4e-9e1b-3c5a8772c29d
docset: aem65
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 0%

---


# Adaptive Forms中的分隔符號元件{#separator-component-in-adaptive-forms}

您可以使用分隔符號元件，以視覺方式分隔表單的面板。 您可以指定分隔符號元件的下列屬性，以定義分隔符號元件的整體外觀和樣式：

* **元素名稱：** 指定元件的名稱。 SOM運算式會使用「元素名稱」欄位中指定的值來處理元件。
* **粗細：** 指定分隔符號元件的粗細（畫素）。

* **CSS類別：** 指定分隔符號元件的自訂CSS類別

* **內嵌樣式：** 替換為 [!DNL AEM Forms]，您現在可以套用內嵌CSS樣式至個別的最適化表單元件，並即時預覽變更。

您可以使用「版面」模式來定義分隔符號元件跨越的欄數。 如需詳細資訊，請參閱 [使用版面模式調整元件大小](resize-using-layout-mode.md).

若要指定分隔符號元件的屬性：

1. 選取分隔符號元件並點選 ![cmppr](assets/cmppr.png). 屬性會在側欄中開啟。
1. 按一下「內嵌CSS屬性」區段中的索引標籤以指定CSS屬性。 例如： a.在「欄位」標籤中，按一下 **新增專案**. 會新增包含兩個欄位的列。
1. 在左側的第一個欄位中，指定要套用的CSS3屬性。 例如， **邊框**. 您也可以按一下向下箭頭按鈕來選取屬性。 下拉式清單並非詳盡無遺，您可以在此欄位中指定任何支援的CSS3屬性名稱。
1. 在相鄰的欄位中，指定指定CSS3屬性的有效值。 例如， **3px實心黑色**.
1. 按一下 **新增專案** 以指定另一個屬性及其值。
1. 按一下 **預覽** 以預覽表單中的變更。
1. 按一下 **確定** 確認變更或 **取消** 結束對話方塊而不進行任何變更。

