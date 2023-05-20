---
title: 修饰标记
description: 呈现网页中的组件后，可以生成一个 HTML 元素，以将呈现的组件封装在其中。对于开发人员而言，AEM 可提供清晰而简单的逻辑来控制用于封装所包含组件的修饰标记。
exl-id: a90fd619-eff6-466f-9178-90374f988b5d
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '789'
ht-degree: 10%

---

# 修饰标记 {#decoration-tag}

呈现网页中的组件后，可以生成一个 HTML 元素，以将呈现的组件封装在其中。這主要有兩個用途：

* 元件必須以HTML元素包住，才能進行編輯。
* 包裝元素是用來套用HTML類別，可提供：
   * 版面資訊
   * 樣式資訊

对于开发人员而言，AEM 可提供清晰而简单的逻辑来控制用于封装所包含组件的修饰标记。裝飾標籤是否及如何呈現取決於兩個因素的組合，此頁面將深入探討這兩個因素：

* 元件本身可使用一組屬性來設定其裝飾標籤。
* 包含元件的指令碼可使用包含引數來定義裝飾標籤的方面。

## 推荐 {#recommendations}

以下為何時包含包裝函式元素的一般建議，可協助避免發生非預期的問題：

* WCMModes （編輯或預覽模式）、例項（製作或發佈）或環境（測試或生產）之間不存在包裝函式元素，因此頁面的CSS和JavaScripts在所有情況下皆相同運作。
* 應將此包裝函式元素新增至所有可編輯的元件，讓頁面編輯器可以正確初始化及更新這些元件。
* 對於不可編輯的元件，如果包裝函式元素沒有特定功能，則可以避免，這樣產生的標籤就不會不必要地膨脹。

## 元件控制項 {#component-controls}

可將下列屬性和節點套用至元件，以控制其裝飾標籤的行為：

* **`cq:noDecoration {boolean}`：** 此屬性可以新增至元件，true值會強制AEM不在元件上產生任何包裝函式元素。
* **`cq:htmlTag`節點：** 此節點可新增至元件下，並可擁有下列屬性：
   * **`cq:tagName {String}`：** 這可用來指定用於包住元件的自訂HTML標籤，而非預設DIV元素。
   * **`class {String}`：** 這可用來指定要新增至包裝函式的css類別名稱。
   * 其他屬性名稱將會新增為HTML屬性，其字串值與提供的值相同。

## 指令碼控制項 {#script-controls}

一般而言，HTL中的包裝函式行為可歸納如下：

* 預設不會轉譯任何包裝函式DIV (僅在執行 `data-sly-resource="foo"`)。
* 所有wcm模式（已停用、預覽、編輯作者和發佈）的轉譯方式相同。

您也可以完全控制包裝函式的行為。

* HTL指令碼可完全控制包裝函式標籤的結果行為。
* 元件屬性(類似 `cq:noDecoration` 和 `cq:tagName`)也可以定義包裝函式標籤。

您可以從HTL指令碼及其相關邏輯完全控制包裝函式標籤的行為。

如需有關在HTL中進行開發的進一步資訊，請參閱 [HTL檔案](https://experienceleague.adobe.com/docs/experience-manager-htl/using/overview.html?lang=zh-Hans).

### 決策樹 {#decision-tree}

此決策樹會總結決定包裝函式標籤行為的邏輯。

![決策樹](assets/decoration-tag-decision-tree.png)

### 使用案例 {#use-cases}

以下三個使用案例提供如何處理包裝函式標籤的範例，並說明控制包裝函式標籤的所需行為是何等簡單。

以下所有範例都假設下列內容結構和元件：

```
/content/test/
  @resourceType = "test/components/one"
  child/
    @resourceType = "test/components/two"
```

```
/apps/test/components/
  one/
    one.html
  two/
    two.html
    cq:htmlTag/
      @cq:tagName = "article"
      @class = "component-two"
```

#### 使用案例1：包含程式碼重複使用的元件 {#use-case-include-a-component-for-code-reuse}

最典型的使用案例是當一個元件包含另一個元件來重複使用程式碼時。 在這種情況下，包含的元件不需要使用其本身的工具列和對話方塊進行編輯，因此不需要包裝函式，以及元件的 `cq:htmlTag` 將被忽略。 這可以視為預設行為。

`one.html: <sly data-sly-resource="child"></sly>`

`two.html: Hello World!`

產生的輸出於 `/content/test.html`：

**`Hello World!`**

例如，包含核心影像元件的元件會顯示影像，且通常會使用合成資源來顯示，這包括透過將代表元件所具有之所有屬性的Map物件傳遞至data-sly-resource來包含虛擬子元件。

#### 使用案例2：包含可編輯的元件 {#use-case-include-an-editable-component}

另一個常見的使用案例是容器元件包含可編輯的子元件，例如版面配置容器。 在這種情況下，每個包含的子項都需要包裝函式才能讓編輯器運作(除非明確透過 `cq:noDecoration` 屬性)。

由於包含的元件在此情況下是獨立元件，因此它需要包裝函式元素才能讓編輯器運作，並定義其要套用的版面和樣式。 若要觸發此行為，需使用 `decoration=true` 選項。

`one.html: <sly data-sly-resource="${'child' @ decoration=true}"></sly>`

`two.html: Hello World!`

產生的輸出於 `/content/test.html`：

**`<article class="component-two">Hello World!</article>`**

#### 使用案例3：自訂行為 {#use-case-custom-behavior}

複雜案例不限數量，透過HTL明確提供以下內容的可能性，即可輕鬆做到：

* **`decorationTagName='ELEMENT_NAME'`** 定義包裝函式的元素名稱。
* **`cssClassName='CLASS_NAME'`** 定義要在其中設定的CSS類別名稱。

`one.html: <sly data-sly-resource="${'child' @ decorationTagName='aside', cssClassName='child'}"></sly>`

`two.html: Hello World!`

產生的輸出 `/content/test.html`：

**`<aside class="child">Hello World!</aside>`**
